## ON UPDATE

```sql
CREATE TABLE DEPARTMENT17 (
    deptid INT PRIMARY KEY,
    deptname VARCHAR(30)
);

CREATE TABLE EMPLOYEE17 (
    empid INT PRIMARY KEY,
    empname VARCHAR(30),
    deptid INT,
    FOREIGN KEY (deptid)
        REFERENCES DEPARTMENT17(deptid)
);
Insert Data
INSERT INTO DEPARTMENT17 VALUES
(101, 'CSE'),
(102, 'IT'),
(103, 'HR');

INSERT INTO EMPLOYEE17 VALUES
(1, 'Anil', 101),
(2, 'Abhi', 101),
(3, 'Purab', 102),
(4, 'Ravi', 102),
(5, 'Amit', 103);
```

Now try:

```sql
UPDATE DEPARTMENT17
SET deptid = 105
WHERE deptid = 101;
```

If we change departmentid and if child records are reffering to it then by default it does not allow to update.

<br>

## ON UPDATE CASCADE

If the referenced in the parent table changes automatically update the corresponding foreign key values in the child table.

```sql
DROP TABLE IF EXISTS employee185;
DROP TABLE IF EXISTS department185;

CREATE TABLE department185 (
    deptid INT PRIMARY KEY,
    deptname VARCHAR(20)
);

INSERT INTO department185 VALUES
(101, 'CSE'),
(102, 'IT'),
(103, 'HR');

CREATE TABLE employee185 (
    empid INT PRIMARY KEY,
    empname VARCHAR(20),
    deptid INT,
    FOREIGN KEY (deptid)
        REFERENCES department185(deptid)
        ON UPDATE CASCADE
);

INSERT INTO employee185 VALUES
(1, 'Anil', 101),
(2, 'Abhi', 101),
(3, 'Purab', 102),
(4, 'Ravi', 102),
(5, 'Amit', 103);

SELECT * FROM department185;
SELECT * FROM employee185;

UPDATE department185
SET deptid = 105
WHERE deptid = 101;

SELECT * FROM department185;
SELECT * FROM employee185;
```

<br>

## ON UPDATE SET NULL

when the parent key changes set the corresponding child foreign key values to null.

```sql
DROP TABLE IF EXISTS employee186;
DROP TABLE IF EXISTS department186;

CREATE TABLE department186 (
    deptid INT PRIMARY KEY,
    deptname VARCHAR(20)
);

INSERT INTO department186 VALUES
(101, 'CSE'),
(102, 'IT'),
(103, 'HR');

CREATE TABLE employee186 (
    empid INT PRIMARY KEY,
    empname VARCHAR(20),
    deptid INT NULL,
    FOREIGN KEY (deptid)
        REFERENCES department186(deptid)
        ON UPDATE SET NULL
);

INSERT INTO employee186 VALUES
(1, 'Anil', 101),
(2, 'Abhi', 101),
(3, 'Purab', 102),
(4, 'Ravi', 102),
(5, 'Amit', 103);

SELECT * FROM department186;
SELECT * FROM employee186;

UPDATE department186
SET deptid = 105
WHERE deptid = 101;

SELECT * FROM department186;
SELECT * FROM employee186;
```
