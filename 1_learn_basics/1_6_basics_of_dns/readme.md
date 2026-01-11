# DNS (Domain Name System)

The **Domain Name System (DNS)** is the phonebook of the Internet. It translates **human-readable domain names** (like `example.com`) into **IP addresses** (like `192.168.1.1` or `2400:cb00:2048::1`) that computers use to locate each other.

---

## Table of Contents

1. [What is DNS?](#what-is-dns)
2. [How DNS Works](#how-dns-works)
3. [DNS Servers](#dns-servers)
4. [Types of DNS Queries](#types-of-dns-queries)
5. [DNS Caching](#dns-caching)
6. [Python Examples](#python-examples)
7. [Summary](#summary)

---

## What is DNS?

-   Humans access websites via **domain names**.
-   Computers communicate via **IP addresses**.
-   DNS **resolves domain names to IP addresses**, so users don’t have to remember numeric addresses.

**Analogy:** DNS is like a librarian who looks up the street address of a book for you.

---

## How DNS Works

When a user types a URL into their browser:

1. The browser queries a **DNS resolver**.
2. The resolver contacts a **root nameserver** (`.`).
3. The root points to the **TLD server** (`.com`, `.net`, etc.).
4. The TLD server points to the **authoritative nameserver** for the domain.
5. The authoritative server returns the **IP address**.
6. The browser uses the IP to send an **HTTP request** to the server.

**Step-by-step summary:**

```text
User types "example.com" → Resolver → Root → TLD → Authoritative → Resolver → Browser → Server
```

---

## DNS Servers

| Server Type                  | Role                                                                                  |
| ---------------------------- | ------------------------------------------------------------------------------------- |
| **Recursive Resolver**       | Receives the client’s query, tracks down the IP by querying other servers recursively |
| **Root Nameserver**          | First step; points to TLD nameservers                                                 |
| **TLD Nameserver**           | Hosts top-level domains like `.com` or `.org`; points to authoritative servers        |
| **Authoritative Nameserver** | Holds the definitive record for a domain; returns IP address to resolver              |

**Analogy:** Librarian (recursive resolver) → Index (root) → Rack (TLD) → Dictionary (authoritative)

---

## Types of DNS Queries

1. **Recursive Query**

    - Resolver must return the final answer (IP address) or an error.

2. **Iterative Query**

    - Resolver returns the best answer it has, possibly a referral to another server.

3. **Non-Recursive Query**

    - Resolver returns an answer from its cache or if it is authoritative for the domain.

---

## DNS Caching

Caching improves **performance** and **reduces load**:

-   **Browser Cache:** First place checked before making external DNS requests.
-   **Operating System Cache (Stub Resolver):** Checks local cache before querying external resolvers.
-   **Recursive Resolver Cache:** Stores previous query results to speed up future lookups.

**TTL (Time-To-Live)** defines how long a DNS record is cached before it expires.

---

## Python Examples: DNS Lookup

```python
import socket

# Simple DNS lookup
domain = "example.com"
ip_address = socket.gethostbyname(domain)
print(f"{domain} -> {ip_address}")

# Get all IP addresses (IPv4 + IPv6)
addresses = socket.getaddrinfo(domain, None)
for addr in addresses:
    print(addr[4][0])
```

**Using `dnspython` for more advanced queries:**

```python
import dns.resolver

domain = "example.com"
result = dns.resolver.resolve(domain, 'A')  # Query A record (IPv4)
for ip in result:
    print(f"A record: {ip}")

# Query MX record (mail server)
mx_records = dns.resolver.resolve(domain, 'MX')
for mx in mx_records:
    print(f"MX record: {mx.exchange}")
```

---

## Summary

-   **DNS** translates domain names → IP addresses, enabling human-friendly browsing.
-   **Recursive resolver** starts the query; **authoritative server** is the final source.
-   Queries can be **recursive, iterative, or non-recursive**.
-   **Caching** improves speed and reduces network traffic.
-   In Python, `socket` or `dnspython` libraries can be used to perform DNS lookups.
