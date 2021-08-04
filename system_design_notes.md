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
