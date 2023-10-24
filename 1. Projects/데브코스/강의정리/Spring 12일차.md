## Spring MVC
### DispatcherServlet
Front Controller Pattern으로 DispatcherServlet이 요청을 받고 어떤 컨트롤러/뷰가 필요한지 결정

사용자 요청을 기준으로 어떤 핸들러(컨트롤러)에 작업을 위임할지 결정 => **핸들러 매핑 전략**
이때 컨트롤러 타입에 맞게 파라미터를 변환 -> **Handler Adapter**
컨트롤러가 호출한 뷰를 찾아서 호출 -> **View Resolver**
