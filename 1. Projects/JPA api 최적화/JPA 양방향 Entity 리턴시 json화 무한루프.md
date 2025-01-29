### Order
```java
@Entity  
@Table(name = "orders")  
@Getter @Setter  
@NoArgsConstructor(access = AccessLevel.PROTECTED)  
public class Order {  
  
	@Id @GeneratedValue  
	@Column(name = "order_id")  
	private Long id;  
	  
	@ManyToOne(fetch = LAZY)  
	@JoinColumn(name = "member_id")  
	private Member member;  
	  
	@JsonIgnore  
	@OneToMany(mappedBy = "order", cascade = CascadeType.ALL)  
	private List<OrderItem> orderItems = new ArrayList<>();  
	  
	@JsonIgnore  
	@OneToOne(fetch = LAZY, cascade = CascadeType.ALL)  
	@JoinColumn(name = "delivery_id")  
	private Delivery delivery;
	
}
```
### Member
```java
@Entity  
@Getter @Setter  
public class Member {  
	  
	@Id @GeneratedValue  
	@Column(name = "member_id")  
	private Long id;  
	  
	private String name;  
	  
	@Embedded  
	private Address address;  
	  
	@JsonIgnore  // Member, Order 둘 중 하나는 JsonIgnore
	@OneToMany(mappedBy = "member")  
	private List<Order> orders = new ArrayList<>();  
	  
}

@Bean  
Hibernate5Module hibernate5Module() {  
	return new Hibernate5Module();  
}
```

- 양방향 매핑 시, Entity를 그대로 json화할때 무한루프 발생
  -> 둘 중 하나는 @JsonIgnore