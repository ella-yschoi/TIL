## **함수** <p>
- 함수는 유사한 동작을 하는 코드가 여러 곳에서 필요할 때가 많다. 예를 들어 사용자가 로그인이나 로그아웃을 할 때 안내 메시지를 보여주는 동작 등. 
- 함수는 프로그램을 구성하는 주요 '구성 요소'이며, 중복 없이 유사한 동작을 하는 코드를 여러번 호출할 수 있다. 

<br/><p>

### **1. 함수 선언문** <p>
- function 키워드, 함수 이름, 괄호로 둘러싼 매개변수를 차례로 써주면 된다. 만약 매개변수가 여러 개라면 콤마로 구분해 준다.
- 이어서 함수를 구성하는 코드의 모임인 함수의 본문(body)을 중괄호로 감싼다.

  ```jsx
  function name(parameter1, parameter2) {
      // 함수 본문
  }
  ```
<br/><p>

### **2. 지역 변수** <p>
- 함수 내에서 선언한 변수인 지역 변수(local variable)는 함수 안에서만 접근할 수 있다.
  
  ```jsx
  function showMessage() {
      let message = 'hello'; // 지역변수
      console.log(message);
  }

  showMessage(); // 'hello'
  console.log(message); // ReferenceError: message is not defined (message는 함수 내 지역 변수이기 때문)
  ```
<br/><p>

### **3. 외부 변수** <p>
- 함수 내부에서 함수 외부 변수인 외부 변수(outer variable)에 접근할 수 있음
  
  ```jsx
  let userName = 'Ella';

  function showMessage() {
    let message = 'Hello, ' + userName;
    console.log(message);
  }

  showMessage(); // Hello, Ella
  ```

- 외부 변수 접근 뿐만 아니라 수정도 가능
  ```jsx
  let userName = 'Ella'

  function showMessage() {
    userName = 'Chloe'; // 외부 변수 수정
    let message = 'Hello, ' + userName;
    console.log(message);
  }

  console.log(userName); // 함수 호출 전이므로 Ella 출력

  showMessage(); // Hello, Chloe: 함수 호출
  console.log(userName); // 함수에 의해 Chloe 출력
  ```

- 외부 변수는 지역 변수가 없는 경우에만 사용 가능. 함수 내부에 외부 변수와 동일한 이름을 가진 변수가 선언되었다면, 내부 변수는 외부 변수를 가림. 
  
  ```jsx
  let userName = 'Ella';

  function showMessage() {
    let userName = 'Chloe'; // 같은 이름을 가진 지역 변수 선언

    let message = 'Hello, ' + userName; // Hello, Chloe: 외부 변수인 Ella는 내부 변수인 Chloe에 가려짐
    console.log(message);
  }
  
  showMessage(); // 함수는 내부 변수인 userName만 사용
  console.log(userName); // Ella : 함수는 외부변수에 접근하지 않으므로 값이 변경되지 않고 Ella 출력
  ```
    cf. userName처럼 함수 외부에 선언된 변수는 전역변수(global variable)이라고 하며, 지역변수에 의해 가려지지만 않는다면 모든 함수에서 접근 가능. 하지만 변수는 연관되는 함수 내에서만 선언하고, 되도록 사용을 권하지 않음.

<br/><p>

### **4. 매개 변수** <p>
- 매개변수(parameter, 인자)를 사용하면 임의의 데이터를 함수 안에 전달할 수 있음. 
- 아래 코드에서 (*), (**) 로 표시한 줄에서 함수 호출 시, 함수에 전달된 인자는 지역변수 from과 text에 각각 복사됨. 이후 함수는 지역변수에 복사된 값을 사용
  
  ```jsx
  function showMessage(from, text) { // 인자: from, text
    console.log(from + ': ' + text);
  } 

  showMessage ('Ella', 'Hello'); // Ella: Hello! (*)
  showMessage ('Chloe', 'Hello'); // Chloe: Hello! (**)
  ````

- 정리하자면, **매개변수, 인자(parameter)** 는 함수 선언 방식 괄호 사이에 있는 변수의 값으로, 선언 시 사용되는 용어다. **인수(argument)** 는 함수의 매개변수에 전달된 값을 말하며, 함수를 호출할 때 사용된다. 즉, 함수 선언 시 **매개변수를 나열**하고, 함수 호출 시 **인자를 전달**해 호출한다.
  
<br/><p>

### **5. 기본값** <p>
- 매개변수에 값을 전달하지 않아도 그 값이 undefined가 되지 않게 하려면 함수 선언시 = 를 사용해 기본값(default value)을 설정해 주면 된다.
  
  ```jsx
  function showMessage(from, text = 'please enter your last name') {
    console.log(from + " " + text);
  }

  showMessage("Ella"); // Ella: please enter your last name: text가 값을 전달받지 못해도 기본값이 할당
  ```

- 아래와 같이 복잡한 표현식도 기본값으로 설정 가능하다.
  
  ```jsx
  function showMessage(from, text = anotherFunction()) {
    // anotherFunction()은 text값이 없을 때만 호출됨
    // anotherFunction()의 반환 값이 text의 값이 됨
  }
  ```

<br/><p>

### **6. 매개변수 기본값을 설정할 수 있는 또다른 방법** <p>
- 가끔은 함수 선언 시가 아닌, **함수 선언 후**에 매개변수 기본값을 설정할 때가 있음. 이때는 함수 호출 시 **매개변수를 undefined와 비교**해 매개변수가 잘 전달되었는지를 확인

  ```jsx
  function showMessage(text) {
      // ...

      if (text === undefined) { // 매개변수 생략 시
          text = '빈 문자열';
      }
      console.log(text);
  }
  showMessage(); // 빈 문자열
  ```

- if문 대신 논리 연산자 || 사용 가능하며, 아래 예시는 매개변수 생략 혹은 빈 문자열이 넘어오면 변수에 '빈 문자열'이 할당되도록 했다.
  
  ```jsx
  function showMessage(text) {
      text = text || '빈 문자열';
  }
  ```

<br/><p>

### **7. 반환값** <p>
- 함수 호출 시, 함수를 호출한 자리에 특정 값을 반환하게 할 수 있다. 이때 이 특정 값을 반환 값(return value)라고 한다. 
- 지시자 return은 함수 내 어디서든 사용 가능하며, 이 return을 만나면 함수 실행은 즉시 중단되고, 함수를 호출한 곳에 값을 반환한다. 아래 예시에서는 반환 값을 result에 할당했다.

  ```jsx
  function sum(a, b) {
    return a + b;
  }

  let result = sum(1, 2); // return에서 반환한 값을 result에 할당
  console.log(result); // 3
  ```

- 아래와 같이 함수 하나에 여러 개의 return문이 올 수도 있다. 
  ```jsx
    function checkAge(age) {
        if (age >= 18) {
            return true;
        } else {
            return confirm('보호자의 동의를 받으셨나요?');
        }
    }

    let age = prompt('나이를 입력해 주세요', 18);

    if (checkAge(age)) {
        alert('접속 허용');
    } else {
        alert('접속 차단');
    }
    ```
- cf. return문이 없는 함수는 undefined를 반환한다.
    ```jsx
    function doNothing() { /*empty */ }
    console.log(doNothing() === undefined); // true
    ```

- cf. return 지시자만 있는 경우도 undefined를 반환한다. return은 return undefined와 동일하게 동작한다.
    ```jsx
    function donNothin() {
        return;
    }
    console.log(doNothing() === undefined); // true
    ```

- caution) return과 값 사이에는 절대 새 줄을 넣어 코드를 작성하면 안된다. 자바스크립트는 return문 끝에 자동으로 세미콜론을 넣기 때문에 반환하고자 했던 표현식을 반환하지 못한다. 
    ```jsx
    // 예를 들면 이런 코드를
    return;
    (1 + 2 + 3 + 4 + 5 + 6)
    
    // 표현식을 여러 줄에 걸쳐 작성하고자 한다면, 아래와 같이 여는 괄호를 return과 같은 줄에 쓰거나, return이 있는 줄에서 표현식을 작성해야 한다.
    return (
        1 + 2 + 3
        + 4 + 5 + 6
    );

<br/><p>

### **8. 함수 이름 짓기** <p>
- 함수는 어떤 **동작**을 수행하기 위해 코드를 모아 놓은 것이므로, 이름은 대개 동사이며, 가능한 어떤 동작을 하는지 간결하고 명확하게 작성해야 한다. 
- 더불어, 함수는 **동작 하나만 담당**하며, 해당 동작을 정확히 수행해야 하는 것이 목적이다.
- 함수가 어떤 동작을 하는지 축약해 설명하는 동사를 접두어로 붙여 함수 이름을 만드는 것이 관습이다. 예를 들면,

  - "show…" - 무언가를 보여줌
  - "get…" – 값을 반환함
  - "calc…" – 무언가를 계산함
  - "create…" – 무언가를 생성함
  - "check…" – 무언가를 확인하고 불린값을 반환함

<br/><p>

### **9. 함수 == 주석** <p>
- 함수를 간결하게 만들면 테스트와 디버깅이 쉬워지며, 함수 그 자체로 주석의 역할까지 해낸다. 이를 '자기 설명적 (self-describing) 코드' 라고 한다. 