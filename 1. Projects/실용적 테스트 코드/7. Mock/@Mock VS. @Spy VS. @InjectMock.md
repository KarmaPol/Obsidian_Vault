# Mock
- 순수 Mock() 객체 생성
  -> Mockito를 사용하면 @Mock 어노테이션으로 쉽게 생성 가능
# Spy
- @Spy 어노테이션으로 생성 가능
- **실제 객체를 특정 행동을 할때, 특정 결과를 반환하도록 설정**
- Mock이 아닌 실제 객체로 Stub가능
```java
doReturn(true)
	.when(mailSendClient)
	.sendEmail(anyString(), anyString());
```
- 하지만 Mock 객체를 많이 씀, Spy가 유용할때도 있으니 알아두자

[[Stub VS. Mock]]