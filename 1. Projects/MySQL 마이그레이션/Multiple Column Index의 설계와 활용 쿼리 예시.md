```sql
CREATE TABLE test1 (
	one_field BIGINT,
	...
	INDEX idx_col1_col2 (one_field, two_field) // 복합 인덱스
);
```
- **INDEX idx_col1_col2 (one_field, two_field, extra_field...)**
복합 인덱스를 계속해서 생성하면 오버로드 발생할수 있음, 되도록 쿼리 최적화

```sql
EXPLAIN SELECT hashEmail, one_field, two_field FROM test1 where two_field = 3;
```
- EXPLAIN 시에 type이 ALL이 나온다면 -> 인덱스를 활용하지 못하고 Full Scan
- type이 **index로** 나와야 인덱스 제대로 활용 중 -> 쿼리를 입력해보면서 튜닝하자

```sql
EXPLAIN SELECT one_field, two_field FROM test1 where one_field = 4 and two_field = 3;
```
- **type이 ref나 range가 나올때가 가장 베스트**
### 좋은 복합 인덱스 활용 예시
```sql
CREATE INDEX idx_order_search ON orders (user_id, product_id, created_at);`
SELECT * FROM orders WHERE user_id = 1 AND product_id = 10 ORDER BY created_at DESC;
```
- user_id, product_id로 검색 범위 좁히고, created_at으로 정렬
### 나쁜 복합 인덱스 활용 예시
```sql
CREATE INDEX idx_abc ON table_name (A, B, C);
SELECT * FROM table_name WHERE B = 2 AND C = 3;
```
- **맨 앞의 A가 빠지면 인덱스를 전혀 활용할 수 없다**
- A, C만 쿼리 하는 경우도 인덱스를 못탄다
```sql
SELECT * FROM table_name WHERE B = 2 AND C = 3 AND A = 1;
```
- Where 내의 필드 순서는 자동으로 최적화되므로 걱정하지말자
## Multiple Column Index 설계 기준
- Cardinality를 기준으로 index를 설계하자
ex) hash_email ⬆️, gender ⬇️

#### 좋지 않은 Index의 Side effect
- 불필요한 저장 공간 증가
- 테이블의 Insert, Update, Delete 성능 저하
- 불필요한 인덱스 최신 상태 유지비용
```java
SHOW INDEX FROM test1; // 인덱스 확인 가능
```

### (A)와 (A, B, C)가 모두 인덱스가 필요할때
```sql
CREATE INDEX idx_abc ON table_name (A, B, C);

EXPLAIN SELECT * FROM table_name WHERE A = 1;
```
- 복합 인덱스만 추가해도 A 단일 조건 쿼리도 사용 가능하다
-> 하지만 불필요한 B, C컬럼으로 인해 I/O 비용이 높아진다
- A 값만 변경해도 인덱스 전체가 업데이트됨

```sql
CREATE INDEX idx_a ON table_name (A);
```
- 테이블이 클수록 A 단독으로 활용이 잦거나, Range 검색이 자주 이용되면 단일 인덱스를 추가하자
- 작은 인덱스는 메모리에서 Cache Hit 할 확률이 더 높다!

##### Refer.
https://www.inflearn.com/course/%EB%8D%B0%EC%9D%B4%ED%84%B0-mysql-%EB%A7%88%EC%9D%B4%EA%B7%B8%EB%A0%88%EC%9D%B4%EC%85%98/dashboard
[[EXPLAIN 실행 계획에서 type 분류]]