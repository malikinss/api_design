# HTTP Response Status Codes: A Guide for Backend Engineers

HTTP response status codes indicate whether an HTTP request was successfully completed.  
They are **grouped into five classes**, each serving a specific purpose.

---

## 1. Informational Responses (100–199)

These codes are **interim responses**, usually used to indicate that the request is still being processed.

| Code | Name                    | Description                                              |
| ---- | ----------------------- | -------------------------------------------------------- |
| 100  | Continue                | Client should continue the request or ignore if finished |
| 101  | Switching Protocols     | Server is switching protocols requested by client        |
| 102  | Processing (Deprecated) | WebDAV: request received but no status yet               |
| 103  | Early Hints             | Preload resources while server prepares the response     |

---

## 2. Successful Responses (200–299)

Indicate that the request was **successfully received and processed**.

| Code | Name                      | Description                                                                                |
| ---- | ------------------------- | ------------------------------------------------------------------------------------------ |
| 200  | OK                        | Request succeeded (GET returns data, HEAD returns headers, POST/PUT returns resource info) |
| 201  | Created                   | New resource created (usually after POST)                                                  |
| 202  | Accepted                  | Request received but not processed yet (async/batch processing)                            |
| 203  | Non-Authoritative Info    | Metadata from a third-party/mirror                                                         |
| 204  | No Content                | No body, only headers                                                                      |
| 205  | Reset Content             | Client should reset the document that sent the request                                     |
| 206  | Partial Content           | Response to a range request                                                                |
| 207  | Multi-Status (WebDAV)     | Information about multiple resources                                                       |
| 208  | Already Reported (WebDAV) | Avoids repeating internal collection members                                               |
| 226  | IM Used                   | Response is a result of instance manipulations                                             |

---

## 3. Redirection Messages (300–399)

Used to indicate **URL changes** or **alternate locations**.

| Code | Name                   | Description                             |
| ---- | ---------------------- | --------------------------------------- |
| 300  | Multiple Choices       | More than one possible response         |
| 301  | Moved Permanently      | Resource moved permanently to a new URL |
| 302  | Found                  | Temporary redirect to another URI       |
| 303  | See Other              | Redirect using GET                      |
| 304  | Not Modified           | Caching: resource unchanged             |
| 305  | Use Proxy (Deprecated) | Must use a proxy to access resource     |
| 306  | Unused                 | Reserved in old HTTP specs              |
| 307  | Temporary Redirect     | Redirect using the same HTTP method     |
| 308  | Permanent Redirect     | Redirect using same method permanently  |

---

## 4. Client Error Responses (400–499)

Indicate errors on the **client side**.

| Code | Name                            | Description                                     |
| ---- | ------------------------------- | ----------------------------------------------- |
| 400  | Bad Request                     | Malformed or invalid request                    |
| 401  | Unauthorized                    | Client must authenticate                        |
| 402  | Payment Required                | Rarely used, for digital payments               |
| 403  | Forbidden                       | Client is known but not allowed                 |
| 404  | Not Found                       | Resource not found (most common)                |
| 405  | Method Not Allowed              | HTTP method not supported for this resource     |
| 406  | Not Acceptable                  | Server cannot provide content matching criteria |
| 407  | Proxy Authentication Required   | Auth required via proxy                         |
| 408  | Request Timeout                 | Connection idle timeout                         |
| 409  | Conflict                        | Request conflicts with server state             |
| 410  | Gone                            | Resource permanently deleted                    |
| 411  | Length Required                 | Missing `Content-Length` header                 |
| 412  | Precondition Failed             | Headers conditions not met                      |
| 413  | Content Too Large               | Request body exceeds server limit               |
| 414  | URI Too Long                    | Request URI too long                            |
| 415  | Unsupported Media Type          | Media format not supported                      |
| 416  | Range Not Satisfiable           | Requested range cannot be fulfilled             |
| 417  | Expectation Failed              | `Expect` header cannot be met                   |
| 418  | I'm a teapot                    | Easter egg / humorous RFC                       |
| 421  | Misdirected Request             | Sent to wrong server                            |
| 422  | Unprocessable Content (WebDAV)  | Well-formed but semantically invalid            |
| 423  | Locked (WebDAV)                 | Resource is locked                              |
| 424  | Failed Dependency (WebDAV)      | Failed due to previous request failure          |
| 425  | Too Early                       | Experimental: avoid replay risks                |
| 426  | Upgrade Required                | Client must upgrade protocol                    |
| 428  | Precondition Required           | Prevents lost updates                           |
| 429  | Too Many Requests               | Rate limiting                                   |
| 431  | Request Header Fields Too Large | Header fields too large                         |
| 451  | Unavailable For Legal Reasons   | Censored or blocked by law                      |

---

## 5. Server Error Responses (500–599)

Indicate errors **on the server side**.

| Code | Name                            | Description                                          |
| ---- | ------------------------------- | ---------------------------------------------------- |
| 500  | Internal Server Error           | Generic server error                                 |
| 501  | Not Implemented                 | Method not supported (except GET/HEAD)               |
| 502  | Bad Gateway                     | Invalid response from upstream server                |
| 503  | Service Unavailable             | Server overloaded or down, `Retry-After` recommended |
| 504  | Gateway Timeout                 | Upstream server timed out                            |
| 505  | HTTP Version Not Supported      | Version not supported by server                      |
| 506  | Variant Also Negotiates         | Circular content negotiation error                   |
| 507  | Insufficient Storage (WebDAV)   | Cannot store resource                                |
| 508  | Loop Detected (WebDAV)          | Infinite loop detected                               |
| 510  | Not Extended                    | HTTP extension not supported                         |
| 511  | Network Authentication Required | Auth needed to access network                        |

---

### ✅ Notes for Junior Backend Engineers

-   **2xx** → success
-   **3xx** → redirection
-   **4xx** → client error
-   **5xx** → server error

-   Always **log unusual 4xx/5xx codes** for debugging APIs
-   **Understand method semantics** to interpret status codes correctly
-   Common ones to remember: `200 OK`, `201 Created`, `204 No Content`, `400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`, `500 Internal Server Error`, `503 Service Unavailable`

---

This table will help you **quickly identify and troubleshoot HTTP issues** when building backend services or REST APIs.
