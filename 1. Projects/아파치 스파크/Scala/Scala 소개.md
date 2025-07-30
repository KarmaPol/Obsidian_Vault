- 분산 프로그램에 유용. 주로 Spark 코드에서 사용
- JVM 기반
- Functional programming
# 스칼라 타입
1. val hello: String = "Hola!"
   value - 불변
2. var hello: String = hello
   variable - 가변
## 왜 불변타입을 쓰는가?
- 함수형 패러다임
- 병렬 프로그래밍에서 각 스레드간 간섭, 레이스 컨디션을 걱정할 필요 없음