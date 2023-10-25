Java 14 이상에서 지원하는 불변 데이터 객체
```java
public record Person(String name, String address){
	// 기본 생성자 외의 생성자 생성 가능
	public Person(String name){
		this(name, "Unknown");
	}
}

// 인스턴스 생성
Person person = new Person("John Doe", "100 Ln.");

// getter
String name = person.name();
```
Getter, Eqauls 등 따로 만들어주지 않아도 된다
equals()의 경우, 모든 필드 값이 일치하면 true 반환