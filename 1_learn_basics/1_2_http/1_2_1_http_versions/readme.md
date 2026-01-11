# HTTP Protocol Evolution: HTTP Versions

---

## 1. Introduction

In networking, protocols are organized using models like **OSI** and **TCP/IP**, each with distinct layers:

-   **Network Layer**: e.g., IP
-   **Transport Layer**: e.g., TCP, UDP
-   **Application Layer**: e.g., HTTP

Protocols evolve over time and have multiple versions. This lecture focuses on the **HTTP application protocol**, covering:

1. Application layer protocols
2. HTTP general purpose
3. HTTP versions and their differences

---

## 2. Application Layer Protocols

The **application layer** (OSI Layer 7 / TCP/IP Layer 4) provides end-to-end communication between applications.  
It is the **closest layer to the user**: browsers, email clients, streaming apps operate here.

### Common architectures

1. **Client-Server**: Multiple clients request services from a central server
2. **Peer-to-Peer (P2P)**: Independent computers collaborate in a network
3. **Hybrid**: Combines client-server and peer-to-peer

### Examples of application layer protocols

-   HTTP, FTP, TELNET, POP, DNS, SMTP

---

## 3. The Hypertext Transfer Protocol (HTTP)

**HTTP** is a layer 7 (OSI) / layer 4 (TCP/IP) protocol for **distributed hypermedia systems**.

-   **Agile**: Works independently of addressing and transport
-   **Connection-based**: Relies on TCP/IP
-   **Sessions**: Series of message exchanges between client and server

### History

-   **HTTP 0.9** (early 1990s):
    -   Only `GET` method
    -   ASCII text only
-   Later versions added headers, new methods, content types, and status codes

---

## 3.1 HTTP 1.0 (1996)

Enhancements over 0.9:

-   **HTTP headers**: Metadata for flexible communication
-   **Versioning**: Requests include HTTP version
-   **Status codes**: Indicates success or failure
-   **Content-Type**: Supports multiple file types
-   **New methods**: `POST` (send data) and `HEAD` (fetch metadata)

**Summary**: HTTP 1.0 made the protocol **robust and extensible**.

---

## 3.2 HTTP 1.1 (1997)

Enhancements over 1.0:

-   **Host header**: Required; supports virtual hosts via proxies
-   **Persistent connections**: Multiple requests per connection
-   **Continue status (100)**: Allows clients to send headers first
-   **New methods**: `PUT`, `PATCH`, `DELETE`, `CONNECT`, `TRACE`, `OPTIONS`
-   Other features: compression, byte-range transfers, multi-language support

**Method Highlights**:

| Method  | Purpose                   |
| ------- | ------------------------- |
| PUT     | Replace resource          |
| PATCH   | Partial update            |
| DELETE  | Remove resource           |
| CONNECT | Tunnel via proxy          |
| TRACE   | Loopback test             |
| OPTIONS | Get communication options |

---

## 3.3 HTTP 2.0 (2015)

Focus: **Performance improvements**

-   **Request multiplexing**: Multiple requests simultaneously over one connection
-   **Request prioritization**: Specify order for responses
-   **Automatic compression**: GZip compression enabled automatically
-   **Connection reset**: Close and reopen connections quickly
-   **Server push**: Server proactively sends resources to client cache
-   **Binary protocol**: Replaces plain-text HTTP 1.x

**Summary**: Solves sequential processing, reduces latency, improves efficiency.

---

## 3.4 HTTP 3.0 (2020)

**Key change**: Transport protocol switched from **TCP** → **QUIC (UDP-based)**

-   **QUIC features**: Multiplexing, encryption, fast handshake, low-latency connections
-   **Always encrypted**: No more separate HTTP/HTTPS distinction
-   Aims to improve connection speed and reliability

---

## 4. Systematic Summary of HTTP Evolution

| Version | Key Features                                                                      |
| ------- | --------------------------------------------------------------------------------- |
| 0.9     | Only GET, ASCII text                                                              |
| 1.0     | Headers, versioning, status codes, Content-Type, POST & HEAD                      |
| 1.1     | Host header, persistent connections, 6 new methods, compression, byte ranges      |
| 2.0     | Multiplexing, prioritization, automatic compression, server push, binary protocol |
| 3.0     | QUIC transport, always encrypted, fast connections                                |

**Method Evolution**:

-   GET (0.9)
-   POST, HEAD (1.0)
-   PUT, PATCH, DELETE, CONNECT, TRACE, OPTIONS (1.1)

**Main novelty of 3.0**: Replacing TCP with QUIC for **encryption and faster connections**.

---

## 5. Conclusion

HTTP evolved from a **simple ASCII-based GET protocol** to a **powerful binary protocol** supporting modern web systems.  
Key points for backend engineers:

-   Understand HTTP **requests, responses, headers, status codes**
-   Recognize **method purposes** and evolution
-   Grasp HTTP **performance improvements** (multiplexing, server push)
-   Learn about **transport layer differences** (TCP vs QUIC)

HTTP remains **fundamental** for backend development and REST API design.
