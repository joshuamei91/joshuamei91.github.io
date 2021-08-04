---
layout: page
title: Database
permalink: /db/
---

## SQL

- [How does database indexing work](https://stackoverflow.com/questions/1108/how-does-database-indexing-work)

- [How SQL indexing works](https://www.sqlshack.com/top-10-questions-answers-sql-server-indexes/)

- Considerations for indexing
1. Creating a large number of indexes on a database table affects data modification (e.g. Updates) operation performance. When you add or modify a row in the underlying table, the row will also be adjusted appropriately in all related table indexes. Because of that, you need to avoid creating a large number of indexes on the heavily modified tables and create the minimum possible number of indexes, with the least possible number of columns on each index. ([ref](https://www.sqlshack.com/top-25-sql-interview-questions-and-answers-about-indexes/))

