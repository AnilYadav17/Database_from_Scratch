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

mysql> update accounts set balance=balance-2000 where accid=101;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> update accounts set balance=balance+2000 where accid=102;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from accounts;
+-------+---------+----------+
| accid | accname | balance  |
+-------+---------+----------+
|   101 | Anil    |  8000.00 |
|   102 | Abhi    | 22000.00 |
|   103 | Harsh   | 30000.00 |
+-------+---------+----------+
3 rows in set (0.00 sec)

mysql> commit;
Query OK, 0 rows affected (0.08 sec)

mysql> rollback;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from accounts;
+-------+---------+----------+
| accid | accname | balance  |
+-------+---------+----------+
|   101 | Anil    |  8000.00 |
|   102 | Abhi    | 22000.00 |
|   103 | Harsh   | 30000.00 |
+-------+---------+----------+
3 rows in set (0.00 sec)
```

**_OBSERVATION_** <br>
-> Once `COMMIT` is executed, the changes (balance of 101 → 8000, 102 → 22000) are permanently saved to the database.<br>
-> After `COMMIT`, firing `ROLLBACK` has **no effect** — data remains as it was after commit, because there is no active/pending transaction left to undo.<br>
-> `ROLLBACK` only works for changes made **after** the last `COMMIT` (i.e., within the current, still-open transaction).

### **_ROLLBACK_**

-> It is used to UNDO changes made during the current transaction. <br>
-> Undoes changes made during the current transaction (reverts to the last COMMIT point).

### EXAMPLE -> ROLLBACK undoes changes

```sql
mysql> select * from accounts;
+-------+---------+----------+
| accid | accname | balance  |
+-------+---------+----------+
|   101 | Anil    |  8000.00 |
|   102 | Abhi    | 19000.00 |
|   103 | Harsh   | 30000.00 |
+-------+---------+----------+
3 rows in set (0.00 sec)

mysql> update accounts set balance=balance+3000 where accid=101;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from accounts;
+-------+---------+----------+
| accid | accname | balance  |
+-------+---------+----------+
|   101 | Anil    | 11000.00 |
|   102 | Abhi    | 19000.00 |
|   103 | Harsh   | 30000.00 |
+-------+---------+----------+
3 rows in set (0.00 sec)

mysql> rollback;
Query OK, 0 rows affected (0.03 sec)

mysql> select * from accounts;
+-------+---------+----------+
| accid | accname | balance  |
+-------+---------+----------+
|   101 | Anil    |  8000.00 |
|   102 | Abhi    | 22000.00 |
|   103 | Harsh   | 30000.00 |
+-------+---------+----------+
3 rows in set (0.00 sec)
```

**_OBSERVATION_** <br>
-> The `UPDATE` on `accid=101` (balance changed from 8000 → 11000) was **not committed**, so it was still part of the open/pending transaction.<br>
-> Firing `ROLLBACK` **undid** this uncommitted change, and the balance of `accid=101` reverted back to `8000.00`.<br>
-> Note: `accid=102` shows `19000.00` before rollback but `22000.00` after — this value was already committed earlier (from a previous transaction), so it stays as it was; ROLLBACK only affects the **uncommitted** change made in the current transaction (on `accid=101`), not previously committed data.

### EXAMPLE -> ROLLBACK has no effect without an active transaction

```sql
mysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from accounts;
+-------+---------+----------+
| accid | accname | balance  |
+-------+---------+----------+
|   101 | Anil    |  8000.00 |
|   102 | Abhi    | 22000.00 |
|   103 | Harsh   | 30000.00 |
+-------+---------+----------+
3 rows in set (0.00 sec)

mysql> update accounts set balance=balance+2000 where accid=101;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from accounts;
+-------+---------+----------+
| accid | accname | balance  |
+-------+---------+----------+
|   101 | Anil    | 10000.00 |
|   102 | Abhi    | 22000.00 |
|   103 | Harsh   | 30000.00 |
+-------+---------+----------+
3 rows in set (0.00 sec)

mysql> rollback;
Query OK, 0 rows affected (0.03 sec)

mysql> select * from accounts;
+-------+---------+----------+
| accid | accname | balance  |
+-------+---------+----------+
|   101 | Anil    |  8000.00 |
|   102 | Abhi    | 22000.00 |
|   103 | Harsh   | 30000.00 |
+-------+---------+----------+
3 rows in set (0.00 sec)

mysql> update accounts set balance=balance+2000 where accid=101;
Query OK, 1 row affected (0.08 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> rollback;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from accounts;
+-------+---------+----------+
| accid | accname | balance  |
+-------+---------+----------+
|   101 | Anil    | 10000.00 |
|   102 | Abhi    | 22000.00 |
|   103 | Harsh   | 30000.00 |
+-------+---------+----------+
3 rows in set (0.00 sec)
```

**_OBSERVATION_** <br>
-> First block: `START TRANSACTION` was fired explicitly, so the `UPDATE` (101 → 10000) was part of an **open transaction**. `ROLLBACK` successfully undid it, and balance went back to `8000.00`.<br>
-> Second block: `ROLLBACK` **ended** the previous transaction. After that, MySQL went back to its default **autocommit = ON** mode.<br>
-> Since **no fresh `START TRANSACTION`** was fired before the second `UPDATE`, that `UPDATE` (101 → 10000) got **auto-committed immediately** on its own (it became its own single-statement transaction).<br>
-> So when `ROLLBACK` was fired again, there was **no pending/uncommitted transaction** left to undo — hence balance stayed at `10000.00` instead of reverting to `8000.00`.<br>

**_KEY TAKEAWAY_** <br>
-> `ROLLBACK` / `COMMIT` only works on the **currently active transaction**.<br>
-> Once a transaction ends (via `COMMIT` or `ROLLBACK`), you **must** fire `START TRANSACTION` (or `BEGIN`) again before making further changes — otherwise, with autocommit ON, each statement commits itself instantly and cannot be rolled back.

<br>

### EXAMPLE -> ROLLBACK has no effect after DDL (implicit commit) + no active transaction

```sql
mysql> alter table accounts add column `add` varchar(20);
Query OK, 0 rows affected (0.43 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> insert into accounts values (105,"Sahil",6.0001,"Indore");
Query OK, 1 row affected, 1 warning (0.08 sec)

mysql> rollback;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from accounts;
+-------+---------+----------+--------+
| accid | accname | balance  | add    |
+-------+---------+----------+--------+
|   101 | Anil    | 10000.00 | NULL   |
|   102 | Abhi    | 22000.00 | NULL   |
|   103 | Harsh   | 30000.00 | NULL   |
|   104 | Bhuma   | 40000.00 | NULL   |
|   105 | Sahil   |     6.00 | Indore |
+-------+---------+----------+--------+
5 rows in set (0.00 sec)
