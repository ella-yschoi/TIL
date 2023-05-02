## **웹 애플리케이션 아키텍처** ##
### 1. 클라이언트-서버 아키텍처
   - 상품 정보와 같은 리소스가 존재하는 곳과, 리소스를 사용하는 앱을 분리시킨 것을 2티어 아키텍처
   - 클라이언트: 리소스를 사용하는 앱
   - 서버: 리소스를 제공하는 곳

<br/>

### 2. 클라이언트와 서버의 특징
   - 클라이언트와 서버는 요청과 응답을 주고받는 관계
   - 클라이언트 - 서버 아키텍처에서는 요청이 선행되고 그 이후에 응답이 옴
   - 서버는 리소스만 전달해주는 역할
   - 리소스를 저장하는 공간을 데이터 베이스라고 부르며, DB가 추가된 형태를 3티어 아키텍처라고 부름

<br/>

### 3. 클라이언트와 서버의 종류
   - 클라이언트는 플랫폼에 따라 구별됨
     - 브라우저를 통해 주로 이용하는 웹 플랫폼에서의 클라이언트: 웹사이트 or 웹앱
     - iOS, 안드로이드 등 앱도 클라이언트가 될 수 있음
   - 서버는 무엇을 하느냐에 따라 달라짐 (메일서버, 파일서버, 웹서버 등)

<br/>

### 4. 클라이언트 - 서버 통신과 API
   - 웹 애플리케이션 아키텍처에서는 클라이언트와 서버가 HTTP라는 프로토콜을 이용해 대화함
   - 이때, 서버는 클라이언트에게 리소스를 잘 활용할 수 있도록 인터페이스를 제공하는데, 이를 API(Application Programming *Interface)라고 함 (*Interface: 의사소통이 가능하도록 만들어진 접점)
   - API 문서를 작성해야 클라이언트가 이를 활용할 수 있음