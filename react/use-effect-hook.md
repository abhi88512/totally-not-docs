# React useEffect Guide - Interview Questions

## Question 1: What is useEffect in React?
useEffect is a hook used in functional components to perform side effects after rendering, such as data fetching, subscriptions, or manual DOM manipulation.

### Simple Example:
```jsx
function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;
  });

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
}
```

---

## Question 2: Why is dependency array used in useEffect?
- **When it's empty `[]`** - runs only once
- **When values inside it change** - the effect re-runs
- **If removed** - the effect runs after every render

Handling dependencies ensures that the effect runs only when necessary and prevents unnecessary re-execution of the effect, optimizing performance and avoiding potential bugs.

### Examples:
```jsx
// Runs every render
useEffect(() => {
  console.log('Every render');
});

// Runs once
useEffect(() => {
  console.log('Only once');
}, []);

// Runs when count changes
useEffect(() => {
  console.log('Count changed');
}, [count]);
```

---

## Question 3: Example of useEffect for data fetching.

```jsx
function UserProfile() {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch('/api/user/1')
      .then(response => response.json())
      .then(data => setUser(data));
  }, []);

  if (!user) return <div>Loading...</div>;

  return <div>{user.first_name} {user.last_name}</div>;
}
```

---

## Question 4: Convert major lifecycle methods to useEffect and Explain.

```jsx
function LifecycleExample() {
  const [count, setCount] = useState(0);

  // componentDidMount - runs once
  useEffect(() => {
    console.log('Mounted');
  }, []);

  // componentDidUpdate - runs when count changes
  useEffect(() => {
    console.log('Count updated');
  }, [count]);

  // componentWillUnmount - cleanup function
  useEffect(() => {
    return () => console.log('Unmounting');
  }, []);

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
}
```

---

## Question 5: How to perform cleanup in useEffect? Explain with example.
You can return a cleanup function inside useEffect, which runs before the effect re-runs or when the component unmounts. This is useful for cleaning up subscriptions or event listeners.

```jsx
function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(prev => prev + 1);
    }, 1000);

    // Cleanup function
    return () => clearInterval(interval);
  }, []);

  return <div>{seconds}</div>;
}
```

### Event Listener Cleanup:
```jsx
function WindowSize() {
  const [size, setSize] = useState(window.innerWidth);

  useEffect(() => {
    const handleResize = () => setSize(window.innerWidth);
    
    window.addEventListener('resize', handleResize);
    
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  return <div>Width: {size}</div>;
}
```

---

## Question 6: Explain useLayoutEffect and how it is different from useEffect?

### useEffect:
- **Asynchronous**: Runs after the render cycle is committed to the screen
- **Good for Performance**: Does not block the browser from painting changes on the screen

### useLayoutEffect:
- **Synchronous**: Runs synchronously immediately after DOM is updated but before the browser paints
- **Potentially Blocking**: Can cause delays in rendering if operations are heavy

### Simple Comparison:
```jsx
function EffectComparison() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log('useEffect - runs after paint');
  });

  useLayoutEffect(() => {
    console.log('useLayoutEffect - runs before paint');
  });

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
}
```

### useLayoutEffect Examples:

**1. Preventing Visual Flicker:**
```jsx
function ScrollToTop() {
  const ref = useRef();

  useLayoutEffect(() => {
    // This runs BEFORE paint - no flicker
    ref.current.scrollTop = 0;
  });

  return <div ref={ref}>Long scrollable content...</div>;
}
```

**2. DOM Measurements:**
```jsx
function AutoSize() {
  const [width, setWidth] = useState(0);
  const ref = useRef();

  useLayoutEffect(() => {
    // Measure before paint to avoid layout shift
    setWidth(ref.current.getBoundingClientRect().width);
  });

  return (
    <div>
      <div ref={ref}>Content to measure</div>
      <p>Width: {width}px</p>
    </div>
  );
}
```

**3. Tooltip Positioning:**
```jsx
function Tooltip({ children, text }) {
  const [position, setPosition] = useState({ top: 0, left: 0 });
  const tooltipRef = useRef();

  useLayoutEffect(() => {
    const rect = tooltipRef.current.getBoundingClientRect();
    // Position tooltip before paint to avoid jump
    setPosition({
      top: rect.bottom + 5,
      left: rect.left
    });
  });

  return (
    <div ref={tooltipRef}>
      {children}
      <div style={{ position: 'absolute', ...position }}>
        {text}
      </div>
    </div>
  );
}
```

### When to use useLayoutEffect:
- **DOM measurements** - Reading element dimensions, positions
- **Preventing visual flicker** - When you need to update DOM before paint
- **Synchronous DOM mutations** - Immediate DOM changes that affect layout
- **Animation setup** - When timing is critical for smooth animations

### When to use useEffect (most cases):
- **Data fetching** - API calls, async operations
- **Subscriptions** - Event listeners, websockets
- **Timers** - setTimeout, setInterval
- **Side effects** - Logging, analytics, non-DOM operations

**Rule of thumb:** Use useEffect by default, only use useLayoutEffect when you specifically need synchronous DOM operations before paint.

---

## Question 7: Create a useEffect polyfill

```jsx
import { useRef } from 'react';

function useEffectPolyfill(callback, dependencies) {
  const hasMount = useRef(false);
  const prevDeps = useRef(null);
  const cleanup = useRef(null);

  // Helper function to compare dependencies
  const areDepsEqual = (prevDeps, nextDeps) => {
    if (prevDeps === null || nextDeps === null) return false;
    if (prevDeps.length !== nextDeps.length) return false;
    
    for (let i = 0; i < prevDeps.length; i++) {
      if (prevDeps[i] !== nextDeps[i]) return false;
    }
    return true;
  };

  // Determine if effect should run
  const shouldRunEffect = 
    !hasMount.current || // First render
    dependencies === undefined || // No dependency array (run every time)
    !areDepsEqual(prevDeps.current, dependencies); // Dependencies changed

  if (shouldRunEffect) {
    // Run cleanup function if exists
    if (cleanup.current) {
      cleanup.current();
      cleanup.current = null;
    }

    // Execute the effect after render (simulate async behavior)
    setTimeout(() => {
      const cleanupFn = callback();
      cleanup.current = typeof cleanupFn === 'function' ? cleanupFn : null;
    }, 0);
    
    // Update refs
    hasMount.current = true;
    prevDeps.current = dependencies ? [...dependencies] : null;
  }
}
```

### Usage Example:
```jsx
function Counter() {
  const [count, setCount] = useState(0);

  useEffectPolyfill(() => {
    console.log('Count changed:', count);
    
    // Cleanup function
    return () => {
      console.log('Cleanup for count:', count);
    };
  }, [count]);

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
}
```

### Key Fixes in Implementation:
- **Async execution**: Uses `setTimeout` to simulate useEffect's post-render timing
- **Proper dependency handling**: Handles `undefined` dependencies (runs every render)
- **Cleanup safety**: Checks if cleanup is a function before storing
- **Dependency copying**: Creates a copy of dependencies array to prevent mutations
- **Null initialization**: Properly initializes refs with `null`