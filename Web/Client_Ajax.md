# Client AJAX

## 1. React 데이터 흐름

- React의 가장 큰 특징은 페이지가 아닌, 컴포넌트 단위로 시작한다는 점
- 데이터는 위에서 아래로 흐른다 : **단방향 데이터 흐름 (one-way data flow)**
- state 끌어 올리기로 역방향 데이터 흐름 추가 → 상위 컴포넌트의 "상태를 변경하는 함수" 그 자체를 하위 컴포넌트로 전달하고, 이 함수를 하위 컴포넌트가 실행함

### (1) Side Effect (부수 효과)

  ```javascript
  let foo = 'hello';

  function bar() {
      foo = 'world';
  }
  
  bar();
  // 전역변수 foo를 bar 라는 함수가 수정시키기에 bar는 Side Effect를 발생시킴
  ```

- 함수 내에서 어떤 구현이 **함수 외부에 영향을 끼치는 경우**
- React에서는 컴포넌트 내에서 fetch를 사용해 API 정보를 가져오거나 이벤트를 활용해 DOM을 직접 조작할 때 Side Effect가 발생했다고 함

### (2) Pure Function (순수 함수)

```javascript
function upper(str) {
   return str.toUpperCase(); // toUpperCase 메소드는 원본을 수정하지 않음 (Immutable)
} 
upper('hello') // 'HELLO'
```

- 오직 함수의 입력만이 함수의 결과에 영향을 주는 함수를 의미
- 순수함수는 입력으로 전달된 값을 수정하지 않음
- 순수함수에는 네트워크 요청과 같은 Side Effect이 없음
- 어떠한 전달인자가 주어질 경우, **항상 똑같은 값이 리턴됨을 보장하여 예측 가능한 함수**임

### (3) React의 함수 컴포넌트

React의 함수 컴포넌트는 props가 입력으로, javascript Element가 출력으로 나가며, 여기엔 그 어떠한 Side Effect도 없으며 순수 함수로 작동

```javascript
function SingleTweet({writer, body, createdAt}) {
   return <div>
      <div>{writer}</div>
      <div>{body}</div>
      <div>{createdAt}</div>
   </div>
}
```

다만, 보통 React 애플리케이션 작성 시, AJAX 요청이 필요하거나 fetch API, LocalStorage 또는 타이머와 같은 React와 상관없는 API를 사용하는 경우 발생 가능하고, 이는 React 입장에서는 모두 Side Effect임

<br/>

## 2. Effect Hook

### (1) Effect Hook

- `useEffect`는 컴포넌트 내에서 Side Effect를 실행할 수 있게 하는 Hook임.
- `useEffect`의 첫 번째 인자는 함수이며, 해당 함수 내에서 Side Effect를 실행하면 됨
- 실행되는 때: 매번 새롭게 컴포넌트가 렌더링될 때 Effect Hook이 실행됨
  - 컴포넌트 생성 후 처음 화면에 렌더링
  - 컴포넌트에 새로운 props가 전달되며 렌더링
  - 컴포넌트에 상태(state)가 바뀌며 렌더링
- 주의할 점
  - **최상위**에서만 Hook을 호출
  - React 함수 내에서 Hook을 호출

### (2) 조건부 effect 발생 (dependency array)

- `useEffect`의 두 번째 인자는 배열이며, 이 배열은 조건을 담고 있음.
- 여기서 조건은 **어떤 값의 변경이 일어날 때**를 의미하며 해당 배열에는 **어떤 값**의 목록이 들어감 → 종속성 배열

### (3) API

- `useEffect`의 두 번째 인자는 종속성 배열
- 배열 내의 종속성 1, 또는 종속성 2의 값이 변할 때 첫 번째 인자의 함수가 실행됨
- 배열 내의 어떤 값이 변할 때만 (effect가 발생하는) 함수가 실행됨

### (4) 단 한 번만 실행되는 Effect 함수  

#### 종속성 목록에 아무런 종속성도 없다면?

- 빈 배열 넣기 `useEffect(함수, [])`: 컴포넌트가 처음 생성될 때만 effect 함수 실행되며, 외부 API를 통해 리소스를 받아오고 더이상 API 호출이 필요하지 않을 때 사용 가능
- 아무것도 넣지 않기 `useEffect(함수)`

### (5) Data Fetching: 목록 내 필터링 구현하기

#### 컴포넌트 내 필터링

- 전체 목록 데이터를 불러오고, 목록을 검색어로 filtering
- 장점: HTTP 요청 빈도를 줄일 수 있음
- 단점: 브라우저(클라이언트)의 메모리 상에 많은 데이터를 가지므로 클라이언트 단의 부담 증가

#### 컴포넌트 외부에서 필터링: 컴포넌트 외부로 API 요청 시, 필터링한 결과를 받아오기

- 장점: 클라이언트가 필터링 구현 필요 X
- 단점: 빈번한 HTTP 요청이 일어나 서버가 필터링을 처리하므로 서버의 부담 증가

<br/>

## 3. AJAX

### (1) AJAX 요청 보내기

fetch API를 써서 서버에 요청하면, API 접속이 느릴 경우를 고려해 로딩 화면(loading Indicator) 구현 필수

```javascript
const [isLoading, setIsLoading] = useState(true);

// 생략, LoadingIndicator 컴포넌트는 별도로 구현했음을 가정
return {isLoading ? <LoadingIndicator /> : <div>로딩 완료 화면</div>}
```

fetch 요청 전후로 setIsLoading을 설정해 보다 나은 UX 구현

```javascript
useEffect(() => {
setIsLoading(true);
fetch(`http://서버주소/proverbs?q=${filter}`)
  .then(resp => resp.json())
  .then(result => {
     setProverbs(result);
     setIsLoading(false);
  });
}, [filter]);
```
