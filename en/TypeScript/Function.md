# TypeScript Function

## JavaScript vs. TypeScript

- JavaScript ver.

  ```javascript
  // named function
  function add(x, y) {
    return x + y;
  }

  // arrow function
  let add = (x, y) => {
    return x + y;
  };
  ```

- TypeScript ver.

  ```typescript
  // named function
  function add(x: number, y: number): number {
    return x + y;
  }

  // arrow function
  let add = (x: number, y: number): number => {
    return x + y;
  };
  ```

- When expressing functions in TypeScript, **parameter types** and **return types** must be specified
- After writing the type corresponding to each parameter, **the return type must be written after the parentheses** (assuming type inference is not used)
- If the function **has no return value**, `void` can be used (assuming type inference is not used)

  ```typescript
  let printAnswer = (): void => {
    console.log('YES');
  };
  ```

- Unlike JavaScript, TypeScript requires **passing arguments according to the number of parameters**

  ```typescript
  let greeting = (firstName: string, lastName: string): string => {
    return `hello, ${firstName} ${lastName}`;
  };

  // Error occurs
  greeting('coding');

  // Works normally
  greeting('coding', 'kim');

  // Error occurs
  greeting('coding', 'kim', 'hacker');
  ```

- You can also set the value to be assigned to a parameter when no argument is passed or undefined is passed
- This works the same as default parameters in JavaScript

  ```typescript
  let greeting = (firstName: string, lastName: string = 'kim'): string => {
    return `hello, ${firstName} ${lastName}`;
  };

  // Works normally
  greeting('coding');

  // Works normally
  greeting('coding', undefined);

  // Error occurs
  greeting('coding', 'kim', 'hacker');
  ```

- Or if you want optional parameters, you can solve it by **adding ? at the end of the parameter name**

  ```typescript
  let greeting = (firstName: string, lastName?: string): string => {
    return `hello, ${firstName} ${lastName}`;
  };

  // Works normally
  greeting('coding');

  // Works normally
  greeting('coding', 'kim');

  // Error occurs
  greeting('coding', 'kim', 'hacker');
  ```
