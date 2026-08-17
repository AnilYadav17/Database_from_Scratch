# Data Types in MYSQL

- A data type defines what kind of value a column can store.
- How much storage is required.
- What kind of values are allowed.
- What operations can be performed.

## Types:

1. Numeric
2. String
3. Date and Time
4. JSON

---

## 1. Numeric:

- Numeric data types are used to store numeric values such as integers and decimal numbers.
- They allow database to perform mathematical operations.

Example: int, tinyint, smallint, bigint, decimal, float, double.

![image](images/image.png)

**NOTE:**
- BY DEFAULT, INTEGER TYPES ARE SIGNED SO THEY CAN STORE POSITIVE AND NEGATIVE VALUES.
- UNSIGNED DOES NOT ALLOW NEGATIVE VALUES AND INCREASE THE POSITIVE RANGE.

```sql
create table demo1(id tinyint unsigned);
desc demo1;
```

### Decimal-

- It is used for exact decimal values.

```sql
decimal(m,d)
m= total digits
d= digits after decimal

salary decimal(10,2)
```

### Float & Double -

- It is used for approximate decimal values.

```sql
float ----- Lower precision
double ---- higher decimal
decimal --- exact precision
```

---

## 2. String:

- It is used for text.

Example: char, varchar

### a. Char-

- Fixed length string

```sql
countrycode char(2)
IN
US
UK
```

### b. Varchar-

- Variable length string
- It is most commonly used string type in application development.

```sql
name varchar(100)
```

### c. Text-

- It is used for larger text.

Example: `tinytext` —— 255 bytes, `text` ——— 65535 bytes, `mediumtext`, `longtext`.

```sql
create table demo2(id int, description text);
desc demo2;
```

### d. enum-

- It allows one value from a predefined list.

```sql
status enum('active' , 'onleave' , 'inactive')
```
```sql
create table demo3(id int, status enum('active' , 'inactive' , 'onleave'));

insert into demo3 values(101,'active');
insert into demo3 values(102,'onleave');
select * from demo3;
insert into demo3 values(103,'yes'); -- This will cause an error as 'yes' is not in the enum list
```

### e. set-

- It allows multiple values from a predefined list.

```sql
skills set('java','python','SQL','react')
```

- Here, multiple values can be selected.
- Set is less commonly used in modern application database design.
- For complex relationships, a separate mapping table is created.

```sql
create table demo4(id int, name varchar(100), status enum('leave','active'), skills set('java','python','SQL','react'));
```

```sql
insert into demo4 values (101,'kuldeep','active','python'), (102,'dhruv','leave','java,python,SQL');
```
