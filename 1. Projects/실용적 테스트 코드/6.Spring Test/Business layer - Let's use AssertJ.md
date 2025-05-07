# AssertJ
- useful test tool with Junit
- better readability
## Reference
- https://pjh3749.tistory.com/241
```java
assertThat(actual).isEqualTo(expected);

// list filter
assertThat(list).filteredOn(human -> human.getName().contains("a"))
                .containsOnly(park, jack);

// extracting property
assertThat(list).extracting("name", "age")
                .contains(tuple("Kim", 22),
                        tuple("Park", 25),
                        tuple("Lee", 25),
                        tuple("Amy", 22),
                        tuple("Jack",22));

// exception
assertThat(thrown).isInstanceOf(Exception.class)
```

### Test profile
- Lecturer wrote the test code with test DB profile. not mocking
- It depends on Mockist Vs. Classist. But I prefer Mock

[[@Mock VS. @Spy VS. @InjectMock]]
[[Classical Vs. Mockist Testing]]

