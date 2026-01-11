# HTTP Methods (HTTP Verbs)

This article explains **HTTP methods** in a clear, practical way for a **Backend Engineer**.  
HTTP methods are a core concept behind **REST APIs**, API design, and correct client–server interaction.

---

## Table of Contents

1. [What Are HTTP Methods?](#1-what-are-http-methods)
2. [HTTP and Resources](#2-http-and-resources)
3. [GET](#3-get)
4. [POST](#4-post)
5. [PUT](#5-put)
6. [PATCH](#6-patch)
7. [DELETE](#7-delete)
8. [Safe vs Idempotent Methods](#8-safe-vs-idempotent-methods)
9. [Common Backend Mistakes](#9-common-backend-mistakes)
10. [Summary Table](#10-summary-table)
11. [Key Takeaways for Backend Engineers](#11-key-takeaways-for-backend-engineers)

---

## 1. What Are HTTP Methods?

**HTTP methods (also called HTTP verbs)** define **what action** the client wants to perform on a server resource.

Every HTTP request **must** include a method.

HTTP follows a **request–response model**:

1. Client sends a request (with method)
2. Server processes it
3. Server sends a response (data or error)

HTTP is **stateless**:

-   each request is independent
-   server does not remember previous requests
-   all required data must be sent every time

REST APIs are built on this model and organize interactions around **resources**.

---

## 2. HTTP and Resources

A **resource** is any object accessible via HTTP:

-   user
-   product
-   order
-   file

Each resource is identified by a **URL**.

Examples:

```text
/products
/products/123
/users/42/orders
```

HTTP methods define **what you do** with these resources.

---

## 3. GET

### Purpose

Retrieve data from the server.

### Key Properties

-   Does **not** modify server state
-   Request body is usually empty
-   Can be cached
-   Can be repeated safely

### Example

```http
GET /products HTTP/1.1
Host: api.example.com
```

### Typical Behavior

-   `/products` → list of products
-   `/products/123` → product with ID 123

### Backend Notes

-   Must never create, update, or delete data
-   Ideal for read-only operations

**Safe**: ✅
**Idempotent**: ✅

---

## 4. POST

### Purpose

Create a new resource or trigger a server-side action.

### Key Properties

-   Sends data in request body
-   Usually changes server state
-   Cannot be safely repeated

### Example

```http
POST /products HTTP/1.1
Content-Type: application/json

{
  "name": "Sneakers",
  "color": "blue",
  "price": 59.95
}
```

### Typical Behavior

-   Creates a new product
-   Returns `201 Created`

### Backend Notes

-   Multiple identical POST requests usually create multiple resources
-   Often used for:

    -   creation
    -   login
    -   complex operations

**Safe**: ❌
**Idempotent**: ❌

---

## 5. PUT

### Purpose

Replace an **entire resource** with new data.

### Key Properties

-   Requires full resource representation
-   Overwrites existing data
-   Same request → same result

### Example

```http
PUT /products/123 HTTP/1.1
Content-Type: application/json

{
  "name": "Sneakers",
  "color": "red",
  "price": 49.95
}
```

### Backend Notes

-   Missing fields may be deleted
-   Should be used carefully
-   Best for full updates

**Safe**: ❌
**Idempotent**: ✅

---

## 6. PATCH

### Purpose

Update **part of a resource**.

### Key Properties

-   Sends only changed fields
-   Less destructive than PUT
-   Idempotency depends on implementation

### Example

```http
PATCH /products/123 HTTP/1.1
Content-Type: application/json

{
  "price": 45.95
}
```

### Backend Notes

-   Most commonly used update method
-   Easier to evolve APIs
-   Must handle partial updates correctly

**Safe**: ❌
**Idempotent**: ⚠️ (not guaranteed)

---

## 7. DELETE

### Purpose

Remove a resource from the server.

### Example

```http
DELETE /products/123 HTTP/1.1
Host: api.example.com
```

### Backend Notes

-   Repeating DELETE has no further effect
-   Often returns:

    -   `204 No Content`
    -   or `200 OK`

**Safe**: ❌
**Idempotent**: ✅

---

## 8. Safe vs Idempotent Methods

### Safe Methods

Do **not modify** server state.

Examples:

-   `GET`
-   `HEAD`

Safe ≠ secure
Safe means **no data change**, not access control.

---

### Idempotent Methods

Multiple identical requests result in the **same final state**.

Examples:

-   `GET`
-   `PUT`
-   `DELETE`

Not idempotent:

-   `POST`
-   many `PATCH` implementations

---

## 9. Common Backend Mistakes

❌ Using `GET` to modify data
❌ Using `POST` for updates
❌ Mixing `PUT` and `PATCH` without rules
❌ Ignoring idempotency in distributed systems
❌ Returning wrong status codes

📌 Correct method usage improves:

-   API clarity
-   caching
-   security
-   client expectations

---

## 10. Summary Table

| Method | Purpose          | Body | Safe | Idempotent     |
| ------ | ---------------- | ---- | ---- | -------------- |
| GET    | Read data        | No   | Yes  | Yes            |
| POST   | Create resource  | Yes  | No   | No             |
| PUT    | Replace resource | Yes  | No   | Yes            |
| PATCH  | Partial update   | Yes  | No   | Not guaranteed |
| DELETE | Remove resource  | No   | No   | Yes            |

---

## 11. Key Takeaways for Backend Engineers

-   HTTP methods define **intent**
-   REST APIs depend on correct method usage
-   Safe and idempotent methods enable:

    -   retries
    -   caching
    -   scalability

-   Choose:

    -   `GET` → read
    -   `POST` → create / actions
    -   `PUT` → full replace
    -   `PATCH` → partial update
    -   `DELETE` → removal

Understanding HTTP methods is **mandatory** for building reliable backend systems.
