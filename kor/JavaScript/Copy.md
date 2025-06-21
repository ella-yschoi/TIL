# Copy

## 1. 배열을 복사하는 두 가지 방법

### (1) slice

- 원본 배열 복사 가능
- 복사하여 새롭게 생성된 배열은 원본 배열과 같은 요소를 갖지만, 참조하고 있는 주소는 다르다.

     ```javascript
     let arr = [0, 1, 2, 3];
     let copiedArr = arr.slice();
     console.log(copiedArr); // [0, 1, 2, 3]
     console.log(arr === copiedArr); // false
     ```

- 주소가 다르기 때문에 복사한 배열에 요소를 추가해도, 원본 배열에는 추가되지 않는다.

     ``` javascript
     copiedArr.push(4);
     console.log(copiedArr); // [0, 1, 2, 3, 4]
     console.log(arr);// [0, 1, 2, 3]
     ```

### (2) Spread Syntax of Array

- ES6에서 새롭게 추가된 문법으로, 배열을 펼칠 수 있다.
- 배열이 할당된 변수명 앞에 ...을 붙여주면 된다.

    ```javascript
    let arr = [0, 1, 2, 3];
    console.log(...arr); // 0 1 2 3
    ```

- 배열을 생성하는 방법을 먼저 이해해 보자.
- 아래와 같이 같은 요소를 가진 배열을 두 개 만든 후 변수에 각각 할당한다면, 두 변수는 같은 주소를 참조할까?
- 답은, 참조 자료형이기 때문에 각각 다른 주소를 참조한다.

    ```javascript
    let num = [1, 2, 3];
    let int = [1, 2, 3];

    console.log(num === int) // false
    ```

- 또한 새로운 배열 안에 원본 배열을 펼쳐서 전달하면, 원본 배열과 같은 요소를 가지고 있지만 각각 다른 주소를 참조하게 된다.
- 결과적으로 slice() 메서드를 사용한 것과 동일하게 동작하는 것이다.

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

## 2. 객체를 복사하는 두 가지 방법

### (1) Object.assign

   ```javascript
   let obj = {firstName: "Ella", lastName: "Choi"};
   let copiedObj = Object.assign({}, obj);

   console.log(copiedObj) // { firstName: "Ella", lastName: "Choi" }
   console.log(obj === copiedObj) // false
   ```

### (2) Spread Syntax of Object

- 배열 뿐만 아니라, 객체 복사 시에도 사용 가능

    ```javascript
    let obj = {firstNmae: "Ella", lastName: "Choi"};
    let copiedObj = {...obj};

    console.log(copiedObj) // { firstName: "Ella", lastName: "**Choi**" }
    console.log(obj === copiedObj) // false
    ```
