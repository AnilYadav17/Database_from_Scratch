## FOREIGN KEY

### ADVANTAGES :
1. Maintains refferential integritry :- The foreign key maintains the value in the child table must corresponds to an existing value in parent table.
2. Prevents invalid data : It stops users from inserting unrelated or invalid id's into the child table.
3. Maintains relationship between two tables.
4. Prevents orphan records:- An orphan records is child record whose parent no longer exists.
5. Controls delete operation.
6. Controls update operation.
7. Makes database design more reliable.


***Syntax***
```sql
create table parenttable (id int primary key,name varchar(30));
create table childtable (id int primary key,parentid int,foreign key(parentid) references parenttable(id));
```
***Example1***
```sql
create table employee17(empid int primary key,empname varchar(20),deptid int,foreign key(deptid) references department17(deptid));


insert into department17 values (1,'HR'),(2,'IT'),(3,'Finance');
insert into employee17 values (101,"Anil",1),(102,"Abhi",2),(103,"Harsh",3);
--Query OK, 3 rows affected (0.07 sec)
--Records: 3  Duplicates: 0  Warnings: 0

select * from employee17;
--+-------+---------+--------+
--| empid | empname | deptid |-
--+-------+---------+--------+-
--|   101 | Anil    |      1 |
--|   102 | Abhi    |      2 |
--|   103 | Harsh   |      3 |
--+-------+---------+--------+
--3 rows in set (0.00 sec)
```
so,
```sql
 insert into employee17 values (104,"Harsh",10);
 --ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`batch18`.`employee17`, CONSTRAINT `employee17_ibfk_1` FOREIGN KEY (`deptid`) REFERENCES `department17` (`deptid`))
```




The above query key gives error because department id 4 is not available in department.

***NOTE: Foreign key does not meant it can consistes unique values, it can consists of duplicate values.***


```sql
insert into employee17(empid,empname) values (104,"Harsh");

select * from employee17;
--+-------+---------+--------+
--| empid | empname | deptid |
--+-------+---------+--------+
--|   101 | Anil    |      1 |
--|   102 | Abhi    |      2 |
--|   103 | Harsh   |      3 |
--|   104 | Harsh   |   NULL |
--+-------+---------+--------+
---4 rows in set (0.00 sec)
```

***NOTE: Foriegn can contain NULL value by default,because NULL is not equal to invalid department. It means in our example the employee currently has no department value***
we can use NOT NULL to solve it.


---

<br>

### FOREIGN KEY vs PRIMARY KEY

| Feature | Primary Key (PK) | Foreign Key (FK) |
|---|---|---|
| Purpose | Uniquely identifies a row | Establishes a relationship between tables |
| NULL | Cannot contain NULL | Can contain NULL by default |
| Duplicate Values | Not allowed | Allowed |
| Number per Table | One PK constraint per table | Multiple FK constraints per table |
| Role | Identifies an entity | References a key in another table |
| Integrity | Ensures entity integrity | Ensures referential integrity |
| Reference | Identifies rows in its own table | References a key in another table |
---
<br>

### FORIEN KEY with  UNIQUE KEY
***Example2***

```sql
CREATE TABLE DEPARTMENT18(
    deptid INT PRIMARY KEY,
    deptcode VARCHAR(20) UNIQUE
);

CREATE TABLE EMPLOYEE18(
    emptid INT PRIMARY KEY,
    empname VARCHAR(20),
    dcode VARCHAR(20),
    FOREIGN KEY (dcode) REFERENCES DEPARTMENT18(deptcode)
);

INSERT INTO DEPARTMENT18 VALUES
(1, "IT"),
(2, "CS");

INSERT INTO EMPLOYEE18 VALUES
(101, "Anil", "IT"),
(102, "Abhi", "CS");

SELECT * FROM DEPARTMENT18;

SELECT * FROM EMPLOYEE18;
```
Visual View,

```
        DEPARTMENT18
   ┌─────────────────────┐
   │ deptid    deptcode  │
   │   PK       UNIQUE   │
   ├─────────────────────┤
   │   1          IT     │
   │   2          CS     │
   │   3          ME     │
   └──────────┬──────────┘
              │
              │ references
              ▼
        EMPLOYEE18
   ┌───────────────────-──┐
   │ emptid  empname dcode│
   │   PK            FK   │
   ├────────────────────-─┤
   │  101    Anil    IT   │
   │  102    Abhi    CS   │
   │  103    Harsh   ME   │
   └───────────────────-──┘
```
---
<br>

### NAMING A FOREIGN KEY
When we craete a foreign key we can give the foreign key constraint a name , that name helps us to idetify the relationship between two tables easily.

***Syntax***
```sql
constraint constraintname foreign key(column name) references parenttable(parent columnname);
```
```sql
CREATE TABLE EMPLOYEE19(emptid INT PRIMARY KEY,
     empname VARCHAR(20),dcode VARCHAR(20),constraint 
     fk_employee_department FOREIGN KEY (dcode) REFERENCES 
     DEPARTMENT18(deptcode) );
```
