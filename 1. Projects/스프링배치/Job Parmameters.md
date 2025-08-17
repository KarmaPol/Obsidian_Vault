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

