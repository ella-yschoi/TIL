# JSX

## 1. What is JSX?

- **JavaScript syntax extension** used to compose UI in React, and can be used to create **React elements**
- 'Babel' compiles JSX into JavaScript that browsers can understand -> browsers can read JavaScript and render it on screen
- In React, unlike DOM, web application development is possible with only CSS and JSX syntax. In other words, markup-style code can be written with only JavaScript and placed in the DOM (however, since JSX is not HTML, compilation with Babel is needed)

<br/>

## 2. JSX Syntax

- All elements are included inside one element. Must be wrapped with opening and closing tags at the top level

  ```jsx
  <div>
    <div>
      <h1>Hello</h1>
    </div>
    <div>
      <h2>World</h2>
    </div>
  </div>
  ```

- When using element classes, use **className**

  ```jsx
  <div className='greeting'>Hello</div>
  ```

- When using JavaScript expressions, use **curly braces**

  ```jsx
  function App() {
    const name = 'Ella Choi';
    return <div>Hello, {name}!</div>;
  }
  ```

- Custom components must **start with uppercase**

  ```jsx
  function Hello() {
    return <div>Hello!</div>;
  }

  function HelloWorld() {
    return <Hello />;
  }
  ```

- For conditional rendering, use **ternary operators** instead of if statements

  ```jsx
  <div>
    {
      (1+1 === 2) ? (<p>Correct</p>) : <p>Wrong</p>)
    }
  </div>
  ```

- When displaying multiple HTML elements, use the map() function and must include the 'key' JSX attribute

  ```jsx
  const posts = [
    { id: 1, title: 'Hello World', content: 'Welcome to learning React!' },
    { id: 2, title: 'Installation', content: 'You can install React from npm' },
  ];

  function Blog() {
    const content = posts.map((post) => (
      <div key={post.id}>
        <h3>{post.title}</h3>
        <p>{post.content}</p>
      </div>
    ));
    return <div>{content}</div>;
  }
  ```

- Each element in an array is a single JSX expression that can be stored in a variable

  ```jsx
  const Hello - () => {
    return (
      [<div>Hello</div>, <div>Nice to meet you</div>]
    )
  }
  ```
