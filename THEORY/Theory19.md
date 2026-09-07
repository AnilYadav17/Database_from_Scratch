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
