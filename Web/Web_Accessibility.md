## **Web Accessibility**

### What is Web Accessibility?

- With web accessibility, you can be guaranteed to always receive information at an equal level regardless of the situation when accessing the web

<br/>

## **2. Web Content Accessibility Guidelines (WCAG)**

### ✅ **Perceivable** : All content must be perceivable by users

- Appropriate alternative text
  - Provide alternative text with `alt` attribute
  - For cases like background images where information recognition is not needed, give empty string as `alt` value so screen readers don't recognize it
- Caption provision
  - Include captions or use `track` element inside video element to load caption files
- Content recognition independent of color
  - Content must be recognized regardless of color, so set borders on content or add labels to make content understandable
- Clear instruction provision
  - Write alternative text for instructions or provide visual feedback together
- Text content luminance contrast
  - If luminance contrast is not sufficiently secured, text reading becomes difficult
  - Luminance contrast between text content and background must be 4.5:1 or higher
- Prohibit auto-play
  - When using screen readers, it's difficult to understand page content due to overlapping auto-played sounds
- Content distinction
  - Adjacent content must be distinguishable, so distinguish with borders, dividing lines, luminance contrast, spacing, etc.

### ✅ **Operable** : User interface components must be operable and navigable

- Keyboard usage guarantee
  - All functions must be usable with keyboard only
- Focus movement
  - Focus by keyboard must move logically and be visually distinguishable
- Operable
  - User input and controls must be provided to be operable
  - Must be able to select and operate desired elements even in situations where fine manipulation is difficult
- Response time adjustment
  - Content with time limits must allow response time adjustment or inform end time
- Pause time provision
  - Content that changes automatically must be controllable
- Limit blinking and flashing usage
  - Can cause eye fatigue or photosensitive seizures, so certain conditions must be met even if used
- Skip repeated areas
  - Provide methods to skip to main content even if provided
- Title provision
  - Help quick access to content by providing appropriate titles
- Appropriate link text
  - Link text must be provided to understand purpose or goal

### ✅ **Understandable** : Content must be understandable

- Basic language indication
  - Specify the primary language used ex) `<html lang = "ko">`
- Execution according to user requirements
  - Functions not intended by users (new windows, context changes by focus, etc.) should not be executed
- Content linear structure
  - Content must be provided in logical order
- Table composition
  - Tables must be composed to be easily understood
- Label provision
  - User input must have corresponding labels
  - Setting only `value` or `placeholder` attributes on `<input>` elements is not appropriate
  - Set `id` on `<input>` element and connect with `for` attribute of `<label>` element
- Error correction
  - Must provide methods to correct input errors

### ✅ **Robust** : Web content must be made robust to be accessible with future technologies

- Prevent markup errors
  - Markup language elements must have no errors in opening/closing, nesting relationships, and attribute declarations
- Web application accessibility compliance
  - Web applications included in content must be accessible, and if not, alternative means must be provided

<br/>

## **3. WAI-ARIA**

### 1. WAI-ARIA

- WAI (Web Accessibility Initiative)
  - Organization responsible for web accessibility at W3C that sets web standards
- ARIA (Accessible Rich Internet Applications)
  - Technology to enable people with disabilities to more easily access web content and web applications, i.e., technology for web accessibility

### 2. Need for WAI-ARIA

- Can enhance web accessibility by allowing additional meaning to be given to HTML elements

### 3. How to Use WAI-ARIA

1. Role

- Attribute used to specify what role an element plays when HTML element type and role don't match
  ```html
  <div role="button">Element that uses div as button</div>
  ```
  ```html
  <!-- Wrong usage example of WAI-ARIA: explaining again with WAI-ARIA -->
  <button role="button">button element</button>
  <h1 role="button">h1 element</h1>
  ```

2. State

- `aria-selected`: Attribute that can indicate selected elements among multiple selectable elements

  ```html
  <ul role="tabList">
    <!-- First tab is selected -->
    <li role="tab" aria-selected="true">Tab1</li>
    <li role="tab" aria-selected="false">Tab2</li>
    <li role="tab" aria-selected="false">Tab3</li>
  </ul>

  <div role="tabpanel">Tab menu ONE</div>
  <div role="tabpanel">Tab menu TWO</div>
  <div role="tabpanel">Tab menu THREE</div>
  ```

3. Property

- `aria-label`: Attaches a label to an element

  ```html
    <!-- 1. It's hard to know what role the button plays with just HTML element structure -->
    <button> <img src="X.png" /> </button>
    <button> <img src="magnifying_glass.png" /> </button>

    <!-- 2. Using aria-label -->
    <button aria-label="Close"/> <img src="X.png" /> </button>
    <button aria-label="Search"/> <img src="magnifying_glass.png" /> </button>
  ```

- `aria-live`: Indicates whether the element is an area that changes content in real-time (alert, modal, etc.)
  - Property values include `polite`, `assertive`, `off(default)`
