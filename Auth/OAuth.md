# OAuth

## 1. What is OAuth?

- Unlike traditional servers that handle authentication directly, OAuth is **a mechanism that mediates authentication**
- A protocol that simplifies the process of providing clients with permissions to access secured resources
- In other words, web services that already have user information can handle user authentication on your behalf, issue tokens for access permissions, and use them for authentication on your server

<br/>

## 2. OAuth Operation Mechanism

- Resource Owner
  - The user who wants to perform social login through OAuth authentication
- Resource Server
  - The server that stores user information
- Authorization Server
  - Among servers that store user information, the server responsible for authentication
- Application
  - The environment where users want to use social login

<br/>

## 3. Types and Flow of OAuth Authentication Methods

- **Implicit Grant Type**
  - If already logged into an existing service, immediately provides access token to new service, making it less secure
- **Authorization Code Grant Type**
  - More secure than Implicit Grant Type because it has an additional authentication step using Authorization Code
  - Also, tokens can be managed only on the server without exposing them to the Application's Client, increasing options for implementing social login
- **Refresh Token Grant Type**
  - If access tokens expire, having to go through this process every time to reissue access tokens is not good for user convenience → issue refresh tokens as well

<br/>

## 4. OAuth Advantages

- Easy and safe to use new services
- Can set permission scopes
