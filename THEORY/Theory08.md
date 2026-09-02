# Date and Time Data Types in MySQL

MySQL provides comprehensive support for temporal data through several Date and Time data types:

1. **`DATE`**: Stores date only (`YYYY-MM-DD`). Example: `2026-08-13`
2. **`TIME`**: Stores time only (`HH:MM:SS`). Example: `14:30:45`
3. **`DATETIME`**: Stores both date and time (`YYYY-MM-DD HH:MM:SS`). Example: `2026-08-13 14:30:45`
4. **`TIMESTAMP`**: Stores date and time with automatic timezone handling and timestamps.
5. **`YEAR`**: Stores 4-digit year value. Example: `2026`

---

## 1. DATE

- Stores date without time components.
- Standard format: `YYYY-MM-DD`.
- Ideal for values like date of birth, joining date, invoice date, and event dates.

```sql
CREATE TABLE employeedt (
    id INT, 
    name VARCHAR(20), 
    birthdate DATE
);
```

---

## 2. TIME

- Stores time of day or elapsed time intervals.
- Standard format: `HH:MM:SS`.

```sql
CREATE TABLE classschedule (
    classid INT, 
    classname VARCHAR(30), 
    starttime TIME
);
```

---

## 3. DATETIME

- Stores both date and time components.
- Standard format: `YYYY-MM-DD HH:MM:SS`.
- Value range: `'1000-01-01 00:00:00'` to `'9999-12-31 23:59:59'`.

```sql
CREATE TABLE appointment (
    apid INT, 
    cusname VARCHAR(20), 
    aptime DATETIME
);
```

---

## 4. TIMESTAMP

- Stores date and time values converted to UTC for storage and converted back to the current session time zone on retrieval.
- Value range: `'1970-01-01 00:00:01'` UTC to `'2038-01-19 03:14:07'` UTC.
- Supports automatic record initialization (`DEFAULT CURRENT_TIMESTAMP`) and automatic modification tracking (`ON UPDATE CURRENT_TIMESTAMP`).

```sql
CREATE TABLE employeedt1 (
    id INT, 
    name VARCHAR(20), 
    createdate TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### DATETIME vs. TIMESTAMP Comparison

| Feature | DATETIME | TIMESTAMP |
| :--- | :--- | :--- |
| **Storage Range** | `1000-01-01` to `9999-12-31` | `1970-01-01` to `2038-01-19` (UTC) |
| **Storage Size** | 5 bytes (+ fractional seconds) | 4 bytes (+ fractional seconds) |
| **Timezone Support** | Stores exact constant value | Converts between session timezone and UTC |
| **Auto-update** | Supported in modern MySQL | Supported (widely used for audits) |

```sql
CREATE TABLE employeedt3 (
    id INT, 
    name VARCHAR(20), 
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

---

## 5. YEAR

- Stores a 4-digit year.
- Valid range: `1901` to `2155` (and `0000`).

```sql
CREATE TABLE vehicle1 (
    vid INT, 
    model VARCHAR(20), 
    mfg_year YEAR
);
```

---

## 6. BOOLEAN in MySQL

- In MySQL, `BOOLEAN` and `BOOL` are synonyms for `TINYINT(1)`.
- `TRUE` is stored and returned as `1`, `FALSE` is stored and returned as `0`.

```sql
CREATE TABLE employeedt4 (
    id INT, 
    name VARCHAR(20), 
    is_active BOOLEAN
);
```
