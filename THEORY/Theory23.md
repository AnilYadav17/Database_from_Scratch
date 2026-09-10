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

