# 🗄️ Database From Scratch - Mock Assessment

Welcome to the mock assessment! This test is designed to evaluate your understanding of the concepts covered in the "Database From Scratch" repository, including DDL, DML, DQL, TCL, Data Types, and primary key constraints.

---

## Part 1: Theory (Multiple Choice & Short Answer)

**1. Which of the following SQL commands belongs to Data Definition Language (DDL)?**
A) `INSERT`
B) `SELECT`
C) `ALTER`
D) `COMMIT`

**2. What is the primary difference between `DELETE` and `TRUNCATE`?**
A) `TRUNCATE` can be used with a `WHERE` clause, while `DELETE` cannot.
B) `DELETE` removes the table structure, while `TRUNCATE` only removes data.
C) `TRUNCATE` is a DDL command that resets the table and is faster, while `DELETE` is a DML command that removes rows one by one.
D) `DELETE` resets the `AUTO_INCREMENT` counter, while `TRUNCATE` does not.

**3. What does `CTAS` stand for in the context of table creation?**
A) Create Table And Save
B) Create Table As Select
C) Copy Table And Structure
D) Create Table Alter Select

**4. When using `INSERT IGNORE`, what happens if you try to insert a duplicate primary key?**
A) An error is thrown and the transaction is aborted.
B) The existing record is updated with the new values.
C) The new record is skipped, no error is thrown, and execution continues.
D) The database automatically generates a new primary key.

**5. Which data type would be most appropriate for storing a user's role if the only possible values are 'admin', 'editor', and 'viewer'?**
A) `VARCHAR(50)`
B) `TEXT`
C) `SET`
D) `ENUM`

---

## Part 2: Practical Query Writing

**6. Database Creation & Setup**
Write the SQL query to create a database named `mock_db` and switch to using it.

**7. Table Creation**
Write a query to create a table named `employees`. It should have the following columns:
- `emp_id`: Integer, Primary Key, Auto-incrementing.
- `first_name`: String (max 50 characters), cannot be null.
- `last_name`: String (max 50 characters).
- `hire_date`: Date type.

**8. Data Modification (`ALTER TABLE`)**
You realized you need to store the employee's salary. Write a query to add a `salary` column to the `employees` table. The salary should be a decimal number allowing up to 8 digits in total, with 2 decimal places.

**9. Data Insertion**
Write a single query to insert two records into the `employees` table:
- John Doe, hired on '2023-01-15', salary 65000.00
- Jane Smith, hired on '2023-02-20', salary 72000.50
*(Assume `emp_id` is handled automatically)*

**10. Data Querying (`SELECT` & Filtering)**
Write a query to fetch the `first_name`, `last_name`, and `salary` of all employees whose salary is greater than 70000. Sort the results by `salary` in descending order.

---
---

<details>
<summary><b>Click here to view the Answer Key</b></summary>

### Part 1: Theory Answers
1. **C) `ALTER`** (`INSERT` is DML, `SELECT` is DQL, `COMMIT` is TCL).
2. **C)** `TRUNCATE` is DDL and faster; `DELETE` is DML and removes row by row.
3. **B) Create Table As Select** (Used to create a new table from the results of a SELECT query).
4. **C)** The new record is skipped, and no error is thrown.
5. **D) `ENUM`** (Best for a predefined set of mutually exclusive values).

### Part 2: Practical Answers

**6.** 
```sql
CREATE DATABASE mock_db;
USE mock_db;
```

**7.**
```sql
CREATE TABLE employees (
    emp_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50),
    hire_date DATE
);
```

**8.**
```sql
ALTER TABLE employees 
ADD salary DECIMAL(8, 2);
```

**9.**
```sql
INSERT INTO employees (first_name, last_name, hire_date, salary) 
VALUES 
    ('John', 'Doe', '2023-01-15', 65000.00),
    ('Jane', 'Smith', '2023-02-20', 72000.50);
```

**10.**
```sql
SELECT first_name, last_name, salary 
FROM employees 
WHERE salary > 70000 
ORDER BY salary DESC;
```

</details>
