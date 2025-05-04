# Single case, Multiple parameter
- @ParameterizedTest is useful
```java
// @CsvSource("provideProductCSV")
@MethodSource("provideProduct")
// @ValueSource(ints = {1, 2, 3}) can use this when just a value
@ParamaterizedTest
void containsStockType4(ProductType produtType, boolean expected) {
	// when
	boolean result = PorductType.containsStockType(productType);

	// then
	assertThat(result).isEqualTo(expected);
}
```
## @EnumSource
- Get Enum values with rule
## @CsvSource
```java=
@CsvSource(value = { 
"apple, 1", 
"banana, 2", 
"'lemon, lime', 0xF1" })
@ParameterizedTest
```
## @MethodSource
```java
static Stream<Arguments> stringIntAndListProvider() { 
	return Stream.of( 
		arguments("apple", 1, Arrays.asList("a", "b")),
		arguments("lemon", 2, Arrays.asList("x", "y")) 
	); 
}

@ParameterizedTest 
@MethodSource("stringIntAndListProvider")
```
- Should return Stream