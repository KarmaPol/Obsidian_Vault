```java
@GetMapping("/api/v1/simple-orders")  
public List<Order> ordersV1() {  
	List<Order> all = orderRepository.findAllByString(new OrderSearch());  
	all.forEach(o -> o.getDelivery().getStatus());  // 강제 초기화
	return all;  
}
```

- ID 는 프록시 객체도 조회 가능하다