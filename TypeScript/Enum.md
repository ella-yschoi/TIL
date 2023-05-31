# Enum

## 1. 열거형(Enum)이란?

- TypeScript의 열거형(Enum)은 **특정 값의 집합을 정의**할 때 사용됨.
- Enum은 일반적으로 **상수값을 대신하여 사용**되므로, 타입스크립트에서는 Enum이 많이 사용
- Enum은 코드를 더욱 **가독성 높게** 만들어주고, **오타와 같은 실수를 방지**해줌
- JavaScript에서는 기본적으로 Enum을 지원하지 않지만, TypeScript에서는 문자형 Enum과 숫자형 Enum을 지원하며, 아래와 같은 형태로 지원
  
  ```typescript
  enum Color {
    
    // Color 라는 Enum 정의
    // Enum의 값은 아래 세 개
    Red, 
    Green,
    Blue,
  }
  ```

<br/>

## 2. 숫자형 열거형(Enum)

- Enum은 디폴트 값으로 숫자형을 사용하며, 각 값은 **자동으로 0부터 시작하여 1씩 증가**
- 아래와 같이 수동으로 값을 지정할 수도 있음

  ```typescript
    enum Color {
    Red = 1,
    Green = 2,
    Blue = 4,
    }
  ```

- Enum 값에 대해 산술 연산 수행도 가능
  
  ```typescript
  enum Color {
    Red = 1,
    Green = 2,
    Blue = 4,
  }

  let c: Color = Color.Green;
  let greenValue: number = Color.Green;
  let blueValue: number = Color.Blue;

    console.log(c); // 2
    console.log(greenValue); // 2
    console.log(blueValue); // 4 
  ```

<br/>

## 3. 문자형 열거형(Enum)

- 문자형 Enum은 Enum의 값을 전부 다 특정 문자 또는 다른 Enum 값으로 초기화해야 함

  ```typescript
  // Direction 이라는 문자열 기반의 Enum을 정의
  enum Direction {
    Up = "UP",
    Down = "DOWN",
    Left = "LEFT",
    Right = "RIGHT",
    }

    // Up, Down, Left, Right 각각에는 문자열 값이 할당되어 있고
    // myDirection 변수를 Direction.Up 으로 초기화 하기에
    let myDirection: Direction = Direction.Up;

    // 출력 결과로는 "UP"이 나오게 됨
    console.log(myDirection); // "UP"
  }
  ```

- **문자형 Enum**에는 숫자형 Enum과는 다르게 **auto-incrementing이 없음**.
- 디버깅 시 숫자형 Enum의 값은 불명확하게 나올 때가 있지만 **문자형 Enum은 항상 명확한 값이 나와 읽기 편함**.
- 문자열 기반의 Enum은 주로 **외부에서 가져온 값을 TypeScript에서 다루기 위해**서 사용됨 (e.g. HTTP 요청 방식을 나타내는 Enum 정의 가능)
  
  ```typescript
  // HTTP 요청 방식을 나타내는 HttpMethod Enum을 정의
  enum HttpMethod {
    Get = "GET",
    Post = "POST",
    Put = "PUT",
    Delete = "DELETE",
  }

  // makeRequest 함수는 URL과 HTTP 요청 방식을 인자로 받음
  function makeRequest(url: string, method: HttpMethod) {
    // ...
  }

  makeRequest("/api/data", HttpMethod.Post);
  ```

- HTTP 요청 방식을 지정할 때는 HttpMethod.Post와 같이 Enum 값을 사용함.
- 이렇듯 Enum 사용 시 오타와 같은 실수 방지 가능, 코드의 가독성과 안정성을 높일 수 있음.

<br/>

## 4. 역 매핑 (Reverse mappings)

- 역 매핑은 숫자형 Enum에만 존재하며, **문자형 Enum에는 존재하지 않는 특징**임.
- 열거형의 키(key)로 값(value)을 얻을 수 있고 & 값(value)으로 키(key)를 얻을 수도 있음.

  ```typescript
    enum Enum {
        A
    }

    // Enum의 키로 값을 얻을 수 있음
    let a = Enum.A;

    // 값으로도 Enum의 키를 얻을 수 있음
    let nameOfA = Enum[a]; // "A"
  ```
