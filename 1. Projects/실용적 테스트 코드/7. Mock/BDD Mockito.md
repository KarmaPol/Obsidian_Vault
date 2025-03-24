```java
BDDMockito.given(mailSendClient.sendEmail(anyString()))
	.willReturn(true);
```
- Mockito Mock과 차이는 없다
- BDD 스타일에 맞게 given으로 작성할 수 있다

[[@Mock VS. @Spy VS. @InjectMock]]