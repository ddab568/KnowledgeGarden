
## Types

### Relational (SQL)

Information is stored in tables, in rows and columns. Tables usually have relationships with other tables.

Structured Query Language (SQL) is used to interact with relational databases.

Examples:

- Microsoft SQL Server
- MySQL
- PostgresSQL

Advantages of using a relational database include:

**ACID Compliance**

Atomicity, Consistency, Isolation, Durability (ACID) is a standard that guarantees the reliability of database transactions. ACID transactions are a group of database operations that succeed only if all the operations within succeed. This ensures that the database remains in a consistent state and there are no dangling incomplete mutations.

To understand this, we can think of a bank transfer where we transfer from one account to another. Here we expect that in our first account, we expect both accounts to reflect a new transaction e.g. $100 from ACC1 to ACC2:

```SQL
UPDATE bankaccounts SET funds=funds-100 WHERE accountno='ACC1';
UPDATE bankaccounts SET funds=funds+100 WHERE accountno='ACC2';
```

If our second statement were to fail, the accuracy of the database would be compromised. In order to fix this, we use a transaction:

```SQL
START TRANSACTION or BEGIN; -- Wrap the statements in a transaction
UPDATE bankaccounts SET funds=funds-100 WHERE accountno='ACC1'; --statement2
UPDATE bankaccounts SET funds=funds+100 WHERE accountno='ACC2'; --statement3
COMMIT; -- COMMIT to DB once all statements pass successfully
```

**Data Accuracy**

Primary and foreign keys ensure there is no duplication.

### Non-relational (No SQL)

### Relational or Non-relational?

#### References

1. https://www.softwaretestinghelp.com/mysql-transaction-tutorial/
2. https://www.mongodb.com/basics/acid-transactions
3. https://www.mongodb.com/compare/relational-vs-non-relational-databases
