[자바 callable, future](https://mangkyu.tistory.com/259)
## 기존 Thread의 문제점
- 지나치게 저수준 API
- 값 반환 불가능
- 매번 쓰레드 생성, 종료
## Callable
```java
public interface Callable<V> {
	V call() throws Exception;
}
```
- Runnable과 다르게 V 리턴 값을 받을 수 있음
## Future
```java
public interface Future<V> {

    boolean cancel(boolean mayInterruptIfRunning);

    boolean isCancelled();

    boolean isDone();

    V get() throws InterruptedException, ExecutionException;

    V get(long timeout, TimeUnit unit)
        throws InterruptedException, ExecutionException, TimeoutException;
}
```
- get
  블로킹 방식으로 결과 가져옴
  타임아웃 설정 가능
- isDone, isCancelled
  완료, 취소 여부 가져오기
- cancel
  작업 취소시키고, 취소 여부는 boolean으로 반환
## Executor
- 쓰레드를 미리 만들어두고 재사용하기 위한 쓰레드 풀 구현 인터페이스
## ExecutorService
- Callable, Runnable 등록을 위한 인터페이스
![](https://blog.kakaocdn.net/dn/bcGfch/btrGEhU3Y4W/owqnKjYucjVNZDu4TwEdZ0/img.gif)
### 라이프 사이클 관리 메소드
- shutdown()
  새로운 작업을 더이상 받아들이지 않음
  호출하지 않으면 다음 작업 무한 대기
### 비동기 작업을 위한 기능들
- submit
  실행할 작업들 추가 및 작업 상태와 결과 포함하는 Future 반환
- invokeAll
  모든 작업 반환까지 대기
- invokeAny
  아무 작업 반환 하나 대기
## Executors
- executorService를 생성해주는 고수준 팩토리 클래스
- newFixedThreadPool
- newScheduledThreadPool
- newSingleThreadExecutor

[자바 CompletableFuture](https://mangkyu.tistory.com/263)
## CompletableFuture
- Future의 단점 보완하고자 JAVA 8에서 등장
- CompletionStage 인터페이스도 implement -> 외부에서 작업 완료, 중첩 및 콜백 등록 가능
