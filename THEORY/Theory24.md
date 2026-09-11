## SELF REFERENCING FOREIGN KEY
It is foreign key where a cloumn in a table refers to the primary key or the unique key.
In simple words a tale creates a relationship with it self.

```sql
create table selfemployee(empid int primary key,empname varchar(20) not null,managerid int,foreign key (managerid) references selfemployee(empid));
```