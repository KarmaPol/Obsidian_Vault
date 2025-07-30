# DataFrame
- DataSet of Row Objects (DataSet\[Row])
- 데이터셋은 컴파일 타임에 스키마가 결정됨
	- 단 컴파일 언어(자바, 스칼라)에서만 정해짐
- DataSets are more efficient
	- 효율적으로 직렬화
	- 컴파일 타임에 최적화
- 머신러닝에 최적화된 라이브러리
- DataSets가 훨씬 쉬움
### SparkSQL 쉘
- 대화형으로 하나의 분산 RDB 같이 작동
## UDF
- user defined functions
```scala
val square = udf{(x => x* x)}
```
- 데이터프레임의 컬럼을 다룸
- 자동 분산 처리
