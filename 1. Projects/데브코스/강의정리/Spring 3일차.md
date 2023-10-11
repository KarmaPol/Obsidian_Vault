## Dependency Injenction
### Dependency Resolution Process
Application Context에 의해 Bean Injection 주입
### Circular Dependency
A->B->A 참조 시 순환 참조으로 인해 오류 발생
### 컴포넌트 스캔
스프링이 직접 클래스를 검색해서 빈으로 등록해주는 기능
StereoType 어노테이션(@Component, @Repository, @Service, @Controller, @Configuration)
으로 검색 대상 지정