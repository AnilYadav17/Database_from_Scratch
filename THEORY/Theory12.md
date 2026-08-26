# Practical 12 — UPDATE, CASE Statements & UPDATE with LIMIT

## 1. Multiple Column Updates

We can update multiple columns in the same `UPDATE` statement.

```sql
UPDATE employeeup
SET salary = 2000,
    city = 'Bhopal',
    department = 'HR'
WHERE employee_id = 5;
```

---

## 2. UPDATE Using Comparison Operator

We can use comparison operators such as `<`, `>`, `=`, `<=`, and `>=` with `UPDATE`.

```sql
UPDATE employeeup
SET salary = 55000
WHERE salary < 50000;
```

```sql
UPDATE employeeup
SET salary = 90000
WHERE experience = 5;
```

---

## 3. UPDATE Using AND

### i) Give 5000 increment to IT employees having at least 5 years of experience.

```sql
UPDATE employeeup
SET salary = salary + 5000
WHERE department = 'IT'
AND experience >= 5;
```

> **Note:** The original query used `salary + 50000`, which gives a ₹50,000 increment, not ₹5,000.

---

## 4. UPDATE Using OR

### ii) Give an increment of 3000 to employees of HR or Finance department.

```sql
UPDATE employeeup
SET salary = salary + 3000
WHERE department = 'HR'
   OR department = 'Finance';
```

---

## 5. UPDATE Using IN

### iii) Give an increment of 4000 to employees in HR, Finance, or Sales.

```sql
UPDATE employeeup
SET salary = salary + 4000
WHERE department IN ('HR', 'Finance', 'Sales');
```

---

## 6. UPDATE Using NOT IN

### iv) Give an increment of 10000 to all employees outside HR and Finance departments.

```sql
UPDATE employeeup
SET salary = salary + 10000
WHERE department NOT IN ('HR', 'Finance');
```

---

## 7. UPDATE Using BETWEEN

### v) Give an increment of 7000 to employees whose salary is between 60000 and 70000.

```sql
UPDATE employeeup
SET salary = salary + 7000
WHERE salary BETWEEN 60000 AND 70000;
```

---

## 8. UPDATE Using LIKE

### vi) Move all employees to IT department whose name starts with A.

```sql
UPDATE employeeup
SET department = 'IT'
WHERE employee_name LIKE 'A%';
```

---

## 9. UPDATE Using IS NULL

### vii) Update employee cities to Goa where city is NULL.

```sql
UPDATE employeeup
SET city = 'Goa'
WHERE city IS NULL;
```

---

## 10. UPDATE Using Percentage

### viii) Give a 10% increment to all IT employees.

```sql
UPDATE employeeup
SET salary = salary * 1.10
WHERE department = 'IT';
```

---

## 11. UPDATE Using Multiple Conditions

### ix) Give a 15% increment to IT employees having more than 5 years of experience and salary below 80000.

```sql
UPDATE employeeup
SET salary = salary * 1.15
WHERE department = 'IT'
  AND experience >= 5
  AND salary < 80000;
```

---

## 12. UPDATE Using Joining Date

### x) Give a 10% increment to employees who joined before 2020.

```sql
UPDATE employeeup
SET salary = salary * 1.10
WHERE joining_date < '2020-01-01';
```

---

# CASE STATEMENTS

## 13. What is CASE?

`CASE` is a conditional expression in MySQL used to return different values based on different conditions.

It works similarly to `if-else` in programming languages.

### Syntax

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ELSE result
END
```

---

## 14. CASE with SELECT

We can use `CASE` to create a new calculated/category column based on conditions.

```sql
SELECT
    employee_name,
    salary,
    CASE
        WHEN salary >= 120000 THEN 'High'
        WHEN salary >= 60000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employeeup;
```

> **Important:** Conditions are checked from top to bottom. The first matching `WHEN` is executed.

---

## 15. CASE with ORDER BY

`CASE` with `ORDER BY` is used when we want custom sorting instead of normal alphabetical or numerical sorting.

### Example

```sql
SELECT employee_name, department, salary
FROM employeeup
ORDER BY
    CASE
        WHEN department = 'IT' THEN 1
        WHEN department = 'HR' THEN 2
        WHEN department = 'Finance' THEN 3
        ELSE 4
    END;
```

### Custom Order

1. IT
2. HR
3. Finance
4. Other departments

---

## 16. CASE with UPDATE

We can use `CASE` inside `UPDATE` to apply different changes to different rows.

### WAQ: Give 10% increment to IT, 8% to HR, and 7% to Finance.

```sql
UPDATE employeeup
SET salary =
    CASE
        WHEN department = 'IT' THEN salary * 1.10
        WHEN department = 'HR' THEN salary * 1.08
        WHEN department = 'Finance' THEN salary * 1.07
        ELSE salary
    END;
```

> **Important:** `ELSE salary` keeps the salary unchanged for other departments.

---

## 17. CASE with Experience

### WAQ:

- Experience greater than 8 years → 15% increment
- Experience greater than 5 years → 10% increment
- Experience greater than 3 years → 7% increment
- Otherwise → 5% increment

```sql
UPDATE employeeup
SET salary =
    CASE
        WHEN experience > 8 THEN salary * 1.15
        WHEN experience > 5 THEN salary * 1.10
        WHEN experience > 3 THEN salary * 1.07
        ELSE salary * 1.05
    END;
```

> **Important:** The order matters. A condition such as `experience > 8` must be checked before `experience > 5`.

---

# UPDATE with LIMIT

## 18. What is UPDATE with LIMIT?

`LIMIT` can restrict the number of rows affected by an `UPDATE`.

It is useful when we want to update only a specific number of matching rows.

---

## 19. Update One HR Employee

### WAQ: Update the status of one HR employee to Inactive.

```sql
UPDATE employeeup
SET status = 'Inactive'
WHERE department = 'HR'
LIMIT 1;
```

---

## 20. Give Increment to Lowest-Paid IT Employee

### WAQ: Give 5000 increment to the lowest-paid IT employee.

```sql
UPDATE employeeup
SET salary = salary + 5000
WHERE department = 'IT'
ORDER BY salary ASC
LIMIT 1;
```

### How it works

```text
WHERE department = 'IT'
        ↓
Select IT employees
        ↓
ORDER BY salary ASC
        ↓
Lowest salary comes first
        ↓
LIMIT 1
        ↓
Only one employee is updated
```

---

# Quick Revision

| Concept    | Purpose                         |
| ---------- | ------------------------------- |
| `UPDATE`   | Modify existing records         |
| `SET`      | Specify new values              |
| `WHERE`    | Select rows to update           |
| `AND`      | Apply multiple conditions       |
| `OR`       | Match any one condition         |
| `IN`       | Match multiple values           |
| `NOT IN`   | Exclude multiple values         |
| `BETWEEN`  | Match a range                   |
| `LIKE`     | Pattern matching                |
| `IS NULL`  | Find NULL values                |
| `CASE`     | Apply conditional logic         |
| `ORDER BY` | Sort rows                       |
| `LIMIT`    | Restrict affected/returned rows |

## UPDATE Flow

```text
UPDATE
   ↓
SET
   ↓
WHERE
   ↓
Condition filters rows
   ↓
Matching rows are updated
```

## CASE Flow

```text
CASE
   ↓
WHEN condition
   ↓
THEN result
   ↓
Next WHEN if condition is false
   ↓
ELSE
   ↓
END
```
