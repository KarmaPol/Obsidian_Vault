https://velog.io/@appti/ResponseEntityExceptionHandler%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%B4%EC%95%BC-%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0

- `@ControllerAdvice, @RestControllerAdvice`만을 사용할 경우 `Spring MVC Exception`을 모두 처리하지 못할 수 있습니다.
    - 이 경우 사실상 하나의 클래스에서 전역적인 예외 처리가 불가능합니다.
    - 모든 `Spring MVC Exception`을 수작업으로 처리할 수도 있지만, 매우 번거롭습니다.
- `ResponseEntityExceptionHandler`를 확장하면 `Spring MVC Exception`에 대한 최소한의 예외 처리가 가능합니다.
    - 필요한 경우 오버라이딩을 통해 예외 처리 관련 메소드를 커스터마이징 할 수 있습니다.