# Redux

## 1. State Management

### Global State Management

- State in frontend development: Data expressed dynamically

### Global State

- If different components use different types of state, it's okay to have different sources
- However, if different components handle the same state, it's better to avoid getting it from different sources

### Data Integrity

- Identical data is always retrieved from the same place → Single source of truth

### Problems State Management Tools Solve

- Provide global state storage
- Solve Props Drilling issues

### Props Drilling

- Phenomenon of passing data through components that are only used to pass props
- To pass state from a parent component to a component that wants to receive it through props

### Problems with Props Drilling

- Code readability becomes poor
- Code maintenance also becomes difficult
- When state changes, components unnecessarily involved in the props passing process also re-render, negatively affecting performance

### Solutions for This

- Keep state related to components as close as possible
- Use state management libraries: Effective in preventing Props Drilling since state can be directly retrieved from globally managed storage

<br/>

## 2. What is Redux

A state management library that separates components and state to enable global state management

### Order of Redux State Management

1. When an event that requires state change occurs, an Action object containing information about the state to be changed is created
2. This Action object is passed as an argument to the Dispatch function
3. The Dispatch function passes the Action object to the Reducer function
4. The Reducer function checks the Action object's value and changes the state of the global state storage Store according to that value
5. When the state changes, React re-renders the screen
6. In other words, in Redux, data flows unidirectionally in the order Action → Dispatch → Reducer → Store

<br/>

## 3. Redux Structure

### Store

Acts as the only storage where state is managed, the space where the Redux app's state is stored

```javascript
// Create store by connecting Reducer with `createStore` method
import { createStore } from 'redux';
const store = createStore(rootReducer);
```

### Reducer

A function that changes state according to the type value of the Action object received from Dispatch

```javascript
const count = 1;

// Requires initial state as argument when creating Reducer
const counterReducer = (state = count, action) => {
  // Switch conditional statement that branches according to Action object's type value
  switch (action.type) {
    // when action === 'INCREASE'
    case 'INCREASE':
      return state + 1;
    // when action === 'DECREASE'
    case 'DECREASE':
      return state - 1;
    // when action === 'SET_NUMBER'
    case 'SET_NUMBER':
      return action.payload;
    // when no case matches, return existing state as is
    default:
      return state;
  }
};
// The value returned by Reducer becomes the new state
// At this time, Reducer must be a pure function.
```

### Action

Action is an object that defines what action to take, type must be specified as required, and is written in uppercase and Snake Case. Usually, a function that creates Action objects is made and used, which is called an Action Creator.

```javascript
// When payload is not needed
const increase = () => {
  return {
    type: 'INCREASE',
  };
};

// When payload is needed
const setNumber = (num) => {
  return {
    type: 'SET_NUMBER',
    payload: num,
  };
};
```

### Dispatch

A function that passes Action to Reducer

```javascript
// When writing Action object directly
dispatch({ type: 'INCREASE' });
dispatch({ type: 'SET_NUMBER', payload: 5 });

// When using Action Creator
dispatch(increase());
dispatch(setNumber(5));
```

<br/>

## 4. Redux Hooks

### useDispatch()

A method that returns the Dispatch function that passes Action objects to Reducer

```javascript
import { useDispatch } from 'react-redux';

const dispatch = useDispatch();
dispatch(increase());
console.log(counter); // 2

dispatch(setNumber(5));
console.log(counter); // 5
```

### useSelector()

A method that connects components and state to access Redux's state

```javascript
// Redux Hooks methods are imported from react-redux, not redux
import { useSelector } from 'react-redux';
const counter = useSelector((state) => state);
console.log(counter); // 1
```

<br/>

## 5. Three Principles of Redux

### Single source of truth

- Identical data must always be retrieved from the same place
- Redux has only one space called Store for storing data

### State is read-only

- State is read-only
- Just like in React where state was only changed with state update functions, Redux state cannot be changed directly
- In other words, state can only be changed when there's an Action object

### Changes are made with pure functions

- Changes are only possible with pure functions
- Must be written only with pure functions to prevent state from being changed to unexpected values
