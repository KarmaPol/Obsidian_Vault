- 스파크가 스키마를 추론할때 필요
```scala
import spark.implicits._  
val schemaPeople = spark.read  
.option("header", "true")  
.option("inferSchema", "true")  
.csv("data/fakefriends.csv")  
.as[Person]
```

- DataSet 타입 인코딩
- Seq -> DataFrame
- RDD -> DataFrame
- $"컬럼명" 구문
	- import spark.implicits._
	  df.select($"name")
- 헤더에서 추론할때 필요