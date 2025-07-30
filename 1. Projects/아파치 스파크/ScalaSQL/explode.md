+---+------+
|id |letter|
+---+------+
|1  |a     |
|1  |b     |
|1  |c     |
|2  |x     |
|2  |y     |
+---+------+

- 1, {a, b, c} 를 3개의 행으로 쪼갬
```scala
val words = input  
.select(explode(split($"value", "\\W+")).alias("word"))  
.filter($"word" =!= "")
```