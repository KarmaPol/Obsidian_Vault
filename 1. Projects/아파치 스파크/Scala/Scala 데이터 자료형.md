# 튜플
```
val stuff = ("Picard", "Ncc-2344")
```
- 불변형 리스트
## 튜플 인덱스 참조
```scala
stuff._1 // "Picard"
```
# 키 밸류 기반 튜플
```scala
val ship = "Picard" -> "Enterprise - D"
```
# 리스트
```scala
val shipList = List("A1", "B2", "C3")

shipList(1)

// 리스트 합치기
shipList ++ shipList
```
## 리스트 맵 연산
```scala
val backwardShips = shipList.map((ship: String) => {ship.reverse})
```
## 리스트 reduce 연산
```scala
val sum = numberList.reduce((x: Int, y: Int) => x + y)
```
# 리스트 filter 연산
```scala
val iHateFives = numberList.filter((x: Int) => x != 5)
val iHateFives = numberList.filter(_ != 3)
```
## 스파크 MapReduce?
- scala와 혼동될수 있음
- Spark 자체 MapReduce는 병렬로 처리됨
## 리스트 연산들
```scala
numberList.reverse
numberList.sorted
numberList.distinct
numberList.max
numberList.sum

numberList.contains(3)
```
# Map
```scala
val shipMap = Map("Kirk" -> "Enterprise", "Picard" -> "Enterprise-D")

shipMap("Kirk")
shipMap.contains("Timo")
```
## Exception Handling
```scala
val archerShip = util.Try(shipMap("Archer")) getOrElse "Unknown"
```
- Map에서 미싱 밸류 처리
	- Undefined -> String

