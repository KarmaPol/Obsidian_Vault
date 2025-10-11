# 전송 과정
- Serialize -> Partitioning -> Compression(선택) -> Record Accumulator(배치 단위로 저장) -> Sender Thread
	- Accumulator에 배치 단위로 여러 레코드 저장
	- buffer.memory 만큼 저장
	- buffer.size 단일 배치 사이즈
	- linger.ms 까지 대기
	  반드시 0보다 크게 설정할 필요없음
	  전송이 매우 빠르면 linger.ms가 0이어도 무방
		- **단, 전반적으로 전송이 느리다면 20ms 권장**
