# Class 7 — Databases
## SQL vs NoSQL, Indexing, Replication, Sharding

This is one of the most important classes in the entire course.

Many system design interviews are actually database design discussions disguised as system design questions.

---

# Part 1 — What Is a Database?

A database is where data lives.

Without a database:

```text
User Registers
      ↓
Server Restarts
      ↓
User Disappears
```

Not acceptable.

We need **persistent storage**.

---

## Example: Food Delivery App

Store:

- Users
- Restaurants
- Orders
- Payments
- Addresses

All of this goes into a database.

---

# Part 2 — SQL Databases

Popular SQL databases:

- PostgreSQL
- MySQL
- Microsoft SQL Server

SQL stands for:

> Structured Query Language

Data is stored in tables.

---

## Users Table

| id | name | email |
|----|------|--------|
| 1 | Rahul | r@gmail.com |
| 2 | Amit | a@gmail.com |

---

## Orders Table

| id | user_id | amount |
|----|---------|---------|
| 101 | 1 | 500 |
| 102 | 2 | 700 |

Notice:

```text
user_id
```

connects the tables.

Because tables can be related, SQL databases are called:

> Relational Databases

---

# SQL Strengths

## Strong Consistency

When data is written:

```text
Write
  ↓
Immediately Visible
```

---

## Transactions

Critical for:

- Banking
- Payments
- Inventory Management
- Financial Systems

---

## Complex Queries

Example:

```sql
SELECT *
FROM Orders
JOIN Users
ON Orders.user_id = Users.id;
```

SQL excels at joins and analytical queries.

---

# SQL Weaknesses

At very large scale:

- Scaling becomes harder
- Sharding becomes complex
- Large joins become expensive

---

# Part 3 — NoSQL Databases

Popular NoSQL databases:

- MongoDB
- Cassandra
- DynamoDB

NoSQL means:

> Not Only SQL

It does **not** mean:

> No SQL

---

## Example Document

```json
{
  "id": 1,
  "name": "Rahul",
  "skills": ["Java", "Python"]
}
```

Instead of rows and tables, data is often stored as documents.

---

# NoSQL Advantages

- Flexible schema
- Easy horizontal scaling
- High write throughput
- Good for rapidly changing data structures

---

# NoSQL Disadvantages

- Weaker joins
- Sometimes weaker consistency
- More application-side logic

---

# SQL vs NoSQL

| Feature | SQL | NoSQL |
|----------|----------|----------|
| Schema | Fixed | Flexible |
| Joins | Excellent | Weak |
| Consistency | Strong | Often Configurable |
| Scaling | Harder | Easier |
| Transactions | Strong | Limited / Varies |

---

# Interview Rule

## Use SQL When

- Payments
- Banking
- Orders
- Inventory
- Financial Records

---

## Use NoSQL When

- Massive scale
- Flexible data structures
- High throughput requirements

---

## Reality

Most large companies use both.

---

# Part 4 — The Big Problem

Suppose:

```text
10 Users
```

Database is fast.

Then:

```text
10 Million Users
```

Database becomes slow.

Why?

Because searching data becomes expensive.

---

# Part 5 — Indexing

Imagine a book.

Need information about:

```text
Distributed Systems
```

You don't read every page.

You use:

```text
Index
```

Databases work the same way.

---

# Without Index

Searching for an email:

```text
user1
user2
user3
...
user10,000,000
```

Database may scan millions of rows.

This is called a:

> Full Table Scan

Slow.

---

# With Index

Database can jump directly to the desired record.

Much faster.

---

## Example

```sql
CREATE INDEX idx_email
ON users(email);
```

Now email lookups become significantly faster.

---

# Cost of Indexes

Indexes are not free.

Every write must update:

```text
Table
  +
Index
```

Result:

```text
Reads  → Faster
Writes → Slower
```

A classic tradeoff.

---

# Part 6 — Replication

Suppose you have:

```text
1 Database
```

Problems:

- Too many reads
- Single point of failure

Solution:

> Replication

---

# Replication Architecture

```text
Primary
   |
-----------
|         |
Replica1 Replica2
```

---

## Primary Database

Handles writes:

```text
INSERT
UPDATE
DELETE
```

---

## Replica Databases

Handle reads:

```text
SELECT
```

---

# Benefits of Replication

## More Read Capacity

```text
1 Database
    ↓
3 Databases
```

More users can be served.

---

## Fault Tolerance

If one replica fails:

```text
Replica 1 ❌

Replica 2 ✅
```

System continues working.

---

# Replication Lag

Very important concept.

Suppose:

```text
User Changes Password
```

Primary updates immediately.

Replica receives update:

```text
200 ms Later
```

This delay is called:

> Replication Lag

---

## Example

```text
Write
  ↓
Primary Updated
  ↓
Replica Updated Later
```

Important interview topic.

---

# Part 7 — Sharding

Now imagine:

```text
500 Million Users
```

One database is no longer enough.

Need partitioning.

---

# What Is Sharding?

Split data across multiple databases.

Example:

```text
Users A-H → Shard 1
Users I-P → Shard 2
Users Q-Z → Shard 3
```

---

## Architecture

```text
           Router
              |
------------------------------
|             |             |
Shard1      Shard2       Shard3
```

---

# Benefits of Sharding

## More Storage

Each shard stores less data.

---

## More Throughput

Queries are spread across databases.

```text
Shard 1 → Some Users
Shard 2 → Some Users
Shard 3 → Some Users
```

Less load per database.

---

# Problems With Sharding

Very important.

---

## Cross-Shard Queries

Need:

```text
All Users
```

But data exists everywhere.

```text
Shard1
Shard2
Shard3
```

Harder to query.

---

## Rebalancing

Suppose:

```text
New Shard Added
```

```text
Shard4
```

Need to move data.

Complex operation.

---

## Hot Shards

Suppose all celebrity users end up in:

```text
Shard 1
```

Now:

```text
Shard1 = Overloaded
Shard2 = Idle
Shard3 = Idle
```

This is called a:

> Hot Shard

A common real-world problem.

---

# Replication vs Sharding

Students frequently confuse these.

---

## Replication

```text
Same Data
Multiple Copies
```

Goal:

- Availability
- Read Scaling

---

## Sharding

```text
Different Data
Different Databases
```

Goal:

- Storage Scaling
- Write Scaling

---

# Memorize

```text
Replication = Copies

Sharding = Splits
```

---

# Real Example

Imagine an Instagram-like platform.

Scale:

```text
Users: 500 Million
Posts: 50 Billion
```

Likely architecture:

```text
Sharded Databases
        |
     Replicas
        |
Application Servers
```

A single database would never survive this scale.

---

# Interview Insight

Whenever you hear:

> "The database is slow."

Think:

```text
Can I add indexes?
```

```text
Can I add replicas?
```

```text
Can I add caching?
```

```text
Can I shard the data?
```

These are some of the most common scaling moves in system design.

---

# Mental Model

Database scaling usually follows this journey:

```text
Small Database
       ↓
Add Indexes
       ↓
Add Replicas
       ↓
Add Cache
       ↓
Shard Data
```

Each step helps support more users and more traffic.

---

# Key Takeaways

- Databases provide persistent storage.
- SQL databases excel at consistency, joins, and transactions.
- NoSQL databases excel at scale and flexibility.
- Indexes speed up reads but make writes more expensive.
- Replication improves availability and read performance.
- Replication introduces replication lag.
- Sharding splits data across multiple databases.
- Sharding improves storage and write scalability.
- Replication = Copies.
- Sharding = Splits.

Master these concepts before moving to Caching, Redis, Message Queues, and Distributed Systems.
