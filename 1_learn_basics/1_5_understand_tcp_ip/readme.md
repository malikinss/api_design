# IP & TCP: The Basics for Backend Engineers

The **Internet Protocol (IP)** and **Transmission Control Protocol (TCP)** are the foundations of how devices communicate over the Internet. They work together as part of the **TCP/IP suite**, enabling reliable data delivery.

---

## Table of Contents

1. [What is IP?](#what-is-ip)
2. [What is TCP?](#what-is-tcp)
3. [TCP & IP Relationship](#tcp--ip-relationship)
4. [TCP 3-Way Handshake](#tcp-3-way-handshake)
5. [IPv4 vs IPv6](#ipv4-vs-ipv6)
6. [Python Examples](#python-examples)
7. [Summary](#summary)

---

## What is IP?

-   **IP (Internet Protocol)** is responsible for **addressing and delivering packets** of data from a source device to a destination device.
-   IP is **connectionless**:
    -   Each packet is routed individually.
    -   No guarantee of packet order or delivery.
    -   The recipient does **not** acknowledge receipt.
-   Primary function: **routing packets across networks**.

**Example analogy:** Sending puzzle pieces in separate envelopes to a friend. Each envelope may take a different path.

---

## What is TCP?

-   **TCP (Transmission Control Protocol)** provides:
    -   **Connection-oriented communication**.
    -   **Packet ordering** – ensures packets arrive in the correct order.
    -   **Reliability** – resends missing packets.
    -   **Acknowledgements** – lets the sender know the data was received.
-   TCP ensures **complete and reliable communication** over IP.

**Example analogy:** Your friend receives the puzzle pieces and puts them together, asking for missing pieces if needed.

---

## TCP & IP Relationship

| Protocol | Responsibility                                  | Type                |
| -------- | ----------------------------------------------- | ------------------- |
| IP       | Routes individual packets to the target address | Connectionless      |
| TCP      | Ensures order, reliability, and connection      | Connection-oriented |

-   Together, **TCP/IP** provides reliable, ordered data delivery across networks.
-   IP handles **where packets go**, TCP handles **how they arrive**.

---

## TCP 3-Way Handshake

Before sending data, TCP establishes a connection using a **3-step handshake**:

1. **SYN** – Client sends a synchronization request to the server.
2. **SYN-ACK** – Server acknowledges the request and sends its own SYN.
3. **ACK** – Client acknowledges the server’s SYN, establishing the connection.

After this handshake, data packets are transmitted over the established connection.

**Python Example using `socket`**:

```python
import socket

# Client example
client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect(("example.com", 80))  # TCP connection initiated
client.send(b"GET / HTTP/1.1\r\nHost: example.com\r\n\r\n")
response = client.recv(4096)
print(response.decode())
client.close()
```

---

## IPv4 vs IPv6

| Feature           | IPv4                       | IPv6                         |
| ----------------- | -------------------------- | ---------------------------- |
| Address format    | 32-bit (e.g., 192.168.0.1) | 128-bit (e.g., 2001:0db8::1) |
| Address space     | ~4.3 billion               | ~340 undecillion             |
| Header complexity | Simple                     | More complex but extensible  |
| Adoption          | Widely used                | Increasing adoption          |

-   IPv6 solves **address exhaustion** problems of IPv4.
-   Both IPv4 and IPv6 use TCP for reliable connections.

---

## Python Examples: Checking TCP/IP Info

```python
import socket

# Get local host name and IP
hostname = socket.gethostname()
local_ip = socket.gethostbyname(hostname)
print(f"Hostname: {hostname}")
print(f"Local IP: {local_ip}")

# Connect to a server via TCP
server_ip = "93.184.216.34"  # example.com
port = 80
with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.connect((server_ip, port))
    s.sendall(b"GET / HTTP/1.1\r\nHost: example.com\r\n\r\n")
    data = s.recv(1024)
    print(data.decode())
```

---

## Summary

-   **IP** = delivers packets to the correct address (**connectionless**).
-   **TCP** = ensures packets arrive reliably, in order, and manages connections (**connection-oriented**).
-   **TCP/IP** = foundational protocol stack for the Internet.
-   TCP connections begin with a **3-way handshake**.
-   **IPv4** is still the most common, but **IPv6** provides a vastly larger address space.
-   In Python, you can explore TCP/IP using the `socket` module.
