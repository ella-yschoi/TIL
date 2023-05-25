## **SOP, CORS**
### 1. SOP(Same-Origin Policy) 
- 동일 출처 정책으로, **같은 출처의 리소스만 공유 가능**함. 
- 이 출처는 프로토콜, 호스트, 포트의 조합으로 이루어져 있는데 이 중 하나라도 다르면 동일한 출처로 보지 않음.
- 잠재적으로 해로울 수 있는 문서를 분리해 공격받을 수 있는 경로를 줄여줌

<br/>

### 2. CORS(Cross-Origin Resource Sharing)
- 교차 출처 리소스 공유이며, 추가 HTTP 헤더를 사용하고 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제
- 즉, 브라우저는 SOP에 의해 기본적으로 다른 출처의 리소스 공유를 막지만, CORS를 사용하면 접근 권한을 얻을 수 있게 되는 것

<br/>

### 3. CORS의 동작 방식
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

<br/>

### 4. CORS 설정 방법
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