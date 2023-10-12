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
