## GRPC
구글에서 개발한 오픈소스 고성능 RPC 프레임워크
### RPC
다른 주소공간에서 명령을 수행할때 마치 자신의 코드를 실행하는 것처럼 작동
### 스텁
객체를 메시지로 변환/역변환하는 레이어
서버와 클라이언트간의 언어가 달라도 요청과 응답을 구현할 수 있음
### 프로토콜 버퍼
구조화된 데이터를 직렬화하기 위한 메커니즘
JSON과 유사하나 더 작고 간단함 (binary protocol)
### GRPC 구조
애플리케이션, 프레임워크, 전송 계층으로 구성
GRPC CORE 계층이 HTTP 2.0 위에 올라가 있음
### GRPC 채널
서브 채널을 열고 재사용하므로 통신 비용 절약
### gRPC 장점
MSA에 적합
지연시간 감소에 강력한 장점
양방향 통신 가능
언어에 구애받지 않음
JSON 기반 통신 보다 가벼움
REST보다 처리량 3배, CPU 고려시 처리량 11배 차이
