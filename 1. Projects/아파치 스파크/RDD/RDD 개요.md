## RDD
- Resilient
- Distributed
- Dataset
## SparkContext
- 드라이버 프로그램이 자동 작성
- 복원, 분산 처리를 위해 필수적
- SparkContext가 SC object를 만들어줌
## RDD 데이터 로드
- File
  sc.textFile("s3n://~")
- DB
  HiveContext(sc)

- JDBC, Cassanandra, S3 등
# 대표적인 연산
1. map
   rdd.map(x => x* x)
2. flatmap
3. filter
4. distinct
5. sample
6. union, intersetction, subtract, cartesian
# RDD Actions
1. collect
2. count
3. countByValue
4. take
5. top
6. reduce
	...
# Lazy Evaluation 전략
- 스파크는 **최종 목표**에 따라 최적화된 DAG 그래프를 생성함
- 즉 실제로 실행되는 순간에 결정되고 클러스터 여러 노드로 전송