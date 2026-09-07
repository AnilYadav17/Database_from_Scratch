***WAQ to find highest salary in each department considering only active employees***
```sql
select department,msc(salary) from employee where status='Active' group by department;
```

***WAQ to find number of active employees for each department and city***
```sql
select department,city,count(*) from employee where status='Active' group by department,city;
```


## HAVING

It is a SQL clause used to filter groups created by the group by clause.

Where clause filter indidual rows,where HAVING clause filters groups.

***WAQ to find departments having more than 2 employees***
```sql
select department,city,count(*) from employee group byrtment having count(*) > 2;
```

### WHERE vs HAVING
| WHERE | HAVING |
|---|---|
| Filters individual rows | Filters groups |
| Works before `GROUP BY` | Works after `GROUP BY` |
| Used with individual row values | Commonly used with aggregate results |
| Cannot normally use aggregate functions directly | Commonly used with aggregate functions |
| Example: `WHERE salary > 50000` | Example: `HAVING COUNT(*) > 3` |



***WAQ to find departments where total salary is greater than 2 lakhs***
```sql
select department,sum(salary) from employee group by department having sum(salary) > 20000;
```

***WAQ to find departments where employee count>2 and avg salary is greater than 15000***
```sql
select department,count(*),avg(salary) from employee group by department having count(*)>2 and avg(salary) > 50000;
```
***WAQ to find departments having atleast 2 active employees***
```sql
select department,count(*) from employee where status="Active" group by department having count(*)>=2;
```
<br>

## GROUP BY rules
1. Selected normal column  should be in GROUP BY.  
```sql
select city,count(*) from employee group by department;
```
2. If multiple columns are selected then put them in group by.
```sql
select city,count(*) from employee group by department;
```

3. Aggregate functions are not required in group by 
```
select department,count(*) as total from employee_batch group by department,count(*);
error: Can't group on 'tota;'
```
4.  Use aggregate functions to summarize group data 
```
select department from employee_batch group by department;
+------------+
| department |
+------------+
| IT         |
| Finance    |
| Sales      |
+------------+
3 rows in set (0.01 sec)
```
5. Where clause must be first 
6. Having doesn't work without aggregate functions
7. Without group by having don't work
```
select sum(salary) from employee_batch having sum(salary)>50000;
```

# with roll up 
It is an extension of group by that automatically adds summary rows such as sub totals to the result.
```
select column1,aggregate(column2) from employee group by column1 with rollup;
```
```
select department,sum(salary) from employee_batch group by department with rollup;
+------------+-------------+
| department | sum(salary) |
+------------+-------------+
| Finance    |   276001.10 |
| IT         |   215001.20 |
| Sales      |   218001.45 |
| NULL       |   709003.75 |  Here Null is showing total of all 
+------------+-------------+
4 rows in set (0.01 sec)
```

```
select department,city from employee_batch group by department,city;
+------------+--------+
| department | city   |
+------------+--------+
| IT         | Pune   |
| Finance    | Delhi  |
| Sales      | Indore |
| Sales      | Mumbai |
| Finance    | Pune   |
| IT         | Delhi  |
| Finance    | Bhopal |
| IT         | NULL   |
| Sales      | Pune   |
+------------+--------+
9 rows in set (0.00 sec)
We can use group by without aggregate in that case it will give one row for each group
```
## Diff b/w distinct and group by