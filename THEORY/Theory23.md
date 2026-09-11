## MANY TO MANY RELATIONSHIP

```sql
CREATE DATABASE college191;

USE college191;

DROP TABLE IF EXISTS student_course191;
DROP TABLE IF EXISTS student191;
DROP TABLE IF EXISTS course191;

CREATE TABLE student191 (
    stuid INT PRIMARY KEY,
    stuname VARCHAR(20)
);

CREATE TABLE course191 (
    cid INT PRIMARY KEY,
    cname VARCHAR(30)
);

INSERT INTO student191 VALUES
(101, 'Anil'),
(102, 'Abhi'),
(103, 'Purab');

INSERT INTO course191 VALUES
(1, 'Python'),
(2, 'MySQL'),
(3, 'Django');

CREATE TABLE student_course191 (
    stuid INT,
    cid INT,
    PRIMARY KEY (stuid, cid),
    FOREIGN KEY (stuid)
        REFERENCES student191(stuid),
    FOREIGN KEY (cid)
        REFERENCES course191(cid)
);

INSERT INTO student_course191 VALUES
(101, 1),
(101, 2),
(102, 1),
(102, 3),
(103, 2),
(103, 3);

SELECT * FROM student191;
SELECT * FROM course191;
SELECT * FROM student_course191;
```

# SELF-REFERENCING FOREIGN KEY

A **self-referencing foreign key** is a foreign key where a column in a table refers to the **primary key or a unique key of the same table**.

In simple words, **a table creates a relationship with itself**.

## Example: Employee and Manager

An employee can have another employee as their manager.

* `empid` → identifies the employee.
* `empname` → stores the employee's name.
* `managerid` → stores the `empid` of the employee's manager.

```sql
CREATE TABLE selfemployee(
    empid INT PRIMARY KEY,
    empname VARCHAR(20) NOT NULL,
    managerid INT,
    FOREIGN KEY (managerid) REFERENCES selfemployee(empid)
);
```

Here:

```text
managerid → references → empid
                ↑
          Same table
```

## Insert the Top-Level Employee

First, insert an employee who does not have a manager:

```sql
INSERT INTO selfemployee
VALUES (101, 'Anil', NULL);
```

Output:

```text
+-------+---------+-----------+
| empid | empname | managerid |
+-------+---------+-----------+
|   101 | Anil    |      NULL |
+-------+---------+-----------+
```

`NULL` means Anil does not have a manager in this table.

## Insert an Employee Under Anil

Now insert another employee whose manager is Anil:

```sql
INSERT INTO selfemployee
VALUES (102, 'Rahul', 101);
```

Output:

```text
+-------+---------+-----------+
| empid | empname | managerid |
+-------+---------+-----------+
|   101 | Anil    |      NULL |
|   102 | Rahul   |       101 |
+-------+---------+-----------+
```

The relationship is:

```text
        Anil
      empid = 101
          ↑
          |
    managerid = 101
          |
        Rahul
      empid = 102
```

Therefore:

**Rahul's manager is Anil.**

## Foreign Key Rule

If we try:

```sql
INSERT INTO selfemployee
VALUES (103, 'Amit', 108);
```

MySQL will reject it if `empid = 108` does not exist.

Why?

Because:

```text
managerid = 108
       ↓
empid = 108 must exist
```

Since there is no employee with `empid = 108`, the foreign key constraint fails.

```text
ERROR 1452
Cannot add or update a child row:
a foreign key constraint fails
```

### Important Rule

> A foreign-key value must match an existing referenced key, unless the foreign-key column allows `NULL`.

## Why Your Query Failed

You executed:

```sql
INSERT INTO selfemployee
VALUES (102, 'Anil', 108);
```

Here:

```text
empid     = 102
empname   = Anil
managerid = 108
```

MySQL interpreted this as:

> Employee 102 has employee 108 as their manager.

But employee `108` does not exist.

Therefore, MySQL rejected the insertion.

## Duplicate Primary Key

You also tried:

```sql
INSERT INTO selfemployee
VALUES (101, 'Anil', 108);
```

This failed because `101` already exists.

```text
ERROR 1062
Duplicate entry '101' for key 'PRIMARY'
```

A primary key must be **unique**.

Therefore:

```text
empid = 101
```

cannot be inserted again.

## Common Uses

Self-referencing foreign keys are commonly used for hierarchical data:

* Employee → Manager
* Category → Parent Category
* Folder → Parent Folder
* Comment → Parent Comment
* Employee → Department Head

Example:

```text
Company
│
├── Anil (101)
│   ├── Rahul (102)
│   └── Amit (103)
│
└── Priya (104)
    └── Neha (105)
```

The database can represent this hierarchy using:

```text
empid
  ↓
managerid
  ↓
same table
```

## Key Point for Interview

**Self-referencing foreign key = a foreign key that references a primary key or unique key in the same table.**

It is also called a **recursive relationship** or **recursive foreign-key relationship**.

```text
┌──────────────────────────────┐
│       selfemployee           │
│                              │
│ empid       ←───┐            │
│ empname         │            │
│ managerid ──────┘            │
│                              │
└──────────────────────────────┘
```
and,
```sql
insert into selfemployee values(103,'Abhi',103);
```
