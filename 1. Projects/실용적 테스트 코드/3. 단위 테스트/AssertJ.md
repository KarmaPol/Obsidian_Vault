- 테스트 코드 작성을 돕는 라이브러리
- 연쇄적인 메서드 체이닝 지원
```java
@Test  
void add() {  
	CafeKiosk cafeKiosk = new CafeKiosk();  
	cafeKiosk.add(new Americano());  
	  
	assertThat(cafeKiosk.getBeverages().size()).isEqualTo(1);  
	assertThat(cafeKiosk.getBeverages().get(0).getName()).isEqualTo("Americano");  
}
```