# Async

## 1. Synchronous and Asynchronous

- Synchronous
  - **Waiting** for specific code execution to complete **before** performing the next code
- Asynchronous
  - **Not waiting** for specific code execution to complete, but performing the next code

<br/>

## 2. Asynchronous JavaScript (Timer API)

### setTimeout(callback, millisecond)

```javascript
setTimeout(function () {
  console.log('Execute after 1 second');
}, 1000);
/// 123
```

- Execute a function after a certain time
- parameter: callback function to execute, time to wait before executing the callback function (milliseconds)
- return value: arbitrary timer ID

### clearTimeout(timerId)

```javascript
const timer = setTimeout(function () {
  console.log('Execute after 10 seconds');
}, 10000);
clearTimeout(timer);
// setTimeout terminated
```

- Terminate `setTimeout` timer
- parameter: timer ID
- return value: none

### setInterval(callback, millisecond)

```javascript
setInterval(function () {
  console.log('Execute every 1 second');
}, 1000);
/// 345
```

- Execute a function repeatedly at regular time intervals
- parameter: callback function to execute, time interval for repeatedly executing the function (milliseconds)
- return value: arbitrary timer ID

### clearInterval(timerId)

```javascript
const timer = setInterval(function () {
  console.log('Execute every 1 second');
}, 1000);
clearInterval(timer);
// setInterval terminated
```

- Terminate `setInterval` timer
- parameter: timer ID
- return value: none

<br/>

## 3. Callback

- One way to control code asynchronously is to utilize `callback` functions
- However, as code gets longer, callback Hell occurs, making it complex and reducing readability

<br/>

## 4. Promise

### new Promise

- `Promise` is a class, so create a `Promise` object using the `new` keyword
- `Promise` takes a callback function that performs asynchronous processing as an argument, and this callback function receives `resolve` and `reject` functions as arguments
- When a `Promise` object is created, the callback function is automatically executed
- If the code is processed well, call the `resolve` function, and if an error occurs, call the `reject` function

  ```javascript
  let promise = new Promise((resove, reject) => {
    // 1. When processed normally, pass value to resolve's argument
    resolve(value);

    // 2. When error occurs, pass error message to reject's argument
    reject(value);
  });
  ```

### Promise Object's Internal Properties

- The Promise object returned by `new Promise` has `state` and `result` internal properties
- However, cannot access directly and must use `.then`, `.catch`, `.finally` methods to access

### State

- Default state is `pending`. If the callback function performing asynchronous processing works well → changes to `fulfilled`, if error occurs → `rejected`

### Result

- Default state is `undefined`. If the callback function performing asynchronous processing works well and `resolve(value)` is called → changes to value, if error occurs and `reject(error)` is called → changes to `error`

### Then

- If the code written in the callback function is processed well, call the `resolve` function → can access through `.then` method
- If the value returned in `.then` is a `Promise`, receive the `Promise`'s internal property `result` as the argument of the next `.then`'s callback function
- If it's not a `Promise`, can receive the returned value as the argument of `.then`'s callback function

  ```javascript
  let promise = new Promise((resolve, reject) => {
    resolve('Success');
  });

  promise.then((value) => {
    console.log(value); // "Success"
  });
  ```

### Catch

- When an error occurs in the code written in the callback function, call the `reject` function and can access through `.catch` method

  ```javascript
  let promise = new Promise(function (resolve, reject) {
    reject(new Error('Error'));
  });

  promise.catch((error) => {
    console.log(error); // Error: Error
  });
  ```

### Finally

- Can access through `.finally` method regardless of whether the code written in the callback function is processed normally

  ```javascript
  let promise = new Promise(function (resolve, reject) {
    resolve('Success');
  });

  promise
    .then((value) => {
      console.log(value); // "Success"
    })
    .catch((error) => {
      console.log(error);
    })
    .finally(() => {
      console.log('Works whether success or failure'); // "Works whether success or failure"
    });
  ```

### Promise Chaining

- When asynchronous tasks need to be performed sequentially

### Promise all()

- Used when you want to process multiple asynchronous tasks simultaneously
- Takes an array as an argument, and if all the code written in the callback functions of all `Promise` in that array is processed normally, stores the results in an array and returns a new `Promise`
- Additionally, if any of the `Promise` in the argument array encounters an error, immediately terminates regardless of the state of the remaining `Promise`

  ```javascript
  Promise.all([promiseOne(), promiseTwo(), promiseThree()])
    .then((value) => console.log(value)) // ['1초', '2초', '3초']
    .catch((err) => console.log(err));
  ```

<br/>

## 5. Async, Await

- Can write complex `Promise` code concisely using `async` and `await`
- Use `async` before a function and use the `await` keyword only inside `async` functions: code written this way runs the next code after the code with the `await` keyword runs

  ```javascript
  // Function declaration
  async function funcDeclarations() {
    await code you want to write
    ...
  }

  // Function expression
  const funcExpression = async function () {
    await code you want to write
    ...
  }

  // Arrow function
  const ArrowFunc = async() => {
    await code you want to write
    ...
  }
  ```

<br/>

## 6. fetch API

### fetch API

- Role of receiving information from a specific URL
- This process is asynchronous, so it may take some time depending on the situation

  ```javascript
  let url = 'https://koreanjson.com/posts/1';
  fetch(url)
    .then((response) => response.json())
    .then((json) => console.log(json))
    .catch((error) => console.log(error));
  ```

<br/>

## 7. Axios

- A library that performs a similar role to fetch API
- An HTTP asynchronous communication library that utilizes Promise API for browsers and Node.js
- Easier to use than Fetch API with additional features included
- A third-party library that requires installation
- Automatically converts to JSON data format

### GET Request

```shell
axios.get("url"[,config])
```

### POST Request

```shell
axios.post("url"[, data[, config]])
```
