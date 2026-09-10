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

### TO DO ....?

1. How to add foreign key constraints if tables are created.

<BR>

## COMBINING ON DELETE and ON UPDATE

```sql
DROP TABLE IF EXISTS employee187;
DROP TABLE IF EXISTS department187;

CREATE TABLE department187 (
    deptid INT PRIMARY KEY,
    deptname VARCHAR(20)
);

INSERT INTO department187 VALUES
(101, 'CSE'),
(102, 'IT'),
(103, 'HR');

CREATE TABLE employee187 (
    empid INT PRIMARY KEY,
    empname VARCHAR(20),
    deptid INT NULL,
    FOREIGN KEY (deptid)
        REFERENCES department187(deptid)
        ON UPDATE CASCADE
        ON DELETE CASCADE
);

INSERT INTO employee187 VALUES
(1, 'Anil', 101),
(2, 'Abhi', 101),
(3, 'Purab', 102),
(4, 'Ravi', 102),
(5, 'Amit', 103);

SELECT * FROM department187;
SELECT * FROM employee187;
```

<BR>

## RELATIONSHIP

In a relational database a relationship descreate tabele department187(deptid int primary key,deptname varchar(20));

CREATE TABLE employee187 (
empid INT PRIMARY KEY,
empname VARCHAR(20),
deptid INT NULL,
FOREIGN KEY (deptid)
REFERENCES department187(deptid)
ON UPDATE SET CASCADE ON DELETE CASCADE
);cribes how rows in one table are connected to rows in another table.

### (i) ONE TO ONE RELATIONSHIP

It means one row in table A is associated with atmost one row in table b and one row in table b is associated with atmost table A.

**_Examples_**<br>
One employee have one employee card.<br>
One person with one passport.<br>
One user with one profile.<br>

```sql
DROP TABLE IF EXISTS empcard;
DROP TABLE IF EXISTS employee189;

CREATE TABLE employee189 (
    epmid INT PRIMARY KEY,
    empname VARCHAR(20)
);

INSERT INTO employee189 VALUES
(101, 'Anil'),
(102, 'Jugal');

CREATE TABLE empcard (
    cardid INT PRIMARY KEY,
    empid INT UNIQUE,
    cardnumber VARCHAR(20),
    FOREIGN KEY (empid)
        REFERENCES employee189(epmid)
);

INSERT INTO empcard VALUES
(1, 101, 'Card111'),
(2, 102, 'Card222');

SELECT * FROM employee189;
SELECT * FROM empcard;

-- Testing ONE-TO-ONE:
-- This will fail because employee 101 already has a card
INSERT INTO empcard VALUES
(3, 101, 'Card333');
```

### (ii) ONE TO MANY RELATIONSHIP

It means one row in table A can be associated with multiple rows in another table but each child rows belongs to one parent.

**_The foriegn is placed on the many side.
One company can have departments.One Employee with many skills_**

### (iii) MANY TO ONE RELATIONSHIP

It is similar to One To Many but viewd from the opposite direction.

### (iv) MANY TO MANY RELATIONSHIP

It means one row in table a can be associated with many rows in table B and One row in table B can also be associated with many rows in table A.

M : N

Suppose we have student table and course table
like <br>
Deepika -> Java <br>
Deepika -> Python <br>
Deepika -> React

Java -> Rashmika
Java -> Anil

**_We can not directly create many to many relationships using 2 tables.Because in that case we have to repeat the student information there we need third table.The additional table is called JUNCTION TABLE.BRIDGE TABLE/MAPPING TABLE/ASSPCIATED TABLE._**

LIKE here we will create student_course
