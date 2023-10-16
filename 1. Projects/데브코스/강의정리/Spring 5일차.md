## 로깅
시스템 작동 상태의 기록과 보존, 이용자 습성 조사 및 시스템 동작의 분석을 위해 정보를 기록
버그를 수정하기 위해 필수적

println()으로 일일히 콘솔로 찍으면 저장도 어렵고, 성능에 큰 영향
### SLF4J
퍼사드 패턴으로 여러 Logging Framework들을 추상화
### 로그 레벨
1. trace
2. debug
3. info
4. warn
5. error
error 레벨로 로그레벨을 조회시 trace 레벨은 조회 X
### logback 설정
로깅 설정은 실제 라이브러리인 logback의 설정을 해줘야한다
- **logback 설정파일 찾는 순서**
1. logback-test.xml (테스트 코드 우선, test/resources)
2. 없으면 logback.groovy (main/resources)
3. 없으면 logback.xml
4. 없으면 기본 설정인 BasicConfiguration
각 logger 클래스 별로 레벨을 다르게 설정 가능
