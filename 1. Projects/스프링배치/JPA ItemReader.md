# JpaCursorItemReader
- JdbcCursor과 유사
## 구성
1. queryString 또는 < JpaQueryProvider
   Query 생성
2. EntityManager
   JPA 엔진
3. Query
   실행가능한 쿼리 인스턴스
- getResultStream() 으로 하나씩 스트림
  단, 기본 구현은 모든 데이터 메모리에 불러옴으로 주의
- next()로 다음 아이템 불러옴. 없으면 null
## JpaQueryProvider
- query String에 비해 복잡한 쿼리에 용이
- Entity에 미리 어노테이션으로  지정
  @NamedQuery(name= 12, query="SELECT ~")
  public class Post {}
- hintValues(Mpa.of("org.hibernate.fetchSize",100))
  Spring batch 5.2부터 힌트 바로 지정 가능
# JpaPagingItemReader
- 오프셋 페이지는 지양하자. 실시간 변경 및 DB 메모리 성능 저하
- 커서 방식은 한번에 메모리에 띄웠지만, 페이징은 페이지마다 쿼리 생성
## 페이징 방식은 Fetch join 제거
- 페이지 보다 Fetch join이 먼저 작동
	- 페이징이 10개라면 관련 엔티티 100개를 10번 항상 조회함
- 즉 **@EAGER, @BatchSize로 변경해 사용하자**
- 왜 @LAZY 는 안되는거지?
	- **읽고 곧바로 page commit해 트랜잭션 종료. N+1 문제 발생**!
	- 스프링 배치 JpaPagingItemReader 트랜잭션 구현으로 인한 결함
	- 웹 애플리케이션에선 불필요한 필드 스킵하는데 레이지 로딩 장점있지만,
	  **배치 애플리케이션은 상대적으로 비즈니스 로직 단순해 Eager 충분**