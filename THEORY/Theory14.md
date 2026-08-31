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

---

# RELEASE SAVEPOINT

`RELEASE SAVEPOINT` is used to remove a savepoint from the current transaction.

```sql
RELEASE SAVEPOINT SP1;
```

After releasing a savepoint, we cannot rollback to that savepoint.
