# **React Diffing Algorithm**

## 1. Need for Diffing Algorithm

- When React compares existing virtual DOM with changed new virtual DOM
- Need to find out **efficient method to update existing UI** to match changed new virtual DOM tree
- In other words, had to find out **the smallest operation method** to transform one tree into another tree
- Previously discovered operation method algorithm had O(n^3) complexity
- This was too expensive operation, so implemented new heuristic algorithm with two assumptions
- These two assumptions fit almost all actual use cases, and React uses comparison algorithm (Diffing Algorithm)
  - Two elements that are different from each other will **build different trees**
  - With key property provided by developers, can find out **which child elements should not change** even through multiple renderings

<br/>

## 2. How React Traverses DOM Tree

- Traverses in level order of tree
- In other words, compares elements at the same level (position)
- This is a type of breadth-first search (BFS)

### 1) When DOM elements are of different types

- DOM tree has the characteristic that each HTML tag has its own rules, so child tags that go under it are limited
- There's also the characteristic that parent tags of child tags are also predetermined, so if parent tag changes, React discards previous tree and builds new tree, and all previous DOM nodes are destroyed

  ```javascript
  <div>
  <Counter />
  </div>

  // If parent tag changes from div to span, child node <Counter/> is completely released
  <span>
  <Counter />
  </span>
  ```

### 2) When DOM elements are of the same type

- If type doesn't change, React tries to minimize changes and avoid rendering as much as possible
- When there's content to update, only modifies properties inside virtual DOM, then attempts actual DOM rendering only once after all node updates are complete

  ```javascript
  <div className="before" title="stuff" />

  // Existing element's tag doesn't change, only className changes
  // React knows that only className is being modified when comparing two elements
  <div className="after" title="stuff" />
  ```

  ```javascript
  // Component with className 'before'
  <div style={{color: 'red', fontWeight: 'bold'}} title="stuff" />

  // Component with className 'after'
  <div style={{color: 'green', fontWeight: 'bold'}} title="stuff" />
  ```

- When comparing two elements, React notices that **exactly only the color style** is changing
- Therefore React only modifies color style, doesn't modify other elements
- After processing one DOM node this way, React **sequentially traverses children under those nodes simultaneously and changes whenever differences are found**
- This is expressed as being processed **recursively**

### 3) Recursive processing of child elements

- When child elements change as below:

  ```javascript
  <ul>
  <li>first</li>
  <li>second</li>
  </ul>

  // Add new child element at the end of child elements
  <ul>
  <li>first</li>
  <li>second</li>
  <li>third</li>
  </ul>
  ```

- When React compares existing `<ul>` with new `<ul>`, it compares child nodes sequentially from top to bottom to find what changed
- Therefore, **confirms matching points of first and second child nodes, then adds third child node**
- Since React compares sequentially from top to bottom this way, inserting elements at the beginning of list can produce much worse performance compared to previous code
- Therefore, when child elements change as below:

  ```javascript
  <ul>
  <li>Duke</li>
  <li>Villanova</li>
  </ul>

  // Add child element at the beginning
  <ul>
  <li>Connecticut</li>
  <li>Duke</li>
  <li>Villanova</li>
  </ul>
  ```

- React cannot operate minimally as we expect. Because it compares first nodes as before
- React recognizes that `<li>Duke</li>` and `<li>Connecticut</li>` child nodes are different from each other and accepts that the entire list has changed
- In other words, it doesn't realize that unchanged child nodes should be maintained, discards everything and renders newly. This is a very inefficient operation method
- Therefore, React supports `key` property to solve this problem

### 4) Key

- If child nodes have keys, React can check matching between children of existing tree and children of new tree using keys

  ```javascript
  <ul>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
  </ul>

  // Add child element with key 2014 at the beginning
  <ul>
  <li key="2014">Connecticut</li>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
  </ul>
  ```

- React knows that child element with key '2014' is newly created, and elements with keys '2015', '2016' just moved positions
- Therefore, React **doesn't change other child elements and only changes added element** as in existing operation method
- For this key property, you can usually assign **unique values** from database (ex. Id)
- Keys don't need to be globally unique, just **unique among sibling elements**

- If there's no unique value, **can also use array index as key**
- However, note that if array is sorted differently, using array index as key can operate inefficiently
- If index stays the same but that element changes, React will accept that the entire array has changed and discard existing DOM tree and build new DOM tree, so it will operate inefficiently
