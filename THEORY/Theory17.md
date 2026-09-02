# FUNCTIONS

They are predefined operations that accepts one or more values as input , perform a specific operation and return a result.
<br>

## TYPES

1. SINGLE ROW FUNCTIONS (Scalar Functions)
2. AGGREGATE FUNCTIONS (Group Functions)
   <br>

## SINGLE ROW FUNCTIONS

They operates on individual rows and produce one result for each row.

### TYPES

1. String Functions.
2. Numeric Functions.
3. Date and Time Functions.
4. Conditional Functions.
5. Null Handling Functions.
6. Conversion Functions.

### (i) STRING FUNCTIONS

They are used to perform opertaions on character or string data.

```sql
select * from student;
---+------------+-------+------+------+
---| student_id | name  | age  | city |
---+------------+-------+------+------+
---|          1 | Anil  |   21 | goa  |
---|          2 | Rahul |   22 | goa  |
---|          3 | Amit  |   20 | goa  |
---+------------+-------+------+------+
---3 rows in set (0.05 sec)

select name,upper(name) from student;
---+-------+-------------+
---| name  | upper(name) |
---+-------+-------------+
---| Anil  | ANIL        |
---| Rahul | RAHUL       |
---| Amit  | AMIT        |
---+-------+-------------+---
---3 rows in set (0.00 sec)
```
