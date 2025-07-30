```scala
println("Filter out anyone over 21:")  
people.filter(people("age") < 21).show()  
  
println("Group by age:")  
people.groupBy("age").count().show()  
  
println("Make everyone 10 years older:")  
people.select(people("name"), people("age") + 10).show()
```
- sql 과 유사하게 dataframe과 사용가능