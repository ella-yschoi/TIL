## **1. CORS**
### 1. SOP, CORS
1. SOP(Same-Origin Policy) 
- 동일 출처 정책으로, **같은 출처의 리소스만 공유 가능**함. 
- 이 출처는 프로토콜, 호스트, 포트의 조합으로 이루어져 있는데 이 중 하나라도 다르면 동일한 출처로 보지 않음.
- 잠재적으로 해로울 수 있는 문서를 분리해 공격받을 수 있는 경로를 줄여줌

2. CORS(Cross-Origin Resource Sharing)
- 교차 출처 리소스 공유이며, 추가 HTTP 헤더를 사용하고 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제
- 즉, 브라우저는 SOP에 의해 기본적으로 다른 출처의 리소스 공유를 막지만, CORS를 사용하면 접근 권한을 얻을 수 있게 되는 것

### 2. CORS의 동작 방식
1. 프리플라이트 요청(Preflight Request)
- 실제 요청을 보내기 전, OPTIONS 메소드로 **사전 요청**을 보내 해당 출처 리소스에 **접근 권한이 있는지부터 확인**
- 실제 요청을 보내기 전에 미리 권한 확인이 가능해 효율적
- CORS에 대비가 되지 않은 서버 보호 가능, CORS 이전에 만들어진 서버들은 SOP 요청만 들어오는 상황을 고려
- 하지만 CORS에 대비가 되지 않은 서버라도 프리플라이트 요청을 보내면 CORS 에러를 띄움( → CORS 기본사항)

2. 단순 요청(Simple Request)
- 특정 조건이 만족되면 프리플라이트 요청 생략 후 요청을 보내는 것
- 조건
  - `GET`, `HEAD`, `POST` 요청 중 하나여야 함
  - 자동으로 설정되는 헤더 외에, `Accept`, `Accept-Language`, `Content-Language`, `Content-Type` 헤더의 값만 수동으로 설정 가능
  - `Content-Type` 헤더에는 `application/x-www-form-urlencoded`, `multipart/form-data`, `text/plain` 값만 허용

3. 인증정보를 포함한 요청(Credentialed Request)
- 요청 헤더에 인증정보를 담아 보내는 요청
- 출처가 다를 경우 별도의 설정을 하지 않으면 쿠키를 보낼 수 없음
- 이 경우, 프론트/서버 양 측 모두 CORS 설정이 필요함
  - 프론트 측에서는 요청 헤더에 `withCredentials : true` 를 넣어줘야 함
  - 서버 측에서는 응답 헤더에 `Access-Control-Allow-Credentials : true` 를 넣어줘야 함
  - 서버 측에서 `Access-Control-Allow-Origin` 을 설정할 때, 모든 출처를 허용한다는 뜻의 와일드카드(*)로 설정하면 에러 발생. 인증 정보를 다루는 만큼 출처를 정확하게 설정해주어야 함.

### 3. CORS 설정 방법
1. Node.js 서버
   ```javascript
    const http = require('http');

    const server = http.createServer((request, response) => {
    // 모든 도메인
    response.setHeader("Access-Control-Allow-Origin", "*");

    // 특정 도메인
    response.setHeader("Access-Control-Allow-Origin", "https://naver.com");

    // 인증 정보를 포함한 요청을 받을 경우
    response.setHeader("Access-Control-Allow-Credentials", "true");
    })
   ```

2. Express 서버
   ```javascript
    const cors = require("cors");
    const app = express();

    //모든 도메인
    app.use(cors());

    //특정 도메인
    const options = {
    origin: "https://naver.com", // 접근 권한을 부여하는 도메인
    credentials: true, // 응답 헤더에 Access-Control-Allow-Credentials 추가
    optionsSuccessStatus: 200, // 응답 상태 200으로 설정
    };

    app.use(cors(options));

    //특정 요청
    app.get("/example/:id", cors(), function (req, res, next) {
    res.json({ msg: "example" });
    });
   ```
<br/><br/>

## **2. Refactor Express**
### 1. Express 시작하기
1. Express란
- Node.js 환경에서 웹 서버 또는 API 서버를 제작하기 위해 사용되는 프레임워크
- Node.js HTTP 모듈로 작성한 서버와는 다르게
  - (1) 미들웨어 추가 가능
  - (2) 라우터 제공

2. 간단한 웹 서버 만들기
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

3. 라우팅
   - **메소드와 url로 분기점을 만드는 것**
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

### 2. Middleware
1. 미들웨어란?
   - 자동차 공장의 공정과 비슷, 요청에 필요한 기능을 더하거나, 문제가 발견된 것을 밖으로 걷어내는 역할
   - Express의 큰 장점
   - Node.js만으로 구현한 서버에서는 번거로울 수 있는 작업을 보다 쉽게 적용 가능
  
2. 미들웨어를 사용하는 상황
   1. POST 요청 등에 포함된 **body(payload)를 구조화**할 때 (쉽게 얻어내고자 할 때)
    - Node.js로 HTTP 요청 body를 받는 코드
        ```javascript
        let body = [];
        request.on('data', (chunk) => {
            body.push(chunk);
        }).on('end',() => {
            body = Buffer.concat(body).toString();
            // body 변수에는 문자열 형태로 payload가 담김
            // 네트워크 상의 chunk를 합치고, buffer를 문자열로 변환
        })
        ```
    - body-parser 미들웨어를 사용한 코드
        ```javascript
        const bodyParser = require('body-parser');
        const jsonParser = bodyParser.json();
        // 생략
        app.post('/users', jsonParser, function(req, res) {

        })
        ```
    - Express v4.16.0부터는 body-parser를 설치하지 않고 내장 미들웨어인 express.json() 사용
        ```javascript
        const jsonParser = express.json();
        // 생략
        app.post('/api/users', jsonParser, function(req, res) {

        })
        ```
    - express.json() 미들웨어 사용에 에러가 난다면? → options에 {strict: false}를 추가
        ```javascript
        const jsonParser = express.json({strict: false});
        // 생략
        app.post('/api/users', jsonParser, function(req, res){

        })
        ```
   2. 모든 요청/응답에 **CORS 헤더**를 붙여야 할 때
    - Node.js에 CORS를 적용하기
        ```javascript
        // 라우팅마다 헤더를 넣어주어야 함
        const defaultCorsHeader = { 
            'Access-Control-Allow-Origin': '*',
            'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
            'Access-Control-Allow-Headers': 'Content-Type, Accept',
            'Access-Control-Max-Age': 10
        };
        // 생략

        // OPTIONS 메소드에 대한 라우팅도 따로 구현해야 함
        if (req.method === 'OPTIONS') {
            res.writeHead(200, deaultCorsHeader);
            res.end()
        }
        ```
    - cors 미들웨어 사용: 모든 요청에 CORS 허용
        ```javascript
        cons cors = require('cors');
        // 생략
        app.use(cors());
        ```
    - cors 미들웨어 사용: 특정 요청에 CORS 허용
        ```javascript
        const cors = require('cors')
        // 생략
        app.get('/products/:id', cors(), function(req, res, next) {
            res.json({msg: 'This is CORS-enabled for a Single Route'})
        })
        ```
   3. 모든 요청에 대해 **url이나 메소드를 확인**할 때
   - use 메소드로 모든 요청에 대해 미들웨어 적용
        ```javascript
        const express = require('express');
        const app = express();

        const myLogger = function (req, res, next) {
            console.log('LOGGED');
            next();
        };
        
        app.use(myLogger);

        app.get('/', function(req, res) {
            res.send('Hello World');
        });

        app.listen(3000);
        ```
   4. 요청 헤더에 **사용자 인증 정보**가 담겨있는지 확인할 때
   - HTTP 요청에 토큰이 있는지 판단하여, 이미 로그인한 사용자일 경우 성공, 아닐 경우 에러
        ```javascript
        app.use((req, res, next) => {
            // 토큰이 있는지 확인
            if(req.headers.token) {
                req.isLoggedIn = true;
                next();
            } else {
                res.status(400).send('invalid users')
            }
        })
        ```