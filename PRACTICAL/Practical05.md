==================================================
MYSQL PRACTICAL 05
DATE: 12 AUGUST 2026
==================================================


1. INSERT IGNORE
==================================================

Explanation:
Ignores duplicate-key errors.


INSERT IGNORE INTO student
VALUES(101,"Anil",30);

Output:

Query OK, 0 rows affected, 1 warning


Use:
When duplicate records should be ignored.


==================================================
2. ON DUPLICATE KEY UPDATE
==================================================

Explanation:
Updates the record if the key already exists.


INSERT INTO student
VALUES(101,"Abhi",20)
ON DUPLICATE KEY UPDATE
name="Harsh", age=22;


Output:

+-----+-------+------+
| id  | name  | age  |
+-----+-------+------+
| 101 | Harsh | 22   |
+-----+-------+------+


Explanation:
ID 101 already exists, so the record is updated.


==================================================
3. NEW RECORD WITH ON DUPLICATE KEY
==================================================

INSERT INTO student
VALUES(102,"Abhi",20)
ON DUPLICATE KEY UPDATE
name="Harsh", age=22;


Output:

+-----+-------+------+
| id  | name  | age  |
+-----+-------+------+
| 101 | Harsh | 22   |
| 102 | Abhi  | 20   |
+-----+-------+------+


Explanation:
ID 102 does not exist, so a new record is inserted.


==================================================
4. SHOW CREATE TABLE
==================================================

SHOW CREATE TABLE student;


Explanation:
Shows the complete CREATE TABLE statement.


Output:

PRIMARY KEY (`id`)


==================================================
5. TRUNCATE
==================================================

TRUNCATE TABLE student;


Explanation:
Deletes all records from the table.


SELECT * FROM student;


Output:

Empty set


Important:
TRUNCATE removes all rows but keeps the table structure.


==================================================
6. TRUNCATE AND DESC
==================================================

TRUNCATE TABLE student;

DESC student;


Output:

+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | NO   | PRI | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
| age   | int         | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+


Explanation:
Table structure remains after TRUNCATE.


==================================================
7. AUTO_INCREMENT WITH TRUNCATE
==================================================

CREATE TABLE pytruncate(
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(20)
);


INSERT INTO pytruncate(name)
VALUES("Anil"),("Abhi");


SELECT * FROM pytruncate;


Output:

+----+------+
| id | name |
+----+------+
| 1  | Anil |
| 2  | Abhi |
+----+------+


==================================================
8. TRUNCATE AUTO_INCREMENT TABLE
==================================================

TRUNCATE TABLE pytruncate;


SELECT * FROM pytruncate;


Output:

Empty set


Insert again:

INSERT INTO pytruncate(name)
VALUES("Anil");


SELECT * FROM pytruncate;


Output:

+----+------+
| id | name |
+----+------+
| 1  | Anil |
+----+------+


Explanation:
TRUNCATE resets AUTO_INCREMENT to its starting value.


==================================================
QUICK REVISION
==================================================

INSERT IGNORE
→ Ignores duplicate-key errors.

ON DUPLICATE KEY UPDATE
→ Updates an existing record.

TRUNCATE
→ Deletes all records.

DESC
→ Shows table structure.

SHOW CREATE TABLE
→ Shows the CREATE TABLE statement.

TRUNCATE + AUTO_INCREMENT
→ Resets AUTO_INCREMENT.