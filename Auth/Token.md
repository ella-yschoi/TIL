# Token 🎫

## 1. What is Token?

- Token

  - An encrypted string containing authentication and authorization information
  - Can grant user access permissions to specific applications
  - Using tokens allows storing user authentication information on the **client side** rather than the server

- Token authentication flow
  1. User sends login request to server with authentication information
  2. Server verifies user's authentication information stored in DB
  3. If authentication succeeds, encrypt the user's authentication and authorization information with the server's secret key into a token
  4. Send the generated token to the client
     - Use Authorization header to send authentication token over HTTP or deliver via cookies
  5. Client stores the received token
  6. When client requests resources from server, send token along
     - Also use Authorization header when sending token or deliver via cookies
  7. Server verifies the received token using the server's secret key (can check token forgery and expiration, etc.)
  8. If token is valid, send response data for client's request

<br/>

## 2. Token Characteristics

- Advantages of token authentication method

  - Statelessness
    - Server doesn't manage user authentication state
    - Server only needs to verify the validity of tokens sent by clients using the secret key, enabling stateless architecture
  - Scalability
    - Multiple servers don't need to share common session data
    - Therefore, server scaling is easy
  - Can generate tokens anywhere
    - Token generation and verification don't have to happen on one server
    - Therefore, can build servers dedicated to token generation
  - Easy to grant permissions
    - Can contain various information like authentication status and access permissions, making it easy to grant user permissions
    - Can set admin permissions and information access scope

- Limitations of token authentication method
  - Statelessness
    - Even if a token is stolen, that token cannot be forcibly expired
  - Expiration period
    - Setting short expiration periods causes inconvenience as users must log in every time it expires
    - Setting long expiration periods is dangerous when tokens are stolen
  - Token size
    - Carrying a lot of data increases token size, causing network cost issues

<br/>

## 3. JWT (JSON Web Token)

- What is JWT

  - Technology that carries information in JSON objects and encrypts them into tokens for transmission
  - When a client sends a request to a server, it provides authentication information as an encrypted JWT token, and the server verifies this token to confirm authentication information

- JWT Structure
  - Header
    - Contains data describing the token itself
  - Payload
    - Permissions for what information can be accessed, user's personal information, token issuance time and expiration time, etc.
  - Signature
    - Can verify token integrity
    - Once Header and Payload are complete, use the server's secret key (salt to add to encryption) and the algorithm specified in Header to hash

<br/>

## 4. Access Token and Refresh Token

- Access Token
  - Token for **accessing the server**
  - **Short expiration period of about 24 hours** for security
- Refresh Token
  - Token used to **obtain a new access token** when the access token expires, not for server access
- Summary
  - Even if the access token expires, if the refresh token's expiration period remains, users can maintain continuous authentication without logging in again
  - However, there's a risk of hacking during the token's long expiration period
  - To counter this, **refresh tokens are stored on the server like sessions** and their state is managed
