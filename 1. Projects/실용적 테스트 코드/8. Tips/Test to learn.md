- Test written for learning function, library, framework
- More interesting to learn than just reading a document
### Example
```java
@Test
void partitionLearningTest() {
	// given
	List<Integer> testList = List.of(1,2,3);
	// when
	List<List<Integer>> partitions = Lists.partition(testList, 2);
	// then
	assertThat(partitions).hasSize(2)
		.isEqualTo(List.of(List.of(1,2,), List.of(3)));
}
```
- Don't think about the name
- **Learn from it and delete it depend on the purpose**

[[2. 테스트는 왜 필요할까?]]