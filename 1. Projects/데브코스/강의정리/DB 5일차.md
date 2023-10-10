## 트랜잭션
Atomic하게 실행되어야 하는 SQL들을 묶어서 하나의 작업처럼 처리
-> Select에는 트랜잭션을 사용할 이유가 없음

end, commit 시 DB에 한번에 반영

은행 계좌 이체 : 인출 + 입금
### 형식
BEGIN; -- 트랜잭션 시작
	A 계좌로부터 인출;
	B 계좌로 입금;
END; -- 커밋
### 오토커밋
**autocommit = True**
모든 레코드 수정, 삭제, 추가 작업이 바로 DB에 쓰여짐
-> 오토커밋 없을 시 명시적으로 commit해줘야함
## View
이름 있는 쿼리가 View로 DB에 저장됨
**View가 사용될 때마다 Select가 실행됨**
Virtual Table이라고 부름
```sql
create view test.session_details as
select s.id, s.created, s.channel_id
from session s
join channel c on c.id = s.channel_id;
```
## Stored Procedure
**레코드를 리턴**
MySQL 서버단에 저장되는 SQL 쿼리들
Create Procedure 사용
인자를 넘길수 있고, 간단한 if, case문, loop문 프로그래밍 가능
하지만 디버깅이 힘들고 서버단 부하 증가
```sql
// 정의
DELIMITER //
CREATE PROCEDURE procedure_name(parameter_list)
BEGIN
	statements;
END //
DELIMETER;

// 호출
CALL procedure_name('parameter');
```
## Stored Function
**Scalar 값을 하나 리턴**해주는 서버쪽 함수
모든 함수 인자는 IN 파라미터
SQL 구문 안에서 사용가능 -> Stored Procedure은 call로 호출해줘야함
Create Function 사용
### Trigger
Create Trigger 사용
**SQL 실행 전, 후에 특정 작업 수행**
NEW / OLD modifier로 작업시 수정할 값 / 이전 값 불러오기 가능
```sql
CREATE TRIGGER test.before_update_keeyong_name_gender
	BEFORE UPDATE ON test.keeyong_name_gender
	FOR EACH ROW
INSERT INTO test.keeyong_name_gender_audit
SET name = OLD.name,
gender = OLD.gender,
modified = NOW();
```
## Explain SQL과 Index 튜닝
Select, Update, Insert, Delete 등의 쿼리가 어떻게 수행되는지 내부를 보여주는 SQL 명령어
- 해당 쿼리를 어떻게 실행할지 Execution Plan을 보여줌 -> 느리게 동작하는 쿼리 최적화 가능
- 보통 느린 쿼리의 경우, 문제 테이블에 인덱스를 붙이는 것이 일반적
### Index
특정 찾기 작업을 빠르게 하기 위해 MySQL이 별도로 만드는 데이터 구조
Primary Key, Foreign Key로 지정된 컬럼은 기본적으로 Index를 갖게 됨
Index는 **SELECT, DELETE, JOIN**은 빠르게 한다
하지만 **INSERT, UPDATE** 명령은 느리게 한다(인덱스 테이블까지 수정)
- 테이블에 너무 많은 인덱스를 추가하면, 오버헤드로 인해 전체적으로 느려짐
```sql
// 테이블 생성시 인덱스 생성
CREATE TABLE ex(
	id INT NOT NULL AUTO_INCREMENT,
	index_col VARCHAR(20),
	PRIMARY KEY(id),
	INDEX index_name(index_col)
);

// 나중에 테이블 수정
ALTER TABLE testalter_tbl ADD INDEX(column1);
ALTER TABLE testalter_tbl UNIQUE(column1);
ALTER TABLE testalter_tbl ADD FULLTEXT(column1); // 텍스트 검색이 많은 경우
ALTER TABLE testalter_tbl DROP INDEX(column1);

// 함수로 인덱스 생성
CREATE UNIQUE INDEX index_name ON test_tbl (col1, col2,...);
```
#### 인덱스 성능 비교
인덱싱에 의해 성능이 크게 차이나려면 레코드가 백만개 이상일때
### 맺음말
필요할때마다 RDB 테이블을 생성해 데이터를 넣는다면 용량 증대에 한계
-> 서비스 운영에 직접적으로 필요없다면 다른 스토리지를 사용하자(AWS S3...)