# Express

## 1. What is Express

- A **framework** used to create web servers or API servers in Node.js environment
- Unlike servers written with Node.js HTTP module, middleware can be added and routers are provided

<br/>

## 2. Creating a Simple Web Server

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello World');
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
});
```

<br/>

## 3. Routing

- Creating branching points with methods and URLs
- Clients send HTTP requests (GET, POST, etc.) to specific URIs of the server with specific HTTP request methods, and routing determines how the server responds to these client requests according to the corresponding Endpoint
- Code implementing routing with pure Node.js without additional libraries

  ```javascript
  const requestHandler = (req, res) => {
    if (req.url === '/lower') {
      if (req.method === 'GET') {
        res.end(data);
      } else if (req.method === 'POST') {
        req.on('data', (req, res) => {
          // omitted
        });
      }
    }
  };
  ```

- Intuitive code using Express router

  ```javascript
  const router = express.Router();

  router.get('/lower', (req, res) => {
    res.send(data);
  });

  router.post('/lower', (req, res) => {
    // omitted
  });
  ```
