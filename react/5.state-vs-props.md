# React State vs Props Guide

## Question 1: Explain state vs props in both class and functional components

### Props
- **Read-only data** passed from a parent component to a child component
- **Immutable** and are used to communicate between components
- Cannot be modified by the child component

### State
- **Mutable** and represents the internal state of a component
- **Managed and controlled** within the component itself
- Can be updated using `setState()` (class) or `useState()` (functional)

### Key Differences:

| Aspect | Props | State |
|--------|-------|-------|
| **Mutability** | Immutable | Mutable |
| **Source** | Passed from parent | Internal to component |
| **Purpose** | Data flow between components | Component's internal data |
| **Access in Class** | `this.props` | `this.state` |
| **Access in Functional** | Function parameter | `useState()` hook |

### Class Component Example:

```javascript
// Parent component with state
class Parent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { message: "Hello World" };
  }

  render() {
    return (
      <Child greeting={this.state.message} />
    );
  }
}

// Child component receives props
class Child extends React.Component {
  render() {
    return <h1>{this.props.greeting}</h1>;
  }
}
```

### Functional Component Example:

```javascript
import { useState } from 'react';

// Parent component with state
function Parent() {
  const [message, setMessage] = useState("Hello World");

  return <Child greeting={message} />;
}

// Child component receives props
function Child({ greeting }) {
  return <h1>{greeting}</h1>;
}
```

## Question 2: What is children prop? Give an example

The **`children` prop** is a special prop that allows you to pass components or elements as children to other components. It enables component composition and makes components more reusable.

### Key Points:
- `children` is automatically passed to every component
- Can contain text, elements, or other React components
- Enables wrapper/container components
- Accessible via `props.children` in class components or destructured in functional components

### Class Component Example:

```javascript
// Wrapper component using children
class Box extends React.Component {
  render() {
    return (
      <div style={{ border: '1px solid black', padding: '10px' }}>
        {this.props.children}
      </div>
    );
  }
}

// Usage
class App extends React.Component {
  render() {
    return (
      <Box>
        <h1>Title</h1>
        <p>This is inside the box!</p>
      </Box>
    );
  }
}
```

### Functional Component Example:

```javascript
// Wrapper component using children
function Box({ children }) {
  return (
    <div style={{ border: '1px solid black', padding: '10px' }}>
      {children}
    </div>
  );
}

// Usage
function App() {
  return (
    <Box>
      <h1>Title</h1>
      <p>This is inside the box!</p>
    </Box>
  );
}
```

