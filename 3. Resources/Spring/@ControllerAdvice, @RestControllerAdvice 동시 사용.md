https://stackoverflow.com/questions/45631766/restcontrolleradvice-and-controlleradvice-together

- @Order로 순서를 지정한다
- 각 Package를 지정한다
```java
@ControllerAdvice("my.controller1.package")
```
- 어노테이션을 지정한다
```java
@RestControllerAdvice(annotations = RestController.class)
```

[[@ControllerAdvice 동작 과정]]