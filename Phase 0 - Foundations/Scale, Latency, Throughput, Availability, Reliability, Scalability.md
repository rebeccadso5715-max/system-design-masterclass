# Class 2 — Scale, Latency, Throughput, Availability, Reliability, Scalability

These five concepts appear in almost every system design interview.

Master them and you'll understand why architectures are built the way they are.

---

# 1. Scale

**Scale** means:

> How big is the system?

## Examples

| System | Users |
|----------|----------|
| College Attendance App | 500 |
| Startup App | 10,000 |
| Social Network | 10 Million |
| WhatsApp | Billions |

A design that works for **500 users** may completely fail at **10 million users**.

---

# 2. Latency

**Latency = Time taken for one request to get a response.**

## Example

You open Instagram.

```text
Phone -> Server -> Phone
```

Response arrives in:

- 50 ms → Great
- 500 ms → Noticeable
- 5 sec → Bad

Latency measures delay.

Think:

> "How long must one user wait?"

### Example

```text
Request sent:      10:00:00.000
Response received: 10:00:00.120
```

Latency:

```text
120 ms
```

---

# 3. Throughput

**Throughput = Number of requests processed per unit time.**

## Example

A server handles:

```text
1000 requests/second
```

Throughput:

```text
1000 RPS
```

**RPS = Requests Per Second**

---

## Difference Between Latency and Throughput

### Latency

```text
One request takes 100 ms
```

### Throughput

```text
1000 requests handled every second
```

---

## Real-Life Analogy

### Restaurant

**Latency**

> How long YOUR food takes.

**Throughput**

> How many customers are served per hour.

---

## Latency vs Throughput

Suppose:

### Server A

```text
Latency   = 50 ms
Throughput = 200 req/sec
```

### Server B

```text
Latency   = 100 ms
Throughput = 5000 req/sec
```

Which is better?

### Answer

> It depends on the requirements.

System design is full of "it depends."

---

# 4. Availability

**Availability means:**

> Is the system accessible right now?

## Formula

```text
Availability = Uptime / Total Time
```

### Example

Year:

```text
365 days
```

Server down:

```text
3.65 days
```

Availability:

```text
99%
```

---

## Industry Targets

| Availability | Downtime Per Year |
|-------------|------------------|
| 99% | ~3.65 days |
| 99.9% | ~8.7 hours |
| 99.99% | ~52 minutes |
| 99.999% | ~5 minutes |

This is why people talk about:

> Five Nines Availability

```text
99.999%
```

---

# 5. Reliability

**Reliability means:**

> Does the system behave correctly?

---

## Example: Bank Transfer

You send:

```text
₹1000
```

Money disappears.

System stayed online.

### Availability

✅ High

### Reliability

❌ Low

---

## Example: WhatsApp Message

You send:

```text
Hello
```

Message delivered exactly once.

### Reliability

✅ High

---

## Availability vs Reliability

They are different concepts.

A system can be:

- Available but unreliable
- Reliable but unavailable

Great systems are both.

---

# 6. Scalability

**Scalability means:**

> Can the system handle growth without breaking?

---

## Example

Today:

```text
100 users
```

After viral success:

```text
1,000,000 users
```

Can the system survive?

If yes:

> It is scalable.

---

## Single Server Example

```text
Users
  |
Server
```

### Load Levels

```text
100 users       ✅
10,000 users    ⚠️
1,000,000 users 💀
```

Need scaling.

---

# Vertical Scaling

Add more power to one machine.

```text
8 GB RAM
   ↓
64 GB RAM

4 CPU
   ↓
64 CPU
```

## Benefits

- Easy to implement

## Problems

- Expensive
- Hardware limits exist
- Single point of failure

---

# Horizontal Scaling

Add more machines.

```text
Server1
Server2
Server3
Server4
```

Traffic is distributed across servers.

## Benefits

- Huge scale
- Better fault tolerance

## Problems

- More complexity

This is how companies like Netflix and Google scale.

---

# The Most Important Interview Insight

When traffic grows:

```text
Latency ↑
```

As load increases:

```text
Throughput ↑
```

Until capacity is reached.

Then:

```text
Latency explodes
Errors appear
System crashes
```

A large part of system design is preventing this moment.

---

# Mental Model

Whenever you see a new system, ask:

1. What is the expected scale?
2. What latency is acceptable?
3. What throughput is required?
4. What availability target exists?
5. How will it scale when traffic increases?

If you can answer these five questions, you're already thinking like a system designer.

---

# Key Takeaways

- **Scale** = How big the system is.
- **Latency** = Time for one request to complete.
- **Throughput** = Requests processed per second.
- **Availability** = Is the system up and accessible?
- **Reliability** = Does it behave correctly?
- **Scalability** = Can it grow without breaking?

These concepts form the foundation of every system design discussion and interview.
