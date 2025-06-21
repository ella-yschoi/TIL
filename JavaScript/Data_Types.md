# Data Types

## 1. Number Type

- Dividing any number by 0 results in infinity

  ```javascript
  console.log(1 / 0); // Infinity
  ```

- You can also directly reference Infinity

  ```javascript
  console.log(Infinity); // Infinity
  ```

- NaN means an error occurred during calculation, and additional operations will still return NaN

  ```javascript
  console.log('not a number' / 2); // NaN
  ```

<br/>

## 2. BigInt

- In JavaScript, numbers beyond a certain level of magnitude cannot be represented as number type, but you can create them by adding 'n' to the end of integer literals regardless of length

  ```javascript
  const bigInt = 123456789123456789n;
  ```

<br/>

## 3. String Type

- There are three types of quotes

  ```javascript
  let str = 'Hello'; // double quotes
  let str2 = 'Ella Yeonsu Choi'; // single quotes
  let phrase = `Nice to meet you`; // backticks
  ```

- With backticks, you can wrap variables or expressions in ${...} to insert desired variables or expressions in the middle of strings (double quotes or single quotes do not support expansion)

  ```javascript
  let name = 'Ella';

  // Insert variable in the middle of string
  console.log(`Hello, ${name}!`); // Hello, Ella!

  // Insert expression in the middle of string
  console.log(`the result is ${1 + 2}`); // the result is 3
  ```

<br/>

## 4. Boolean Type

- Only has two values: true and false, also used when storing comparison results

  ```javascript
  let isGreater = 4 > 1;
  console.log(isGreater); // true
  ```

<br/>

## 5. null Value

- A value that doesn't belong to any of the above data types, and is a separate data type that only contains the null value
- It explicitly represents a value that doesn't exist (nothing), is empty, or is unknown

  ```javascript
  let age = null; // unknown, empty
  ```

<br/>

## 6. undefined Value

- Like null, it implicitly indicates a 'state where no value has been assigned', and when a variable is declared but no value is assigned, undefined is assigned to that variable

  ```javascript
  let age; // variable declared but no value assigned
  console.log(age); // 'undefined'
  ```

- It's possible to assign undefined to a variable, but direct assignment is not recommended; use null instead and keep it as a reserved word for variable initialization

<br/>

## 7. Objects and Symbols

- Data types other than object type can only represent **one thing** whether it's a string or number, so they're called primitive data types. On the other hand, objects can represent data collections or complex entities
- Symbol type is used to create unique identifiers for objects

<br/>

## 8. typeof Operator

- Returns the data type of the argument and supports two forms of syntax

  - Operator: typeof x
  - Function: typeof(x)

  ```javascript
  typeof undefined; // 'undefined'
  typeof 0; // 'number'
  typeof 10n; // 'bigint'
  typeof Symbol('id'); // 'symbol'
  typeof Math; // 'object'
  typeof null; // 'object'
  typeof alert; // 'function'
  ```

- Math is a _built-in object_ that provides mathematical operations, so 'object' is output. Note that built-in objects are objects that JavaScript has by default, including function, array, number, string, etc.
- null is a special value with its own data type and is not an object, but it's left as a language error for backward compatibility
- typeof returns 'function' if the operand is a function, but there's no function type and functions belong to the object type
