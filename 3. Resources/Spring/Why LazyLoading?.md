### Eager, Lazy
JPA에서는 데이터를 조회할때 Eager, Lazy 로딩의 2가지 방식이 있다.
연관관계가 있는 객체를 조회할때
- Eager 로딩의 경우, 연관관계로 딸린 객체까지 바로 join하여 가져온다
- Lazy 로딩의 경우, 해당 객체만 조회하고 연관관계의 객체를 사용할때 DB에서 가져온다

비즈니스 로직 상으로 연관관계로 매핑된 객체 모두가 필요한 경우(ex. Member-Team),
Join 연산으로 쿼리 한번에 데이터를 가져오는 EAGER 로딩으로 설정하는 것이 성능적으로 유리하다
=> 하지만, N+1 문제가 발생할 수 있고 예상하지 못한 대량의 SQL이 발생할 수 있으므로 **LAZY로딩을 사용하는 것 이 적절하다**
### @XXXToOne(fetch = FetchType.LAZY)
@XXXToMany의 경우, fetch 디폴트 값이 Lazy이지만
**@XXXToOne**의 경우, fetch 디폴트 값이 Eager이므로 **Lazy로 직접 설정해주어야 한다**
