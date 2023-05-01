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