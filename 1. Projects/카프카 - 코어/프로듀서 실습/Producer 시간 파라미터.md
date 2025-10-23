- delivery.timeout.ms >= linger.ms + request.timeout.ms
	- delivery.timeout 
	  producer 메시지 전송 자체의 최대 시간
	- request.timeout
	  전송에 걸리는 최대 시간
	- linger
	  Sender thread의 배치 대기 시간
- max.block.ms
  main 스레드 -> sender 스레드 최대 대기 시간

- **일반적으로 retires 변수를 조정하기 보단 MAX로 잡고, delivery.timeout으로 조절**
	- 최대 delivery.timeout 시간은 2분 내외