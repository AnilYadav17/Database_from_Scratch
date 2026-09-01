# Table Creation and Data Insertion

## CREATE TABLE AS SELECT (CTAS)

### 1. Definition
**CREATE TABLE AS SELECT (CTAS)** is used to create a **new table** by copying data from an existing table or from the result of a `SELECT` query.
It automatically creates the new table based on the columns returned by the `SELECT` statement.

CTAS copies:
- Selected column names
- Column data types
- Column order
- Selected data

### 2. Limitations of CTAS
CTAS **does not copy the complete table structure, rules, or database objects** from the original table.
The following things are **not copied**:
- Primary Key
- Foreign Key
- Auto Increment property
- Constraints
- Indexes
- Triggers
- Other database objects

---

## INSERT COMMAND

`INSERT` is a DML (Data Manipulation Language) command. It is used to **add new records (rows)** into a table.

### Case 1: Insert Values into All Columns
When inserting values into **all columns**, the values must be given in the **same order as the columns in the table**.

**Syntax:**
```sql
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```

**Example:**
```sql
INSERT INTO pystudent
VALUES (1, 'Anil', 85, 'Dewas');
```

### Case 2: Insert Values into Specific Columns
When we don't want to insert data into every column, or we are providing all values but not in the default order, we need to provide a column list.

**Syntax:**
```sql
INSERT INTO table_name(column1, column2, column3)
VALUES (value1, value2, value3);
```

**Example 1:**
```sql
INSERT INTO pystudent(id, name, city) VALUES (102, 'Abhi', 'Indore');
```

**Example 2:**
```sql
INSERT INTO pystudent(id, name) VALUES (103, 'Harsh');
```

**Best Practice:** Always specify the column names while inserting the data, this makes the query easier to read.

### Case 3: Insert Values into Multiple Columns
Instead of writing multiple insert statements, we can insert many rows in one statement.

**Syntax:**
```sql
INSERT INTO table_name VALUES (value1, value2, value3, ...), (value1, value2, value3, ...);
```

**Example:**
```sql
INSERT INTO pystudent VALUES (104, 'Harshii', 20, 'Dewas'), (105, 'Bhumii', 30, 'Indore');
```

### Case 4: Insert Values into Specific Columns (SET syntax)
MySQL also supports the `SET` syntax.

**Example:**
```sql
INSERT INTO pystudent SET id=106, name='Kuldeep', age=27, city='Dewas';
```
- `INSERT ... SET` can insert one row at a time.
- It is **not** part of the SQL standard (databases like Oracle, PostgreSQL do not support this syntax).

### Case 5: Insert data from another table
We can copy records from one table to another table.

**Examples:**
```sql
INSERT INTO pybackup SELECT * FROM pystudent;
```

```sql
INSERT INTO pybackup(id, name) SELECT id, name FROM pystudent;
```

### Rules to Insert:
- Values must match the column order. The wrong order can lead to errors.
- The number of values must match the number of columns.

---

## PRIMARY KEY

A **Primary Key** is a column or group of columns whose values uniquely identify each row in a table. It does not allow duplicate values or null values.

**Without a primary key:**
- Duplicate records can exist, making it difficult to identify a particular row.
- Relationships between tables cannot be stabilized properly.
- Data integrity is reduced.
- Searching for records becomes less reliable.

### Characteristics:
- Unique values.
- Cannot contain NULL.
- Only one primary key per table is allowed. However, that primary key can consist of multiple columns (this is called a **Composite Key**).
- It automatically creates an Index. When a primary key is created, MySQL automatically creates a unique `INDEX` on that column.
- Values of the primary key should be stable.

### Creating a Primary Key:

**Way 1:**
```sql
CREATE TABLE pyemployee(empid INT PRIMARY KEY, name VARCHAR(20), salary DECIMAL(10,2));
```

**Way 2:**
```sql
CREATE TABLE pyemployee1(empid INT, name VARCHAR(20), salary DECIMAL(10,2), CONSTRAINT pk_employee PRIMARY KEY(empid));
```

**Way 3:**
```sql
CREATE TABLE pyemployee3(empid INT, name VARCHAR(20), salary DECIMAL(10,2));
ALTER TABLE pyemployee3 ADD PRIMARY KEY(empid);
```
