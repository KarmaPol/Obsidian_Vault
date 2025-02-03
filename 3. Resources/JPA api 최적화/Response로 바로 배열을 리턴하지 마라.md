```java
@Data  
@AllArgsConstructor  
static class Result<T> {  
	private int count;  
	private T data;  
}
```
- 배열을 response로 바로 리턴하면, 유연하게 처리하기가 어려워짐