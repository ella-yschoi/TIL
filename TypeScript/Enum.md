# Enum

## 1. What is Enum?

- TypeScript's Enum is used to **define a set of specific values**
- Enum is generally used **instead of constant values**, so Enum is widely used in TypeScript
- Enum makes code more **readable** and **prevents mistakes like typos**
- JavaScript doesn't natively support Enum, but TypeScript supports string and numeric Enums in the following form

  ```typescript
  enum Color {
    // Define Color Enum
    // Enum has three values below
    Red,
    Green,
    Blue,
  }
  ```

<br/>

## 2. Numeric Enum

- Enum uses numeric as default value, and each value **automatically starts from 0 and increments by 1**
- Values can also be manually specified as below

  ```typescript
  enum Color {
    Red = 1,
    Green = 2,
    Blue = 4,
  }
  ```

- Arithmetic operations can also be performed on Enum values

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

## 3. String Enum

- String Enum must initialize all Enum values with specific strings or other Enum values

  ```typescript
  // Define Direction Enum based on strings
  enum Direction {
    Up = "UP",
    Down = "DOWN",
    Left = "LEFT",
    Right = "RIGHT",
    }

    // Up, Down, Left, Right each have string values assigned
    // Initialize myDirection variable with Direction.Up
    let myDirection: Direction = Direction.Up;

    // Output result will be "UP"
    console.log(myDirection); // "UP"
  }
  ```

- **String Enum** doesn't have **auto-incrementing** unlike numeric Enum
- When debugging, numeric Enum values may appear unclear, but **string Enum always shows clear values making it easy to read**
- String-based Enum is mainly used **to handle values brought from external sources in TypeScript** (e.g., can define Enum representing HTTP request methods)

  ```typescript
  // Define HttpMethod Enum representing HTTP request methods
  enum HttpMethod {
    Get = 'GET',
    Post = 'POST',
    Put = 'PUT',
    Delete = 'DELETE',
  }

  // makeRequest function takes URL and HTTP request method as arguments
  function makeRequest(url: string, method: HttpMethod) {
    // ...
  }

  makeRequest('/api/data', HttpMethod.Post);
  ```

- When specifying HTTP request methods, use Enum values like HttpMethod.Post
- Using Enum this way can prevent mistakes like typos and improve code readability and stability

<br/>

## 4. Reverse Mappings

- Reverse mapping only exists in numeric Enum and is a **characteristic that doesn't exist in string Enum**
- Can get value from Enum's key and & can also get key from value

  ```typescript
  enum Enum {
    A,
  }

  // Can get value from Enum's key
  let a = Enum.A;

  // Can also get Enum's key from value
  let nameOfA = Enum[a]; // "A"
  ```
