# ACID Properties in Databases

**ACID** is an acronym that describes the key properties of a reliable database transaction system. These properties ensure that database transactions are processed reliably and protect the integrity of the data.

## What Does ACID Stand For?

- **Atomicity**  
  Transactions are “all or nothing.” Either all steps of the transaction succeed, or none do. This prevents partial updates to the database.

- **Consistency**  
  Transactions bring the database from one valid state to another, maintaining all predefined rules, such as constraints and triggers.

- **Isolation**  
  Concurrent transactions do not interfere with each other. Each transaction behaves as if it were the only one running in the system.

- **Durability**  
  Once a transaction is committed, its changes are permanent, even in the event of a system crash or power failure.

## Why Is ACID Important?

- Guarantees data integrity
- Enables safe concurrent access
- Prevents data corruption and loss

## Example Scenario

Consider transferring money between two bank accounts:

1. Deduct $100 from Account A.
2. Add $100 to Account B.

With ACID:

- **Atomicity** ensures both steps happen, or neither do.
- **Consistency** ensures total money is the same before and after the transaction.
- **Isolation** ensures no other transactions interfere during the transfer.
- **Durability** ensures the transfer is saved permanently once complete.

---

## References

- [Wikipedia: ACID](https://en.wikipedia.org/wiki/ACID)
- [Database Systems Concepts](https://www.db-book.com/)  
