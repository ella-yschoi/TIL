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
    function adder(added) { // 함수 adder는 
        return fuction (num) { // 인자 한 개를 입력받아 다른 함수(익명함수)를 리턴하는 고차함수
            return num + added; // 리턴되는 익명함수는 인자 한 개를 받아 added와 더한 값을 리턴
        };
    }

    // adder(5)는 함수이므로 함수 호출 연산자 () 사용 가능
    let output = adder(5)(3); // 8
    console.log(output); // 8

    // adder가 리턴하는 함수를 변수에 저장 가능
    // javascript에서 함수는 일급 객체이기 때문
    const add3 = adder(3);
    output = add3(2);
    console.log(output); // 5
    ```

    c. 함수를 인자로 받고, 함수를 리턴하는 경우
    ```jsx
    function double(num) { 
        return num * 2
    }
    // 함수 doubleAdder는 고차함수
    // 함수 doubleAdder의 인자 func는 함수 doubleAdder의 콜백함수
    // 함수 double은 함수 doubleAdder의 콜백으로 전달됨
    function doubleAdder(added, func) { 
        const doubled = func(added);
        return function(num) {
            return num + doubled;
        };
    }
    // doubleAdder(5, double)는 함수이므로 함수 호출 기호 () 사용 가능
    doubleAdder(5, double)(3); // 13
    
    // doubleAdder가 리턴하는 함수를 변수에 저장 가능 (일급 객체)
    const addTwice3 = doubleAdder(3, double);
    addTwice(2); // 8
    ```
<br/><p>

## **3. 내장 고차 함수** ##
- JavaScript에서는 기본적으로 내장된 고차함수가 여러 개 있는데, 그 중 배열 메소드들 중 일부가 대표적인 고차함수에 해당됨.
- 배열의 filter 메소드는 모든 배열의 요소 중 특정 조건을 만족하는 요소를 '걸러내는' 메소드

    ```jsx
    let arr = [1, 2, 3, 4];
    let output = arr.filter(짝수);
    console.log(output); // [2, 4]

    arr = ['hello', 'front', 'end', 'happy', 'coding'];
    output = arr.filter(길이 5 이하) // *syntax error : 이 코드는 의미만 이해하기
    console.log(output); // 'hello', 'front', 'end' 'happy'
    ```

- 여기서 걸러내는 기준이 되는 특정 조건은 filter 메소드의 전달인자로 전달되며, 형태는 함수 형태임.
- 따라서 filter 메소드는 걸러내기 위한 조건을 명시한 함수를 전달인자로 받기에 고차함수.
  ```jsx
  // 함수 표현식
  const isEven = function (num) {
    return num % 2 === 0;
  };

  let arr = [1, 2, 3, 4];
  // let output = arr.filter(짝수);
  // 짝수를 판별하는 함수가 조건으로서 filter 메소드의 전달인자로 전달됨
  let output = arr.filter(isEven);
  console.log(output); // [2, 4]

  const isLteFive = function (str) {
    // Lte = less than equal
    return str.length <= 5;
  };

  arr = ['hello', 'front', 'end', 'happy', 'coding'];
  // output = arr.filter(길이 5 이하)
  // 길이 5 이하를 판별하는 함수가 조건으로서 filter 메소드의 전달인자로 전달됨
  let output = arr.filter(isLteFive);
  console.log(output); // 'hello', 'front', 'end' 'happy'
  ```

- filter 활용 시 아래 과정을 기억할 것
  - 배열의 각 요소가
  - 특정 논리 (함수)에 따르면, 사실(true)일 때
  - 따로 분류한다 (filter)

