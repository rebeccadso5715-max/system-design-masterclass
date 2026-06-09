# Class 1 — What Is System Design?

Most beginners think:

> "System design means drawing boxes and arrows."

**Wrong.**

System design is:

> Designing software that continues to work when millions of users use it simultaneously.

---

## Example: Notes App

Imagine you create a Notes App.

For **10 users**:

```text
Users
  |
Server
  |
Database
```

Works perfectly.

---

Now imagine:

- 10 million users
- 100 million notes
- Users from 50 countries
- Data must never be lost
- App should open within 200ms

Suddenly, problems appear.

---

## Problem 1: Server Overload

One server cannot handle everyone.

### Solution

```text
Users
   |
Load Balancer
   |
-------------
|     |     |
S1    S2    S3
```

Use multiple servers behind a load balancer.

---

## Problem 2: Database Overload

The database becomes slow as data grows.

### Solution

- Database Replicas
- Sharding
- Caching

These techniques distribute load and improve performance.

---

## Problem 3: Slow Responses

Every request directly hits the database.

### Solution

Use a cache.

```text
User
 |
Cache
 |
DB
```

Frequently accessed data can be served from cache instead of querying the database every time.

---

## Problem 4: Server Crash

What happens if a server dies?

### Solution

- Multiple servers
- Replication
- Failover mechanisms

This ensures the application remains available even when failures occur.

---

# What Is System Design?

The process of deciding:

- How many servers are needed?
- Which database should be used?
- Which cache should be used?
- How should the system scale?
- How should the system survive failures?

is called:

## System Design

---

# The 5 Questions Every System Designer Asks

Whenever somebody says:

> Design WhatsApp

or

> Design YouTube

Ask these questions first.

---

## 1. How Many Users?

- 100?
- 1 million?
- 1 billion?

The scale determines the architecture.

---

## 2. How Much Data?

- MB?
- GB?
- PB?

Storage requirements influence database and infrastructure choices.

---

## 3. Read Heavy or Write Heavy?

Different systems have different traffic patterns.

### Instagram

- More reads
- Less writes

### WhatsApp

- More writes
- Continuous messaging traffic

Architecture changes based on workload.

---

## 4. What Is the Latency Requirement?

Can the user wait:

- 5 seconds?

Or do they need:

- 50ms response times?

Lower latency generally requires more infrastructure and optimization.

---

## 5. What Is the Availability Requirement?

Can downtime happen?

Or must the system be available:

- 99.9%
- 99.99%
- 99.999%

Higher availability requires redundancy and fault tolerance.

---

# Golden Rule

Every system design problem is a tradeoff between:

## Performance

Speed and responsiveness.

## Cost

Infrastructure and operational expenses.

## Complexity

Engineering effort and maintenance burden.

---

## Remember

You can improve one aspect, but usually at the cost of another.

```text
More Performance  → More Cost
Less Cost         → Less Performance
More Reliability  → More Complexity
```

System Design is the art of balancing these tradeoffs.

---

## Key Takeaway

System Design is not about drawing boxes and arrows.

It is about building systems that:

- Scale
- Stay fast
- Remain available
- Survive failures
- Handle millions of users efficiently

Everything else is just implementation details.
