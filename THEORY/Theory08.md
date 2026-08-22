# Date and Time Data Types in MYSQL

MySQL provides the following types of Date and Time data types:

1. **Date**: It will store date only. Example: `2026-08-13`
2. **Time**: It will store time only. Example: `14:30:45`
3. **DateTime**: It will store both date and time. Example: `2026-08-13 14:30:45`
4. **TimeStamp**: It also stores date + time.
5. **Year**: It will store year only.

---

## 1. Date

- Date stores only the date.
- Format: `YYYY-MM-DD`.
- Use date when time is not required, like date of birth, joining date, invoice date, order date, etc.

```sql
CREATE TABLE employeedt(
    id INT, 
    name VARCHAR(20), 
    birthdate DATE
);
```

## 2. Time

- Format: `HH:MM:SS`
- It stores time only. Example: start time `09:30:45`

```sql
CREATE TABLE classschedule(
    classid INT, 
    classname VARCHAR(30), 
    starttime TIME
);
```

## 3. DateTime

- It stores both date and time.
- Format: `YYYY-MM-DD HH:MM:SS`

```sql
CREATE TABLE appointment(
    apid INT, 
    cusname VARCHAR(20), 
    aptime DATETIME
);
```

## 4. TimeStamp

- It also stores date + time.
- One of its major advantages is that it can work with MySQL's automatic current time features.
- `CURRENT_TIMESTAMP` returns current date and time.

```sql
CREATE TABLE employeedt1(
    id INT, 
    name VARCHAR(20), 
    createdate TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Datetime vs TimeStamp

- Both can store date and time.
- DateTime stores date and time values as given. It does not perform automatic time zone conversion.
- TimeStamp converts values between the session time zone.
- `ON UPDATE CURRENT_TIMESTAMP`: This is useful for tracking when a row was last modified.

```sql
CREATE TABLE employeedt3(
    id INT, 
    name VARCHAR(20), 
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

## 5. Year

- It stores only year.

```sql
CREATE TABLE vehicle1(
    vid INT, 
    model VARCHAR(20), 
    mfg_year YEAR
);
```

---

## 6. Boolean in MySQL

- It is used when column should represent a True/False condition.
- In MySQL, `BOOLEAN` and `BOOL` are synonyms for `TINYINT(1)`.
- MySQL does not provide a separate boolean numeric storage type. 
- Here, 1 historically represents display width, not storage size or restriction to values 0 and 1.
- `TRUE` is stored as 1, `FALSE` is stored as 0.

```sql
CREATE TABLE employeedt4(
    id INT, 
    name VARCHAR(20), 
    is_active BOOLEAN
);
```

*(Note: Binary data types will be covered later.)*
