# Middleware

## 1. What is Middleware?

- Similar to automobile factory processes, adds necessary functionality to requests or removes problematic items
- One of Express's biggest advantages
- Can easily apply tasks that might be cumbersome in servers implemented with Node.js alone

<br/>

## 2. Situations When Using Middleware

### (1) When structuring body (payload) included in POST requests (when you want to easily extract it)

#### Code to receive HTTP request body with Node.js

```javascript
let body = [];
request
  .on('data', (chunk) => {
    body.push(chunk);
  })
  .on('end', () => {
    body = Buffer.concat(body).toString();
    // payload is contained in body variable as string
    // combine chunks on network and convert buffer to string
  });
```

#### Code using body-parser middleware

```javascript
const bodyParser = require('body-parser');
const jsonParser = bodyParser.json();
// ... omitted
app.post('/users', jsonParser, function (req, res) {});
```

#### From Express v4.16.0, use built-in middleware express.json() without installing body-parser

```javascript
const jsonParser = express.json();
// ... omitted
app.post('/api/users', jsonParser, function (req, res) {});
```

#### If there's an error using express.json() middleware? → Add {strict: false} to options

```javascript
const jsonParser = express.json({ strict: false });
// ... omitted
app.post('/api/users', jsonParser, function (req, res) {});
```

### (2) When CORS headers need to be attached to all requests/responses

#### Applying CORS to Node.js

```javascript
// Need to add headers to each routing
const defaultCorsHeader = {
  'Access-Control-Allow-Origin': '*',
  'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
  'Access-Control-Allow-Headers': 'Content-Type, Accept',
  'Access-Control-Max-Age': 10,
};
// ... omitted

// Need to implement routing for OPTIONS method separately
if (req.method === 'OPTIONS') {
  res.writeHead(200, defaultCorsHeader);
  res.end();
}
```

#### Using cors middleware: Allow CORS for all requests

```javascript
const cors = require('cors');
// ... omitted
app.use(cors());
```

#### Using cors middleware: Allow CORS for specific requests

```javascript
const cors = require('cors');
// ... omitted
app.get('/products/:id', cors(), function (req, res, next) {
  res.json({ msg: 'This is CORS-enabled for a Single Route' });
});
```

### (3) When checking URL or method for all requests

#### Apply middleware to all requests using use method

```javascript
const express = require('express');
const app = express();

const myLogger = function (req, res, next) {
  console.log('LOGGED');
  next();
};

app.use(myLogger);

app.get('/', function (req, res) {
  res.send('Hello World');
});

app.listen(3000);
```

### (4) When checking if user authentication information is contained in request headers

#### Determine if there's a token in HTTP request, return success if already logged in user, error if not

```javascript
app.use((req, res, next) => {
  // Check if there's a token
  if (req.headers.token) {
    req.isLoggedIn = true;
    next();
  } else {
    res.status(400).send('invalid users');
  }
});
```
