## Level
1. Resources - virtual machines, cloud storage
2. Project
3. Folder - ex) 금융, HR, 법무 등으로 부서별 나누어 관리
4. Organization node - 특수 organization role 결정 (돈 쓸수 있는)
### Policy
Policy 종류에 따라 어떤 레벨에 적용할 수 있는지 달라짐
하위 레벨은 상위 레벨 Policy 상속
## IAM
policy를 account 별로 관리 - 보통 account는 이메일
허용 policy, 거부 policy 설정 시 하위 resource에 상속
### 3 Roles in IAM
- **Basic role**
  넓은 범위의 role
  Owner, Editor, Viewer, Billing Admin
- **Predefined role**
  특정 compute engine 종류에 할 수 있는 행동을 미리 지정
- **Custom role**
  ex) least-privilege 모델, 인스턴스를 실행할 최소의 권한을 부여
	**커스텀 롤 유의사항**	
	1. 커스텀 롤 생성시 생성된 permission을 관리해야함
	2. 커스텀 롤은 프로젝트, Org. 레벨만 적용 가능
## Service Accounts
**특정 서비스에만 접근** 가능한 계정
Compute Engine은 create, delete, update 가능하나, Storage엔 접근 불가
**서비스 계정에도 IAM 적용 가능** - 같은 서비스 계정이라도 Viewer, Editor 제한
## Cloud Identity
- 유저 권한을 그룹별로 관리
- 같은 이름을 가진 유저가 있는지 로그
- 무료/ 유료 기능 차이 -> 구글 워크 스페이스 사용 시 기본적으로 제공
## Google Cloud 접근 방법
### Google Cloud Console
   GUI 제공, 간단한 웹기반 인터페이스 -> 모든 기능 제공
   리소스 찾기 편하고 health 체크 간편, full access, SSH 쉘 접속 가능
### Google Cloud SDK
리소스 관리를 위한 툴 제공
- Google cloud cli - provide main command-line interface
- bq - command for BigQuery
### APIs
Cloud를 관리하기 위한 API 제공
유저 인증이 필요한 경우도 API 활용 가능
### Google Cloud App
- Stop, Start, use SSH, log
- SQL 인스턴스 관리
- App Engine 롤백 등 관리
- billing 알림
- key metrics alerts
  
