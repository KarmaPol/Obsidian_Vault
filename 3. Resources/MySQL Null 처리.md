### COALESCE
```sql
// Column1 ~ 4 중 NULL이 아닌 첫 번째 Column을 출력
SELECT COALESCE(Column명1, Column명2, Column명3, Column명4)
FROM 테이블명
```

참고블로그
https://velog.io/@gillog/DB-MySQL-NULL-처리IFNULL-CASE-COALESCE