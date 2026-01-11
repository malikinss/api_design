# Path Variables vs Query Parameters in HTTP Requests (Python)

This guide explains **path variables** and **query parameters**, their differences, and how to use them in RESTful APIs using Python.

---

## Table of Contents

1. [What Are Path Variables and Query Parameters?](#what-are-path-variables-and-query-parameters)
2. [Why They Matter in REST APIs](#why-they-matter-in-rest-apis)
3. [Path Variables](#path-variables)
4. [Query Parameters](#query-parameters)
5. [When to Use Path Variables vs Query Parameters](#when-to-use-path-variables-vs-query-parameters)
6. [Examples in Python](#examples-in-python)
7. [Best Practices](#best-practices)
8. [Summary](#summary)

---

## What Are Path Variables and Query Parameters?

Both **path variables** and **query parameters** are ways to pass data to the server via a URL.

-   **Path variables**: part of the URL path, used to identify a specific resource.  
    Example: `/users/{user_id}`

-   **Query parameters**: appended at the end of a URL after a question mark `?`. Used to filter or modify results.  
    Example: `/users?role=admin&status=active`

---

## Why They Matter in REST APIs

In RESTful APIs:

-   **Path variables** identify **specific resources**.
-   **Query parameters** filter, sort, or paginate **collections of resources**.

Choosing the right type improves **API clarity, usability, and scalability**.

---

## Path Variables

### Definition

A **path variable** is part of the URL used to uniquely identify a resource.

-   Typically used with **GET, PUT, PATCH, DELETE** requests.
-   Always required to locate the specific resource.

### Python Example (FastAPI)

```python
from fastapi import FastAPI

app = FastAPI()

# Retrieve a user by ID
@app.get("/users/{user_id}")
def get_user(user_id: int):
    return {"user_id": user_id, "name": "Alice"}
```

**Usage:**

```
GET /users/42
Response: {"user_id": 42, "name": "Alice"}
```

---

## Query Parameters

### Definition

A **query parameter** is used to filter, sort, or paginate resources in a collection.

-   Appended to the URL after `?`.
-   Multiple parameters separated by `&`.
-   Optional in most cases.

### Python Example (FastAPI)

```python
from typing import Optional

@app.get("/users")
def get_users(role: Optional[str] = None, status: Optional[str] = None):
    # Example filter logic
    users = [
        {"id": 1, "name": "Alice", "role": "admin", "status": "active"},
        {"id": 2, "name": "Bob", "role": "user", "status": "inactive"}
    ]
    if role:
        users = [u for u in users if u["role"] == role]
    if status:
        users = [u for u in users if u["status"] == status]
    return users
```

**Usage:**

```
GET /users?role=admin&status=active
Response: [{"id": 1, "name": "Alice", "role": "admin", "status": "active"}]
```

---

## When to Use Path Variables vs Query Parameters

| Use Case                       | Path Variable | Query Parameter    |
| ------------------------------ | ------------- | ------------------ |
| Identify a **single resource** | ✅            | ❌                 |
| Filter or search a collection  | ❌            | ✅                 |
| Pagination / sorting           | ❌            | ✅                 |
| Optional parameters            | ❌            | ✅                 |
| RESTful API clarity            | ✅            | ✅ (for filtering) |

**Rule of thumb**:

-   **Path variable** → unique resource (`/products/{product_id}`)
-   **Query parameter** → filter, sort, paginate (`/products?color=red&size=XL`)

---

## Examples in Python

### Path Variable Example

Retrieve a single product:

```python
@app.get("/products/{product_id}")
def get_product(product_id: int):
    return {"product_id": product_id, "name": "Laptop"}
```

**Request:**

```
GET /products/123
```

**Response:**

```json
{ "product_id": 123, "name": "Laptop" }
```

### Query Parameter Example

Filter products by color:

```python
@app.get("/products")
def get_products(color: Optional[str] = None):
    products = [
        {"id": 1, "name": "Laptop", "color": "silver"},
        {"id": 2, "name": "Mouse", "color": "yellow"},
        {"id": 3, "name": "Keyboard", "color": "yellow"}
    ]
    if color:
        products = [p for p in products if p["color"] == color]
    return products
```

**Request:**

```
GET /products?color=yellow
```

**Response:**

```json
[
	{ "id": 2, "name": "Mouse", "color": "yellow" },
	{ "id": 3, "name": "Keyboard", "color": "yellow" }
]
```

---

## Best Practices

1. Use **path variables** for unique identifiers of resources.
2. Use **query parameters** for filtering, sorting, pagination, or optional attributes.
3. Keep URLs **clean and intuitive**.
4. Avoid overloading path variables with optional data.
5. Clearly **document all variables and parameters** in your API docs.

---

## Summary

-   **Path variables** identify a **specific resource**.
-   **Query parameters** filter or manipulate **collections of resources**.
-   Correct usage ensures **RESTful, readable, and maintainable APIs** in Python.
