### Log Structured Storage Engine
Log파일 기반으로 작동하는 방식
Append-only 한번 쓰여진 정보는 바뀌지 않고 새로운 내용은 항상 파일 끝에 추가
모든 로그를 조회해서 DB를 get한다면 성능 저하 => Index 사용
### Index
쿼리 퍼포먼스를 올리기 위해 추가적으로 갖고 있는 데이터 스트럭처
Read 퍼포먼스는 올라감
추가적인 메모리, 디스크 용량 사용
너무 많으면 Write 성능 저하
### Segment File 
DB 파일을 하나로 가지고 있는게 아니라 일정 사이즈가 되면 새로운 파일 생성
### Compaction
file에서 키가 중복되거나 하는 쓸모없는 데이터를 지워준다
### 문제점
모든 키의 Hash Index가 memory에 들어가야함
Range 쿼리하기가 어려움

## LSM Tree
NoSQL DB에서 많이 사용
Sorted String Table을 사용해서 키값으로 Sort된 데이터를 저장

SSTable에 바로 데이터를 넣는게 아니라 메모리에 있는 self balanced Binary Tree(memtable)에 넣는다
memtable에 데이터가 어느 정도 쌓이면 sstable을 생성한다
이때, DB crash로 인한 메모리 데이터 손실을 방지하고자 Disk에 memtable 데이터를 Log file로 저장
### LSM Tree 데이터 읽기
1. memtable에서 데이터 조회
2. memory의 Sparse Index table 조회 -> 이미 정렬되어있기 때문에 가능
3. 인덱스 기반으로 sstable 조회
### LSM Tree 특징
- Write 빠름
- Range 쿼리 가능
- SSTable 여러개 merge하기 쉬움

## B+ Tree
RDB에서 많이 사용
바이너리 트리와 비슷하나 
Key 값으로 정렬, Children 노드가 여러개임
### B+Tree 값 업데이트
Key를 따라가서 해당 값 수정
### B+Tree 값 쓰기
- **바이너리 서치를 통해 빈자리를 찾은 경우**
-> 빈자리에 키, 값 저장
- **빈자리가 없을 경우**
-> 기존 노드와 연결된 새로운 노드 생성, 기존 노드의 데이터 절반 옮겨주고 부모 노드 포인터 수정

=> B+Tree 쓰기는 여러 Disk write이 필요할 때가 있음
중간에 Crash하는 경우 데이터가 corrupted 가능성
대게 어떤 write를 할지 wal파일에 미리 작성 후 업데이트

### B+ Tree vs LSM Tree
Read는 B+ Tree가 빠르고, Write는 LSM Tree가 더 빠르다
- Read
	B+ Tree는 트리를 따라 내려가면 바로 읽을 수 있다
	LSM Tree는 memtable, 여러 개의 sstable을 확인해야한다
- Write
	LSM Tree는 memtable, log file에 쓰면 끝
	B+ Tree는 여러 번의 Disk write 필요할 수 있음, wal파일 작성해야함

#### 참고 영상
https://youtu.be/yLe7_3cGSeU?si=l5J_w6GF8ZuS_8VF