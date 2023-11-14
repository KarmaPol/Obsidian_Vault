## 로깅
시스템 작동 상태의 기록과 보존, 이용자 습성 조사 및 시스템 동작의 분석을 위해 정보를 기록
버그를 수정하기 위해 필수적

println()으로 일일히 콘솔로 찍으면 저장도 어렵고, 성능에 큰 영향
### SLF4J
퍼사드 패턴으로 여러 Logging Framework들을 추상화
### 로그 레벨
1. trace
2. debug
3. info
4. warn
5. error
error 레벨로 로그레벨을 조회시 trace 레벨은 조회 X
### logback 설정
로깅 설정은 실제 라이브러리인 logback의 설정을 해줘야한다
- **logback 설정파일 찾는 순서**
1. logback-test.xml (테스트 코드 우선, test/resources)
2. 없으면 logback.groovy (main/resources)
3. 없으면 logback.xml
4. 없으면 기본 설정인 BasicConfiguration
#### appender-ref
각 logger 클래스 별로 레벨을 다르게 설정 가능
이때 각 로거의 appender-ref를 갖게 설정하면 중첩돼서 출력된다
-> appender-ref를 주지 않거나, additivity = "false"로 설정
-> 파일 쓰기용 로거라면 appender-ref를 새롭게 만들어서 준다
#### pattern
appender의 로그 형식 설정
property를 선언하면 변수처럼 사용 가능
```xml
<property name="CONSOLE_LOG_PATTERN" value="%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n"/> 
// format이나 지정된 변수명(date, level, logger..) 가져올 수 있음

<appender name = "STDOUT" class = "ch.qos.logback.core.ConsoleAppender">
	<encoder>
		<pattern>${CONSOLE_LOG_PATTERN}</pattern>
	</encdoer>
</appender>
```
#### appender 추가
```xml
<property name="LOG_PATTERN" value="%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n"/> 
// format이나 지정된 변수명(date, level, logger..) 가져올 수 있음

<appender name = "STDOUT" class = "ch.qos.logback.core.ConsoleAppender">
	<encoder>
		<pattern>${LOG_PATTERN}</pattern>
	</encdoer>
</appender>

<appender name = "FILE" class = "ch.qos.logback.core.FileAppender">
	<file>logs/kdt.log</file>
	<append>false</append> // false시 실행 할때마다 override
	<encoder>
		<pattern>${LOG_PATTERN}</pattern>
	</encdoer>
</appender>
```
appender을 추가해 console, file에 로그 출력 동시에 가능
```xml
<timestamp key = "bySecond" datePattern = "yyyyMMdd'T'HHmmss" />

<appender name = "FILE" class = "ch.qos.logback.core.FileAppender">
	<file>logs/kdt_${bySecond}.log</file>
	<encoder>
		<pattern>${LOG_PATTERN}</pattern>
	</encdoer>
</appender>

```
이때 file명에 timestamp를 추가하면 실행시 실행시각을 포함한 새로운 파일 저장
- RollingFileAppender
  용량, 시간에 따라 로그 파일을 새로 생성하면서 저장
#### Conversion
```xml
<conversionRule 
	conversionWord = "clr" 
	converterClass = "logback.ColorCOnverter" />

<property name="LOG_PATTERN" value="%clr(%d{HH:mm:ss.SSS}){red} [%thread] %-5level %logger{36} - %msg%n"/> 
```
문자열 패턴에서 %clr(...){color}로 conversion 적용 가능
이때 AnsiOutput.setEnabled(AnsiOutput.enabled.ALWAYS); 호출해줘야 정상적으로 출력

## 스프링부트
### spring boot starter
spring core, spring mvc, spring web 등 모듈을 선택하면 dependency를 자동으로 설정
#### @SpringBootApplication
@EnableAutoConfiguration 및 configuration 관련 어노테이션을 상속받아
자동으로 인식되어 application.yml 파일, 리소스를 가져올 수 있음
- COC (conversion over configuration)
  설정보다는 관례
  모든 것을 하나하나 설정하는 것보다 일부만 설정하고 best practice를 따르면 빠르게 개발할 수 있다
##### banner.txt
banner.txt에 텍스트를 넣어주면 spring boot 배너도 변경 가능
##### logging
logback.xml 파일을 생성해 설정해주는 대신
application.yml에서 간단하게 설정해줄 수 있다
```yaml
logging:
	level:
		root: error
```
- 별도의 logback.xml 파일을 생성해 application.yml의 로깅 설정을 포함할때
```
<include resource="org/springframework/boot/logging/logback/defaults.xml" />
```
### Spring boot 외부에서 설정 가져오기
**전역 도구, Test 환경 설정, 커맨드 라인 인자, Sevlet 설정, OS 환경변수, @PropertySource** 순
**application.yml** 설정은 마지막에 읽는다
