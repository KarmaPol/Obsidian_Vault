```java
@Test  
void add() {  
	CafeKiosk cafeKiosk = new CafeKiosk();  
	cafeKiosk.add(new Americano());  
	  
	System.out.println(">>> added beverages number : " + cafeKiosk.getBeverages().size());  
	System.out.println(">>> added beverages : " + cafeKiosk.getBeverages().get(0).getName());  
}
```
- 사람이 결과물을 직접 확인한다면 테스트 코드의 이점을 살리지 못한다