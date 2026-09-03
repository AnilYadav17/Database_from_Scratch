# FUNCTIONS

They are predefined operations that accepts one or more values as input , perform a specific operation and return a result.
<br>

## TYPES

1. SINGLE ROW FUNCTIONS (Scalar Functions)
2. AGGREGATE FUNCTIONS (Group Functions)
   <br>

## SINGLE ROW FUNCTIONS

They operates on individual rows and produce one result for each row.

### TYPES

1. String Functions.
2. Numeric Functions.
3. Date and Time Functions.
4. Conditional Functions.
5. Null Handling Functions.
6. Conversion Functions.

### (i) STRING FUNCTIONS

They are used to perform opertaions on character or string data.

```sql
select * from student;
---+------------+-------+------+------+
---| student_id | name  | age  | city |
---+------------+-------+------+------+
---|          1 | Anil  |   21 | goa  |
---|          2 | Rahul |   22 | goa  |
---|          3 | Amit  |   20 | goa  |
---+------------+-------+------+------+
---3 rows in set (0.05 sec)

select name,upper(name) from student;
---+-------+-------------+
---| name  | upper(name) |
---+-------+-------------+
---| Anil  | ANIL        |
---| Rahul | RAHUL       |
---| Amit  | AMIT        |
---+-------+-------------+---
---3 rows in set (0.00 sec)
```

## AGGREGATE FUNCTIONS
They performs calculations on a set of rows and returns one summarised result.They are used in bussiness reports ,sells reports, E-Commerce analytics etc.<br>
They process on multiple rows.

---
### (i) COUNT
It is used to count rows and nun-Null values. <br>
1. count(*)
<br> -> It counts rows. 
<br> -> It counts column even if all the values are null.
```sql
select count(*) from employee;
```

2. count()
-> It counts not null values in column.
<br> -> Like here not null values of age is not count.
```sql
select count(age) from pystudent;
```
***COUNT(*) counts how many rows exists and COUNT(age) count how many students have age value.***

3. count(distinct)
It counts unique not null values.
```sql
select count(distinct city) from employee;
```

---
### (ii) SUM
Calculate total numeric value and Ignores NULL values.
```sql
select sum(saalry) from employee;
```
#### SUM WITH WHERE 
Aggregate functions become more powerfull when combined with filtering.
```sql
select sum(salaey) from employee where depatment = "IT";
```

***Write  a query to give sum of all the salaries above 5000***
```sql
select sum(salary) from employee where salary>50000;
```

---
### (iii) MEAN (AVERAGE)
Calculate arithmatic mean.
```sql
select avg(salary) from employee;
```

-> Not include null values , like if values are 1,2,NULL,3 then it will return (1+2+3/3=2).
<br>->Ignores NULL values.

---
### (iv) MIN
Returns minimum value.
```sql
select min(age) from employee;
```

---
### (v) MAX
```sql
select max(age) from employee;
```

SO,
```sql
select count(*) as totalemployee,sum(salary) as totalsalary,avg(salary) as avgsalary,min(salary) as minimum,max(salary) as maximum from employee;
```
<br>


## GROUPBY
It is a sql clause use to divide rows into groups based on one or more columns, so that aggregate can perform calculations independently for each group.<br>
It  converts a large collection of rows into logical groups and allow us to calculate summary.
***SYNTAX***
```sql
selct columname,aggregatefunction(columname) from tablename group by columnname;
```

***Write a  query to find total salary paid by each department.***
```sql
select department,sum(salary) from employee grofup by department;
```

***Write a query to find number of employees in each department***
```sql
select department,count(*) from employee group by department;
```
AND ->
```sql
select city,count(*) from pystudent group by city;
```
```sql
select city,count(city) from pystudent group by city;
```
***NOTE -
The above type of query commonly used for number of orders per customer , number of produccts per category, number of students per course.***

### COUNT(*) vs COUNT
COUNT(*) will count all the rows but coumn(column) ignores null.

***Write a query to find average salary of each department***
```sql
select department, avg(salary) from employee group by department
```
***EXAMPLE***
```sql
select city, avg(age) from pystudent group by city;
```

***Write a query to find lowest and highest salary in each department.***
```sql
select department, min(salary),max(salary) from employee group by department
```
<BR>


### GROUP BY WITH MULIPLE COLUMNS
---

DEPARTMENT     JOB_ROLE
IT             DEVELOPER
IT             DEVELOPER
IT             TESTER
HR             RECRUITER
HR             MANAGER

```sql
select department,job_role,count(*) from employee group by department job_role;
```
`IT+DEVELOPER,IT+TESTER,HR+RECRUITER,HR+MANAGER`

The above example create a group for every unique combination of department and job role.


---
<br>

```sql
CREATE TABLE grporder(orderid int,cname varchar(20),city varchar(20),productcategory varchar(20),amount decimal(10,2));
```
Then,

```sql
INSERT INTO grporder values(111,"Anil","Mumbai","Electronics",15000);
INSERT INTO grporder values(112,"Abhi","Mumbai","Electronics",10000);
INSERT INTO grporder values(113,"Harsh","Chennai","Household",5000);
```
***Write a query to find total sells city wise***
```sql
select city,sum(amount) from grporder group by city;
```
***Write a query to find total sells for each city and product category***
```sql
select city,productcategory,sum(amount) from grporder order by city,productcategory;
```
