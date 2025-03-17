# Classical TDD
- 최대한 실제 객체를 사용하자
```java
class OrderInteractionTester...

  public void testOrderSendsMailIfUnfilled() {
    Order order = new Order(TALISKER, 51);
    Warehouse warehouse = new Warehouse();
    Mock mailer = mock(MailService.class);
    order.setMailer((MailService) mailer.proxy());

    mailer.expects(once()).method("send");

    order.fill(warehouse);
  }
}
```
- 외부에 의존성이 있는 MailService를 제외하고 모두 실 객체를 사용한다
# Mockist TDD
- SUT 외의 검증하고 싶은 메서드가 있는 모든 객체를 Mock하자
```java
class OrderInteractionTester...

  public void testOrderSendsMailIfUnfilled() {
    Order order = new Order(TALISKER, 51);
    Mock warehouse = mock(Warehouse.class);
    Mock mailer = mock(MailService.class);
    order.setMailer((MailService) mailer.proxy());

    mailer.expects(once()).method("send");
    warehouse.expects(once()).method("hasInventory")
      .withAnyArguments()
      .will(returnValue(false));

    order.fill((Warehouse) warehouse.proxy());
  }
}
```
## 어떤 것을 선택할까?
- 클래식 TDD라면 어색한 연동에 테스트 더블 중 어떤 걸 사용해도 문제가 되지 않는다.
  즉 Mock을 써도 문제가 아니다
- Mockist라면 당연히 Mock으로 행동 검증을 한다

- 클래식 TDD라고 무조건 상태 검증을 하는 것이 아니다. 이것은 선택할 TradeOff이다
- **하지만 대부분의 어색한 연동에서 Mock과 행동 검증이 유리하다**
  (예를 들어 캐시 히트 검증.)

[[TDD]]