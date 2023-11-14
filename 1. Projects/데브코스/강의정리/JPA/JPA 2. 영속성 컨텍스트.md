### EntityManager
#### Entity
RDB의 Table과 매핑되는 객체
#### EntityManagerFactory
Entity를 관리하는 EntityManager 공장
Thread Safe
### EntityManager
엔티티를 CRUD하는 Entity와 관련된 모든 일 처리
Thread Safe하지 않음. 동시성 이슈 발생 가능
### 영속성 컨텍스트
- JPA를 이용하는데 가장 중요한 요소
- 엔티티를 영구 저장하는 환경
- 엔티티 매니저는 엔티티를 영속성 컨텍스트에 보관하고 관리
### 영속성 컨텍스트의 특징
- 엔티티는 식별자 값을 반드시 가져야 함
- key-value로 엔티티 관리
- 트랜잭션 커밋시 영속성 컨텍스트 변경 내용을 DB에 반영 (flush)
### 엔티티 생명주기
- 비영속 (new/transient) 영속성 컨텍스트와 전혀 관계가 없음
- 영속 (managed) 영속성 컨텍스트에 저장된 상태
- 준영속 (detached) 영속성 컨텍스트에 저장되었다가 분리된 상태
- 삭제 (removed) 삭제된 상태
