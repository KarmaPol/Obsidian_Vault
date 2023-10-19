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