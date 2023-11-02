https://www.baeldung.com/javax-validations-enums
https://velog.io/@devlyny/Spring-Boot-Enum-유효성-검사하기

https://jsy1110.github.io/2022/enum-class-validation/

https://cchoimin.tistory.com/entry/Enum-유효성-검사하기 -> 이거로 함

```java
// validator
public class EnumNamepattenValidator implements ConstraintValidator<EnumNamePattern, Enum<?>> {  
  
private final Logger log = LoggerFactory.getLogger(EnumNamepattenValidator.class);  
private Pattern pattern;  
  
@Override  
public void initialize(EnumNamePattern constraintAnnotation) {  
log.info("validator >>>>>>>>>>>");  
try{  
pattern = Pattern.compile(constraintAnnotation.regexp());  
} catch (PatternSyntaxException e){  
throw new VoucherApplicationException(ErrorCode.INVALID_INPUT_DATA);  
}  
}  
  
@Override  
public boolean isValid(Enum<?> value, ConstraintValidatorContext context) {  
if(value == null) {  
return false;  
}  
Matcher matcher = pattern.matcher(value.name());  
return matcher.matches();  
}  
}


// annotation
@Target({METHOD, FIELD, ANNOTATION_TYPE, CONSTRUCTOR, PARAMETER, TYPE_USE})  
@Retention(RUNTIME)  
@Documented  
@Constraint(validatedBy = EnumNamepattenValidator.class)  
public @interface EnumNamePattern {  
String regexp();  
String message() default "must match \"{regexp}\"";  
Class<?>[] groups() default {};  
Class<? extends Payload>[] payload() default {};  
Class<? extends java.lang.Enum<?>> enumClass();  
}


// dto
public class VoucherWebCreateRequestDto {  
@NotNull  
private Integer discount;  
@EnumNamePattern(regexp = "FIXED_AMOUNT_DISCOUNT|PERCENT_DISCOUNT", enumClass = VoucherDiscountType.class)  
private VoucherDiscountType voucherDiscountType;
}

// enum
public enum VoucherDiscountType {  
FIXED_AMOUNT_DISCOUNT("Fixed Amount Discount","Amount"),  
PERCENT_DISCOUNT("Percent Discount","Percent");  

...

// 두번 검증하는 꼴이 아닌가?
@JsonCreator(mode = JsonCreator.Mode.DELEGATING)  
public static VoucherDiscountType findByCode(String code) {  
return Stream.of(VoucherDiscountType.values())  
.filter(v -> v.toString().equals(code))  
.findFirst().orElse(null);  
}  
}
```
@JsonCreator를 선언하지 않으면 기본 컨버터가 Enum.valueof()연산으로 바인딩
-> Type Error 발생

ModelAttribute의 경우, 검증 로직으로 가기전 parsing 할때 오류가 터진다

[Validation 원리](https://incheol-jung.gitbook.io/docs/q-and-a/spring/valid)
#### valid 요약
Handler Mapper -> HandlerMethodAdapter이 Handler연관 Adapter  호출
-> Adapter는 Request유형에 맞는 ArgumentResolver 호출
-> Handler에 맞게 Parameter 변환 후 **validateIfApplicable()** 호출
