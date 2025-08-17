- 동적 제어변수 전달 목적
- 잡 파라미터는 메타데이터 저장소에 저장됨
## 잡파라미터 전달 방법
```bash
./gradlew bootRun --args='--spring.batch.job.name=dataProcessingJob inputFilePath=/data/input/users.csv,java.lang.String'
```
### 기본 표기법
parmeterName = paramatervalue, parameterType(명시하지 않으면 String), identificationFlag(식별자 여부, 기본 true)

# DefaultJobParametersConverter
- 커맨드라인으로 전달된 잡 파라미터를 적절한 타입으로 변환
- Integer, Boolean, LocalDate, LocalDateTime 등
- Spring Batch 5 이전엔 String, Long, Double, Date만

# @StepScope
- @Value로 잡 파라미터 주입 받기위해 필수적
# LocalDateTime 시간 전달
- ISO_LOCAL_DATE_TIME 형식
- 2024-01-01T14:30:00
# 잡 파라미터에 쉼표가 있을때
```bash
infiltrationTargets='{"value": "판교_서버실,안산_데이터센터", "type": "java.lang.String"}'
```
- JSON 표기법 지원
# 잡파라미터 전달 과정
- **JobLauncherApplicationRunner**
1. 잡 목록 준비
2. 유효성 검증 (빈 등록 실패시 - IllegalArgumentException: No job found with name 'noSuchJob')
3. 명령어 변환, JobParameter (DefaultJobParametersConverter)
4. 잡 실행 (this.jobLauncher.run(job, parameters);)
# 잡 파라미터 검증
## **JobParametersValidator**
```java
@Component public class SystemDestructionValidator implements JobParametersValidator { @Override public void validate(@Nullable JobParameters parameters) throws JobParametersInvalidException { 
	if (parameters == null) { throw new JobParametersInvalidException("파라미터가 NULL입니다"); } 
	
	Long destructionPower = parameters.getLong("destructionPower"); 
	if (destructionPower == null) { 
		throw new JobParametersInvalidException("destructionPower 파라미터는 필수값입니다"); } 
	if (destructionPower > 9) { 
		throw new JobParametersInvalidException( "파괴력 수준이 허용치를 초과했습니다: " + destructionPower + " (최대 허용치: 9)"); 
	} 
} }

@Bean public Job systemDestructionJob( JobRepository jobRepository, Step systemDestructionStep, SystemDestructionValidator validator) {
	return new JobBuilder("systemDestructionJob", jobRepository)
		.validator(validator) 
		.start(systemDestructionStep) 
		.build(); 
}
```
- JobParmaterValidator로 커스텀
- JobBuilder에 주입
### 디폴트 밸리데이터
```java
@Bean public Job systemDestructionJob( JobRepository jobRepository, Step systemDestructionStep ) { 
	return new JobBuilder("systemDestructionJob", jobRepository) .validator(new DefaultJobParametersValidator( 
	new String[]{"destructionPower"}, // 필수 파라미터 배열
	new String[]{"targetSystem"} // 선택적 파라미터 배열 
	)).start(systemDestructionStep).build(); 
}
```
- 간단하게 DefaultJobParametersValidator로 있는지 validate
# @JobScope, @StepScope
- 잡 실행 시 빈 생성 (레이지)
- **병렬 처리에 용이**
## 잡스코프 사용 주의사항
1. 프록시 객체이므로 상속가능해야함, final X
2. **Step엔 스텝스코프 X, 잡스코프는 지양**
	1. 하지만 컴파일시점에 없는 잡 파라미터를 위해 필수적임
	2. **따라서 필요할 경우 Tasklet으로 잡스코프, Step에 이 Tasklet 주입**
# ExecutionContext
- 잡 혹은 스텝 실행 도중 Key-Value 저장
```java
@Bean @JobScope public Tasklet systemDestructionTasklet( 
@Value("#{jobExecutionContext['previousSystemState']}") String prevState ) { 
	// JobExecution의 ExecutionContext에서 이전 시스템 상태를 주입받는다 
}
```
- stepExecutionContext 은 해당 스텝 내 컴포넌트끼리만 공유
- Job 재시작 컨텍스트, Step간 데이터 공유