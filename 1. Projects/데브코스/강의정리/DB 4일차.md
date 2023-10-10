### 다양한 SQL
### Insert
INSERT INTO prod.vital(user_id, vital_id, date, weight) VALUES(100, 1, '2020-01-01', 75);
### Delete
DELETE FROM prod.vital WHERE weight <= 0;
- TRUNCATE
  조건없이 모든 레코드 삭제, 속도 빠르지만 롤백 불가
### Update
조건  기반하여 특정 레코드 필드 값 수정
UPDATE prod.vital SET weight = 92 WHERE vital_id = 4;
## JOIN
Inner Join
Left Join / Right Join
Full Join = Outer Join
	단 MySQL은 지원 X, LEFT JOIN과 RIGHT JOIN을 UNION해서 대신
Cross Join
Self Join

[[커리어 이야기]]