## Spring Boot Auto configuration
#### Datasource 설정
스프링 configuration 파일에서 Bean으로 등록해도 되지만
스프링 부트는 application.yml 파일에서 datasource를 등록해도 된다
```yml
spring:
	datasource:
		url: jdbc:mysql:~~
		username: root
		password: root1234!
	thymeleaf:
		view-names: "view/*"
		prefix: "/WEB-INF"
```
### auto config
**@EnableAutoConfiguration** 또는 **@SpringBootApplication**
어노테이션으로 추가한 jar파일에 따라 자동적으로 설정 가능
@Enable