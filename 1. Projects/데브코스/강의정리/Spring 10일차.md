## Aspect Orient Programming
관점 지향 프로그래밍
부가 기능을 코드 수정 없이 핵심 기능에 추가 가능
### 적용 방법
- **컴파일 시점**
  컴파일 시점에 부가 기능 소스 코드 삽입
- **클래스 로딩 시점**
  클래스 로딩 시점에 Binary화된 코드 삽입
- **런타임 시점**
  Proxy를 이용해 런타임에 부가 기능 실행
### Spring AOP
스프링은 proxy를 이용해 런타임에 적용
- **JDK Proxy**
  interface 기반
- **CGLib Proxy**
  class 기반
### Spring Proxies
#### InvocationHandler
```java
class LogginInvocationHandler implements InvocationHandler {
	private static final Logger log = LoggerFactory.getLogger(LoggingInvocationHandler.class);
	private final Object target;

	@Override
	public Objcet invoke(Object proxy, Method method, Object[] args) throws Throwable {
		log..info("{}", method.getName());
		return method.invoke(target, args);
	}
}

// 메인함수
Calculator proxyInstance = (Calculator) Proxy.newProxyInstance(
	LoggingInvocationHandler.class.getClassLoader(),
	new Class[]{Calculator.class},
	new LoggingInvocationHandler(calculator));

proxyInstance.add(1, 2); // Calculator의 add 함수와 프록시 invoke 실행
)
```
Java에서는 InvocationHandler을 implement해 프록시 객체를 만들수 있다
### @AspectJ
#### 주요 용어
- **타겟**
  핵심 기능을 담고 있는 모듈로 부가기능 부여의 대상
- **조인 포인트**
  어드바이스가 적용될 수 있는 위치
  타겟 객체가 구현한 인터페이스의 모든 **메서드**
- **포인트 컷**
  어드바이스를 적용할 타겟의 메서드를 선별하는 **정규표현식**
- **어드바이스**
  타겟의 특정 조인 포인트에 제공할 **부가기능**
  @Before, @After, @Around, @AfterReturning, @AfterThrowing 등
- **애스펙트**
  어드바이스 + 포인트컷
  스프링에서는 Aspect를 빈으로 등록해 사용

- **위빙**
  타겟 조인 포인트에 어드바이스를 적용하는 과정
#### Spring AOP 코드
- 그래들
```java
implementation 'org.springframework.boot:spring-boot-starter-aop'
```

```java
@Aspect  
@Component  
public class LoggingAspect {  
	private final Logger log = LoggerFactory.getLogger(LoggingAspect.class);  
	// [어드바이스]([포인트컷 키워드]([접근자][리턴 타입][패키지][파일명][메소드명]([파라미터])))
	@Around("execution(public * com.pgms.part1..*Repository.*(..))")  
	public Object log(ProceedingJoinPoint joinPoint) throws Throwable {  
		log.info("Before repo method");  
		Object result = joinPoint.proceed();  
		log.info("After repo method => {}", result);  
		return result;  
	}  
}
```
포인트컷 패키지 지정시 com.package..* 과 같이 ..키워드로 모두 지정 가능
- **within 포인트컷**
  within(com.ex.spring.ch3.MyService)
  MyService class의 모든 메소드와 매치
##### 포인트컷 사전 정의
```java
@Pointcut("execution(public * com.pgms.part1..*Repository.*(..))")
public void servicePointCut(){}

// 사전에 정의한 servicePointCut() 사용
@Around("servicePointCut()")  
public Object log(ProceedingJoinPoint joinPoint) throws Throwable {  
	log.info("Before repo method");  
	Object result = joinPoint.proceed();  
	log.info("After repo method => {}", result);  
	return result;  
}
```
사전에 어노테이션으로 정의한 PointCut을 사용할 수 있다
다른 클래스의 PointCut도 참조 가능하다
#### 어노테이션으로 포인트컷 범위 지정
- 임의 어노테이션 생성
```java
@Target(ElementType.METHOD)
@Retention(RetentionType.RUNTIME)
public @interface Tracktime(){
}


// LoggingAspect.class

@Around("@annotation(org.pgms.kdt.aop.Tracktime)")
public Object log(ProceedingJoinPoint joinPoint) throws Throwable {  
	log.info("Before repo method");  
	Object result = joinPoint.proceed();  
	log.info("After repo method => {}", result);  
	return result;  
}


// Voucher.class

@Tracktime
public Voucher insert(Voucher voucher){
	storage.put(voucher);
	return voucher;
}
```
위 코드에서 @Tracktime 어노테이션을 단 메소드를 AOP 범위로 지정
## Spring Transaction 관리
**PlatformTransactionManager** 인터페이스를 상속하여
JDBC의 경우 **DataSourceTransactionManager**, Hibernate는 **HibernateTransactionManger를**
구현한 **JDBC/Connection**, **Hibernate/Transaction** 구현체로 트랜잭션을 관리한다
#### PlatformTransactionManager 빈등록
```java
@Bean
public PlatformTransactionManager platformTransactionManager(Datasource  dataSource) {
	return new DataSourceTransactionManager(dataSource);
}
```
#### 롤백/커밋
```java
var transaction = transactionManager.getTransaction(new DefaultTransactionDefinition());
try {
	jdbctemplate.update(sql1);
	jdbctemplate.update(sql2); // 이때 sql1 실행 후 sql2 실행 시 예외 발생하는 상황
	transactionManager.commit();
}
catch(Exception e){
	log.info(e);
	transactionManager.rollback(transaction); // 예외가 발생하면 롤백
}
```
### TransactionTemplate
JdbcTemplate과 마찬가지로 Transaction도 try catch문 대신 사용 가능
```java
transactionTemplate.execute(new TransactionCallbackWithoutResult(){
	@Override
	protected void doInTransactionWithoutResult(TransactionStatus status){
		jdbc.update(sql1);
		jdbc.update(sql2);
	}
});
```