# HTTP (Hypertext Transfer Protocol)

This guide explains **HTTP**, its structure, usage, and why it is essential for backend engineers.

---

## Table of Contents

1. [What is HTTP?](#what-is-http)
2. [HTTP in the Backend World](#http-in-the-backend-world)
3. [HTTP Requests](#http-requests)
4. [HTTP Methods (Verbs)](#http-methods-verbs)
5. [HTTP Request Headers](#http-request-headers)
6. [HTTP Request Body](#http-request-body)
7. [HTTP Responses](#http-responses)
8. [HTTP Status Codes](#http-status-codes)
9. [HTTP Response Headers](#http-response-headers)
10. [HTTP Response Body](#http-response-body)
11. [Stateless Nature of HTTP](#stateless-nature-of-http)
12. [HTTP Versions and Connections](#http-versions-and-connections)
13. [HTTP and Security](#http-and-security)
14. [Why HTTP Matters for Backend Engineers](#why-http-matters-for-backend-engineers)
15. [Final Takeaways](#final-takeaways)

---

## 1. What is HTTP?

**HTTP (Hypertext Transfer Protocol)** is the foundational protocol of the World Wide Web.  
It defines how **clients** (browsers, apps) and **servers** communicate and exchange data.

**Key points:**

-   HTTP is an **application-layer protocol**
-   Relies on **TCP/IP** to deliver data
-   Follows a **request–response** model

**Basic Flow:**

1. Client sends an HTTP request
2. Server processes the request
3. Server sends back an HTTP response

This cycle is the backbone of how the web works.

---

## 2. HTTP in the Backend World

Why HTTP matters for backend engineers:

-   REST APIs are built on HTTP
-   Almost all web services communicate via HTTP
-   Understanding HTTP helps debug APIs, performance issues, and security problems

Every API call you write is ultimately an HTTP request.

---

## 3. HTTP Requests

An **HTTP request** is how a client asks a server for data or requests an action.

### Request Components:

-   **HTTP version**
-   **URL**
-   **HTTP method**
-   **Request headers**
-   **Optional body**

### Example Request:

```http
POST /login HTTP/1.1
Host: api.example.com
Content-Type: application/json
User-Agent: Mozilla/5.0

{
  "username": "sam",
  "password": "secret"
}
```

---

## 4. HTTP Methods (Verbs)

HTTP methods define what action the client wants the server to perform.

| Method | Purpose       | Typical Use        |
| ------ | ------------- | ------------------ |
| GET    | Retrieve data | Fetch users, pages |
| POST   | Send data     | Create a resource  |
| PUT    | Replace data  | Full update        |
| PATCH  | Modify data   | Partial update     |
| DELETE | Remove data   | Delete a resource  |

**Backend Notes:**

-   GET should not change server state
-   POST, PUT, PATCH, DELETE usually modify data
-   Correct method usage is essential for REST APIs

---

## 5. HTTP Request Headers

**Headers** are key–value pairs providing metadata about the request.

**Purpose:**

-   Identify client
-   Specify content type
-   Define acceptable response types
-   Include authentication credentials

### Common Request Headers:

```http
Content-Type: application/json
Authorization: Bearer <token>
User-Agent: Chrome/120
Accept: application/json
```

**Usage:** authentication, caching, content negotiation, debugging

---

## 6. HTTP Request Body

The **body** contains data sent to the server.

-   Used with POST, PUT, PATCH
-   GET requests usually **do not** have a body

### Example:

```json
{
	"email": "sam@example.com",
	"password": "123456"
}
```

---

## 7. HTTP Responses

An **HTTP response** is what the server sends back after processing a request.

### Response Components:

-   HTTP status code
-   Response headers
-   Optional body

### Example Response:

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 52

{
  "id": 42,
  "name": "Sam",
  "email": "sam@example.com"
}
```

---

## 8. HTTP Status Codes

**Status codes** indicate the result of a request.

| Range | Meaning       |
| ----- | ------------- |
| 1xx   | Informational |
| 2xx   | Success       |
| 3xx   | Redirection   |
| 4xx   | Client Error  |
| 5xx   | Server Error  |

### Common Codes for Backend Engineers

**Success (2xx)**

-   200 OK — request succeeded
-   201 Created — resource created
-   204 No Content — success without body

**Client Errors (4xx)**

-   400 Bad Request — invalid input
-   401 Unauthorized — not authenticated
-   403 Forbidden — no permission
-   404 Not Found — resource missing

**Server Errors (5xx)**

-   500 Internal Server Error — generic server failure
-   502 Bad Gateway — upstream error
-   503 Service Unavailable — overloaded or down

---

## 9. HTTP Response Headers

Response headers provide metadata about the returned data.

### Common Response Headers:

```http
Content-Type: application/json
Content-Language: en
Cache-Control: no-cache
```

They inform the client:

-   How to parse the body
-   Caching behavior
-   Encoding and language

---

## 10. HTTP Response Body

The **body** contains the requested data.

**Examples:**

-   HTML (web pages)
-   JSON (APIs)
-   XML
-   Files (images, PDFs)

### Example JSON Response:

```json
{
	"message": "Login successful"
}
```

---

## 11. Stateless Nature of HTTP

HTTP is **stateless**:

-   Each request is independent
-   Server does not remember previous requests
-   Authentication data must be sent every time

📌 Sessions, cookies, and tokens are workarounds built on top of HTTP.

---

## 12. HTTP Versions and Connections

**HTTP/1.0:** one TCP connection per request
**HTTP/1.1+:** persistent connections, multiple requests per TCP connection, better performance

---

## 13. HTTP and Security

Because HTTP is stateless:

-   Attackers can send massive amounts of requests
-   Servers must handle each request individually

**Backend concerns:**

-   Rate limiting
-   Authentication
-   API gateways
-   Caching

**HTTP-based attacks:** Layer 7 (Application Layer) attacks targeting backend logic

---

## 14. Why HTTP Matters for Backend Engineers

Understanding HTTP helps you:

-   Design better REST APIs
-   Debug client–server issues
-   Choose correct status codes
-   Secure your application
-   Optimize performance and scalability

---

## 15. Final Takeaways

-   HTTP is the foundation of web communication
-   REST APIs rely on HTTP
-   Requests and responses follow strict structures
-   Status codes and headers are crucial
-   Statelessness enables scalability but requires careful design

Mastering HTTP is a **mandatory skill** for every backend engineer.
