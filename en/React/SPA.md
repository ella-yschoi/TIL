# SPA(Single Page Application)

## 1. What is SPA?

### Traditional Websites

- When users moved to different pages within a website, the browser had to load the 'entire page' as an HTML file every time to show the page

### SPA

- SPA doesn't reload overlapping parts before and after page transitions, but only reloads parts that need updates
- Refers to web applications or websites that work by manipulating data needed for updates with JavaScript and generating HTML elements to display on screen

### Benefits of SPA

- Only needs to receive data for necessary parts and update the screen, so it responds quickly to user interactions
- Server only needs to pass requested data, reducing server overload problems
- Provides better user experience since there's no need to render the entire page

### Disadvantages of SPA

- JavaScript file size is large, so first screen loading time becomes longer due to waiting time for this file
- Not good for SEO. Search engines operate search functions by analyzing data in HTML files, but SPA has no special data in HTML, so search engines don't work properly

<br/>

## 2. Difference Between Wireframe and Mockup

### Wireframe

- Skeleton for web page layout and UI elements, allowing developers to understand design concepts and site functionality

### Mockup

- A model with minimal functionality for demo presentation and evaluation, designed with smartphone or desktop frames overlaid for intuitive understanding

<br/>

## 3. Router

### Routing

- Process of showing different views according to different addresses, meaning "change according to path"
- In React, 'React Router' library is most commonly used for this routing

### Main Components

- router: `<BrowserRouter>`
- route matchers: `<Routes>`, `<Route>`
- route changers: `<Link>`
