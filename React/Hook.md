# Hook

## 1. Class Component와 Function Component

- Hook은 함수 컴포넌트에서 사용하는 메서드
- 함수 컴포넌트 이전에는 클래스(class) 컴포넌트가 있었음. 클래스 컴포넌트는 복잡해질수록 이해하기 어려워졌고, 컴포넌트 사이에서 **상태 로직을 재사용하기 어렵다는 단점**이 있었음.
- 또한 React의 클래스 컴포넌트를 사용하기 위해서는 JavaScript의 this 키워드가 어떤 방식으로 동작하는지 알아야 하는데, 이는 문법을 정확히 알지 못하면 동작 방식 자체를 정확히 이해하기 어렵게 만들었음.

### Class Component

```javascript
class Counter extends Component {
    constructor(props) {
        super(props);
        this.state = {
            counter: 0
        }
        this.handleIncrease = this.handleIncrease.bind(this);
    }

    handleIncrease = () => {
        this.setState({
            counter: this.state.counter + 1
        })
    }

    render(){
       return (
            <div>
                <p>You clicked {this.state.counter} times</p>
                <button onClick={this.handleIncrease}>
                    Click me
                </button>
            </div>
       ) 
    }
}
```

<br/>

### Function Component

- 함수형 컴포넌트는 클래스형 컴포넌트에 비해 훨씬 더 직관적이고, 보기 쉽다는 특징이 있음
- 이 Counter 컴포넌트에서 상태값을 저장하고 사용할 수 있게 해주는 useState()라는 메소드 → Hook.
- 즉, Counter 컴포넌트에서 useState() Hook을 호출해 함수 컴포넌트 안에 state를 추가한 형태라고 볼 수 있음.
- 이 state는 컴포넌트가 리렌더링 되어도 그대로 유지될 것.
- 또한 해당 컴포넌트에서 State Hook은 하나만 사용했지만 때에 따라서 여러 개 사용할 수 있음.

```javascript
function Counter () {
    const [counter, setCounter] = useState(0);

    const handleIncrease = () => {
        setCounter(counter + 1)
    }

    return (
        <div>
            <p>You clicked {counter} times</p>
            <button onClick={handleIncrease}>
                Click me
            </button>
        </div>
    )
}
```

<br/>

## 2. Hook이란?

- React 16.8에 새롭게 추가된 기능으로, class를 작성하지 않고도 state와 다른 React의 기능 사용 가능
- 함수형 컴포넌트에서 상태값 및 다른 여러 기능을 사용하기 편리하게 해주는 메서드를 의미
- class가 아닌 function으로만 React를 사용할 수 있게 하기에, 클래스형 컴포넌트에서는 동작하지 않음

<br/>

## 3. Hook 사용 규칙

### 1. 리액트 함수의 최상위에서만 호출해야 함

- 반복문, 조건문, 중첩된 함수 내에서 Hook 실행 시, 예상한 대로 동작하지 않을 우려가 있음
- 컴포넌트 안에는 Hook들이 여러 번 사용될 수 있는데, React는 이 Hook을 호출되는 순서대로 저장을 해놓음. 그런데 조건문, 반복문 안에서 Hook이 호출되는 순서대로 저장을 하기 어려워지기 때문

### 2. 오직 리액트 함수 내에서만 사용되어야 함

- 리액트가 아닌, 다른 일반 JavaScript 함수 안에서 호출해서는 안 됨
