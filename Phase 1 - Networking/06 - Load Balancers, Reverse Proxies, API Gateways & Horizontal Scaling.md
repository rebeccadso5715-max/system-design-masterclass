# Class 6 — Load Balancers, Reverse Proxies, API Gateways & Horizontal Scaling

This is where systems begin to look like real production architectures.

---

# The Problem

Suppose you build a website.

Initial architecture:

```text
Users
  |
Server
  |
Database
```

Works great.

A few months later:

```text
100 users
   ↓
10,000 users
   ↓
100,000 users
   ↓
1,000,000 users
```

The server starts struggling.

### Symptoms

- Slow responses
- Timeouts
- Crashes
- CPU at 100%

Question:

> Can we just buy a bigger machine?

Yes.

This is called:

# Vertical Scaling

```text
8 GB RAM
   ↓
64 GB RAM

4 CPU
   ↓
64 CPU
```

### Advantages

- Easy
- Fast to implement

### Problems

- Expensive
- Hardware limits exist
- Single point of failure

If the machine dies:

```text
Users
  |
 DEAD SERVER
```

Everything goes down.

---

# Horizontal Scaling

Instead of one giant server:

```text
Server A
Server B
Server C
Server D
```

Traffic is distributed across multiple machines.

This is the foundation of modern internet systems.

---

# New Problem

Users now have multiple servers.

Which server should receive the request?

```text
User
 |
 ?
 |
A  B  C  D
```

Need a traffic controller.

---

# Load Balancer

A load balancer sits in front of servers.

```text
Users
   |
Load Balancer
   |
----------------
|      |      |
A      B      C
```

Its job:

> Distribute requests among servers.

---

# Why Load Balancers Exist

Without load balancing:

```text
Server A = 100% load
Server B = idle
Server C = idle
```

Wasteful.

With load balancing:

```text
Server A = 33%
Server B = 33%
Server C = 33%
```

Much better.

---

# Load Balancing Algorithms

## Round Robin

Requests are distributed sequentially.

```text
Request 1 → A
Request 2 → B
Request 3 → C
Request 4 → A
Request 5 → B
...
```

Simple and common.

---

## Least Connections

Send traffic to the server with the fewest active connections.

Example:

```text
A = 100 connections
B = 20 connections
C = 15 connections
```

Next request goes to:

```text
C
```

---

## Weighted Round Robin

Powerful servers receive more traffic.

Example:

```text
A weight = 5
B weight = 2
C weight = 1
```

Server A receives the most requests.

---

# Health Checks

What happens if Server B dies?

Without health checks:

```text
Load Balancer
      |
      v
Dead Server
```

Users receive errors.

---

Modern load balancers continuously ask:

```text
Are you alive?
```

If a server fails:

```text
Remove From Rotation
```

Traffic automatically shifts to healthy servers.

---

# High Availability

Architecture:

```text
Users
  |
Load Balancer
  |
------------
|    |     |
A    B     C
```

If Server A fails:

```text
Users
  |
Load Balancer
  |
--------
|      |
B      C
```

System continues running.

This improves availability.

---

# Reverse Proxy

Many beginners confuse reverse proxies with load balancers.

Let's separate them.

---

# Forward Proxy

Represents the client.

```text
Client
  |
Proxy
  |
Internet
```

Common in offices, schools, and enterprises.

---

# Reverse Proxy

Represents the servers.

```text
Users
   |
Reverse Proxy
   |
Servers
```

Users never directly access backend servers.

---

## Popular Reverse Proxy

```text
NGINX
```

---

# What Can Reverse Proxies Do?

## 1. Hide Backend Servers

Users see:

```text
myapp.com
```

Instead of:

```text
10.0.0.5
10.0.0.6
10.0.0.7
```

---

## 2. SSL/TLS Termination

HTTPS traffic arrives:

```text
Encrypted
```

Reverse proxy decrypts it.

Backend servers receive:

```text
HTTP
```

This reduces work on application servers.

---

## 3. Caching

Frequently requested content:

- Homepage
- Images
- Static Assets

can be served directly from the reverse proxy.

---

## 4. Load Balancing

Many reverse proxies can also distribute traffic.

Examples:

- NGINX
- HAProxy
- Traefik

---

# Load Balancer vs Reverse Proxy

| Load Balancer | Reverse Proxy |
|---------------|---------------|
| Focuses on traffic distribution | Focuses on traffic management |
| Spreads load across servers | Protects and manages backend services |
| Improves scalability | Improves security and performance |

---

## Reality

In production systems, they often overlap.

A reverse proxy frequently performs load balancing too.

---

# API Gateway

Now let's move into microservices.

Suppose we have:

- User Service
- Order Service
- Payment Service
- Inventory Service

Architecture:

```text
Client
 |
 ?
 |
-------------------
|   |   |   |
U   O   P   I
```

How does the client know which service to call?

Messy.

---

# Solution: API Gateway

```text
Client
   |
API Gateway
   |
-------------------
|   |   |   |
U   O   P   I
```

One entry point for all services.

---

## Example Routing

Client requests:

```http
/api/orders
```

Gateway routes to:

```text
Order Service
```

---

Client requests:

```http
/api/payments
```

Gateway routes to:

```text
Payment Service
```

---

# Why API Gateways Exist

## Authentication

Validate tokens once.

```text
JWT Validation
```

instead of every service repeating the work.

---

## Rate Limiting

Prevent abuse.

Example:

```text
100 requests/minute
```

---

## Logging

Track all requests.

```text
Who called what?
When?
How often?
```

---

## Routing

Send requests to the correct service.

---

## Monitoring

Measure:

- Latency
- Error Rates
- Throughput

---

# Real Example — Food Delivery App

Services:

- User Service
- Order Service
- Payment Service
- Delivery Service
- Restaurant Service

Architecture:

```text
Client
   |
API Gateway
   |
--------------------------------
|      |      |      |        |
User  Order Payment Delivery Restaurant
```

Much cleaner than exposing every service directly.

---

# Evolution of Architecture

## Stage 1 — Monolith

```text
Users
 |
Server
 |
Database
```

---

## Stage 2 — Scaled Servers

```text
Users
 |
Load Balancer
 |
A   B   C
 |
Database
```

---

## Stage 3 — Reverse Proxy Layer

```text
Users
 |
Reverse Proxy
 |
Load Balancer
 |
A   B   C
 |
Database
```

---

## Stage 4 — Microservices

```text
Users
 |
API Gateway
 |
Microservices
 |
Databases
```

This is roughly the journey many companies follow as they scale.

---

# Interview Insight

When someone asks:

> "How would you scale the application?"

One of your first thoughts should be:

```text
Can I add more servers?
```

If the answer is yes:

> Horizontal Scaling

Then immediately ask:

```text
How will traffic be distributed?
```

Answer:

> Load Balancer

---

# Mental Model

Whenever traffic increases:

```text
More Users
     ↓
More Servers
     ↓
Load Balancer
     ↓
Traffic Distribution
```

As systems grow:

```text
Load Balancer
     ↓
Reverse Proxy
     ↓
API Gateway
     ↓
Microservices
```

Each layer solves a scaling problem.

---

# Key Takeaways

- Vertical Scaling = Bigger machine.
- Horizontal Scaling = More machines.
- Load Balancers distribute traffic.
- Health checks remove failed servers.
- Reverse Proxies manage and protect backend servers.
- API Gateways provide a single entry point to microservices.
- Horizontal scaling is the foundation of large-scale internet systems.
- Load balancers are often the first scaling component added to a growing application.

Master these concepts before moving to Caching, Databases, Message Queues, and Distributed Systems.
