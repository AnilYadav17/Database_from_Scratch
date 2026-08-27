## DELETE

```sql
syntax>
DELETE from tablename where condition
```

---->
**_WAQ to delete all the employees who to belong to HR department_**

```sql
delete from employeeup where department="HR";
```

**_WAQ to Delete IT employees havign more than 3 years of experience_**

```sql
delete from employeeup where department="IT" and experience>3;
```

**_WAQ to Delete employees who are not from IT or HR_**

```sql
delete from employeeup where department not in ("IT","HR");
```

**_WAQ to Delete employees who joined before 2020_**

```sql
delete from employeeup where joining_date < "2020-01-01" ;
```

**_WAQ to delete the employees with the lowest salary_**

```sql
delete from employeeup order by salary limit 1;
```

**_WAQ to delete lowest paid it employee_**

```sql
delete from employeeup where department = "IT" order by salary limit 1;
