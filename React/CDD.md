# Component Driven Development

## 1. Component Driven Development란?

### CDD란?

- 부품 단위로 UI 컴포넌트를 만들어 나가는 개발 진행 가능
- 컴포넌트 단위로 만들어 페이지를 조립하는 개발 방식인 상향식 개발에 가까움

### CSS in JS

- CSS 구조화를 위한 다양한 시도
  - SASS라는 CSS를 확장해 주는 스크립팅 언어로 전처리기 활용했으나, 컴파일 된 CSS용량이 커졌음
- SASS의 문제를 보완하기 위해 아래의 지향점들을 가진 다양한 CSS 방법론이 대두되었음
  - 코드의 재사용
  - 코드의 간결화 (유지보수 용이)
  - 코드의 확장성
  - 코드의 예측성 (클래스 명 등으로)
  - Styled-Component: 상태를 가진 컴포넌트들로부터 UI를 완전히 분리해 사용할 수 있는 아주 단순한 패턴을 제공

<br/>

## 2.CDD 개발도구

### Styled Components

CSS를 컴포넌트화 하는 라이브러리로, React 환경에서 사용 가능하며, CSS를 Javascript안에 넣어줄 수 있음

#### Styled Components 설치하기

```javascript
// package.json에 코드 추가
{
"resolutions": {
  "styled-components": "^5"
  }
}
```

#### Styled Components를 사용할 파일로 불러와주기

```javascript
import styled from "styled-components"
```

#### 컴포넌트 만들기

```javascript
// 따옴표가 아닌 백 틱(`)을 사용
import styled from "styled-components";

// Styled Components로 컴포넌트를 만들고
const BlueButton = styled.button`
  background-color: blue;
  color: white;
`;

export default function App () {
  // React 컴포넌트를 사용하듯 사용
  return <BlueButton>Blue Button</BlueButton>;
}
```

#### 컴포넌트를 재활용해 새로운 컴포넌트 만들기

```javascript
import styled from "styled-components";

const BlueButton = styled.button`
  background-color: blue;
  color: white;
  `;

// 만들어진 컴포넌트를 재활용해 컴포넌트 만들기
const BigBlueButton = styled(BlueButton)`
  padding: 10px;
  margin-top: 10px;
`;

// 재활용한 컴포넌트를 재활용
const BigRedButton = styled(BigBlueButton)`
  background-color: red;
`;

export default function App() {
return (
  <>
    <BlueButton>Blue Button</BlueButton>
    <br />
    <BigBlueButton>Big Blue Button</BigBlueButton>
    <br />
    <BigRedButton>Big Red Button</BigRedButton>
  </>  
  );
}
```

#### Props 활용하기

```javascript
import styled from "styled-components";
import GlobalStyle from "./GlobalStyle";

// 받아온 prop에 따라 조건부 렌더링 가능
// 삼항 연산자를 활용해 <Button> 컴포넌트에 skyblue 라는 props가 있는지 확인
// 있으면 배경색으로 skyblue를, 없을 경우 white를 지정해 줌
const Button1 = styled.button`
  background: ${(props) => (props.skyblue ? "skyblue" : "white")};
`;

export default function App() {
return (
  <>
    <GlobalStyle />
    <Button1>Button1</Button1>
    <Button1 skyblue>Button1</Button1>
  </>
  );
}
```

#### Props 값으로 렌더링하기

```javascript
import styled from "styled-components";
import GlobalStyle from "./GlobalStyle";

// 받아온 prop 값을 그대로 이용해 렌더링 
const Button1 = styled.button`
    background: ${(props) => (props.color ? props.color : "white")};
`;

// 아래와 같은 형식으로도 활용 가능
const Button2 = styled.button`
    background: ${(props) => props.color || "white"};
`;

export default function App() {
return (
    <>
      <GlobalStyle />
      <Button1>Button1</Button1>
      <Button1 color="orange">Button1</Button1>
      <Button1 color="tomato">Button1</Button1>
      <br />
      <Button2>Button2</Button2>
      <Button2 color="pink">Button2</Button2>
      <Button2 color="turquoise">Button2</Button2>
    </>
  );
}
```

<br/>

## 3. useRef

### DOM reference를 잘 활용할 수 있는 useRef

React는 예외적인 상황에서 `useRef`로 DOM 노드, 엘리먼트, React 엘리먼트로 주소값 참조 가능

```javascript
const 주소값을_담는_그릇 = useRef(참조자료형)
// 이제 주소값을_담는_그릇 변수에 어떤 주소값이든 담을 수 있음
return (
  <div>
    <input ref={주소값을_담는_그릇} type="text" />
      {/* React에서 사용 가능한 ref라는 속성에 주소값을_담는_그릇을 값으로 할당하면*/}
      {/* 주소값을_담는_그릇 변수에는 input DOM 엘리먼트의 주소가 담김 */}
      {/* 향후 다른 컴포넌트에서 input DOM 엘리먼트를 활용할 수 있음 */}
  </div>
);
```

아래의 제한된 상황에서 `useRef` 사용 가능하나, React의 특징이자 장점인 선언형 프로그래밍 원칙과 배치되기에 해당 상황 제외한 경우 `useRef` 남용은 부적절

```javascript
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick = {onButtonClick}>Focus the input</button>
    </>;
  )
}
```
