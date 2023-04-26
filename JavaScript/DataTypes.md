## **자료형** <p>

### **1. 숫자형** <p>
- 어느 숫자든 0으로 나누면 무한대
  
  ```javascript
  console.log(1 / 0); // Infinity
  ```

- Infinity를 직접 참조도 가능
  
  ```javascript
  console.log(Infinity); // Infinity
  ```

- NaN은 계산 중 에러가 발생했다는 의미이며, 추가연산해도 결국 NaN 반환됨

  ```javascript
  console.log("숫자 아님" / 2); // NaN
  ``` 

<br/>

### 2. **BigInt** <p>
- 자바스크립트에서는 일정 수준으로 크거나 작은 값 이하로는 숫자형으로 나타낼 수 없지만, 길이에 상관없이 정수 리터럴 끝에 n을 붙이면 만들 수 있음.
  
  ```javascript
  const bigInt = 123456789123456789n;
  ```

<br/>

### **3. 문자형** <p>
- 따옴표에는 세 가지가 있음
  
   ```javascript
   let str = "Hello"; // 큰 따옴표
   let str2 = 'Ella Yeonsu Choi'; // 작은 따옴표
   let phrase = `Nice to meet you`; // 백틱
   ```

- 백틱으로 변수는 표현식을 감싼 후, ${...} 안에 넣어주면, 원하는 변수나 표현식을 문자열 중간에도 넣을 수 있음 (큰 따옴표나 작은 따옴표는 확장 가능을 지원하지 않음)
  
  ```javascript
  let name = "Ella"

  // 변수를 문자열 중간에 삽입
  console.log(`Hello, ${name}!`) // Hello, Ella!

  // 표현식을 문자열 중간에 삽입
  console.log(`the result is ${1 + 2}`); // the result is 3
  ```
<br/>

### **4. Boolean형** <p>
- true, false 두 가지 값 밖에 없으며, 비교 결과를 저장할 때도 사용됨 
  
  ```javascript
  let isGreater = 4 > 1;
  console.log(isGreater); // true
  ```

<br/>

### **5. null 값** <p>
- 위의 자료형 중 어느 자료형에도 속하지 않는 값이며, 오로지 null 값만 포함하는 별도의 자료형임. 
- 의미는 존재하지 않는 (nothing) 값, 비어있는(empty) 값, 알 수 없는(unknown) 값을 명시적으로 나타냄.
  
  ```javascript
  let age = null; // 알 수 없음, 비어있음
  ```
<br/>

### **6. undefined 값** <p>
- null과 마찬가지로, '값이 할당되지 않은 상태'를 암시적으로 나타내며, 변수를 선언했으나 값이 할당되지 않았을 때 해당 변수에 undefined가 할당됨

  ```javascript
  let age; // 변수를 선언했으나 변수를 할당하지 않음
  console.log(age); // 'undefined'
  ```

- 변수에 undefined를 할당하는 것도 가능하나, 직접 할당은 권하지 않고 이때는 null 사용 권장하고 변수의 초기값을 위해 예약어로 남겨두기.

<br/>

### **7. 객체와 심볼** <p>
- 객체(object)형을 제외한 다른 자료형은 문자열이든 숫자든 **한 가지만 표현** 할 수 있기 때문에 원시(primitive) 자료형이라 부름. 반면, 객체는 data collection이나 복잡한 entity를 표현 가능.
- 심볼(symbol)형은 객체의 고유한 식별자(unique identifier)를 만들 때 사용됨 
  
<br/>

### **8. typeof 연산자** <p>
- 인수의 자료형을 반환하며, 두 가지 형태의 문법 지원
  
    - 연산자: typeof x
    - 함수: typeof(x) <p>
  ```javascript
  typeof undefined // 'undefined'
  typeof 0 // 'number'
  typeof 10n // 'bigint'
  typeof Symbol("id") // 'symbol'
  typeof Math // 'object'
  typeof null // 'object'
  typeof alert // 'function'
  ```
- Math는 수학 연산을 제공하는 *내장객체 이므로 'object'가 출력됨. 참고로 내장객체란, 자바스크립트가 기본적으로 가지고 있는 객체로 function, array, number, string 등이 포함된다. 
- null은 고유한 자료형을 가지는 특수 값으로 객체가 아니나, 하위 호환성 유지를 위해 언어 자체 오류라도 놔둔 것임.
- typeof는 피연산자가 함수면 'function'을 반환하나, 함수형 이라는 것은 없고 함수는 객체형에 속함. 