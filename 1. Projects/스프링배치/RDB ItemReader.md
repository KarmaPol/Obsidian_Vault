# 대용량 데이터 처리 전략
1. 커서 기반 처리
   하나의 커넥션으로 스트리밍
   메모리는 최소한으로 사용
2. 페이징 기반 처리
   데이터를 정확히 잘라서 차근차근
   페이지 마다 새로운 쿼리로 안정성 보장
# JdbcCursorItemReader
- 커넥션을 길게 유지
- rs.next()로 다음 아이템
## 구성
1. DataSource
2. SQL
3. RowMapper
   ResultSet -> Java
4. PrepareStatement
   쿼리 실행 및 결과 조회
## CursorReader 원리
- ResultSet으로 하나씩 조회
- RDB 내에 버퍼에 여러 단위로 읽어옴
- fetchSize로 조절 가능
- **절대 한번에 한 쿼리가 아님!**
## Cursor 트랜잭션
- Step과 별개의 트랜잭션 사용해서 안전
- 따라서 Step에서 수정해도 Cursor의 트랜잭션엔 반영 X
## Cursor의 OrderBy
- 실패 후 재실행해도 같은 순서를 보장해야함
- **PK 값으로 Order By는 필수!**
# JdbcPagingItemReader
- 페이지 단위 읽어오기
## Page 방식
1. Offset + Limit
   Offset 만큼 버리므로 추천되지 않음
   뒤로 갈수록 성능 급격히 저하
2. **Keyset 기반 페이징**
   id(마지막 키) 기반으로 읽어와 성능 일정
## 페이지리더 구성요소
1. DataSource
2. RowMapper
3. NamedParameterJdbcTemplate
4. PagingQueryProvider
	1. selectClause()
	2. fromClause()
	3. whereClause()
	4. groupClause()
	5. **sortKeys() - ORDER BY 정렬키, PK 사용해 순서 보장 필수**
5. 

TBC