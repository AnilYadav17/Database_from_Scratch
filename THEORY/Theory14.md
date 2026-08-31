# SAVEPOINT

## Concept

**SAVEPOINT** = Creates a checkpoint inside a transaction so you can rollback to that point without undoing the entire transaction.<br>
The above syntax will undo the operation3 and Operation4.
It will keep Operation1 and Operation2 .It will keep the transaction ACTIVE.
It allow us to execute more SQL statements. We can finally commit .
Rollback to SAVEPONT does not end the Transaction.

## Syntax

```sql
SAVEPOINT savepoint_name;
```

## Rollback to SAVEPOINT

```sql
ROLLBACK TO SAVEPOINT savepoint_name;
```

## Important Points

- `SAVEPOINT` creates a checkpoint inside a transaction.
- `ROLLBACK TO SAVEPOINT` undoes changes made **after** that savepoint.
- `COMMIT` permanently saves all changes and removes the savepoints.
- `ROLLBACK` undoes the transaction and removes the savepoints.
- You must create the `SAVEPOINT` **before** using `ROLLBACK TO SAVEPOINT`.

## Example

```sql
START TRANSACTION;

UPDATE orders
SET orderstatus = 'Confirmed'
WHERE oderid = 101;

SAVEPOINT orderconfirmed;

UPDATE orders
SET amount = amount + 500
WHERE oderid = 101;

ROLLBACK TO SAVEPOINT orderconfirmed;

COMMIT;
```

## Error

```sql
ROLLBACK TO orderconfirmed;
```

**Error:** `SAVEPOINT orderconfirmed does not exist`

### Reason

The SAVEPOINT was not created before the rollback command, or it was already removed by `COMMIT` or `ROLLBACK`.

### Simple Flow

```text
START TRANSACTION
       ↓
   UPDATE
       ↓
  SAVEPOINT
       ↓
   UPDATE
       ↓
ROLLBACK TO SAVEPOINT
       ↓
    COMMIT
```
