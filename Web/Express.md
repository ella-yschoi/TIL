# Express

## 1. Express란

- Node.js 환경에서 웹 서버 또는 API 서버를 제작하기 위해 사용되는 **프레임워크**
- Node.js HTTP 모듈로 작성한 서버와는 다르게, 미들웨어 추가 가능 및 라우터 제공
  
<br/>

## 2. 간단한 웹 서버 만들기

```javascript
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
res.send('Hello World')
})

app listen(port, () => {
console.log(`Example app listening on port ${port}`)
})
```

<br/>

## 3. 라우팅

- 메소드와 url로 분기점을 만드는 것
- 클라이언트는 특정한 HTTP 요청 메소드와 함께 서버의 특정 URI로 HTTP 요청(GET, POST 등)을 보내는데, 라우팅은 이러한 클라이언트의 요청에 해당하는 Endpoint에 따라 서버가 응답하는 방법을 결정하는 것
- 추가 라이브러리 없이 순수 Node.js로 라우팅을 구현한 코드

    ```javascript
    const requestHandler = (req, res) => {
        if(req.url === '/lower') {
            if(req.method === 'GET') {
                res.end(data)
            } else if(req.method === 'POST') {
                req.on('data', (req, res) => {
                    // 생략
                })
            }
        }
    }
    ```

- Express의 라우터를 활용한 직관적인 코드

    ```javascript
    const router = express.Router()

    router.get('/lower', (req, res) => {
        res.send(data);
    })

    router.post('/lower', (req, res) => {
        // 생략
    })
    ```
