## List entity를 fetch join할때
```java
public List<Order> findAllWithItem(OrderSearch orderSearch) {  
	return em.createQuery(  
	"select o from Order o"  
	+ " join fetch o.member m"  
	+ " join fetch o.delivery d"  
	+ " join fetch o.orderItems oi"  // orderItems - List
	+ " join fetch oi.item i", Order.class  
	).getResultList();  
}
```
- 이때 join으로 인해 OrderItems의 갯수만큼 order가 늘어난다
### 해결책
```java
public List<Order> findAllWithItem(OrderSearch orderSearch) {  
	return em.createQuery(  
	"select distinct o from Order o"  
	+ " join fetch o.member m"  
	+ " join fetch o.delivery d"  
	+ " join fetch o.orderItems oi"  // orderItems - List
	+ " join fetch oi.item i", Order.class  
	).getResultList();  
}
```
- distinct 키워드로 JPA entity 중복을 제거할 수 있다
  -> DB 쿼리와 다르게 JPA Entity id 기준으로 중복 제거
- DB 쿼리에서도 distinct로 기본 중복 제거
#### 한계점
- 페이징 불가능
  -> 메모리에서 모든 데이터를 불러와 페이징을 처리하게 된다.. 
  => **일대다에서는 fetch join 사용금지**, 일대다에서는 Batch로

- Fetch Join은 1:1 또는 다대일에서 사용하자