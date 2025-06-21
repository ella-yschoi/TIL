# HTML (Hyper Text Markup Language)

## 1. HTML 이란?

웹 페이지의 구조를 짜는 마크업 언어

<br/>

## 마크업 언어란?

- 태그는 원래 텍스트와는 별개로 원고의 교정부호나 주석을 표현하기 위한 것이었으나, 용도가 점차 확장되어 문서의 구조를 표현하는 역할을 하게 되었다. 이러한 태그 방법의 체계를 마크업 언어라고 하는데, 일반적으로 데이터를 기술하는 정도로만 사용 되기 때문에 자바스크립트와 같은 프로그래밍 언어와는 구별된다. [참고: 위키피디아](https://ko.wikipedia.org/wiki/%EB%A7%88%ED%81%AC%EC%97%85_%EC%96%B8%EC%96%B4)
- 태그는 원래 텍스트와는 별개로 원고의 교정부호와 주석을 표현하기 위한 것이었으나, 용도가 점차 확장되어 문서의 구조를 표현하는 역할을 하게 되었다. 이러한 태그 방법의 체계를 마크업 언어라고 한다. 일반적으로 데이터를 기술하는 정도로만 사용되기 때문에 자바스크립트와 같은 프로그래밍 언어와는 구별된다.
- 집을 짓기 위해 도면을 그린다고 생각하면 된다.
- 예를 들어, 웹사이트 상의 로그인 페이지를 만든다고 해보자.
- 그렇다면 기본적으로 아이디와 비밀번호를 입력할 수 있는 입력폼이 필요하겠다. 또한 로그인으로 이어지는 버튼과, 로그인 유지 여부를 물어보는 체크박스도 넣어보자. HTML 코드로 작성하면 위와 같은 화면을 만들 수 있다.

<br/>

## 2. HTML 기본 구조

```html
<!DOCTYPE html> 
이 문서가 HTML 문서임을 명시

<html>
html 시작 태그로, 문서 전체의 틀을 구성

<head>
문서의 메타 데이터를 선언

<title>
문서의 제목, 브라우저 탭에 보여짐

<body>
문서의 내용을 담는 곳

<div>
content division을 의미, 줄바꿈 됨

<span>
줄바꿈 없는 content 컨테이너

<a>
링크 삽입 시 사용

<img>
이미지 삽입 시 사용

<input>
텍스트, 라디오 버튼, 체크버튼 삽입

<button>
버튼 삽입
```

<br/>

## 3. HTML 기본 문법

### 이미지 삽입

```html
<html>
  <head></head>
  <body>
    <div>div 태그는 한 줄을 차지합니다</div>
    <div>division 2</div>
    <span>span 태그는 컨텐츠 크기만큼 공간을 차지합니다</span>
    <span>span 2</span>
    <span>span 3</span>
    <div>division 3</div>
    <img src="https://obj-kr.the1.wiki/data/322eebacb4eca78026616d703becbd9828ecb9b4ecb9b4ec98a4ed9484eba08ceca68820eab3b5ec8b9dec82aceca784292e706e67.png">
    <a href="http://naver.com" target="_blank">네이버 바로가기</a>
  </body>
</html>
```

### ul, li 리스트

- ul: unordered list
- ol: ordered list

```html
<html>
  <head></head>
  <body>
    <ol>
      <li>item 1</li>
      <li>item 2</li>
        <ul>
          <li>item 3</li>
        </ul>
    </ol>
  </body>
</html>
```

### input, textarea

```html
<html>
<head></head>
<body>
  <div>
    ID <input type="text" placeholder="type here">
  </div>
  <div>
    password <input type="password">
  </div>
  <div>
    <input type="checkbox"> 다음 접속 시 아이디 기억하기
  </div>

  <input type="radio" name="option1"> 옵션A
  <input type="radio" name="option1"> 옵션B
  <div>
    <textarea></textarea>
  </div>
  <div>
    <button>로그인</button>
  </div>
</body>
</html>
```

<br/>

## 4. 시맨틱 요소

### 의미

- sementic: 의미가 있는
- ex. top level heading을 표현할 때 사용하는 요소인 `<h1>` 요소를 사용할 경우, 브라우저가 큰 폰트 사이즈를 적용할 뿐 아니라, 위아래로 간격을 주어 제목처럼 보이도록 함

### 사용하는 이유

- 검색엔진이 시맨틱 요소를 더 좋아하기 때문 → 시맨틱 요소에 담긴 의미에 따라 검색 결과 상위 노출이 결정될 수 있다는 것임
- 여러 개발자가 함께 작업할 때 `<div>` 요소를 탐색하는 것보다 의미있는 코드 블록을 찾는 것이 훨씬 더 편리하고, 요소 안에 채워질 데이터 유형 예측도 쉬움
- 따라서, HTML 요소 작성 시, 작성할 데이터를 가장 잘 설명할 수 있는 요소는 무엇일지 고려 필요

### 주요 사용되는 요소들

```html
<article>
독립적이고 자체 포함된 컨텐츠 지정

<aside>
본문의 주요 부분을 표시하고 남은 부분을 설명, 특별한 일이 아닌 이상 사이드바나 광고창 등 중요하지 않은 부분에 사용

<footer> 
일반적으로 페이지나 해당 파트의 가장 아랫부분에 위치. 사이트의 라이선스, 주소, 연락처를 넣을 때 사용

<header>
페이지나 섹션의 가장 윗부분, 사이트의 제목이 포함되거나 상단바, 검색창이 들어갈 수도

<nav>
일반적으로 상단바 등 사이트를 안내하는 요소이며, 보통은 안에 <ul>을 넣어 목록 형태로 사용

<main>
문서의 주된 컨텐츠 표시
```

<br/>

## 5. 각 영역에 이름 붙여주기

### id

고유한(unique) 이름을 붙일 때. 한번만, 사실 드물게 사용됨

```html
<!--HTML-->
<div id=”wrting-selection”>
```

```css
/* css */
div#writing-section
```

### class

- 반복되는 영역을 유형별로 분류할 때. 여러 개.
- 반복적으로 사용되는 요소를 유형별로 분류할 때 사용함. 따라서 같은 class를 가지고 있는 요소는 같은 유형으로 분류된 요소라는 것을 유추할 수 있음
- 단 한 번만 사용되어야 하는 이름이 필요한 경우에는 class가 아닌 id를 사용해야 함!

```html
<!--HTML-->
<li class=”comment”>
```

```css
/* css */
li.comment
```
