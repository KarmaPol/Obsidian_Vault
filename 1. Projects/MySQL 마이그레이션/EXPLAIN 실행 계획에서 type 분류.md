```MYSQL
EXPLAIN SELECT * FROM table_name WHERE B = 2 AND C = 3 AND A = 1;
```

| `type` 값 | 설명                                                                    | 성능             |
| -------- | --------------------------------------------------------------------- | -------------- |
| `NULL`   | 쿼리가 테이블을 조회하지 않음 (즉, `SELECT 1` 같은 경우)                                | ✅ 매우 좋음        |
| `system` | 테이블에 **1개만 있는 경우** (`rows=1`)                                         | ✅ 매우 좋음        |
| `const`  | `WHERE` 조건이 **프라이머리 키(PK) 또는 유니크 키(UK)와 비교**될 때 (`WHERE id = 1`)      | ✅ 매우 좋음        |
| `eq_ref` | **조인 시 프라이머리 키 또는 유니크 키를 이용한 정확한 매칭** (`JOIN ON a.id = b.id`)         | ✅ 매우 좋음        |
| `ref`    | **인덱스가 사용되지만, 유니크하지 않고 여러 개의 값을 반환할 때** (`WHERE indexed_col = ?`)     | 👍 좋음          |
| `range`  | **범위 검색 시 사용됨 (`BETWEEN, >, <, IN`)**                                 | 👍 괜찮음         |
| `index`  | **인덱스를 모두 읽음 (Index Full Scan)** (`SELECT indexed_col FROM table`)    | ⚠️ 보통 성능이 안 좋음 |
| `ALL`    | **풀 테이블 스캔(Full Table Scan, FTS)** (`WHERE` 조건이 없거나 인덱스를 활용하지 못하는 경우) | 🚨 매우 나쁨       |
