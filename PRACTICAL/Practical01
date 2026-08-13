===========================
# MySQL Basic SELECT Commands
===========================

### 1. Check MySQL Version
**Query:**
```sql
SELECT VERSION();
```

**Explanation:**
Returns the installed MySQL server version.

**Output:**
```text
+-------------------------+
| version()               |
+-------------------------+
| 8.0.46-0ubuntu0.24.04.3 |
+-------------------------+


### 2. Current Date and Time
**Query:**
```sql
SELECT NOW();
```

**Explanation:**
Returns the current system date and time.

**Output:**
```text
+---------------------+
| now()               |
+---------------------+
| 2026-08-06 10:20:01 |
+---------------------+


### 3. Current Time
**Query:**
```sql
SELECT CURTIME();
```

**Explanation:**
Returns only the current time.

**Output:**
```text
+-----------+
| curtime() |
+-----------+
| 10:20:32  |
+-----------+


### 4. Current Logged-in User (Wrong)
**Query:**
```sql
SELECT USER;
```

**Explanation:**
ERROR because USER is treated as a column name.

**Output:**
```text
ERROR 1054 (42S22): Unknown column 'user' in 'field list'


### 5. Current Logged-in User (Correct)
**Query:**
```sql
SELECT USER();
```

**Explanation:**
Returns the current MySQL user and host.

**Output:**
```text
+----------------+
| user()         |
+----------------+
| root@localhost |
+----------------+


### 6. Current Database
**Query:**
```sql
SELECT DATABASE();
```

**Explanation:**
Returns the currently selected database.

**Output:**
```text
+------------+
| database() |
+------------+
| NULL       |
+------------+
```


Note:
NULL means no database is selected.


### 7. Show All Databases
**Query:**
```sql
SHOW DATABASES;
```

**Explanation:**
Displays all databases in MySQL.

**Output:**
```text
+--------------------+
| Database           |
+--------------------+
| Bank               |
| DBMS               |
| Students           |
| attendance_db1     |
| cricket            |
| db1                |
| information_schema |
| mysql              |
| performance_schema |
| phpmyadmin         |
| sys                |
+--------------------+


### 8. Hostname
**Query:**
```sql
SELECT @@hostname;
```

**Explanation:**
Returns the name of the computer running MySQL.

**Output:**
```text
+------------+
| @@hostname |
+------------+
| Anil       |
+------------+


### 9. MySQL Port Number
**Query:**
```sql
SELECT @@port;
```

**Explanation:**
Returns the port number used by MySQL.

**Output:**
```text
+--------+
| @@port |
+--------+
|   3306 |
+--------+


### 10. Password Variable (Wrong)
**Query:**
```sql
SELECT @@password;
```

**Explanation:**
ERROR because this system variable does not exist.

**Output:**
```text
ERROR 1193 (HY000): Unknown system variable 'password'


### 11. Addition
**Query:**
```sql
SELECT 10+20;
```

**Explanation:**
Adds two numbers.

**Output:**
```text
+-------+
| 10+20 |
+-------+
|    30 |
+-------+


### 12. Modulus (%)
**Query:**
```sql
SELECT 20%2;
```

**Explanation:**
Returns the remainder after division.

**Output:**
```text
+------+
| 20%2 |
+------+
|    0 |
+------+


### 13. Square Root
**Query:**
```sql
SELECT SQRT(10);
```

**Explanation:**
Returns the square root of a number.

**Output:**
```text
+--------------------+
| sqrt(10)           |
+--------------------+
| 3.1622776601683795 |
+--------------------+


### 14. Wrong Function Name
**Query:**
```sql
SELECT PW(2,5);
```

**Explanation:**
ERROR because PW() is not a valid MySQL function.

**Output:**
```text
ERROR 1046 (3D000): No database selected
```


Note:
The intended function is POW(). The error shown is because MySQL interpreted PW as something else while no database was selected.


### 15. Power Function
**Query:**
```sql
SELECT POW(2,5);
```

**Explanation:**
Returns 2 raised to the power of 5.

**Output:**
```text
+----------+
| pow(2,5) |
+----------+
|       32 |
+----------+


### 16. Random Number (Seed = 10)
**Query:**
```sql
SELECT RAND(10);
```

**Explanation:**
Returns a random number based on seed value 10.

**Output:**
```text
+--------------------+
| rand(10)           |
+--------------------+
| 0.6570515219653505 |
+--------------------+


### 17. Random Number (Seed = 100)
**Query:**
```sql
SELECT RAND(100);
```

**Explanation:**
Returns the same random number every time because the seed is fixed.

**Output:**
```text
+---------------------+
| rand(100)           |
+---------------------+
| 0.17353134804734155 |
+---------------------+


### 18. Same Seed Again
**Query:**
```sql
SELECT RAND(100);
```

**Explanation:**
Same seed produces the same random number.

**Output:**
```text
+---------------------+
| rand(100)           |
+---------------------+
| 0.17353134804734155 |
+---------------------+


### 19. Random Number (Seed = 1)
**Query:**
```sql
SELECT RAND(1);
```

**Explanation:**
Returns a random number based on seed value 1.

**Output:**
```text
+---------------------+
| rand(1)             |
+---------------------+
| 0.40540353712197724 |
+---------------------+


### 20. Same Seed Again
**Query:**
```sql
SELECT RAND(1);
```

**Explanation:**
Same seed gives the same random number again.

**Output:**
```text
+---------------------+
| rand(1)             |
+---------------------+
| 0.40540353712197724 |
+---------------------+
```


==========================
# Important Exam Points
==========================

• VERSION() → MySQL version.
• NOW() → Current date and time.
• CURTIME() → Current time only.
• USER() → Current MySQL user.
• DATABASE() → Current selected database.
• SHOW DATABASES; → Lists all databases.
• @@hostname → Computer name.
• @@port → MySQL port number.
• SQRT(n) → Square root.
• POW(a,b) → a raised to power b.
• RAND(seed) → Random number; same seed = same output.
• % → Modulus (remainder).
• NULL → No value or no database selected.
