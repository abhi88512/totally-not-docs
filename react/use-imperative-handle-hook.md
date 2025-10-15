# React useImperativeHandle Guide - Interview Questions

## Question 1: What is useImperativeHandle in React?
- useImperativeHandle is a hook that lets you customize the instance value that is exposed to parent components when using `ref`
- It allows you to expose specific functions or values from a child component to its parent
- Used with `forwardRef` to create imperative APIs for child components

### Basic Syntax:
```jsx
useImperativeHandle(ref, () => ({
  // Methods/values to expose to parent
  methodName: () => { /* implementation */ }
}), [dependencies]);
```

---

## Question 2: How do you call a function of child component from parent component?

### Complete Example:
```jsx
import React, { forwardRef, useImperativeHandle, useRef } from 'react';

// Parent Component
function ParentComponent() {
  const childRef = useRef(null);

  const handleFocusInput = () => {
    childRef.current.focusInput();
  };

  const handleClearInput = () => {
    childRef.current.clearInput();
  };

  return (
    <div>
      <h3>Parent Component</h3>
      <button onClick={handleFocusInput}>Focus Child Input</button>
      <button onClick={handleClearInput}>Clear Child Input</button>
      
      <ChildComponent ref={childRef} />
    </div>
  );
}

// Child Component with forwardRef
const ChildComponent = forwardRef((props, ref) => {
  const inputRef = useRef(null);

  // Functions to expose to parent
  const focusInput = () => {
    inputRef.current.focus();
  };

  const clearInput = () => {
    inputRef.current.value = '';
  };

  // Expose functions to parent through ref
  useImperativeHandle(ref, () => ({
    focusInput,
    clearInput
  }));

  return (
    <div>
      <h4>Child Component</h4>
      <input type="text" ref={inputRef} placeholder="Type something..." />
    </div>
  );
});
```

---

## Question 3: When should you use useImperativeHandle?

### Use Cases:
- **Focus management** - Controlling input focus from parent
- **Animation triggers** - Starting animations from parent component
- **Form validation** - Exposing validation methods
- **Scroll control** - Programmatic scrolling
- **Media controls** - Play/pause video from parent

### Example - Multiple Methods:
```jsx
const MediaPlayer = forwardRef((props, ref) => {
  const videoRef = useRef(null);
  const [isPlaying, setIsPlaying] = useState(false);

  const play = () => {
    videoRef.current.play();
    setIsPlaying(true);
  };

  const pause = () => {
    videoRef.current.pause();
    setIsPlaying(false);
  };

  const setVolume = (volume) => {
    videoRef.current.volume = volume;
  };

  // Expose multiple methods to parent
  useImperativeHandle(ref, () => ({
    play,
    pause,
    setVolume,
    isPlaying
  }));

  return <video ref={videoRef} src={props.src} />;
});

// Usage in Parent
function App() {
  const playerRef = useRef(null);

  return (
    <div>
      <button onClick={() => playerRef.current.play()}>Play</button>
      <button onClick={() => playerRef.current.pause()}>Pause</button>
      <button onClick={() => playerRef.current.setVolume(0.5)}>50% Volume</button>
      
      <MediaPlayer ref={playerRef} src="video.mp4" />
    </div>
  );
}
```

---

## Question 4: What is forwardRef and why is it needed with useImperativeHandle?

### What is forwardRef?
- `forwardRef` lets your component receive a `ref` and pass it down to a child element
- By default, functional components don't receive refs as props
- Required when you want to expose imperative methods from child components

### Without forwardRef (Won't Work):
```jsx
// ❌ This won't work - functional components can't receive ref directly
function ChildComponent(props) {
  // props.ref is undefined
  return <input />;
}
```

### With forwardRef (Works):
```jsx
// ✅ This works - forwardRef passes ref as second parameter
const ChildComponent = forwardRef((props, ref) => {
  // ref is available here
  return <input ref={ref} />;
});
```

### Complete Pattern:
```jsx
const CustomInput = forwardRef((props, ref) => {
  const inputRef = useRef(null);

  useImperativeHandle(ref, () => ({
    focus: () => inputRef.current.focus(),
    getValue: () => inputRef.current.value,
    setValue: (value) => { inputRef.current.value = value; }
  }));

  return <input ref={inputRef} {...props} />;
});

// Parent usage
function Form() {
  const customInputRef = useRef(null);

  const handleSubmit = () => {
    const value = customInputRef.current.getValue();
    console.log('Input value:', value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <CustomInput ref={customInputRef} placeholder="Enter name" />
      <button type="button" onClick={() => customInputRef.current.focus()}>
        Focus Input
      </button>
      <button type="submit">Submit</button>
    </form>
  );
}
```

---

## Question 5: Simple Examples for Different Use Cases

### Example 1: Input Focus Control
```jsx
const FocusableInput = forwardRef((props, ref) => {
  const inputRef = useRef(null);

  useImperativeHandle(ref, () => ({
    focus: () => inputRef.current.focus(),
    blur: () => inputRef.current.blur()
  }));

  return <input ref={inputRef} {...props} />;
});

// Usage
function App() {
  const inputRef = useRef(null);

  return (
    <div>
      <FocusableInput ref={inputRef} placeholder="Click button to focus" />
      <button onClick={() => inputRef.current.focus()}>Focus</button>
    </div>
  );
}
```

### Example 2: Counter with Imperative Controls
```jsx
const Counter = forwardRef((props, ref) => {
  const [count, setCount] = useState(0);

  useImperativeHandle(ref, () => ({
    increment: () => setCount(prev => prev + 1),
    decrement: () => setCount(prev => prev - 1),
    reset: () => setCount(0),
    getCount: () => count
  }));

  return <div>Count: {count}</div>;
});

// Usage
function App() {
  const counterRef = useRef(null);

  return (
    <div>
      <Counter ref={counterRef} />
      <button onClick={() => counterRef.current.increment()}>+</button>
      <button onClick={() => counterRef.current.decrement()}>-</button>
      <button onClick={() => counterRef.current.reset()}>Reset</button>
    </div>
  );
}
```

### Example 3: Modal Control
```jsx
const Modal = forwardRef(({ children }, ref) => {
  const [isOpen, setIsOpen] = useState(false);

  useImperativeHandle(ref, () => ({
    open: () => setIsOpen(true),
    close: () => setIsOpen(false),
    toggle: () => setIsOpen(prev => !prev)
  }));

  if (!isOpen) return null;

  return (
    <div style={{ position: 'fixed', background: 'rgba(0,0,0,0.5)' }}>
      <div style={{ background: 'white', padding: '20px' }}>
        {children}
        <button onClick={() => setIsOpen(false)}>Close</button>
      </div>
    </div>
  );
});

// Usage
function App() {
  const modalRef = useRef(null);

  return (
    <div>
      <button onClick={() => modalRef.current.open()}>Open Modal</button>
      
      <Modal ref={modalRef}>
        <h3>Modal Content</h3>
        <p>This modal was opened imperatively!</p>
      </Modal>
    </div>
  );
}
```

---

## Key Interview Points:

### When to Use:
- ✅ **Need imperative API** - Parent needs to call child methods
- ✅ **Focus management** - Programmatic focus control
- ✅ **Animation triggers** - Starting/stopping animations
- ✅ **Form utilities** - Validation, clearing, etc.

### When NOT to Use:
- ❌ **Simple data passing** - Use props instead
- ❌ **Most cases** - React prefers declarative patterns
- ❌ **State sharing** - Use lifting state up or context

### Best Practices:
1. **Use sparingly** - Prefer declarative patterns when possible
2. **Clear method names** - Make the API intuitive
3. **Include dependencies** - Third parameter for optimization
4. **Document the API** - What methods are available to parent

### Pattern Summary:
```jsx
// 1. Child component uses forwardRef
const ChildComponent = forwardRef((props, ref) => {
  
  // 2. Define methods to expose
  const method1 = () => { /* logic */ };
  const method2 = () => { /* logic */ };
  
  // 3. Use useImperativeHandle to expose methods
  useImperativeHandle(ref, () => ({
    method1,
    method2
  }));
  
  return <div>Child Content</div>;
});

// 4. Parent creates ref and calls methods
function Parent() {
  const childRef = useRef(null);
  
  const handleClick = () => {
    childRef.current.method1();
  };
  
  return <ChildComponent ref={childRef} />;
}
```