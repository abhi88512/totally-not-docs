# React Components Guide

## Question 1: What are Smart / Stateful / Container Components?
Manages state, handles business logic, and passes data down to presentational components.

## Question 2: What are Dumb / Stateless / Presentational Components?
- Only renders UI based on the props it receives.
- Doesn't have its own state or lifecycle methods.

## Question 3: What are Higher Order Component (HOC)?
- Function that takes a component and returns a new enhanced component.
- Used for code reuse, logic sharing, and adding additional functionalities to components.

## Question 4: What are Pure Components?
- Optimize the rendering performance of components by reducing unnecessary re-renders by implementing shallow comparison of props and state.

## Question 5: What are Controlled Components?
- Value of the input field is controlled by React through state.
- React manages the input's value and handles updates through event handlers.

## Question 6: What are Un-Controlled Components?
- Input field maintains its own state using the DOM.
- React doesn't control the value, but it can still interact with the input using refs.

## Question 7: Examples of Each Component Type (Interview-Friendly)

### 1. Smart/Container Components
**Class-based:**
```jsx
class Counter extends React.Component {
  state = { count: 0 };

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return <CounterDisplay count={this.state.count} onIncrement={this.increment} />;
  }
}
```

**Functional:**
```jsx
function Counter() {
  const [count, setCount] = useState(0);
  return <CounterDisplay count={count} onIncrement={() => setCount(count + 1)} />;
}
```

### 2. Dumb/Presentational Components
**Class-based:**
```jsx
class CounterDisplay extends React.Component {
  render() {
    return (
      <div>
        <p>Count: {this.props.count}</p>
        <button onClick={this.props.onIncrement}>+</button>
      </div>
    );
  }
}
```

**Functional:**
```jsx
function CounterDisplay({ count, onIncrement }) {
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={onIncrement}>+</button>
    </div>
  );
}
```

### 3. Higher Order Components (HOC)
**Basic HOC:**
```jsx
function withLoading(Component) {
  return function(props) {
    if (props.loading) return <div>Loading...</div>;
    return <Component {...props} />;
  };
}

// Usage
const ProfileWithLoading = withLoading(UserProfile);
```

### 4. Pure Components
**Class-based:**
```jsx
class PureButton extends React.PureComponent {
  render() {
    return <button onClick={this.props.onClick}>{this.props.label}</button>;
  }
}
```

**Functional:**
```jsx
const PureButton = React.memo(({ onClick, label }) => {
  return <button onClick={onClick}>{label}</button>;
});
```

### 5. Controlled Components
**Class-based:**
```jsx
class ControlledInput extends React.Component {
  state = { value: '' };

  handleChange = (e) => {
    this.setState({ value: e.target.value });
  };

  render() {
    return <input value={this.state.value} onChange={this.handleChange} />;
  }
}
```

**Functional:**
```jsx
function ControlledInput() {
  const [value, setValue] = useState('');
  return <input value={value} onChange={(e) => setValue(e.target.value)} />;
}
```

### 6. Un-Controlled Components
**Class-based:**
```jsx
class UncontrolledInput extends React.Component {
  inputRef = React.createRef();

  handleSubmit = () => {
    console.log(this.inputRef.current.value);
  };

  render() {
    return (
      <div>
        <input ref={this.inputRef} defaultValue="Hello" />
        <button onClick={this.handleSubmit}>Submit</button>
      </div>
    );
  }
}
```

**Functional:**
```jsx
function UncontrolledInput() {
  const inputRef = useRef();

  const handleSubmit = () => {
    console.log(inputRef.current.value);
  };

  return (
    <div>
      <input ref={inputRef} defaultValue="Hello" />
      <button onClick={handleSubmit}>Submit</button>
    </div>
  );
}
```

## Key Differences Summary

- **Smart Components**: Handle state and business logic, pass data to presentational components
- **Dumb Components**: Pure UI components that only receive and display props
- **HOC**: Functions that enhance components with additional functionality
- **Pure Components**: Optimize performance by preventing unnecessary re-renders
- **Controlled Components**: React controls the input values through state
- **Uncontrolled Components**: DOM maintains input state, accessed via refs