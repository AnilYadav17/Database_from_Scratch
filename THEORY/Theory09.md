# SELECT Command in MYSQL

The `SELECT` command is used to retrieve or read data from one or more tables in MySQL. 
It is the most important command in DQL (Data Query Language). 
`SELECT` does not change the data, it only fetches the data from the database.

## 1. Select All Columns
```sql
SELECT * FROM employeebatch;
```
- `*` means select all the columns.

## 2. Select Specific Columns
Instead of retrieving everything, specify the required columns.
```sql
SELECT name, city FROM employeebatch;
```
- **Note:** The order in which we write columns determines the order in the result.

## 3. Select with an Expression (Calculations)
`SELECT` can also perform calculations.
```sql
SELECT name, Salary, Salary * 12 FROM employeebatch;
```

## 4. Column Alias
In the above example, the calculated column name `Salary * 12` is not readable. We can give an alternate name using alias with `AS`.
```sql
SELECT name, Salary, Salary * 12 AS annual_salary FROM employeebatch;
```

## 5. SELECT DISTINCT
Used to fetch distinct (unique) values.
```sql
SELECT DISTINCT city FROM employeebatch;
```
- If we want to see different combinations, it considers the combination of columns:
```sql
SELECT DISTINCT city, department FROM employeebatch;
```
Here the duplicate `indore and IT` combination will appear only once.

---

## 6. WHERE Clause
`SELECT` with `WHERE` clause is used to filter the rows based on a condition.
```sql
SELECT * FROM employeebatch WHERE Salary > 50000;
```
- Different operators can be used: `<`, `>`, `<=`, `>=`, `!=`, `=`.

### Logical Operators

- **AND**: Both conditions must be True.
  ```sql
  SELECT * FROM employeebatch WHERE city = 'indore' AND Salary > 50000;
  ```
- **OR**: At least one condition must be True.
  ```sql
  SELECT * FROM employeebatch WHERE city = 'indore' OR Salary > 50000;
  ```
- **NOT**: Reverses the condition.
  ```sql
  SELECT * FROM employeebatch WHERE NOT city = 'indore';
  ```

---

## 7. BETWEEN Operator
- It is used when we want a value within a range.
- `BETWEEN` is inclusive.
```sql
SELECT * FROM employeebatch WHERE Salary BETWEEN 40000 AND 55000;
```
- `NOT BETWEEN` can be used to exclude a range.

---

## 8. IN Operator
- The `IN` operator is used to check whether a value matches any value in a given list of values.
- It is specially useful when we want to replace multiple `OR` conditions with a shorter and cleaner condition.
- `IN` works like multiple `OR`.
- `NOT IN` works like multiple `AND` (for inequality).

```sql
SELECT * FROM employeebatch WHERE city IN ('indore', 'bhopal', 'pune');
```

We can combine `IN` with `WHERE + AND`:
```sql
SELECT * FROM employeebatch WHERE city IN ('indore', 'bhopal') AND age > 28;
```
This gives a list of employees whose city is either indore or bhopal AND their age must be greater than 28.
