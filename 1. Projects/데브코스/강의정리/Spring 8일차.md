## DataSource
### DataBase Connection Pool
커넥션을 매 SQL마다 생성하고 소멸하면 비용이 높다
-> **커넥션 풀**
### HikariCP
매우 가볍고 빠른 JDBC 커넥션 풀 라이브러리
#### DataSource 주입
```java
private final DataSource dataSource;

public CustomerJdbcRepository(DataSource dataSource){
	this.dataSource = dataSource;
}

public void findAll(){
	var connection = 
	dataSource.getConnection();
	var statement = connection.prepareStatement(SELECT_SQL);
	var resultSet = statement.executeQuery("select * from customers");
}
```
DriverManager로 매번 연결을 맺는 대신
Connection Pool에서 connection을 할당받을 수 있다
#### DataSource Configuration
```java
@Bean
public DataSource dataSource(){
	return DataSourceBuilder.create()
	.url("jdbc:mysql://localhost")
	.username("root")
	.password("1234")
	.type(HikariDataSource.class)
	.build();
}
```
DataSourceBuilder로 DataSource를 빌드하여 빈 등록 가능
- **커넥션 풀 크기 변경**
  기본은 10개
  dataSource.setMaximumPoolSize(100)
  dataSource.setMinimumPoolSize(100)
#### @TestInstance(TestInstance.Lifecycle.PER_CLASS)
Test 코드에서 해당 어노테이션을 사용하면 인스턴스를 클래스 단위로 사용할 수 있다

기본은 PER_METHOD로 테스트 메소드 별로 인스턴스가 분리되지만,
의도적으로 상태 값을 다음 테스트로 전달할 경우 유용하다
##### @TestMethodOrder(MethodOrderer.OrderAnnotation.class)
테스트 실행 순서를 @Order(1), @Order(2) 등을 메소드에 붙임으로써 보장할 수 있다
## JdbcTemplate
Jdbc를 이용해 SQL문을 실행할때, 중복이 많이 발생
-> JdbcTemplate으로 중복 X
