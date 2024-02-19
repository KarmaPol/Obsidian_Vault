## Data 종류
- structured data
- unstructured data
- transactional data
- relational data
  -> 데이터 종류에 따라 서비스 선택
## Cloud storage
객체 저장소 (S3랑 유사)
actual data itself 저장, 메타데이터 필요, 고유키 필수
완전 관리형
**웹사이트 컨텐츠, 큰 용량의 다운로드 리소스를 저장하기에 용이함**
### 버켓
- 지역에 따라 고유한 (저장소)버켓 생성
데이터 자체는 불변 -> 새로운 데이터를 버저닝해서 계속 생성
### 권한 설정
IAM role를 활용해 access 권한을 관리해줘야함
또는 더 자세한 범위의 Scope, Permission 지정 가능

특성 상 계속 데이터가 쌓이기 때문에, 보유 기간을 설정해 이후엔 자동 삭제되게 할수 있다
## Storage 종류
### Standard Storage
최신 데이터만 저장
### Nearline Storage
once per month
아카이빙에 사용
### Coldline Storage
90일에 한번 저장
### Archive Storage
1년에 한번 저장
=> 가장 비용이 저렴

**But** 모든 스토리지는 객체 사이즈 제한 없고, low latency 제공 및 지역 제한 없음
## Auto class
Object access patern에 따라 Storage 종류를 자동으로 관리해준다
-> 비용 절감 가능
## Cloud Storage 장점
- 사용량에 따라 요금 부과
- 가용성을 미리 계산할 필요 없음
- 서버 사이드 암호화
- HTTPS/TLS 암호화
## Cloud Storage에 데이터 저장
- Cloud 콘솔, SDK 등으로 손쉽게 저장
- 대용량 데이터의 경우, 다른 클라우드, 리전으로부터의 배치 작업 제공
- **Transfer Applicance**, hicapacity cloud server 페타바이트 단위 데이터 지원
- cloud storage -> firestore, cloud sql 등으로 데이터 이동 가능
## Cloud SQL
관리형 RDB 서비스
자동 복제 시나리오 제공
자동 백업 제공 (7개 백업 까지)
구글 내부 망에서 암호화
네트워크 방화벽 제공
다른 클라우드 서비스, 외부 서비스에서 CLOUD SQL에 접근 가능

cloud sql 인가 검증을 위해 compute engine을 같은 region에 배치해 사용 가능
## Cloud Spanner
- 관리형 RDB 서비스
- Scales horizontally
- Strongly consistent
- Speaks SQL
**구글 핵심 비즈니스**

- secondary index, 조인 있을때 유용
- 강한 일관성 제공
- 매우 많은 인풋, 아웃풋 요청 있을 때 유용
## FireStore
- 도큐먼트 단위로 저장, 도큐먼트 - 콜렉션
- NoSQL
- 각각의 도큐먼트 혹은 한꺼번에 모든 도큐먼트 가져올 수 있음
- 필터 조건, sorting 조건 조합 가능
- 기본적으로 인덱싱
- **캐시**해주기 때문에 OFFLINE 되어도 서비스 제공,  ONLINE 되면 동기화
- multi-region
- strong consistency
- atomic batch operation
- real transaction support
### 요금 계산
도큐먼트 단위로 요금 부과 (50000 read, 20000 write/delete 까지 무료)
쿼리 사용시 요금 부과 -> 1개의 read
DB 용량에 따라 요금 부과 (일 1GB까지 무료)
네트워크 대역폭에 따라 요금 부과 (US 내에선 월 10기가까지 무료)
## Cloud Bigtable
- NoSQL 빅데이터 서버
- gmail, 검색, 아날리틱스에서 해당 서버 사용
- low latency, high throughput
- 1GB 이상의 정형 데이터에 유용
- 매우 빨라야함
- NOSQL 데이터에 유용
- 시간에 따라 순차적일 수록 유용
- 비동기 배치, 실시간 동기 작업에 유용
- 머신 러닝 알고리즘에 유용
### Bigtable 데이터 수신
- API를 통해 **HBASE, 자바 서버로부터** 데이터 읽어올수 있음
- Spark, Storm 등으로 **데이터 스트리밍** 가능
- Dataflow, Hadoop, Dataflow로 **데이터 배치 전송** 가능
## 스토리지 서비스 비교
| 서비스            | 데이터              | 용량                          |
| ----------------- |:------------------- | ----------------------------- |
| 클라우드 스토리지 | 10MB 이상 blobs     | 페타바이트                    |
| 클라우드 SQL      | web 프레임워크, sql | 64TB까지                      |
| Spanner           | sql, 확장성         | Petabytes                     |
| Firestore         | 실시간 쿼리 및 캐싱 - 웹앱 | 테라바이트 <br>엔티티 당 1MB까지 |
| Cloud Bigtable                  | 빅데이터, 통계 데이터, <br>heavy read and write                    | 페타바이트                              |
### BigQuery?
빅데이터 통계에 주로 사용, pure storage 제품은 아님