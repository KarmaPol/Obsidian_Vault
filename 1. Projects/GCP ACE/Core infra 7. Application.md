## Cloud Run
- 관리형 배포 서비스
- 서버리스
- 쿠버네티스 기반
- 매우 빠르게 automatically 스케일링 -> 효율적인 요금
### 과정
1. write your code
2. build to image
3. deploy to cloud run
   https 터널링까지 자동으로 지원
### BuildPack
소스 코드 채로 업로드 해도 buildpack으로 자동 이미지 빌드 -> 배포
### 요금 계산
특이하게 계산 (람다와 유사)
요청을 처리할때, 서버 생성, 서버 종료 시에만 요금 부과
vCPU, memory에 따라 차등
Java, Python, Node, PHP, C++, Cobol, Haskell, Perl 등 유명 언어 지원
## 이벤트 기반
**Cloud Functions**(= 람다)
- 이벤트가 발생할때만 실행
- 경량, 비동기, 이벤트 기반
- single, small functions에 적합
- 100milliseconds 단위로 사용중일 때만 요금부과
- node, python, go, java, .net, ruby, php 지원
- cloud storage 이벤트, pub/sub이 비동기적으로 트리거 혹은 http 호출로 동기 실행