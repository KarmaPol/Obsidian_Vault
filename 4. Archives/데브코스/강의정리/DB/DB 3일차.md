## 조회문
테이블에서 레코드들 읽어오는데 사용

**포맷**
SELECT
FROM
WHERE
GROUP BY
ORDER BY
LIMIT N;
### CASE WHEN 조건문
CASE
	WHEN 조건 1 THEN 값1
	ELSE 값3
END 필드이름
### WHERE 조건
- IN
  where channel_id in (3,4)
- LIKE
  where channel like '%G'
- BETWEEN
  날짜 범위
위 오퍼레이터들은 CASE문 내에서도 사용가능
### String functions
|함수 이름|설명|
|---|---|
|CONCAT(문자열, 문자열)|문자열을 합쳐준다.|
|SUBSTRING(문자열, 시작, 끝)|문자열을 기준에 따라 나눠준다.|
|REPLACE(문자열, target, replace)|문자열 중의 target에 해당하는 부분을 replace로 바꾼다.|
|REVERSE(문자열)|문자열을 거꾸로 뒤집는다.|
|CHAR_LENGTH(문자열)|문자열의 길이를 반환한다.(공백도 포함)|
|UPPER(문자열)|문자열을 대문자로 전부 변환하여 반환한다.|
|LOWER(문자열)|문자열을 소문자로 전부 변환하여 반환한다.|
### ORDER BY
디폴트는 ASC
NULL 값은 ASC일때 처음, DESC일때 마지막
### 타입변환
- **Date Type**
  NOW
  DATE, WEEK, MONTH, YEAR, HOUR, MINUTE, MONTHNAME
  DATEDIFF(now(), createdDate)
  DATE_ADD(createdDate, INTERVAL 10 DAY)
- **String -> Date**
  STR_TO_DATE('01,5,2013', '%d,%m,%Y'); => 2013-05-01
  DATE_FORMAT
- **Date Format**
```sql
DATE_FORMAT(DATETIME, '%Y-%m-%d')
```
### 타입 캐스팅
**cast**('100.0' as float), **convert**('100.0', float);
### Join
서로 다른 테이블에 존재하는 레코드들을 특정 조건을 바탕으로 병합하는 작업
### Group By
group by & aggregate 함수
[[MySQL Set함수]]
