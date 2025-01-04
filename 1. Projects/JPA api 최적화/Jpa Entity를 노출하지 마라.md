### 문제상황
- entity
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
  
@JsonIgnore  
@OneToMany(mappedBy = "member")  
private List<Order> orders = new ArrayList<>();  
  
}
```
- controller
```java
@PostMapping("/api/v1/members")  
public CreateMemberResponse saveMemberV1(@RequestBody @Valid Member member) {  
	Long id = memberService.join(member);  
	return new CreateMemberResponse(id);  
}
```
API request로 entity를 직접 노출
-> API 수정때마다 entity를 수정해야하고, SOLID 원칙 X
### 해결책 
```java
@PostMapping("/api/v2/members")  
	public CreateMemberResponse saveMemberV2(@RequestBody @Valid CreateMemberRequest request) {  
	Member member = new Member();  
	member.setName(request.getName());  
	  
	Long id = memberService.join(member);  
	return new CreateMemberResponse(id);  
}  
  
@Data  
static class CreateMemberRequest {  
	@NotEmpty  
	private String name;  
}
```
- API별로 DTO를 분리한다
  -> 추가작업이 필요하지만, 유지보수가 용이