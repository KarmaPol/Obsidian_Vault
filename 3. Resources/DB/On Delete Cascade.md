```sql
mysql> create table personinfo (
    -> person char(10) not null,
    -> age int(11),
    -> parent char(10) not null,
    -> primary key(person),
    -> foreign key(parent) references personinfo(person)
    -> on delete cascade);
```
B가 A를 foreign key로 가리키고 있을때, A를 삭제하면 B도 같이 삭제