# TypeScript Type

## 1. Boolean Type

- Boolean values called true and false, same as JavaScript

  ```typescript
  let isShow: boolean = true;
  let isDone: boolean = false;
  ```

<br/>

## 2. Number Type

- Like JavaScript, TypeScript also uses one Number type to represent integers and decimals without distinction
- TypeScript additionally supports bigint

  ```typescript
  let number1: number = 5;
  let number2: number = 0.7;
  ```

<br/>

## 3. String Type

- Like JavaScript, uses double quotes or single quotes to represent string data
- Also, using template literals with backticks allows writing strings across multiple lines

  ```typescript
  let firstName: string = 'coding';
  let lastName: string = 'kim';
  let longString: string = `Ella is a developer.
  He is 20 years old.`;
  ```

<br/>

## 4. Array Type

- Like JavaScript, can handle values as arrays, and can declare and use array types in two ways
- First method: Write `[]` representing array after the type representing array elements

  ```typescript
  let items: string[] = ['apple', 'banana', 'grape'];
  ```

- Second method: Generic array type, write Array first, then write type representing array elements inside `<>`
- Array type basically writes only one type, mixing types is not allowed

  ```typescript
  let numberList: Array<number> = [4, 6, 10];
  ```

<br/>

## 5. Tuple Type

- Using tuple type in TypeScript allows expressing arrays with fixed element types and count
- Since each array index has a defined type, need to access exact index

  ```typescript
  let user: [string, number, boolean] = ['Ella', 20, true];
  ```

<br/>

## 6. Object Type

- In TypeScript, objects represent non-primitive types like JavaScript
- In JavaScript, Object type refers to JavaScript values with properties, and means all types that return "object" when using typeof operator

  ```typescript
  let obj: object = {};
  ```

- In TypeScript, object type is a type that accepts all objects, and since object property types are specified as any, any property can be added
- However, **it's much better to explicitly specify each object property type**
- Objects can specify specific types for key-value pairs in the way below

  ```typescript
  let user: { name: string; age: number } = {
    name: 'Ella',
    age: 20,
  };
  ```

<br/>

## 7. Any Type

- Can use any type when you need to express unknown types and don't want to do type checking

  ```typescript
  let maybe: any = 4;
  ```

- When using any type, unlike variables with explicit types, **can reassign values without being constrained by type**

  ```typescript
  let obj: object = {};

  // error occurs
  obj = 'hello';

  let maybe: any = 4;

  // works normally
  maybe = true;
  ```

- Also, since strict type checking is not performed, no error occurs even when accessing methods and properties that the actually assigned value doesn't have
- Instead, since it's a method and property that the actually assigned value doesn't have, the returned value is undefined

  ```typescript
  let maybe: any = 4;

  console.log(maybe.length); // undefined
  ```

- Also, any type is useful when you know only part of the type, not the whole
- For example, useful when you want to receive arrays mixed with multiple types

  ```typescript
  let list: any[] = [1, true, 'free'];

  // Since handling with any, index 1st element can be reassigned as number type even though it's boolean type
  list[1] = 100;
  ```
