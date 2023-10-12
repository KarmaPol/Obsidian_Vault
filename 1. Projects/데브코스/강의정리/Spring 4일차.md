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
