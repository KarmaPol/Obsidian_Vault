```java
public class VoucherWebCreateRequestDto {  
	@NotNull  
	private Integer discount;  
	@EnumNamePattern(regexp = "FIXED_AMOUNT_DISCOUNT|PERCENT_DISCOUNT", enumClass = VoucherDiscountType.class)  
	private VoucherDiscountType voucherDiscountType;  
	  
	private VoucherWebCreateRequestDto() {  
	}  
	  
	public VoucherWebCreateRequestDto(Integer discount, VoucherDiscountType voucherDiscountType) {  
		this.discount = discount;  
		this.voucherDiscountType = voucherDiscountType;  
	}  
	  
	public Integer getDiscount() {  
		return discount;  
	}  
	  
	public VoucherDiscountType getVoucherDiscountType() {  
		return voucherDiscountType;  
	}  
}
```

이때 VoucherWebCreateRequestDto() { }를
- **public** 
  @ModelAttribute에서 Can not invoke 에러 발생
  -> ModelAttributeMethodProcessor.constructAttribute()는 빈 생성자 먼저 호출하고, setter로 바인딩
- **private**
  @ModelAttribute, @RequestBody 모두 잘 동작
- **없을 경우**
  @RequestBody Type definition error 에러 발생
  -> RequestBody는 Jackson이 Json을 역직렬화
  -> 빈 생성자 호출, getter나 setter로 필드 인식, reflection으로 값 주입

[ModelAttribute 기본생성자 Setter 정리](https://hyeon9mak.github.io/model-attribute-without-setter/)
[Request Body 빈 생성자?](https://yeonyeon.tistory.com/221)