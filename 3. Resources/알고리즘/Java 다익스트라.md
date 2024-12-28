- List 배열 선언
```java
static List<Node>[] graph = new ArrayList[105];
```
- PriorityQueue 선언, Comparator
```java
Queue<Node> pq = new PriorityQueue<>((n1, n2) -> Integer.compare(n1.price, n2.price));
```
- 다익스트라 순회
```java
while(!pq.isEmpty()) {

Node node = pq.poll();

  
// 이미 방문한 노드는 스킵
if(distances[node.next] < node.price) {
	continue;
}  

// 갱신 처리
for(Node adj : graph[node.next]) {
	if(distances[adj.next] > distances[node.next] + adj.price) {
		distances[adj.next] = distances[node.next] + adj.price;
		pq.offer(new Node(adj.next, distances[adj.next]));
		
	}
}
```