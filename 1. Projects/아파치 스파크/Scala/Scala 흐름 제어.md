# IF 문
- 자바와 유사
```scala
if (1 > 3) {
	...
} else {
	...
}
```
# Matching
- switch문과 유사
```scala
number match {
	case 1 => println("one")
	case _ => println("one")
}
```
# For 문
```scala
for (x <- 1 to 4) {
	val squared = x * x
}
```
## While문, Do while 문
- 자바와 동일
# Scala internal return
```scala
{val x = 10; x + 20}
// res6: Int = 30
```
- 명시적으로 리턴하지 않아도, 마지막에 발생하는것이 반환 값
