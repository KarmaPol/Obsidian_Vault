### @RequestBody, @ResponseBody
@RequsetBody, @ResponseBody으로 데이터를 역직렬화/직렬화할때
1. Jackson은 getter, setter 메서드의 이름을 가져와서
2. 해당 메서드 이름에서 get, set을 제거한 후
3. 제거된 이름의 첫글자를 소문자로 변경
과정을 통해 filed에 접근한다

실제 데이터의 주입은 java.lang.reflect를 통해 주입하기 때문에
getter, setter 둘 중 하나만 있으면 된다

https://blogshine.tistory.com/446
### @ModelAttribute
다만 @ModelAttribute의 경우 setter를 사용해 값을 객체에 주입한다
- **setter을 사용하고 싶지 않을 경우**
  @AllArgsConstructor로 모든 필드를 매개변수로 만드는 생성자를 사용한다
  파라미터 갯수가 0개인 기본 생성자가 있다면 인스턴스를 생성 후, setter로 바인딩하지만
  그렇지 않다면 필드에 맞는 파라미터를 가진 생성자로 바인딩된다
  
https://hyeon9mak.github.io/model-attribute-without-setter/

### 결론
결국 @Getter와 생성자를 사용하면 @Setter를 사용하지 않아도 된다