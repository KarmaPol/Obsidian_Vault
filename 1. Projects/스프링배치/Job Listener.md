- 배치의 여러 순간 관찰하고 행동 정의
1. JobExecutionListener
2. StepExecutionListener
3. ChunkListener
# Item Listener
```java
public interface ItemReadListener<T> extends StepListener {
public interface ItemProcessListener<T, S> extends StepListener {
public interface ItemWriteListener<S> extends StepListener {
```
# 리스너의 목적
- 단계별 모니터링
- 데이터 가공
- 부가 기능
# 인터페이스 구현 VS 어노테이션 구현
```java
@Component public class BigBrotherStepExecutionListener implements StepExecutionListener { 
@Override
// method

@Component public class ServerRackControlListener { 
@BeforeStep
// method

@Bean 
public Step serverRackControlStep(Tasklet destructiveTasklet) {
	return new StepBuilder("serverRackControlStep", jobRepository)
		.tasklet(destructiveTasklet(), transactionManager)
		.listener(newServerRackControlListener()) // 빌더의 listener() 메서드에 전달 
		.build(); 
}
```
1. 인터페이스 구현 후 오버라이드
2. 어노테이션 기반
   AfterStep일땐 ExitStatus 반환 필수
# 왜 JobParameters를 그대로 전달하지 않을까?
- 배치에서 JobParameters는 불변값
	-  **재현 가능성(Repeatability)과 일관성(Consistency)**
- Job 실행 중 동적 생성, 변경되는 값은 ExecutionContext
## ExecutionContext 유의점
- LocalDate.now()로 Context 생성 X
- 원하는 날의 데이터 다시 처리가 어려워짐
- 이때는 JobParameter로 주입이 나음
# Step -> Job ExcutionContext 전달시
- 매번 변환하지말고
- **ExecutionContextPromotionListener** 사용하자
- afterStep 오버라이드
# 리스너 예외처리
- 직접 catch로 잡아서 처리해줘도 됨
- BeforeJob, BeforeStep에서 예외 터지면 Job 실패 처리
- AfterJob, AfterStep에서 예외 터지면 무시
- **리스너는 감시, 모니터링와 통제만(보조)! 비즈니스 로직은 X**
# 리스너 성능 고려
- JobExecutionListener/StepExecutionListener
  는 잡 당 1번이므로 성능에 영향 없음
- ItemReadListener/ItemProcessListener
	- **아이템당 1회이므로 장애 발생 가능**
	- 외부 API 호출은 더 위험함

- **리스너에서 API호출, DB접근, IO는 최소화!**
- **리스너는 최대한 가볍게**
