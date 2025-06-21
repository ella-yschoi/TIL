# State & Props

## 1. Understanding Through Examples

### State

- Values that can change 'inside' the component during component usage
- ex) age, address, employment status

### Props

- Values received from 'external' sources
- ex) name, gender

<br/>

## 2. Characteristics of Props

### Component Properties

- (Unchanging) properties that the component has in web applications

### Values Received from Parent Component

- React components are JavaScript functions and classes
- Receive props like function arguments → return React elements that describe how to display on screen based on this
- Therefore, can be used as initial values containing data to be output on screen when the component is first rendered

### Object Form

- Can pass any type of value

### Read-Only

- Read-only objects that cannot be changed arbitrarily
- If not read-only, could affect values of parent components that passed props
- Also violates unintended side effects or React's unidirectional/downward data flow principle

<br/>

## 3. How to Use Props

### Define Values and Properties to Pass to Child Components

```jsx
function Parent() {
  return (
    <div className = 'parent'> // <Parent> declaration
        <h1>I am the parent</h1>
        <Child /> // Write <Child> component inside <Parent> component
    </div>
  );
};

function Child() {
  return (
      <div className = 'Child'>
  );
};
```

### Pass Defined Values and Properties Using Props

```jsx
// Assign attributes and values, wrap values to be passed with {}
<Child attribute = {value} />

// Declare text attribute, then assign string value to this attribute and pass to <Child> component
<Child text = {'I am the eldest child'} />

// Receive string passed from <Parent> component in <Child> component
function Child(props) {
  return (
    <div className = 'Child'></div>
  );
};

```

### Render Received Props

```jsx
function Child(props) {
  // {key : value} of props object takes the form of {attribute : value} defined in <Parent> component
  return (
    <div className='child'>
      // Like JavaScript, props values can also be accessed with Dot notation
      <p>{props.text}</p>
    </div>
  );
}
```

### Props Children

There's also a method to pass values by putting them between opening and closing tags

```jsx
function Parent() {
  return (
    <div className='parent'>
      <h1>I am the parent</h1>
      <Child>I am the eldest child</Child>
    </div>
  );
}
function Child(props) {
  return (
    <div className='child'>
      <p>{props.children}</p>
    </div>
  );
}
```

<br/>

## 4. State Hook, useState

### How to Use useState and How It Works

```jsx
// Import useState from React
import { useState } from 'react';
// Call useState inside component: state variables don't disappear even after function ends, managed by React
function CheckboxExample() {
  // Declare new state variable
  const [isChecked, setIsChecked] = useState(false);
}
```

### useState Pseudocode

```jsx
// When useState is called, it returns an array
// 0th element of array is current state variable, 1st element is function to update this variable
// Value passed as argument to useState is initial value of state

const [state storage variable, state update function] = useState(state initial value);
```

### useState Syntax Example

```jsx
function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);
}

// isChecked: variable that stores state
// setIsChecked: function that changes state isChecked
// useState: state hook
// false: state initial value
```

### JSX Ternary Operator Usage Example

```jsx
<span>{isChecked ? 'Checked!!' : 'Unchecked'} </span>
```

<br/>

## 5. Updating State

- To update, call setIsChecked which is a function that can update state variables
- When user changes checkbox value, onchange event calls event handler function handleChecked, and this function calls setIsChecked
- When setIsChecked is called, isChecked variable is updated according to result
- React passes new isChecked variable to CheckboxExample component, re-rendering that component

```jsx
function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);

  const handleChecked = (event) => {
    setIsChecked(event.target.checked);
  };

  return (
    <div className='App'>
      <input type='checkbox' checked={isChecked} onChange={handleChecked} />
      <span>{isChecked ? 'Checked!!' : 'Unchecked'}</span>
    </div>
  );
}
```

<br/>

## 6. Points to Note

- React components are newly called and re-rendered when state changes
- React state must be changed by calling state update functions, cannot be forcibly changed

<br/>

## 7. Event Handling

- In React, events use camelCase
- Use JSX to pass event handling functions (event handlers) as functions, not strings

```jsx
<button onClick={handleEvent}>Event</button>
```

### onChange

```jsx
function NameForm() {
  const [name, setName] = useState('');

  const handleChange = (e) => {
    setName(e.target.value);
  };

  return (
    // When onChange event occurs, can read input value contained in event object through e.target.value
    // onChange is an event that occurs every time input text changes
    // When event occurs, handleChange function works and updates to new state through setState with input value contained in event object
    <div>
      <input type='text' value={name} onChange={handleChange}></input>
      <h1>{name}</h1>
    </div>
  );
}
```

### onClick

Event used when application should react according to user actions like button clicks or link navigation through `<a>` tags

```jsx
function NameForm() {
  const [name, setName] = useState();

  const handleChange = (e) => {
    setName(e.target.value);
  };

  return (
    // When button is clicked, alert popup shows name entered in input tag
    <div>
      <input type='text' value={name} onChange={handleChange}></input>
      <button onClick={alert(name)}>Button</button>
      <h1>{name}</h1>
    </div>
  );
}
```
