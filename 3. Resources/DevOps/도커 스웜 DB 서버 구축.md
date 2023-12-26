https://seongjin.me/docker-swarm-services/

- 도커 볼륨 타입
1. volume : 도커 볼륨을 컨테이너 안에 마운트 (주로 사용)
2. bind : 호스트 특정 경로나 파일을 컨테이너 안에 직접 마운트 
   -> 노드 별로 파일 존재하므로 오케스트레이션에 적합하지 않다
3. tmpfs : 임시 파일 스토리지 마운트
4. npipe : named pipe 마운트, 윈도우 기반 컨테이너만 가능

```bash
docker service create --name nginx \
  --replicas 3 \
  --mount type=volume,source=html,destination=/usr/share/nginx/html,volume-label="type=html" \
  nginx
```