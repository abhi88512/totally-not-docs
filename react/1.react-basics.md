### React Basics

1. What is react ?
    - React is a JavaScript library for building user interfaces, maintained by Meta (formerly Facebook).
    - It allows developers to create reusable UI components.
    - React is known for its efficiency, leveraging a Virtual DOM to optimize rendering performance.

2. Why react is fast ?
    - React is fast because it uses a Virtual DOM to minimize direct DOM manipulations, which are computationally expensive.

3. What React Dom and Virtual Dom ?
    - React DOM is the library that updates the actual DOM to match React elements.
    - Virtual DOM is a lightweight copy of the real DOM used for efficient updates.

4. What is the diffing algorithm in React, and how does it optimize updates?
    - The diffing algorithm is a technique used by React to efficiently update the DOM by comparing the Virtual DOM with the previous version.
    - It identifies the minimal set of changes required and applies them to the real DOM, improving performance.

5. What is a React component?
    - A component is a reusable, self-contained unit (function or class) that returns JSX to describe part of the UI.
    - The name of component always starts with a capital letter.

6. Give an example of virtual dom?
    - Virtual DOM is a JavaScript representation of the real DOM. For example: `{type: 'div', props: {className: 'container'}, children: ['Hello World']}` represents `<div class="container">Hello World</div>`.

7. What is react class component and functional component?
    - Class component: A React component defined using ES6 class syntax that extends React.Component, has access to lifecycle methods and state.
    - Functional component: A React component defined as a JavaScript function that returns JSX, simpler and uses hooks for state and lifecycle.

8. React class component vs functional component?
    - Class components: Use lifecycle methods, have `this.state` and `this.setState()`, more verbose syntax.
    - Functional components: Use hooks (useState, useEffect), simpler syntax, better performance, preferred in modern React development.

### JSX

9. What is jsx?
    - JSX (JavaScript XML) is a syntax extension for JavaScript that allows writing HTML-like code in React components.

10. How react understands jsx?
    - React uses Babel to transpile JSX into JavaScript function calls (e.g., `React.createElement`).

11. What is a React fragment, and why is it used?
    - A fragment groups multiple elements without adding an extra DOM node; useful to return multiple siblings from a component.

### State Management

12. What is state ? How it makes react reactive ?
    - State is an object that holds dynamic data for a component.
    - Reactivity comes from React re-rendering components when state changes.

13. What is state vs common variable or const ?
    - State is managed by React and triggers re-renders when updated.
    - Regular variables/constants do not trigger re-renders.

14. What is the difference between state and props?
    - State is local to a component and mutable via setState/useState; props are read-only values passed from parent to child.

15. How do you define and use state in a React functional component?
    - Use the `useState` hook: `const [value, setValue] = useState(initial)`, update with `setValue(newValue)` and use `value` in JSX.

16. How do you define and use state in a React class component?
    - Initialize state in the constructor (`this.state = {}`) and update with `this.setState({})`; access via `this.state`.

17. How do you pass props to a functional component?
    - Pass values as attributes: `<MyComp foo={bar} />`; receive them as the first function argument `function MyComp(props) {}` or via destructuring `({foo})`.

18. How do you use props in a class component?
    - Access via `this.props.propName` inside lifecycle methods or `render()`; props are provided by the parent component.

19. What is prop drilling?
    - Prop drilling is passing props through several intermediate components until they reach the component that needs them; it can be reduced with context or state managers.

20. Is setstate sychronus or asynchronus ? describe the reason ?
    - setState is asynchronous for performance optimization.
    - React batches multiple setState calls to avoid unnecessary re-renders.
    - Use callback functions or useEffect to handle state updates that depend on previous values.

21. What are propTypes ?
    - PropTypes is a library for runtime type checking of React props during development.
    - It helps catch bugs by validating the types of props passed to components.
    - Example: `MyComponent.propTypes = { name: PropTypes.string.isRequired }`

### Tools and Ecosystem

22. What is package bundler ?
    - A package bundler combines multiple JavaScript files into one or more bundles for efficient loading in a browser.

23. Create react app vs Vit ?
    - Create React App (CRA) is a boilerplate for React projects with built-in configurations.
    - Vite is a faster build tool optimized for modern JavaScript frameworks, including React.

24. What is babel , how it is used in react ?
    - Babel is a JavaScript compiler that converts modern JavaScript (ES6+) and JSX into browser-compatible JavaScript.

25. What is web pack or varcell ?
    - Webpack is a module bundler for JavaScript applications.
    - Vercel is a platform for deploying modern web applications.

26. What are PropTypes?
    - PropTypes is a runtime prop-type checking utility for React that warns in development if prop types mismatch.

27. In how many ways can we export/import things from a JS Module?
    - Two main ways: default export/import (`export default ...` / `import Foo from './foo'`) and named export/import (`export const Foo` / `import { Foo } from './foo'`).

### Rendering

28. React renders everything under the root element
    - Correct. React applications are rendered within a single root DOM element, typically `<div id="root">`.

29. Reconciliation vs Rendering?
    - Reconciliation computes the diff between old and new virtual DOM trees; rendering is the actual update of the real DOM based on that diff.

30. React is declarative in nature not imparative ? what does it mean  to declarative or impartaive ? how react is decalartive ?
    - Declarative programming describes "what" you want to achieve, while imperative describes "how" to achieve it.
    - React is declarative because you describe the desired UI state using JSX, and React handles the DOM updates.
    - Instead of manually manipulating DOM elements (imperative), you define components that render based on state (declarative).

31. How does the rendering process work from JSX -> React Elemnt -> Virtual Dom -> Actual Dom ?
    - JSX is transpiled to React.createElement() calls by Babel.
    - React.createElement() returns React elements (plain JavaScript objects describing the UI).
    - React elements form the Virtual DOM tree structure.
    - React's reconciliation algorithm compares Virtual DOM trees and updates the actual DOM with minimal changes.

32. What is Diffing Algorithim ? How it works (compares old Virtual DOM with new Virtual DOM) ?
    - The diffing algorithm compares the current Virtual DOM tree with the previous Virtual DOM tree to identify changes.
    - It uses heuristics: assumes elements of different types produce different trees, uses keys to identify moved elements.
    - The algorithm efficiently calculates the minimal set of operations needed to transform the old tree into the new tree.

33. Why can not we directly update the DOM , why use virtual dom and diffing algorithm ?
    - Direct DOM manipulation is expensive and can cause performance issues with frequent updates.
    - Virtual DOM allows React to batch updates and apply minimal changes to the real DOM.
    - The diffing algorithm ensures only necessary DOM operations are performed, improving performance significantly.

### Importing and Exporting

34. What is default export and how it is imported?
    - Default export allows exporting a single value as the default export from a module.
    - Export: `export default Component` or `const Component = () => {}; export default Component`
    - Import: `import Component from './Component'` (can use any name when importing)

35. What is named export and how it is imported?
    - Named export allows exporting multiple values from a module with specific names.
    - Export: `export const Component = () => {}` or `export { Component, AnotherComponent }`
    - Import: `import { Component } from './Component'` (must use exact name or alias with `as`)

36. default vs named export ?
    - Default export: One per module, can rename during import, used for main module functionality.
    - Named export: Multiple per module, must use exact names (or aliases), used for utility functions and secondary exports.
    - A module can have both default and named exports simultaneously.


### Small precise points

1. In-browser Babel (type="text/babel") transforms JSX at runtime for quick demos.
2. Browsers don't provide Node's `require()` function. Keeping `import`/`export` with the in-browser transformer may produce `require()` calls.
3. `require is not defined` is a runtime symptom of CommonJS code running in the browser.
4. Quick fix: remove `import`/`export` and use globals for tiny examples. Expose components as `window.ComponentName` to share across scripts.
5. Ensure load order: define providers before consumers (counter.js before script.js). `type="module"` enables native imports but browsers don't transform JSX—precompile first.
6. Bundlers perform optimizations: tree-shaking, minification, and asset fingerprinting.
7. In-browser Babel is slower and not suitable for production use.

Example (before / after):

Before (problematic for in-browser Babel):

```javascript
// counter.js
export const Counter = () => <div>Counter</div>;

// script.js
import { Counter } from './counter.js';
ReactDOM.createRoot(document.getElementById('root')).render(<Counter />);
```

After (works with type="text/babel"):

```javascript
// counter.js
const Counter = () => <div>Counter</div>;
window.Counter = Counter;

// script.js
ReactDOM.createRoot(document.getElementById('root')).render(<Counter />);
```


