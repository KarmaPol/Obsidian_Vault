## Cloud 특징
1. Customers get resource on-demand and self-service
2. get access from anywhere
3. provider allocates resources to users out of the pool
4. Resources are flexible
5. Customers pay only for what they use
## IaaS and PaaS
### IaaS
- Raw compute
- Storage
- Network capabilities
  -> Pay for allocate
### PaaS
- Libraries (ex. Google App Engine)
  -> Pay for what they use
## 클라우드의 진화
### Managed Resources, Managed Services
more quickly and reliably
### Serverless
Infra 필요성의 제거 (람다)
Cloud Functions (이벤트 기반, pay as you go service)
Cloud Run (microservice 컨테이너 관리)
### SaaS
Entire Service 제공
클라우드에만 연결되면 서비스 이용 가능
Gmail, Gdrive..
## Location
- Latency
- Availability
- Durability
-> Location(ex. EU)/ Region(ex. europe-west2)/ Zone(ex. eu-west-2a)
=> 몇몇 서비스(ex. Cloud Spanner)는 복제해서 여러 Region에 분산 저장
## Security
### Hardware infra layer
서버 보드, 네트워크 장비
OS image, 커널 등
Data Center 접근 통제
### Service deployment layer
데이터 센터 내 서비스간 RPC traffic 자동 암호화
### User Identify layer
구글 로그인
### Storage Services layer
저장 매체 암호화 (Key)
### Internet Communication layer
Google Front End(GFE) -> TLS 통신, CA 등 암호화, 보호 제공
Denial of Service(DOS) -> DoS 공격 방어, GFE 보조
### Google Operational Security layer
Intrusion detection
Reduce insider risk
Employee Universal Second Factor use
Software development practices
-> ex) 버그 발견시 포상 캠페인
## Open Source Ecosystem
특정 벤더에 갇히지 않게 하고자, EcoSystem을 오픈소스로 제공 (Kube, TensorFolow, Operations Suite-모니터링툴)
## Pricing
**Per-second billing**
월 25퍼 이상 사용 시 할인
**Custom virtual machines**
pricing calcuator

갑자기 비용이 너무 많아지면?
Budget 설정, 한계치 알림, Reports 모니터링, Quotas (에러, 공격에서 방어)
### Quotas
1. Rate Quotas - 특정 시간 동안 측정 이후 리셋
2. Allocation Quotas - 갯수 제한

