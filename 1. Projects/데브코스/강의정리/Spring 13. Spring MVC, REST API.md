## 타임리프

#### 반복문 예시
```html
<tr th:each="customer: ${customers}" th:object="${customer}" >
  <td th:text="${customer.customerId}"></td>
  <td th:text="*{name}"></td>
  <td th:text="*{email}"></td>
  <td th:text="*{createdAt}"></td>
  <td th:text="*{lastLoginAt}"></td>
</tr>
```
#### Form 예시
```html
<form th:action="@{/customers/new}" method="post">
  <div class="mb-3">
    <label for="exampleInputEmail1" class="form-label">Email address</label>
    <input type="email" name="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
  </div>
  <div class="mb-3">
    <label for="exampleInputPassword1" class="form-label">Name</label>
    <input type="text" name="name" class="form-control" id="exampleInputPassword1">
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>
</form>
```
## WebApplicationContext
ServletContext 생성 시 ApplicationContext도 생성
Controller 계층은 ServletApplicationContext
서비스 계층, 데이터 엑세스 계층은 RootApplicationContext로 분리
-> 서비스에 따라 ApplicationContext를 여러개로 분리할 수 있다
-> 최근에는 코드 자체를 분리하는 MSA

https://jaehun2841.github.io/2018/10/21/2018-10-21-spring-context/#Web-Application-Context

```java
@Configuration
@EnableWebMvc
@ComponentScan(basePackages = "org.prgrms.kdt.customer",
includeFilters = @ComponentScan.Filter(type = FilterType.ASSIGNABLE_TYPE, value = CustomerController.class), useDefaultFilters = false)
static class ServletConfig implements WebMvcConfigurer, ApplicationContextAware {...}

@Configuration
@ComponentScan(basePackages = "org.prgrms.kdt.customer",
excludeFilters = @ComponentScan.Filter(type = FilterType.ASSIGNABLE_TYPE, value = CustomerController.class))
@EnableTransactionManagement
static class RootConfig {...}

@Override
  public void onStartup(ServletContext servletContext) {
    logger.info("Staring Server...");
    var rootApplicationContext = new AnnotationConfigWebApplicationContext();
    rootApplicationContext.register(RootConfig.class);
    var loaderListener = new ContextLoaderListener(rootApplicationContext);
    servletContext.addListener(loaderListener);

    var applicationContext = new AnnotationConfigWebApplicationContext();
    applicationContext.register(ServletConfig.class);
    var dispatcherServlet = new DispatcherServlet(applicationContext);
    var servletRegistration = servletContext.addServlet("test", dispatcherServlet);
    servletRegistration.addMapping("/");
    servletRegistration.setLoadOnStartup(1); 
    // -1이 기본값, api 요청이 오면 로드, 1은 서버 시작시 로드
  }
```
WebApplicationInitializer을 구현하여 ServletConfig, WebApplicationConfig을 각각 생성해
Context를 따로 생성해 줄 수 있다
## REST API
- REST 네트워크 아키텍처 원리의 모음
- HTTP 통신을 SOAP이나 쿠키를 통한 세션 트래킹 같은 별도 전송 계층 없이 가능하게 한다
=> REST 아키텍처 스타일을 따르는 API
### REST 아키텍처 스타일
- **클라이언트 - 서버**
- **Stateless**
- **캐시**
- **균일한 인터페이스**
  URI로 지정한 리소스에 대한 조작을 통일되고 한정된 인터페이스로 수행
- **계층화된 시스템**
  유연하게 보안, 로드 밸런싱, 암호화 계층 혹은 PROXY, 게이트웨이 계층을 추가 가능
### HATEOAS
Hypermedia as the Engine of Application State
리소스를 받으면, 할 수 있는 행위까지 제공
```json
HTTP/1.1 200 OK

{
    "account": {
        "account_number": 12345,
        "balance": {
            "currency": "usd",
            "value": 100.00
        },
        "links": {
            "deposits": "/accounts/12345/deposits",
            "withdrawals": "/accounts/12345/withdrawals",
            "transfers": "/accounts/12345/transfers",
            "close-requests": "/accounts/12345/close-requests"
        }
    }
}
```
Hateoas까지 만족해야 진정한 REST API -> 하지만 잘 사용하지 않는다
### API 설계
1. URI는 정보의 자원 표기 (동사 보다 명사)
2. 자원에 대한 행위는 HTTP Method로 
   POST /task/1/run (O)
   POST /task/run/1 (X)
3. /는 계층 관계 표현
4. 마지막 문자로 /포함 X
5. 하이픈은 URI 가독성 높이는데 사용
### HTTP 메시지 컨버터
Dispatcher Servlet -> 핸들러 어댑터 -> Argument Resolver - **HTTP 메시지 컨버터** -> 컨트롤러
