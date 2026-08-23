# 🗄️ Database From Scratch - Mock Assessment Answer Key

Here are the answers to the comprehensive 25-question mock assessment.

---

## 📚 Part 1: Theory Answers

| Question | Correct Answer | Explanation |
| :--- | :--- | :--- |
| **1.** | **C) `UPDATE`** | `CREATE` and `ALTER` are DDL; `GRANT` is DCL. |
| **2.** | **C)** | `TRUNCATE` is a DDL command that resets the table and `AUTO_INCREMENT`, while `DELETE` is a DML command that removes rows one by one. |
| **3.** | **A)** | A table can only have **one** Primary Key, though it can be a composite key spanning multiple columns. |
| **4.** | **B)** | Create Table As Select (CTAS). |
| **5.** | **C)** | The new record is skipped, a warning is generated, and the execution continues without throwing an error. |
| **6.** | **B) `ON DUPLICATE KEY UPDATE`** | Used to gracefully handle duplicate key insertions by updating the existing row instead. |
| **7.** | **B) `1`** | `AUTO_INCREMENT` starts at 1 by default unless specified otherwise. |
| **8.** | **D) `DROP TABLE`** | Drops the table structure and its data completely. |
| **9.** | **A)** | `ALTER TABLE users ADD COLUMN birth_date DATE;` (The `COLUMN` keyword is technically optional, but this is standard syntax). |
| **10.** | **A)** | `ALTER TABLE users MODIFY age TINYINT;` |
| **11.** | **B) `ENUM`** | Best for storing one value from a predefined list. |
| **12.** | **C) `4`** | `DECIMAL(6,2)` means 6 total digits, 2 of which are after the decimal, leaving 4 before. |
| **13.** | **B)** | `DATE` stores `YYYY-MM-DD`, while `DATETIME` stores `YYYY-MM-DD HH:MM:SS`. |
| **14.** | **B)** | `SET` allows selecting multiple values from the predefined list at the same time. |
| **15.** | **C) `NOW()`** | Returns both current date and time. |
| **16.** | **B) `WHERE`** | Used to filter records in a `SELECT`, `UPDATE`, or `DELETE` statement. |
| **17.** | **C) `WHERE email IS NULL`** | You cannot use `=` with `NULL`. |
| **18.** | **B)** | Ascending (`ASC`) is the default sort order. |
| **19.** | **B)** | Undoes transactions that have not yet been saved to the database. |
| **20.** | **B)** | `AND` is evaluated before `OR` based on standard SQL operator precedence. |

---

## 💻 Part 2: Practical Answers

### **21. Database & Table Creation**
```sql
CREATE DATABASE academy_db;
USE academy_db;

CREATE TABLE courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    price DECIMAL(6, 2)
);
```

### **22. Table Alteration**
```sql
ALTER TABLE courses 
ADD instructor_name VARCHAR(50);
```

### **23. Data Insertion**
```sql
INSERT INTO courses (course_name, price, instructor_name) 
VALUES 
    ('SQL Basics', 49.99, 'John Doe'),
    ('Advanced MySQL', 89.50, 'Jane Smith');
```

### **24. Table Cloning (CTAS)**
```sql
CREATE TABLE courses_backup AS 
SELECT * FROM courses;
```

### **25. Querying & Sorting**
```sql
SELECT course_name, price 
FROM courses 
WHERE price > 50.00 
ORDER BY price DESC;
```
