[[TDD]]
# TDD를 어떻게 시작할까
## Mockist 관점
- Presentation 계층부터 아래 레이어는 전부 Mock
- 다음은 Service, Persistence 계층의 테스트를 단계적으로 작성한다
## Classic TDD 관점
- 계층적 테스트는 비슷하지만, Mock이 아닌 Stub으로 하드코딩해 시작
  -> 통과부터 하고 적절한 메서드로 교체
- 만약 UI를 테스트를 한다면,
  feature에 실제 도메인 객체를 가져온 뒤에 UI로 보내 테스트한다
- 도메인 모델과 로직에 먼저 집중할 수 있음
## 공통점
- 레이어 별로 차례대로 테스트를 작성하라