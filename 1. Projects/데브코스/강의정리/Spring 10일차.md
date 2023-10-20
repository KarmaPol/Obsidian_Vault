## Aspect Orient Programming
관점 지향 프로그래밍
부가 기능을 코드 수정 없이 핵심 기능에 추가 가능
### 적용 방법
- 컴파일 시점
  컴파일 시점에 부가 기능 소스 코드 삽입
- 클래스 로딩 시점
  클래스 로딩 시점에 Binary화된 코드 삽입
- 런타임 시점
  Proxy를 이용해 런타임에 부가 기능 실행
### Spring AOP
스프링은 proxy를 이용
- **JDK Proxy**
  interface 기반
- **CGLib Proxy**
  class 기반
