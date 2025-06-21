# SOP, CORS

## 1. SOP (Same-Origin Policy)

- Same-origin policy that only allows sharing resources from the same origin
- This origin consists of a combination of protocol, host, and port, and if any one of these is different, it's not considered the same origin
- Separates potentially harmful documents and reduces attack paths

<br/>

## 2. CORS (Cross-Origin Resource Sharing)

- Cross-origin resource sharing, uses additional HTTP headers and tells the browser to grant permission for web applications running in one origin to access selected resources from other origins
- In other words, browsers block sharing of resources from other origins by default due to SOP, but using CORS allows access to resources

<br/>

## 3. How CORS Works

### (1) Preflight Request

- Before sending actual request, sends OPTIONS method pre-request to check if there's permission to access resources from that origin
- Can check permissions in advance before sending actual request, making it efficient
- Can protect servers not prepared for CORS, considering that servers made before CORS only receive SOP requests
- But even servers not prepared for CORS will show CORS error when sending preflight request (→ CORS basics)

### (2) Simple Request

- Sends request after omitting preflight request if certain conditions are met
- Conditions:
  - Must be one of `GET`, `HEAD`, `POST` requests
  - Can only manually set values of `Accept`, `Accept-Language`, `Content-Language`, `Content-Type` headers other than automatically set headers
  - `Content-Type` header only allows `application/x-www-form-urlencoded`, `multipart/form-data`, `text/plain` values

### (3) Credentialed Request

- Request that includes authentication information in request headers
- If origins are different, cookies cannot be sent without separate settings
- In this case, CORS settings are needed on both frontend and server sides:
  - Frontend side must put `withCredentials: true` in request headers
  - Server side must put `Access-Control-Allow-Credentials: true` in response headers
  - When setting `Access-Control-Allow-Origin` on server side, error occurs if set with wildcard (\*) meaning allow all origins. Since dealing with authentication information, origins must be set accurately.

<br/>

## 4. CORS Configuration Methods

### (1) Node.js Server

```javascript
const http = require('http');

const server = http.createServer((request, response) => {
  // All domains
  response.setHeader('Access-Control-Allow-Origin', '*');

  // Specific domain
  response.setHeader('Access-Control-Allow-Origin', 'https://naver.com');

  // When receiving requests with authentication information
  response.setHeader('Access-Control-Allow-Credentials', 'true');
});
```

### (2) Express Server

```javascript
const cors = require('cors');
const app = express();

// All domains
app.use(cors());

// Specific domain
const options = {
  origin: 'https://naver.com', // Domain to grant access permission
  credentials: true, // Add Access-Control-Allow-Credentials to response headers
  optionsSuccessStatus: 200, // Set response status to 200
};

app.use(cors(options));

// Specific request
app.get('/example/:id', cors(), function (req, res, next) {
  res.json({ msg: 'example' });
});
```
