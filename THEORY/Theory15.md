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

<br>

### UNIQUE VS NOT NULL

UNIQUE prevents duplicate values but NOT NULL prevents missing values.

```sql

mysql> create table employee4(id int,email varchar(20) unique);
Query OK, 0 rows affected (1.68 sec)

mysql> insert into employee4(id) VALUES (201);
Query OK, 1 row affected (0.11 sec)

mysql> insert into employee4(id) VALUES (202);
Query OK, 1 row affected (0.10 sec)

mysql> select * from employee4;
+------+-------+
| id   | email |
--+------+-------+
--|  201 | NULL  |
--|  202 | NULL  |
---+------+-------+
--2 rows in set (0.01 sec)

```

From the above example it is clear that email can not be duplicated but NULL handling is different from ordinary value.

If an application requires every employee to have an email and taht should be unique.

```sql
create table employee3(id int,email varchar(20) unique not null);
```

### UNIQUE VS PRIMARY KEY

PRIMARY KEY ->
Uniquely identify row values.
It can not contain NULL.
One per table is allowed.

UNIQUE ->
Prevents duplicates.
It can contain NULL.
Multiple possible in a table.
Used for alternate candidate key.

```sql
create table employee5(id int primary key,name varchar(20) unique,email varchar(20) unique);
---Query OK, 0 rows affected (1.55 sec)

create table employee6(id int primary key,name varchar(20) primary key,email varchar(20) unique);
---ERROR 1068 (42000): Multiple primary key defined
```

### (iii) CHECK CONSTRAINTS

Domain constraints used to restrict the values that can be inserted or uodated in a column based on specified condition.
Ensured data stored n a column satisfied a particular condition.

```sql
SYSNTAX>
create table tablename (columnname datatypee check(condition))
```

**_EXAMPLE1_**

```sql
create table employee6(id int,name varchar(20),age int check(age>=18));
--Query OK, 0 rows affected (0.58 sec)
```

SO ->

```sql
insert into employee6 values(101,"Anil",19);
--Query OK, 1 row affected (0.08 sec)

insert into employee6 values(102,"Abhi",16);
--ERROR 3819 (HY000): Check constraint 'employee6_chk_1' is violated.
```

**_EXAMPLE2_**

```sql
create table employee7(id int,name varchar(20),dno int check(dno in (10,20,30)));

insert into employee7 values (101,"Anil",40);
--ERROR 3819 (HY000): Check constraint 'employee7_chk_1' is violated.

insert into employee7(id,name) values (102,"Anii");
--Query OK, 1 row affected (0.13 sec)
```

```sql
create table employee8(id int,name varchar(20),dno int check(dno in (10,20,30)) not null);
```

<br>

> CHECK CONSTRAINTS WTIH MULTIPLE CONDITIONS:

CHECK can contain multiple conditions using operator.

```sql
mysql> create table employee9(id int,name varchar(20),age int,salary decimal(10,2), check(age>=18 and salary>=10000));
Query OK, 0 rows affected (1.28 sec)

mysql> insert into employee9 values(101,"Anil",17,9000);
---ERROR 3819 (HY000): Check constraint 'employee9_chk_1' is violated.

insert into employee9 values(102,"Abhi",19,19000);
---Query OK, 1 row affected (0.14 sec)

insert into employee9 values(101,"Anil",19,9000);
--ERROR 3819 (HY000): Check constraint 'employee9_chk_1' is violated.
```

```sql
create table employee10(id int,name varchar(20),marks int, check(marks between 0 and 100));
--Query OK, 0 rows affected (1.14 sec)

insert into employee10 values (101,"Anii",100);
--Query OK, 1 row affected (0.09 sec)

insert into employee10 values (101,"Anii",101);
--ERROR 3819 (HY000): Check constraint 'employee10_chk_1' is violated.
```

**_EXAMPLE_**

```sql
create table employee11(id int,salary int, ex int , check ((salary>=15000 and ex <2 ) or (ex>2 and salary>=25000)));
```

so,

```sql

```

<BR>
> CHECK CONSTRAINTS WITH UPDATE<BR>

Check constraint does not only check new insertions .
