# TypeScript Operator Type Usage

## 1. Union Type

- New type created by combining two or more types
- Uses `|` operator, like JavaScript's || (OR) operator, meaning "A or B" type (e.g. `number | string`: number or string type)

- When defining `value` parameter type as `any` and outputting with if-else statement according to whether type is `number` or `string`

  ```javascript
  function printValue(value: any): void {
    if (typeof value === 'number') {
      console.log(`The value is a number: ${value}`);
    } else {
      console.log(`The value is a string: ${value}`);
    }
  }

  printValue(10); // The value is a number: 10
  printValue('hello'); // The value is a string: hello
  ```

- Using `any` doesn't differ much from JavaScript code, so it's better to code utilizing TypeScript's advantages using union types

  ```typescript
  function printValue(value: number | string): void {
    if (typeof value === 'number') {
      console.log(`The value is a number: ${value}`);
    } else {
      console.log(`The value is a string: ${value}`);
    }
  }

  printValue(10); // The value is a number: 10
  printValue('hello'); // The value is a string: hello
  ```

- The above `printValue` function receives number or string values
- At this time, using union type to specify as `number | string` type
- Then check the type of input value using typeof operator → output different logs for number and string cases respectively
- Like this, **union types are useful when you need to handle values of various types**

### (1) Advantages of Union Type

- Can infer types, so can easily get type-related APIs through autocomplete
- Can improve code readability: explicitly shows that variables declared with types can have one value among string, number, boolean types, making code easier to understand

  ```typescript
  let value: string | number | boolean;
  ```

### (2) Points to Note When Using Union Type

- Need to be careful because you can only access members common to all types in the union

  ```typescript
  // Define Developer and Person using interface
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

- In the `askSomeone` function, can only access `name`, which is the common property that `Developer` and `Person` have. Because **only common and guaranteed properties should be provided**
- If you want to access other properties, you need to use **type guards** (Type guards: One of the features used to protect types in TypeScript, **restricts type scope in specific code blocks to ensure type safety within that code block**)

  ```typescript
  function askSomeone(someone: Developer | Person) {
    // in operator: operator that checks existence of object properties in TypeScript
    // in operator is used with object property names to check whether that property exists within the object

    if ('skill' in someone) {
      console.log(someone.skill);
    }

    if ('age' in someone) {
      console.log(someone.age);
    }
  }
  ```

<br/>

## 2. Intersection Type

- Method of **combining two or more types to create a new type**
- Expressed using `&` operator

- Combines types to receive all properties defined in `Developer` and `Person` respectively below

  ```typescript
  interface Developer {
    name: string;
    skill: string;
  }

  interface Person {
    name: string;
    age: number;
  }

  // Type combination
  type User = Developer & Person;
  ```

- Can express as a single type by connecting types with `&`, so **no type guards needed**
- Can access **all properties defined in the `askSomeone` function**

  ```typescript
  interface Developer {
    name: string;
    skill: string;
  }

  interface Person {
    name: string;
    age: number;
  }

  // Type combination, no guards needed
  function askSomeone(someone: Developer & Person) {
    console.log(someone.age);
    console.log(someone.name);
    console.log(someone.skill);
  }
  ```

- However, since it creates a new intersection of `Developer` and `Person`, when passing arguments, **all properties must be sent**
- Conversely, union types need type guards but get choices when passing arguments

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
    // Access properties like below
    if ('skill' in someone) {
      console.log(someone.skill);
    }

    if ('age' in someone) {
      console.log(someone.age);
    }
  }

  // Union types get choices when passing arguments
  askSomeone({ name: '김코딩', skill: '웹 개발' });
  askSomeone({ name: '김코딩', age: 20 });

  function askSomeone2(someone: Developer & Person) {
    // Can access all properties without using type guards
    console.log(someone.age);
    console.log(someone.name);
    console.log(someone.skill);
  }

  // However, when combining with intersection type, there are no choices when passing arguments
  askSomeone2({ name: '김코딩', skill: '웹 개발', age: 20 });
  ```
