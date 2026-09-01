# Advanced Primary Keys and Auto Increment

## COMPOSITE PRIMARY KEY
Sometimes one column is not sufficient, meaning a single column is not unique enough to identify a row. In that case, we create a **Composite Key**.

### Syntax
```sql
CREATE TABLE pycustomer_product (
    cid INT,
    pid INT,
    quantity INT,
    PRIMARY KEY (cid, pid)
);
```

---

## AUTO INCREMENT PROPERTY
It is a MySQL attribute used with numeric columns to automatically generate a unique number whenever a new record is inserted into a table. It is most commonly used with the `PRIMARY KEY` so that the user does not have to enter the ID manually.

Whenever a new employee joins, we would otherwise have to manually decide the next ID.

**Problems with manual IDs:**
- We may forget the ID.
- Duplicate IDs can be inserted accidentally.

To solve the above problems, `AUTO_INCREMENT` is used.

### Syntax
```sql
CREATE TABLE pyemployee5 (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(20),
    salary DECIMAL(10,2)
);
```

### Rules:
1. **Only one auto increment column per table is allowed.**
   ```sql
   mysql> CREATE TABLE pyemployee6(eid INT AUTO_INCREMENT, did INT AUTO_INCREMENT);
   ERROR 1075 (42000): Incorrect table definition; there can be only one auto column and it must be defined as a key
   ```
2. **Default Starting value:** By default, auto increment starts from 1, and by default, it increases by one.

### Changing the Starting Value:
We can change the starting value of auto increment.
```sql
CREATE TABLE pyemployee7 (
    eid INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(20)
) AUTO_INCREMENT=100;
```

### Manually Inserting an Auto Increment Value:
If we manually insert a value that is greater than the current auto increment value, MySQL updates the next auto increment value from there.
```sql
CREATE TABLE pyemployee8 (
    eid INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(20)
);

INSERT INTO pyemployee8(name) VALUES ('Katappa');
INSERT INTO pyemployee8 VALUES (10, 'Bahubali');
INSERT INTO pyemployee8(name) VALUES ('Rajmata');
```

### Auto Increment with NULL Value:
If we explicitly insert a `NULL` value into an auto increment column, MySQL treats it as if we did not provide any value and automatically generates the next sequence number.
```sql
CREATE TABLE employee5 (
    sid INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(20),
    age INT
);

INSERT INTO employee5(name, age) VALUES ('Anil', 22);
INSERT INTO employee5 VALUES (NULL, 'Abhi', 22);

SELECT * FROM employee5;
```
Output:
```text
+-----+------+------+
| sid | name | age  |
+-----+------+------+
|   1 | Anil |   22 |
|   2 | Abhi |   22 |
+-----+------+------+
```

### Auto Increment with 0:
If we insert `0` into an auto increment column, the result depends on the MySQL SQL Mode:

- **Case 1 (Default Behavior):** In most MySQL installations, if the MySQL Mode does not include `NO_AUTO_VALUE_ON_ZERO`, then inserting `0` into an auto increment column behaves exactly like inserting `NULL`. It means MySQL automatically generates the next available value.
- **Case 2:** When `NO_AUTO_VALUE_ON_ZERO` mode is enabled, then zero is treated as a normal value and stored as `0`.
