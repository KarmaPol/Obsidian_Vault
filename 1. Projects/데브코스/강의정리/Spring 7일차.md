## JDBC
Java application과 Database를 연결해주는 표준 인터페이스
백엔드 엔지니어는 JDBC API를 활용
JDBC Driver type4를 주로 사용
### JDBC flow
- get connection
- create statement
- configure statement
- execute statement
- handle warnings
- return result
- close statement
- close connection
#### Docker mysql 실행
```
docker run --name kdt-mysql -e MYSQL_PORT_HOST=% 
-e MYSQL_ROOT_PASSWORD=root1234! -p3306:3306 -d mysql:8
```
#### MySQL JDBC 연동
- gradle, maven 에 MySql jdbc driver dependency 추가
#### JDBC connection
```java
try{
	connection = 
	DriverManager.getConnection("jdbc:mySql://localhost","root","1234");
	statement = connection.createStatement();
	resultSet = statement.executeQuery("select * from customers");
	while(resultSet.next()){
		var name = resultSet.getString("name");
		var customerId = 
		UUID.nameUUIDFromBytes(resultSet.getBytes("customer_id"));
	}
}
catch(SQLException e){
	log.error("got error while closing connection", e);
}
finally {
	try{
		if(connection != null) connection.close();
		if(statement != null) statement.close();
		if(resultSet != null) resultSet.close();
	}
	catch(SQLException execption){
		log.error("got error while closing connection", exception);
	}
}
```
**connection은 반드시 close해줘야한다**
finally 구문으로 직접 닫아줄 수 있지만, 
AutoClosable 인터페이스의 구현체 Connection을 사용하면 자동으로 cloase해준다
##### TimeStamp
```java
var createAt = resultSet.getTimestamp("created_at").toLocalDateTime();
```
TimeStamp 타입을 그대로 사용하는 것보다 자바의 LocalDateTIme 타입을 사용하면 편리하다
toLocalDateTime() 메소드로 바꿀 수 있으나 null 체크를 반드시 해줘야한다
#### Select SQL
```java
String SELECT_SQL = 
MessageFormat.format("select * from customers where name = '{0}'", name);
```
String에 변수를 입력받아 조건을 포함한 select문을 실행할 수 있다
단, String을 단순히 조합하는 경우 SQL 인젝션 공격이 발생할 수 있다
##### SQL 인젝션
```java
findNames("'test01' OR 'a' = 'a'");
```
입력 변수에 의도치 않게 여러 조건을 같이 입력할 수 있다
=> PreparedStatement 사용
##### Prepared Statement
```java
String SELECT_SQL = "select * from customers where name = ?";

PreparedStatement statement = connection.prepareStatement(SELECT_SQL);
statement.setString(1, name);
```
특수 문자(따옴표, 콤마)를 자동 파싱해주기 때문에 SQL 인젝션 방지 가능
? 자리에 setString()으로 변수 설정
#### Insert SQL
```java
String INSERT_SQL = 
"insert into customers(customer_id, name, email) values (UUID_TO_BIN(?), ?, ?)";

PreparedStatement statement = connection.prepareStatement(INSERT_SQL);
statement.setBytes(1, customerId.toString().getBytes());
statement.setString(2, name);
statement.setString(3, email);
```
#### Delete SQL
```java
String DELETE_ALL_SQL = "delete from customers";
```
#### Update SQL
```java
String UPDATE_BY_ID_SQL = 
"update customers set name = ? where customer_id = UUID_TO_BIN(?)";

PreparedStatement statement = connection.prepareStatement(UPDATE_BY_ID_SQL);
statement.setString(1, name);
statement.setBytes(2, customerId.toString().getBytes());
```
