https://chanhuiseok.github.io/posts/db-6/

```sql
SET @HOUR = -1;
SELECT (@HOUR := @HOUR +1) AS HOUR
FROM ANIMAL_OUTS
WHERE @HOUR < 23;
```

Hour 변수 선언
0부터 23까지 생성