# SAVEPOINT

SAVEPOINT is a temporary checkpoint created inside a **Transaction**.

It allows us to **partially undo a Transaction** without undoing the entire Transaction.

```sql
START TRANSACTION;

OPERATION1;

OPERATION2;

SAVEPOINT SP1;

OPERATION3;

OPERATION4;

ROLLBACK TO SAVEPOINT SP1;
```

The above syntax will undo **Operation3** and **Operation4**.

It will keep **Operation1** and **Operation2**.

`ROLLBACK TO SAVEPOINT` keeps the **Transaction ACTIVE**.

It allows us to execute more SQL statements after the rollback.

We can finally use `COMMIT` to permanently save the remaining changes.

**ROLLBACK TO SAVEPOINT does not end the Transaction.**

<br>

---

# RELEASE SAVEPOINT

`RELEASE SAVEPOINT` is used to remove a savepoint from the current transaction.

```sql
RELEASE SAVEPOINT SP1;
```

After releasing a savepoint, we cannot rollback to that savepoint.

```sql
UPDATE orders
SET orderstatus = 'Confirmed'
WHERE oderid = 102;

SAVEPOINT orderconfirmed;

UPDATE orders
SET amount = amount - 5000
WHERE oderid = 102;

RELEASE SAVEPOINT orderconfirmed;
```

If we perform ROLLBACK then entire TRANSACTION is cancelled and the SAVEPOINT is also gone. Therefor if we use cmnd **_rollback to Savepoint Savepoint_Name_**, then it will say savepoint_name does not exist.

If we perform commit then no Save Point will be remain.

<br>

---

# AUTO COMMIT

`AUTO COMMIT` is a MySQL setting that determines whether each sql statement is automatically commited as soon as it executes.

By default MySQL usually has auto commit=1 or autocommit=ON,That means every every successfull transaction statement is automatically commited.

```sql
mysql> select @@autocommit;
+--------------+
| @@autocommit |
+--------------+
|            1 |
+--------------+
1 row in set (0.00 sec)

mysql> show variables like 'autocommit';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| autocommit    | ON    |
+---------------+-------+
1 row in set (0.05 sec)

```

<br>

---

# RELEASE SAVEPOINT

`RELEASE SAVEPOINT` is used to **remove a SAVEPOINT** from the current Transaction.

It does **not undo the changes** made after the SAVEPOINT.

## Syntax

```sql
RELEASE SAVEPOINT savepoint_name;
```

## Example

```sql
START TRANSACTION;

UPDATE orders
SET orderstatus = 'Confirmed'
WHERE oderid = 102;

SAVEPOINT orderconfirmed;

UPDATE orders
SET amount = amount - 5000
WHERE oderid = 102;

RELEASE SAVEPOINT orderconfirmed;

COMMIT;
```

After `RELEASE SAVEPOINT`:

- The SAVEPOINT is removed.
- All changes are still present.
- The Transaction remains **ACTIVE**.
- We can continue executing SQL statements.
- We can finally use `COMMIT` or `ROLLBACK`.

## Important Difference

```text
SAVEPOINT              → Creates a checkpoint
ROLLBACK TO SAVEPOINT  → Undoes changes after the checkpoint
RELEASE SAVEPOINT      → Removes the checkpoint but keeps the changes
COMMIT                 → Permanently saves the transaction
ROLLBACK               → Undoes the entire active transaction
```

## Important

The correct command is:

```sql
RELEASE SAVEPOINT orderconfirmed;
```

Not:

```sql
relase savepoint orderconfirmed;
```

`relase` is a spelling mistake.

Also, `RELEASE SAVEPOINT` works only if the specified SAVEPOINT currently exists in the active Transaction.

---

# Difference Between AUTOCOMMIT and COMMIT

## AUTOCOMMIT

→ It is a **setting**.

→ It controls **automatic committing** of transactions.

→ If `AUTOCOMMIT` is **ON**, each statement is automatically committed.

→ If `AUTOCOMMIT` is **OFF**, changes are not automatically committed; `COMMIT` is required.

---

## COMMIT

→ It is a **TCL command**.

→ It is used to **permanently save the changes** made in a Transaction.

→ `COMMIT` can be **explicit or implicit**.

---

## Example

```sql
-- Check AUTOCOMMIT
SELECT @@autocommit;

-- Turn AUTOCOMMIT OFF
SET AUTOCOMMIT = 0;

-- Make changes
UPDATE orders
SET amount = amount + 500
WHERE oderid = 101;

-- Permanently save changes
COMMIT;
```

## One-Line Difference

**AUTOCOMMIT = Setting that controls automatic committing.**

**COMMIT = TCL command used to permanently save changes.**

<br>

<br>

# CONSTRAINTS

They are the RULE or RESTRICTION applied on a table based on our requirement.

They are
