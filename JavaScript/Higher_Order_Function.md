# Higher Order Function

- In JavaScript, functions are first-class objects, so they can be assigned to variables
- Function expressions cannot be used before assignment
- square(7); -> Reference Error

  ```javascript
  const square = function (num) {
    // Function expression assigning a function to variable square
    return num * num;
  }; // Since the variable square is assigned a function, it's a first-class object, and you can use the function call operator ()

  output = square(7);
  ```

- Since functions have the characteristics of first-class objects, they can be assigned as values of object properties as shown below

  ```javascript
  const cat = {
    name: 'nabi',
    age: 3,
    cry: function () {
      console.log('miaow..');
    },
  };
  ```

<br/>

## 2. Understanding Higher Order Functions

- Definition: A function that can take a function as an argument and return a function
- A function passed as an argument to another function (caller) is called a callback function
- The higher order function (caller) that receives the callback function can call (invoke) this callback function inside, and can decide whether to execute the callback function depending on the condition
- A function that returns a function is called a currying function, and when using this term, it's sometimes limited to 'a function that takes a function as an argument'. In other words, higher order functions include currying functions.
- In summary, both 'a function that returns a function' and 'a function that takes a function as an argument' are used as higher order functions

  a. When taking another function as an argument

  ```javascript
  function double(num) {
    return num * 2;
  }

  function doubleNum(func, num) {
    return func(num);
  }

  // The function doubleNum is a higher order function that takes another function as an argument
  // If a function comes into the first argument func of doubleNum, the function func is the callback function of doubleNum
  // In the case below, the function double is the callback function of doubleNum

  let output = doubleNum(double, 4);
  console.log(output); // 8
  ```

  b. When returning a function

  ```javascript
  function adder(added) {
    // The function adder
    return function (num) {
      // is a higher order function that takes one argument and returns another function (anonymous function)
      return num + added; // The returned anonymous function takes one argument and returns the value added to added
    };
  }

  // adder(5) is a function, so you can use the function call operator ()
  let output = adder(5)(3); // 8
  console.log(output); // 8

  // The function returned by adder can be stored in a variable
  // because functions are first-class objects in JavaScript
  const add3 = adder(3);
  output = add3(2);
  console.log(output); // 5
  ```

  c. When taking a function as an argument and returning a function

  ```javascript
  function double(num) {
    return num * 2;
  }
  // The function doubleAdder is a higher order function
  // The argument func of doubleAdder is the callback function of doubleAdder
  // The function double is passed as a callback to doubleAdder
  function doubleAdder(added, func) {
    const doubled = func(added);
    return function (num) {
      return num + doubled;
    };
  }
  // doubleAdder(5, double) is a function, so you can use the function call operator ()
  doubleAdder(5, double)(3); // 13

  // The function returned by doubleAdder can be stored in a variable (first-class object)
  const addTwice3 = doubleAdder(3, double);
  addTwice3(2); // 8
  ```

<br/>

## 3. Built-in Higher Order Functions

- In JavaScript, there are several built-in higher order functions, and some of the array methods are representative higher order functions.
- The filter method of arrays is a method that 'filters' elements that meet a certain condition among all elements of the array

  ```javascript
  let arr = [1, 2, 3, 4];
  let output = arr.filter(isEven);
  console.log(output); // [2, 4]

  arr = ['hello', 'front', 'end', 'happy', 'coding'];
  output = arr.filter(isLteFive); // *syntax error: just for understanding the meaning
  console.log(output); // 'hello', 'front', 'end', 'happy'
  ```

- The specific condition that serves as the filtering criterion is passed as an argument to the filter method, and the form is a function.
- Therefore, the filter method is a higher order function because it takes a function specifying the filtering condition as an argument.

  ```javascript
  // Function expression
  const isEven = function (num) {
    return num % 2 === 0;
  };

  let arr = [1, 2, 3, 4];
  // let output = arr.filter(isEven);
  // The function that determines even numbers is passed as a condition to the filter method as an argument
  let output = arr.filter(isEven);
  console.log(output); // [2, 4]

  const isLteFive = function (str) {
    // Lte = less than equal
    return str.length <= 5;
  };

  arr = ['hello', 'front', 'end', 'happy', 'coding'];
  // output = arr.filter(isLteFive);
  // The function that determines length <= 5 is passed as a condition to the filter method as an argument
  let output = arr.filter(isLteFive);
  console.log(output); // 'hello', 'front', 'end', 'happy'
  ```

- When using filter, remember the following process
  - Each element of the array
  - If it is true according to a certain logic (function)
  - It is classified separately (filter)
