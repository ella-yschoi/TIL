# Web Standard

## 1. Concept of Web Standards

### Internet

The Internet is a more comprehensive concept than the web. It's a globally connected computer network communication system that includes not only the web but also **various services using networks** such as online games, mobile apps, email, etc.

### Web

A space where various information such as documents, images, and videos can be shared with many people

### Web Standards

- 'Technologies or rules used as standards on the web' recommended by W3C
- Web page creation techniques that allow web pages to look and function identically regardless of what operating system or browser the user uses

### Benefits of Web Standards

- Ease of maintenance
- Web compatibility assurance
- Increased search efficiency
- Enhanced web accessibility

<br/>

## 2. Semantic HTML

### Semantic Elements

- Elements that have clear meaning about what content they will contain and what function they will perform
- HTML composed using semantic elements appropriately → Semantic HTML

### Need for Semantic HTML

- Communication between developers
- Search efficiency
- Web accessibility

### Commonly Used Semantic Elements

- `<header>`: Element that serves as a header located at the top of a page or element
- `<nav>`: Element used for menus and table of contents
- `<aside>`: Element that contains content related to the document but not directly related
- `<main>`: Main content that is the core of the document
- `<article>`: Parts that can be distinguished independently and reused such as posts and articles. A means to distinguish each `<article>` is needed, usually using a method that includes a title `<hgroup>`
- `<section>`: Represents an independent section of a document, used when there's no suitable semantic element. Often includes a title `<hgroup>`
- `<hgroup>`: Element used to display titles
- `<footer>`: Located at the bottom of a page or element

<br/>

## 3. Commonly Mistaken Markup

1. Putting block elements inside inline elements
   - Inline elements: Only occupy as much space as the content (ex. `<span>`, `<label>`)
   - Block elements: Occupy screen area widely horizontally (ex. `<div>`, `<h1>`)
2. Using `<b>`, `<i>` elements
   - `<b>` → `<strong>`
   - `<i>` → `<em>`
3. Using `<hgroup>` randomly
   - X for the purpose of applying styles while overlooking the role as a semantic element and the purpose of indicating content hierarchy
   - In other words, `<h1>` must be above `<h2>` and `<h3>`, and the opposite is X
4. Using `<br/>` consecutively
   - When wanting to give spacing between elements, use `<p>` element to separate into completely different paragraphs or set spacing with CSS properties
5. Using inline styling
   - To follow web standards, write HTML and CSS code separately

<br/>

## 4. Cross Browsing

### What is Cross Browsing?

- Work to provide **equal** screen and functionality regardless of the type of browser accessing the website
- Since each browser has a different rendering engine, it's X to make the screen look exactly the same in all browsers

### Cross Browsing Workflow

1. Initial planning: What content and functions, design, who is the target customer base
2. Development: Understand compatibility of code in each browser when writing code, then use
3. Test/Discovery: Can use cross-browsing test tools like TestComplete, LambdaTest, BitBar, etc.
4. Fix/Repeat
