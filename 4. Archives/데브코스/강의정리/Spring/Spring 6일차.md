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

Happy flow, Edge Case 모두에 대해 테스트 코드를 작성해줘야 한다
##### @Disabled
Test 메소드에 어노테이션 달면, 실행시 무시
##### @BeforeAll
Test 실행전 메소드 한번 실행
##### @BeforeEach
매 Test 메소드 실행 전 마다 메소드 실행
##### assertAll()
입력한 모든 메소드에 대해 테스트
파라미터에 람다식으로 함수 여러개 전달
### Hamcrest 라이브러리
```java
assertThat(1+1, is(2));
assertThat(1+1, anyOf(is(2), is(1)));
assertThat(1+1, not(2));
```
Hamcrest 라이브러리의 Matcher 활용

```java
var prices = List.of(1,2,3);

// 리스트에 대한 여러 Matcher 제공
assertThat(prices, hasSize(3));
assertThat(prices, everyItem(greaterThan(1)));
assertThat(prices, containsInAnyOrder(3,2,1));
assertThat(prices, hasItem(1));
assertThat(prices, hasItem(greaterThan(2)));
```
컬렉션에 대해 여러 편리한 Matcher 제공
### Mock Object
- **상태 검증**
  메소드 수행 후, 객체의 상태를 확인 (Stub)
- **행위 검증**
  특정 동작을 수행하는지 확인 (Mock 객체)
#### Stub
```java
// given
var voucherService = new VoucherService(new MemoryVoucherRepository());
var sut = new OrderService(voucherService, new MemoryOrderRepository());

// when
var order = sut.createOrder(UUID.randomUUID(), List.of(new OrderItem(UUID.randomUUID), 200, 1));

// then
assertThat(order.totalAmount(), is(10L));
```
상태를 검증
테스트를 위한 가짜 객체 Stub을 만들어준다
#### Mock
```java
// given
var voucherServiceMock = mock(VoucherService.class);
var orderRepositoryMock = mock(OrderRepository.class);
when(voucherServiceMock.getVoucher(fixedAmountVoucher.getVoucherId())).thenReturn(fixedAmountVoucher)

var sut = new OrderService(vocherServiceMock, orderRepositoryMock);

// when
var order = sut.createOrder(UUID.randomUUID());

// then
assertThat(order.totalAmount(), is(100L));
assertThat(order.getVoucher().isEmpty(), is(false));
var inOrder = inOrder(voucherServiceMock, orderRepositoryMock); // 순서 지정
inOrder.verify(voucherServiceMock).getVoucher(fixedAmountVoucher.getVoucherId());
verify(ordeRepositoryMock).insert(order);
inOrder.verify(voucherServiceMock).useVoucher(fixedAmountVoucher);
```
mock 객체는 when()으로 기술한 행위만 작동한다
mock의 경우, 메소드 전후 상태를 검사를 넘어서 특정 메소드가 객체에서 작동하였는지 검증해야한다
### Spring의 JUnit5 지원
Spirng에서 Junit을 사용해 테스트를 할때,
**@ExtendWith(SpringExtension.class)
@ContextConfiguration** 필요
=> **@SpringJUnitConfig** 사용

- **@ActiveProfiles()**
  @ActiveProfiles("test")처럼 작성하여 프로파일 지정 가능