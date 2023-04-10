## **1. 비동기**
### 1. 동기와 비동기
- 동기(synchronous)
  - 특정 코드의 실행이 완료될 때까지 기다리고 난 후, 다음 코드를 수행하는 것
- 비동기(asynchronous)
  - 특정 코드의 실행이 완료될 때까지 **기다리지 않고**, 다음 코드들을 수행하는 것

### 2. 비동기 JavaScript (Timer API)
- setTimeout(callback, millisecond): 일정 시간 후에 함수를 실행
  - parameter: 실행할 콜백 함수, 콜백 함수 실행 전 기다려야 할 시간 (밀리초)
  - return 값: 임의의 타이머 ID
    ```javascript
    setTimeout(function() {
        console.log('1초 후 실행');
    }, 1000); 
    /// 123
    ```

- clearTimeout(timerId): `setTimeout` 타이머를 종료
  - parameter: 타이머 ID
  - return 값: 없음
    ```javascript
    const timer = setTimeout(function () {
    console.log('10초 후 실행');
    }, 10000);
    clearTimeout(timer);
    // setTimeout 종료
    ```

- setInterval(callback, millisecond): 일정 시간 간격을 가지고 함수를 반복적으로 실행
  - parameter: 실행할 콜백함수, 반복적으로 함수를 실행시키기 위한 시간 간격 (밀리초)
  - return 값: 임의의 타이머 ID
    ```javascript
    setInterval(function() {
        console.log('1초마다 실행');
    }, 1000);
    /// 345
    ```

- clearInterval(timerId): `setInterval` 타이머를 종료
  - parameter: 타이머 ID
  - return 값: 없음
    ```javascript
    const timer = setInterval(function() {
        console.log('1초마다 실행');
    }, 1000);
    clearInterval(timer);
    // setInterval 종료
    ```

### 3. Callback
- 비동기로 코드를 제어하는 방법 중 하나는 `callback` 함수 활용
- 그러나, 코드가 길어질수록 복잡하고 가독성이 낮아지는 callback Hell 발생

### 4. Promise, Async/Await
- contents
- contents

<br/><br/>

## **2. Node.js**
### 1. 
- contents
- contents

<br/><br/>

## **3.fetch API**
### 1. 
- contents
- contents