---
layout: page
title: System Design
permalink: /system-design/
---

## Handling concurrent transactions to same record (preventing lost updates)

### Pessimistic locking 

Lock the record so that other processes cannot retrieve and update the same record. In SQL server, this can be done by setting the transaction isolation level to `Repeatable Read`.

Cons: 
- Some DBMS don't support locking, while some support only locking at table level or page lock (locking chunks of data)
- Process will be waiting for first process to free up the record
- Favours process that requests the record first instead of the process that makes the changes quickly

### Read before write

1. Read 'before' state of record
2. Update record with the change. Eg. amount += 100
3. Read 'current' state of record
4. If 'before' and 'after' state is the same, commit the changes. Else, start the update from the beginning.

Pros: 
- Works for non-DBMS stores

Cons:
- Extra code to compare all the fields in the 'before' and 'current' state

### Timestamping or versioning

Add a 'last modified' field to the record. Perform read before write technique but only compare the 'last modified' time

### References:
- https://www.informit.com/articles/article.aspx?p=22681&seqNum=3
- https://www.sqlservercentral.com/articles/concurrency-control-in-sql-server
- https://stackoverflow.com/questions/29025278/how-does-the-inc-modifier-work-with-concurrent-requests-in-mongodb
- https://stackoverflow.com/questions/61391417/mongodb-optimistic-concurrency-control-for-update


## [Choosing between SQL and NoSQL database](https://towardsdatascience.com/datastore-choices-sql-vs-nosql-database-ebec24d56106)
- Consistent read and write queries, not many joins, large amount of data with simple lookup queries - use NoSQL
- Differences between RDBMS and NoSQL databases stem from their choices for:
  - Data Model: RDBMS databases are used for normalized structured (tabular) data strictly adhering to a relational schema. NoSQL datastores are used for non-relational data, e.g. key-value, document tree, graph.
  - Transaction Guarantees: All RDBMS databases support ACID transactions, but most NoSQL datastores offer BASE transactions.
  - CAP Tradeoffs: RDBMS databases prioritize strong consistency over everything else. But NoSQL datastores typically prioritize availability and partition tolerance (horizontal scale) and offer only eventual consistency.

## Bottleneck in read/write for database
- For read heavy applications: can have read replicas that will offload the reads from the main database

## Key advantages of microservices
- Able to scale up different services depending on their traffic pattern
- Able to decouple services so that it is easier to troubleshoot any problems, do upgrades, maintenance, prevent failure of one service from affecting another service

## Asynchronous requests
- Can introduce a message queue to queue the records and reply to the client, then process the records 

## Reduce latency of results
- Introduce cache before the database so that the same queries will get results faster from the cache
- Have a CDN to cache the static content closer to the client

## Event driven real time streaming
- [Understanding Kafka](https://medium.com/event-driven-utopia/understanding-kafka-topic-partitions-ae40f80552e8)

## Deduplicate same content
- Use file hashes

## System Design Interview Tips
- Define core functional requirements (product thinking: thinking of more in depth features which will improve user experience)
- Define non-functional requirements (scale, latency, availability)
- Define some estimates (no. of users per day, size of data)
- Define services, APIs 
- Type of database. When using NoSQL database, have to talk about the access pattern. Access pattern will guide you towards the appropriate data schema
- Type of data tables / collections, fields in each table
- Request / data flow from client to database
- Talk about the tradeoffs
- For search on text based data, can mention to use elastic search

