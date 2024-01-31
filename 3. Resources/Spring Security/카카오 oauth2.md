```
2024-01-30T18:26:58.752Z DEBUG 1 --- [nio-8080-exec-8] o.s.web.client.RestTemplate              : HTTP POST https://kauth.kakao.com/oauth/token

2024-01-30T18:26:58.752Z DEBUG 1 --- [nio-8080-exec-8] o.s.web.client.RestTemplate              : Accept=[application/json, application/*+json]

2024-01-30T18:26:58.752Z DEBUG 1 --- [nio-8080-exec-8] o.s.web.client.RestTemplate              : Writing [{grant_type=[authorization_code], code=[5lFZLTvX7vaVCZ-wKv-t_4Oe91W1Vvn534y-lnyjEePFrwMCXKqC02_aLdIKPXUZAAABjVuf2CjE017PSiBv1Q], redirect_uri=[https://daldal.karmapol.link/oauth2/callback/kakao], client_id=[a6bf5da73daa49afc402150a5a56ccc4], client_secret=[Ztw0tJsCsH25gltqJgmYdaWcSc0RzGdN]}] as "application/x-www-form-urlencoded;charset=UTF-8"

2024-01-30T18:26:58.752Z TRACE 1 --- [nio-8080-exec-8] s.n.www.protocol.http.HttpURLConnection  : ProxySelector Request for https://kauth.kakao.com/oauth/token

2024-01-30T18:26:58.753Z TRACE 1 --- [nio-8080-exec-8] s.n.www.protocol.http.HttpURLConnection  : Looking for HttpClient for URL https://kauth.kakao.com/oauth/token and proxy value of DIRECT

2024-01-30T18:26:58.753Z TRACE 1 --- [nio-8080-exec-8] s.n.www.protocol.http.HttpURLConnection  : Creating new HttpsClient with url:https://kauth.kakao.com/oauth/token and proxy:DIRECT with connect timeout:-1

2024-01-30T18:26:59.741Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639219741; nextExpiration=1706639219007; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:00.742Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639220742; nextExpiration=1706639220741; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:01.743Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639221743; nextExpiration=1706639221742; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:02.745Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639222745; nextExpiration=1706639222743; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:03.745Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639223745; nextExpiration=1706639223745; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:04.746Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639224746; nextExpiration=1706639224745; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:04.878Z DEBUG 1 --- [l-1 housekeeper] com.zaxxer.hikari.pool.HikariPool        : HikariPool-1 - Pool stats (total=10, active=0, idle=10, waiting=0)

2024-01-30T18:27:04.878Z DEBUG 1 --- [l-1 housekeeper] com.zaxxer.hikari.pool.HikariPool        : HikariPool-1 - Fill pool skipped, pool has sufficient level or currently being filled (queueDepth=0).

2024-01-30T18:27:05.539Z DEBUG 1 --- [alina-utility-1] o.apache.catalina.session.ManagerBase    : Start expire sessions StandardManager at 1706639225539 sessioncount 0

2024-01-30T18:27:05.539Z DEBUG 1 --- [alina-utility-1] o.apache.catalina.session.ManagerBase    : End expire sessions StandardManager processingTime 0 expired sessions: 0

2024-01-30T18:27:05.748Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639225747; nextExpiration=1706639225746; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:06.749Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639226749; nextExpiration=1706639226747; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:07.750Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639227750; nextExpiration=1706639227749; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:08.751Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639228751; nextExpiration=1706639228750; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:09.753Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639229753; nextExpiration=1706639229751; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:10.753Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639230753; nextExpiration=1706639230753; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:10.766Z DEBUG 1 --- [nnection-reaper] h.i.c.PoolingHttpClientConnectionManager : Closing connections idle longer than 60000 MILLISECONDS

2024-01-30T18:27:11.754Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639231754; nextExpiration=1706639231753; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:12.755Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639232755; nextExpiration=1706639232754; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:13.757Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639233756; nextExpiration=1706639233755; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:14.757Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639234757; nextExpiration=1706639234756; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:15.758Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639235758; nextExpiration=1706639235757; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:16.759Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639236759; nextExpiration=1706639236758; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:17.761Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639237761; nextExpiration=1706639237759; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:18.761Z DEBUG 1 --- [nio-8080-Poller] org.apache.tomcat.util.net.NioEndpoint   : timeout completed: keys processed=1; now=1706639238761; nextExpiration=1706639238761; keyCount=0; hasEvents=false; eval=false

2024-01-30T18:27:18.763Z TRACE 1 --- [nio-8080-exec-8] o.s.s.authentication.ProviderManager     : Authenticating request with OidcAuthorizationCodeAuthenticationProvider (2/2)

2024-01-30T18:27:18.763Z DEBUG 1 --- [nio-8080-exec-8] .s.a.DefaultAuthenticationEventPublisher : No event was found for the exception org.springframework.security.oauth2.core.OAuth2AuthenticationException

2024-01-30T18:27:18.763Z TRACE 1 --- [nio-8080-exec-8] .s.o.c.w.OAuth2LoginAuthenticationFilter : Failed to process authentication request



ngframework.security.oauth2.core.OAuth2AuthenticationException: [invalid_token_response] An error occurred while attempting to retrieve the OAuth 2.0 Access Token Response: I/O error on POST request for "https://kauth.kakao.com/oauth/token": kauth.kakao.com

	at org.springframework.security.oauth2.client.authentication.OAuth2LoginAuthenticationProvider.authenticate(OAuth2LoginAuthenticationProvider.java:113) ~[spring-security-oauth2-client-6.0.2.jar!/:6.0.2]

	at org.springframework.security.authentication.ProviderManager.authenticate(ProviderManager.java:182) ~[spring-security-core-6.0.2.jar!/:6.0.2]

	at org.springframework.security.oauth2.client.web.OAuth2LoginAuthenticationFilter.attemptAuthentication(OAuth2LoginAuthenticationFilter.java:195) ~[spring-security-oauth2-client-6.0.2.jar!/:6.0.2]

	at org.springframework.security.web.authentication.AbstractAuthenticationProcessingFilter.doFilter(AbstractAuthenticationProcessingFilter.java:231) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.security.web.authentication.AbstractAuthenticationProcessingFilter.doFilter(AbstractAuthenticationProcessingFilter.java:221) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.security.oauth2.client.web.OAuth2AuthorizationRequestRedirectFilter.doFilterInternal(OAuth2AuthorizationRequestRedirectFilter.java:181) ~[spring-security-oauth2-client-6.0.2.jar!/:6.0.2]

	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at com.mm.coresecurity.jwt.JwtAuthenticationFilter.doFilterInternal(JwtAuthenticationFilter.java:45) ~[core-security-plain.jar!/:na]

	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.security.web.header.HeaderWriterFilter.doHeadersAfter(HeaderWriterFilter.java:90) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.security.web.header.HeaderWriterFilter.doFilterInternal(HeaderWriterFilter.java:75) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.security.web.context.SecurityContextHolderFilter.doFilter(SecurityContextHolderFilter.java:82) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.security.web.context.SecurityContextHolderFilter.doFilter(SecurityContextHolderFilter.java:69) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.security.web.context.request.async.WebAsyncManagerIntegrationFilter.doFilterInternal(WebAsyncManagerIntegrationFilter.java:62) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.security.web.session.DisableEncodeUrlFilter.doFilterInternal(DisableEncodeUrlFilter.java:42) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.security.web.FilterChainProxy.doFilterInternal(FilterChainProxy.java:233) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.security.web.FilterChainProxy.doFilter(FilterChainProxy.java:191) ~[spring-security-web-6.0.2.jar!/:6.0.2]

	at org.springframework.web.filter.DelegatingFilterProxy.invokeDelegate(DelegatingFilterProxy.java:352) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.web.filter.DelegatingFilterProxy.doFilter(DelegatingFilterProxy.java:268) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:185) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.springframework.web.filter.RequestContextFilter.doFilterInternal(RequestContextFilter.java:100) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:185) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.springframework.web.filter.FormContentFilter.doFilterInternal(FormContentFilter.java:93) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:185) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.springframework.session.web.http.SessionRepositoryFilter.doFilterInternal(SessionRepositoryFilter.java:143) ~[spring-session-core-3.0.0.jar!/:3.0.0]

	at org.springframework.session.web.http.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:82) ~[spring-session-core-3.0.0.jar!/:3.0.0]

	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:185) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at io.sentry.spring.jakarta.tracing.SentryTracingFilter.doFilterWithTransaction(SentryTracingFilter.java:107) ~[sentry-spring-jakarta-7.1.0.jar!/:na]

	at io.sentry.spring.jakarta.tracing.SentryTracingFilter.doFilterInternal(SentryTracingFilter.java:87) ~[sentry-spring-jakarta-7.1.0.jar!/:na]

	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:185) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:201) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:185) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at io.sentry.spring.jakarta.SentrySpringFilter.doFilterInternal(SentrySpringFilter.java:71) ~[sentry-spring-jakarta-7.1.0.jar!/:na]

	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:185) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:177) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:97) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:542) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:119) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:92) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:78) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:357) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.coyote.http11.Http11Processor.service(Http11Processor.java:400) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.coyote.AbstractProcessorLight.process(AbstractProcessorLight.java:65) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.coyote.AbstractProtocol$ConnectionHandler.process(AbstractProtocol.java:859) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1734) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.tomcat.util.net.SocketProcessorBase.run(SocketProcessorBase.java:52) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.tomcat.util.threads.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1191) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.tomcat.util.threads.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:659) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61) ~[tomcat-embed-core-10.1.5.jar!/:na]

	at java.base/java.lang.Thread.run(Thread.java:833) ~[na:na]

Caused by: org.springframework.security.oauth2.core.OAuth2AuthorizationException: [invalid_token_response] An error occurred while attempting to retrieve the OAuth 2.0 Access Token Response: I/O error on POST request for "https://kauth.kakao.com/oauth/token": kauth.kakao.com

	at org.springframework.security.oauth2.client.endpoint.DefaultAuthorizationCodeTokenResponseClient.getResponse(DefaultAuthorizationCodeTokenResponseClient.java:95) ~[spring-security-oauth2-client-6.0.2.jar!/:6.0.2]

	at org.springframework.security.oauth2.client.endpoint.DefaultAuthorizationCodeTokenResponseClient.getTokenResponse(DefaultAuthorizationCodeTokenResponseClient.java:77) ~[spring-security-oauth2-client-6.0.2.jar!/:6.0.2]

	at org.springframework.security.oauth2.client.endpoint.DefaultAuthorizationCodeTokenResponseClient.getTokenResponse(DefaultAuthorizationCodeTokenResponseClient.java:56) ~[spring-security-oauth2-client-6.0.2.jar!/:6.0.2]

	at org.springframework.security.oauth2.client.authentication.OAuth2AuthorizationCodeAuthenticationProvider.authenticate(OAuth2AuthorizationCodeAuthenticationProvider.java:85) ~[spring-security-oauth2-client-6.0.2.jar!/:6.0.2]

	at org.springframework.security.oauth2.client.authentication.OAuth2LoginAuthenticationProvider.authenticate(OAuth2LoginAuthenticationProvider.java:107) ~[spring-security-oauth2-client-6.0.2.jar!/:6.0.2]

	... 71 common frames omitted

Caused by: org.springframework.web.client.ResourceAccessException: I/O error on POST request for "https://kauth.kakao.com/oauth/token": kauth.kakao.com

	at org.springframework.web.client.RestTemplate.createResourceAccessException(RestTemplate.java:888) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.web.client.RestTemplate.doExecute(RestTemplate.java:868) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.web.client.RestTemplate.exchange(RestTemplate.java:704) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.security.oauth2.client.endpoint.DefaultAuthorizationCodeTokenResponseClient.getResponse(DefaultAuthorizationCodeTokenResponseClient.java:88) ~[spring-security-oauth2-client-6.0.2.jar!/:6.0.2]

	... 75 common frames omitted

Caused by: java.net.UnknownHostException: kauth.kakao.com

	at java.base/sun.nio.ch.NioSocketImpl.connect(NioSocketImpl.java:567) ~[na:na]

	at java.base/java.net.SocksSocketImpl.connect(SocksSocketImpl.java:327) ~[na:na]

	at java.base/java.net.Socket.connect(Socket.java:633) ~[na:na]

	at java.base/sun.security.ssl.SSLSocketImpl.connect(SSLSocketImpl.java:299) ~[na:na]

	at java.base/sun.security.ssl.BaseSSLSocketImpl.connect(BaseSSLSocketImpl.java:174) ~[na:na]

	at java.base/sun.net.NetworkClient.doConnect(NetworkClient.java:183) ~[na:na]

	at java.base/sun.net.www.http.HttpClient.openServer(HttpClient.java:498) ~[na:na]

	at java.base/sun.net.www.http.HttpClient.openServer(HttpClient.java:603) ~[na:na]

	at java.base/sun.net.www.protocol.https.HttpsClient.<init>(HttpsClient.java:266) ~[na:na]

	at java.base/sun.net.www.protocol.https.HttpsClient.New(HttpsClient.java:380) ~[na:na]

	at java.base/sun.net.www.protocol.https.AbstractDelegateHttpsURLConnection.getNewHttpClient(AbstractDelegateHttpsURLConnection.java:189) ~[na:na]

	at java.base/sun.net.www.protocol.http.HttpURLConnection.plainConnect0(HttpURLConnection.java:1242) ~[na:na]

	at java.base/sun.net.www.protocol.http.HttpURLConnection.plainConnect(HttpURLConnection.java:1128) ~[na:na]

	at java.base/sun.net.www.protocol.https.AbstractDelegateHttpsURLConnection.connect(AbstractDelegateHttpsURLConnection.java:175) ~[na:na]

	at java.base/sun.net.www.protocol.https.HttpsURLConnectionImpl.connect(HttpsURLConnectionImpl.java:142) ~[na:na]

	at org.springframework.http.client.SimpleBufferingClientHttpRequest.executeInternal(SimpleBufferingClientHttpRequest.java:75) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.http.client.AbstractBufferingClientHttpRequest.executeInternal(AbstractBufferingClientHttpRequest.java:48) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.http.client.AbstractClientHttpRequest.execute(AbstractClientHttpRequest.java:66) ~[spring-web-6.0.6.jar!/:6.0.6]

	at org.springframework.web.client.RestTemplate.doExecute(RestTemplate.java:862) ~[spring-web-6.0.6.jar!/:6.0.6]

	... 77 common frames omitted
```

ngframework.security.oauth2.core.OAuth2AuthenticationException: [invalid_token_response] An error occurred while attempting to retrieve the OAuth 2.0 Access Token Response: I/O error on POST request for "https://kauth.kakao.com/oauth/token": kauth.kakao.com