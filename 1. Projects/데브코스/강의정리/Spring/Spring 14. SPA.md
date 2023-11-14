## SPA
단일 페이지 웹 어플리케이션
다이나믹 렌더링을 브라우저에서 처리
URL 변경 시 DOM 조작을 통해 특정 영역만 렌더링
라우팅을 프론트엔드에서 처리
### CORS
#### SOP 정책
사용자를 악의적인 공격으로부터 보호하기 위해
동일한 출처의 요청만 허용하는 정책
#### CORS 동작
client가 server에 option 메소드로 origin을 예비 요청
서버에서 허용 시 본 요청
#### CORS 에러
Client와 Server측 Origin이 달라서 발생
#### 설정
WebConfigurer의 구현체에서 addCoursMappings()를 overrride
```java
@Overrride
public void addCorsMappings(CorsRegistry registry) {
	registry.addMapping("/api/**")
	.allowedMethods("POST", "GET")
	.allowedOrigins("**");
}
```