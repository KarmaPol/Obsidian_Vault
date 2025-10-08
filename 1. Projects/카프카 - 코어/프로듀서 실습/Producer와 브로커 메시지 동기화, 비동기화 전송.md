- 동기방식
  send() 후 get() 호출해 ack 메시지까지 기다림
- 비동기방식
  ack 메시지 오면 callback 호출
	- 카프카는 기본적으로 비동기 호출
	- Sender 스레드에서 onCompletion 메서드로 콜백\
	- 주로 비동기 방식 사용