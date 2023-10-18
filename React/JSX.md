# JSX

## 1. JSX란?

- React에서 UI를 구성할 때 사용하는 **JavaScript를 확장한 문법**이며, 이를 활용해 **React element**를 만들 수 있음
- 'Babel'로 JSX를 브라우저가 이해할 수 있는 JavaScript로 compile -> JavaScript를 브라우저가 읽고 화면에 렌더링 가능
- React에서는 DOM과는 다르게 CSS, JSX 문법만으로 웹 애플리케이션 개발 가능. 즉, JavaScript만으로 마크업 형태의 코드를 작성하여 DOM에 배치 가능 (단, JSX는 HTML이 아니기에 Babel로 compile 필요)

<br/>

## 2. JSX 문법

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

- 엘리먼트 클래스 사용 시, **className**으로 표기

  ```jsx
  <div className = "greeting">Hello</div>
  ```

- JavaScript 표현식 사용 시, **중괄호** 이용

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

- 사용자 정의 컴포넌트는 **대문자로 시작**

  ```jsx
  function Hello() {
    return <div>Hello!</div>
  }
  
  function HelloWorld() {
    return <Hello />;
  }
  ```

- 조건부 렌더링에는 if문이 아닌, **삼항연산자** 사용

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
