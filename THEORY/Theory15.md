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
