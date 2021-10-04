---
layout: page
title: Database
permalink: /db/
---

## MongoDB

- Find distinct values: `db.inventory.distinct( "item.field", { queryKey: "queryValue" } )`
- Find records that are in the list: `db.collection.find( { _id : { $in : [1,2,3,4] } } )`;

## SQL

- [How does database indexing work](https://stackoverflow.com/questions/1108/how-does-database-indexing-work)

- [How SQL indexing works](https://www.sqlshack.com/top-10-questions-answers-sql-server-indexes/)

- Considerations for indexing
1. Creating a large number of indexes on a database table affects data modification (e.g. Updates) operation performance. When you add or modify a row in the underlying table, the row will also be adjusted appropriately in all related table indexes. Because of that, you need to avoid creating a large number of indexes on the heavily modified tables and create the minimum possible number of indexes, with the least possible number of columns on each index. ([ref](https://www.sqlshack.com/top-25-sql-interview-questions-and-answers-about-indexes/))

- ACID Trasaction (a sequence of database operations that satisfies the ACID properties, which can be perceived as a single logical operation on the data, is called a transaction)
  - Atomicity: Any transaction that updates multiple rows is treated as a single unit. A successful transaction performs all updates. A failed transaction performs none of the updates, i.e., the database is left unchanged.
  - Consistency: Every transaction brings the database from one valid state to another. It guarantees to maintain all database invariants and constraints.
  - Isolation: Concurrent execution of multiple transactions leaves the database in the same state as if the transactions were executed sequentially.
  - Durability: Committed transactions are permanent, and survive even a system crash.

- [SQL Joins](https://www.sqlshack.com/different-approaches-to-sql-join-multiple-tables/)
- A foreign key is designed to protect database integrity. Eg. What a foreign key will do is prevent you form corrupting your data by doing things like deleting the parent record that a child record refers to.

- CAP Theorem
  
  NoSQL datastores offer horizontal scale at various CAP Theorem tradeoffs. As per CAP Theorem, a distributed datastore can give at most 2 of the following 3 guarantees:
  - Consistency: Every read receives the most recent write or an error. It is about the state of all nodes being consistent with each other at any given time.
  - Availability: Every request gets a (non-error) response, regardless of the individual states of the nodes.
  - Partition tolerance: The cluster does not fail despite an arbitrary number of messages being dropped (or delayed) by the network between nodes.
  - Good [article](https://www.gavstech.com/the-cap-on-choosing-the-right-distributed-databases/) on the trade offs in CAP Theorem

- [Benefits of NoSQL](https://www.mongodb.com/nosql-explained/nosql-vs-sql)
  - Flexible data models
  - Horizontal scaling is easy
  - Fast queries
    > Queries in NoSQL databases can be faster than SQL databases. Why? Data in SQL databases is typically normalized, so queries for a single object or entity require you to join data from multiple tables. However, data in NoSQL databases is typically stored in a way that is optimized for queries. The rule of thumb when you use MongoDB is Data is that is accessed together should be stored together. Queries typically do not require joins, so the queries are very fast.