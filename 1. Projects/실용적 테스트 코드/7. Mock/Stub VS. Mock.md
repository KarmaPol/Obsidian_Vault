- 두 테스트 더블은 자주 혼용됨
# Stub
- 상태 검증.
- 미리 준비한 요청, 결과가 아니면 응답하지 않음
```java
class OrderStateTester...

  public void testOrderSendsMailIfUnfilled() {
    Order order = new Order(TALISKER, 51);
    MailServiceStub mailer = new MailServiceStub();
    order.setMailer(mailer);
    order.fill(warehouse);
    assertEquals(1, mailer.numberSent());
  }
```
- **보낸 Mail의 갯수가 1인가?**
# Mock
- 행위 검증.
- 행위에 대한 기대를 명시하고 그에 따라 동작
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
- **Mail Send를 1번 실행했는가?**

[[Classical Vs. Mockist Testing]]