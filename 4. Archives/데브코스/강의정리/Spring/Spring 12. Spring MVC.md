## Spring MVC
### DispatcherServlet
Front Controller Pattern으로 DispatcherServlet이 요청을 받고 어떤 컨트롤러/뷰가 필요한지 결정

사용자 요청을 기준으로 어떤 핸들러(컨트롤러)에 작업을 위임할지 결정 => **핸들러 매핑 전략**
이때 컨트롤러 타입에 맞게 파라미터를 변환 -> **Handler Adapter**
컨트롤러가 호출한 뷰를 찾아서 호출 -> **View Resolver**
### 리소스 핸들러
```java
@Override 
public void addResourceHandlers(ResourceHandlerRegistry registry) {
	registry.addResourceHandler("/resources/**") // 외부 노출 주소
	.addResourceLocations("/resources/") // 프로젝트 리소스 주소
	.setCachePeriod(60); // 캐시 지정 가능
}

// html 
<link href="<c:url value="/resources/myCss.css" />" rel="stylesheet">
```
스프링 부트에서는 기본적으로 **_/static, /public, /resources,_ and _/META-INF/resources_**
경로에 대해 정적 리소스 자동 탐색

https://www.baeldung.com/spring-mvc-static-resources
## 타임리프
WebMvcConfigurer의 configureViewResolvers를 Override하여
타임리프 ViewResolver 커스텀 설정 가능

https://www.baeldung.com/thymeleaf-in-spring-mvc
https://rebornbb.tistory.com/entry/StringBoot-Thymeleaf-%EB%AC%B8%EB%B2%95-%EC%A0%95%EB%A6%AC