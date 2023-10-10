## 배움의 전형적인 패턴

가장 중요한 것은 버티는 힘 → 더딘 기간을 즐기자, 배움의 발전이란 tipping point를 거치면서 폭발

내가 뭘 모르는지 생각

잘하는 사람 보고 기죽지 않기

### DBMS

필요 데이터를 저장하는 곳

빠른 처리 속도가 중요

1. 프로덕션용 관계형 DB - 구조화된 데이터에 적합 (Mysql, PostgreSql)
2. 데이터 웨어하우스 관계형 DB (스노우 플레이크, BigQuery) 비즈니스 인사이트, 제품 서비스 개선
3. NoSQL DB - RDBMS 보완 용도 Key/Value Storage - Redis, Memcache Document Store - MongoDB Wide Column Storage - Cassandra, DynamoDB Search Engine - Elastic Search

### 시스템 구성

프리젠테이션 티어(FE) - 애플리케이션 티어(BE) - 데이터 티어(BE - DB Server)