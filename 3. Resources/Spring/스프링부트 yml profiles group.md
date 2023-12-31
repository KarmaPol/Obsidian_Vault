로컬, 개발 서버, 배포 서버 등 여러 서버에서 환경 설정을 다르게 해야할때 사용 가능
여러 개의 profile들을 하나의 profile처럼 관리할 수 있다
### yml 파일

```json
spring:
  profiles:
    active: dev // 기본적으로 활성화할 profile
    group:
      dev: profile1
      test: profile2,common
      prod: profile3,common
  // include: profiles 불러들어올 yml 파일(application-profiles.yml)
default:
  string: default property
---
spring:
  config:
    activate:
      on-profile: profile1
  datasource:
    driver-class-name: org.h2.Driver
    url: jdbc:h2:~/test
    username: dev
    password:
server:
  port: 7777
---
spring:
  config:
    activate:
      on-profile: profile2
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/test
    username: test
    password: test1234!
server:
  port: 8888
---
spring:
  config:
    activate:
      on-profile: profile3
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/prod
    username: prod
    password: prod1234!
server:
  port: 9999
---
spring:
  config:
    activate:
      on-profile: common
common:
  string: common property
```
--- 로 프로파일 구분 가능, yml 여러개를 생성해도 됨
#### 인텔리제이 프로파일 설정
Run → Edit Configurations에서 Active Profile 설정
#### 테스트 환경 프로파일 설정
```java
@SpringBootTest
@ActiveProfiles("dev")
class MultiProfilesTest{}
```
@ActiveProfiles로 프로파일 설정
#### 빌드 파일 실행시 프로파일 설정
```
java -jar multi_profiles.jar --spring.profiles.active=prod
```
#### Deprecated된 Profile 설정 방식
[http://honeymon.io/tech/2021/01/16/spring-boot-config-data-migration.html](http://honeymon.io/tech/2021/01/16/spring-boot-config-data-migration.html)
#### 참고 블로그
https://colabear754.tistory.com/112#주의사항
https://zzang9ha.tistory.com/415