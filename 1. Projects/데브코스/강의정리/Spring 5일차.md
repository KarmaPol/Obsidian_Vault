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