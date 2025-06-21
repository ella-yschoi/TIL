# Object

## 1. What is an Object?

- Objects in JavaScript can be compared to game characters. User characters have the same job and abilities, but each has different detailed content.
- Someone has an ID of Ella and a job as a wizard, while someone else has an ID of Chloe and a job as a warrior.
- Similarly, when users register on a website, the items they need to enter are all the same, but the information they enter is different for each user. In cases like this where each can have different values but the types of data that need to be entered are the same, using objects makes it easy to manage data.
- In such cases where there are common properties, you should use objects. Let's assume you're creating an address book of members who registered on a website.

  ```jsx
  // Do you need to declare multiple variables like this every time?
  let userFirstName = 'Ella';
  let userLastName = 'Choi';
  let userEmail = 'ella@gmail.com';
  let userCity = 'Seoul';

  let userFirstName = 'Chloe';
  let userLastName = 'Kim';
  let userEmail = 'chloe@gmail.com';
  let userCity = 'Seoul';
  ```

  ```jsx
  let user = {
    // create object with curly braces
    firstName: 'Ella', // separate pairs of names and values with ',', separate names and values with ':'
    lastName: 'Choi', // here lastName is the key, 'Choi' is the value
    email: 'ella@gmail.com',
    city: 'Seoul',
  };
  ```

<br/>

## 2. Two Ways to Access Object Values

### Dot notation: object + .(dot) + key value

```jsx
let user = {
  firstName: 'Ella',
  lastName: 'Choi',
  email: 'ella@gmail.com',
  city: 'Seoul',
};

// format: object + .(dot) + key value
user.firstName; // 'Ella'
user.city; // 'Seoul'
```

### Bracket notation: key value as 'string' inside square brackets

```jsx
let user = {
  firstName: 'Ella',
  lastName: 'Choi',
  email: 'ella@gmail.com',
  city: 'Seoul',
};

// format: key value goes inside square brackets as a 'string'
user['firstName']; // 'Ella'
user['city']; // 'Seoul'
```

<br/>

## 3. Various Ways to Handle Objects

### Bracket notation: must be used when key values change dynamically

```jsx
let person = {
  name: 'Ella',
  age: 16,
}; // situation where key values keep changing

// get name value
let output = getProperty(person, 'name');
console.log(output); // -> 'Ella'

// method to get name value
function getProperty(obj, propertyName) {
  return obj[propertyName]; // obj['name']
}

// Note1: return person.name (X) only outputs Ella -> must use obj[propertyName]
// Note2: return.propertyName (X) -> need a separate key name called propertyName to use it

// get age value
let output = getProperty(person, 'age');
console.log(output2); // -> 16

// method to get age value
function getProperty(obj, propertyName) {
  return obj[propertyName]; // obj['age']
}
```

### You can also add values using dot/bracket notation

```jsx
let tweet = {
  writer: 'Ella Choi',
  createdAt: '2022-02-28 12:03:33',
  content: 'Coding is fun',
};

// You can add various values
tweet['category'] = 'story'; // Add string 'story' using Bracket notation
tweet.isPublic = true; // Add Boolean value using Dot notation
tweet.tags = ['#coding', '#developer']; // Add array using Dot notation
```

### You can also delete properties using the delete keyword

```jsx
let tweet = {
  writer: 'Ella Choi',
  createdAt: '2022-02-28 12:03:33',
  content: 'Coding is fun',
};

delete tweet.createdAt; // delete the createAt key-value pair
tweet.createdAt; // since it's deleted, it will output undefined in console

// tweet becomes like this
// {writer: 'Ella Choi', content: 'Coding is fun'}
```

### You can check if a key exists using the in operator

```jsx
let tweet = {
  writer: 'Stevelee',
  createdAt: '2022-02-28 12:03:33',
  content: 'Coding is fun',
};

'content' in tweet; // true
'updatedAt' in tweet; // false
```

<br/>

## 4. Common Mistakes When Writing Strings

To prevent minor mistakes like forgetting square brackets when using bracket notation, or not declaring variables, etc., let's understand and familiarize ourselves with the content below one by one!

```jsx
let user = {
  firstName: 'Ella',
  lastName: 'Choi',
  email: 'ella@gmail.com',
  city: 'Seoul',
};
user['firstName']; // 'Ella': access object value using Bracket notation
user[firstName]; // ReferenceError: firstName is not defined: firstName is being treated as a variable

let keyname = 'firstName'; // store 'firstName' string in keyname
user[keyname]; // 'Ella': because the string value 'firstName' went into keyname
user[keyname] === user['firstName']; // true: essentially the same as accessing object value using Bracket notation

let firstName = 'Ella';
user[firstName] === user['firstName']; // false: when using Bracket notation, a string must go inside the square brackets
user[keyname] === user['firstName']; // true

user['firstName'] === user.firstName; // true: Dot notation === Bracket notation
user[firstName] === user.firstName; // false: when using Bracket notation, a string must go inside the square brackets
user[firstName] === user['firstName']; // false
```
