# Proxy

## 1. CORS 정책이 필요한 이유

- 브라우저에서는 기본적으로 API를 요청할 때에, 브라우저의 현재 주소와 API의 주소의 도메인이 일치해야만 데이터를 접근할 수 있게 되어 있음
- 구축한 클라이언트 뒤의 서버와 연결된 DB에는 live data는 민감성이 높은 데이터들이 위주이기 때문에 보안이 무엇보다 중요
- 만약 서비스가 모든 출처의 접근을 허락한다면 해킹의 위험에 노출될 수 있기에 **모든 도메인을 허용해서는 안 되고, 특정 도메인을 허용하도록 구현**해야 함.
- 따라서 프론트엔드 개발자가 백엔드 개발자에게 프론트엔드 개발 서버 도메인을 허용해 달라고 요청을 해야 하고,
- 백엔드 개발자는 응답 헤더에 필요한 값들을 담아서 전달을 해줘야 함.
- 서버에서 적절한 응답 헤더를 받지 못하면 브라우저에서 에러가 발생하기 때문

<br/>

## 2. Proxy

- 위의 정석적인 과정 없이 React 라이브러리, 혹은 Webpack Dev Server에서 제공하는 proxy 기능을 사용하면 CORS 정책 우회 가능
- 즉, **별도의 응답 헤더를 받을 필요 없이 브라우저는 React 앱으로 데이터를 요청하고, 해당 요청을 백엔드로 전달하게 되는 것**.
- 여기서 React 앱이 서버로부터 받은 응답 데이터를 다시 브라우저로 전달하기에, 브라우저는 CORS 정책을 위반했는지 모르게 됨.
- 즉, 브라우저를 proxy 기능을 통해 속이는 것.

<br/>

## 3. Proxy 작동 흐름

### proxy 적용 전 흐름

  ![proxy_before](/Images/proxy_before.png)

1. 프론트엔드에서 개발한 React 앱에서 브라우저 쪽으로 요청을 보냄
2. 브라우저는 백엔드, 즉 서버 쪽으로 리소스를 요청함. 이때 접근 권한이 있는지, 즉 출처가 같은지 확인하는데 이때 백엔드 서버는 정상적으로 200 OK 응답을 브라우저에게 보냄.
3. 브라우저는 받은 리소스 및 응답과 함께 출처가 같은지 아닌지 확인하게 되는데, 이때 출처가 다르다면 응답을 파기(CORS Error) 하고, 출처가 같다면 응답을 파기하지 않고 다시 프론트엔드 쪽으로 응답을 보내주는 것임.

### proxy 적용 후 흐름

  ![proxy_after](/Images/proxy_after.png)

1. React 앱에서 브라우저를 통해 API를 요청할 때, **proxy를 통해 백엔드 서버로 요청을 우회**하여 보냄
2. **백엔드 서버는 응답을 React 앱으로** 보내고, **React 앱은 받은 응답을 백엔드 서버 대신 브라우저에게 전달**함.
3. 이렇게 되면 출처가 같아지기 때문에 브라우저는 이 사실을 눈치채지 못하고 허용하게 됩니다.

<br/>

## 4. Proxy 사용법

### webpack dev server proxy

1. 웹팩 개발서버의 proxy 설정은 원래 웹팩 설정을 통해서 적용하지만, CRA를 통해 만든 리액트 프로젝트에서는 package.json 에서 "proxy" 값을 설정하여 쉽게 적용할 수 있도록 구성됨

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
        "proxy" : "우회할 API 주소" // proxy는 보통 맨 밑에 작성해 금방 찾을 수 있도록 함
    }
  ```

2. 기존의 fetch, 혹은 axios를 통해 요청하던 부분에서 도메인 부분을 제거

  ```javascript
    export async function getAllfetch() {

        const response = await fetch('우회할 api주소/params');
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

### React Proxy 사용법

- webpack dev server에서 제공하는 proxy는 전역적인 설정이기에, 종종 해당 방법이 충분히 적용되지 않는 경우가 생기기도 함.
- 그래서 수동으로 proxy를 적용해줘야 하는 경우가 있는데, 이때는 http-proxy-middleware 라이브러리를 사용

1. http-proxy-middleware 라이브러리 설치

   ```shell
    npm install http-proxy-middleware --save
   ```

2. React App의 src 파일 안에서 setupProxy.js 파일 생성 후, 안에서 설치한 라이브러리 파일을 불러온 다음, 아래와 같이 작성

   ```javascript
    const { createProxyMiddleware } = require('http-proxy-middleware');

    module.exports = function(app) {
    app.use(
        '/api', // proxy가 필요한 path prameter를 입력
        createProxyMiddleware({
        target: 'http://localhost:5000', // 타겟이 되는 api url를 입력
        changeOrigin: true, // 대상 서버 구성에 따라 호스트 헤더가 변경되도록 설정하는 부분
        })
    );
    };
   ```

3. 기존의 fetch, 혹은 axios를 통해 요청하던 부분에서 도메인 부분을 제거

   ```javascript
    export async function getAllfetch() {

        const response = await fetch('우회할 api주소/params');
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
