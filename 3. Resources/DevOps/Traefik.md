https://velog.io/@johnsuhr4542/Traefik-on-Docker
- GoLang 경량 고성능 웹 서버
- Let's encrypt 내장으로 https 매우 쉬움
#### traefik.yml - traefik 설정 파일
```yml
# traefik.yml
log:
  level: error

global:
  checkNewVersion: true
  sendAnonymousUsage: true

accessLog:
  filePath: "/var/log/traefik/traefik.log"
  bufferingSize: 100
  filters:
    statusCodes:
      - "200-530"

entryPoints:
  http:
    address: ":80"
  https:
    address: ":443"
  # 기본적으로 대시보드를 지원합니다
  traefik:
    address: ":5000"

api:
  dashboard: true
  insecure: true

providers:
  docker:
    exposedByDefault: false
    swarmMode: false
    endpoint: "unix:///var/run/docker.sock"
  file:
    watch: true
    filename: "/etc/traefik/dynamic_conf.yml"

# TLS 인증
certificatesResolvers:
  letsencrypt:
    acme:
      email: [YOUR_EMAIL]
      storage: "/etc/traefik/acme.json"
      httpChallenge:
        entryPoint: "http"
```
#### dynamic_conf.yml - 라우팅, 미들웨어 설정
```yml
# dynamic_conf.yml
http:
  services:
    greeting:
      loadBalancer:
        servers:
          - url: "http://host.docker.internal:8080"
          - url: "http://host.docker.internal:8081"

  routers:
    # 대시보드용 라우팅
    traefik-api:
      entryPoints: ["traefik"]
      rule: "PathPrefix(`/api`) || PathPrefix(`/dashboard`)"
      service: api@internal

    # NGINX 의 location 에 해당
    greeting-http:
      entryPoints:
        - http
      rule: "Host(`{domain}`)"
      service: greeting
```
#### acme.json - https 인증 파일
```sh
$ touch acme.json
$ sudo chmod 600 acme.json
```
```yml
# docker-compose.yml
version: "3.3"

services:
  reverse-proxy:
    image: traefik:v2.7.0
    container_name: reverse-proxy
    restart: always
    extra_hosts:
      - "host.docker.internal:host-gateway"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock:ro"
      - "/etc/localtime:/etc/localtime:ro"
      - "./traefik/traefik.yml:/etc/traefik/traefik.yml:ro"
      - "./traefik/dynamic_conf.yml:/etc/traefik/dynamic_conf.yml"
      - "./traefik/acme.json:/etc/traefik/acme.json"
    ports:
      - "80:80"
      - "443:443"
      - "5000:5000" # dashboard
```
#### docker-compose deploy
```
docker stack deploy -c docker-compose.yml traefik
```

- traefik이 도메인 까지 자동 발급해주는 것은 아니다
- 도커 스웜, 네트워크에 대해 추가적인 공부가 필요하다
- host.docker.internal로 manager node의 ip 주소를 참조하더라도 인그레스 네트워크에 의해 로드밸런싱은 동작해야 한다
  -> 로드 밸런싱이 동작하지 않는 것은 도커 스웜 인그레스 네트워크 자체에 문제가 있다
#### 로드 밸런싱 문제 해결
- 스웜에 필요한 포트를 열어줘야 한다
https://docs.docker.com/engine/swarm/swarm-tutorial/#open-protocols-and-ports-between-the-hosts
https://xn--os5ba3q.com/162
#### 스웜 핏 워커 노드 모니터링 안되는 문제
https://github.com/swarmpit/swarmpit/issues/560
```
I have finally found a solution to this issue.  
You need to include the `--advertise-addr` flag with the 'docker swarm join' command.  
For example: `docker swarm join --token <manager-node-token> <manager-node-ip>:2377 --advertise-addr <worker-node-external-ip>`
```