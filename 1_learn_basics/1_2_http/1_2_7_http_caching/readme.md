# HTTP Caching

This guide explains **HTTP caching**, its purpose, how it works, and best practices for implementation.

---

## Table of Contents

1. [What is HTTP Caching?](#what-is-http-caching)
2. [Why HTTP Caching is Important](#why-http-caching-is-important)
3. [Types of HTTP Caching](#types-of-http-caching)
4. [HTTP Cache Headers](#http-cache-headers)
5. [Cache Validation](#cache-validation)
6. [Cache-Control Directives](#cache-control-directives)
7. [ETag and Last-Modified](#etag-and-last-modified)
8. [Browser and Proxy Caching](#browser-and-proxy-caching)
9. [Best Practices for HTTP Caching](#best-practices-for-http-caching)

---

## What is HTTP Caching?

**HTTP caching** is a mechanism that stores copies of HTTP responses to reuse them for subsequent requests. Caching reduces **network latency**, decreases **server load**, and improves **user experience** by delivering content faster.

When a browser or proxy cache stores a response, it can serve it without contacting the server again, if the response is still valid.

---

## Why HTTP Caching is Important

Caching improves:

-   **Performance** – pages load faster as resources come from local or intermediary caches.
-   **Scalability** – reduces the number of requests reaching the origin server.
-   **Bandwidth efficiency** – decreases repeated downloads of the same resources.

Without caching, every request requires a full round trip to the server, increasing latency and server load.

---

## Types of HTTP Caching

1. **Browser (Client) Cache**

    - Stored locally in the user’s browser.
    - Can be reused for future requests to the same origin.

2. **Proxy (Intermediate) Cache**

    - Stored on CDN nodes, reverse proxies, or ISP caches.
    - Can serve responses to multiple users.

3. **Server Cache**
    - Stored on the origin server.
    - Reduces database or computation load before responding to clients.

---

## HTTP Cache Headers

HTTP caching is controlled using **HTTP headers**, which can be classified as:

1. **General headers** – applicable to both request and response

    - `Date` – timestamp of the response creation

2. **Request headers** – sent by client to control caching behavior

    - `Cache-Control` – allows client to specify caching preferences (e.g., `no-cache`, `max-age`)
    - `Pragma` – legacy header, similar to `Cache-Control`
    - `If-Modified-Since` – conditional request using last modification date
    - `If-None-Match` – conditional request using entity tags (ETags)

3. **Response headers** – sent by server to control how content is cached
    - `Cache-Control` – primary header for caching rules
    - `Expires` – absolute expiration date/time
    - `ETag` – unique identifier for a resource version
    - `Last-Modified` – timestamp of the last modification

---

## Cache Validation

HTTP caching supports **two types of validation**:

1. **Strong Validation** – uses `ETag`

    - Server compares client’s `If-None-Match` header with resource version.
    - Returns `304 Not Modified` if resource hasn’t changed.

2. **Weak Validation** – uses `Last-Modified`
    - Server compares client’s `If-Modified-Since` with resource’s last modification date.
    - Returns `304 Not Modified` if resource hasn’t changed.

**304 responses** reduce payload because the content is already cached.

---

## Cache-Control Directives

The `Cache-Control` header allows precise control over caching:

-   `public` – response can be cached by browsers and proxies
-   `private` – only browser can cache
-   `no-cache` – forces revalidation with server before reuse
-   `no-store` – response must not be stored anywhere
-   `max-age=<seconds>` – sets max time the response is considered fresh
-   `must-revalidate` – cache must revalidate after expiration

**Example:**

```http
Cache-Control: public, max-age=3600, must-revalidate
```

---

## ETag and Last-Modified

**ETag (Entity Tag)** – a unique hash representing the resource version.
**Last-Modified** – timestamp of the last modification.

**Conditional request example:**

```http
GET /style.css HTTP/1.1
If-None-Match: "abc123"
If-Modified-Since: Wed, 01 Jan 2026 12:00:00 GMT
```

**Server response if unchanged:**

```http
HTTP/1.1 304 Not Modified
```

---

## Browser and Proxy Caching

-   **Browser caching** stores content locally for repeated use.
-   **Proxy/CDN caching** stores content closer to users to reduce latency.

**Important points:**

-   Not all responses are cacheable (e.g., dynamic content, sensitive data).
-   Caches obey `Cache-Control`, `Expires`, `ETag`, and `Last-Modified` headers.

---

## Best Practices for HTTP Caching

1. Use **Cache-Control** instead of the old `Expires` header.
2. Set appropriate caching for **static assets** (CSS, JS, images).
3. Use **ETags** and **Last-Modified** for dynamic content.
4. Avoid caching **sensitive or personalized data**.
5. Use **shorter max-age** for frequently changing resources.
6. Leverage **CDNs** for caching globally.
7. Test caching behavior using browser dev tools or curl.
