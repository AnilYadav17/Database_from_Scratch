### 1. DDL (Data Definition Language) 
-> Its is used to create, define, delete the structure of database structure.
-> They deals with structure of the objects.
-> They interact with database directly , they enforce an implicit commit before and after the statement.
-> In it we can not undo(rollback) the changes.
->  Auto commit before and after after DDL Command.
-> They are faster than other commands. 
Example : CREATE, ALTER, DROP, TRUNCATE, RENAME.
	

### 2. DML - DATA  MANIPULATION LANGUAGE
-> Deals with the data only.
-> These commands interect with buffer first then with the database.
-> We can undo or rollback the changes.
-> They are slow as compare to DDL commands.
-> They are used to manipulate the data stored inside the database tables.
-> It does not create or modify the table structure.
EXAMPLES :- INSERT, UPDATE ,DELETE etc.

### 3. DQL - DATA QUERY LANGUAGE
-> It is a subset of SQL that is used to retrieve(fetch) data from one or more database tables.
-> It allow users to view , search , filter Data.
EXAMPLE :- SELECT 

### 4. TCL - TRANSACTION CONTROL LANGUAGE
-> It is a category of SQL and used to manage transactios in a database.
-> A TRANSACTION is sequence of one or more SQL statements that are treated as a single unit of work.
-> A set of DML OPERATIONS with commit or rollback is called TRANSACTION.
-> Every TRANSACTION will start with DML operations and commit or rollback is a ending point to these transactions.
   This commit maybe implicit or explicit. 
EXAMPLE:- BEGIN ,COMMIT ,ROLLBACK ,SAVEPOINT ,SETTRANSACTION 

### 5. DCL - DATA CONTROL LANGUAGE
-> It is a subset of SQL which is used to control access to database.