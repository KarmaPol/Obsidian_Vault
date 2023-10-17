## 스프링 테스트
### 소프트웨어 테스팅
#### 테스팅 레벨
- **unit test**
  메소드나 클래스 단위 코드 테스트
- **integration test**
  컴포넌트 간 결합 테스트
- **system(E2E) test**
  시스템, 프로덕트 전체의 동작 테스트
- **acceptance test**
  인수 테스트, 고객 관점 요구사항대로 동작하는지 테스트
#### 테스팅 피라미드
**Unit test > Service test > UI test**
단위테스트를 통합테스트보다 더 많이 작성해라
## 단위 테스트 Unit Test
프로그램 기본 단위인 모듈을 테스트
가장 중요하고, 가장 많이 작성해야 한다
Given/When/Then으로 테스트 대상 코드(SUT)를 테스트
#### 단위 테스트의 목적
1. 코드의 지속적 변경에서 발생하는 오류를 테스트 코드로 검출 가능
2. 테스트 코드로 기능 명세서 역할
#### 테스트 더블
의존 구성요소를 사용할 수 없을 때 테스트 대상 코드와 상호 작용하는 객체
Stub, Mock객체 등
## 통합 테스트 Integration Test
컴포넌트 간 연결을 테스트
서비스-DB 연결
- **End to End Test**
  UI 등 시스템 전체 테스트
## JUnit
매 단위 테스트마다 테스트 클래스 인스턴스를 생성해 독립적인 테스트 가능
어노테이션을 제공해 테스트 라이프 사이클을 관리
테스트 러너를 제공해 더 쉽게 테스트 실행
assert로 테스트 결과 판독
#### JUnit5
JUnit4는 확장성이 떨어지는 문제
- **JUnit Platform**
  JVM 상에 테스팅 프레임워크 런칭을 위한 근간을 제공, testEngine을 통해 테스트 발견 및 실행, 결과 보고
- **JUnit Jupiter**
  testEngine의 구현체 포함, 개발자는 jupiter api를 사용해 테스트 코드 작성
- **JUnit Vintage**
  junit4 버전 작성 테스트 코드 실행 구현체 포함
##### @Disabled
Test 메소드에 어노테이션 달면, 실행시 무시
##### @BeforeAll
Test 실행전 메소드 한번 실행
##### @BeforeEach
매 Test 메소드 실행 전 마다 메소드 실행