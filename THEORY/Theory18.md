## GROUP BY with WHERE CLAUSE
WHERE filters indidual rows first and then group by creates groups from the remaining row.

table --->   where(filter rows)--- > group by---> aggregate functions result.

***Write a query to find the average salary of employes in each department but consider only employees ,whose salary is greater > 50000.***

```sql
select department,avg(salary) from employee where salary > 50000 group by department;
```

***Write a query to find thenumber of employees in each department whose salary > 50000.***
```sql
select department,count(*) from employees where salary > 50000 group by department;
```


***WAQ to find the highest salary in each department considering only active employees.***
```sql
select department,count(*) from employees where status ="Active"
group by department;
```

***WAQ to find the number of active employees for each department and city.***
```sql
select department,city,count(*) from employees where status = "Active" order by department,city;
```

***WAQ to find department wise employees count, who joined after january2025.***
```sql
select department,count(*) from employees where joining_date > "2025-01-01" group by department;
```