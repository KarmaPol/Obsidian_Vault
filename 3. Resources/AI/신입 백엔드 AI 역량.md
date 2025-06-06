# 신입 백엔드 개발자를 위한 성장 가이드

회사에 막 입사한 백엔드 신입 개발자가 아래 4가지 역량을 어떻게 기를 수 있는지 구체적인 방법을 소개합니다.

---

## 1. 🧠 AI 도구 활용 능력

**ChatGPT, GitHub Copilot, IntelliJ AI 플러그인 등**을 코드 작성/검토에 활용하는 능력

### 실무 적용 포인트
- 익숙하지 않은 코드/로직 요약 설명 받기
- 테스트 코드 자동 생성 요청
- 네이밍/리팩터링/주석 정리에 활용

### 학습 방법
- GitHub Copilot으로 자동완성 기능 적극 사용
- ChatGPT에게 기능 명세를 주고 테스트 코드나 구현 코드 요청
- 예시 프롬프트:
  "아래 요구사항에 따라 Java Spring 기반 컨트롤러와 서비스 코드를 생성해줘.  
  - 로그인한 유저의 ID로 알림 목록을 조회  
  - 30일 이내 알림만 반환  
  - 최신순 정렬"

### 추천 자료
- Prompt Engineering Guide: https://www.promptingguide.ai/
- GitHub Copilot Labs 확장
- 도서: *You Look Like a Thing and I Love You*

---

## 2. 🔍 코드 검토 및 검증 능력

**좋은 코드와 나쁜 코드의 차이**를 알고, 리뷰를 통해 피드백을 줄 수 있는 능력

### 실무 적용 포인트
- PR 올릴 때 자기 코드에 자기 리뷰 달기
- 시니어 개발자 리뷰를 정리하며 학습
- 리팩터링 전후 차이를 문서화해보기

### 학습 방법
- 리팩터링한 이유를 주석 또는 메모로 정리
- 시니어 리뷰 기록 노트 작성 (왜 저 리뷰가 나왔는지)
- 코드 품질 기준 익히기: 가독성, 네이밍, 책임 분리 등

### 추천 자료
- 도서: *Clean Code*, *Refactoring*
- Google Code Review Guide: https://google.github.io/eng-practices/review/
- Refactoring Guru: https://refactoring.guru/

---

## 3. 🏗 시스템 설계 및 가이드라인 제시 능력

아키텍처 수준이 아닌 **API 흐름, 모듈 연결 구조, DB 설계 이유**에 대한 이해부터 시작

### 실무 적용 포인트
- API 호출 흐름을 시퀀스 다이어그램으로 시각화
- ERD 이해 및 테이블 구조 분석
- 신규 기능 요구사항을 작은 단위로 쪼개 설계

### 학습 방법
- 컨트롤러 → 서비스 → DB 흐름 정리
- 기존 기능 하나를 해체해서 흐름 문서화
- 간단한 예시로 설계 연습 (예: 사용자 피드백 API 설계)

### 추천 자료
- 도서: *시스템 설계 면접 완전 정복*
- System Design Primer: https://github.com/donnemartin/system-design-primer

---

## 4. 🧭 좋은 소프트웨어 엔지니어링 관행

**테스트, 문서화, 배포 자동화, 로깅, 모니터링** 등의 관행을 체득하는 것

### 실무 적용 포인트
- 기능 PR에 테스트 코드 추가 + README 작성
- 로그 레벨(trace/info/error 등) 적절히 사용
- CI/CD 파이프라인 관찰하고 작은 수정 실습

### 학습 방법
- 본인이 구현한 기능 테스트 코드 작성 습관화
- Postman으로 API 문서 수동 작성
- GitHub Actions로 간단한 CI 구성 실습 (build → test → lint)

### 추천 자료
- 도서: *The Pragmatic Programmer*
- 12 Factor App: https://12factor.net/
- GitHub Actions 튜토리얼

---

## 📅 신입 개발자 주간 루틴 예시

| 항목           | 매일 해야 할 일                         | 주 1회 정리                          |
|----------------|------------------------------------------|--------------------------------------|
| AI 도구        | Copilot 활용 / GPT 질문                 | 유용했던 프롬프트 정리               |
| 코드 검토      | PR 자기 리뷰                            | 시니어 리뷰 패턴 기록                |
| 시스템 흐름    | 호출 흐름 메모                          | 시퀀스 다이어그램 작성               |
| 엔지니어링 관행 | 테스트/로깅 추가                        | GitHub Action 실습 or 문서화 정리    |

---

## 🎯 신입 개발자 마인드셋

| 키워드 | 설명 |
|--------|------|
| 🔎 관찰 | 코드, 시스템, 리뷰를 ‘왜 이렇게 했는지’ 기준으로 바라보기 |
| 🧪 실험 | 작은 테스트라도 자주 해보고 직접 오류를 겪기 |
| ✍️ 문서화 | 배운 것/알게 된 것/궁금한 것 정리하는 습관 |
| 💬 질문 | 무작정 물어보지 않고, 사전 조사 후 질문 ("제가 이렇게 이해했는데 맞나요?") |

---
