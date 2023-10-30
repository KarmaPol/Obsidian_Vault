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
**resources/META-INF/spring.factories**의 Default 의존성 설정을 스프링 부트가 알아서 처리
등록한 Bean이 우선
https://donghyeon.dev/spring/2020/08/01/스프링부트의-AutoConfiguration의-원리-및-만들어-보기/

### 싱가포르 스타트업 생활 및 구직
가장 중요한 것은 링크드인
indeed, jobwiz, jobstreet, nodeflair
페이스북 개발자해외취업 그룹

**영어가 중요하다**