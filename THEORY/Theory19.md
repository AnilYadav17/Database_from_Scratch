***WAQ to find highest salary in each department considering only active employees***
```sql
select department,msc(salary) from employee where status='Active' group by department;
```

***WAQ to find number of active employees for each department and city***
```sql
select department,city,count(*) from employee where status='Active' group by department,city;
```


