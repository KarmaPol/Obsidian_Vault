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
