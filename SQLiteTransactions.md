# @Transactional #

The **@Transactional** annotation indicates that an activity method is **transactional**, and therefore that a transaction will be **started before** the method is executed, and **committed afterwards**.

If the method throws a **`RuntimeException`**, the transaction will be **rollbacked**.

The method must have **at least** one parameter, which must be a SQLiteDatabase.

The method must not be private and must not declare throwing any exception.

Usage example:
```
@Transactional
void doSomeDbWork(SQLiteDatabase db) {
    db.execSQL("Some SQL");
}
```

Equivalent boilerplate code:
```
void doSomeDbWork(SQLiteDatabase db) {
    db.beginTransaction();
    try {
        db.execSQL("Some SQL");
        db.setTransactionSuccessful();
        return ;
    } catch (RuntimeException e) {
        Log.e("TransactionalActivity", "Error in transaction", e);
        throw e;
    } finally {
        db.endTransaction();
    }
}
```