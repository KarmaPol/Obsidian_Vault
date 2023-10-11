## Dependency Injenction
### Dependency Resolution Process
Application Context에 의해 Bean Injection 주입
### Circular Dependency
A->B->A 참조 시 순환 참조으로 인해 오류 발생
### 컴포넌트 스캔
스프링이 직접 클래스를 검색해서 빈으로 등록해주는 기능
StereoType 어노테이션(@Component, @Repository, @Service, @Controller, @Configuration)
으로 검색 대상 지정
- **@ComponentScan(basePackages = {"패키지1", "패키지2"})**
- **@ComponentScan(basePackageClasses = {A.class, B.class})**
  어노테이션으로 스캔 범위를 패키지, 클래스 단위로 지정할 수 있다
- **@ComponentScan(
  excludeFilters = { @ComponentScan.Filter(type= FilterType.ASSIGNABLE_TYPE, 
  value = MemoryVoucherRepository.class)})**
  스캔된 컴포넌트 중에 사용하지 않을 컴포넌트를 지정할 수 있다
## Autowired
IOC 컨테이너에 의해 자동으로 빈 주입

Spring에 의해 자동으로 @Autowired가 붙지만,
생성자가 2개 이상일때는 @Autowired 어노테이션을 명시해주어야 한다
### 왜 생성자 주입 방식이 좋은가
- 초기화 시에 필요한 모든 의존관계가 형성되기 떄문에 안전하다
- 잘못된 패턴을 찾을 수 있게 도와준다 (지나치게 큰 생성자는 너무 많은 책임)
- 테스트를 쉽게 해준다 (mock 객체를 쉽게 주입할 수 있다)
- final 키워드로 불변성을 확보한다
### 동일 Bean이 여러 개 일때
- 우선순위가 명확할때
```java
@Repository
@Primary
public class MemoryRepository
```
- 우선순위가 같을때
```java
@Repository
@Qualifier("memory")
public class MemoryRepository

@Repository
@Qualifier("jdbc")
public class JdbcRepository

// 서비스 단
@Service
public class VoucherService{
	public VoucherService(@Qualifier("memory") Repository repository){
		...
	}
}
```
@Qualifier 어노테이션으로 Bean 선택 가능

Bean을 여러개 만들어서 선택할 경우는 그렇게 많지 않다
-> Configuration도 컴포넌트이기 때문에 Configuration파일을 여러개 만들어서 선택한다