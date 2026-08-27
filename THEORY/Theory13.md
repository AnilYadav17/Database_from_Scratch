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
```

**_WAQ to delete IT or HR employees whose salary is below 60000_**

```sql
delete from employeeup where department in ("IT","HR") and salary > 60000;
```

### TRUNCATE vs DELETE

| Aspect             | TRUNCATE                                                 | DELETE                                                                                         |
| ------------------ | -------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Type               | DDL (Data Definition Language)                           | DML (Data Manipulation Language)                                                               |
| WHERE clause       | Not allowed                                              | Allowed                                                                                        |
| Row selection      | Removes all rows directly                                | Can delete selected rows                                                                       |
| Conditions         | No conditions possible                                   | Conditions can be used                                                                         |
| ORDER BY / LIMIT   | Cannot be used                                           | Can be used                                                                                    |
| Deletion mechanism | Deallocates table data directly (deallocates data pages) | Follows row-by-row deletion semantics                                                          |
| Commit behavior    | Implicit commit — rollback not possible                  | Can be rolled back when used within a transaction (under appropriate transactional conditions) |
| Auto Increment     | Counter resets — next insert starts from one             | Does not reset auto increment                                                                  |

### DELETE vs DROP

| Aspect                      | DELETE                              | DROP                                               |
| --------------------------- | ----------------------------------- | -------------------------------------------------- |
| Type                        | DML                                 | DDL                                                |
| Scope                       | Removes rows                        | Removes the database object itself                 |
| Table structure             | Remains after deletion              | Removed after drop                                 |
| Columns, Constraints, Index | Remain                              | Removed                                            |
| WHERE clause                | Allowed                             | Not allowed                                        |
| Row selection               | Selected or all rows can be deleted | Not applicable — entire object is removed          |
| Rollback                    | Possible                            | Not possible                                       |
| Auto Increment              | Not reset                           | No concept applies — object is removed permanently |

<br><br>

## TCL -> TRANSACTION CONTROL LANGUAGE

TCL commands are used to manage TRANSACTIONS in a Database.<br>
TRANSACTION is a group of SQL statements that should be treated as one logical unit of work.<br>

**_TOP COMMANDS_** <br>
i) COMMIT <BR>
ii) ROLLBACK <BR>
iii) SAVEPOINT<BR>
iv) ROLLBACK TO SAVEPOINT<BR>
v) RELEASE SAVEPOINT<BR>
vi) START TRANSACTION<BR>

**_SYNTAX_**

```sql
syntax>
start transaction;
sql statement1;
sql statement2;
sql statement3;
commit;

OR
begin;
sql statements;
commit;
```

### COMMIT

Permanently saves all changes made during the current transaction.

### EXAMPLE -> COMMIT makes changes permanent

```sql
mysql> select * from accounts;
+-------+---------+----------+
| accid | accname | balance  |
+-------+---------+----------+
|   101 | Anil    | 10000.00 |
|   102 | Abhi    | 20000.00 |
|   103 | Harsh   | 30000.00 |
+-------+---------+----------+
3 rows in set (0.00 sec)

mysql> start transaction;
Query OK, 0 rows affected (0.00 sec)
