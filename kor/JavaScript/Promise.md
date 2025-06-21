# Promise

## new Promise

- `Promise`는 class이기에 `new` 키워드를 통해 `Promise` 객체를 생성
- `Promise`는 비동기 처리를 수행할 콜백함수를 인수로 받는데, 이 콜백함수는 `resolve`, `reject` 함수를 인수로 전달받음
- `Promise` 객체가 생성되면 콜백함수는 자동으로 실행됨
- 코드가 잘 처리되었다면 `resolve`함수를 호출하고, 에러 발생 시 `reject`함수를 호출

    ```javascript
    let promise = new Promise((resove, reject) => {
        // 1. 정상적으로 처리되는 경우 resolve의 인자에 값 전달
        resolve(value);

        // 2. 에러 발생시 reject의 인자에 에러메시지 전달
        reject(value);
    })
    ```

<br/>

## Promise 객체의 내부 프로퍼티

- `new Promise`가 반환하는 Promise 객체는 `state`, `result` 내부 프로퍼티를 가짐
- 다만, 직접 접근할 수 없고 `.then`, `.catch`, `.finally` 메소드 사용해 접근 가능
- State
  - 기본 상태는 `pending`. 비동기 처리를 수행할 콜백함수가 잘 작동했다면 → `fulfilled`로 변경, 에러 발생 시 `rejected`
- Result
  - 기본 상태는 `undefined` 비동기 처리를 수행할 콜백함수가 잘 작동하여 `resolve(value)` 호출되면 → value로, 에러 발생해 `reject(error)` 호출되면 → `error` 로 변경

<br/>

## then, catch, finally

### then

- 콜백함수에 작성했던 코드들이 잘 처리되었다면 `resolve` 함수 호출 → `.then` 메소드로 접근 가능
- `.then` 안에서 리턴한 값이 `Promise`라면 `Promise` 내부 프로퍼티 `result`를 다음 `.then`의 콜백함수의 인자로 받아옴
- `Promise`가 아니라면 리턴한 값을 `.then`의 콜백함수 인자로 받아올 수 있음

    ```javascript
    let promise = new Promise((resolve, reject) => {
        resolve("성공");
    });

    promise.then(value => {
        console.log(value); // "성공"
    })
    ```

### Catch

- 콜백함수에 작성한 코드의 에러 발생 시 `reject`함수를 호출하고 `.catch` 메소드로 접근 가능

    ```javascript
    let promise = new Promise(function(resolve, reject) {
    reject(new Error("에러"))
    });

    promise.catch(error => {
    console.log(error); // Error: 에러
    })
    ```

### Finally

- 콜백함수에 작성한 코드들이 정상 처리 여부와 관계 없이 `.finally` 메소드로 접근 가능

  ```javascript
  let promise = new Promise(function(resolve, reject) {
    resolve("성공");
  });

  promise
  .then(value => {
    console.log(value); // "성공"
  })
  .catch(error => {
    console.log(error);
  })
  .finally(() => {
    console.log("성공이든 실패든 작동"); // "성공이든 실패든 작동"
  })
  ```

### Promise Chaining

- 비동기 작업을 순차적으로 진행해야 하는 경우
- Promise all()
- 여러 개의 비동기 작업을 동시에 처리하고 싶을 때 사용
- 인자로는 배열을 받으며, 해당 배열에 있는 모든 `Promise`에서 콜백함수 내 작성했던 코드들이 정상적으로 처리되었다면 결과를 배열에 저장해 새로운 `Promise`를 반환
- 더불어, 인자로 받은 배열의 `Promise` 중 하나라도 에러 발생 시, 나머지 `Promise` state와 상관없이 즉시 종료

    ```javascript
    Promise.all([promiseOne(), promiseTwo(), promiseThree()])
        .then((value) => console.log(value)) // ['1초', '2초', '3초']
        .catch((err) => console.log(err));
    ```
