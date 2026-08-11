# CREATE TABLE AS SELECT (CTAS)

### 1. Definition
**CREATE TABLE AS SELECT (CTAS)** is used to create a **new table** by copying data from an existing table or from the result of a `SELECT` query.
It automatically creates the new table based on the columns returned by the `SELECT` statement.
CTAS copies:
* Selected column names
* Column data types
* Column order
* Selected data

### 2. Limitations of CTAS
CTAS does not copy the complete table structure, rules, or database objects** from the original table.
The following things are **not copied**:
* Primary Key
* Foreign Key
* Auto Increment property
* Constraints
* Indexes
* Triggers
* Other database objects

----------------------------------------------------------------------------------- x --------------------------------------------------------------------------------
# INSERT COMMAND
`INSERT` is a DML (Data Manipulation Language) command.
It is used to **add new records (rows) into a table.

## Case 1: Insert Values into All Columns
When inserting values into **all columns**, the values must be given in the **same order as the columns in the table**.

### Syntax:
```sql
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```
### Example:
```sql
INSERT INTO pystudent
VALUES (1, 'Anil', 85, 'Dewas');
```
------------------------------------------------
## Case 2: Insert Values into Specific Columns :
When we don't want to insert data into every column or we are providing all the values but order not follows , then we need to provide column list.

### Syntax:
```sql
INSERT INTO table_name(column1, column2,column3)
VALUES (value1, value2, value3);
```
### Example1:
```sql
INSERT INTO pystudent(id,name,city) VALUES(102,'Abhi','Indore');
```
### Example2:
```sql
INSERT INTO pystudent(id,name) VALUES(103,'Harsh');
```
### Best Practice:
Always specify the column names while inserting the data, this makes the query easier to read.

------------------------------------------------
## Case 3: Insert Values into Multiple Columns :
Instead of writing multiple insert statements we can insert many rows in one statement 

### Syntax:
```sql
INSERT INTO table_name VALUES (value1, value2, value3, ......),(value1, value2, value3, ......);
```
### Example:
```sql
INSERT INTO pystudent VALUES(104,'Harshii',20,'Dewas'),(105,'Bhumii',30,'Indore');
```

----------------------------------------------
## Case 4: Insert Values into Specific Columns:
MySQL also support the set syntax

### Example:
```sql
INSERT INTO pystudent set id=106,name='Kuldeep',age=27,city='dewas';
```
i) INSERT...set  can insert one row at a time
ii) Not the part of SQL Stanadard , it means databases like ORACLE , POSTGREYSQL do not support this syntax.



---------------------------------------------
## Case 5: Insert data from another table:
We can copy records from one table to another table.

```sql
INSERT INTO pybackup select * from pystudent;
```
```sql
INSERT INTO pybackup(id,name) select id,name from pystudent;
```
---------------------------------------------


####RULES TO INSERT:
->  Values must match with column order, Wrong order can lead to errors.
->  Number of values must match with number of columns.


--------------------------------------------------------------------------------- x ----------------------------------------------------------------------------
### PRIMARY KEY:
It is column or group of columns whose values uniquely identify each row in a table.
It does not allow duplicate values or null values.
Without a primary key:
                     Duplicate records can exist , it become difficult to identify a particular row
                     Relationships between tables can not be stablised properly.
                     Data integrity will be reduced.
                     Searhching records become less reliable.
CHARACTERISTICS:
-> Unique values.
-> Can not contain null.
-> Only one primary key per table is allowed , however that primary can consists multiple column(its called COMPOSITE KEY).
-> It automatically creates an Index , when a primary key is created MySQL automatically creates a unique INDEX on that column.
-> Values of primary key should be stable.

##CREATE PRIMARY KEY:
WAY 1:
      create table pyemployee(empid int primary key, name varchar(20),salary decimal(10,2));

WAY 2:
    create table pyemployee1(empid int , name varchar(20),salary decimal(10,2),constraint pk_employee primary key(empid));
    
WAY 3:
     create table pyemployee3(empid int , name varchar(20),salary decimal(10,2));
     alter table pyemployee3 add primary key(empid);


    
