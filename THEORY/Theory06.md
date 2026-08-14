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

#### SYNTAX
```sql
ALTER TABLE talbe_name alteroperation;
```