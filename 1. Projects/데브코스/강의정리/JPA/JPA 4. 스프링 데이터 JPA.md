## SPRING DATA JPA
JPA를 편리하게 사용할 수 있도록 지원하는 프로젝트
```java
public interface OrderRepository extends JpaRepository<Order, String> {}
```
### 메소드 쿼리
OrderBy, By 등의 키워드로 조합하여 쿼리 사용 가능
```java
orderRepository.findAllByOrderStatus(OPENED);
```
### 커스텀 쿼리
```java
@Query("SELECT o FROM Order AS o WHERE o.memo LIKE %?1%")
Optional<Order> findByMemo(String memo);
```
## API 개발
- 보통 실무에서는 save 시 꼭 필요한 값인 id값만 반환 (객체 전부 X)
- JPA 자체적으로 Pagable로 페이징 처리 지원