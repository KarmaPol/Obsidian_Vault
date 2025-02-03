- 먼저 ToOne 관계는 모두 fetch join
- application.yml
```java
jpa:  
	hibernate:  
		ddl-auto: create  
		properties:  
		hibernate:  
			default_batch_fetch_size: 100 // batch size 100 ~ 1000
```
batch 설정으로 where in 쿼리 사용 (위 설정에선 100개)
- 또는 Entity 자체 설정 (잘 활용 X)
```java
@BatchSize(100)
class Member {
```


```java
public List<Order> findAllWithMemberDelivery(int offset, int limit) {  
	return em.createQuery(  
		"select o from Order o" +  
		" join fetch o.member m" +  
		" join fetch o.delivery d", Order.class  
		).setFirstResult(offset)  
		.setMaxResults(limit)  
	.getResultList();  
}
```

**=> 1 + N + N의 쿼리를 1 + 1+ 1로 최적화**