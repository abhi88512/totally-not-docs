# React Components Guide

## 1. What are Class-Based Components in React?

Class-based components are one way to define components in React, using ES6 classes that extend `React.Component`. They provide a structure for managing state, handling events, and accessing lifecycle methods.

### Key Points:

- **Built with ES6 class syntax:**
  ```javascript
  class MyComponent extends React.Component { ... }
  ```

- Can contain local state and logic via `this.state`
- Include access to lifecycle methods (e.g., `componentDidMount`)
- Historically, were the primary way to write React components before hooks

## 2. How do the constructor and super keywords work in class components?

The `constructor` method runs first in a class component. It is mainly used for initializing state and binding methods.

### Key Points:

- **State Initialization:**
  Set up initial state with `this.state`.
  ```javascript
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }
  ```

- **Method Binding:**
  Bind event handlers to ensure they reference the correct `this`.
  ```javascript
  this.handleClick = this.handleClick.bind(this);
  ```

- **super(props):**
  - Calls parent constructor (`React.Component`)
  - Enables access to `this.props` inside the constructor

## 3. What are Lifecycle Methods in React?

Lifecycle methods are special methods in class components that let you interact with a component's "life"—from creation to removal.

### Key Points:

- Enable running code at different phases (mounting, updating, unmounting)
- Useful for side effects, data fetching, subscriptions, and cleanup
- Only available in class-based components (function components use hooks for similar functionality)

## 4. List and Explain Major Component Lifecycle Methods

React class components progress through several phases. Each phase offers lifecycle methods for handling side effects and other logic.

### Lifecycle Phases and Methods:

#### **Mounting:** Component is added to the DOM
- `constructor()`
- `componentDidMount()`

#### **Updating:** Props/state change, component re-renders
- `shouldComponentUpdate(nextProps, nextState)`
- `componentDidUpdate(prevProps, prevState)`

#### **Unmounting:** Component is removed from the DOM
- `componentWillUnmount()`

#### **Error Handling:** Catches errors in child components
- `componentDidCatch(error, info)`

## 5. What are Function-Based Components and Hooks in React?

Function-based (or functional) components use simple JavaScript functions to return React elements. With hooks, they can now handle state, effects, and more logic.

### Key Points:

- **Simple Syntax:**
  ```javascript
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }
  ```

- **Hooks:** Built-in functions to replicate lifecycle and state features
  - `useState`: Local state management
  - `useEffect`: Side effects (similar to lifecycle methods)
  - Additional hooks: `useContext`, `useReducer`, and custom hooks

- Hooks have made function components the new standard in React development

---

# React Lifecycle Methods Explained

## Mounting: Component is Added to the DOM

### `constructor()`

- **When:** Called first, before mounting.
- **Purpose:**
  - Initialize local state (`this.state`)
  - Bind class methods to the component instance

- **Example:**
  ```javascript
  constructor(props) {
    super(props);
    this.state = { count: 0 };
    this.handleClick = this.handleClick.bind(this);
  }
  ```

- **Notes:**
  - You must call `super(props)` before using `this`

### `componentDidMount()`

- **When:** Immediately after the component has been inserted into the DOM.
- **Purpose:**
  - Perform side effects (data fetching, subscriptions, DOM mutations)

- **Example:**
  ```javascript
  componentDidMount() {
    this.timerID = setInterval(() => this.tick(), 1000);
    fetchData().then(data => this.setState({ data }));
  }
  ```

- **Notes:**
  - Runs once per mount; safe to set state here (will trigger another render)

## Updating: Props/State Change, Component Re-renders

### `shouldComponentUpdate(nextProps, nextState)`

- **When:** Before re-rendering (after state/props changes).
- **Purpose:**
  - Decide if React should proceed with rendering
  - Used for performance optimization to skip unnecessary renders

- **Example:**
  ```javascript
  shouldComponentUpdate(nextProps, nextState) {
    return nextProps.value !== this.props.value;
  }
  ```

- **Notes:**
  - Return `false` to prevent updating
  - Default implementation always returns `true` if not overridden

### `componentDidUpdate(prevProps, prevState)`

- **When:** After the component updates (re-rendered due to props/state).
- **Purpose:**
  - Act on changes (network requests, manually updating DOM)

- **Example:**
  ```javascript
  componentDidUpdate(prevProps) {
    if (prevProps.userId !== this.props.userId) {
      this.fetchNewData();
    }
    if (prevProps.id !== this.props.id) {
      this.loadDetail(this.props.id);
    }
  }
  ```

- **Notes:**
  - Beware of infinite loops if setting state here; always compare previous and new props/state

## Unmounting: Component is Removed from the DOM

### `componentWillUnmount()`

- **When:** Right before React destroys the component.
- **Purpose:**
  - Cleanup (cancel timers, remove subscriptions or event listeners)

- **Example:**
  ```javascript
  componentWillUnmount() {
    clearInterval(this.timerID);
    window.removeEventListener('resize', this.handleResize);
  }
  ```

- **Notes:**
  - Never call `setState` here—it won't have any effect
  - Runs only once, just before unmounting

## Error Handling: Catches Errors in Child Components

### `componentDidCatch(error, info)`

- **When:** When a child component throws an error during rendering, in a lifecycle method, or in the constructor.
- **Purpose:**
  - Handle errors gracefully and prevent the app from crashing
  - Useful for logging and rendering fallback UIs

- **Example:**
  ```javascript
  componentDidCatch(error, info) {
    logErrorToMyService(error, info);
    this.setState({ hasError: true });
  }
  ```

- **Notes:**
  - Only works in class components that act as "error boundaries"

---

## Complete Class Component Example

```javascript
class Timer extends React.Component {
  constructor(props) {
    super(props);
    this.state = { 
      seconds: 0,
      hasError: false 
    };
    this.tick = this.tick.bind(this);
  }

  componentDidMount() {
    this.interval = setInterval(this.tick, 1000);
  }

  componentDidUpdate(prevProps, prevState) {
    if (prevState.seconds !== this.state.seconds) {
      console.log(`Timer updated: ${this.state.seconds} seconds`);
    }
  }

  componentWillUnmount() {
    clearInterval(this.interval);
  }

  componentDidCatch(error, info) {
    this.setState({ hasError: true });
    console.error('Timer error:', error, info);
  }

  tick() {
    this.setState(prevState => ({
      seconds: prevState.seconds + 1
    }));
  }

  render() {
    if (this.state.hasError) {
      return <div>Something went wrong.</div>;
    }

    return (
      <div>
        Seconds: {this.state.seconds}
      </div>
    );
  }
}
```

## Functional Component with Hooks Equivalent

```javascript
import { useState, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(prevSeconds => prevSeconds + 1);
    }, 1000);

    // Cleanup function (equivalent to componentWillUnmount)
    return () => clearInterval(interval);
  }, []); // Empty dependency array means this effect runs once (like componentDidMount)

  useEffect(() => {
    // This runs after every update (like componentDidUpdate)
    console.log(`Timer updated: ${seconds} seconds`);
  }, [seconds]); // Only runs when seconds changes

  return (
    <div>
      Seconds: {seconds}
    </div>
  );
}
```

## Class Components vs Hooks Comparison

| Feature | Class Components | Function Components with Hooks |
|---------|------------------|--------------------------------|
| **State** | `this.state` and `this.setState()` | `useState()` hook |
| **Side Effects** | Lifecycle methods | `useEffect()` hook |
| **Performance** | `shouldComponentUpdate()` | `React.memo()` and `useMemo()` |
| **Context** | `this.context` | `useContext()` hook |
| **Refs** | `this.refs` or `React.createRef()` | `useRef()` hook |
| **Error Boundaries** | `componentDidCatch()` | Not available (use class components) |
| **Code Reuse** | Higher-Order Components (HOCs) | Custom hooks |
| **Learning Curve** | Steeper (need to understand `this`) | Gentler (just functions) |
| **Bundle Size** | Slightly larger | Slightly smaller |