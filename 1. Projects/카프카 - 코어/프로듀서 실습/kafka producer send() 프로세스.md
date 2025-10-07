1. 메인 Thread - send()
   별도 스레드에 위임하고 끝
2. 비동기로 별도 Thread에서 처리.
	1. Serializer
	2. Partitioner
	   파티션 마다 배치 단위로 모아서 전송
	3. Sender