```scala
def squareIf(x: Int) : Int = {
	x*x
}
```
- function name - parameter name: type - return type 
# 함수를 parameter로
```scala
def transformInt(x: Int, f: Int => Int): Int = {
	f(x)
}
```
# 람다 펑션
```scala
transformInt(3, x => x*x*x)
```
- 매개변수로 바로 람다 함수 전달