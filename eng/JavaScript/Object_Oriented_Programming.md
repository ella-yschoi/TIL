# Object-Oriented Programming

## 1. What is Object-Oriented Programming

- Object-oriented programming bundles data together for processing, unlike procedural programming
- Properties and methods are included in one concept called 'object', which is different from JavaScript's built-in object type and is called a class
- Object-oriented programming creates a blueprint that serves as a model → class
- The prototype (original form) used when creating the model's blueprint → prototype
- A programming pattern that creates objects (instances) based on that blueprint

<br/>

## 2. Class Module Pattern

### Method Call

```javascript
let counter1 = {
  value: 0;
  increase: function() {
    this.value++ // When calling a method, this refers to counter1
  },
  decrease: function() {
    this.value--
  },
  getValue: function() {
    return this.value
  }
}

counter1.increase()
counter1.decrease()
counter1.increase()
counter1.decrease()
counter1.getValue() // 2
```

### Creating New Objects Each Time Using Closure

```javascript
function makeCounter() {
  let value = 0;
  return {
    increase: function () {
      value++;
    },
    decrease: function () {
      value--;
    },
    getValue: function () {
      return value;
    },
  };
}

let counter1 = makeCounter();
counter1.increase();
counter1.getValue(); // 1

let counter2 = makeCounter();
counter2.decrease();
counter2.decrease();
counter2.getValue(); // -2
```

<br/>

## 3. Class and Instance

### Syntax for Creating Classes: class keyword

```javascript
class Car {
  constructor(brand, name, color) {
    // Code that runs when an instance is created (= initialized): constructor
    // Note that constructor functions don't create return values
  }
}
```

### Creating Class Instances

```javascript
let avante = new Car('hyundai', 'avante', 'black');
// Use new keyword when creating instances
// Each instance has unique properties and methods of the Car class
```

### this: Instance Object

- Brand, name, color, etc. passed as parameters are values specified when creating instances
- Assigning to this means 'giving' the created instance that brand, name, and color
- A unique execution context created for each scope when a function runs
- When creating an instance with the new keyword, that instance becomes the this value

### Method Definition

Define together with constructor function inside the class keyword

```javascript
class Car {
  constructor(brand, name, color) {
    /* omitted */
  }
  refuel() {}
  drive() {}
}
```

Usage in instances: How to use the properties and methods set above in instances

```javascript
let avante = new Car('hyundai', 'avnante', 'black');
avante.color; // 'black'
avante.drive(); // Avante starts driving

let mini = new Car('bmw', 'mini', 'white');
mini.brand; // 'bmw'
mini.refuel(); // Refueling the mini
```

### Summary

```javascript
// constructor function
function Car(brand, name, color) {
  // Car is the class
  this.brand = brand; // here avante === this
  this.name = name;
  this.color = color;
}

// Car.prototype object: can define properties or methods here
Car.prototype.drive = function () {
  console.log(this.name + ' starts driving');
};

let avante = new Car('hyundai', 'avante', 'black'); // avante: instance
avante.color; // 'black'
avante.drive(); // 'avante starts driving'
```

<br/>

## 4. Object-Oriented Programming

### Procedural Language > Object-Oriented Language

- Procedural language: Combination of sequential commands
- Object-oriented language: Code is written using class as a blueprint for data models, with data and functionality bundled together for processing
- JavaScript is not an object-oriented language, but can be written in object-oriented patterns

### Four Basic Concepts of OOP

#### (1) Encapsulation

- Bundling data and functionality into one unit
- Hiding: Hide implementation, expose behavior
- Favorable for Loose Coupling: Instead of writing code procedurally according to execution order, bundle code to resemble the actual appearance it represents, enabling implementation modifications anytime
- Makes code less complex and increases reusability

#### (2) Inheritance

- Child, or derived class, inherits characteristics from parent, or base class
- Makes code simple and increases reusability

#### (3) Abstraction

- Internal implementation is complex but the actually exposed part is made simple to prevent unexpected usage changes
- Encapsulation focuses on hiding data, while abstraction focuses on not exposing unnecessary methods to people using the class and defining them with simple names
- Makes code less complex and minimizes impact on changes

#### (4) Polymorphism

- ex) Methods with the same name are applied slightly differently to each element
- Instead of conditional statements like if/else for the same method, can write differently according to each object's characteristics

<br/>

## 5. Prototype

### Prototype and Class

JavaScript is a prototype-based language, and prototype means original object

```javascript
class Human {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  sleep() {
    console.log(`${this.name} fell asleep`);
  }
}

let kimcoding = new Human('Kim Coding', 30);

Human.prototype.constructor === Human; // true
Human.prototype === kimcoding.__proto__; // true
Human.prototype.sleep === kimcoding.sleep; // true
```

### Prototype Chain

When implementing inheritance, one of the characteristics of object-oriented programming, use prototype chain
