# HTTP Content Negotiation

**Content negotiation** in HTTP is the mechanism that allows a server to serve different representations of the same resource at a single URL, depending on the client’s preferences. This can include language, content type (HTML, JSON, XML), or encoding (gzip, Brotli).

---

## Table of Contents

1. [Principles of Content Negotiation](#principles-of-content-negotiation)
2. [Server-Driven Content Negotiation](#server-driven-content-negotiation)
3. [Agent-Driven (Client-Driven) Negotiation](#agent-driven-client-driven-negotiation)
4. [Common HTTP Headers for Content Negotiation](#common-http-headers-for-content-negotiation)
5. [Python Examples](#python-examples)
6. [Best Practices](#best-practices)
7. [Summary](#summary)

---

## Principles of Content Negotiation

-   A **resource** can have multiple **representations** (e.g., HTML page, JSON API, image formats).
-   The server chooses a representation based on:
    1. HTTP headers sent by the client (**server-driven negotiation**)
    2. HTTP status codes like `300 Multiple Choices` or `406 Not Acceptable` (**agent-driven negotiation**)
-   The **Vary** header informs caches which client headers were used to select the response.

---

## Server-Driven Content Negotiation

-   Also called **proactive negotiation**.
-   The client sends headers indicating preferences (`Accept`, `Accept-Encoding`, `Accept-Language`, etc.).
-   The server selects the best match using an internal algorithm.
-   If no suitable match exists, the server may respond with:
    -   `406 Not Acceptable`
    -   `415 Unsupported Media Type`
-   The `Vary` header is used to indicate which request headers affected the server's choice, so caches work correctly.

**Advantages:**

-   Fully automated selection by the server.
-   Commonly used and supported by browsers.

**Drawbacks:**

-   Server may not have full knowledge of the client.
-   Verbose headers increase request size.
-   Shared caches are less efficient due to multiple representations.

---

## Agent-Driven (Client-Driven) Negotiation

-   Also called **reactive negotiation**.
-   The server responds with multiple available representations.
-   The client chooses the preferred resource.
-   Typically implemented with:
    -   `300 Multiple Choices` responses
    -   HTML or JavaScript redirect pages for resource selection
-   Less common because it requires additional client requests.

---

## Common HTTP Headers for Content Negotiation

| Header            | Purpose                                                                          |
| ----------------- | -------------------------------------------------------------------------------- |
| `Accept`          | Client specifies preferred media types (e.g., `application/json`)                |
| `Accept-Encoding` | Client specifies supported compressions (gzip, br, deflate)                      |
| `Accept-Language` | Client specifies preferred languages (e.g., `en-US`, `fr`)                       |
| `User-Agent`      | Identifies browser or client; sometimes used to choose content (not recommended) |
| `Vary`            | Sent by server to indicate which headers were used for negotiation               |
| `Accept-CH`       | Experimental: client hints for device capabilities (screen size, memory, etc.)   |

---

## Python Examples

### Server-Driven Content Negotiation (FastAPI)

```python
from fastapi import FastAPI, Request
from fastapi.responses import JSONResponse, HTMLResponse

app = FastAPI()

@app.get("/resource")
async def get_resource(request: Request):
    accept = request.headers.get("accept", "")

    if "application/json" in accept:
        return JSONResponse(content={"message": "Hello, JSON!"})
    elif "text/html" in accept:
        return HTMLResponse(content="<h1>Hello, HTML!</h1>")
    else:
        return JSONResponse(content={"message": "Default response"}, status_code=406)
```

**Request Examples:**

```
GET /resource
Accept: application/json
→ Returns JSON

GET /resource
Accept: text/html
→ Returns HTML

GET /resource
Accept: application/xml
→ Returns 406 Not Acceptable
```

---

### Using Accept-Encoding for Compression

```python
from fastapi import FastAPI, Request
from fastapi.responses import PlainTextResponse
import gzip

app = FastAPI()

@app.get("/compressed")
async def compressed(request: Request):
    accept_encoding = request.headers.get("accept-encoding", "")
    data = b"Hello world!" * 50

    if "gzip" in accept_encoding:
        compressed_data = gzip.compress(data)
        return PlainTextResponse(content=compressed_data, headers={"Content-Encoding": "gzip"})

    return PlainTextResponse(content=data.decode())
```

---

### Accept-Language Example

```python
from fastapi import FastAPI, Request
from fastapi.responses import PlainTextResponse

app = FastAPI()

@app.get("/greet")
async def greet(request: Request):
    accept_language = request.headers.get("accept-language", "en")

    if "fr" in accept_language:
        return PlainTextResponse(content="Bonjour!")
    elif "es" in accept_language:
        return PlainTextResponse(content="¡Hola!")
    else:
        return PlainTextResponse(content="Hello!")
```

---

## Best Practices

1. Prefer **server-driven negotiation** for automation.
2. Use `Vary` header to make caching work correctly.
3. Avoid using `User-Agent` to select content when possible.
4. Always provide a **fallback representation**.
5. Allow **user override** for language or format preferences.
6. Use **Accept headers** properly in API design.

---

## Summary

-   HTTP content negotiation allows the **server to serve multiple representations** of the same resource.
-   **Server-driven negotiation** relies on headers like `Accept`, `Accept-Encoding`, and `Accept-Language`.
-   **Agent-driven negotiation** lets the client choose from multiple options provided by the server.
-   Proper implementation ensures **efficient caching, better user experience, and RESTful API design**.
