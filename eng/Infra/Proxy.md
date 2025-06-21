# Proxy

## 1. Why CORS Policy is Needed

- In browsers, by default, when making API requests, the domain of the browser's current address and the API's address must match to access data
- The DB connected to the server behind the built client contains live data that is mainly sensitive data, so security is most important
- If a service allows access from all origins, it could be exposed to hacking risks, so **you shouldn't allow all domains, but implement to allow specific domains**.
- Therefore, frontend developers need to request backend developers to allow the frontend development server domain,
- Backend developers need to include necessary values in response headers and deliver them.
- This is because if the server doesn't receive appropriate response headers, an error occurs in the browser

<br/>

## 2. Proxy

- You can bypass CORS policy by using proxy functionality provided by React library or Webpack Dev Server without the above standard process
- In other words, **without needing to receive separate response headers, the browser requests data to the React app, and that request is forwarded to the backend**.
- Here, the React app forwards the response data received from the server back to the browser, so the browser doesn't know if it violated CORS policy.
- In other words, deceiving the browser through proxy functionality.

<br/>

## 3. Proxy Operation Flow

### Flow before proxy application

![proxy_before](/Images/proxy_before.png)

1. The React app developed in frontend sends a request to the browser
2. The browser requests resources from the backend, i.e., the server. At this time, it checks if there's access permission, i.e., if the origin is the same, and the backend server sends a normal 200 OK response to the browser.
3. The browser checks if the received resource and response have the same origin, and if the origins are different, it discards the response (CORS Error), and if the origins are the same, it doesn't discard the response and sends the response back to the frontend.

### Flow after proxy application

![proxy_after](/Images/proxy_after.png)

1. When requesting API through browser from React app, **the request is bypassed to the backend server through proxy**
2. **The backend server sends the response to the React app**, and **the React app forwards the received response to the browser instead of the backend server**.
3. This way, the origins become the same, so the browser doesn't notice this fact and allows it.

<br/>

## 4. How to Use Proxy

### webpack dev server proxy

1. Webpack dev server proxy settings are originally applied through webpack configuration, but in React projects created through CRA, they're configured to be easily applied by setting the "proxy" value in package.json

```json
  ...
  "browserslist": {
      "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
      ],
      "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
      ]
  },
      "proxy" : "API address to bypass" // proxy is usually written at the bottom for easy finding
  }
```

2. Remove the domain part from the existing fetch or axios request section

```javascript
  export async function getAllfetch() {

      const response = await fetch('API address to bypass/params');
      .then(() => {
              ...
          })
  }

  export async function getAllfetch() {

      const response = await fetch('/params');
      .then(() => {
              ...
          })
  }
```

### React Proxy Usage

- Since the proxy provided by webpack dev server is a global setting, sometimes this method isn't sufficiently applied.
- So there are cases where you need to manually apply proxy, and at this time, use the http-proxy-middleware library

1. Install http-proxy-middleware library

   ```shell
    npm install http-proxy-middleware --save
   ```

2. Create setupProxy.js file inside the src file of React App, import the installed library file, and write as follows

   ```javascript
   const { createProxyMiddleware } = require('http-proxy-middleware');

   module.exports = function (app) {
     app.use(
       '/api', // enter the path parameter that needs proxy
       createProxyMiddleware({
         target: 'http://localhost:5000', // enter the target api url
         changeOrigin: true, // part that sets the host header to change according to the target server configuration
       })
     );
   };
   ```

3. Remove the domain part from the existing fetch or axios request section

   ```javascript
    export async function getAllfetch() {

        const response = await fetch('API address to bypass/params');
        .then(() => {
                ...
            })
    }

    export async function getAllfetch() {

        const response = await fetch('/params');
        .then(() => {
                ...
            })
    }
   ```
