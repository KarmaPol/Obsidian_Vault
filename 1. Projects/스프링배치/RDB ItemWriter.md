# 단일 VS 멀티 write
- 수백건을 청크 단위로 한번에 전송하는것이 네트워크 왕복 횟수 500배 줄임
- jdbc:mysql://localhost:3306/mysql?rewriteBatchedStatements=true
  로 멀티 밸류 인서트로 자동 변환
# JdbcBatchItemWriter
## 구성
1. NamedParameterJdbcTemplate
2. SQL
3. ItemSqlParameterSourceProvider OR ItemPreparedStatementSetter
   자바 객체, 레코드를 리플렉션 기반으로 바인딩
