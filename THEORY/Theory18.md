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
