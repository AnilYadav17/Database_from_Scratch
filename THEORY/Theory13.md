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
