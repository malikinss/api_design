# HTTP Headers

This guide explains **HTTP headers**, their types, purposes, and best practices for backend engineers.

---

## Table of Contents

1. [What Are HTTP Headers?](#what-are-http-headers)
2. [Types of HTTP Headers](#types-of-http-headers)
    - [Request Headers](#request-headers)
    - [Response Headers](#response-headers)
    - [General Headers](#general-headers)
    - [Entity Headers](#entity-headers)
3. [Special Categories of HTTP Headers](#special-categories-of-http-headers)
    - [Security Headers](#security-headers)
    - [Authentication Headers](#authentication-headers)
    - [Caching Headers](#caching-headers)
    - [CORS Headers](#cors-headers)
    - [Proxy Headers](#proxy-headers)
    - [Debugging Headers](#debugging-headers)
    - [Content-Related Headers](#content-related-headers)
4. [Manipulating HTTP Headers](#manipulating-http-headers)
5. [Best Practices for Backend Engineers](#best-practices-for-backend-engineers)

---

## What Are HTTP Headers?

**HTTP headers** are **key-value pairs** sent along with HTTP requests and responses.  
They provide metadata about the request or response beyond the main body.

Headers affect:

-   Caching
-   Authentication
-   Security
-   Content type and encoding
-   Debugging

---

## Types of HTTP Headers

### Request Headers

Sent **from client → server** to provide context about the request.

| Header          | Purpose                                                                                |
| --------------- | -------------------------------------------------------------------------------------- |
| `Accept`        | Indicates which content types the client can process (`application/json`, `text/html`) |
| `User-Agent`    | Identifies the client software or browser                                              |
| `Authorization` | Credentials for accessing protected resources                                          |
| `Content-Type`  | Media type of the request body                                                         |

---

### Response Headers

Sent **from server → client** to provide information about the response.

| Header          | Purpose                               |
| --------------- | ------------------------------------- |
| `Content-Type`  | Media type of the response body       |
| `Cache-Control` | Caching instructions for client/proxy |
| `Set-Cookie`    | Sets cookies for session management   |
| `Location`      | URL for redirection                   |

---

### General Headers

Used in **both requests and responses**.

| Header       | Purpose                                       |
| ------------ | --------------------------------------------- |
| `Date`       | Timestamp of message generation               |
| `Connection` | Indicates if the TCP connection is kept alive |

---

### Entity Headers

Describe **the request or response body**.

| Header                | Purpose                                 |
| --------------------- | --------------------------------------- |
| `Content-Length`      | Size of the body in bytes               |
| `Content-Encoding`    | Compression applied (gzip, deflate)     |
| `Content-Language`    | Language of the body                    |
| `Content-Disposition` | How content should be handled/displayed |
| `Transfer-Encoding`   | Encoding applied during transfer        |

---

## Special Categories of HTTP Headers

### Security Headers

Protect applications from **XSS, CSRF, clickjacking**, and enforce HTTPS.

| Header                      | Purpose                                      |
| --------------------------- | -------------------------------------------- |
| `X-Content-Type-Options`    | Prevent MIME type sniffing                   |
| `Strict-Transport-Security` | Enforce HTTPS                                |
| `X-XSS-Protection`          | Enable browser XSS filter                    |
| `Content-Security-Policy`   | Restrict allowed sources for content/scripts |
| `X-Frame-Options`           | Prevent clickjacking                         |
| `Referrer-Policy`           | Control referrer information                 |
| `Feature-Policy`            | Restrict web platform features               |

---

### Authentication Headers

Used to **identify and authorize clients**.

| Header             | Purpose                                              |
| ------------------ | ---------------------------------------------------- |
| `Authorization`    | Credentials (username/password, token, Bearer)       |
| `WWW-Authenticate` | Server requests authentication (scheme + parameters) |
| `Bearer`           | Token-based authentication (OAuth2, JWT)             |

---

### Caching Headers

Control caching behavior for **browsers and proxies**.

| Header          | Purpose                                       |
| --------------- | --------------------------------------------- |
| `Cache-Control` | Directives: `max-age`, `no-cache`, `no-store` |
| `Expires`       | Absolute expiration time                      |
| `ETag`          | Unique identifier for resource version        |
| `Last-Modified` | Timestamp of last resource modification       |

---

### CORS Headers

Enable **cross-origin requests**.

| Header                             | Purpose                      |
| ---------------------------------- | ---------------------------- |
| `Access-Control-Allow-Origin`      | Allowed origins for requests |
| `Access-Control-Allow-Methods`     | Allowed HTTP methods         |
| `Access-Control-Allow-Headers`     | Allowed headers in request   |
| `Access-Control-Allow-Credentials` | Allow cookies/credentials    |

> Missing/incorrect CORS headers trigger browser errors.

---

### Proxy Headers

Provide client info when **passing through proxies**.

| Header              | Purpose                          |
| ------------------- | -------------------------------- |
| `Forwarded`         | Client IP and protocol via proxy |
| `X-Forwarded-For`   | Original client IP               |
| `X-Forwarded-Proto` | Original protocol (HTTP/HTTPS)   |

---

### Debugging Headers

Aid in **troubleshooting and monitoring**.

| Header               | Purpose                            |
| -------------------- | ---------------------------------- |
| `X-Debug-Token`      | Token to fetch debugging info      |
| `X-Debug-Token-Link` | Link to detailed debug information |

---

### Content-Related Headers

Provide metadata about the **message body**.

| Header                | Purpose                                 |
| --------------------- | --------------------------------------- |
| `Content-Type`        | MIME type of content                    |
| `Content-Length`      | Body size in bytes                      |
| `Content-Encoding`    | Compression applied (gzip, deflate)     |
| `Content-Language`    | Language of the body                    |
| `Content-Disposition` | How content should be handled/displayed |
| `Transfer-Encoding`   | Encoding during transfer                |

---

## Manipulating HTTP Headers

### Client-Side

-   Modify headers **before sending a request**.
-   Examples: JS `fetch`, Python `requests`, browser dev tools.

### Server-Side

-   Modify headers **before sending a response**.
-   Examples: Node.js `res.setHeader()`, PHP `header()`, Nginx/Apache config.

### Use Cases

-   Control **cache**, preferred language, authentication credentials.
-   Enforce **security & privacy** (HTTPS, XSS/CSRF).
-   Specify **content handling** (compression, MIME type).

---

## Best Practices for Backend Engineers

1. Always send **appropriate headers** for each request/response.
2. Use **security headers** for HTTPS, XSS, and clickjacking protection.
3. Use **authentication headers** for APIs (`Authorization`, JWT, OAuth2).
4. Use **caching headers** (`Cache-Control`, `ETag`, `Last-Modified`) for performance.
5. Implement **CORS headers** correctly for cross-origin requests.
6. Log or expose **debug headers** only in development.
7. Manipulate headers carefully for **custom behavior, security, and monitoring**.

---

**Summary:** HTTP headers are fundamental in backend development.  
Mastering them ensures **secure, efficient, and reliable** web services.
