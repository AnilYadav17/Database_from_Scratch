### auto_increment gap :
There are several reasons why gaps can occur.
i) If we perform DELETE operation.
=========== Table STUDENT =============
1. Anil
2. Bhumi
3. Harsh

-> DELETE 2..
1. Anil
3. Harsh

-> Next INSERT Abhi
1. Anil
3. Harsh
4. Abhi
The deleted value can not be reused automatically.


### insert ignore :-
It is a variation of the insert statement in MySQL that attempts to insert new records into a table.
If an inserted row violates certain CONSTRAINTS then MySQL ignores that row instead of generating an error and continue processing the remaining rows.
In many real world situations such as importing large datasets, csv files Duplicates may already exist in the database.

### insert on duplicate key update :-
It is a MySQL SPECIFIC EXTENSION of the INSETRT statement that allow you to insert a new record into a table.
If the inserted row vialotes PRIMARY KEY OR UNIQUE KEY constarints then MySQL updates the existing record instead of generating an error.

```sql 
insert into student values (101,"Abhi",20) on duplicate key update name="Harsh" ,age=22;
```

### SHOW CREATE TABLE :-
It is a MySQL command used to display the exact SQL statement that was used to create an existing table, It shows the complete structure.

```sql 
 show  create table student;
```
