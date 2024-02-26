```bash
sudo yum install docker -y
```

```bash
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
sudo chmod 666 /var/run/docker.sock
```
## docker-compose 설치
```bash
# Docker Compose 1.27.2 버전 설치
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# 바이너리에 실행 권한 추가
sudo chmod +x /usr/local/bin/docker-compose

# Docker Compose 설치 확인
docker-compose -v
```
