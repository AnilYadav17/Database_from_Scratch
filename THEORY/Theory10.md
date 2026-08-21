# Query Filtering and Sorting

## IS NULL and IS NOT NULL

When querying data, evaluating nulls requires special syntax.

```sql
select * from employeebatch;
```

Incorrect way to check for null:
```sql
select * from employeebatch where city = null;
```

### Note on NULL
**NULL** means there is no value known or the value has not been provided. It is **not** the same as the following:
- `0`
- `''` (empty string)
- `'Null'` (string containing the word Null)
- `false`

`IS NULL` is used to find rows where a column contains a null value.

```sql
select * from employeebatch where city is null;
```

```sql
select * from employeebatch where city is not null;
```

### IS NULL with AND
```sql
select * from employee where city is null and salary > 35000;
```

---

## Operator Precedence with AND, OR, and NOT

When using multiple conditions inside a `WHERE` clause, MySQL has to decide which conditions to evaluate first.

```sql
select * from employeebatch where city = "Indore" or city = "Bhopal" and salary > 50000;
```

In MySQL, the precedence is:
1. `NOT`
2. `AND`
3. `OR`

When we write:
```sql
where a or b and c;
```
It becomes:
```sql
where a or (b and c);
```

So our query becomes:
```sql
select * from employeebatch where city = "Indore" or (city = "Bhopal" and salary > 50000);
```

### Practice Queries

**1. Write a query to fetch employees who are from Indore or Bhopal, and their salary must be greater than 40000:**
```sql
select * from employeebatch where (city = "Indore" or city = "Bhopal") and salary > 40000;
```

**2. Write a query whose city is not Indore:**
```sql
select * from employeebatch where not city = "Indore";
```
Equivalent to:
```sql
select * from employeebatch where city <> "Indore";
```

**3. Write a query to give me employees who are neither from Indore nor Bhopal:**
```sql
select * from employeebatch where not (city = "Indore" or city = "Bhopal");
```

### NOT with AND

**4. Write a query to give me employees who are not from Indore, Bhopal and earning more than 50000:**
```sql
select * from employeebatch where not (city = "Indore" or city = "Bhopal") and salary > 50000;
```

### Complex Precedence Examples

Consider this query:
```sql
select * from employeebatch where city = "Indore" or city = "Bhopal" and salary > 40000 and age > 35;
```

This query is implicitly converted into:
```sql
select * from employeebatch where city = "Indore" or (city = "Bhopal" and salary > 40000 and age > 35);
```

**5. Write a query to give me employees who are from Indore or Bhopal, earning more than 40000, and age greater than 25:**
```sql
select * from employeebatch where (city = "Indore" or city = "Bhopal") and (salary > 40000 and age > 25);
```

Therefore:
```sql
where not a or b and c
```
Becomes:
```sql
where (not a) or (b and c)
```

---

## ORDER BY

`ORDER BY` is used to sort the rows returned by a `SELECT` query.
This does not change the actual data stored in the table; it only changes the order in which the result is displayed.

```sql
select name from employeebatch order by salary asc;
```

```sql
select name from employeebatch order by salary desc;
```

```sql
select * from employeebatch order by name;
```

```sql
select * from employeebatch order by city;
```

**Note:** When sorting in ascending (`ASC`) order, `NULL` values will appear first.

### Practice Queries

**1. Write a query to select all the IT employees, ordering them by high salary to low salary:**
```sql
select * from employees where department = "IT" order by salary desc;
```
*In the above query, the `WHERE` clause decides which rows we want, and `ORDER BY` decides in which order we want those rows displayed.*

### ORDER BY with Multiple Columns

You can sort by multiple columns. The results will be sorted by the first column, and then by the second column if there are ties in the first.

```sql
select * from employeebatch order by city, salary desc;
```

```sql
select * from employeebatch order by city desc, salary desc;
```
