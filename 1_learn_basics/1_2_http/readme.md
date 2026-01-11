# HTTP (Hypertext Transfer Protocol)

---

## 1. What Is HTTP?

**HTTP (Hypertext Transfer Protocol)** is the foundational protocol of the World Wide Web.  
It defines how **clients** and **servers** communicate and exchange data over the internet.

HTTP is an **application-layer protocol**, meaning it operates at a high level of the network stack and relies on lower-level protocols (like TCP/IP) to deliver data.

### Basic idea

-   A **client** (usually a browser or an app) sends an HTTP request
-   A **server** processes the request
-   The server sends back an HTTP response

This request–response cycle is the core of how the web works.

---

## 2. HTTP in the Backend World

For a backend engineer, HTTP is critical because:

-   REST APIs are built on top of HTTP
-   Almost all web services communicate via HTTP
-   Understanding HTTP helps debug APIs, performance issues, and security problems

Every API call you write or consume is ultimately an HTTP request.

---

## 3. What Is an HTTP Request?

An **HTTP request** is how a client asks a server for data or requests an action.

Each request contains **encoded information** that tells the server:

-   what resource is needed
-   what action to perform
-   who is making the request
-   how to interpret the data

### Typical HTTP Request Structure

An HTTP request consists of:

1. HTTP version
2. URL
3. HTTP method
4. HTTP request headers
5. Optional HTTP body

---

## 4. HTTP Request Example

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

## 5. HTTP Methods (Verbs)

An **HTTP method** defines the action the client wants the server to perform.

### Common HTTP Methods

| Method | Purpose       | Typical Use        |
| ------ | ------------- | ------------------ |
| GET    | Retrieve data | Fetch users, pages |
| POST   | Send data     | Create a resource  |
| PUT    | Replace data  | Full update        |
| PATCH  | Modify data   | Partial update     |
| DELETE | Remove data   | Delete a resource  |

### Backend Perspective

-   **GET** should not change server state
-   **POST / PUT / PATCH / DELETE** usually modify data
-   Correct method usage is essential for RESTful APIs

---

## 6. HTTP Request Headers

**Headers** are key–value pairs that provide metadata about the request.

They tell the server:

-   who is making the request
-   what format the data is in
-   what response formats are acceptable
-   authentication details

### Common Request Headers

```http
Content-Type: application/json
Authorization: Bearer <token>
User-Agent: Chrome/120
Accept: application/json
```

📌 Headers are heavily used in:

-   authentication
-   content negotiation
-   caching
-   debugging

---

## 7. HTTP Request Body

The **request body** contains the actual data being sent to the server.

It is commonly used with:

-   POST
-   PUT
-   PATCH

### Example Request Body

```json
{
	"email": "sam@example.com",
	"password": "123456"
}
```

📌 GET requests usually **do not** have a body.

---

## 8. What Is an HTTP Response?

An **HTTP response** is what the server sends back after processing a request.

### Typical HTTP Response Structure

1. HTTP status code
2. HTTP response headers
3. Optional HTTP body

---

## 9. HTTP Response Example

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

## 10. HTTP Status Codes

HTTP status codes are **3-digit numbers** indicating the result of a request.

### Status Code Categories

| Range | Meaning       |
| ----- | ------------- |
| 1xx   | Informational |
| 2xx   | Success       |
| 3xx   | Redirection   |
| 4xx   | Client Error  |
| 5xx   | Server Error  |

---

### Common Status Codes for Backend Engineers

#### Success (2xx)

-   **200 OK** — request succeeded
-   **201 Created** — resource created
-   **204 No Content** — success without body

#### Client Errors (4xx)

-   **400 Bad Request** — invalid input
-   **401 Unauthorized** — not authenticated
-   **403 Forbidden** — no permission
-   **404 Not Found** — resource missing

#### Server Errors (5xx)

-   **500 Internal Server Error** — generic server failure
-   **502 Bad Gateway** — upstream error
-   **503 Service Unavailable** — overloaded or down

📌 Correct status codes are crucial for API usability.

---

## 11. HTTP Response Headers

Response headers provide metadata about the returned data.

### Common Response Headers

```http
Content-Type: application/json
Content-Language: en
Cache-Control: no-cache
```

They inform the client:

-   how to parse the body
-   how to cache the response
-   encoding and language

---

## 12. HTTP Response Body

The **response body** contains the requested data.

Examples:

-   HTML (for web pages)
-   JSON (for APIs)
-   XML
-   Files (images, PDFs)

### Example JSON Response Body

```json
{
	"message": "Login successful"
}
```

---

## 13. Stateless Nature of HTTP

HTTP is a **stateless protocol**.

This means:

-   each request is independent
-   the server does not remember previous requests
-   authentication data must be sent every time

📌 Sessions, cookies, and tokens are **workarounds** built on top of HTTP.

---

## 14. HTTP Versions and Connections

Originally:

-   one TCP connection per request

Modern HTTP (1.1+):

-   persistent connections
-   multiple requests over one TCP connection
-   better performance and resource usage

---

## 15. HTTP and Security (DoS / DDoS)

Because HTTP is stateless:

-   attackers can send massive amounts of requests
-   servers must process each one independently

### HTTP-based attacks:

-   considered **Layer 7 (Application Layer)** attacks
-   overwhelm backend logic rather than network bandwidth

📌 This is why backend engineers care about:

-   rate limiting
-   authentication
-   API gateways
-   caching

---

## 16. Why HTTP Matters for Backend Engineers

Understanding HTTP helps you:

-   design better REST APIs
-   debug client–server issues
-   choose correct status codes
-   secure your application
-   reason about performance and scalability

---

## Final Takeaways

-   HTTP is the foundation of web communication
-   Everything in REST APIs is built on HTTP
-   Requests and responses follow strict structure
-   Status codes and headers matter
-   Statelessness enables scalability but requires careful design

Mastering HTTP is a **mandatory skill** for every backend engineer.
