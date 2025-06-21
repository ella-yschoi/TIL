# TypeScript Funtion

## JavaScript vs. TypeScript

- JavaScript ver.
  
    ```javascript
    // named function
    function add(x, y){
        return x + y;
    }

    // arrow function
    let add = (x, y) => {
        return x + y;
    }
    ```

- TypeScript ver.

  ```typescript
  // named function
  function add(x: number, y: number): number {
    return x + y;
  }

  // arrow function
  let add = (x: number, y: number): number => {
    return x + y;
  }
  ```

- TypeScript에서 함수를 표현할 때는 **매개변수의 타입**과 **반환 타입**을 명시해야 함
- 각 매개변수에 해당하는 타입을 작성한 뒤, **반환되는 타입을 괄호 뒤에 작성** 해줘야 함 (타입 추론 기능을 활용하지 않는다고 가정했을 때)
- 만일 함수에 **리턴값이 없다면**, `void`를 사용해 작성 가능 (타입 추론 기능을 활용하지 않는다고 가정했을 때)

  ```typescript
  let printAnswer = (): void => {
    console.log("YES");
  }
  ```

- TypeScript는 JavaScript와 달리 **매개변수의 개수에 맞춰 전달인자를 전달**해야 함

  ```typescript
  let greeting = (firstName: string, lastName: string): string => {
    return `hello, ${firstName} ${lastName}`;
  }

  // 에러 발생
  greeting('coding');

  // 정상 작동
  greeing('coding', 'kim');

  // 에러 발생
  greeting('coding', 'kim', 'hacker');
  ```

- 만약 전달인자를 전달하지 않거나, undefined를 전달했을 때 할당될 매개변수의 값을 정해놓을 수도 있음.
- 이는 JavaScript에서의 default parameter와 같은 동작을 함.

  ```typescript
  let greeting = (firstName: string, lastName: string ="kim"): string => {
        return `hello, ${firstName} ${lastName}`;
    }

    // 정상 작동 
    greeting('coding');

    // 정상 작동
    greeting('coding', undefined);

    // 에러 발생
    greeting('coding', 'kim', 'hacker');
  ```

- 혹은 선택적 매개변수를 원한다면 **매개변수의 이름 끝에 ?**를 붙임으로써 해결할 수도 있음

  ```typescript
    let greeting = (firstName: string, lastName?: string): string => {
        return `hello, ${firstName} ${lastName}`;
    }

    // 정상 작동
    greeting('coding');

    // 정상 작동
    greeting('coding', 'kim');

    // 에러 발생
    greeting('coding', 'kim', 'hacker');
  ```
