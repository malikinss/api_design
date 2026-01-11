# HTTP Response Status Codes

This guide explains **HTTP response status codes**, their meaning, categories, and best practices for backend engineers.

---

## Table of Contents

1. [What Are HTTP Status Codes?](#what-are-http-status-codes)
2. [Informational Responses (100–199)](#informational-responses-100–199)
3. [Successful Responses (200–299)](#successful-responses-200–299)
4. [Redirection Responses (300–399)](#redirection-responses-300–399)
5. [Client Error Responses (400–499)](#client-error-responses-400–499)
6. [Server Error Responses (500–599)](#server-error-responses-500–599)
7. [Best Practices for Backend Engineers](#best-practices-for-backend-engineers)

---

## What Are HTTP Status Codes?

**HTTP status codes** are **3-digit numbers** returned by the server to indicate the result of an HTTP request.

They help the client understand whether:

-   the request succeeded
-   it failed
-   it was redirected
-   further action is needed

Status codes are grouped into **5 categories**:

1. Informational (1xx)
2. Successful (2xx)
3. Redirection (3xx)
4. Client Errors (4xx)
5. Server Errors (5xx)

---

## Informational Responses (100–199)

These codes indicate that the request was received and is being processed.

| Code | Name                | Description                                       |
| ---- | ------------------- | ------------------------------------------------- |
| 100  | Continue            | Client can continue sending request body          |
| 101  | Switching Protocols | Server switches protocol (e.g., HTTP → WebSocket) |
| 102  | Processing          | WebDAV: request received but not completed        |
| 103  | Early Hints         | Preload resources before final response           |

**Example:** WebSocket handshake uses `101 Switching Protocols`.

---

## Successful Responses (200–299)

Indicate that the request **was successfully received and processed**.

| Code | Name            | When to Use                             |
| ---- | --------------- | --------------------------------------- |
| 200  | OK              | Standard success for GET/PUT/PATCH      |
| 201  | Created         | Resource successfully created (POST)    |
| 202  | Accepted        | Request accepted but not yet processed  |
| 204  | No Content      | Success but no body to return           |
| 206  | Partial Content | Range requests (streaming files/videos) |

**Examples:**

-   `GET /users/42 → 200 OK`
-   `POST /users → 201 Created`
-   `DELETE /users/42 → 204 No Content`

---

## Redirection Responses (300–399)

Used when the resource **has moved** or **another location should be used**.

| Code | Name               | Description                          |
| ---- | ------------------ | ------------------------------------ |
| 301  | Moved Permanently  | Permanent redirect (SEO friendly)    |
| 302  | Found              | Temporary redirect                   |
| 303  | See Other          | Redirect using GET                   |
| 304  | Not Modified       | Resource unchanged (used in caching) |
| 307  | Temporary Redirect | Temporary redirect preserving method |
| 308  | Permanent Redirect | Permanent redirect preserving method |

**Example (cache):**

```http
GET /logo.png
If-None-Match: "abc123"

→ 304 Not Modified
```

---

## Client Error Responses (400–499)

Errors caused by **incorrect requests from the client**.

| Code | Name                 | Typical Use                       |
| ---- | -------------------- | --------------------------------- |
| 400  | Bad Request          | Invalid JSON, missing fields      |
| 401  | Unauthorized         | Missing or invalid authentication |
| 403  | Forbidden            | Authenticated but access denied   |
| 404  | Not Found            | Resource does not exist           |
| 405  | Method Not Allowed   | Wrong HTTP method                 |
| 409  | Conflict             | Duplicate or conflicting state    |
| 422  | Unprocessable Entity | Validation failed                 |
| 429  | Too Many Requests    | Rate limiting exceeded            |

**Example:**

```http
POST /users
{
  "email": "invalid"
}
→ 422 Unprocessable Entity
```

---

## Server Error Responses (500–599)

Errors caused by **server-side issues**.

| Code | Name                       | Meaning                                |
| ---- | -------------------------- | -------------------------------------- |
| 500  | Internal Server Error      | Generic server failure                 |
| 502  | Bad Gateway                | Upstream service error                 |
| 503  | Service Unavailable        | Server overloaded or under maintenance |
| 504  | Gateway Timeout            | Upstream service timed out             |
| 505  | HTTP Version Not Supported | Client used unsupported HTTP version   |

**Example (microservice architecture):**

```text
API → Auth Service → Database
```

If Auth Service fails:

```http
→ 502 Bad Gateway
```

---

## Best Practices for Backend Engineers

1. Always **return appropriate status codes** for each request.
2. `2xx` → success, `3xx` → redirect, `4xx` → client error, `5xx` → server error.
3. Log **unusual 4xx/5xx codes** for debugging.
4. Use **422** for validation errors instead of generic 400.
5. Use `304 Not Modified` to optimize caching and reduce bandwidth.
6. Never expose **stack traces** to clients—log internally.
7. Remember common codes:

    ```
    200 OK
    201 Created
    204 No Content
    400 Bad Request
    401 Unauthorized
    403 Forbidden
    404 Not Found
    409 Conflict
    422 Unprocessable Entity
    429 Too Many Requests
    500 Internal Server Error
    503 Service Unavailable
    ```

---

Mastering HTTP status codes helps backend engineers:

-   Debug APIs efficiently
-   Design predictable and professional APIs
-   Handle caching and redirects correctly
-   Maintain scalable and robust backend systems
