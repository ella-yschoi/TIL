# Hook

## 1. Class Component and Function Component

- Hook is a method used in function components
- Before function components, there were class components. Class components became harder to understand as they became more complex, and had the disadvantage of **difficulty in reusing state logic between components**.
- Additionally, to use React's class components, you need to understand how JavaScript's this keyword works, which made it difficult to understand the behavior itself if you didn't know the syntax exactly.

### Class Component

```javascript
class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 0,
    };
    this.handleIncrease = this.handleIncrease.bind(this);
  }

  handleIncrease = () => {
    this.setState({
      counter: this.state.counter + 1,
    });
  };

  render() {
    return (
      <div>
        <p>You clicked {this.state.counter} times</p>
        <button onClick={this.handleIncrease}>Click me</button>
      </div>
    );
  }
}
```

<br/>

### Function Component

- Function components are much more intuitive and easier to read compared to class components
- The useState() method that allows storing and using state values in this Counter component → Hook.
- In other words, you can see it as the Counter component calling the useState() Hook to add state inside the function component.
- This state will persist even when the component re-renders.
- Also, while only one State Hook was used in this component, you can use multiple ones depending on the situation.

```javascript
function Counter() {
  const [counter, setCounter] = useState(0);

  const handleIncrease = () => {
    setCounter(counter + 1);
  };

  return (
    <div>
      <p>You clicked {counter} times</p>
      <button onClick={handleIncrease}>Click me</button>
    </div>
  );
}
```

<br/>

## 2. What is Hook?

- A newly added feature in React 16.8 that allows using state and other React features without writing classes
- Refers to methods that make it convenient to use state values and other various features in function components
- Enables using React only with functions, not classes, so it doesn't work in class components

<br/>

## 3. Hook Usage Rules

### 1. Must only be called at the top level of React functions

- When Hooks are executed inside loops, conditionals, or nested functions, there's concern they might not work as expected
- Multiple Hooks can be used inside components, and React stores these Hooks in the order they're called. However, it becomes difficult to store Hooks in the order they're called when they're inside conditionals or loops

### 2. Must only be used inside React functions

- Should not be called inside other general JavaScript functions that are not React
