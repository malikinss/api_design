# CORS (Cross-Origin Resource Sharing)

This guide explains **CORS (Cross-Origin Resource Sharing)**, its purpose, how it works, and best practices for implementation.

---

## Table of Contents

1. [What is CORS?](#what-is-cors)
2. [Why is CORS Important?](#why-is-cors-important)
3. [Same-Origin Policy](#same-origin-policy)
4. [How CORS Works](#how-cors-works)
5. [CORS Request Example](#cors-request-example)
6. [Preflight Requests](#preflight-requests)
7. [Complex Requests](#complex-requests)
8. [CORS vs JSONP](#cors-vs-jsonp)
9. [CORS Best Practices](#cors-best-practices)

---

## What is CORS?

**Cross-Origin Resource Sharing (CORS)** is a mechanism that allows web applications running in one domain to access resources from another domain.

CORS is essential because modern web applications often rely on **third-party APIs** or resources, such as:

-   Video content from media APIs
-   Fonts from public libraries
-   Weather or other external datasets

CORS allows the browser to check if a cross-origin request is authorized before sending data to the client application.

---

## Why is CORS Important?

Without CORS, browsers restrict cross-origin requests to prevent **Cross-Site Request Forgery (CSRF)** attacks.

**Example:**

1. A user logs into their bank at `bank.com`.
2. The user opens a malicious website in another tab.
3. The malicious site could attempt to use the user’s credentials to perform unauthorized actions on `bank.com`.

CORS provides a secure way to allow **authorized cross-origin requests** without exposing sensitive credentials.

---

## Same-Origin Policy

The **same-origin policy** restricts requests to the same origin:

-   **Origin** = protocol + host + port
-   Requests to different protocols, hosts, or ports are considered cross-origin.

**Examples (origin: `http://store.aws.com/dir/page.html`):**

| URL                                     | Same origin? | Reason            |
| --------------------------------------- | ------------ | ----------------- |
| `http://store.aws.com/dir2/new.html`    | ✅ Yes       | Only path differs |
| `https://store.aws.com/page.html`       | ❌ No        | Protocol differs  |
| `http://store.aws.com:81/dir/page.html` | ❌ No        | Port differs      |
| `http://news.aws.com/dir/page.html`     | ❌ No        | Host differs      |

CORS extends the same-origin policy by allowing controlled access to **authorized external domains**.

---

## How CORS Works

1. Browser adds an **Origin header** to the request.
2. Server checks the origin and responds with **Access-Control-Allow-Origin**.
3. Browser receives headers and decides whether to allow the response.

If the server doesn’t allow the origin, the browser blocks the request.

---

## CORS Request Example

**Scenario:** `https://news.example.com` wants access to `https://partner-api.com`.

**Server setup:**

```http
Access-Control-Allow-Origin: https://news.example.com
Access-Control-Allow-Credentials: true
```

-   Server explicitly authorizes the origin.
-   Browser allows the request and response.

> For multiple origins, a comma-separated list or wildcard `*` can be used (for public APIs).

---

## Preflight Requests

Some cross-origin requests are considered **complex** and require a **preflight request**:

-   Methods other than GET, POST, HEAD
-   Custom headers other than Accept-Language, Accept, Content-Language
-   Content-Type other than `multipart/form-data`, `application/x-www-form-urlencoded`, or `text/plain`

**Preflight request example (OPTIONS method):**

```http
OPTIONS /data HTTP/1.1
Origin: https://example.com
Access-Control-Request-Method: DELETE
```

**Preflight response example:**

```http
HTTP/1.1 200 OK
Access-Control-Allow-Headers: Content-Type
Access-Control-Allow-Origin: https://news.example.com
Access-Control-Allow-Methods: GET, DELETE, HEAD, OPTIONS
Access-Control-Max-Age: 86400
```

-   `Access-Control-Max-Age` specifies how long the browser can cache the preflight response.

---

## Complex Requests

Complex requests include:

-   DELETE, PUT, PATCH methods
-   Custom headers
-   Non-simple Content-Types

Browsers automatically send preflight OPTIONS requests to verify authorization.

---

## CORS vs JSONP

**JSONP** is an older technique for cross-origin requests:

-   Uses `<script>` tags to load JSON data from other domains.
-   Bypasses same-origin policy.
-   Only supports JSON format.
-   Less secure than CORS; depends on trusting the third-party domain.

**CORS** is the modern standard:

-   Secure
-   Works with any response type
-   Browser-enforced

---

## CORS Best Practices

1. **Specify exact allowed origins** instead of wildcards `*`.
2. **Avoid including `null` origin** in allowed list (can create vulnerabilities).
3. **Use Access-Control-Allow-Credentials** carefully.
4. **Set proper headers for complex requests**:

    - `Access-Control-Allow-Methods`
    - `Access-Control-Allow-Headers`
    - `Access-Control-Allow-Origin`

5. **Cache preflight responses** using `Access-Control-Max-Age` to reduce network overhead.
