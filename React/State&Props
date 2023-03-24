 ## **0.React State & Props** ##
- State
  - 컴포넌트 사용 중 컴포넌트 '내부'에서 변할 수 있는 값
  - ex) 나이, 주소, 취업 여부
- Props
  - '외부'로부터 전달받은 값
  - ex) 이름, 성별

<br/><p>

## **1.Props의 특징** ##
- (1) 컴포넌트의 속성 (property)
  - 웹 애플리케이션에서 해당 컴포넌트가 가진 (변하지 않는) 속성
- (2) 부모 컴포넌트로부터 전달받은 값
  - React 컴포넌트는 JavaScript 함수와 클래스로, 
  - props를 함수의 전달인자처럼 받아 → 이를 기반으로 화면에 어떻게 표시되는지를 기술하는 React 엘리먼트를 반환
  - 따라서 컴포넌트가 최초 렌더링될 때 화면에 출력하고자 하는 데이터를 담은 초기값으로 사용 가능 
- (3) 객체 형태
  - 어떤 타입의 값도 넣어 전달할 수 있음
- (4) 읽기 전용
  - 함부로 변경될 수 없는 읽기전용 (read-only)객체
  - 만약 읽기 전용이 아니라면 props를 전달한 상위 컴포넌트 값에 영향을 미칠 수 있음
  - 또한 의도치 않은 side effect이나 React의 단방향/하향식 데이터 흐름 원칙에 위배됨
  
<br/><p>

## **2.How to use Props** ##
- (1) 하위 컴포넌트에 전달하고자 하는 값과 속성을 '정의'한다.

  ```jsx
  function Parent() { 
    return (
        <div className = 'parent'> // <Parent> 선언
            <h1>I am the parent</h1>
            <Child /> // <Parent> 컴포넌트 안에 <Child> 컴포넌트 작성
        </div>
    );
  };

  funtion Child() {
    return (
        <div className = 'Child'>
    );
  };
  ```
- (2) props를 이용하여 정의된 값과 속성을 '전달'한다.

  ```jsx
  // 속성 및 값을 할당함, 전달하고자 하는 값을 {}로 감싸줌
  <Child attribute = {value} /> 

  // text 속성 선언 후, 이 속성에 문자열 값을 할당하여 <Child> 컴포넌트에 전달
  <Child text = {'I am the eldest child'} />  

  //<Parent> 컴포넌트에서 전달한 문자열을 <Child> 컴포넌트에서 받아옴
  function Child(props) {
    return (
        <div className = 'Child'></div>
    );
  };

  ```
- (3) 전달받은 props를 '렌더링'한다.
  
  ```jsx
  function Child(props) { 
    // props라는 객체의 {key : value}는 <Parent> 컴포넌트에서 정의한 {attribute : value} 형태를 띔
    return (
        <div className = 'child'>
        // JavaScript처럼 props의 value 또한 Dot notation으로 접근 가능
        <p>{props.text}</p>
        </div>
    );
  };
  ```

- (4) props children: 여는 태그와 닫는 태그 사이에 value를 넣어 전달하는 방법도 있음

  ```jsx
  function Parent () {
    return (
        <div className = 'parent'>
            <h1>I am the parent</h1>
            <Child>I am the eldest child</Child>
        </div>
    );
  };
  function Child(props) {
    return (
        <div className = 'child'>
            <p>{props.children}</p>
        </div>
    );
  };
  ```
  
<br/><p>

## **3. State hook, useState** ##
- useState 사용 방법과 작동 방식
  ```jsx
  // React로부터 useState 불러옴
  import {useState} from 'react';
  // useState를 컴포넌트 안에서 호출: state 변수는 React에 의해 함수가 끝나도 사라지지 않음
  function CheckboxExample() {
    // 새로운 state 변수 선언
    const [isChecked, setIsChecked] = useState(false);
  }
  ```

- useState 수도코드
  ```jsx
  // useState를 호출하면 배열을 반환하는데
  // 배열의 0번째 요소는 현재 state 변수, 1번째 요소는 이 변수를 갱신하는 함수
  // useState의 인자로 넘겨주는 값은 state의 초기값

  const [state 저장변수, state 갱신함수] = useState(상태 초기값);
  ```

- useState 문법 예시
  ```jsx
  function CheckboxExample() {
    const [isChecked, setIsChecked] = useState(false);
  }

  // ischecked: state를 저장하는 변수
  // setIsChecked: state인 isChecked를 변경하는 함수
  // useState: state hook
  // false: state 초기값
  ```

- JSX 삼항연산자 사용 예시
  ```jsx
  <span>{isChecked ? 'Checked!!' : 'Unchecked'} </span>
  ```
  
<br/><p>

## **4. State 갱신하기** ##
- 갱신하려면 state 변수를 갱신할 수 있는 함수인 setIsChecked를 호출
- 사용자가 체크박스 값을 변경하면 onchange 이벤트가 이벤트 핸들러 함수인 handleChecked를 호출하고, 이 함수가 setIsChecked 호출
- setIschecked 호출되면 결과에 따라 isChecked 변수 갱신
- React는 새로운 isChecked 변수를 CheckboxExample 컴포넌트에 넘겨, 해당 컴포넌트 다시 렌더링
  
  ```jsx
    function CheckboxExample() {
    const [isChecked, setIsChecked] = useState(false);

    const handleChecked = (event) => {
        setIsChecked(event.target.checked);
    };

    return (
        <div className = 'App'>
        <input type = 'checkbox' checked = {isChecked} onChange = {handleChecked} />
        <span>{isChecked ? 'Checked!!' : 'Unchecked'}</span>
        </div>
    );
    }
    ```
  
<br/><p>

## **5. 주의점** ##
- React 컴포넌트는 state가 변경되면 새롭게 호출되고, 리렌더링 됨
- React state는 상태 변경 함수 호출로 변경해야 함, 강제로 변경 X
  
<br/><p>

## **6. 이벤트 처리** ##
- React에서 이벤트는 camelCase 사용
- JSX를 사용해 문자열이 아닌, 함수로 이벤트 처리 함수 (이벤트 핸들러) 전달
  ```jsx
  <button onClick = {handleEvent}>Event</button>
  ```

- onChange
  ```jsx
  function NameForm() {
    const [name, setName] = useState('');

    const handleChange = (e) => {
        setName(e.target.value);
    }

    return (
        <div>
            // onChange 이벤트 발생시, e.target.value를 통해 이벤트 객체에 담겨있는 input 값을 읽어올 수 있음
            // onChange는 input의 텍스트가 바뀔 때마다 발생하는 이벤트
            // 이벤트 발생시, handleChange 함수가 작동하며, 이벤트 객체에 담긴 input 값을 setState를 통해 새로운 state로 갱신
            <input type = 'text' value = {name} onChange = {handleChange}></input>
            <h1>{name}</h1>
        </div>
    )
  };
  ```

- onClick
  - 버튼이나 <a> 태그를 통한 링크 이동 등 사용자의 행동에 따라 애플리케이션이 반응해야 할 때 사용하는 이벤트
  ```jsx
  function NameForm() {
    const [name, setName] = useState();

    const handleChange = (e) => {
        setName(e.target.value);
    }

    return (
        <div>
            <input type = 'text' value = {name} onChange = {handleChange}></input>
            // 버튼 클릭 시 input tag에 입력한 이름이 alert를 통해 알림창이 팝업
            <button onClick = {alert(name)}>Button</button>
            <h1>{name}</h1>
        </div>
    );
  };
  ```