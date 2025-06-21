# Session 🪪

## 1. What is Session?

- Server assigns a unique and encrypted ID to the client

<br/>

## 2. Session-based Authentication

- Login
  - If the server knows 'this user has successfully authenticated', the user doesn't need to log in every time
  - Roles of server and client
    - Server: Must know that the user has successfully authenticated
    - Client: Must have a means to prove successful authentication
  - Session: 'State where user has successfully authenticated'
    - Important data is stored and managed on the server or stored in session store
    - When a session is created, a session_id is created to distinguish each session
    - Usually session_id is passed to the client as a means to prove session success
- Logout
  - Roles of server and client
    - Server: Delete session information
    - Client: Modify/delete cookies
  - To remove session information from client, change the cookie value to an invalid value using `res.cookie`
  - Or you can delete the cookie using `res.clearCookie`
