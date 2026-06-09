# Class 5 — DNS, IP Addresses, TCP, UDP, Ports & How Data Travels on the Internet

This is one of the most important networking classes.

A huge percentage of system design concepts ultimately rely on understanding how machines communicate.

---

# Part 1 — What Is an IP Address?

Every device on the Internet needs an address.

Just as your house has an address:

```text
Flat 402, XYZ Building
Mumbai
```

Computers have addresses too.

Example:

```text
142.250.183.46
```

This is an IP address.

Think:

> IP Address = Internet Address of a Machine

---

## Why Do We Need IP Addresses?

Suppose you open:

```text
google.com
```

How does your laptop know where Google's server is?

It needs an address.

Without an IP:

```text
Client ----> ???
```

No idea where to send data.

---

# IPv4

Most common format:

```text
192.168.1.1
```

Four numbers separated by dots.

Each section ranges from:

```text
0 - 255
```

Example:

```text
8.8.8.8
```

Google Public DNS.

---

## Problem With IPv4

The Internet grew massively.

Billions of devices came online.

IPv4 addresses started running out.

---

# IPv6

Newer format:

```text
2001:0db8:85a3::8a2e:0370:7334
```

Provides a huge address space.

Enough for an enormous number of devices.

---

## Interview Note

Most system design discussions still casually use IPv4 examples because they are easier to read.

---

# Part 2 — What Is DNS?

Nobody wants to remember:

```text
142.250.183.46
```

Humans prefer:

```text
google.com
```

DNS solves this problem.

DNS stands for:

> Domain Name System

Think:

> DNS is the Internet's phonebook.

---

## Example

```text
google.com
      ↓
142.250.183.46
```

---

## DNS Flow

```text
Browser
   |
DNS Query
   |
DNS Server
   |
Returns IP
   |
Browser Contacts Server
```

---

# Real Request Flow

You type:

```text
youtube.com
```

Browser asks:

```text
Where is youtube.com?
```

DNS replies:

```text
142.x.x.x
```

Browser:

```text
Okay, connecting...
```

---

## Why DNS Matters in System Design

DNS failures can take down huge systems.

If DNS fails:

```text
Users
  |
Cannot Locate Servers
  |
Website Appears Down
```

Even if servers are perfectly healthy.

---

# Part 3 — What Is a Port?

One machine can run many applications.

Example:

- Chrome
- VS Code
- Spotify
- Discord

All on the same machine.

All sharing the same IP address.

So how does traffic reach the correct application?

Using ports.

---

## Easy Analogy

Think:

```text
IP Address = Apartment Building
Port       = Apartment Number
```

---

## Example

```text
IP Address: 142.250.183.46
Port:       443
```

Together:

```text
142.250.183.46:443
```

---

# Common Ports

| Port | Purpose |
|--------|---------|
| 80 | HTTP |
| 443 | HTTPS |
| 22 | SSH |
| 3306 | MySQL |
| 5432 | PostgreSQL |

---

## Memorize

```text
80  → HTTP
443 → HTTPS
```

---

# Part 4 — What Is TCP?

Data travels across networks as packets.

Suppose you're sending:

```text
Hello World
```

The Internet is not perfectly reliable.

Packets may:

- Arrive late
- Arrive out of order
- Get lost

TCP solves these problems.

TCP stands for:

> Transmission Control Protocol

Think:

> Reliable communication.

---

# TCP Guarantees

## 1. Delivery

Packet lost?

```text
Retransmit
```

---

## 2. Correct Order

Packets arrive:

```text
3
1
2
```

TCP reorders them:

```text
1
2
3
```

---

## 3. Error Checking

Packet corrupted?

```text
Send Again
```

---

# Why TCP Exists

Without TCP:

```text
HELLO
```

might arrive as:

```text
HLO
```

or

```text
ELHLO
```

Not acceptable for:

- Banking
- Login Systems
- APIs
- Databases

---

# TCP Three-Way Handshake

Before communication starts, a connection must be established.

---

## Step 1

Client sends:

```text
SYN
```

Meaning:

> Can we talk?

---

## Step 2

Server responds:

```text
SYN-ACK
```

Meaning:

> Yes, I can hear you.

---

## Step 3

Client sends:

```text
ACK
```

Meaning:

> Great, let's begin.
```

Connection established.

```text
Client <----> Server
```

---

## Memorize

```text
SYN
SYN-ACK
ACK
```

A very common interview question.

---

# Part 5 — What Is UDP?

UDP stands for:

> User Datagram Protocol

Unlike TCP, UDP does **not** guarantee:

- Delivery
- Ordering
- Retransmission

---

## Why Use UDP Then?

Because it is fast.

Very fast.

---

### TCP

```text
Reliable
Slower
```

---

### UDP

```text
Fast
Unreliable
```

---

# Common UDP Use Cases

## Video Calls

Missing one packet?

No problem.

Keep moving.

Uses UDP heavily.

---

## Online Gaming

Speed matters more than perfection.

Often uses UDP.

---

## Live Streaming

Small packet loss is acceptable.

Uses UDP extensively.

---

# TCP vs UDP

| Feature | TCP | UDP |
|----------|----------|----------|
| Reliable | Yes | No |
| Ordered | Yes | No |
| Connection Required | Yes | No |
| Faster | No | Yes |
| Retransmission | Yes | No |

---

# Part 6 — Complete Internet Journey

Suppose you open:

```text
https://youtube.com
```

---

## Step 1

Browser asks DNS:

```text
Where is youtube.com?
```

---

## Step 2

DNS returns:

```text
142.x.x.x
```

---

## Step 3

Browser connects to:

```text
142.x.x.x:443
```

Port 443 because HTTPS.

---

## Step 4

TCP Handshake

```text
SYN
SYN-ACK
ACK
```

Connection established.

---

## Step 5

HTTP Request Sent

```http
GET /
```

Meaning:

> Give me the homepage.

---

## Step 6

Server Processes Request

```text
Request Received
       ↓
Business Logic
       ↓
Response Generated
```

---

## Step 7

Response Returned

```text
HTML
CSS
JavaScript
Images
```

sent back to the browser.

---

## Step 8

Browser Renders Page

```text
Code
  ↓
UI
```

User sees:

```text
YouTube Homepage
```

---

# Complete Flow Diagram

```text
Domain Name
     |
     v
DNS
     |
     v
IP Address
     |
     v
Port
     |
     v
TCP Connection
     |
     v
HTTP Request
     |
     v
Server
     |
     v
HTTP Response
     |
     v
Browser
```

Everything you see online starts with this chain.

---

# Mental Model

Whenever you open a website:

```text
Domain
  ↓
DNS
  ↓
IP Address
  ↓
Port
  ↓
TCP
  ↓
HTTP
  ↓
Server
  ↓
Response
  ↓
Browser
```

If you understand this flow deeply, networking becomes much easier.

---

# Key Takeaways

- Every device on the Internet has an IP address.
- DNS converts domain names into IP addresses.
- Ports help route traffic to the correct application.
- TCP provides reliable communication.
- UDP provides fast communication with fewer guarantees.
- HTTPS commonly uses Port 443.
- Every web request follows a networking journey before reaching a server.
- Most advanced system design topics build on these networking fundamentals.

Master this flow before moving to Load Balancers, CDNs, Reverse Proxies, and Distributed Systems.
