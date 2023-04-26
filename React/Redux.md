## **1. 상태 관리**
### 1. 전역 상태 관리
- 프론트엔드 개발에서의 상태: 동적으로 표현되는 데이터
- 전역 상태
  - 서로 다른 컴포넌트가 사용하는 상태의 종류가 다르다면, 서로 다른 출처가 있어도 괜찮음
  - 하지만 서로 다른 컴포넌트가 동일한 상태를 다룬다면, 서로 다른 출처로 가져오는 것은 피하는 것이 좋음
- 데이터 무결성
  - 동일한 데이터는 항상 같은 곳에서 데이터를 가져온다. → Single source of truth
- 상태 관리 툴이 해결해주는 문제들
  - 전역 상태 저장소 제공
  - Props Drilling 이슈 해결

### 2. Props Drilling
- Props Drilling 이란?
  - 상위 컴포넌트의 state를 props를 통해 전달하고자 하는 컴포넌트로 전달하기 위해 그 사이는 props를 전달하는 용도로만 쓰이는 컴포넌트들을 거치면서 데이터를 전달하는 현상
- Props Drilling의 문제점
  - 코드 가독성이 나빠짐
  - 코드의 유지보수 또한 힘들어짐
  - state 변경 시, Props의 전달 과정에서 불필요하게 관여된 컴포넌트들 또한 리렌더링 발생해 성능에 악영향
- 해결책
  - 컴포넌트와 관련있는 state는 가능하면 가까이 유지하기
  - 상태관리 라이브러리 사용: 전역으로 관리하는 저장소에서 직접 state 꺼내 쓸 수 있기에 Props Drilling 방지 효과적

<br/>

## **2. Redux**
### 1. Redux 기초
1. Redux란
  - 컴포넌트와 상태를 분리하여 전역에서 상태 관리를 해줄 수 있게 해주는 상태 관리 라이브러리

2. Redux가 상태를 관리하는 순서
  <br/>(1) 상태가 변경되어야 하는 이벤트가 발생하면, 변경될 상태에 대한 정보가 담긴 Action 객체가 생성
  <br/>(2) 이 Action 객체는 Dispatch 함수의 인자로 전달됨
  <br/>(3) Dispatch 함수는 Action 객체를 Reducer 함수로 전달함
  <br/>(4) Reducer 함수는 Action 객체의 값을 확인하고, 그 값에 따라 전역 상태 저장소 Store의 상태를 변경함
  <br/>(5) 상태가 변경되면, React는 화면을 다시 렌더링
  <br/> → 즉, Redux에서는 Action → Dispatch → Reducer → Store 순서로 데이터가 단방향으로 흐름

### 2. Redux 구조
1. Store
- 상태가 관리되는 오직 하나뿐인 저장소 역할로, Redux 앱의 state가 저장되어 있는 공간
  ```javascript
  // `createStore` 메소드로 Reducer 연결해 store 생성
  import { createStore } from 'redux';
  const store = createStore(rootReducer);
  ```

2. Reducer
- Dispatch에게서 전달받은 Action 객체의 type 값에 따라서 상태를 변경시키는 함수
  ```javascript
  const count = 1

  // Reducer 생성시 초기 상태의 인자로 요구
  const counterReducer = (state = count, action) => {
    // Action 객체의 type 값에 따라 분기하는 switch 조건문
    switch(action.type) {
      // action === 'INCREASE'일 경우
      case 'INCREASE':
        return state + 1
      // action === 'DECREASE'일 경우
      case 'DECREASE':
        return state - 1
      // action === 'SET_NUMBER'일 경우
      case 'SET_NUMBER':
        return action.payload
      // 해당되는 경우가 없을 때는 기존 상태를 그대로 리턴
      default:
        return state;
    }
  }
  // Reducer가 리턴하는 값이 새로운 상태가 됨
  // 이때 Reducer는 순수함수여야 함.
  ```

3. Action
- Action은 어떤 액션을 취할 것인지 정의해 놓은 객체
- type은 필수로 지정해 주어야 하며, 대문자와 Snake Case로 작성
- 보통 Action 객체를 생성하는 함수를 만들어 사용 → 액션 생성자 (Action Creator)
  ```javascript
  // payload가 필요 없는 경우
  const increase = () => {
    return {
      type: 'INCREASE'
    }
  }

  // payload가 필요한 경우
  const setNumber = (num) => {
    return {
      type: 'SET_NUMBER',
      payload: num
    }
  }
  ```

4. Dispatch
- Reducer로 Action을 전달해 주는 함수
  ```javascript
  // Action 객체를 직접 작성하는 경우
  dispatch( {type: 'INCREASE'} );
  dispatch( {type: 'SET_NUMBER', payload: 5} );

  // Action Creator를 사용하는 경우
  dispatch( increase() );
  dispatch( setNumber(5) );
  ```

### 3. Redux Hooks
1. useDispatch()
- Action 객체를 Reducer로 전달해 주는 Dispatch 함수를 반환하는 메소드
  ```javascript
  import {useDispatch} from 'react-redux'

  const dispatch = useDispatch()
  dispatch(increase())
  console.log(counter) // 2

  dispatch(setNumber(5))
  console.log(counter) // 5
  ```

2. useSelector()
- 컴포넌트와 state를 연결해 Redux의 state에 접근할 수 있게 해주는 메소드
  ```javascript
  // Redux Hooks 메소드는 redux가 아닌 react-redux에서 불러옴
  import {useSelector} from 'react-redux'
  const counter = useSelector(state => state)
  console.log(counter) // 1
  ```

<br/>

## **3. Redux의 세 가지 원칙**
1. Single source of truth
  - 동일한 데이터는 항상 같은 곳에서 가지고 와야 함
  - Redux에는 데이터를 저장하는 Store 라는 하나뿐인 공간이 있음

2. State is read-only
  - 상태는 읽기 전용
  - React에서 상태갱신함수로만 상태를 변경했던 것처럼 Redux의 상태도 직접 변경할 수 없음을 의미
  - 즉, Action 객체가 있어야만 상태를 변경 가능

3. Changes are made with pure functions
  - 변경은 순수함수로만 가능
  - 상태가 엉뚱한 값으로 변경되는 일이 없도록 순수함수로만 작성되어야 함