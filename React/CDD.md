# Component Driven Development

## 1. What is Component Driven Development?

### What is CDD?

- Can proceed with development by making UI components in parts
- Development method closer to bottom-up development that builds pages by assembling components in component units

### CSS in JS

- Various attempts for CSS structuring
  - Used SASS, a scripting language that extends CSS, as preprocessor, but compiled CSS size became large
- To supplement SASS problems, various CSS methodologies with the following orientations emerged:
  - Code reusability
  - Code simplification (easy maintenance)
  - Code extensibility
  - Code predictability (through class names, etc.)
  - Styled-Component: Provides very simple pattern that can completely separate UI from components with state

<br/>

## 2. CDD Development Tools

### Styled Components

Library that componentizes CSS, usable in React environment, can put CSS inside JavaScript

#### Installing Styled Components

```javascript
// Add code to package.json
{
"resolutions": {
  "styled-components": "^5"
  }
}
```

#### Import to file that will use Styled Components

```javascript
import styled from 'styled-components';
```

#### Making Components

```javascript
// Use backtick (`) instead of quotes
import styled from 'styled-components';

// Make component with Styled Components
const BlueButton = styled.button`
  background-color: blue;
  color: white;
`;

export default function App() {
  // Use like React component
  return <BlueButton>Blue Button</BlueButton>;
}
```

#### Making new component by reusing component

```javascript
import styled from 'styled-components';

const BlueButton = styled.button`
  background-color: blue;
  color: white;
`;

// Make component by reusing made component
const BigBlueButton = styled(BlueButton)`
  padding: 10px;
  margin-top: 10px;
`;

// Reuse reused component
const BigRedButton = styled(BigBlueButton)`
  background-color: red;
`;

export default function App() {
  return (
    <>
      <BlueButton>Blue Button</BlueButton>
      <br />
      <BigBlueButton>Big Blue Button</BigBlueButton>
      <br />
      <BigRedButton>Big Red Button</BigRedButton>
    </>
  );
}
```

#### Using Props

```javascript
import styled from 'styled-components';
import GlobalStyle from './GlobalStyle';

// Can do conditional rendering according to received prop
// Use ternary operator to check if <Button> component has skyblue props
// If exists, specify skyblue as background color, if not, specify white
const Button1 = styled.button`
  background: ${(props) => (props.skyblue ? 'skyblue' : 'white')};
`;

export default function App() {
  return (
    <>
      <GlobalStyle />
      <Button1>Button1</Button1>
      <Button1 skyblue>Button1</Button1>
    </>
  );
}
```

#### Rendering with Props value

```javascript
import styled from 'styled-components';
import GlobalStyle from './GlobalStyle';

// Use received prop value as-is for rendering
const Button1 = styled.button`
  background: ${(props) => (props.color ? props.color : 'white')};
`;

// Can also use in format like below
const Button2 = styled.button`
  background: ${(props) => props.color || 'white'};
`;

export default function App() {
  return (
    <>
      <GlobalStyle />
      <Button1>Button1</Button1>
      <Button1 color='orange'>Button1</Button1>
      <Button1 color='tomato'>Button1</Button1>
      <br />
      <Button2>Button2</Button2>
      <Button2 color='pink'>Button2</Button2>
      <Button2 color='turquoise'>Button2</Button2>
    </>
  );
}
```

<br/>

## 3. useRef

### useRef that can utilize DOM reference well

React can reference address values to DOM nodes, elements, React elements with `useRef` in exceptional situations

```javascript
const container_for_address_value = useRef(reference_data_type);
// Now container_for_address_value variable can hold any address value
return (
  <div>
    <input ref={container_for_address_value} type='text' />
    {/* When assigning container_for_address_value as value to ref property available in React*/}
    {/* container_for_address_value variable holds address of input DOM element */}
    {/* Can utilize input DOM element in other components later */}
  </div>
);
```

Can use `useRef` in limited situations below, but goes against React's characteristic and advantage of declarative programming principle, so except for those situations, overuse of `useRef` is inappropriate

```javascript
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick = {onButtonClick}>Focus the input</button>
    </>;
  )
}
```
