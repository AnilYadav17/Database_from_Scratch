### DROP
It is DDL comma
When we use drop the object itself deleted along with the data stored insode it.

```sql
DROP copy2;
```
After DROP command the table will no longer exist.


#### DROP MULTIPLE TABLES
```sql
drop table pyemployee1,pyemployee3,pyemployee5;
```
```sql
drop table if exists yemployee1,pyemployee3,pyemployee5;
```

#### DROP vs TRUNCATE
TRUNCATE is used to remove all rows from the table while keeping the table.<br>
-> Data is removed but Structure retaint.<br>
-> It Resets the auto_increment counter.<br>
-> Does not support WHERE because it removes the all rows.<br>
-> Its a DDL command so can not be Rolled Back.<br>

DROP is used to remove the entire table.<br>
-> Data and structure both removed.<br>
-> The Table itself is removed including its auto_increament.<br>
-> Also does not support WHERE because it remove the entire table.<br>
->  Its a DDL command so can not be Rolled Back.<br>

### ALTER 
Its a DDL command used to modify the structure of an existing DataBase object.<br>
It allow us to change an existing table without droping and recreating the entire table.<br>
We can use ALTER command <br>
   Add a new column <br>
   Drop a column. <br>
   Modify a columns datatype. <br>
   Change a column definetion. <br>
   Rename a column. <br>
   Rename a table. <br>
   Add a Constraints.<br>
   Drop Constraints. <br>
   Add and DROP Primary key <br>
   Add and DROP Foreign key <br>
ALTER TABLE is one of the mechanism used to evolve the database schema. <br>

#### SYNTAX:
```sql
>syntax
ALTER TABLE talbe_name alteroperation;
```
<br>

#### ADD  COLUMN:
```sql
ALTER TABLE talbe_name ADD COLUMN column_name datatype;
```

```sql
ALTER TABLE azadi ADD COLUMN email varchar(20);
```
Existing rows will have null value in the newly added **column** when no applicable default is suplied.


#### ADD  MULTIPLE COLUMNS:
```sql
ALTER TABLE azadi ADD COLUMN mobile varchar(20), ADD COLUMN course varchar(30), ADD COLUMN salary decimal(10,2);
```

#### ADD  COLUMN AT SPECIFIC POSITION:
By default a new column is added at the end , but MySQL allow positioning.
```sql
 ALTER TABLE azadi ADD COLUMN gender varchar(10) first;
```
```sql
ALTER TABLE azadi ADD COLUMN dob date after name;
```
Column order has no bussiness significance 

<br>

#### DROP COLUMN
Its is used to permanently remove a column from the talbe
```sql
ALTER TABLE azadi drop column dob;
```

#### DROP MULTIPLE COLUMN
```sql
ALTER TABLE azadi drop column mobile,drop column course;
```
<br>

### MODIFY COLUMN
It is used to change the definition of an existing column.
```sql
>syntax
alter table table_name modify column column_name newdefinition;
```
```sql
alter table azadi modify column age smallint;
alter table azadi modify column name varchar(30);
```
