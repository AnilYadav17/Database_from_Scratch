## NAMING a check constraints :

In industry level database design giving constraints meaningfull name is a good practice.

```sql
create table employee(id int,name varchar(20),age int, constraint chk_age check(age>=18));
```

## CHECK vs NOT NULL

-
-
-
-
-
-

<br>

## DEFAULT CONSTRAINT

It provides a value automatically whe the user does not supply one.

```sql
create table employee(id int primary key,name varchar(20),status varchar(20) default "Active");
--Query OK, 0 rows affected (0.52 sec)

desc employee;
--+--------+-------------+------+-----+---------+-------+
--| Field  | Type        | Null | Key | Default | Extra |
--+--------+-------------+------+-----+---------+-------+
--| id     | int         | NO   | PRI | NULL    |       |
--| name   | varchar(20) | YES  |     | NULL    |       |
--| status | varchar(20) | YES  |     | Active  |       |
--+--------+-------------+------+-----+---------+-------+
--3 rows in set (0.00 sec)

insert into employee(id,name) values (101,"Anil");
--Query OK, 1 row affected (0.13 sec)

select * from employee;
---+-----+------+--------+
--| id  | name | status |
--+-----+------+--------+
--| 101 | Anil | Active |
--+-----+------+--------+
--1 row in set (0.00 sec)
```

**_Example 2_**

```sql
create table product (pid int,pname varchar(20),price int default 0);
```

<br>

### DEFAULT with date time :

With the help of default you can automatically record the creation time.

```sql
create table employee(id int,name varchar(20), createdate datetime default current_timestamp);
```

**_Example_**

```sql
 create table employee(id int not null default 1,name varchar(20));
```

DEMO ANSWERS :

```sql
select * from employee;
--+----+------+
--| id | name |
--+----+------+
--|  1 | Anil |
--|  1 | Abhi |
--|  1 | Anil |
--|  1 | Abhi |
--+----+------+
--4 rows in set (0.00 sec)
```

**_AND if_**

```sql
create table employee(id int ,name varchar(20),not null(id));
```

-> NOT NULL constraint can not defined at table level.

<br>

**_NEXT EXAMPLE_**

```SQL
create table employee(id int ,name varchar(20),dno int default 10 check(dno in(10,20,30)));
```

<br>

> Generate a table with NOT NULL,DEFAULT and CHECK....?
