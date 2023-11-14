## WEB 기술
- Web
  인터넷을 이용해 정보를 공유할 수 있는 공간
#### 웹 구성요소
- HTTP - 무엇
- URI - 어디서
- HTML - 어떻게
### 웹 서버
http, https 프로토콜을 지원하는 서버
정적 리소스(html, image)를 지원
프록시 기능
### WAS
비즈니스 로직을 처리해서 동적 컨텐츠를 제공하는 서버
Web Server - Web Container(Servlet)로 구성
## 서블릿
웹 요청과 응답을 처리하는 Java 서버 기술
```java
@WebServlet(value ="/*", loadOnStartup = 1) 
// loadOnStartup = 1이면 시작 시 로드, -1면 호출 시 로드(디폴트)
public class TestServlet extends HttpServlet {

	@Overrride
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOExceeption{
		var uri = req.RequestURI();
		resp.getWriter().write(uri);
	}
}
```
HttpServlet을 상속받아 서블릿 객체 사용가능
web.xml에 서블릿 설정 파일을 작성하는 대신, @WebServlet 어노테이션으로 선언 가능
- WebApplicationIntializer
  어노테이션 만으로 설정이 부족할 때
  WebApplicationInitializer을 구현한다
```java
public KdtInitializer implements WebApplicaitonInitializer {
	@Override
	public void onStartUp(ServletContext servletContext){
		var registration = servletContext.addServlet("test", new TestServlet());
		registration.addMapping("/*");
	}
}
```