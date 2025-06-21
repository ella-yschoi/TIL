# Copy

## 1. Two Methods to Copy Arrays

### (1) slice

- Can copy the original array
- The newly created array from copying has the same elements as the original array, but references a different address

  ```javascript
  let arr = [0, 1, 2, 3];
  let copiedArr = arr.slice();
  console.log(copiedArr); // [0, 1, 2, 3]
  console.log(arr === copiedArr); // false
  ```

- Since the addresses are different, even if you add elements to the copied array, they won't be added to the original array

  ```javascript
  copiedArr.push(4);
  console.log(copiedArr); // [0, 1, 2, 3, 4]
  console.log(arr); // [0, 1, 2, 3]
  ```

### (2) Spread Syntax of Array

- A newly added syntax in ES6 that can spread arrays
- Add ... before the variable name assigned to the array

  ```javascript
  let arr = [0, 1, 2, 3];
  console.log(...arr); // 0 1 2 3
  ```

- First, understand how to create arrays
- If you create two arrays with the same elements as below and assign them to variables respectively, do the two variables reference the same address?
- The answer is, since they are reference data types, they reference different addresses

  ```javascript
  let num = [1, 2, 3];
  let int = [1, 2, 3];

  console.log(num === int); // false
  ```

- Also, if you spread the original array into a new array, it has the same elements as the original array but references different addresses
- As a result, it behaves identically to using the slice() method

  ```javascript
  let arr = [0, 1, 2, 3];
  let copiedArr = [...arr];
  console.log(copiedArr); // [0, 1, 2, 3]
  console.log(arr === copiedArr); // false

  copiedArr.push(4);
  console.log(copiedArr); // [0, 1, 2, 3, 4]
  console.log(arr); // [0, 1, 2, 3]
  ```

<br/>

## 2. Two Methods to Copy Objects

### (1) Object.assign

```javascript
let obj = { firstName: 'Ella', lastName: 'Choi' };
let copiedObj = Object.assign({}, obj);

console.log(copiedObj); // { firstName: "Ella", lastName: "Choi" }
console.log(obj === copiedObj); // false
```

### (2) Spread Syntax of Object

- Can be used not only for arrays but also for object copying

  ```javascript
  let obj = { firstNmae: 'Ella', lastName: 'Choi' };
  let copiedObj = { ...obj };

  console.log(copiedObj); // { firstName: "Ella", lastName: "**Choi**" }
  console.log(obj === copiedObj); // false
  ```
