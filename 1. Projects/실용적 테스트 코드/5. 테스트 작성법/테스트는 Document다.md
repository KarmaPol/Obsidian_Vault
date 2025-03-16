- 테스트 코드는 프로덕션의 이해를 위해 
  팀이 공유하는 문서와 같은 에셋이다

# Display Name을 섬세하게 작성하라
```java
@DisplayName("음료 1개를 추가할 수 있다")
@Test
void add() {
  ...
}
```
- 메서드 이름에 직접 넣을 수 있지만
  Junit5를 사용한다면 DisplayName에 넣자
- 명사의 나열보다 문장으로.
  (음료 1개 추가 테스트 -> 음료 1개를 추가할 수 있다)
## 도메인 용어를 사용하여 추상화된 내용 담기
- 특정 시간 이전에 주문을 생성하면 실패한다
  **=> 영업 시작 시간 이전에는 주문을 생성할 수 없다.**
- 테스트 메서드의 동작에 집중하지말고
  도메인 정책 관점으로 접근하자
  -> Not just a success or fail. Use domain terminology like "Order"