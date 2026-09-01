# Types of SQL Commands

## 1. DDL (Data Definition Language)

- It is used to create, define, and delete the structure of a database.
- Deals with the structure of the objects.
- Interacts with the database directly; enforces an implicit commit before and after the statement.
- We cannot undo (rollback) the changes.
- Auto-commit occurs before and after a DDL Command.
- Faster than other commands.

**Examples:** `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`.

## 2. DML (Data Manipulation Language)

- Deals with the data only.
- These commands interact with the buffer first, then with the database.
- We can undo or rollback the changes.
- Slower compared to DDL commands.
- Used to manipulate the data stored inside database tables.
- Does not create or modify the table structure.

**Examples:** `INSERT`, `UPDATE`, `DELETE`, etc.

## 3. DQL (Data Query Language)

- A subset of SQL used to retrieve (fetch) data from one or more database tables.
- Allows users to view, search, and filter data.

**Example:** `SELECT`.

## 4. TCL (Transaction Control Language)

- A category of SQL used to manage transactions in a database.
- A **TRANSACTION** is a sequence of one or more SQL statements treated as a single unit of work.
- A set of DML operations combined with a commit or rollback is called a TRANSACTION.
- Every transaction starts with DML operations, and a commit or rollback is the ending point for these transactions. This commit may be implicit or explicit.

**Examples:** `BEGIN`, `COMMIT`, `ROLLBACK`, `SAVEPOINT`, `SET TRANSACTION`.

## 5. DCL (Data Control Language)

- A subset of SQL used to control access to the database.

**Examples:** `GRANT`, `REVOKE`.