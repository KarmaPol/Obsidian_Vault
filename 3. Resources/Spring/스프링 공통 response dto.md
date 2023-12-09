https://velog.io/@qotndus43/스프링-API-공통-응답-포맷-개발하기

```java
@Getter  
@NoArgsConstructor(access = AccessLevel.PROTECTED)  
public class ApiResponse<T> {  
private static final String SUCCESS_STATUS = "success";  
  
private String status;  
private T data;  
  
private ApiResponse(String status, T data) {  
this.status = status;  
this.data = data;  
}  
  
public static <T> ApiResponse<T> createSuccess(T data) {  
return new ApiResponse<>(SUCCESS_STATUS, data);  
}  
  
public static ApiResponse<?> createSuccessWithNoContent() {  
return new ApiResponse<>(SUCCESS_STATUS, null);  
}  
}
```
ResponseEntity로 응답 시, 객체 하나만 리턴할 시엔 text/plain으로 날아간다
=> 모두 json 양식으로 보내게 통일한다