# HTTP Protocol Evolution: HTTP Versions

This lecture-style article explains **how HTTP evolved**, why new versions appeared, and what every **backend engineer** must understand about HTTP versions in practice.

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Application Layer Protocols](#2-application-layer-protocols)
3. [What Is HTTP?](#3-what-is-http)
4. [HTTP 0.9](#4-http-09)
5. [HTTP 1.0](#5-http-10)
6. [HTTP 1.1](#6-http-11)
7. [HTTP 2.0](#7-http-20)
8. [HTTP 3.0](#8-http-30)
9. [HTTP Versions Comparison](#9-http-versions-comparison)
10. [Why HTTP Evolution Matters for Backend Engineers](#10-why-http-evolution-matters-for-backend-engineers)

---

## 1. Introduction

Network communication is structured using layered models such as:

### OSI Model (simplified)

-   **Network layer** → IP
-   **Transport layer** → TCP / UDP
-   **Application layer** → HTTP, SMTP, FTP

### TCP/IP Model

-   Application
-   Transport
-   Internet
-   Network access

**HTTP belongs to the Application Layer**, meaning it defines **how applications talk**, not how packets are routed.

Protocols evolve because:

-   the web grows
-   performance requirements increase
-   security becomes critical

This document focuses on **HTTP evolution from 0.9 to 3.0**.

---

## 2. Application Layer Protocols

The **application layer** is the closest to the user.

Examples of applications:

-   Web browsers
-   Mobile apps
-   Email clients
-   Backend services

### Common Network Architectures

1. **Client–Server**

    - Browser → Backend API
    - Most web applications

2. **Peer-to-Peer (P2P)**

    - Nodes communicate directly
    - Example: BitTorrent

3. **Hybrid**
    - Mix of centralized and P2P
    - Example: modern messaging systems

### Common Application Layer Protocols

-   HTTP / HTTPS
-   FTP
-   SMTP
-   POP / IMAP
-   DNS
-   TELNET

---

## 3. What Is HTTP?

**HTTP (Hypertext Transfer Protocol)** is an application-layer protocol for **distributed hypermedia systems**.

Key properties:

-   Request–response based
-   Client initiates communication
-   Server responds with data
-   Stateless by design

### HTTP Sessions

A **session** is a sequence of:

-   requests
-   responses

Even though HTTP is stateless, sessions are simulated using:

-   cookies
-   tokens
-   headers

---

## 4. HTTP 0.9 (Early 1990s)

The very first HTTP version.

### Features

-   Only one method: `GET`
-   No headers
-   No status codes
-   Only plain ASCII text
-   One request → one response → connection closed

### Example

```http
GET /index.html
```

📌 Extremely limited, but enough for early web pages.

---

## 5. HTTP 1.0 (1996)

HTTP became **usable for real applications**.

### New Features

-   Request and response **headers**
-   HTTP version specified in requests
-   **Status codes** (200, 404, etc.)
-   `Content-Type` header
-   New methods:

    -   `POST`
    -   `HEAD`

### Example

```http
POST /login HTTP/1.0
Content-Type: application/json
```

📌 HTTP 1.0 introduced **extensibility**.

---

## 6. HTTP 1.1 (1997)

Still widely used today.

### Major Improvements

#### 1. Persistent Connections

-   Multiple requests per TCP connection
-   Reduced overhead

#### 2. Host Header (Mandatory)

```http
Host: api.example.com
```

Allows **multiple websites on one IP** (virtual hosting).

#### 3. New HTTP Methods

| Method  | Purpose               |
| ------- | --------------------- |
| PUT     | Replace resource      |
| PATCH   | Partial update        |
| DELETE  | Remove resource       |
| CONNECT | Proxy tunneling       |
| TRACE   | Debugging             |
| OPTIONS | Discover capabilities |

#### 4. Performance & Features

-   Compression
-   Byte-range requests
-   Language and encoding negotiation

📌 HTTP 1.1 is the **foundation of REST APIs**.

---

## 7. HTTP 2.0 (2015)

Focus: **performance**, not semantics.

### Key Improvements

#### Multiplexing

-   Multiple requests in parallel
-   No more head-of-line blocking

#### Binary Protocol

-   Replaced text-based format
-   Faster parsing

#### Header Compression

-   Reduced request size

#### Server Push

-   Server sends resources **before client asks**

Example:

-   HTML requested
-   CSS and JS pushed automatically

📌 Same HTTP methods, same URLs — faster delivery.

---

## 8. HTTP 3.0 (2020)

### Biggest Change: Transport Layer

| HTTP Version | Transport        |
| ------------ | ---------------- |
| 1.x / 2.0    | TCP              |
| 3.0          | QUIC (UDP-based) |

### Why QUIC?

-   Faster handshakes
-   Built-in encryption
-   Better handling of packet loss
-   Independent streams (no blocking)

### Key Properties

-   Always encrypted
-   Lower latency
-   Better performance on mobile networks

📌 HTTP/3 improves **connection reliability**, not API design.

---

## 9. HTTP Versions Comparison

| Version | Key Features                               |
| ------- | ------------------------------------------ |
| 0.9     | GET only, ASCII                            |
| 1.0     | Headers, status codes, POST                |
| 1.1     | Persistent connections, many methods       |
| 2.0     | Multiplexing, binary protocol, server push |
| 3.0     | QUIC, UDP-based, always encrypted          |

### HTTP Method Evolution

-   `GET` → 0.9
-   `POST`, `HEAD` → 1.0
-   `PUT`, `PATCH`, `DELETE`, `OPTIONS`, `TRACE`, `CONNECT` → 1.1

---

## 10. Why HTTP Evolution Matters for Backend Engineers

As a backend engineer, you must:

-   Understand how HTTP requests work
-   Know which version impacts performance
-   Design APIs that work efficiently over HTTP
-   Debug latency, headers, caching, and proxies

### Practical Takeaways

-   REST APIs rely heavily on **HTTP 1.1 semantics**
-   HTTP/2 and HTTP/3 mostly affect **transport performance**
-   Correct use of headers and methods matters more than version choice
-   Stateless design remains critical

---

## Final Summary

HTTP evolved from a **simple document-fetching protocol** into a **high-performance foundation of modern APIs**.

A strong backend engineer:

-   Understands HTTP deeply
-   Uses methods correctly
-   Thinks about performance and scalability
-   Knows how transport affects real-world systems
