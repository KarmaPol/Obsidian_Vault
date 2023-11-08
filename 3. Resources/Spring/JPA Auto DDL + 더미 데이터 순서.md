https://velog.io/@kmw89891/Spring-Boot-서버-실행시-ddl-auto-init-sql

```java
spring.sql.init.mode=always
spring.jpa.defer-datasource-initialization=true
```
위 옵션 추가 시
1. `Hibernate` 의 `ddl-auto`
2. `data.sql` 실행