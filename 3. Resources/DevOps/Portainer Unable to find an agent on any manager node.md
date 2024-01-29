### 참고
https://github.com/portainer/portainer/issues/2015
### 해결책
```
docker stack rm [스택이름]
docker stack deploy -c [스택설정파일] [스택이름]
```
연결 실패로 인한 일시적 오류 -> 스택 재실행으로 해결