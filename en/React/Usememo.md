# UseMemo

## 1. Role of useMemo

- Components are structured to re-render whenever state changes or parent components render
- However, too frequent re-rendering causes poor performance in apps
- React Hooks are methods that allow function components to manipulate state and use optimization features
- Among them, there are also **Hooks for rendering optimization** → useCallback and useMemo are Hooks that perform that role

<br/>

## 2. What is useMemo?

- useMemo is a Hook used when you want to reuse specific values
- For example, if there's code in the component below that passes the value prop to a function called calculate to get the result value, then outputs it as a `<div>` element:

  ```javascript
  function Calculator({ value }) {
    const result = calculate(value);
    return (
      <>
        <div>{result}</div>
      </>
    );
  }
  ```

- If the above calculate function takes a long time to return, **the component will continuously call this function every time it renders**, increasing loading time and ultimately giving users a poor experience

  ```javascript
  import { useMemo } from 'react';
  const result = useMemo(() => calculate(value), [value]);
  return (
    <>
      <div>{result}</div>
    </>
  );
  ```

- The value of the above Calculator component is a kind of value, and if this value doesn't keep changing every time it renders & if the value can be stored somewhere and retrieved for reuse, there's no need to call the calculate function
- Here you can use the useMemo Hook
- By calling useMemo to wrap calculate, **when comparing previous rendering with newly constructed rendering, if the value is the same → previous rendering's value can be reused (Memoization)**

<br/>

## 3. What is Memoization?

- Programming technique that **stores the result value of previously performed operations in memory** and **reuses them when the same input comes in**
- If you use this memoization appropriately, there's no need for duplicate operations, so app performance can be optimized → useMemo utilizes this
- You can implement logic using memoization concept directly, but it's much more convenient because useMemo Hook call handles logic implementation for you
