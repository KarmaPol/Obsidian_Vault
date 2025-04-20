[[프로세스와 스레드]]
[망나니개발자 completableFuture](https://mangkyu.tistory.com/263)

# 특징
- 외부에서 완료시킬수 있음 (몇초 이내에 응답이 없으면 기본값 반환 콜백)
# 비동기 작업
### runAsync
```java
Completable.runAsync(() -> {
	Thread.currentThread().getName();
})
```
- 반환값이 없음
### supplyAsync
```java
Completable<String> future = Completable.runAsync(() -> {
	return Thread.currentThread().getName();
})
future.get();
```
- 반환값 존재. 비동기 결과 반환값 받기 가능
# 커스텀 스레드 풀 생성 VS 기본풀 사용
| **상황**               | **권장 선택**                                     |
| -------------------- | --------------------------------------------- |
| 단순 비동기 작업, 블로킹 없는 계산 | ForkJoinPool.commonPool()                     |
| 복잡한 작업, 자원 격리 필요     | 직접 풀 생성 (new ForkJoinPool(), ExecutorService) |
| 블로킹 I/O 작업 포함        | Executors.newCachedThreadPool() 같은 커스텀 풀      |
| 외부 라이브러리/다수 사용자 환경   | 직접 풀 생성하여 공유 풀과 격리                            |
- 상황에 따라 커스텀 스레드 풀을 CompletableFuture 변수로 등록
# 작업 콜백
### thenApply
```java
Completable<String> future = Completable.runAsync(() -> {
	return Thread.currentThread().getName();
}).thenApply( s-> {
    return s.upperCase();
})
```
- 반환 값을 받아 다른 값 반환
- 함수형 인터페이스 Function을 파라미터
### thenAccept
```java
Completable<Void> future = Completable.runAsync(() -> {
	return Thread.currentThread().getName();
}).thenAccept( s-> {
    System.out.println(s.toUpperCase());
})
```
- 반환값을 받아 다른 값 반환 X
- Consumer
### thenRun
```java
Completable<Void> future = Completable.runAsync(() -> {
	return Thread.currentThread().getName();
}).thenRun(() -> {
    System.out.println(s.toUpperCase());
})
```
- 반환값 받지않고 다음 작업 실행
- Runnable
# 작업 조합
```java
void thenCompose() throws ExecutionException, InterruptedException {
    CompletableFuture<String> hello = CompletableFuture.supplyAsync(() -> {
        return "Hello";
    });

    CompletableFuture<String> future = hello.thenCompose(this::mangKyu);
    System.out.println(future.get());
}

private CompletableFuture<String> mangKyu(String message) {
    return CompletableFuture.supplyAsync(() -> {
        return message + " " + "MangKyu"; // 이어서 실행
    });
}
```
- thenCompose
  두 작업 이어서 실행, 앞의 결과 사용가능
- thenCombine
  두 작업 완료 후 콜백 실행
- allOf
  모든 작업 동시 실행, 콜백 모두 실행
- anyOf
  여러 작업 중 가장 빠른 작업의 콜백 실행
# 예외 처리
- execptionally
  에러를 받아 예외 처리. Function
- handle, handleAsync
  결과값, 에러를 받아 정상/에러 모두 처리. BiFunction
```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
        if (doThrow) {
            throw new IllegalArgumentException("Invalid Argument");
        }

        return "Thread: " + Thread.currentThread().getName();
    }).handle((result, e) -> { // 동시에 처리
        return e == null
                ? result
                : e.getMessage();
    });
```
# get() VS join()
- get은 checked exception 던짐. try-catch 처리 필요
  -> 엄격히 예외처리할때 유용
- join은 unchecked exception
  -> stream에 유용
  -> 단, 예외를 무시하라는 뜻이 아님! exeptionally나 handle로 처리 필요