# Data Types in MySQL

A data type defines what kind of value a column can store:
- How much storage is required.
- What kind of values are allowed.
- What operations can be performed on the data.

## Major Categories of Data Types

1. **Numeric Data Types**
2. **String Data Types**
3. **Date and Time Data Types**
4. **JSON / Spatial Data Types**

---

## 1. Numeric Data Types

Numeric data types are used to store numeric values such as integers and decimal numbers. They allow the database to perform arithmetic and mathematical operations.

**Examples:** `TINYINT`, `SMALLINT`, `MEDIUMINT`, `INT`, `BIGINT`, `DECIMAL`, `FLOAT`, `DOUBLE`.

![Numeric Data Types](images/image.png)

### Integer Types and Modifiers

- **SIGNED (Default):** Can store both positive and negative values.
- **UNSIGNED:** Disallows negative values, effectively doubling the positive range.

```sql
CREATE TABLE demo1 (
    id TINYINT UNSIGNED
);

DESC demo1;
```

### Exact vs. Approximate Numeric Types

#### DECIMAL
Used for exact decimal values (financial transactions, currency, precision calculations):
- `DECIMAL(M, D)`
  - `M` = Total number of digits (precision)
  - `D` = Number of digits after the decimal point (scale)

```sql
salary DECIMAL(10, 2)
```

#### FLOAT & DOUBLE
Used for approximate decimal values (scientific calculations, continuous measurements):
- `FLOAT` — Single precision (lower precision)
- `DOUBLE` — Double precision (higher precision)
- `DECIMAL` — Exact precision

---

## 2. String Data Types

String data types are used to store text, characters, and predefined values.

### a. CHAR
- **Fixed-length** character string.
- Padded with spaces up to the defined length if input is shorter.

```sql
country_code CHAR(2)  -- 'IN', 'US', 'UK'
```

### b. VARCHAR
- **Variable-length** character string.
- Stores only the actual characters plus length bytes.
- The most commonly used string type in application development.

```sql
name VARCHAR(100)
```

### c. TEXT
- Used for larger text content where `VARCHAR` limit is insufficient.
- Available variants: `TINYTEXT` (255 bytes), `TEXT` (65,535 bytes), `MEDIUMTEXT` (16MB), `LONGTEXT` (4GB).

```sql
CREATE TABLE demo2 (
    id INT, 
    description TEXT
);

DESC demo2;
```

### d. ENUM
- A string object whose value is chosen from a **single value** out of a predefined list of permitted values.

```sql
CREATE TABLE demo3 (
    id INT, 
    status ENUM('active', 'inactive', 'onleave')
);

INSERT INTO demo3 VALUES (101, 'active');
INSERT INTO demo3 VALUES (102, 'onleave');
SELECT * FROM demo3;

-- The following will cause an error because 'yes' is not in the ENUM list:
-- INSERT INTO demo3 VALUES (103, 'yes');
```

### e. SET
- A string object that can have **zero or more values** chosen from a predefined list of permitted values.

```sql
CREATE TABLE demo4 (
    id INT, 
    name VARCHAR(100), 
    status ENUM('leave', 'active'), 
    skills SET('java', 'python', 'SQL', 'react')
);

INSERT INTO demo4 VALUES 
    (101, 'kuldeep', 'active', 'python'), 
    (102, 'dhruv', 'leave', 'java,python,SQL');
```

> **Note:** While `SET` allows multiple values in a single column, relational design often prefers separate junction/mapping tables for many-to-many relationships.
