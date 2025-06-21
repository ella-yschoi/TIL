# UseCallback

## 1. What is useCallback?

- `useCallback` is also a Hook that uses memoization technique, just like useMemo
- If `useMemo` is a Hook used for reusing values, `useCallback` is a Hook used for **reusing functions**

  ```javascript
  import React, { useCallback } from 'react'; // import required

  function Calculator({ x, y }) {
    const add = useCallback(() => x + y, [x, y]);

    return (
      <>
        <div>{add()}</div>
      </>
    );
  }
  ```

- When you use the `useCallback` Hook, as long as the values the function depends on don't change, it **keeps returning the existing function**. In the example above, if x and y are the same, the function is reused on the next render.
- However, if you only use `useCallback`, you won't notice significant optimization compared to `useMemo`
- This is because `useCallback` is not a Hook that calls a function, but **just a Hook that retrieves a function from somewhere in memory and calls it**
- Therefore, rather than using `useCallback` simply to avoid repeatedly creating functions inside a component, it's better to use it **when passing a function as a prop to a child component**.

<br/>

## 2. useCallback and Reference Equality

- `useCallback` relies on reference equality.
- Since React is an open-source library made with JavaScript, it basically follows JavaScript syntax.
- In JavaScript, functions are objects, and when objects are stored in memory, **the address of the value is stored, not the value itself**, so even if the returned value is the same, comparing with the equality operator will output **false**.
- React is the same. When React re-renders, it creates and calls a new function, and the newly created function is not the same as the previous function
- However, **if you use `useCallback` to store and reuse the function itself**, **the memory address of the function is stored and reused**.
- Therefore, when passing a function as an argument to another function or as a prop to a child component inside a React component function, you can prevent unexpected performance issues.
