# TypeScript의 연산자 활용 타입

## 1. 유니온(Union) 타입

- 둘 이상의 타입을 합쳐서 만들어진 새로운 타입
- `|` 연산자를 이용하며, 자바스크립트의 || (OR) 연산자와 같이 “A이거나 B이다”라는 의미의 타입 (e.g. `number | string` : 숫자 또는 문자열 타입)

- `value` 매개변수의 타입을 `any`로 정의하고, 타입이 `number`인지 `string`인지에 따라 if-else 문으로 나누어 출력한 경우

  ```javascript
    function printValue(value: any): void {
    if (typeof value === "number") {
        console.log(`The value is a number: ${value}`);
    } else {
        console.log(`The value is a string: ${value}`);
    }
    }

    printValue(10); // The value is a number: 10
    printValue("hello"); // The value is a string: hello
  ```

- `any` 사용은 JavaScript 작성 코드와 큰 차이가 없기에, 유니온 타입을 사용해 TypeScript의 이점을 살리 코딩하는 것이 좋음
  
  ```typescript
  function printValue(value: number|string): void {
    if (typeof value === "number") {
        console.log(`The value is a number: ${value}`);
    } else { 
        console.log(`The value is a string: ${value}`);
    }
  }

  printValue(10); // The value is a number: 10
  printValue("hello"); // The value is a string: hello
  ```

- 위의 `printValue` 함수는 숫자 또는 문자열 값을 입력받고 있음.
- 이때, 유니온 타입을 사용해 `number | string` 타입으로 지정하고 있음.
- 이후 입력된 값의 타입을 typeof 연산자를 사용하여 검사 → 해당 값이 숫자인 경우와 문자열인 경우 각각 다른 로그를 출력
- 이처럼 **유니온 타입은 다양한 타입의 값을 처리해야 하는 경우 유용**

### (1) 유니온(Union) 타입의 장점

- 타입을 추론할 수 있기에, 타입에 관련된 API를 쉽게 자동완성으로 얻어낼 수 있음
- 코드의 가독성을 높일 수 있음: 타입으로 선언된 변수는 문자열, 숫자, 불리언 타입 중 하나의 값을 가질 수 있다는 것이 명시적으로 표시되어 코드를 이해하기 쉽게 만들어 줌
  
  ```typescript
  let value: string | number | boolean;
  ```

### (2) 유니온(Union) 타입 사용 시 유의할 점

- 유니온에 있는 모든 타입에 공통인 멤버들에만 접근할 수 있기 때문에 유의해야 함
  
  ```typescript
  // interface를 사용해 Developer와 Person을 정의
  interface Developer {
    name: string;
    skill: string;
  }

  interface Person {
    name: string;
    age: number;
  }
  ```

  ```typescript
  function askSomeone(someone: Developer | Person) {
    console.log(someone.name);
  }
  ```

- 실질적으로 `askSomenone` 함수 내부에서는 `Developer`와 `Person`이 갖고 있는 공통 프로퍼티인 `name`에만 접근 가능. **공통되고 보장된 프로퍼티만 제공해야** 하기 때문
- 만약 나머지 프로퍼티에도 접근하고 싶다면 **타입 가드**를 사용해야 함. (타입 가드: TypeScript에서 타입을 보호하기 위해 사용되는 기능 중 하나로, 특정 코드 블록에서 **타입의 범위를 제한해 해당 코드 블록 안에서 타입 안정성을 보장**해 줌)

  ```typescript
  function askSomeone(someone: Developer | Person) {
    // in 연산자 : 타입스크립트에서 객체의 속성의 존재 여부를 체크하는 연산자
    // in 연산자는 객체의 속성 이름과 함께 사용하여 해당 속성이 객체 내에 존재하는지 여부를 검사
    
    if ('skill' in someone) {
        console.log(someone.skill);
    }

    if ('age' in someone) {
        console.log(someone.age);
    }
  }
  ```

<br/>

## 2. 인터섹션(Intersection) 타입

- 둘 이상의 타입을 **결합하여 새로운 타입**을 만드는 방법
- `&` 연산자를 사용하여 표현

- 타입을 결합해 아래 `Developer`와 `Person` 각각에 정의된 속성 모두 받음

  ```typescript
  interface Developer {
    name: string;
    skill: string;
  }

  interface Person {
    name: string;
    age: number;
  }

  // 타입 결합
  type User = Developer & Person;
  ```

- `&`로 타입을 연결해 하나의 단일 타입으로 표현할 수 있기에, **타입 가드가 필요 없음**
- `askSomeone` **함수 내에 정의된 프로퍼티에 전부 접근** 가능

  ```typescript
    interface Developer {
    name: string;
    skill: string;
    }

    interface Person {
    name: string;
    age: number;
    }

    // 타입 결합해 가드 필요 X
    function askSomeone(someone: Developer & Person) {
        console.log(someone.age);
        console.log(someone.name);
        console.log(someone.skill);
    }
  ```

- 반면 `Developer`와 `Person`이라는 새로운 교집합을 만들어 내는 것이기에, 전달인자를 전달할 때 **모든 프로퍼티를 전부** 보내줘야만 함.
- 반대로 유니온 타입은 타입 가드를 해줘야 하지만 전달인자를 전달할 때 선택지가 생기게 됨

  ```typescript
    interface Developer {
    name: string;
    skill: string;
    }

    interface Person {
    name: string;
    age: number;
    }

    function askSomeone(someone: Developer | Person) {
        // 아래와 같이 프로퍼티에 접근
        if ('skill' in someone) {
            console.log(someone.skill);
        }

        if ('age' in someone) {
            console.log(someone.age);
        }
    }

    // 유니온 타입은 전달인자를 전달할 때 선택지가 생김
    askSomeone({name: '김코딩', skill: '웹 개발'});
    askSomeone({name: '김코딩', age: 20});

    function askSomeone2(someone: Developer & Person) {
        // 타입 가드를 사용하지 않아도 모든 프로퍼티에 접근할 수 있음
        console.log(someone.age);
        console.log(someone.name);
        console.log(someone.skill);
    }

    // 그러나 인터섹션 타입으로 결합하게 된다면 전달인자를 전달할 때 선택지가 없음
    askSomeone2({name: '김코딩', skill: '웹 개발', age: 20});

  ```
