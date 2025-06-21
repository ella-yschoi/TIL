# HTTP

## 1. HTTP Messages

### Definition

- The way data is exchanged between client and server
- Requests and responses have similar structures as shown below, and the start line and HTTP headers together are called the head of the request or response, while the Payload is called the body

### Structure

![http_message](../Images/http_message.png)

- start line: represents the status of the request or response, always located on the first line, and called status line in responses
- HTTP headers: a collection of headers that specify the request or describe the body included in the message
- empty line: empty line that separates headers and body
- body: contains data related to the request or response, or documents, used optionally depending on the type

<br/>

## 2. HTTP Requests

Messages sent by clients to servers

### Three elements of start line

- HTTP method that describes the operation or method to be performed
- Request target or absolute path of protocol, port, domain is written in the request context

### Headers

- Enter header name, colon, and value
- General headers
- Request headers
- Representation headers

### Body

- Not required for all requests
- Single-resource bodies
- Multiple-resource bodies

<br/>

## 3. HTTP Responses

Messages sent by servers to clients

### Status line

- Current protocol version (HTTP/1.1)
- Status code: result of the request (e.g., 200, 302, 404, etc.)
- Status text: description of the status code

### Header

- Same structure as request headers

<br/>

## 4. Stateful vs. Stateless

### Stateful

- The same server must always be maintained
- If the server fails, the maintained state information is lost, so you need to request the server again from the beginning

### Stateless

- Since the client sends all necessary data when making a request, any server can be called
- Even if one server fails, another server can deliver the response, so the client doesn't need to request again
- Since the response server can be easily changed, unlimited server scaling is possible
- However, you can design everything as stateless, or there are cases where it's not possible (e.g., simple service introduction screens that don't require login can be designed as stateless, but services that require login need to maintain user state using browser cookies, sessions, tokens, etc.)

<br/>

## 5. Connection Oriented vs. Connectionless

### Connection Oriented

- Model that maintains connections
- Server resources are consumed because connections must be maintained even when clients don't send requests

### Connectionless

- Model that doesn't maintain connections
- Only maintains connections when actually sending and receiving requests, and disconnects TCP/IP connection after sending response, so minimal server resources are used

<br/>

## 6. Characteristics of HTTP

### HTTP 1.0

- HTTP is basically a model that doesn't maintain connections
- Generally responds at speeds below seconds
- Even if thousands of people use the service for an hour, the actual number of requests processed simultaneously by the server is very small, below dozens
- However, in large services with high traffic, the non-connection nature shows limitations
- It's inefficient to repeatedly disconnect and reconnect each time resources are sent

### HTTP Persistent Connections

- This problem is solved and further optimized in HTTP2, 3
- After connection is established, request each resource, and connection ends after responses for all resources are returned, so time is reduced

<br/>

## 7. HTTPS

### Meaning and Characteristics

- Abbreviation for HTTP Secure, meaning HTTP protocol can be used more safely
- Unlike HTTP, it encrypts the content going back and forth in requests and responses
- Therefore, even if a third party intercepts HTTPS request and response data, they cannot understand the content

### Encryption Methods

#### Symmetric Key Encryption

- Uses only one key, so decryption is possible with the key used for encryption
- Has the advantage of fast computation speed, but requires careful key management when the key is compromised

#### Asymmetric Key Encryption (Public Key Encryption)

- Uses two keys (public key, private key), so decryption is only possible with a different key than the one used for encryption
- Usually the user sending the request has the public key, and the server receiving the request has the private key, so the private key cannot be compromised unless the server is hacked
- Good security but requires more complex computation, so more time is consumed

<br/>

## 8. SSL/TLS Protocol

- HTTPS performs server authentication and data encryption using SSL or TLS protocol in the socket part that handles HTTP communication
- TLS is the standardized name that changed from SSL, so they are essentially the same protocol

### Characteristics of SSL/TLS

- Uses certificates through CA (Certificate Authority)
- Uses both symmetric key and public key encryption methods
