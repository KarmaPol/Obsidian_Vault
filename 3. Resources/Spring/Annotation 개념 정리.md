[Annotation 알짜배기](https://aljjabaegi.tistory.com/660)

### @Alias
@Alias는 상위 어노테이션 (@Controller -> @Component)의 속성에 접근할 수 있도록 도와준다
즉 @Controller에서 지정한 속성은 @Component의 value에 지정되고,
Component Scan후 Bean 등록 시 이름을 지정한 value값으로 할 수 있다