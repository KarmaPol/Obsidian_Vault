## 보안 그룹
NACL과 함께 방화벽의 역할을 하는 서비스
Port 허용
- 기본적으로 모든 포트는 비활성화
- Deny는 불가능 -> NACL은 가능
인스턴스 단위
Stateful -> 알아서 아웃바운드 처리
## 네트워크 ACL(NACL)
방화벽 역할
서브넷 단위
포트 및 아이피 직접 Deny
Stateless -> 아웃바운드 직접 처리해줘야함
### NACL 규칙
규칙 번호 : 고유 숫자, 규칙이 평가되는 순서
- 작은 순서부터 평가, 매칭되면 빠져나가고 끝
## NAT
public subnet의 NAT가 private subnet에 외부 인터넷을 **대신** 연결
