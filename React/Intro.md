 ## **1. 리액트란?** ##
- 프론트엔드 개발을 위한 JavaScript 오픈소스 라이브러리
- 주요한 세 가지 특징
  - (1) 선언형: 하나의 파일에 명시적으로 작성할 수 있게 JSX를 활용한 선언형 프로그래밍 지향
  - (2) 컴포넌트 기반: 하나의 기능 구현을 위해 여러 종류의 코드를 묶어둔 컴포넌트를 기반으로 개발, 컴포넌트로 분리하면 서로 독립적이고 재사용이 가능하기에 기능 자체에 집중하여 개발 가능
  - (3) 범용성: JavaScript 프로젝트 어디든 유연하게 적용 가능, facebook에서 관리되어 안정적, 리액트 네이티브로 모바일 개발 가능

<br/><p>

## **2. JSX란?** ##
- React에서 UI를 구성할 때 사용하는 JavaScript를 확장한 문법이며, 이를 활용해 React element를 만들 수 있음
- 'Babel'로 JSX를 브라우저가 이해할 수 있는 JavaScript로 compile -> JavaScript를 브라우저가 읽고 화면에 렌더링 가능
- React에서는 DOM과는 다르게 CSS, JSX 문법만으로 웹 애플리케이션 개발 가능. 즉, JavaScript만으로 마크업 형태의 코드를 작성하여 DOM에 배치 가능 (단, JSX는 HTML이 아니기에 Babel로 compile 필요)

<br/><p>

## **3. JSX 문법** ##
- 하나의 엘리먼트 안에 모든 엘리먼트가 포함. 최상위에서 opening tag와 closing tag로 감싸주어야 함
  ```jsx
  <div>
    <div>
        <h1>Hello</h1>
    </div>
    <div>
        <h2>World</h2>
    </div>
  </div>
  ```

- 엘리먼트 클래스 사용 시, className으로 표기
  ```jsx
  <div className = "greeting">Hello</div>
  ```
 
- JavaScript 표현식 사용 시, 중괄호 이용
  ```jsx
  function App () {
    const name = 'Ella Choi';
    return (
        <div>
        Hello, {name}!
        </div>
    );
  }
  ```

- 사용자 정의 컴포넌트는 대문자로 시작
  ```jsx
  function Hello() {
    return <div>Hello!</div>
  }
  
  function HelloWorld() {
    return <Hello />;
  }
  ```

- 조건부 렌더링에는 if문이 아닌, 삼항연산자 사용
  ```jsx
  <div>
    {
        (1+1 === 2) ? (<p>정답</p>) : <p>탈락</p>)
    }
  </div>
  ```

- 여러 개의 HTML 엘리먼트를 표시할 때, map()함수 사용하며, 반드시 'key'JSX 속성을 넣어야 함.
  ```jsx
  const posts = [
    {id: 1, title: 'Hello World', content: 'Welcome to learning React!'},
    {id: 2, title: 'Installation', content: 'You can install React from npm'}
  ];

  function Blog() {
    const content = posts.map((post) =>
        <div key = {post.id}>
        <h3>{post.title}</h3>
        <p>{post.content}</p>
        </div>
    );
    return (
        <div>
        {content}
        </div>
    );
  }
  ```

- 배열의 각 요소는 각각 변수에 담길 수 있는 하나의 JSX 표현식임.
  ```jsx
  const Hello - () => {
    return (
      [<div>안녕하세요</div>, <div>반갑습니다</div>]
    )
  }
  ```
<br/><p>

## **4. 컴포넌트 기반 개발** ##
- 정의: 하나의 기능 구현을 위한 여러 종류의 코드 묶음이자, UI를 구성하는 필수 요소
- 특징
  - 컴포넌트를 여러 개 만들고 조합하면 application 제작 가능
  - React Application은 컴포넌트들의 관계를 트리구조로 형상화하여 표현 가능
  - 트리구조에서 각각의 컴포넌트는 각자의 고유 기능을 가지고 있으면서도 UI의 한 부분 담당