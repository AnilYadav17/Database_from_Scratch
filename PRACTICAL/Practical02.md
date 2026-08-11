==================================================
# MYSQL DATABASE, TABLE & DATA BASICS
==================================================


### 1. LOGIN TO MYSQL

Command:
mysql -u root -p

Explanation:
Logs into MySQL using the root user and password.

**Output:**
```text
Welcome to the MySQL monitor.
Server version: 8.0.46-0ubuntu0.24.04.3 (Ubuntu)

```


==================================================
# DATABASE CREATION
==================================================


### 2. CREATE DATABASE

**Query:**
```sql
CREATE DATABASE batch18;
```

**Explanation:**
Creates a new database named batch18.

**Output:**
```text
Query OK, 1 row affected (1.30 sec)


### 3. SHOW DATABASES

**Query:**
```sql
SHOW DATABASES;
```

**Explanation:**
Displays all databases available in MySQL.

**Output:**
```text
+--------------------+
| Database           |
+--------------------+
| Bank               |
| DBMS               |
| Students           |
| attendance_db1     |
| batch18            |
| cricket            |
| db1                |
| information_schema |
| mysql              |
| performance_schema |
| phpmyadmin         |
| sys                |
+--------------------+
12 rows in set (0.09 sec)


### 4. CREATE EXISTING DATABASE

**Query:**
```sql
CREATE DATABASE batch18;
```

**Explanation:**
Gives an error because batch18 already exists.

**Output:**
```text
ERROR 1007 (HY000): Can't create database 'batch18'; database exists


### 5. CREATE DATABASE IF NOT EXISTS

**Query:**
```sql
CREATE DATABASE IF NOT EXISTS batch18;
```

**Explanation:**
Creates the database only if it does not already exist.

**Output:**
```text
Query OK, 1 row affected, 1 warning (0.18 sec)
```


Note:
The warning occurs because batch18 already exists.


### 6. SELECT DATABASE

**Query:**
```sql
USE batch18;
```

**Explanation:**
Selects batch18 as the current database.

**Output:**
```text
Database changed


### 7. WRONG DATABASE SYNTAX

**Query:**
```sql
SELECT @DATABASE();
```

**Explanation:**
Incorrect syntax because DATABASE() is a function.

**Output:**
```text
ERROR 1064 (42000): You have an error in your SQL syntax;


### 8. WRONG @@DATABASE SYNTAX

**Query:**
```sql
SELECT @@DATABASE();
```

**Explanation:**
Incorrect syntax because DATABASE() is not used with @@.

**Output:**
```text
ERROR 1064 (42000): You have an error in your SQL syntax;


### 9. CHECK CURRENT DATABASE

**Query:**
```sql
SELECT DATABASE();
```

**Explanation:**
Shows the currently selected database.

**Output:**
```text
+------------+
| database() |
+------------+
| batch18    |
+------------+


### 10. CREATE ANOTHER DATABASE

**Query:**
```sql
CREATE DATABASE newone;
```

**Explanation:**
Creates a new database named newone.

**Output:**
```text
Query OK, 1 row affected (0.24 sec)


### 11. USE NEWONE

**Query:**
```sql
USE newone;
```

**Explanation:**
Selects newone as the current database.

**Output:**
```text
Database changed


### 12. CHECK CURRENT DATABASE

**Query:**
```sql
SELECT DATABASE();
```

**Explanation:**
Shows the currently selected database.

**Output:**
```text
+------------+
| database() |
+------------+
| newone     |
+------------+


### 13. DROP DATABASE

**Query:**
```sql
DROP DATABASE newone;
```

**Explanation:**
Permanently deletes the newone database.

**Output:**
```text
Query OK, 0 rows affected (1.25 sec)


### 14. USE NON-EXISTING DATABASE

**Query:**
```sql
USE batck18;
```

**Explanation:**
Gives an error because batck18 does not exist.

**Output:**
```text
ERROR 1049 (42000): Unknown database 'batck18'


### 15. USE CORRECT DATABASE

**Query:**
```sql
USE batch18;
```

**Explanation:**
Selects the existing batch18 database.

**Output:**
```text
Database changed


### 16. DROP DATABASE IF EXISTS

**Query:**
```sql
DROP DATABASE IF EXISTS newone;
```

**Explanation:**
Deletes newone if it exists and avoids an error if it does not exist.

**Output:**
```text
Query OK, 0 rows affected, 1 warning (0.07 sec)

```


==================================================
# TABLE CREATION
==================================================


### 17. CREATE STUDENT TABLE

**Query:**
```sql
CREATE TABLE student(
    id INT,
    name VARCHAR(20),
    age INT
);
```

**Explanation:**
Creates a student table with id, name and age columns.

**Output:**
```text
Query OK, 0 rows affected (7.56 sec)


### 18. DESCRIBE TABLE

**Query:**
```sql
DESC student;
```

**Explanation:**
Shows the structure of the student table.

**Output:**
```text
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | YES  |     | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
| age   | int         | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+


### 19. SHOW TABLES

**Query:**
```sql
SHOW TABLES;
```

**Explanation:**
Displays all tables in the current database.

**Output:**
```text
+-------------------+
| Tables_in_batch18 |
+-------------------+
| student           |
+-------------------+


### 20. CREATE TABLE A

**Query:**
```sql
CREATE TABLE A(A INT);
```

**Explanation:**
Creates a table named A with one integer column named A.

**Output:**
```text
Query OK, 0 rows affected (2.15 sec)


### 21. DESCRIBE TABLE A

**Query:**
```sql
DESC A;
```

**Explanation:**
Shows the structure of table A.

**Output:**
```text
+-------+------+------+-----+---------+-------+
| Field | Type | Null | Key | Default | Extra |
+-------+------+------+-----+---------+-------+
| A     | int  | YES  |     | NULL    |       |
+-------+------+------+-----+---------+-------+


### 22. SHOW TABLES

**Query:**
```sql
SHOW TABLES;
```

**Explanation:**
Displays all tables in batch18.

**Output:**
```text
+-------------------+
| Tables_in_batch18 |
+-------------------+
| A                 |
| student           |
+-------------------+

```


==================================================
# SELECT DATA
==================================================


### 23. SELECT ALL DATA FROM STUDENT

**Query:**
```sql
SELECT * FROM student;
```

**Explanation:**
Displays all columns and all rows from student.

**Output:**
```text
Empty set (0.07 sec)
```


Note:
The table exists, but no data has been inserted.


### 24. SELECT TABLE USING WRONG CASE

**Query:**
```sql
SELECT * FROM a;
```

**Explanation:**
Gives an error because the actual table name is A.

**Output:**
```text
ERROR 1146 (42S02): Table 'batch18.a' doesn't exist


### 25. SELECT TABLE A

**Query:**
```sql
SELECT * FROM A;
```

**Explanation:**
Displays all data from table A.

**Output:**
```text
Empty set (0.02 sec)

```


==================================================
# PRIMARY KEY
==================================================


### 26. CREATE STUDENT1 TABLE

**Query:**
```sql
CREATE TABLE student1(
    id INT PRIMARY KEY,
    name VARCHAR(20),
    age INT
);
```

**Explanation:**
Creates student1 with id as the PRIMARY KEY.

**Output:**
```text
Query OK, 0 rows affected (1.47 sec)


PRIMARY KEY:
A PRIMARY KEY uniquely identifies each row in a table.

Important Points:

• PRIMARY KEY must contain UNIQUE values.
• PRIMARY KEY cannot contain NULL.
• A table can have only one PRIMARY KEY.
• PRIMARY KEY uniquely identifies every record.

```


==================================================
# CREATE TABLE AS SELECT
==================================================


### 27. CREATE EMPLOYEE FROM STUDENT

**Query:**
```sql
CREATE TABLE employee AS SELECT * FROM student;
```

**Explanation:**
Creates employee table with the same columns and copies all data from student.

**Output:**
```text
Query OK, 0 rows affected (1.83 sec)
Records: 0  Duplicates: 0  Warnings: 0
```


Note:
Student was empty at this time, so employee also contains no records.


### 28. DESCRIBE EMPLOYEE

**Query:**
```sql
DESC employee;
```

**Explanation:**
Shows the structure of the employee table.

**Output:**
```text
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | YES  |     | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
| age   | int         | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+


### 29. SHOW TABLES

**Query:**
```sql
SHOW TABLES;
```

**Explanation:**
Shows all tables currently present in batch18.

**Output:**
```text
+-------------------+
| Tables_in_batch18 |
+-------------------+
| A                 |
| employee          |
| student           |
| student1          |
+-------------------+


### 30. CREATE TABLE WITH SELECTED COLUMNS

**Query:**
```sql
CREATE TABLE emp2 AS SELECT id,name FROM student;
```

**Explanation:**
Creates emp2 using only the id and name columns from student.

**Output:**
```text
Query OK, 0 rows affected (1.38 sec)
Records: 0  Duplicates: 0  Warnings: 0


### 31. DESCRIBE EMP2

**Query:**
```sql
DESC emp2;
```

**Explanation:**
Shows the structure of emp2.

**Output:**
```text
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | YES  |     | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+

```


==================================================
# CREATE TABLE WITHOUT DATA
==================================================


### 32. CREATE EMP3 WITHOUT DATA

**Query:**
```sql
CREATE TABLE emp3 AS SELECT * FROM student WHERE 1=2;
```

**Explanation:**
Creates emp3 with the same structure as student but copies no records.

**Output:**
```text
Query OK, 0 rows affected (1.67 sec)
Records: 0  Duplicates: 0  Warnings: 0


IMPORTANT:

WHERE 1=2

→ 1=2 is always FALSE.

Therefore:
No rows are copied.

But:
The table structure is created.

```


==================================================
# INSERT DATA
==================================================


### 33. INSERT RECORD INTO STUDENT

**Query:**
```sql
INSERT INTO student VALUES(101,"Anil",30);
```

**Explanation:**
Inserts one student record into the student table.

**Output:**
```text
Query OK, 1 row affected (0.17 sec)


### 34. WRONG SELECT KEYWORD

**Query:**
```sql
SELECT * FORM student;
```

**Explanation:**
Gives an error because FORM is incorrect; the correct keyword is FROM.

**Output:**
```text
ERROR 1064 (42000): You have an error in your SQL syntax;


### 35. WRONG SELECT ON STUDENT1

**Query:**
```sql
SELECT * FORM student1;
```

**Explanation:**
Again gives an error because FORM should be FROM.

**Output:**
```text
ERROR 1064 (42000): You have an error in your SQL syntax;


### 36. SELECT STUDENT1

**Query:**
```sql
SELECT * FROM student1;
```

**Explanation:**
Displays all records from student1.

**Output:**
```text
Empty set (0.06 sec)
```


Note:
student1 has no records yet.


### 37. SELECT STUDENT

**Query:**
```sql
SELECT * FROM student;
```

**Explanation:**
Displays all records from student.

**Output:**
```text
+------+------+------+
| id   | name | age  |
+------+------+------+
|  101 | Anil |   30 |
+------+------+------+
1 row in set (0.00 sec)

```


==================================================
# COPY TABLE WITHOUT DATA
==================================================


### 38. CREATE COPY1 WITHOUT DATA

**Query:**
```sql
CREATE TABLE copy1 AS SELECT * FROM student WHERE 1=2;
```

**Explanation:**
Creates copy1 with the same columns as student but without copying data.

**Output:**
```text
Query OK, 0 rows affected (2.08 sec)
Records: 0  Duplicates: 0  Warnings: 0


### 39. CHECK COPY1

**Query:**
```sql
SELECT * FROM copy1;
```

**Explanation:**
Displays data from copy1.

**Output:**
```text
Empty set (0.00 sec)

```

Reason:
WHERE 1=2 prevented the rows from being copied.


==================================================
# COPY TABLE WITH DATA
==================================================


### 40. CREATE COPY2 WITH DATA

**Query:**
```sql
CREATE TABLE copy2 AS SELECT * FROM student;
```

**Explanation:**
Creates copy2 with the same columns and copies all data from student.

**Output:**
```text
Query OK, 1 row affected (1.98 sec)
Records: 1  Duplicates: 0  Warnings: 0


### 41. CHECK COPY2

**Query:**
```sql
SELECT * FROM copy2;
```

**Explanation:**
Displays the copied data from copy2.

**Output:**
```text
+------+------+------+
| id   | name | age  |
+------+------+------+
|  101 | Anil |   30 |
+------+------+------+
1 row in set (0.00 sec)

```


==================================================
# IMPORTANT CONCEPT
==================================================

CREATE TABLE new_table AS SELECT ...

This is called:

CTAS
(Create Table As Select)


Example 1:
CREATE TABLE employee AS SELECT * FROM student;

→ Copies all columns and existing rows.


Example 2:
CREATE TABLE emp2 AS SELECT id,name FROM student;

→ Copies only id and name columns.


Example 3:
CREATE TABLE copy1 AS SELECT * FROM student WHERE 1=2;

→ Copies structure but no rows.


Example 4:
CREATE TABLE copy2 AS SELECT * FROM student;

→ Copies structure and rows.


==================================================
# CTAS QUICK COMPARISON
==================================================

COMMAND:

CREATE TABLE employee AS SELECT * FROM student;

Result:
Structure + Data


COMMAND:

CREATE TABLE emp2 AS SELECT id,name FROM student;

Result:
Selected Columns + Data


COMMAND:

CREATE TABLE copy1 AS SELECT * FROM student WHERE 1=2;

Result:
Structure Only


COMMAND:

CREATE TABLE copy2 AS SELECT * FROM student;

Result:
Structure + Data


==================================================
# IMPORTANT COMMANDS
==================================================

CREATE DATABASE database_name;

→ Creates a database.


SHOW DATABASES;

→ Shows all databases.


USE database_name;

→ Selects a database.


SELECT DATABASE();

→ Shows the current database.


DROP DATABASE database_name;

→ Deletes a database.


CREATE TABLE table_name(...);

→ Creates a table.


DESC table_name;

→ Shows table structure.


SHOW TABLES;

→ Shows all tables.


SELECT * FROM table_name;

→ Displays all data.


INSERT INTO table_name VALUES(...);

→ Inserts a record.


PRIMARY KEY

→ Uniquely identifies each row.


CREATE TABLE new_table AS SELECT ...

→ Creates a new table using data/structure from another table.


WHERE 1=2

→ Always FALSE, so no records are copied.


==================================================
# IMPORTANT ERRORS FROM YOUR PRACTICE
==================================================

### 1. Database already exists:

CREATE DATABASE batch18;

ERROR 1007:
Database exists.


### 2. Wrong database name:

USE batck18;

ERROR 1049:
Unknown database.


### 3. Wrong DATABASE syntax:

SELECT @DATABASE();

ERROR 1064:
Syntax error.


### 4. Wrong table name/case:

SELECT * FROM a;

ERROR 1146:
Table 'batch18.a' doesn't exist.


### 5. Wrong keyword:

SELECT * FORM student;

ERROR 1064:
Syntax error.

Correct:
SELECT * FROM student;


==================================================
# CURRENT DATABASE
==================================================

batch18


CURRENT TABLES
==============
# 
A
employee
emp2
emp3
copy1
copy2
student
student1
