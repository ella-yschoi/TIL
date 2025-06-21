# Recursion

## 1. What is Recursive Function?

- A function that calls itself
- When recursion is suitable to use
  - When a given problem can be divided into smaller problems with similar structure
  - When there are many nested loops or when it's difficult to predict the number of nested loops
- Example code

  ```javascript
  // Conditional statement that returns 0 when an empty array is received
  // Code that solves the smallest problem & code that stops recursion
  function arrSum(arr) {
    if (arr.length === 0) {
      return 0;
    }
    // First element of array + arrSum function that receives array with remaining elements
    // Code that breaks down the problem through recursion
    // arrSum([5]) === 5 + arrSum([]) === 5 + 0 === 5;
    // arrSum([4, 5]) === 4 + arrSum([5]) === 4 + 5 === 9;
    return arr.shift() + arrSum(arr);
  }
  ```

<br/>

## 2. Recursive Thinking

### 1. Define the input and output of the recursive function

- Define in the most abstract or simplest way

### 2. Break down the problem and divide into cases

- Break down according to input values or problem order/size

### 3. Solve simple problems

- Solve the easiest problem first → recursion base: this constitutes the escape condition for future recursion
- If there's no escape condition, the recursive function calls itself endlessly, so break down the problem as small as possible

### 4. Solve complex problems

- Solve the remaining complex problems

### 5. Implement the code

```javascript
function recursive (input1, input2, ...) {
    // base case: when the problem can no longer be broken down
    if (when the problem can no longer be broken down) {
        return answer to the simple problem;
    }

    // recursive case: otherwise
    return problem newly defined as a smaller problem
}
```

<br/>

## 3.JSON.stringigy

### 1. Background of JSON Creation

- JSON is JavaScript Object Notation, an object format created for data exchange between different programs

### 2. Methods

#### `JSON.stringify`: Method to convert object → JSON

```javascript
// Method JSON.stringify to convert message object to JSON

let transferableMessage = JSON.stringify(message);

console.log(transferableMessage);
// `{"sender":"Ella","receiver":"Chloe","message":"Hi, Chloe.","createdAt":"2023-04-12 10:10:10"}`

console.log(typeof transferableMessage); // `string`
```

#### `JSON.parse`: Method to convert JSON → object

```javascript
// Apply JSON.parse method to serialized JSON to convert back to object: deserialization

let packet = `{"sender":"Ella","receiver":"Chloe","message":"Hi, Chloe.","createdAt":"2023-04-12 10:10:10"}`;
let obj = JSON.parse(packet);

console.log(obj);
/*
 * {
 * sender: "Ella",
 * receiver: "Chloe",
 * message: "Hi, Chloe.",
 * createdAt: "2023-04-12 10:10:10"
 * }
 */

console.log(typeof obj); // `object`
```

### 3. JSON Basic Rules

![json_rules.png](/Images/json_rules.png)
