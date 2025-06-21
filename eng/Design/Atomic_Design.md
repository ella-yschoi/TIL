# Atomic Design

## 1. Background of Atomic Design

- Providing consistent user experience becomes more important as web environments are provided across various devices
- As project scale grows, the importance of managing design elements and maintaining UI consistency emerges
- A frontend development methodology emerged by web designer Brad Frost, aiming to build a consistent design system by breaking down UI into the smallest units like atoms (the smallest unit of matter), combining them, and gradually expanding them

<br/>

## 2. Components of Atomic Design

### Atoms

- Refers to the most basic design elements that cannot be broken down further
- Examples include inputs, labels, icons, buttons, etc.

### Molecules

- Collections of UI where atoms come together to work as a single unit
- Molecules are intermediate stages where atoms combine to form more complex structures
- Just as the purpose (input value) of a molecule changes according to its title, molecules can be reused according to their function

### Organisms

- Unlike molecules composed of atoms, organisms are slightly more complex UI components that can be composed of atoms, molecules, and even other organisms
- Generally specific sections of pages, e.g., headers and sidebars

### Templates

- Elements that constitute page-level layouts
- If you've created elements to go into pages using atoms, molecules, and organisms, templates define the arrangement of these elements and the overall structure of the page to provide a consistent user experience
- In other words, you can define how elements are arranged and interact

### Pages

- In atomic design, separation of data and design is important, so pages are distinguished from templates as elements where data and design are combined, with templates being simple collections of UI elements without data
- Therefore, pages contain the completed UI appearance as elements where actual content is filled into copied templates
- Thus, pages in atomic design can be seen as the most concrete stage and allow confirmation of the final result shown to users

<br/>

## 3. Advantages of Atomic Design

- Modularity and reusability
- Convenience of maintenance
- Scalability
