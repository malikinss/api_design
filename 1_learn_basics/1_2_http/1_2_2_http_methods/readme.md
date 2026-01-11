# HTTP Methods

---

## 1. What Are HTTP Methods?

HTTP methods (or **HTTP verbs**) indicate the action a client wants to perform on a resource.  
They are **essential for REST APIs**, as every request must include a method.

HTTP operates on a **request-response model**:

1. **Client** sends a request
2. **Server** responds with data or an error

HTTP is **stateless**, meaning each request is independent. REST APIs leverage this model, organizing interactions around **resources** accessed via unique endpoints.

---

## 2. Common HTTP Methods

HTTP methods correspond to **CRUD operations** (Create, Read, Update, Delete):

### 2.1 GET

-   **Purpose**: Retrieve data from the server
-   **Request body**: Usually empty
-   **Example**:

```http
GET /products HTTP/1.1
Host: example.com
```

-   **Behavior**:

    -   `/products` → returns all products
    -   `/products/123` → returns product with ID 123

-   **Safe and idempotent**: Yes

---

### 2.2 POST

-   **Purpose**: Create a new resource
-   **Request body**: Contains data for the new resource
-   **Example**:

```http
POST /products HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "Sneakers",
  "color": "blue",
  "price": 59.95,
  "currency": "USD"
}
```

-   **Behavior**: Adds a new product to the database
-   **Safe**: No
-   **Idempotent**: No (multiple requests create multiple resources)

---

### 2.3 PUT

-   **Purpose**: Replace an existing resource
-   **Request body**: Complete resource data
-   **Example**:

```http
PUT /products/123 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "Sneakers",
  "color": "red",
  "price": 49.95,
  "currency": "USD"
}
```

-   **Behavior**: Overwrites the existing product
-   **Safe**: No
-   **Idempotent**: Yes

---

### 2.4 PATCH

-   **Purpose**: Update specific fields of an existing resource
-   **Request body**: Only the fields to be updated
-   **Example**:

```http
PATCH /products/123 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "price": 45.95
}
```

-   **Behavior**: Updates only the `price` field, leaving other fields unchanged
-   **Safe**: No
-   **Idempotent**: Not guaranteed

---

### 2.5 DELETE

-   **Purpose**: Remove a resource
-   **Example**:

```http
DELETE /products/123 HTTP/1.1
Host: example.com
```

-   **Behavior**: Deletes the product with ID 123
-   **Safe**: No
-   **Idempotent**: Yes

---

## 3. Safe vs Idempotent Methods

### Safe Methods

-   Do **not modify** resources
-   **Examples**: `GET`, `HEAD`

### Idempotent Methods

-   **Same outcome** regardless of how many times executed
-   **Examples**: `GET`, `HEAD`, `PUT`, `DELETE`
-   **Non-idempotent**: `POST`, `PATCH` (depending on behavior)

---

## 4. Summary Table

| Method | Purpose          | Request Body | Safe | Idempotent     |
| ------ | ---------------- | ------------ | ---- | -------------- |
| GET    | Read data        | No           | Yes  | Yes            |
| POST   | Create resource  | Yes          | No   | No             |
| PUT    | Replace resource | Yes          | No   | Yes            |
| PATCH  | Update resource  | Partial      | No   | Not guaranteed |
| DELETE | Remove resource  | No           | No   | Yes            |

---

**Takeaways for Backend Engineers**:

-   Always include an **HTTP method** when interacting with REST APIs.
-   Understand which methods are **safe** and **idempotent** to prevent unexpected behavior.
-   Use **GET** for reading, **POST** for creating, **PUT/PATCH** for updating, and **DELETE** for removal.
