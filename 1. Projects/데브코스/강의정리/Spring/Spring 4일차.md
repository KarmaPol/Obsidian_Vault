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
@PropertySource를 사용하는 대신 SpringBoot의 경우
yml파일을 지원하는 @ConfigurationProperties 어노테이션을 지원한다
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
### @EnableConfigurationProperties
```java
@Service
@EnableConfigurationProperties(OrderProperties.class)
public class MyService {

    private final OrderProperties orderProperties;

    public MyService(OrderProperties orderProperties) {
        this.OrderProperties = orderProperties;
    }

    public String message() {
        return this.orderProperties.getMessage();
    }
}
```
@EnableConfigurationProperties 어노테이션으로 
@ConfigurationProperties 클래스를 빈으로 등록할 수 있다

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
Application Context의 Environment를 참조해 profile을 설정하거나 조회 가능하다
@Qualifier를 사용하는 대신 @Profile로 프로파일별로 빈 설정 가능

[[스프링부트 yml profiles group]]

```java
SpringApplication.setAdditionalProfiles("local")
```
코드로도 직접 프로파일 설정 가능
## 리소스
이미지 파일, 텍스트 파일, 키파일 등 외부 리소스를 읽을 필요가 있을 수 있음
스프링에서 **Resource, ResourceLoader** 제공 -> 구현체까지 알 필요 없다
```java
var ymlResource = applicationContext.getResource("application.yml");
// classpath: 와 같이 경로 schema 입력 가능
var textResource = applicationContext.getResource("classpath:test/sample.txt");

// url에서 다운로드
var urlResource = applicationContext.getResource("www.google.com");
var readableByteChannel = Channels.newChannel(urlResource.getURL().openStream());
var bufferedReader = new BufferedReader(Channels.newReader(readableByteChannel, StandardCharsets.UTF_8));
var contents = bufferedReader.lines.collect(Collectors.joining("\n"));
```
[URL에서 HTML 파일 다운로드](https://jaime-note.tistory.com/35)

