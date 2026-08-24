```sql
select name,salary,salary*12 as annual_salary from employeebatch order by salary*12 desc;
```

## ORDER BY WITH DISTINCT

Removes duplicates.

```SQL
select distinct city from employeebatch order by city;
```

<br>

**_(i) Write a query to get employees from indore or Bhopal and arrange them by highest salary first and if two employees have the same salary arrrange by younger age first._**

```sql
select name,city,age,salary from employeebatch where city in ("Indore","Bhopal") order by salary desc,age desc
```

<br>

## LIMIT

It is used to restrict the number of rowsa return by a select query.

```sql
select * from employeebatch limit 2;
```

<br>

**_(ii) Write a query to get highest three paid employees._**

```sql
select * from employeebatch ordr by salary desc limit 3;
```

**_(iii) Write a query to getlowest paid employee._**

```sql
select * from employeebatch ordr by salary asc limit 1;
```

#### If we give more value in limit then it will not produce any error, It will just give the available rows.

```sql
select * from employeebatch where department = "IT" order by salary desc
limit 100;
```

**_iv) Write a query to give two highest paid emp whose salary is greater then 50000_**

```sql
select * from employeebatch where salary > 50000 order by salary desc limit 2;
```

```sql
select distinct city from employeebatch;
```

<br>

## DISTINCT WITH LIMIT

```sql
select distinct city from employeebatch limit 2;
```

<br>

**_(iv) Write a query to find two employees with the highest annual salary._**

```sql
select name,salary,salary*12 as annual_salary  from employeebatch order by annual_salary desc limit 2;
```

<br>

## OFFSET

It is used to skip specified number of rows before returning the result.

```sql
syntax:-
select column1,column22 from tablename limit numberofrows offset numberofrowstoskip;
```

-> Skip two rows then return two rows

```sql
SELECT * FROM employeebatch limit 2 offset 2;
```

<br>

**_(v) Write a query to find third and fourth highest paid employees._**

```sql
SELECT * FROM employeebatch order by salary desc limit 2 offset 2;
```

**_(v) Write a query to find third highest paid employees in IT department._**

```sql
SELECT * FROM employeebatch WHERE department = 'IT' order by salary desc
limit 1 offset 2;
```

**_FLOW_** <BR>
SELECT -> choose column -> from -> choose table -> where -> filter -> rows -> orderby -> sort rows -> limit -> how many rows -> offset -> how many rows to skip.

```sql
SELECT * FROM employeebatch  limit 2,2;
```

<br>

## UPDATE

It is a DML command which is used to modify existing records in a table.

```sql
syntax:-
update tablename set column1=value1,column2=value2 ..... where condition;
```

In the above syntax Where is not mandatory but without where every row will be udpated.

```sql
update student set city = "Goa";
```

#### USING ANOTHER TABLE

```sql
CREATE TABLE employeeup (     employee_id INT PRIMARY KEY AUTO_INCREMENT,     employee_name VARCHAR(50),     department VARCHAR(50),     city VARCHAR(30),     salary DECIMAL(10,2),     experience INT,     age INT,     joining_date DATE,     status VARCHAR(20) );
```

```sql
INSERT INTO employeeup (employee_name, department, city, salary, experience, age, joining_date, status) VALUES ('Anil', 'IT', 'Indore', 45000.00, 1, 22,
'2025-07-10', 'Active'), ('Rahul', 'HR', 'Bhopal', 55000.00, 3, 26, '2023-05-15', 'Active'), ('Amit', 'Finance', 'Dewas', 62000.00, 5, 30, '2021-03-20', 'Active'), ('Vikas', 'IT', 'Indore', 38000.00, 2, 24, '2024-06-12', 'Inactive'), ('Rohit', 'IT', 'Bhopal', 75000.00, 7, 35, '2019-01-25', 'Active'), ('Suresh', 'HR', 'Ujjain', 42000.00, 2, 27, '2024-02-18', 'Active'), ('Karan', 'Finance', 'Indore', 68000.00, 6, 33, '2020-09-05', 'Inactive'), ('Mohit', 'IT', 'Dewas', 50000.00, 4, 29, '2022-11-10', 'Active'), ('Deepak', 'Sales', 'Bhopal', 35000.00, 1, 23,
'2025-01-08', 'Active'), ('Nitin', 'Sales', 'Indore', 58000.00, 4, 31, '2022-04-14', 'Active');
```
