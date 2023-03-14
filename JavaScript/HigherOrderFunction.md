## **1. 일급 객체** ##
- JavaScript에서 함수는 일급 객체이기에 변수를 할당할 수 있음
- 함수 표현식은 할당 전에 사용할 수 없음
- square(7); -> Reference Error 

    ```jsx
    const square = function(num) { // 변수 square에 함수를 할당하는 함수 표현식
        return num * num;
    }; // 변수 square에는 함수가 할당되어 있으므로 일급객체, 함수 호출 연산자 () 사용 가능

    output = square(7);
    ```
- 함수는 일급 객체의 특징을 가지기에 아래처럼 객체 속성의 값으로 할당될 수 있음
    ```jsx
    const cat = {
        name: 'nabi',
        age: 3,
        cry: fuction(){
            console.log('miaow..')
        }
    }
    ```
<br/><p>

## **2. 고차함수의 이해** ##
- 정의: 함수를 전달인자(argument)로 받을 수 있고, 함수를 return할 수 있는 함수
- 다른 함수(caller)의 전달인자로 전달되는 함수를 콜백 함수 (callback function)라고 함
- 콜백 함수를 전달받은 고차함수(caller)는 함수 내부에서 이 콜백함수를 호출(invoke)할 수 있고, 조건에 따라 콜백함수의 실행 여부를 결정할 수도 있음
- 함수를 리턴하는 함수는 커링함수 라고 하며, 이 용어를 사용할 때는 '함수를 전달인자로 받는 함수'에만 한정해 사용하기도 함. 즉, 고차함수가 커링함수를 포함하는 격.
- 정리하자면, '함수를 리턴하는 함수'와 '함수를 전달인자로 받는 함수' 모두 고차함수로 사용

a. 다른 함수를 인자로 받는 경우
  ```jsx
  function double(num) {
      return num * 2;
  }

  function doubleNum(func, num) {
      return func(num);
  }

  // 함수 doubleNum은 다른 함수를 인자로 받는 고차함수
  // 함수 doubleNum의 첫 번째 인자 func에 함수가 들어올 경우, 함수 func은 함수 doubleNum의 콜백함수
  // 아래와 같은 경우, 함수 double은 함수 doubleNum의 콜백함수

  let output = doubleNum(double, 4);
  console.log(output); // 8
  ```

  b. 함수를 리턴하는 경우
  ```jsx
  function adder(added) {
    return fuction (num) {
        return num + added;
    };
  }

  // 함수 adder는 다른 함수를 리턴하는 고차함수
  // adder라는 인자 한 개를 입력받아 함수(익명 함수)를 리턴
  // 리턴되는 익명함수는 인자 한 개를 받아 added와 더한 값을 리턴