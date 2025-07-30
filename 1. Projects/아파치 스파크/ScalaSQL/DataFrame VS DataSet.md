- DataSet 컴파일 타임
```scala
case class Person(id:Int, name:String, age:Int, friends:Int)
val schemaPeople = spark.read  
.option("header", "true")  
.option("inferSchema", "true")  
.csv("data/fakefriends.csv")  
.as[Person]

```

- Datatframe 런타임 추측
```scala
val schemaPeople = spark.read  
.option("header", "true")  
.option("inferSchema", "true")  
.csv("data/fakefriends.csv")  
```