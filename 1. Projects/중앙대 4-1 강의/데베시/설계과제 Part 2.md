- R, S 테이블은 파일로 저장 (기존 과제 사용)
- Temporary files : Partition 저장 - 그림 13.1 파일구조
- Hash-Join 알고리즘
  1. 파티셔닝할때의 해시 함수 h
  2. 해시 인덱스 함수

1. 해시 함수로 join 연산키를 기준으로 PK 저장하는 파티션 파일 2개 생성
2. 파티션한 파일을 다시 불러올때 인메모리에 해시함수로 저장 (1과 별개)
SELECT * FROM member JOIN member ON id=id;