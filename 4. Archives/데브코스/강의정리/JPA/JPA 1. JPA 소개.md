### 마이바티스
Jdbc, Jdbc template의 경우, 코드 내에 sql문이 있어 유지보수가 어려움 -> Sql을 따로 관리하자
interface에서 어노테이션 또는 Xml 파일로 sql과 매핑
-> Sql result는 POJO 객체에 바인딩해 가져올 수 있음
### JPA
Java의 대표적인 ORM
update는 save()를 호출하지 않아도 dirty checking
#### 환경 세팅
```java

@Bean
public DataSource dataSource(){
...
	return dataSource;
}

// Jpa 벤더 설정, 일반적으로 hibernate
@Bean
public JpaVendorAdapter jpaVendorAdapter(JpaProperties jpaProperties){
	AbstractJpaVendorAdapter jpaVendorAdapter = new HibernateJpaVendorAdapter();
	jpaVendorAdapter.set(jpaProperties.jpaProperties.getDatabasePlatform());
}

// Entity Manger 설정, datasource, jpa 벤더, 프로퍼티 등 주입
@Bean
public LocalContainerEntityMangerFactoryBean entityMangerFactory(DataSource datasource, JpaVendorAdapter jpaVendorAdapter, JpaProperties jpaProperties) {
	LocalContainerEntityMangerFactoryBean em = new LocalContainerEntityManagerFactoryBean();
	em.setDataSource(dataSource);
	em.setJpaVendorAdapter(jpaVendorAdapter);
	...
	em.setJpaProperties(properties);
	
	return em;
}

// 트랜잭션 매니저 설정
@Bean
public PlatformTransactionManager transactionManager(LocalContainerEntityMangerFactoryBean entityManagerFactoryBean) {
	JpaTransactionManager transactionManager = new JpaTransactionManager();
	transactionManager.setEntityMangerFactory(entityMangerFactory.getObject());
	return transactionManager;
}
```
@AutoConfiguration이 자동으로 설정해주지만, Bean 설정을 직접 해줄 수도 있다.