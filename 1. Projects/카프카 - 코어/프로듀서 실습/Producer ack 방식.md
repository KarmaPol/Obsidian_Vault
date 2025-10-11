1. **acks 0**
   ack를 기다리지 않고 다음 메시지. 가장 빠름(IOT 센서, 메시지 소실 민감하지 않을때 사용)
   실제 동작 시 offset = -1으로 나옴
2. **acks**
   leader 만 ack, 복제중 leader 다운 시 메시지 소실
3. **acks all**
   복제 모두 마무리된 뒤에 ack. 안정성 뛰어남

- callback 기반 Async 방식(디폴트)에서도 ack 설정에 기반해 retry 수행
	- 비동기 retry 시 순서 뒤바뀔수 있음