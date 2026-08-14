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
TRUNCATE is used to remove all rows from the table while keeping the table.
-> Data is removed but Structure retaint.
-> It Resets the auto_increment counter.
-> Does not support WHERE because it removes the all rows.
-> Its a DDL command so can not be Rolled Back.

DROP is used to remove the entire table.
-> Data and structure both removed
-> The Table itself is removed including its auto_increament.
-> Also does not support WHERE because it remove the entire table.
->  Its a DDL command so can not be Rolled Back.