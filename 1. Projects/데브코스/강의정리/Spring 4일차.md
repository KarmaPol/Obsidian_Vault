## Environment
ApplicationContext에서 제공
### Properties
프로젝트 속성 관리
properties 파일이나 OS 환경변수 등으로 관리
```java
@Configuration
@PropertySource("application.properties")
public class Appconfiguration {}
```
@PropertySource 어노테이션으로 어떤 properties 파일 사용할지 명시 가능

```java
@Component
public class OrderProperties{
	@Value("${kdt.version}")
	private String version;

	// default 값을 설정할 수 있다
	@Value("${kdt.minimum-order-amount:0}")
	private int minimumOrderAmount;

	// 환경 변수도 가져올 수 있다
	@Value("${JAVA_HOME}")
	private int javaHome;
}
```
@Value 어노테이션으로 properties 내부 값을 가져올 수 있다
## YAML 프로퍼티 작성
Spring의 @PropertySource 어노테이션은 yml 파일을 지원하지 않는다
PropertySourceFactory를 구현해주고 @PropertySource의 factory로 넣어줘야한다
#### @ConfigurationProperties
SpringBoot의 경우, yml파일을 지원하는 @ConfigurationProperties 어노테이션을 지원한다
```java
@Configuration
@ConfigurationProperties(prefix = "kdt")
@Getter
@Setter
public class OrderProperties{
	private String version;
	private int minimumOrderAmount;
	...
}
```
SpringBoot가 자동으로 인식해 yml 파일의 값을 매칭한다
이때 getter, setter가 필요하다
[[DTO getter, setter]]
## 프로파일
```java
@Repository
@Profile({"local", "dev"}) // 프로파일은 여러개 설정 가능
public class MemoryRepository implements repository{
	...
}

...
environment.setActiveProfiles("local");
application.refresh();
```
@Qualifier 대신 @Profile로 프로파일별로 빈 설정 가능

[[스프링부트 yml profiles group]]

```java
SpringApplication.setAdditionalProfiles("local")
```
코드로도 직접 프로파일 설정 가능
## 리소스
이미지 파일, 텍스트 파일, 키파일 등 외부 리소스를 읽을 필요가 있을 수 있음

