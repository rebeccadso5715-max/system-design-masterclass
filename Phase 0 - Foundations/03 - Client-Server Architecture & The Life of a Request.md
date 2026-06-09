# Class 3 — Client-Server Architecture & The Life of a Request

This class is extremely important.

Many people memorize Redis, Kafka, and Load Balancers without understanding what actually happens when they open a website.

Today we're fixing that.

---

# What Happens When You Open YouTube?

When you type:

```text
youtube.com
```

A huge chain of events starts.

Understanding this chain is one of the foundations of system design.

---

# The Client

A **client** is something that requests a service.

## Examples

- Browser
- Mobile App
- Desktop App

Your phone running:

```text
Instagram App
```

is a client.

Your Chrome browser opening:

```text
google.com
```

is also a client.

---

# The Server

A **server** provides services.

### Example

User asks for a video.

Server responds:

> Here is the video.

---

## Simple Model

```text
Client ----> Server
Request

Client <---- Server
Response
```

This is called:

# Client-Server Architecture

---

# Example: Food Delivery App

```text
Phone App
     |
     |
Internet
     |
     |
Backend Server
     |
Database
```

User presses:

> Show nearby restaurants

The app sends a request.

Server:

1. Reads database
2. Finds restaurants
3. Sends result back

---

# Every System Starts Like This

Even giant systems usually start as:

```text
Client
   |
Server
   |
Database
```

Only later do they become complex.

---

# Request and Response

Suppose a user logs in.

### Request

```text
Username: Rahul
Password: ****
```

Server receives it.

Server processes it.

### Response

```text
Login Successful
```

This pattern is called:

```text
Request → Processing → Response
```

Nearly every software system follows this model.

---

# The Internet Is Just Connected Computers

Many beginners imagine the Internet as magic.

Actually it looks more like:

```text
Computer
   |
Routers
   |
Switches
   |
Fiber Cables
   |
Data Centers
   |
Servers
```

Everything is simply computers talking to other computers.

---

# Life of a Request

Suppose you're in Mumbai.

You open:

```text
amazon.com
```

Your browser begins a journey.

---

# Step 1: Browser Needs an IP Address

Humans remember:

```text
amazon.com
```

Computers use:

```text
54.x.x.x
```

(IP Address)

So the browser asks:

> Where is amazon.com?

---

# Step 2: DNS Lookup

DNS stands for:

> Domain Name System

Think of it as the Internet's phonebook.

### Example

```text
amazon.com
        ↓
     54.x.x.x
```

DNS converts names into IP addresses.

We'll study DNS in detail later.

For now remember:

> DNS translates domain names into IP addresses.

---

# Step 3: Connection Established

Now the browser knows where the server lives.

It creates a connection.

```text
Browser ----------> Server
```

Communication can now begin.

---

# Step 4: Request Sent

The browser sends:

```http
GET /
```

Meaning:

> Give me the homepage.

---

# Step 5: Server Processes the Request

The server:

- Checks the request
- Reads data
- Executes business logic
- Generates a response

Example:

```text
Request Received
        ↓
Read Data
        ↓
Generate Page
```

---

# Step 6: Response Returned

Server sends back:

- HTML
- CSS
- JavaScript
- Images

Example:

```text
Server
   |
HTML
CSS
JS
Images
   |
Browser
```

---

# Step 7: Rendering

The browser converts code into a visual interface.

```text
HTML + CSS + JS
         ↓
      UI
```

You finally see:

> Amazon Homepage

---

# Important Insight

The user sees only:

```text
Page Loaded
```

But internally:

```text
DNS
 ↓
Connection
 ↓
Request
 ↓
Server Processing
 ↓
Database
 ↓
Response
 ↓
Rendering
```

This entire chain often completes within a few hundred milliseconds.

---

# Why System Designers Care

Latency can occur at every stage.

Examples:

### DNS Slow

```text
DNS Lookup
     ↓
Delay
```

### Network Slow

```text
Browser
    ↓
Slow Internet
    ↓
Server
```

### Database Slow

```text
Server
   ↓
Database Query
   ↓
Delay
```

### Server Overloaded

```text
Too Many Requests
       ↓
Slow Processing
```

Users don't know where the issue is.

They only see:

> The website is slow.

A system designer must determine where the delay is occurring.

---

# The Golden Diagram

Memorize this:

```text
Client
   |
Internet
   |
Server
   |
Database
```

Almost every large-scale architecture is an evolved version of this diagram.

---

# Why This Diagram Matters

Everything you'll study later gets inserted somewhere into this flow.

Examples:

```text
Client
   |
CDN
   |
Load Balancer
   |
Server
   |
Cache
   |
Database
   |
Queue
```

Concepts like:

- Load Balancers
- Redis
- Kafka
- CDNs
- Microservices
- Message Queues

all exist to improve some part of this request lifecycle.

---

# Mental Model

Whenever a website or app feels slow, ask:

1. Is DNS slow?
2. Is the network slow?
3. Is the server overloaded?
4. Is the database slow?
5. Is the response too large?
6. Is rendering taking too long?

This is how system designers think.

---

# Key Takeaways

- A client requests services.
- A server provides services.
- Communication happens through requests and responses.
- DNS converts domain names into IP addresses.
- Every request follows a lifecycle before the user sees a page.
- Latency can occur at multiple stages.
- Most advanced architectures are extensions of:

```text
Client
   |
Internet
   |
Server
   |
Database
```

Master this flow first, and every future system design concept will make much more sense.
