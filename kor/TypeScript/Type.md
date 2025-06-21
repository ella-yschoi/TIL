# TypeScript Type

## 1. Boolean(불리언) 타입

- JavaScript와 같은 boolean 값이라고 불리는 참(true), 거짓(false) 값

  ```typescript
  let isShow: boolean = true;
  let isDone: boolean = false;
  ```

<br/>

## 2. Number(숫자) 타입

- JavaScript와 같이 TypeScript 또한 정수와 실수의 구분 없이 Number 타입 하나로 표기
- TypeScript는 이 외에도 추가로 bigint를 지원

  ```typescript
  let number1: number = 5;
  let number2: number = 0.7;
  ```

<br/>

## 3. String(문자열) 타입

- JavaScript와 같이 큰따옴표나 작은따옴표를 사용해 문자열 데이터를 표현
- 또한 백틱을 사용한 문자열인 템플릿 리터럴을 사용하면 여러 줄에 걸쳐 문자열을 작성 가능

  ```typescript
  let firstName: string = "coding";
  let lastName: string = 'kim';
  let longString: string = `Ella is a developer.
  He is 20 years old.`
  ```

<br/>

## 4. Array(배열) 타입

- JavaScript와 같이 값들을 배열로 다룰 수 있으며, 두 가지 방법으로 배열 타입을 선언해 사용 가능
- 첫 번째 방법: 배열의 요소들을 나타내는 타입 뒤에 배열을 나타내는 `[]`을 쓰는 것

  ```typescript
  let items: string[] = ["apple", "banana", "grape"];
  ```

- 두 번째 방법: 제네릭 배열 타입, 즉 Array를 먼저 작성한 뒤, `<>` 안에 배열의 요소들을 나타내는 타입 작성
- 배열 타입은 기본적으로 하나의 타입만 작성, 타입 혼용 작성은 불가

  ```typescript
  let numberList: Array<number> = [4, 6, 10];
  ```

<br/>

## 5. Tuple(튜플) 타입

- TypeScript에서 튜플 타입을 사용하면 요소의 타입과 개수가 고정된 배열 표현 가능
- 배열의 index마다 타입이 정해져 있기 때문에 정확한 index에 접근 필요

  ```typescript
  let user: [string, number, boolean] = ["Ella",  20, true];
  ```

<br/>

## 6. Object(객체) 타입

- TypeScript에서 객체는 JavaScript와 마찬가지로 원시 타입이 아닌 타입을 나타냄
- JavaScript에서 Object 타입은 프로퍼티를 가지는 JavaScript의 값을 말하며 typeof 연산자를 사용했을 때 “object”을 반환하는 모든 타입을 의미함.

  ```typescript
  let obj: object = {};
  ```

- TypeScript에서 object 타입은 모든 객체를 수용하는 타입으로, 객체의 프로퍼티 타입들이 any로 지정되기 때문에 어떠한 프로퍼티라도 추가할 수 있음
- 하지만 **객체의 프로퍼티 타입들을 각기 명시해 주는 것이 훨씬 좋음**
- 객체는 아래 방식으로 key-value에 구체적인 타입까지도 지정

  ```typescript
  let user: {name: string, age: number} = {
    name: "Ella",
    age: 20
  }
  ```

<br/>

## 7. Any 타입

- 알지 못하는 타입 표현이 필요하고 타입 검사를 하지 않고자 할 때 any 타입 사용 가능

  ```typescript
  let maybe: any = 4;
  ```

- any 타입 사용 시, 변수에 값을 재할당하는 경우 타입을 명시한 변수와 달리 **타입에 구애받지 않고 값을 재할당 가능**

  ```typescript
  let obj: object = {};

  // error 발생
  obj = "hello";

  let maybe: any = 4;

  // 정상 작동
  maybe = true;
  ```

- 또한 엄격한 타입 검사를 진행하지 않기에 실제 할당된 값이 가지지 않는 메서드 및 프로퍼티로 접근해도 에러가 나지 않음.
- 대신, 실제 할당된 값이 가지지 않는 메서드 및 프로퍼티이기 때문에 반환되는 값은 undefined

  ```typescript
  let maybe: any = 4;

  console.log(maybe.length) // undefined
  ```

- 또한 any 타입은 타입의 일부만 알고, 전체는 알지 못할 때 유용함.
- 예를 들어 여러 타입이 섞인 배열을 받고자 할 때 유용

  ```typescript
  let list: any[] = [1, true, "free"];

  // any로 다루고 있기에 index 1번째 요소가 boolean 타입이나, number 타입으로 재할당 가능
  list[1] = 100;
  ```
