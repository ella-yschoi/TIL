# **Cookie 🍪**

## 1. 쿠키란?

- 서버에서 클라이언트에 영속성 있는 데이터를 저장하는 방법
- 서버가 웹 브라우저에 정보를 저장하고 불러올 수 있는 수단
- 해당 도메인에 대해 쿠키가 존재하면, 웹 브라우저는 도메인에게 http 요청 시 쿠키를 함께 전달
- 서버에서 클라이언트에 전송하는 것 뿐만 아니라, 클라이언트에서 서버로 쿠키를 다시 전송하는 것도 포함
- 다만, 데이터를 저장한 이후 http 헤더 설정 등 **특정 조건들이 만족되어야 다시 가져올 수 있음**

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

## 2. 쿠키 옵션 종류

1. **Domain**
   - `www.google.com`과 같이 서버에 접속할 수 있는 이름
   - 포트 및 서브 도메인 정보, 세부 경로 등을 포함하지 않음
   - 클라이언트에서는 쿠키의 도메인 옵션과 서버의 도메인이 일치해야 쿠키 전송 가능
   - `http://www.localhost.com:3000/users/login` 에서 Domain은 `localhost.com`

2. **Path**
   - 세부 경로로서 서버가 라우팅할 때 사용하는 경로
   - 설정된 경로를 포함하는 하위 경로로 요청해도 쿠키를 서버에 전송 가능
   - `http://www.localhost.com:3000/users/login` 에서 Path는 `/users/login`

3. **MaxAge or Expires**
   - 쿠키가 유효한 기간을 정하는 옵션
   - MaxAge는 쿠키가 유효한 시간을 초 단위로 설정하는 옵션
   - Expires는 (클라이언트 시간 기준) 쿠키가 유효한 시간과 날짜
   - 세션 쿠키(Session Cookie)
     - MaxAge 또는 Expires 옵션이 없는 쿠키
     - 브라우저가 실행 중일 때 사용할 수 있는 임시 쿠키
     - 브라우저를 종료하면 해당 쿠키는 삭제
   - 영속성 쿠키(Persistent Cookie)
     - 브라우저의 종료 여부와 상관없음
     - MaxAge 또는 Expires에 지정된 유효시간만큼 사용가능한 쿠키
  
4. **Secure**
   - 사용하는 프로토콜에 따른 쿠키 전송 여부를 결정하는 옵션
   - 옵션이 `true`인 경우 HTTPS를 이용하는 경우에만 쿠키 전송 가능
   - secure 옵션이 없다면 프로토콜에 상관 없이 http든 https든 모두 쿠키 전송 가능
   - 단, 도메인이 `localhost`인 경우 https가 아니어도 쿠키 전송 가능

5. **HttpOnly**
   - 자바스크립트로 브라우저 쿠키에 접근이 가능한지 여부 결정
   - 클라이언트에서 DOM을 이용해 쿠키에 접근하는 것을 막아주는 옵션
   - 사용하는 프로토콜에 따른 쿠키 전송 여부를 결정하는 옵션
   - 디폴트 false로 지정되고 옵션이 `true`인 경우, 자바스크립트로 쿠키에 접근 불가
   - 만약 `false`인 경우, `document.cookie`를 이용해 쿠키가 탈취될 위험이 있음

6. **SameSite**
   - Cross-site 요청을 받은 경우, 요청에서 사용한 메소드와 해당 옵션의 조합을 기준으로 쿠키 전송 여부 결정
   - Cross-origin
     - 서버의 도메인, 프로토콜, 포트 중 하나라도 다른 경우 Cross-origin으로 구분
   - Cross-site
     - eTLD+1이 다른 경우 (*eTLD+1: 최상위 도메인의 바로 왼쪽 하위 레벨 도메인을 합한 것)
   - SameSite 옵션에서 사용할 수 있는 속성
     - Lax: Cross-Site 요청이라면 GET 메서드에 대해서만 쿠키 전송 가능
     - Strict: Cross-Site가 아닌 Same-Site인 경우에만 쿠키를 전송
     - None: 항상 쿠키를 보내줄 수 있으나, Secure 옵션 필요

<br/>

## 3. 쿠키를 이용한 상태 유지

- 쿠키의 특성을 이용해 stateless한 인터넷 연결을 stateful하게 유지 가능
- 다만, 기본적으로 쿠키는 오랜 시간 동안 유지될 수 있고, HttpOnly 옵션을 사용하지 않았다면 자바스크립트로 쿠키 접근이 가능하므로 쿠키에 민감한 정보를 담는 것은 위험
