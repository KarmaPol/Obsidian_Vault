- 영속성 컨텍스트에 엔티티 넣어서 DB에 커밋
- usePersist() - true 시 persist(), false시 merge()
	- 생성은 persist, 수정은 merge
- **reWriteBatchedInserts=true** -> 멀티 밸류 한번에 인서트

- 데이터 수정은 JPA ItemCusorReader가 Page보다 유리.
	- 기본 JPAItemPageReader는 flush()처리해 데이터 중복, 누락 등 문제 생길수 있음