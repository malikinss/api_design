# API and Web APIs

## 1. What Is an API?

**API (Application Programming Interface)** is a set of rules that allows different software systems to communicate with each other.

An API defines:

-   what operations are available,
-   how to request them,
-   what data format is expected,
-   what response will be returned.

In backend development, APIs are the **main way services interact** — both internally (between microservices) and externally (with web/mobile clients).

### Real-World Analogy

Think of an API as a **restaurant menu**:

-   the customer (client) chooses from allowed options,
-   the waiter (API) accepts the order,
-   the kitchen (server) prepares the result.

The client never interacts with the kitchen directly.

---

## 2. Meaning of API

**Application Programming Interface**:

-   **Application** — any software system (server, service, library)
-   **Programming Interface** — a clearly defined way to interact with it

An API is a **contract** between two systems.
As long as the contract is respected, each side can change internally without breaking the other.

API documentation describes:

-   available endpoints
-   request structure
-   response structure
-   error formats
-   authentication rules

---

## 3. How APIs Work: Client–Server Model

Most APIs follow a **client–server architecture**.

-   **Client** — sends a request  
    (browser, mobile app, another backend service)
-   **Server** — processes the request and returns a response  
    (backend logic + database)

### Example HTTP Request

```http
GET /users/42 HTTP/1.1
Host: api.example.com
Authorization: Bearer <token>
```

### Example Response

```json
{
	"id": 42,
	"name": "Sam",
	"email": "sam@example.com"
}
```

---

## 4. Main Types of APIs (Architecture-Based)

### SOAP API

-   Uses XML for communication
-   Strict and verbose
-   Strong contracts (WSDL)

📌 Mostly found in legacy enterprise systems (banks, insurance).

---

### RPC API (Remote Procedure Call)

-   Client calls a function on the server
-   Server executes and returns the result

Example:

```text
getUserById(42)
```

📌 Easy to understand, but tightly coupled and less flexible for HTTP-based systems.

---

### WebSocket API

-   Persistent connection
-   Two-way communication
-   Server can push data to clients

📌 Used for:

-   chats
-   real-time notifications
-   live dashboards

---

### REST API

The most common API style in modern backend development.

-   Built on top of HTTP
-   Resource-oriented
-   Scales well
-   Easy to cache and monitor

---

## 5. REST API in Detail

**REST (Representational State Transfer)** is an architectural style, not a protocol.

### Core HTTP Methods

| Method | Purpose                   |
| ------ | ------------------------- |
| GET    | Read data                 |
| POST   | Create a resource         |
| PUT    | Replace a resource        |
| PATCH  | Update part of a resource |
| DELETE | Remove a resource         |

### REST Example

```http
GET /api/v1/orders/1001
```

Response:

```json
{
	"id": 1001,
	"status": "paid",
	"total": 49.99
}
```

---

## 6. Statelessness in REST

A key REST principle is **statelessness**.

This means:

-   the server does not store client session state
-   every request contains all required information

Example:

```http
Authorization: Bearer <JWT>
```

📌 Stateless APIs are:

-   easier to scale
-   easier to cache
-   more fault-tolerant

---

## 7. What Is a Web API?

A **Web API** is an API accessible over the web using HTTP.

Important distinction:

-   All REST APIs are Web APIs
-   Not all APIs are Web APIs (e.g., Java API, OS API)

Today, most backend engineers work primarily with Web APIs.

---

## 8. API Integrations

API integrations allow different systems to **automatically exchange data**.

### Examples:

-   payment systems (Stripe, PayPal)
-   authentication (Google Login)
-   cloud synchronization
-   microservice communication

📌 For backend engineers, APIs are the backbone of integrations.

---

## 9. Benefits of REST APIs

### 1. Integration

New applications can be connected to existing systems without rewriting code.

### 2. Innovation

Changes can be introduced at the API level without affecting clients.

### 3. Scalability

One API can serve:

-   web apps
-   mobile apps
-   partner systems

### 4. Maintainability

API acts as a stable boundary between systems.

---

## 10. API Types by Access Level

-   **Private APIs** — internal use only
-   **Public APIs** — available to external developers
-   **Partner APIs** — restricted to authorized partners
-   **Composite APIs** — combine multiple APIs into one call

---

## 11. API Endpoints

An **endpoint** is a specific API address.

```text
POST /api/v1/users
```

### Why endpoints matter:

-   they are attack targets
-   they can become performance bottlenecks

---

## 12. REST API Security

### Authentication Tokens

-   JWT, OAuth2
-   Identify and authorize users

```http
Authorization: Bearer <token>
```

---

### API Keys

-   Identify the calling application
-   Less secure than tokens
-   Useful for rate limiting and analytics

📌 Often used for public APIs.

---

## 13. API Design Process

1. **Planning**

    - OpenAPI / Swagger
    - use cases and contracts

2. **Development**

    - prototypes and iterations

3. **Testing**

    - correctness, performance, security

4. **Documentation**
5. **Publishing and versioning**

---

## 14. API Testing

API testing focuses on server responses:

-   correctness
-   error handling
-   performance under load
-   security vulnerabilities

📌 Automated tests are critical in backend development.

---

## 15. API Documentation

Good API documentation:

-   uses clear language
-   provides examples
-   stays up-to-date
-   targets beginners and advanced users
-   explains real use cases

---

## 16. How to Use an API

1. Register and obtain an API key or token
2. Read the documentation
3. Make test requests
4. Integrate into your backend or frontend code

---

## 17. API Gateway

An **API Gateway** is a single entry point for multiple APIs.

Responsibilities:

-   authentication
-   rate limiting
-   logging and monitoring
-   version management

Example: **Amazon API Gateway**

---

## 18. GraphQL

**GraphQL** is a query language designed specifically for APIs.

### Key Features:

-   clients request only needed fields
-   single endpoint
-   efficient for complex data graphs

### Example Query

```graphql
query {
	user(id: 42) {
		name
		email
	}
}
```

---

## 19. REST vs GraphQL (Summary)

| REST                | GraphQL                  |
| ------------------- | ------------------------ |
| Multiple endpoints  | Single endpoint          |
| Fixed responses     | Client-defined responses |
| Simple and explicit | Flexible and powerful    |

---

## Final Notes for Backend Engineers

APIs are the foundation of backend systems.
Understanding REST, security, documentation, and testing is mandatory.
GraphQL is a powerful alternative worth learning after mastering REST.

A good backend engineer:

-   designs clear APIs
-   writes documentation
-   ensures security
-   thinks about scalability
