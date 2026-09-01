# CONSTRAINTS

They are the RULE or RESTRICTION applied on a table based on our requirement.

They are classified into THREE:<br>
i) Domain Integrity Constraints :- default,not null,check<br>
ii) Entity Integrity Constraints :- Unique or Primary key <br>
iii) Referential Integriry Constraints :- Foreign key...

`Constraints` are primarily used for data integrity.<br>
<br><br>

## Domain Integrity Constraints

### (i) NOT NULL

It specify that column must contain a value.

```sql
 create table employee(id int,name varchar(20) not null, salary decimal(20,2));
```

**_VALID_**

```sql
 insert into employee values(101,"null",50000);
--Query OK, 1 row affected (0.11 sec)
insert into employee values(103,"",50000);
--Query OK, 1 row affected (0.14 sec)
```

**_INVALID_**

```sql
insert into employee values(102,null,50000);
--ERROR 1048 (23000): Column 'name' cannot be null
```

NULL does not mean 0 or '' or 'NULL'.<br>
NULL means unknown value or missing value or not available value.
The not NULL constraint is also applied during updation.

### (ii) UNIQUE CONSTRIANTS

It ensures that a column can not contain duplicate values.

```sql
create table employee1(id int,email varchar(20) unique);
```

**_VALID_**

```sql
insert into employee1 values(101,"ay@gmail.com");
--Query OK, 1 row affected (0.12 sec)
```

**_INVALID_**

```sql
insert into employee1 values(102,"ay@gmail.com");
--ERROR 1062 (23000): Duplicate entry 'ay@gmail.com' for key 'employee1.email'
```

-> UNIQUE CONSTRAINTS ON MULTIPLE COLUMNS:

```sql
create table employee2(id int,deptid int,employeecode varchar(20),constraint uk_dept unique(deptid,employeecode));
```

**_VALID_**

```sql
insert into employee2 values (101,501,401);
---Query OK, 1 row affected (0.26 sec)

insert into employee2 values (101,501,402);
--Query OK, 1 row affected (0.13 sec)

insert into employee2 values (101,502,401);
--Query OK, 1 row affected (0.11 sec)

insert into employee2 values (101,502,402);
---Query OK, 1 row affected (0.11 sec)
```

**_INVALID_**

```sql
insert into employee2 values (101,502,402);
--ERROR 1062 (23000): Duplicate entry '502-402' for key 'employee2.uk_dept'
```

From the above example it is clear that combinations shoudl be unique.
