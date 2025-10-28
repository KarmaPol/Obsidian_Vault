# 단일 VS 멀티 write
- 수백건을 청크 단위로 한번에 전송하는것이 네트워크 왕복 횟수 500배 줄임ㅑ
	- INSERT INTO data () VALUES (1, 2), (3,4)..;
- jdbc:mysql://localhost:3306/mysql?rewriteBatchedStatements=true
  로 멀티 밸류 인서트로 자동 변환
# JdbcBatchItemWriter
## 구성
1. NamedParameterJdbcTemplate
2. SQL
3. ItemSqlParameterSourceProvider OR ItemPreparedStatementSetter
   자바 객체, 레코드를 리플렉션 기반으로 SQL 파라미터 바인딩
## 네트워크 통신 최적화
- 청크 내 모든 아이템을 prepared statement로 변환해 한번에 INSERT
## 주의사항
- 배치 Write 작업은 조회한 PK를 사용하자. Where 절로 바로 업데이트 시 예상치 못한 부작용
### **assertUpdates()**
- true (기본값) - 하나라도 실패시 중단
- false - dlfqn antl