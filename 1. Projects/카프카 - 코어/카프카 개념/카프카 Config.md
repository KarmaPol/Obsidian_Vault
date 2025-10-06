# Config 구분
1. Broker, Topic 레벨 Config
	1. 카프카 서버에서 설정
	2. server.properties 변경시 재기동 필요
2. Producer, Consumer 레벨 Config
	1. 클라이언트에서 설정
	2. 클라이언트 수행시마다 설정 가능
---
- Broker, Topic config 조회/변경 가능
	- kafka-configs --descrribe
	- kafka-configs --alter
	- kafka-configs --delete