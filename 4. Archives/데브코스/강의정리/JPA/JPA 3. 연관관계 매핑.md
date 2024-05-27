## 객체 연관관계 vs 테이블 연관관계
- 테이블을 외래키로 연관관계를 맺는다
- 객체는 참조로 연관관계를 맺는다
## 핵심 키워드
### 방향성
- 회원 -> 주문과 같이 둘 중 한 쪽만 참조하는 것을 단방향 관계
- 회원 -> 주문, 주문 -> 회원 양쪽 모두 서로 참조하는 것을 양방향 관계라고 한다
- **테이블에서의 관계는 항상 양방향이다**
### 다중성
- 회원(1) : 주문(N) 일대다
- 주문(N) : 회원(1) 다대일
- 연관관계 주인만 외래키 등록, 수정, 삭제 가능
- 테이블 중 FK가 있는 쪽이 연관관계 주인 (일반적으로 '다' 쪽)
### 객체 그래프 탐색
```java
Order findOrder = member.getOrders.get(0);
```
### 양방향 연관관계
```java
// Order.class
@ManyToOne
@JoinColumn(name = "member_id")
private Member member;

// Member.class
@OneToMany(mappedBy = "member") // Order가 연관관계의 주인
private List<Order> orders = new ArrayList<>();
```
- xxxToOne
  기본 값이 eager loading -> lazy loading으로 설정해야 n+1 문제를 피할 수 있다
## 고급 매핑
### 상속
#### @Inheritance(strategy = InheritanceType.JOINED)
```java
// 부모
@Entity
@Inheritance(strategy = InheritanceType.JOINED)
public abstract class Item {
	private Long id;
}

// 자식
@Entity
public class Car extends Item {
	private String rider;
}
```
Join 전략은 테이블을 여러 개 생성해서 자식 테이블 조회 시 Join
#### @Inheritance(strategy = InheritanceType.SINGLE_TABLE)
```java
// 부모
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "DTYPE")
public abstract class Item {
	private Long id;
}

// 자식
@Entity
@DiscriminatorValue("CAR")
public class Car extends Item {
	private String rider;
}
```
SingleTable 전략은 하나의 테이블만 생성하여 DTYPE 컬럼으로 구분
관리하기가 더 용이하므로 실무에서 더 자주 사용
### @MappedSuperclass
```java
@MappedSuperclass
@Entity
public class BaseEntity {
	private LocalDateTime createAt;
}

@Entity
public class Item extends BaseEntity {
	private Long id;
}
```
supperclass인 기본 클래스를 만들어 상속 가능
### 복합키 식별자 클래스
```java
public class Member {
	@Id
	private Long id1;
	@Id
	private Long id2;
}
```
id1, id2 복합키를 그대로 사용하면 오류 발생
#### 전략 1. @IdClass -> 비추, 객체지향적 X
```java
@Entity
@IdClass(ParentId.class)
public class Parent {
	@Id
	private Long id1;
	@Id
	private Long id2;
}

@EqualsAndHashCode // jpa는 equals, hashcode 메소드를 통해 객체 비교하므로 반드시 구현
public class ParentId implements Serializable {
	private Long id1;
	private Long id2;
}

// 엔티티 조회
em.find(Parent.class, new ParentId("id1", "id2"));
```
#### 전략 2. @EmbeddedId -> 강추, 객체지향적
```java
@Entity
public class Parent {
	@EmbeddedId
	private ParentId;
}

@EqualsAndHashCode // jpa는 equals, hashcode 메소드를 통해 객체 비교하므로 반드시 구현
@Embeddable
public class ParentId implements Serializable {
	private Long id1;
	private Long id2;
}

// 엔티티 조회
em.find(Parent.class, new ParentId("id1", "id2"));
```
## 프록시와 연관관계
- 지연로딩
  연관된 엔티티를 실제 사용할 때 조회
- 즉시로딩
  엔티티를 조회할때, 연관된 엔티티를 함께 조회
[Eager 로딩은 왜 좋지 않은가](https://velog.io/@jin0849/JPA-%EC%A6%89%EC%8B%9C%EB%A1%9C%EB%94%A9EAGER%EA%B3%BC-%EC%A7%80%EC%97%B0%EB%A1%9C%EB%94%A9LAZY)
### CASCADE 영속성 전이
```java
// Order.class
@OneToMany(mappedBy = "order", cascade = CascadeType.ALL)
private List<OrderItem> orderItems;

// OrderItem.class
@ManyToOne
private Order order;
```
이 때 Order 영속성 변경 시 OrderItem까지 전이된다
### 고아 상태 관리
```java
@OneToMany(mappedBy = "order", orphanRemoval = true) // 기본 값은 false
private List<OrderItem> orderItems;

// OrderItem.class
@ManyToOne
private Order order;
```
부모 객체와 연결이 끊어진 Entity를 flush가 되는 순간 DB에서도 삭제
