# API and Web APIs Guide

This guide explains **APIs**, how they work, types, security, and why they are essential for backend engineers.

---

## Table of Contents

1. [What is an API?](#what-is-an-api)
2. [Meaning of API](#meaning-of-api)
3. [How APIs Work: Client–Server Model](#how-apis-work-client–server-model)
4. [Main Types of APIs](#main-types-of-apis)
5. [REST API in Detail](#rest-api-in-detail)
6. [Statelessness in REST](#statelessness-in-rest)
7. [What is a Web API?](#what-is-a-web-api)
8. [API Integrations](#api-integrations)
9. [Benefits of REST APIs](#benefits-of-rest-apis)
10. [API Types by Access Level](#api-types-by-access-level)
11. [API Endpoints](#api-endpoints)
12. [REST API Security](#rest-api-security)
13. [API Design Process](#api-design-process)
14. [API Testing](#api-testing)
15. [API Documentation](#api-documentation)
16. [How to Use an API](#how-to-use-an-api)
17. [API Gateway](#api-gateway)
18. [GraphQL](#graphql)
19. [REST vs GraphQL](#rest-vs-graphql)
20. [Final Notes for Backend Engineers](#final-notes-for-backend-engineers)

---

## 1. What is an API?

**API (Application Programming Interface)** is a set of rules that allows software systems to communicate.

It defines:

-   available operations
-   request and response formats
-   authentication rules

**Analogy:**  
API is like a **restaurant menu**:

-   Customer (client) chooses
-   Waiter (API) takes order
-   Kitchen (server) prepares result  
    Client never interacts with kitchen directly.

---

## 2. Meaning of API

**Application Programming Interface**:

-   **Application** — any software (server, service, library)
-   **Programming Interface** — clearly defined interaction

An API is a **contract**:  
Systems can change internally as long as the contract is respected.

**API Documentation** describes:

-   endpoints
-   request/response structures
-   errors
-   authentication

---

## 3. How APIs Work: Client–Server Model

Most APIs follow a **client–server architecture**:

-   **Client** — browser, mobile app, or backend service
-   **Server** — processes requests, returns responses

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

## 4. Main Types of APIs

### SOAP API

-   Uses XML
-   Strict and verbose
-   Strong contracts (WSDL)

📌 Mostly in legacy enterprise systems.

---

### RPC API

-   Calls a server function directly
-   Example: `getUserById(42)`

📌 Simple, but tightly coupled.

---

### WebSocket API

-   Persistent, two-way connection
-   Server can push data
-   Use cases: chat, live dashboards, notifications

---

### REST API

-   Built on HTTP
-   Resource-oriented
-   Scalable, cacheable, monitorable

---

## 5. REST API in Detail

**REST (Representational State Transfer)** — an architectural style

### Core HTTP Methods

| Method | Purpose          |
| ------ | ---------------- |
| GET    | Read data        |
| POST   | Create resource  |
| PUT    | Replace resource |
| PATCH  | Partial update   |
| DELETE | Remove resource  |

### Example

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

REST APIs are **stateless**:

-   Server does not store client session
-   Each request contains all info

Example:

```http
Authorization: Bearer <JWT>
```

📌 Benefits: scalable, cacheable, fault-tolerant

---

## 7. What is a Web API?

A **Web API** is an API accessible via **HTTP**.

-   All REST APIs are Web APIs
-   Not all APIs are Web APIs (e.g., Java API)

---

## 8. API Integrations

Allow automatic data exchange between systems:

-   Payment systems (Stripe, PayPal)
-   Authentication (Google Login)
-   Cloud sync
-   Microservices

📌 APIs are the backbone of backend integrations.

---

## 9. Benefits of REST APIs

1. **Integration** — connect new apps without rewriting
2. **Innovation** — backend changes without breaking clients
3. **Scalability** — one API serves web, mobile, partners
4. **Maintainability** — stable boundary between systems

---

## 10. API Types by Access Level

-   **Private** — internal
-   **Public** — external developers
-   **Partner** — restricted
-   **Composite** — combines multiple APIs

---

## 11. API Endpoints

An **endpoint** is a specific API address:

```text
POST /api/v1/users
```

Endpoints matter:

-   Attack targets
-   Potential bottlenecks

---

## 12. REST API Security

### Authentication Tokens

-   JWT, OAuth2
-   Identify and authorize users

```http
Authorization: Bearer <token>
```

### API Keys

-   Identify the calling app
-   Useful for rate limiting and analytics
-   Less secure than tokens

📌 Often used for public APIs.

---

## 13. API Design Process

1. **Planning** — OpenAPI, use cases
2. **Development** — prototypes, iterations
3. **Testing** — correctness, performance, security
4. **Documentation**
5. **Publishing and Versioning**

---

## 14. API Testing

Focuses on server responses:

-   Correctness
-   Error handling
-   Performance under load
-   Security

📌 Automated testing is critical.

---

## 15. API Documentation

Good documentation:

-   Clear language
-   Examples
-   Up-to-date
-   Real use cases

---

## 16. How to Use an API

1. Register and get a token/key
2. Read documentation
3. Test requests
4. Integrate into code

---

## 17. API Gateway

A **single entry point** for multiple APIs:

-   Authentication
-   Rate limiting
-   Logging/monitoring
-   Version management

Example: Amazon API Gateway

---

## 18. GraphQL

Query language for APIs:

-   Clients request only needed fields
-   Single endpoint
-   Efficient for complex graphs

Example:

```graphql
query {
	user(id: 42) {
		name
		email
	}
}
```

---

## 19. REST vs GraphQL

| REST                | GraphQL                  |
| ------------------- | ------------------------ |
| Multiple endpoints  | Single endpoint          |
| Fixed responses     | Client-defined responses |
| Simple and explicit | Flexible and powerful    |

---

## 20. Final Notes for Backend Engineers

APIs are the foundation of backend systems.
A good backend engineer:

-   Designs clear APIs
-   Writes documentation
-   Ensures security
-   Thinks about scalability

REST is mandatory; GraphQL is a valuable next step.
