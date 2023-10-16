# Recursion

## 1. 재귀함수란?

- 자기 자신을 호출하는 함수
- 재귀를 사용하기 적합한 때
  - 주어진 문제를 비슷한 구조의 더 작은 문제로 나눌 수 있는 경우
  - 중첩된 반복문이 많거나 반복문의 중첩 횟수를 예측하기 어려운 경우
- 예시 코드

  ```javascript
  // 빈 배열을 받았을 때 0을 리턴하는 조건문
  // 가장 작은 문제를 해결하는 코드 & 재귀를 멈추는 코드
  function arrSum(arr) {
    if(arr.length === 0) {
        return 0
    }
    // 배열의 첫 요소 + 나머지 요소가 담긴 배열을 받는 arrSum 함수
    // 재귀를 통해 문제를 작게 쪼개 나가는 코드
    // arrSum([5]) === 5 + arrSum([]) === 5 + 0 === 5;
    // arrSum([4, 5]) === 4 + arrSum([5]) === 4 + 5 === 9;
    return arr.shift() + arrSum(arr)
  }
  ```

<br/>

## 2. 재귀적 사고

### 1. 재귀 함수의 입력값과 출력값 정의하기

- 가장 추상적 or 가장 단순하게 정의하기

### 2. 문제를 쪼개고 경우의 수를 나누기

- 입력값이나 문제의 순서/크기에 따라 쪼개기

### 3. 단순한 문제 해결하기

- 가장 쉬운 문제부터 해결 → 재귀의 기초: 이는 추후 재귀의 탈출 조건을 구성
- 탈출 조건이 없다면 재귀 함수는 자신을 끝없이 호출하므로 문제를 최대한 작게 쪼개기

### 4. 복잡한 문제 해결하기

- 남아있는 복잡한 문제 해결

### 5. 코드 구현하기

```javascript
function recursive (input1, input2, ...) {
    // base case: 문제를 더이상 쪼갤 수 없는 경우
    if (문제를 더이상 쪼갤 수 없을 경우) {
        return 단순한 문제의 해답;
    }

    // recursive case: 그렇지 않은 경우
    return 더 작은 문제로 새롭게 정의된 문제
}
```

<br/>

## 3.JSON.stringigy

### 1. JSON의 탄생 배경

- JSON은 JavaScript Object Notation로서, 서로 다른 프로그램 사이에서 데이터 교환을 위해 만들어진 객체 형태의 포맷

### 2. 메소드

#### `JSON.stringify`: 객체 → JSON로 변환하는 메소드

  ```javascript
  // message 객체를 JSON으로 변환하는 메소드 JSON.stringify

  let transferableMessage = JSON.stringify(message)
  
  console.log(transferableMessage)
  // `{"sender":"Ella","receiver":"Chloe","message":"Hi, Chloe.","createdAt":"2023-04-12 10:10:10"}`

  console.log(typeof(transferableMessage)) // `string`
  ```

#### `JSON.parse`: JSON → 객체로 변환하는 메소드

  ```javascript
  // 직렬화된 JSON에 메소드 JSON.parse를 적용해 다시 객체로 변환: 역질렬화

  let packet = `{"sender":"Ella","receiver":"Chloe","message":"Hi, Chloe.","createdAt":"2023-04-12 10:10:10"}`
  let obj = JSON.parse(packet)

  console.log(obj)
  /*
   * {
   * sender: "Ella",
   * receiver: "Chloe",
   * message: "Hi, Chloe.",
   * createdAt: "2023-04-12 10:10:10"
   * }
   */

  console.log(typeof(obj)) // `object`
  ```

### 3. JSON 기본 규칙

![json_rules.png](/Images/json_rules.png)
