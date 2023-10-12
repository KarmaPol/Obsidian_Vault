### 의존성 관리
인터페이스를 사용함으로써 **컴파일 의존에서 런타임 의존**으로 변경, 결합도 낮출 수 있음
### IOC
제어의 역전
저의존(서비스) - 고의존(리포지토리) -> 결합도 높아지고, oop 설계 위반
저의존(서비스) - 저의존(인터페이스) - 고의존(리포지토리) -> 중간에 인터페이스를 둠으로써 제어 역전 
Context 클래스를 생성해 인스턴스를 리턴해준다 -> 외부에서 주입받아 **런타임 의존 해결가능**
## DDD
[[도메인 주도 설계]]
## IOC Container
객체들의 생성과 파괴 담당
의존관계를 맺어주고 관리
스프링에서는 ApplicationContext
ApplicationContext는 BeanFactory 상속 - AOP, Event Publication 등 추가
스프링부트에서는 @Configuration 애노테이션으로 Context 설정
### Dependency Injection
IOC를 구현하는 패턴 중 하나 (전략 패턴, 서비스 로케이터 패턴, 팩토리 패턴)
그 중 스프링에서는 생성자나 세터 등을 통해 객체를 주입 받아 구현