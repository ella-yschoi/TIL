# **Virtual DOM**

## 1. What is Virtual DOM?

- Virtual DOM, a concept like a **copy** of the actual DOM
- Instead of accessing and manipulating actual DOM objects, React accesses virtual DOM objects and **compares before and after changes to apply only the changed parts**
- In other words, it's a technology that uses virtual DOM trees made of JavaScript objects to **minimize actual DOM manipulation and optimize performance**

<br/>

## 2. Form of Virtual DOM

- Like actual DOM, **virtual DOM is also based on HTML document objects**
- Just abstracted, ordinary JavaScript objects
- Therefore, can freely manipulate as needed without touching the actual DOM
- **Created newly whenever component state or props change** in React
- React compares previous virtual DOM with new virtual DOM and reflects only changed parts to actual DOM

<br/>

## 3. Virtual DOM Operation Process

- During comparison process, React uses **Diffing algorithm** to detect changed parts
- In Diffing algorithm, to detect this, uses methods like **setState instead of direct assignment** to change state
- Compares virtual DOM with changed new virtual DOM and reflects only parts that need changes to actual DOM for update → Reconciliation
- When there are multiple state changes, updates them all at once (Batch Update)
- Through this, optimizes performance and minimizes unnecessary re-rendering

<br/>

## 4. Is Virtual DOM Fast?

- Virtual DOM is generally faster than directly manipulating actual DOM, but not in all cases
- Sometimes directly manipulating DOM can be faster
