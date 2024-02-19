## VPC
virtual public cloud
public / private
- 서브넷 내 요소 연결 - 경로 지정 가능
- 여러 region에 걸쳐 생성 가능
- 방화벽 설정 가능
## Compute Engine
- 버츄얼 머신
- 상황에 따른 다양한 조건 제공
- 클라우드 콘솔, api, cli로 생성 가능
- 리눅스, 윈도우 이미지 생성 가능
- 다른 운영체제로 유연하게 재생성 가능
-> 1분 마다 요금 계산, 월 25 퍼센트 이상 사용 시 할인
### Preemptible & Spot VM
VM을 껐다 켰다, Spot(제한 X) > Preemptible(제한)
### Custom Engine
미리 사용할 것으로 지정한 machine에 대해서만 요금 부과
## AutoScaling
traffic에 따라 자동으로 VM 갯수 조절
일반적으로 스케일업(인메모리 DB, CPU기반 모니터링)보다는 스케일 아웃
## VPC compatibilities
- 라우팅 테이블
- 방화벽으로 인바운드, 아웃바운드 rule 지정 가능
- **VPC peering** -> VPC 간 traffic 공유
	또는 IAM으로 **VPC share** 가능
## Cloud load balancing
mulitple 인스턴스가 있을 때 트래픽을 분할
- fully distributed, software 기반, 관리형 서비스
- 다양한 프로토콜에 대해 제공(HTTPS, TLS, UDP)
- multi region
## Cloud DNS
8.8.8.8 구글 dns 서버 무료로 제공
유사하게 구글 cloud내 서비스에 대해 Cloud DNS로 관리형 서비스 제공
-> cloud console, api, cli를 통해 관리, 프로그래밍 가능
## Cloud CDN
- low network latency
- save money
- origin 호출 감소
## Connecting VPC network 방법
1. cloud vpn
   터널 연결 제공
   Cloud router로 동적 연결 제공
   Border Gatewary Protocol로 VPN으로 VPC-네트워크 간 교환 제공
   대역폭 문제로 항상 best는 아님
2. Direct Peering
   같은 데이터 센터에 라우팅
3. Carrier Peering
   직접 연결 제공 -> 구글 서비스 레벨에 의해 통제되지 않음
4. **Dedicated Interconnect**
   google에 private connection 제공
   99.99퍼센트 SLA, VPN에 의해 연결 회복 가능
5. Partener Interconnect
   dedicated 연결이 불가능 할때 유용
   초당 10기가 전송이 필요없을때 유용
   mission-critical한 작업에 유용
   99.99퍼센트 SLA
6. Cross-Cloud Interconnect
   구글과 다른 클라우드 서비스 연결시 유용
   초당 10기가, 100기가 연결 제공