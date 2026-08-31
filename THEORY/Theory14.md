## SAVEPOIT

SAVE POINT is a temporary checkpoint created inside a Transaction.
It allow us to partially undo a Transaction , Without undoing the entire Transaction.

```sql
SYNTAX>
START TRANSCATION
OPERATION1
OPERATION2
SAVEPOINT SP1;
OPERATION3
OPERATION4
ROLLBACK to SP1;
```

The above syntax will undo the operation3 and Operation4.
It will keep Operation1 and Operation2 .It will keep the transaction ACTIVE.
It allow us to execute more SQL statements. We can finally commit .
Rollback to SAVEPONT does not end the Transaction.
