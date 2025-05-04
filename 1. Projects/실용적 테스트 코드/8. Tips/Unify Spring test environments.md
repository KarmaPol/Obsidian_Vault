# @SpringBootTest
- Environment is created **by each test class profile**
  -> Increase test time
# Create a common support class for bean injection
```java
@SpringBootTest
class IntegrationTestSupport {
	@Autowired
	private OrderStatisticsService orderStatisticsService;

	@Autowired
	private OrderRepository orderRepository;
}
```

[[@Mock VS. @Spy VS. @InjectMock]]
[[@Mockbean]]