## Embedded Database
스프링 내부적으로 사용하는 DB를 bean으로 등록 가능
EmbeddedDatabaseBuilder가 DataSource를 리턴
보통 H2 DB를 많이 사용
### Embedded MySql
wix-embedded-mysql 라이브러리로 embedded mysql 띄워서 사용가능
테스트 코드는 Embedded DB를 활용하자
### NamedParameterJdbcTemplate
Index 기반의 parameter -> 이름 기반의 parameter
```java
paramMap.put("customerId", customer.getCustomerId());
paramMap.put("name", customer.getName());
namedJdbcTemplate.update("insert into customers(customer_id, name) values 
						 (UUID_TO_BIN(:customer_id), :name)", paramMap);
```
Map에 preparedStatement 설정값을 미리 담아서 전달해줄 수 있다
key를 미리 지정할 수 있기 때문에, 발생하는 실수를 줄일 수 있다
Map에 다른 다른 변수가 있어도 SQL에 삽입되지 않으므로, 하나의 맵을 만들어 재사용 가능하다
- **getJdbcTemplate()**
  namedParameterJdbcTemplate 내부에 JdbcTemplate을 포함하고 있으므로
  내부 JdbcTemplate을 얻어 사용할 수 있다
### 트랜잭션
여러 쿼리 작업을 논리적으로 묶은 작업 단위
실패 시 Rollback, 성공 시 Commit -> 원자성, 일관성, 독립성, 영구성의 보장
```java
try {
	connection.setAutoCommit(false);
	updateNameStatement.executeUpdate();
	updateEmailStatement.executeUpdate();
	connection.setAutoCommit(true);
} catch (SQLException exception) {
	if (connection != null) {
		try {
			connection.rollback();
			connection.close();
		}
		catch (SQLException e){
			log.error(e);
			throw new RuntimeException(exception);
		}
	}
	throw new RuntimeException(exception);
}
```
작업 시작 시점 setAutoCommit(false)
작업 종료 시점 setAutoCommit(true)
작업 실패시 catch -> rollback()