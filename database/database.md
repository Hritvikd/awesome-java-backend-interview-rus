Here is the translated version of the page:

---

[Table of Contents](../README.md)

# Database

- [ACID - decrypt and explain a bit](#acid---decrypt-and-explain-a-bit)
- [Transaction isolation levels. What problem does each level solve? What is the default in most databases?](#transaction-isolation-levels)
- [What are the types of indexes in a database and how are they structured under the hood? What is an index anyway?](#types-of-indexes)
- [What is the difference between optimistic and pessimistic locking?](#difference-between-optimistic-and-pessimistic-locking)

## ACID - decrypt and explain a bit

- *A* - Atomicity. Ensures that no transaction is partially committed in the system.
- *C* - Consistency. Each successful transaction records only permissible results.
- *I* - Isolation. During the execution of a transaction, parallel transactions should not affect it.
- *D* - Durability. Confirmed changes will not be undone (e.g., due to a failure).

[Back to content](#database)

## Transaction isolation levels. What problem does each level solve? What is the default in most databases?

Brief summary of the [article](https://ru.wikipedia.org/wiki/Transaction_isolation_level)
- `Read uncommitted`. Ensures only that there are no lost updates.
- `Read committed`. This is often the default level. Ensures that data read are committed.
- `Repeatable read`. Solves the problem of non-repeatable reads.
- `Serializable`. Transactions are fully isolated from each other, each executed as if they were alone.

On Habr, there are several articles on the topic:
- [For beginners](https://habr.com/ru/post/469415/)
- For MSSQL: [one](https://habr.com/ru/post/305600/), [two](https://habr.com/ru/company/infopulse/blog/261097/), [three](https://habr.com/ru/company/infopulse/blog/261101/)
- [For PostgreSQL](https://habr.com/ru/post/317884/)
- For MySQL: [one](https://habr.com/ru/post/135217/), [two](https://habr.com/ru/post/238513/)
- [Transactions and their control mechanisms](https://habr.com/ru/post/446662/)

[Back to content](#database)

## What are the types of indexes in a database and how are they structured under the hood? What is an index anyway?

[Database index](https://en.wikipedia.org/wiki/Database_index) - is a data structure that increases the speed of data retrieval operations.

The most common data structures used in indexes are:
- [B-Tree Family](https://en.wikipedia.org/wiki/B-tree)
- [HASH tables](https://en.wikipedia.org/wiki/Hash_table)
- [Bitmap](http://citforum.ru/database/oracle/bitmap_index/)
- [Bloom filter](https://en.wikipedia.org/wiki/Bloom_filter)
- [Spatial grid](https://en.wikipedia.org/wiki/Grid_(spatial_index))
- [Quadtree](https://en.wikipedia.org/wiki/Quadtree)
- [R-Tree](https://en.wikipedia.org/wiki/Hilbert_R-tree)

[Index classification](http://tokarchuk.ru/2012/08/indexes-classification/) can be divided by different criteria.
For example, by sorting order:
- Ordered - indexes where records are sorted in ascending or descending order, implemented using B-Trees.
- Unordered - indexes where records are not sorted, implemented using hashes.
Or by the impact on the data source:
- Non-clustered - these indexes organize references to the corresponding rows and values. The reference contains information...
- Clustered - these indexes represent a tree-like data structure, where the index values...

Further reading:
- [Overview of index types Oracle, MySQL, PostgreSQL, MS SQL](https://habr.com/ru/post/102785/)
- Excellent series of articles by Yegor Rogov on indexes in PostgreSQL: [part 1](https://habr.com/ru/company/postgrespro/blog/326096/), [part 2](https://habr.com/ru/company/postgrespro/blog/326096/)
- [Clustered and "regular" indexes MySQL (InnoDB)](https://habr.com/ru/post/141767/)
- [Under the hood of Postgres indexes](https://habr.com/ru/company/mailru/blog/261871/)
- [Types of indexes, types of indexes, or what indexes are there?](http://tokarchuk.ru/2012/08/indexes-classification/)
- [Database index: types of indexes](https://alextoolsblog.blogspot.com/2019/11/database-index-types.html)
- [Database index: indexing methods, applications, and limitations](https://alextoolsblog.blogspot.com/2019/11/database-index-methods.html)
- [Database index](https://alextoolsblog.blogspot.com/2019/11/database-index.html)
- [Database Indexes Explained](https://www.essentialsql.com/what-is-a-database-index/)
- [Bitmap or B*tree index: which and when to apply?](http://citforum.ru/database/oracle/bb_indexes/)
- [Indexes in MySQL](https://ruhighload.com/Indexes+in+mysql)
- [How relational databases work](https://habr.com/ru/company/mailru/blog/266811/)
- [Index health in PostgreSQL through the eyes of a Java developer](https://habr.com/ru/post/490824/)
- [14 questions about indexes in SQL Server that you were too shy to ask](https://habr.com/ru/post/247373/)
- [Questions about indexes that you won't need to ask](https://habr.com/ru/post/247949/)
- [Using all the possibilities of indexes in PostgreSQL](https://habr.com/ru/company/mailru/blog/453046/)
- [Anatomy of an SQL Index](https://use-the-index-luke.com/sql/anatomy)
- [SQL Indexing and Tuning e-Book](https://use-the-index-luke.com/)
- [Deep dive into Hash indexes for In-Memory OLTP tables](https://www.sqlshack.com/deep-dive-hash-indexes-in-memory-oltp-tables/)
- [Indexing based on Hashing](http://www.mathcs.emory.edu/~cheung/Courses/554/Syllabus/3-index/hashing.html)
- [SQL Server Indexes Interview Questions and Answers](https://dotnettutorials.net/lesson/sql-server-indexes-interview-questions-answers/)
- [Top 25 SQL interview questions and answers about indexes](https://www.sqlshack.com/top-25-sql-interview-questions-and-answers-about-indexes/)
- [An in-depth look at Database Indexing](https://www.freecodecamp.org/news/database-indexing-at-a-glance-bb50809d48bd/)

[Back to content](#database)

## What is the difference between optimistic and pessimistic locking?

[Locking](https://ru.wikipedia.org/wiki/Lock_(database)) in a DBMS - a mark of capturing a resource.

Pessimistic locking - applied before the anticipated modification of data to all rows...
Pessimistic locking can be of two types:
- shared (read) - blocks writers but allows readers to continue working. In other words, allows other transactions...
- exclusive (write) - blocks both writers and readers. Makes all write operations sequential. In other words, ...

[Optimistic locking](https://en.wikipedia.org/wiki/Optimistic_concurrency_control) - does not restrict the modification of processed...

The main difference is that optimistic locking incurs overhead only in case of conflict...

Many articles about locks with code and pictures can be read on Vlad Mihalcea's blog:
- [A beginner’s guide to Java Persistence locking](https://vladmihalcea.com/a-beginners-guide-to-java-persistence-locking/)
- [A beginner’s guide to database locking and the lost update phenomena](https://vladmihalcea.com/a-beginners-guide-to-database-locking-and-the-lost-update-phenomena/)
- [How do LockModeType.PESSIMISTIC_READ and LockModeType.PESSIMISTIC_WRITE work in JPA and Hibernate](https://vladmihalcea.com/hibernate-locking-patterns-how-do-pessimistic_read-and-pessimistic_write-work/)
- [How does LockModeType.PESSIMISTIC_FORCE_INCREMENT work in JPA and Hibernate](https://vladmihalcea.com/hibernate-locking-patterns-how-does-pessimistic_force_increment-lock-mode-work/)
- [How does LockModeType.OPTIMISTIC work in JPA and Hibernate](https://vladmihalcea.com/hibernate-locking-patterns-how-does-optimistic-lock-mode-work/)
- [How does LockModeType.OPTIMISTIC_FORCE_INCREMENT work in JPA and Hibernate](https://vladmihalcea.com/hibernate-locking-patterns-how-does-optimistic_force_increment-lock-mode-work/)
- [How to prevent OptimisticLockException with Hibernate versionless optimistic locking](https://vladmihalcea.com/how-to-prevent-optimisticlockexception-using-hibernate-versionless-optimistic-locking/)
- [How does database pessimistic locking interact with INSERT, UPDATE, and DELETE SQL statements](https://vladmihalcea.com/how-does-database-pessimistic-locking-interact-with-insert-update-and-delete-sql-statements/)
- [How does MVCC (Multi-Version Concurrency Control) work](https://vladmihalcea.com/how-does-mvcc-multi-version-concurrency-control-work/)
- [How does the 2PL (Two-Phase Locking) algorithm work](https://vladmihalcea.com/2pl-two-phase-locking/)
- [How to prevent lost updates in long conversations](https://vladmihalcea.com/preventing-lost-updates-in-long-conversations/)

More on Habr:
- [Concurrent access to relational databases](https://habr.com/ru/post/121858/)
- [Databases. Parallel access conflicts](https://habr.com/ru/post/86302/)
- [Remarkable annotation Version in JPA](https://habr.com/ru/post/434836/)
- [Hibernate Developer Documentation – Chapter V. Locking](https://habr.com/ru/post/268903/)
- [Locks in PostgreSQL: 1. Relation locks](https://habr.com/ru/company/postgrespro/blog/462877/)
- [Locks in PostgreSQL: 2. Row locks](https://habr.com/ru/company/postgrespro/blog/463819/)
- [Locks in PostgreSQL: 3. Other object locks](https://habr.com/ru/company/postgrespro/blog/465263/)
- [Locks in PostgreSQL: 4. Memory locks](https://habr.com/ru/company/postgrespro/blog/466199/)

More in other sources:
- [Pessimistic Locking in JPA](https://www.baeldung.com/jpa-pessimistic-locking)
- [Optimistic Locking in JPA](https://www.baeldung.com/jpa-optimistic-locking)
- [Enabling Transaction Locks in Spring Data JPA](https://www.baeldung.com/java-jpa-transaction-locks)
- [Deadlock](https://en.wikipedia.org/wiki/Deadlock)
- [Enum LockModeType](https://docs.oracle.com/javaee/7/api/javax/persistence/LockModeType.html)
- [Explicit locks in Postgresql](https://postgrespro.ru/docs/postgresql/12/explicit-locking)
- [PostgreSQL Concurrency with MVCC](https://devcenter.heroku.com/articles/postgresql-concurrency)
- [Locking](https://docs.jboss.org/hibernate/orm/current/userguide/html_single/Hibernate_User_Guide.html#locking) in Hibernate documentation
- [Optimistic locking](https://www.jooq.org/doc/latest/manual/sql-execution/crud-with-updatablerecords/optimistic-locking/) in JOOQ documentation
- [Optimistically Locking Your Spring Boot Web Services](https://medium.com/slalom-build/optimistically-locking-your-spring-boot-web-services-187662eb8a91)
- [Optimistic and pessimistic locking with SQL](https://convincedcoder.com/2018/09/01/Optimistic-pessimistic-locking-sql/)

[Back to content](#database)

---

If you need any further assistance, feel free to ask!
