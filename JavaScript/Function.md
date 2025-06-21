# Function

- Functions are often needed when similar code actions are required in multiple places. For example, actions like showing notification messages when users log in or log out. Additionally, functions are major 'building blocks' that make up programs, and you can call code that performs similar actions multiple times without duplication.

<br/>

## 1. Function Declaration

- Write the function keyword, function name, and parameters surrounded by parentheses in order. If there are multiple parameters, separate them with commas.
- Then wrap the function body, which is the collection of code that makes up the function, in curly braces.

  ```javascript
  function name(parameter1, parameter2) {
    // function body
  }
  ```

<br/>

## 2. Local Variables

- Local variables declared within a function can only be accessed inside the function.

  ```javascript
  function showMessage() {
    let message = 'hello'; // local variable
    console.log(message);
  }

  showMessage(); // 'hello'
  console.log(message); // ReferenceError: message is not defined (because message is a local variable within the function)
  ```

<br/>

## 3. Outer Variables

- You can access outer variables (variables outside the function) from within the function

  ```javascript
  let userName = 'Ella';

  function showMessage() {
    let message = 'Hello, ' + userName;
    console.log(message);
  }

  showMessage(); // Hello, Ella
  ```

- You can not only access outer variables but also modify them

  ```javascript
  let userName = 'Ella';

  function showMessage() {
    userName = 'Chloe'; // modify outer variable
    let message = 'Hello, ' + userName;
    console.log(message);
  }

  console.log(userName); // outputs Ella because function hasn't been called yet

  showMessage(); // Hello, Chloe: function call
  console.log(userName); // outputs Chloe due to function
  ```

- Outer variables can only be used when there are no local variables. If a variable with the same name as an outer variable is declared inside the function, the inner variable shadows the outer variable.

  ```javascript
  let userName = 'Ella';

  function showMessage() {
    let userName = 'Chloe'; // declare local variable with same name

    let message = 'Hello, ' + userName; // Hello, Chloe: outer variable Ella is shadowed by inner variable Chloe
    console.log(message);
  }

  showMessage(); // function only uses inner variable userName
  console.log(userName); // Ella: function doesn't access outer variable, so value remains unchanged and outputs Ella
  ```

  cf. Variables declared outside functions like userName are called global variables, and can be accessed from all functions unless shadowed by local variables. However, it's recommended to declare variables only within related functions and avoid using them when possible.

<br/>

## 4. Parameters

- Using parameters allows you to pass arbitrary data into a function.
- In the code below, at the lines marked (\*), (\*\*), when the function is called, the arguments passed to the function are copied to local variables from and text respectively. The function then uses the values copied to the local variables

  ```javascript
  function showMessage(from, text) {
    // parameters: from, text
    console.log(from + ': ' + text);
  }

  showMessage('Ella', 'Hello'); // Ella: Hello! (*)
  showMessage('Chloe', 'Hello'); // Chloe: Hello! (**)
  ```

- To summarize, **parameters** are the variable values between parentheses in function declaration syntax, and are terms used during declaration. **Arguments** refer to values passed to function parameters, and are used when calling functions. In other words, you **list parameters** when declaring functions, and **pass arguments** when calling functions.

<br/>

## 5. Default Values

- To prevent a parameter from becoming undefined when no value is passed, you can set a default value using = during function declaration.

  ```javascript
  function showMessage(from, text = 'please enter your last name') {
    console.log(from + ' ' + text);
  }

  showMessage('Ella'); // Ella: please enter your last name: default value is assigned even if text doesn't receive a value
  ```

- You can also set complex expressions as default values like below.

  ```javascript
  function showMessage(from, text = anotherFunction()) {
    // anotherFunction() is only called when text has no value
    // the return value of anotherFunction() becomes the value of text
  }
  ```

<br/>

## 6. Another Way to Set Parameter Default Values

- Sometimes you need to set parameter default values **after function declaration** rather than during declaration. In this case, you check if parameters are properly passed by **comparing parameters with undefined** during function call

  ```javascript
  function showMessage(text) {
    // ...

    if (text === undefined) {
      // when parameter is omitted
      text = 'empty string';
    }
    console.log(text);
  }
  showMessage(); // empty string
  ```

- You can use the logical OR operator || instead of if statements, and the example below assigns 'empty string' to the variable when the parameter is omitted or an empty string is passed.

  ```javascript
  function showMessage(text) {
    text = text || 'empty string';
  }
  ```

<br/>

## 7. Return Values

- When calling a function, you can make it return a specific value to the place where the function was called. This specific value is called the return value.
- The return directive can be used anywhere within a function, and when it's encountered, function execution immediately stops and returns a value to where the function was called. In the example below, the return value is assigned to result.

  ```javascript
  function sum(a, b) {
    return a + b;
  }

  let result = sum(1, 2); // assign the value returned from return to result
  console.log(result); // 3
  ```

- A function can have multiple return statements like below.

  ```javascript
  function checkAge(age) {
    if (age >= 18) {
      return true;
    } else {
      return confirm('Did you get parental consent?');
    }
  }

  let age = prompt('Please enter your age', 18);

  if (checkAge(age)) {
    alert('Access allowed');
  } else {
    alert('Access denied');
  }
  ```

- cf. Functions without return statements return undefined.

  ```javascript
  function doNothing() {
    /*empty */
  }
  console.log(doNothing() === undefined); // true
  ```

- cf. Functions with only the return directive also return undefined. return works the same as return undefined.

  ```javascript
  function doNothing() {
    return;
  }
  console.log(doNothing() === undefined); // true
  ```

- caution) You should never write code with a new line between return and the value. JavaScript automatically adds a semicolon at the end of return statements, so it cannot return the expression you intended to return.

  ```javascript
  // For example, code like this
  return;
  1 + 2 + 3 + 4 + 5 + 6;

  // If you want to write expressions across multiple lines, you should either write the opening parenthesis on the same line as return, or write the expression on the line with return.
  return 1 + 2 + 3 + 4 + 5 + 6;
  ```

<br/>

## 8. Naming Functions

- Functions are collections of code to perform some **action**, so names are usually verbs and should be written concisely and clearly to indicate what action they perform.
- Additionally, functions should **handle only one action** and their purpose is to perform that action accurately.
- It's conventional to create function names by adding verbs that describe what action the function performs as prefixes. For example,

  - "show…" - shows something
  - "get…" – returns a value
  - "calc…" – calculates something
  - "create…" – creates something
  - "check…" – checks something and returns a boolean value

<br/>

## 9. Function == Comment

- Making functions concise makes testing and debugging easier, and the function itself serves as a comment. This is called 'self-describing code'.
