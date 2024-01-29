### 스웨거 응답
<br>Failed to fetch.**  <br>**Possible Reasons:**<br><br>- CORS<br>- Network Failure<br>- URL scheme must be "http" or "https" for CORS request.

### 개발자 콘솔 에러
```
Mixed Content: The page at 'https://bibum.karmapol.link/swagger-ui/index.html#/%EB%B0%A9%20API/getRoomInfo' was loaded over HTTPS, but requested an insecure resource 'http://bibum.karmapol.link/api/v1/1'. This request has been blocked; the content must be served over HTTPS.
(anonymous) @ index.js:109
```

- https 페이지에서 http 요청 시 오류가 발생한다

### 해결책
- Swagger annotaion 추가 "/" -> 기본 url
```java
@OpenAPIDefinition(  
info = @Info(title = "달달 쇼핑 백엔드 API 명세서",  
description = "달달 쇼핑 백엔드 API 명세서 입니다",  
version = "0.1"),  
servers = {  
@Server(url = "/", description = "달달 서버 url")}  
)
```
