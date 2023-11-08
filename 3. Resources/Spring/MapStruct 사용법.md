```java
// student/mapper/studentMapper.java

@Mapper(componentModel = "spring", unmappedTargetPolicy = ReportingPolicy.IGNORE) 
public interface StudentMapper 
{ 
	public StudentDTO toDTO(Student student); 
}
```
https://marklee1117.tistory.com/121