## VPC
- 가상의 데이터센터
- 외부에 격리된 네트워크 컨테이너 구성 가능
## VPC 구성 요소
### 서브넷
VPC  하위 단위로 VPC에 할당된 IP를 더 작은 단위로 분할 
**하나의 서브넷은 하나의 가용 영역안에 위치**
#### AWS 서브넷 IP 갯수
5개를 제외하고 계산
예) 10.0.0.0/24 라면, 32 -24 = 8
- 10.0.0.0: 네트워크 어드레스
- 10.0.0.255: 브로드 캐스트
- 10.0.0.1~3: aws 할당
#### 서브넷 종류
- 퍼블릭 서브넷
	  외부에서 인터넷을 통해 연결할 수 있는 서브넷 (웹서버, 어플리케이션 서버)
- 프라이빗 서브넷
	  **외부에서 인터넷을 통해 연결할 수 없는 서브넷** -> 보안성
	  퍼블릭 IP 부여 불가능
	  DB, 로직 서버 등 외부에 노출 될 필요가 없는 인프라
### 라우트 테이블
트래픽이 어디로 가야하는지 안내
### 인터넷 게이트웨이
VPC가 외부의 인터넷과 통신할 수 있도록 경로를 만듬
확장성, 고가용성
IPv4의 경우 NAT 역할
Route Table에서 경로 설정 후에 접근 가능
	 라우트 테이블에 목적지 ip가 없으면 인터넷 게이트웨이 -> 외부로 요청 보냄
