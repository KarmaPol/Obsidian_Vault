- List 배열 선언
```java
static List<Node>[] graph = new ArrayList[105];
```
- PriorityQueue 선언, Comparator
```java
Queue<Node> pq = new PriorityQueue<>((n1, n2) -> Integer.compare(n1.price, n2.price));
```
