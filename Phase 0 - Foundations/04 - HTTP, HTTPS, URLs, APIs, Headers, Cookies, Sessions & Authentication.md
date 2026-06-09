# Class 4 — HTTP, HTTPS, URLs, APIs, Headers, Cookies, Sessions & Authentication

This class is the foundation of modern web systems.

If you understand this deeply, APIs, microservices, gateways, load balancers, and backend development become much easier.

---

# Part 1 — What Is HTTP?

**HTTP** stands for:

> HyperText Transfer Protocol

Ignore the scary name.

Think of HTTP as:

> A language that clients and servers use to communicate.

### Example

```text
Browser ---> Server
"Give me homepage"
```

The server understands this because both speak HTTP.

---

## Real Example

You open:

```text
https://amazon.com
```

Your browser sends an HTTP request.

Server responds with an HTTP response.

---

## Request–Response Model

```text
Client
   |
HTTP Request
   |
Server
   |
HTTP Response
   |
Client
```

This is one of the most important diagrams in software engineering.

---

# Part 2 — URL

Consider:

```text
https://amazon.com/products/123
```

Break it into pieces.

## Protocol

```text
https
```

Defines how communication happens.

---

## Domain

```text
amazon.com
```

Specifies which server to contact.

---

## Path

```text
/products/123
```

Specifies which resource is requested.

---

### Another Example

```text
https://youtube.com/watch?v=abc
```

#### Domain

```text
youtube.com
```

#### Path

```text
/watch
```

#### Query Parameter

```text
v=abc
```

---

# Part 3 — HTTP Methods

Methods tell the server what action you want.

---

## GET

Used to read data.

### Example

```http
GET /users/123
```

Meaning:

> Give me user 123

---

## POST

Used to create data.

### Example

```http
POST /users
```

Meaning:

> Create a new user

---

## PUT

Used to replace an entire object.

### Example

```http
PUT /users/123
```

Meaning:

> Replace all user data

---

## PATCH

Used to update some fields.

### Example

```http
PATCH /users/123
```

Meaning:

> Update specific fields only

---

## DELETE

Used to remove data.

### Example

```http
DELETE /users/123
```

Meaning:

> Delete user 123

---

## Common Interview Questions

### Which method should be used to fetch product details?

Answer:

```text
GET
```

### Which method should be used to create a new order?

Answer:

```text
POST
```

---

# Part 4 — HTTP Request Structure

Example:

```http
GET /products/123 HTTP/1.1
Host: amazon.com
User-Agent: Chrome
Authorization: Bearer xyz
```

Contains:

## Request Line

```http
GET /products/123 HTTP/1.1
```

---

## Headers

Examples:

```http
Host: amazon.com
User-Agent: Chrome
Authorization: Bearer xyz
```

Headers contain metadata about the request.

---

# Part 5 — HTTP Response Structure

Example:

```http
HTTP/1.1 200 OK

{
  "name": "iPhone"
}
```

Contains:

## Status Code

```text
200
```

---

## Headers

Metadata about the response.

---

## Body

Actual data returned to the client.

---

# Part 6 — Status Codes

You should know these by heart.

---

## 200 OK

Request succeeded.

```http
200 OK
```

---

## 201 Created

New resource created.

```http
201 Created
```

---

## 400 Bad Request

Client sent an invalid request.

```http
400 Bad Request
```

---

## 401 Unauthorized

User is not authenticated.

```http
401 Unauthorized
```

---

## 403 Forbidden

User is authenticated but lacks permission.

```http
403 Forbidden
```

---

## 404 Not Found

Requested resource does not exist.

```http
404 Not Found
```

---

## 500 Internal Server Error

Something failed on the server.

```http
500 Internal Server Error
```

---

# Part 7 — What Is an API?

**API** stands for:

> Application Programming Interface

Ignore the fancy name.

Think:

> An API is a contract through which software talks to software.

---

## Example

The Instagram app needs posts.

It calls:

```http
GET /posts
```

Server returns posts.

That endpoint is an API.

---

## Example APIs

```http
GET /users
GET /posts
POST /orders
DELETE /comments
```

---

# Part 8 — HTTP Is Stateless

Very important concept.

Suppose:

### Request 1

```text
Login
```

### Request 2

```text
Show Profile
```

HTTP itself does not remember previous requests.

Every request is independent.

This property is called:

> Statelessness

---

## Problem

How does the server know you're logged in?

Answer:

- Cookies
- Sessions
- Tokens

---

# Part 9 — Cookies

A **cookie** is small data stored in the browser.

After login:

Server sends:

```http
Set-Cookie: session_id=123
```

Browser stores it.

Future requests include:

```http
Cookie: session_id=123
```

Now the server knows who you are.

---

# Part 10 — Sessions

The server stores user state.

Example:

```text
Session ID: 123
User: Rahul
Logged In: Yes
Role: Student
```

Stored on the server.

Browser only stores:

```text
session_id=123
```

---

## Session Flow

```text
Login
   |
Server Creates Session
   |
Session ID Returned
   |
Browser Stores Cookie
   |
Future Requests Include Cookie
```

---

# Part 11 — Token Authentication

Modern systems often use tokens.

After login:

Server returns:

```text
JWT Token
```

Example:

```text
abc.xyz.def
```

Browser stores the token.

Future requests include:

```http
Authorization: Bearer abc.xyz.def
```

Server verifies the token.

---

## Advantages of Tokens

- Scales well
- Stateless
- Works across microservices
- Common in modern architectures

---

# Session vs JWT

| Feature | Session | JWT |
|----------|----------|----------|
| State Stored | Server | Token |
| Scalability | Lower | Higher |
| Server Memory Needed | Yes | No |
| Easy to Revoke | Yes | Harder |
| Stateless | No | Yes |

---

## Session

### Pros

- Easy to invalidate
- Simple to understand

### Cons

- Requires server memory
- Harder to scale

---

## JWT

### Pros

- Highly scalable
- Stateless

### Cons

- Harder to revoke immediately
- Token expiration must be managed carefully

---

# Part 12 — HTTP vs HTTPS

---

## HTTP

Traffic is sent in plain text.

```text
Client ---- Server
Readable
```

Anyone intercepting traffic may be able to read it.

---

## HTTPS

Traffic is encrypted.

```text
Client ---- Server
Encrypted
```

Data remains secure during transmission.

---

## HTTPS Is Used By

- Banks
- Shopping Sites
- Social Media Platforms
- SaaS Products
- Nearly every modern website

---

# Complete Login Flow

```text
User Enters Username & Password
              |
              v
Client Sends POST /login
              |
              v
Server Verifies Credentials
              |
              v
Server Returns Session or JWT
              |
              v
Browser Stores It
              |
              v
Future Requests Include Identity
```

This exact flow powers countless systems including Google, Amazon, Netflix, and Meta products.

---

# Mental Model

Whenever you use an app:

```text
Client
   |
HTTP/HTTPS
   |
API
   |
Server
   |
Database
```

The client sends requests.

The server processes them.

Authentication identifies the user.

Responses return data.

This cycle repeats thousands of times every day for every active user.

---

# Key Takeaways

- HTTP is the communication protocol between clients and servers.
- URLs identify resources.
- HTTP methods define actions.
- APIs allow software to communicate.
- Headers carry metadata.
- Status codes communicate results.
- HTTP is stateless.
- Cookies and sessions maintain user identity.
- JWT tokens enable scalable authentication.
- HTTPS encrypts communication and keeps data secure.

Master these concepts before moving to load balancers, caching, databases, and microservices.
