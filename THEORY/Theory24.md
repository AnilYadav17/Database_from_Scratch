# JOINS

A **JOIN** is used to combine data from two or more tables based on a related column.

In simple words:

> **JOIN helps us get related data from multiple tables.**

### Important Point

A JOIN **does not require a foreign key**.

* **Foreign Key** → maintains a relationship and referential integrity.
* **JOIN** → combines data for a query.

---

## Syntax

```sql
SELECT column1, column2
FROM table1
JOIN table2
ON table1.column = table2.column;
```

---

## Example

### employee17

```text
+-------+---------+--------+
| empid | empname | deptid |
+-------+---------+--------+
|   101 | Anil    |      1 |
|   102 | Abhi    |      2 |
|   103 | Harsh   |      3 |
|   104 | Harsh   |   NULL |
|   105 | Kanak   |      1 |
|   106 | Bhumi   |      2 |
+-------+---------+--------+
```

### department17

```text
+--------+----------+
| deptid | deptname |
+--------+----------+
|      1 | HR       |
|      2 | IT       |
|      3 | Finance  |
+--------+----------+
```

Here, `deptid` is the related column.

```text
employee17.deptid
        ↓
department17.deptid
```

---

## INNER JOIN

An **INNER JOIN** returns only the rows that have a match in both tables.

```sql
SELECT employee17.empname, department17.deptname
FROM employee17
JOIN department17
ON employee17.deptid = department17.deptid;
```

Output:

```text
+---------+----------+
| empname | deptname |
+---------+----------+
| Anil    | HR       |
| Abhi    | IT       |
| Harsh   | Finance  |
| Kanak   | HR       |
| Bhumi   | IT       |
+---------+----------+
```

Employee `104` is not shown because:

```text
deptid = NULL
```

There is no matching department for `NULL`.

---

## JOIN = INNER JOIN

In MySQL:

```sql
JOIN
```

is the same as:

```sql
INNER JOIN
```

So both are valid:

```sql
SELECT *
FROM employee17
JOIN department17
ON employee17.deptid = department17.deptid;
```

```sql
SELECT *
FROM employee17
INNER JOIN department17
ON employee17.deptid = department17.deptid;
```

---


### Remember

```text
JOIN
 ↓
Match related columns
 ↓
Combine data
 ↓
Return result
```
<br>

---
USING ALIAS:
```sql
select e.empname,d.deptname from employee17 as e join department17 as d on e.deptid=d.deptid;
```
The ON CLAUSE specify the join condition used to determine which rows from two or more tables are related and shuld be combined.<br>
It tells the database engine how rows from the participating tables should be matched.It means match an employee row with a department row when the employees department is equal to the departments deptid.

```sql
select * from employee17 as e join department17 as d on e.deptid=d.deptid;
```

The Flow :<br>
Employee ---
Department ---
On Condition ---
Find Matching Rows ---
Combined Matching Rows ---
Generate Result .


So,
```sql
select * from employee17 as e join department17 as d on e.deptid<>d.deptid;
```
---

## Common JOIN Types

```text
1. INNER JOIN
2. LEFT JOIN
3. RIGHT JOIN
4. CROSS JOIN
5. SELF JOIN
```

### (i) INNER JOIN: 
It returns only those rows for which a matching condtion exists in both tables.

```sql
select * from employee17 as e inner join department17 as d on e.deptid=d.deptid;
```

