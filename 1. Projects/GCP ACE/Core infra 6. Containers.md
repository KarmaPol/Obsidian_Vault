## 컨테이너
- **independent** workload scalability
- OS and hardware abstraction layer
- dependencies 갖는 invisible box 
- VM 보다 훨씬 빠르게 구축 및 실행
- 컨테이너 실행 시 OS kernel 만 필요
- PaaS 처럼 스케일링, IaaS처럼 유연성
## 쿠버네티스
- open source platform for managing containerized service
- 컨테이너 오케스트레이션 툴로 매우 용이
- node, container 배포 API의 집합체
- 컨트롤 패널과 워커 노드로 나뉨
- 어플리케이션이 서로 어떻게 상호작용하는지 설정 가능
### Pod
- 가장 작은 배포 단위
- 일반적으로 1 컨테이너 당 1 팟
```
kubectl run
```
### 배포
- 어플리케이션 단위 배포
### 실행중인 pod 목록
```
kubectl get pods
```
### 서비스
서비스는 여러개의 pods이 fixed IP로 묶여서 로드밸런싱
- 서비스 목록 조회
```
kubectl get service
```
- 서비스 pod 갯수 조정
```
kubectl scale
```
### deployments
도커 컴포즈와 유사하게 yml로 미리 작성
```yml
# deploy
kubectl get deployments

# update
kubectl apply -f nginx-deploy.yaml
```
### 무중단 배포
```
kubectl rollout

or

yml파일 에서 strategy: rollingUpdate 옵션 조정
```
## GKE
- 구글 쿠버네티스 엔진
- 관리형 쿠버네티스 서비스 - 쿠버네티스 클러스터
### 기능
- 로드밸런싱
- node pools to designate subsets of nodes
- 오토매틱 스케일링
- 자동 업데이트
- 자동 node 수정
- 로깅 및 모니터링
```bash
gloud container clusters create k1
```