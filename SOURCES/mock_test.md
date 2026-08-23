# 🗄️ Database From Scratch - Comprehensive Mock Assessment

Welcome to the comprehensive mock assessment! This test contains **25 questions** designed to evaluate your understanding of Database Management Systems, MySQL concepts, and SQL commands (DDL, DML, DQL, TCL).

> 💡 **Note:** The answer key has been provided in a separate file: `mock_test_answers.md`. Try to complete this test before checking the answers!

---

## 📚 Part 1: Theory and Concepts (Multiple Choice & Short Answer)

### Section A: SQL Languages & Basics

**1. Which of the following SQL commands belongs to Data Manipulation Language (DML)?**
- [ ] A) `CREATE`
- [ ] B) `GRANT`
- [ ] C) `UPDATE`
- [ ] D) `ALTER`

**2. What is the primary difference between `DELETE` and `TRUNCATE`?**
- [ ] A) `TRUNCATE` allows a `WHERE` clause, while `DELETE` does not.
- [ ] B) `DELETE` removes table structure, while `TRUNCATE` only removes data.
- [ ] C) `TRUNCATE` is a DDL command that resets the table and `AUTO_INCREMENT`, while `DELETE` is a DML command that removes rows one by one.
- [ ] D) `DELETE` is used to remove columns, while `TRUNCATE` is used to remove rows.

**3. Which of the following statements about Primary Keys is FALSE?**
- [ ] A) A table can have multiple Primary Keys.
- [ ] B) Primary Key columns cannot contain `NULL` values.
- [ ] C) Primary Keys ensure all rows in a table are unique.
- [ ] D) A Primary Key can consist of multiple columns (Composite Primary Key).

**4. What does the `CTAS` approach stand for in SQL?**
- [ ] A) Copy Table And Save
- [ ] B) Create Table As Select
- [ ] C) Commit Transaction And Save
- [ ] D) Create Table Alter Select

### Section B: Advanced Table Operations

**5. When using the `INSERT IGNORE` command, what happens if you try to insert a record with a duplicate primary key?**
- [ ] A) The transaction fails completely and throws an error.
- [ ] B) The existing record is overwritten with the new data.
- [ ] C) The new record is skipped, a warning is generated, and the execution continues without throwing an error.
- [ ] D) The database automatically generates a new, unique primary key.

**6. Which SQL clause is used to update an existing record if an insert operation causes a unique key violation?**
- [ ] A) `UPDATE ON DUPLICATE`
- [ ] B) `ON DUPLICATE KEY UPDATE`
- [ ] C) `INSERT OR UPDATE`
- [ ] D) `REPLACE INTO`

**7. By default, what value does an `AUTO_INCREMENT` column start at in MySQL?**
- [ ] A) `0`
- [ ] B) `1`
- [ ] C) It must be specified manually.
- [ ] D) `-1`

**8. Which command is used to permanently remove a table AND its structure from the database?**
- [ ] A) `DELETE TABLE`
- [ ] B) `TRUNCATE TABLE`
- [ ] C) `REMOVE TABLE`
- [ ] D) `DROP TABLE`

### Section C: Table Alterations

**9. Which SQL statement correctly adds a new column named `birth_date` of type `DATE` to an existing table named `users`?**
- [ ] A) `ALTER TABLE users ADD COLUMN birth_date DATE;`
- [ ] B) `MODIFY TABLE users ADD birth_date DATE;`
- [ ] C) `ALTER users ADD birth_date DATE;`
- [ ] D) `UPDATE TABLE users ADD birth_date DATE;`

**10. Which command would you use to change the data type of an existing column named `age` to `TINYINT`?**
- [ ] A) `ALTER TABLE users MODIFY age TINYINT;`
- [ ] B) `ALTER TABLE users CHANGE age TINYINT;`
- [ ] C) `ALTER TABLE users RENAME age TO TINYINT;`
- [ ] D) `UPDATE TABLE users MODIFY age TINYINT;`

### Section D: Data Types

**11. Which data type is best suited for storing a user's role if the only possible values are 'Admin', 'Editor', or 'Viewer'?**
- [ ] A) `VARCHAR(50)`
- [ ] B) `ENUM`
- [ ] C) `SET`
- [ ] D) `TEXT`

**12. If a column is defined as `DECIMAL(6, 2)`, what is the maximum number of digits that can be stored before the decimal point?**
- [ ] A) `6`
- [ ] B) `2`
- [ ] C) `4`
- [ ] D) `8`

**13. What is the difference between `DATE` and `DATETIME` data types?**
- [ ] A) `DATE` stores only the year, while `DATETIME` stores the full date.
- [ ] B) `DATE` stores `YYYY-MM-DD`, while `DATETIME` stores `YYYY-MM-DD HH:MM:SS`.
- [ ] C) `DATE` is formatted as DD/MM/YYYY by default.
- [ ] D) There is no difference in MySQL.

**14. What does the `SET` data type allow that `ENUM` does not?**
- [ ] A) Storing numeric values.
- [ ] B) Selecting multiple values from the predefined list at the same time.
- [ ] C) Storing strings longer than 255 characters.
- [ ] D) Defining a default value.

### Section E: Queries & Functions

**15. Which MySQL function returns the current date and time?**
- [ ] A) `CURRENT_DATE()`
- [ ] B) `TODAY()`
- [ ] C) `NOW()`
- [ ] D) `GETDATE()`

**16. Which clause is used to filter records in a `SELECT` statement?**
- [ ] A) `ORDER BY`
- [ ] B) `WHERE`
- [ ] C) `HAVING`
- [ ] D) `FILTER`

**17. How do you correctly check if a column `email` has no value (is null) in a `WHERE` clause?**
- [ ] A) `WHERE email = NULL`
- [ ] B) `WHERE email == NULL`
- [ ] C) `WHERE email IS NULL`
- [ ] D) `WHERE email NOT EXISTS`

**18. By default, the `ORDER BY` clause sorts records in which order?**
- [ ] A) Descending (`DESC`)
- [ ] B) Ascending (`ASC`)
- [ ] C) Random
- [ ] D) Order of insertion

**19. What does the `ROLLBACK` command do?**
- [ ] A) Saves all changes permanently to the database.
- [ ] B) Undoes transactions that have not yet been saved to the database.
- [ ] C) Deletes the last inserted row.
- [ ] D) Restarts the MySQL server.

**20. In what order does SQL evaluate the `AND` and `OR` operators?**
- [ ] A) `OR` is evaluated before `AND`.
- [ ] B) `AND` is evaluated before `OR`.
- [ ] C) Evaluated left to right regardless of the operator.
- [ ] D) You must always use parentheses to specify evaluation order.

---

## 💻 Part 2: Practical Query Writing

For the following questions, write the standard MySQL query to accomplish the described task.

**21. Database & Table Creation**
Write the queries to:
1. Create a database named `academy_db`.
2. Switch to use `academy_db`.
3. Create a table named `courses` with the following columns:
   - `course_id`: Integer, Primary Key, Auto-increment.
   - `course_name`: String (max 100 characters), cannot be null.
   - `price`: Decimal format (up to 9999.99).

**22. Table Alteration**
Write the query to add a new column to the `courses` table named `instructor_name` which can hold up to 50 characters. 

**23. Data Insertion**
Write a single query to insert two records into the `courses` table:
- Course: "SQL Basics", Price: 49.99, Instructor: "John Doe"
- Course: "Advanced MySQL", Price: 89.50, Instructor: "Jane Smith"

**24. Table Cloning (CTAS)**
Write a query to create a backup table called `courses_backup` that copies all the data and structure from the `courses` table using the CTAS method.

**25. Querying & Sorting**
Write a query to fetch the `course_name` and `price` of all courses where the `price` is greater than `50.00`. Sort the results by `price` in descending order.
