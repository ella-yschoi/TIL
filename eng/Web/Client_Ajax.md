# Client AJAX

## 1. React Data Flow

- React's biggest characteristic is that it starts with components, not pages
- Data flows from top to bottom: **one-way data flow**
- Adding reverse data flow with state lifting → passing the "function that changes state" of the parent component itself to the child component, and the child component executes this function

### (1) Side Effect

```javascript
let foo = 'hello';

function bar() {
  foo = 'world';
}

bar();
// Since the bar function modifies the global variable foo, bar causes Side Effect
```

- When some implementation within a function **affects the outside of the function**
- In React, it's said that Side Effect occurs when using fetch within a component to get API information or using events to directly manipulate the DOM

### (2) Pure Function

```javascript
function upper(str) {
  return str.toUpperCase(); // toUpperCase method doesn't modify the original (Immutable)
}
upper('hello'); // 'HELLO'
```

- Refers to a function where only the function's input affects the function's result
- Pure functions don't modify values passed as input
- Pure functions have no Side Effects like network requests
- **Predictable function** that guarantees the same value is always returned for any given argument

### (3) React Function Components

React function components take props as input and output JavaScript Elements, with no Side Effects and operate as pure functions

```javascript
function SingleTweet({ writer, body, createdAt }) {
  return (
    <div>
      <div>{writer}</div>
      <div>{body}</div>
      <div>{createdAt}</div>
    </div>
  );
}
```

However, when writing React applications, AJAX requests may be needed or APIs unrelated to React like fetch API, LocalStorage, or timers may be used, and these are all Side Effects from React's perspective

<br/>

## 2. Effect Hook

### (1) Effect Hook

- `useEffect` is a Hook that allows executing Side Effects within components
- The first argument of `useEffect` is a function, and Side Effects should be executed within that function
- When it executes: Effect Hook executes every time the component is newly rendered
  - First rendering on screen after component creation
  - Rendering when new props are passed to the component
  - Rendering when component state changes
- Points to note
  - Only call Hooks at the **top level**
  - Call Hooks within React functions

### (2) Conditional effect occurrence (dependency array)

- The second argument of `useEffect` is an array, and this array contains conditions
- Here, conditions mean **when changes in what values occur**, and the list of **what values** goes into that array → dependency array

### (3) API

- The second argument of `useEffect` is the dependency array
- When the value of dependency 1 or dependency 2 in the array changes, the function of the first argument is executed
- The function is executed only when some value in the array changes (when effect occurs)

### (4) Effect Function That Executes Only Once

#### What if there are no dependencies in the dependency list?

- Put empty array `useEffect(function, [])`: Effect function executes only when the component is first created, can be used when resources are received through external API and no more API calls are needed
- Put nothing `useEffect(function)`

### (5) Data Fetching: Implementing Filtering in List

#### Filtering Within Component

- Load all list data and filter the list by search term
- Advantages: Can reduce HTTP request frequency
- Disadvantages: Since there's a lot of data in browser (client) memory, client-side burden increases

#### Filtering Outside Component: When making API requests outside the component, receive filtered results

- Advantages: No need for client to implement filtering
- Disadvantages: Frequent HTTP requests occur and server handles filtering, so server burden increases

<br/>

## 3. AJAX

### (1) Sending AJAX Requests

When making requests to server using fetch API, loading screen (loading Indicator) implementation is essential considering cases where API connection is slow

```javascript
const [isLoading, setIsLoading] = useState(true);

// Omitted, assuming LoadingIndicator component is implemented separately
return {isLoading ? <LoadingIndicator /> : <div>Loading complete screen</div>}
```

Set setIsLoading before and after fetch request for better UX implementation

```javascript
useEffect(() => {
  setIsLoading(true);
  fetch(`http://serveraddress/proverbs?q=${filter}`)
    .then((resp) => resp.json())
    .then((result) => {
      setProverbs(result);
      setIsLoading(false);
    });
}, [filter]);
```
