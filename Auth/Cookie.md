# Cookie 🍪

## 1. What is Cookie?

- A method for servers to store persistent data on clients
- A means for servers to store and retrieve information from web browsers
- If a cookie exists for a domain, the web browser sends the cookie along with HTTP requests to that domain
- Includes not only sending cookies from server to client, but also sending cookies from client back to server
- However, **certain conditions must be met** such as HTTP header settings after storing data to retrieve it again

  ```shell
  'Set-Cookie':[
            'cookie=yummy',
            'Secure=Secure; Secure',
            'HttpOnly=HttpOnly; HttpOnly',
            'Path=Path; Path=/cookie',
            'Doamin=Domain; Domain=naver.com'
        ]
  ```

<br/>

## 2. Cookie Option Types

1. **Domain**

   - A name that can access the server like `www.google.com`
   - Does not include port, subdomain information, or detailed paths
   - On the client side, the cookie's domain option must match the server's domain to send the cookie
   - In `http://www.localhost.com:3000/users/login`, the Domain is `localhost.com`

2. **Path**

   - A detailed path used when the server routes
   - Can send cookies to the server even when requesting subpaths that include the set path
   - In `http://www.localhost.com:3000/users/login`, the Path is `/users/login`

3. **MaxAge or Expires**

   - Options that determine the valid period of the cookie
   - MaxAge sets the valid time of the cookie in seconds
   - Expires sets the valid time and date of the cookie (based on client time)
   - Session Cookie
     - A cookie without MaxAge or Expires options
     - A temporary cookie that can be used while the browser is running
     - Deleted when the browser is closed
   - Persistent Cookie
     - Independent of browser closure
     - A cookie that can be used for the valid time specified in MaxAge or Expires

4. **Secure**

   - An option that determines whether to send cookies based on the protocol being used
   - If the option is `true`, cookies can only be sent when using HTTPS
   - If there's no secure option, cookies can be sent regardless of protocol, whether http or https
   - However, if the domain is `localhost`, cookies can be sent even without https

5. **HttpOnly**

   - Determines whether JavaScript can access browser cookies
   - An option that prevents clients from accessing cookies using DOM
   - An option that determines whether to send cookies based on the protocol being used
   - Default is false, and if the option is `true`, JavaScript cannot access cookies
   - If `false`, there's a risk of cookie theft using `document.cookie`

6. **SameSite**
   - When receiving Cross-site requests, determines whether to send cookies based on the combination of the method used in the request and this option
   - Cross-origin
     - Classified as Cross-origin if any of the server's domain, protocol, or port is different
   - Cross-site
     - When eTLD+1 is different (\*eTLD+1: combination of the sublevel domain immediately to the left of the top-level domain)
   - Attributes that can be used in SameSite option
     - Lax: Can only send cookies for GET methods if it's a Cross-Site request
     - Strict: Only sends cookies if it's Same-Site, not Cross-Site
     - None: Can always send cookies, but requires Secure option

<br/>

## 3. State Maintenance Using Cookies

- Can maintain stateless internet connections as stateful using cookie characteristics
- However, cookies can generally be maintained for a long time, and if the HttpOnly option is not used, JavaScript can access cookies, so storing sensitive information in cookies is dangerous
