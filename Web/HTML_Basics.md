# HTML (Hyper Text Markup Language)

## 1. What is HTML?

A markup language for structuring web pages

<br/>

## What is Markup Language?

- Tags were originally separate from text and were used to express proofreading symbols or comments in manuscripts, but their use gradually expanded to play a role in expressing document structure. This systematic method of tagging is called a markup language, and it is generally used only to the extent of describing data, so it is distinguished from programming languages like JavaScript. [Reference: Wikipedia](https://ko.wikipedia.org/wiki/%EB%A7%88%ED%81%AC%EC%97%85_%EC%96%B8%EC%96%B4)
- Tags were originally separate from text and were used to express proofreading symbols and comments in manuscripts, but their use gradually expanded to play a role in expressing document structure. This systematic method of tagging is called a markup language. It is generally used only to the extent of describing data, so it is distinguished from programming languages like JavaScript.
- Think of it as drawing blueprints to build a house.
- For example, let's say you're creating a login page on a website.
- Then you'll basically need an input form where you can enter ID and password. Also, let's add a button that leads to login and a checkbox asking whether to stay logged in. By writing it in HTML code, you can create a screen like the above.

<br/>

## 2. HTML Basic Structure

```html
<!DOCTYPE html>
Specifies that this document is an HTML document

<html>
HTML start tag that constitutes the overall framework of the document

<head>
Declares metadata of the document

<title>
Title of the document, shown in browser tab

<body>
Place where document content is contained

<div>
Means content division, causes line break

<span>
Content container without line break

<a>
Used when inserting links

<img>
Used when inserting images

<input>
Insert text, radio buttons, check buttons

<button>
Insert button
```

<br/>

## 3. HTML Basic Syntax

### Inserting Images

```html
<html>
  <head></head>
  <body>
    <div>div tag occupies one line</div>
    <div>division 2</div>
    <span>span tag occupies space only as much as content size</span>
    <span>span 2</span>
    <span>span 3</span>
    <div>division 3</div>
    <img
      src="https://obj-kr.the1.wiki/data/322eebacb4eca78026616d703becbd9828ecb9b4ecb9b4ec98a4ed9484eba08ceca68820eab3b5ec8b9dec82aceca784292e706e67.png"
    />
    <a href="http://naver.com" target="_blank">Naver Direct Link</a>
  </body>
</html>
```

### ul, li Lists

- ul: unordered list
- ol: ordered list

```html
<html>
  <head></head>
  <body>
    <ol>
      <li>item 1</li>
      <li>item 2</li>
      <ul>
        <li>item 3</li>
      </ul>
    </ol>
  </body>
</html>
```

### input, textarea

```html
<html>
  <head></head>
  <body>
    <div>ID <input type="text" placeholder="type here" /></div>
    <div>password <input type="password" /></div>
    <div><input type="checkbox" /> Remember ID for next login</div>

    <input type="radio" name="option1" /> Option A
    <input type="radio" name="option1" /> Option B
    <div>
      <textarea></textarea>
    </div>
    <div>
      <button>Login</button>
    </div>
  </body>
</html>
```

<br/>

## 4. Semantic Elements

### Meaning

- semantic: having meaning
- ex. When using `<h1>` element, which is an element used to express top level heading, the browser not only applies large font size but also gives spacing above and below to make it look like a title

### Why Use Them

- Because search engines prefer semantic elements → The meaning contained in semantic elements can determine top exposure in search results
- When multiple developers work together, it's much more convenient to find meaningful code blocks than to search for `<div>` elements, and it's also easier to predict the type of data that will be filled inside elements
- Therefore, when writing HTML elements, you need to consider what element can best describe the data you're going to write

### Mainly Used Elements

```html
<article>
  Specify independent and self-contained content

  <aside>
    Display the main part of the text and explain the remaining parts, used for
    unimportant parts like sidebars or ad windows unless it's something special

    <footer>
      Generally located at the bottom of a page or that part. Used when putting
      site license, address, contact information

      <header>
        Top part of page or section, may contain site title or top bar, search
        box

        <nav>
          Generally elements that guide the site like top bar, usually used in
          list form by putting
          <ul>
            inside

            <main>Display the main content of the document</main>
          </ul>
        </nav>
      </header>
    </footer>
  </aside>
</article>
```

<br/>

## 5. Naming Each Area

### id

When attaching a unique name. Used only once, actually rarely used

```html
<!--HTML-->
<div id="writing-section"></div>
```

```css
/* css */
div#writing-section
```

### class

- When classifying repeated areas by type. Multiple.
- Used when classifying repeatedly used elements by type. Therefore, elements with the same class can be inferred as elements classified as the same type
- If you need a name that should be used only once, you should use id, not class!

```html
<!--HTML-->
<li class="comment"></li>
```

```css
/* css */
li.comment
```
