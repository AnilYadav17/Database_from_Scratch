# FOREIGN KEY (Referential Integrity Constraint)

A **Foreign Key** is a column (or combination of columns) in one table that references a candidate key—normally the **Primary Key** or a **Unique Key**—in another table.

Its main purpose is to maintain **Referential Integrity** between related tables, ensuring that data relationships remain valid and preventing orphaned records.

---

## Key Characteristics of Foreign Keys
1. **Referential Integrity:** Prevents inserting values into the child table that do not exist in the parent table.
2. **Matching Data Types:** The referencing column (foreign key) and referenced column (primary key) must have identical or compatible data types.
3. **Multiple Foreign Keys:** A table can have multiple foreign keys pointing to the same or different tables.
4. **NULL Values:** Foreign key columns can accept `NULL` values unless constrained by `NOT NULL`.
5. **Parent vs Child Table:**
   - **PARENT TABLE (Referenced Table):** The table that holds the original (primary/unique key) record.
   - **CHILD TABLE (Referencing Table / Owner):** The table containing the foreign key that points to the parent table.

---

## 1. Syntax of Foreign Key

### At Table Creation (Inline / Constraint Definition)
```sql
CREATE TABLE child_table (
    column1 INT PRIMARY KEY,
    column2 VARCHAR(50),
    parent_id INT,
    CONSTRAINT fk_custom_name FOREIGN KEY (parent_id) 
        REFERENCES parent_table(parent_column)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);
```

### Adding Foreign Key to an Existing Table
```sql
ALTER TABLE child_table 
ADD CONSTRAINT fk_custom_name 
FOREIGN KEY (parent_id) REFERENCES parent_table(parent_column);
```

### Dropping a Foreign Key
```sql
ALTER TABLE child_table 
DROP FOREIGN KEY fk_custom_name;
```

---

## 2. Example 1: Department and Employee

### Parent Table: `departments`
| did | dname |
|:---:|:---:|
| 1 | IT |
| 2 | HR |
| 3 | Finance |

```sql
CREATE TABLE departments (
    did INT PRIMARY KEY,
    dname VARCHAR(30) NOT NULL
);

INSERT INTO departments VALUES (1, 'IT'), (2, 'HR'), (3, 'Finance');
```

### Child Table: `employees`
| empid | empname | deptid |
|:---:|:---:|:---:|
| 101 | Anil | 1 |
| 102 | Harsh | 2 |

```sql
CREATE TABLE employees (
    empid INT PRIMARY KEY,
    empname VARCHAR(50) NOT NULL,
    deptid INT,
    CONSTRAINT fk_emp_dept FOREIGN KEY (deptid) REFERENCES departments(did)
);

-- Valid Inserts
INSERT INTO employees VALUES (101, 'Anil', 1);
INSERT INTO employees VALUES (102, 'Harsh', 2);
```

### ❌ Referential Integrity Violation (Insert Failure)
If we attempt to insert an employee belonging to department `10`:
```sql
INSERT INTO employees VALUES (104, 'Abhi', 10);
```
**Output Error:**
```
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`test_db`.`employees`, CONSTRAINT `fk_emp_dept` FOREIGN KEY (`deptid`) REFERENCES `departments` (`did`))
```
*Reason:* Department `10` does not exist in the parent `departments` table.

### ❌ Referential Integrity Violation (Delete Failure)
If we attempt to delete department `1` from `departments`:
```sql
DELETE FROM departments WHERE did = 1;
```
**Output Error:**
```
ERROR 1451 (23000): Cannot delete or update a parent row: a foreign key constraint fails (`test_db`.`employees`, CONSTRAINT `fk_emp_dept` FOREIGN KEY (`deptid`) REFERENCES `departments` (`did`))
```
*Reason:* Employee `101 (Anil)` references department `1`. Deleting the parent row would orphan the employee.

---

## 3. Example 2: Customer and Orders (Cascading Operations)

When data in the parent table changes, we can configure automatic cascading behavior on the child table using:
- **`ON DELETE CASCADE`**: Automatically deletes matching child rows when a parent row is deleted.
- **`ON UPDATE CASCADE`**: Automatically updates matching child foreign keys when a parent primary key is updated.
- **`ON DELETE SET NULL`**: Sets the foreign key to `NULL` in the child rows when the parent row is deleted.
- **`ON DELETE RESTRICT` / `NO ACTION`** *(Default)*: Rejects delete or update operations on parent if matching child rows exist.

### Parent Table: `customers`
| cid | cname | email |
|:---:|:---:|:---:|
| 101 | Anil | anil@example.com |
| 102 | Dipu | dipu@example.com |
| 103 | Rashmika | rashmika@example.com |

```sql
CREATE TABLE customers (
    cid INT PRIMARY KEY,
    cname VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE
);

INSERT INTO customers VALUES 
(101, 'Anil', 'anil@example.com'),
(102, 'Dipu', 'dipu@example.com'),
(103, 'Rashmika', 'rashmika@example.com');
```

### Child Table: `orders`
| oid | odate | amount | custid |
|:---:|:---:|:---:|:---:|
| 1 | 2026-09-07 | 499.00 | 101 |
| 2 | 2026-09-08 | 499.00 | 101 |
| 3 | 2026-09-09 | 999.00 | 103 |

*Here: `oid` is Primary Key and `custid` is Foreign Key.*

```sql
CREATE TABLE orders (
    oid INT PRIMARY KEY,
    odate DATE NOT NULL,
    amount DECIMAL(10,2) NOT NULL,
    custid INT,
    CONSTRAINT fk_orders_customer FOREIGN KEY (custid) 
        REFERENCES customers(cid)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

INSERT INTO orders VALUES 
(1, '2026-09-07', 499.00, 101),
(2, '2026-09-08', 499.00, 101),
(3, '2026-09-09', 999.00, 103);
```

### Testing ON DELETE CASCADE:
```sql
DELETE FROM customers WHERE cid = 101;
```
*Result:* Customer `101` is deleted from `customers`, and both orders (`oid 1` and `oid 2`) are automatically deleted from `orders` without error!

---

## 4. Example 3: Multiple Foreign Keys (Doctor, Patient & Appointment)

A single child table can reference multiple parent tables.

### Parent 1: `doctors`
| did | dname | spec | address |
|:---:|:---:|:---:|:---:|
| 101 | Anil | Cardiologist | Mumbai |
| 102 | Priya | Neurologist | Pune |

```sql
CREATE TABLE doctors (
    did INT PRIMARY KEY,
    dname VARCHAR(50) NOT NULL,
    spec VARCHAR(50),
    address VARCHAR(100)
);

INSERT INTO doctors VALUES 
(101, 'Anil', 'Cardiologist', 'Mumbai'),
(102, 'Priya', 'Neurologist', 'Pune');
```

### Parent 2: `patients`
| pid | pname | disease | address |
|:---:|:---:|:---:|:---:|
| 1 | Abhi | Fever | Indore |
| 2 | Sneha | Migraine | Bhopal |

```sql
CREATE TABLE patients (
    pid INT PRIMARY KEY,
    pname VARCHAR(50) NOT NULL,
    disease VARCHAR(50),
    address VARCHAR(100)
);

INSERT INTO patients VALUES 
(1, 'Abhi', 'Fever', 'Indore'),
(2, 'Sneha', 'Migraine', 'Bhopal');
```

### Child Table: `appointments`
| aid | did | pid | date |
|:---:|:---:|:---:|:---:|
| 201 | 101 | 1 | 2026-09-07 |
| 202 | 102 | 2 | 2026-09-08 |

```sql
CREATE TABLE appointments (
    aid INT PRIMARY KEY,
    did INT,
    pid INT,
    app_date DATE NOT NULL,
    CONSTRAINT fk_app_doctor FOREIGN KEY (did) REFERENCES doctors(did),
    CONSTRAINT fk_app_patient FOREIGN KEY (pid) REFERENCES patients(pid)
);

INSERT INTO appointments VALUES (201, 101, 1, '2026-09-07');
INSERT INTO appointments VALUES (202, 102, 2, '2026-09-08');
```

---

## 5. Summary Table: Referential Integrity Rules

| Scenario | Default Behavior (`RESTRICT`) | With `CASCADE` | With `SET NULL` |
|:---|:---|:---|:---|
| **Insert into child with non-existent parent key** | ❌ Rejected (Error 1452) | ❌ Rejected (Error 1452) | ❌ Rejected (Error 1452) |
| **Delete row in parent that child references** | ❌ Rejected (Error 1451) | ✅ Deletes child row | ✅ Sets child foreign key to NULL |
| **Update parent primary key** | ❌ Rejected (Error 1451) | ✅ Updates child foreign key | ✅ Sets child foreign key to NULL |
