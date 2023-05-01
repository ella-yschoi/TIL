## **웹 표준**
### 1. 웹 표준의 개념
- 인터넷은 웹보다 더 포괄적인 개념
  - 인터넷: 전 세계적으로 연결되어 있는 컴퓨터 네트워크 통신망이며, 웹 뿐만 아니라 온라인 게임, 모바일 앱, 이메일 등 **네트워크를 사용하는 다양한 서비스 모두 포함**
  - 웹: 문서, 이미지, 영상 등 다양한 정보를 여러 사람과 공유할 수 있는 **공간**
- 웹 표준
  - W3C에서 권고하는 '웹에서 표준적으로 사용되는 기술이나 규칙'
  - 사용자가 어떠한 운영체제나 브라우저를 사용하더라도 웹 페이지가 동일하게 보이고 작동할 수 있도록 하는 웹 페이지 제작 기법
- 웹 표준의 장점
  1. 유지 보수의 용이성
  2. 웹 호환성 확보
  3. 검색 효율성 증대
  4. 웹 접근성 향상

### 2. Semantic HTML
- 시맨틱 요소
  - 요소가 어떤 내용을 담게 될지, 어떤 기능을 하게 될지 확실하게 의미를 가지고 있는 요소
  - 시맨틱 요소를 적절하게 사용해 구성한 HTML → 시맨틱 HTML
- 시멘틱 HTML의 필요성
  - 개발자 간 소통
  - 검색 효율성
  - 웹 접근성
- 자주 사용되는 시맨틱 요소들
  - `<header>`: 페이지나 요소의 최상단에 위치하는 머리말 역할의 요소
  - `<nav>`: 메뉴, 목차에 사용되는 요소
  - `<aside>`: 문서와 연관은 있으나 직접적인 연관은 없는 내용을 담는 요소
  - `<main>`: 문서의 메인이 되는 주요 컨텐츠
  - `<article>`: 게시글, 기사 등 독립적으로 구분해 재사용할 수 있는 부분. 각각의 `<article>`을 구분하기 위한 수단이 필요하며 보통 제목 `<hgroup>`을 포함하는 방법 사용
  - `<section>`: 문서의 독립적인 구획을 나타내며, 적합한 의미의 요소가 없을 때 사용. 제목 `<hgroup>`을 포함하는 경우가 많음
  - `<hgroup>`: 제목을 표시할 때 사용하는 요소
  - `<footer>`: 페이지나 요소의 최하단에 위치

### 3. 자주 틀리는 마크업
1. 인라인 요소 안에 블록 요소 넣기
   - 인라인 요소: 콘텐츠가 차지하는 만큼만 (ex. `<span>`, `<label>`)
   - 블록 요소: 가로로 넓게 화면 영역을 차지 (ex. `<div>`, `<h1>`)
2. `<b>`, `<i>` 요소 사용하기
   - `<b>` → `<strong>`
   - `<i> `→ `<em>`
3. `<hgroup>` 마구잡이로 사용하기
   - 시맨틱 요소로서의 역할 및 컨텐츠의 상하관계 표시 목적을 간과한 채 스타일을 적용하기 위한 목적으로는 X
   - 즉, `<h1>`은 `<h2>`와 `<h3>` 상위에 있어야 하며, 그 반대는 X
4. `<br/>` 연속으로 사용하기
   - 요소 사이에 여백을 주고 싶을 때는 `<p>`요소를 사용해 아예 별도의 단락으로 구분하거나 CSS 속성으로 여백 설정하기
5. 인라인 스타일링 사용하기
   - 웹 표준을 지키기 위해서는 HTML과 CSS 코드 분리하여 작성할 것

### 4. 크로스 브라우징
- 크로스 브라우징 이란?
  - 웹 사이트에 접근하는 브라우저의 종류에 상관 없이 **동등한** 화면과 기능을 제공할 수 있도록 만드는 작업
  - 브라우저마다 렌더링 엔진이 다르기에 모든 브라우저에서 완전히 똑같은 화면이 보이도록 하는 것은 X
- 크로스 브라우징 워크 플로우
  1. 초기 기획: 어떤 컨텐츠와 기능, 디자인, 타겟 고객층은 누구인지
  2. 개발: 코드 작성시 코드가 각 브라우저에서 호환성이 어떤지 파악 후 사용
  3. 테스트/발견: TestComplete, LambdaTest, BitBar 등의 크로스 브라우징 테스트 툴 사용 가능
  4. 수정/ 반복

