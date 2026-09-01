# DBMS vs RDBMS and Introduction to SQL

## Difference Between DBMS and RDBMS

A **DBMS** (Database Management System) is a general software used to manage databases, but an **RDBMS** (Relational Database Management System) is an advanced type of DBMS that stores data in related tables.
- Every RDBMS is a DBMS, but a DBMS is not always an RDBMS.
- In a DBMS, data may be stored in files, but in an RDBMS, data is stored in tables.

## 1. SQL (Structured Query Language)

It is a standard programming language used to communicate with a Relational Database Management System (RDBMS). It allows users to create, store, retrieve, update, delete, and manage data stored in a relational database.

It is a bridge between the user and the database. The user sends SQL commands to the DBMS, and the DBMS processes those commands to perform the requested operations.

- **Standard:** Data is organized.
- **Query:** A request made to the database to perform an operation.
- **Language:** A standard language used to communicate with the RDBMS.
- **Domain Specific Language**

### Features:
1. **Standard Language**
2. **Easy to Learn:** SQL has a simple English-like syntax and supports transactions.
3. **Capabilities:** Provides data definition, manipulation, and retrieval.

## 2. MySQL

It is an Open Source RDBMS that uses SQL (Structured Query Language) to store, manage, retrieve, and manipulate data efficiently. It stores data in the form of tables consisting of rows and columns and establishes relationships between tables using primary keys and foreign keys.

- **My:** Named after My Widenius, daughter of Michael Widenius.
- **SQL:** Stands for Structured Query Language.

### Why MySQL?
1. **Open Source:** MySQL community edition is free to download and use.
2. **Easy to Learn**
3. **High Performance:** It is optimized for fast data retrieval and efficient query execution.
4. **Cross Platform:** It runs on Windows, Linux, Mac, UNIX, etc.
5. **Secure**
6. **Easy to Integrate:** MySQL integrates easily with Java, Python, PHP, etc.
7. **SQL Supports**
8. **Multi-user Access**
9. **Large Community Support**

## Database Objects

Database objects include **Tables**, **Views**, **Databases**, **Indexes**, **Stored Procedures**, **Triggers**, and **Functions**.

## 3. Types of SQL Languages

SQL consists of different categories of commands. Each category is designed to perform a specific type of operation on a database, such as creating database objects, manipulating data, retrieving information, managing user permissions, and controlling transactions.

- **DDL** (Data Definition Language)
- **DML** (Data Manipulation Language)
- **DCL** (Data Control Language)
- **DQL** (Data Query Language)
- **TCL** (Transaction Control Language)

## SQL vs MySQL

- **SQL** is a language; **MySQL** is software.
- SQL cannot store data by itself, but MySQL stores data in databases and tables.
- SQL provides commands such as `INSERT`, `UPDATE`, `DELETE`, `SELECT`.
- MySQL executes SQL commands and returns the result.
- SQL is a standard language supported by many database systems. MySQL is one specific database system that implements SQL.
- SQL does not need installation because it is a language, but MySQL must be installed on a computer or server before use.

## History
- **1995:** MySQL was developed by MySQL AB by Michael Widenius.
- **2008:** Acquired by Sun Microsystems.
- **2010:** Oracle Corporation acquired Sun Microsystems and became the owner of MySQL.

## Connection Details

- **Host Name (`@@hostname`):** The unique name assigned to a computer or server on a network so that it can be identified and accessed.
- **Port (`@@port`):** A system variable that returns the port number on which the MySQL server is listening for incoming client connections.

Whenever any application wants to connect with MySQL, we need connection details:
- **HOST:** `localhost`
- **PORT:** `3306`
- **USERNAME:** `root`
- **PASSWORD:** `1234`
- **DATABASE:** `university`
