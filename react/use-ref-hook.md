# React useRef Guide - Interview Questions

## Question 1: What is useRef in React?
- useRef is a hook used to create a mutable reference that persists across renders.
- It returns a mutable object with a .current property.

### Basic Syntax:
```jsx
const ref = useRef(initialValue);
```

### Simple Example:
```jsx
import React, { useRef, useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  const renderCount = useRef(0);

  // Increment render count on every render
  renderCount.current += 1;

  return (
    <div>
      <p>Count: {count}</p>
      <p>Renders: {renderCount.current}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

---

## Question 2: When would you use useRef?

### Common Use Cases:
- **Accessing DOM elements** or managing focus
- **Storing mutable values** that persist without causing re-renders
- **Caching values** to avoid re-initialization on re-renders
- **Storing previous values** for comparison
- **Timers and intervals** that need to be cleared

### Examples:

**1. Storing Values Without Re-renders:**
```jsx
function Timer() {
  const [time, setTime] = useState(0);
  const intervalRef = useRef(null);

  const startTimer = () => {
    intervalRef.current = setInterval(() => {
      setTime(prev => prev + 1);
    }, 1000);
  };

  const stopTimer = () => {
    clearInterval(intervalRef.current);
  };

  return (
    <div>
      <p>Time: {time}</p>
      <button onClick={startTimer}>Start</button>
      <button onClick={stopTimer}>Stop</button>
    </div>
  );
}
```

**2. Storing Previous Values:**
```jsx
function PreviousValue({ value }) {
  const prevValue = useRef();

  useEffect(() => {
    prevValue.current = value;
  });

  return (
    <div>
      <p>Current: {value}</p>
      <p>Previous: {prevValue.current}</p>
    </div>
  );
}
```

---

## Question 3: How do you access a DOM element using useRef?

### Basic DOM Access:
```jsx
function FocusInput() {
  const inputRef = useRef(null);

  const handleClick = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="Click button to focus" />
      <button onClick={handleClick}>Focus Input</button>
    </div>
  );
}
```

### Scroll to Element:
```jsx
function ScrollExample() {
  const elementRef = useRef(null);

  const scrollToElement = () => {
    elementRef.current.scrollIntoView({ behavior: 'smooth' });
  };

  return (
    <div>
      <button onClick={scrollToElement}>Scroll to Element</button>
      <div style={{ height: '1000px' }}>Spacer</div>
      <div ref={elementRef} style={{ backgroundColor: 'yellow' }}>
        Target Element
      </div>
    </div>
  );
}
```

### Getting Element Properties:
```jsx
function ElementInfo() {
  const divRef = useRef(null);
  const [info, setInfo] = useState({});

  const getInfo = () => {
    const element = divRef.current;
    setInfo({
      width: element.offsetWidth,
      height: element.offsetHeight,
      text: element.textContent
    });
  };

  return (
    <div>
      <div ref={divRef} style={{ padding: '20px', backgroundColor: 'lightblue' }}>
        This is a div element
      </div>
      <button onClick={getInfo}>Get Element Info</button>
      <pre>{JSON.stringify(info, null, 2)}</pre>
    </div>
  );
}
```

---

## Question 4: Difference between useState and useRef?

### useState:
- **Manages state** and triggers re-renders when its value changes
- When you update it using `setStateValue`, the component re-renders
- **Updated value is reflected in the UI**
- **Asynchronous updates** (batched)

### useRef:
- **Holds a mutable value** (`current`) that persists across renders without causing re-renders
- When you update it (`refValue.current = ...`), the component doesn't re-render
- **Updated value is stored and accessible** across renders
- **Synchronous updates** (immediate)

### Comparison Example:
```jsx
function StateVsRef() {
  const [stateCount, setStateCount] = useState(0);
  const refCount = useRef(0);

  const incrementState = () => {
    setStateCount(stateCount + 1); // Triggers re-render
    console.log('State updated, component will re-render');
  };

  const incrementRef = () => {
    refCount.current += 1; // No re-render
    console.log('Ref updated, no re-render:', refCount.current);
  };

  console.log('Component rendered'); // Logs on every render

  return (
    <div>
      <p>State Count: {stateCount}</p>
      <p>Ref Count: {refCount.current}</p>
      
      <button onClick={incrementState}>Increment State</button>
      <button onClick={incrementRef}>Increment Ref</button>
      
      {/* Force re-render to see ref value update */}
      <button onClick={() => setStateCount(s => s)}>Force Re-render</button>
    </div>
  );
}
```

### When to Use Which:

**Use useState when:**
- Value changes should trigger re-renders
- Value is displayed in UI
- You need component to react to changes

**Use useRef when:**
- Need to store values without re-rendering
- Accessing DOM elements
- Storing timers, intervals, or subscriptions
- Caching expensive computations
- Storing previous values for comparison

### Key Differences Summary:

| Feature | useState | useRef |
|---------|----------|---------|
| **Re-renders** | ✅ Yes | ❌ No |
| **UI Updates** | ✅ Automatic | ❌ Manual |
| **Persistence** | ✅ Yes | ✅ Yes |
| **Direct Mutation** | ❌ No (use setter) | ✅ Yes (.current) |
| **Update Timing** | Async | Sync |
| **Use Cases** | UI state | DOM access, caching |