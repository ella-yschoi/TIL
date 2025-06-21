# Promise

## new Promise

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

<br/>

## Promise Object's Internal Properties

- The Promise object returned by `new Promise` has `state` and `result` internal properties
- However, cannot access directly and must use `.then`, `.catch`, `.finally` methods to access
- State
  - Default state is `pending`. If the callback function performing asynchronous processing works well → changes to `fulfilled`, if error occurs → `rejected`
- Result
  - Default state is `undefined`. If the callback function performing asynchronous processing works well and `resolve(value)` is called → changes to value, if error occurs and `reject(error)` is called → changes to `error`

<br/>

## then, catch, finally

### then

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
- Promise all()
- Used when you want to process multiple asynchronous tasks simultaneously
- Takes an array as an argument, and if all the code written in the callback functions of all `Promise` in that array is processed normally, stores the results in an array and returns a new `Promise`
- Additionally, if any of the `Promise` in the argument array encounters an error, immediately terminates regardless of the state of the remaining `Promise`

  ```javascript
  Promise.all([promiseOne(), promiseTwo(), promiseThree()])
    .then((value) => console.log(value)) // ['1초', '2초', '3초']
    .catch((err) => console.log(err));
  ```
