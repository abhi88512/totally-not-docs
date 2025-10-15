# React useReducer Guide - Interview Questions

## Question 1: What is useReducer in React?
- It is a hook used for managing complex state logic by utilizing a reducer function
- Alternative to useState and provides a way to update state based on defined actions
- Follows Redux-like pattern with state, actions, and reducer function

### Basic Syntax:
```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

### Simple Example:
```jsx
function counterReducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    case 'reset':
      return { count: 0 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(counterReducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <button onClick={() => dispatch({ type: 'reset' })}>Reset</button>
    </div>
  );
}
```

---

## Question 2: When should you use useReducer instead of useState?
- When managing complex state transitions or logic that involves multiple sub-values
- When state logic follows a pattern or when multiple actions need to update the state in predictable ways
- When you have multiple related state updates
- When next state depends on previous state

### Simple Comparison:

**useState - Simple:**
```jsx
function SimpleCounter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
}
```

**useReducer - Complex:**
```jsx
function todoReducer(state, action) {
  switch (action.type) {
    case 'add':
      return [...state, { id: Date.now(), text: action.text, done: false }];
    case 'toggle':
      return state.map(todo => 
        todo.id === action.id ? { ...todo, done: !todo.done } : todo
      );
    default:
      return state;
  }
}

function TodoList() {
  const [todos, dispatch] = useReducer(todoReducer, []);

  return (
    <div>
      <button onClick={() => dispatch({ type: 'add', text: 'New Todo' })}>
        Add Todo
      </button>
      {todos.map(todo => (
        <div key={todo.id} onClick={() => dispatch({ type: 'toggle', id: todo.id })}>
          {todo.text} - {todo.done ? 'Done' : 'Pending'}
        </div>
      ))}
    </div>
  );
}
```

---

## Question 3: Give Example of useReducer?

### Example 1: Simple Todo App
```jsx
function todoReducer(state, action) {
  switch (action.type) {
    case 'add':
      return [...state, { id: Date.now(), text: action.text }];
    case 'remove':
      return state.filter(todo => todo.id !== action.id);
    default:
      return state;
  }
}

function TodoApp() {
  const [todos, dispatch] = useReducer(todoReducer, []);

  const addTodo = () => {
    dispatch({ type: 'add', text: 'New Task' });
  };

  return (
    <div>
      <button onClick={addTodo}>Add Todo</button>
      {todos.map(todo => (
        <div key={todo.id}>
          {todo.text}
          <button onClick={() => dispatch({ type: 'remove', id: todo.id })}>
            Delete
          </button>
        </div>
      ))}
    </div>
  );
}
```

### Example 2: Form State
```jsx
function formReducer(state, action) {
  switch (action.type) {
    case 'setName':
      return { ...state, name: action.value };
    case 'setEmail':
      return { ...state, email: action.value };
    case 'reset':
      return { name: '', email: '' };
    default:
      return state;
  }
}

function ContactForm() {
  const [state, dispatch] = useReducer(formReducer, { name: '', email: '' });

  return (
    <form>
      <input
        value={state.name}
        onChange={(e) => dispatch({ type: 'setName', value: e.target.value })}
        placeholder="Name"
      />
      <input
        value={state.email}
        onChange={(e) => dispatch({ type: 'setEmail', value: e.target.value })}
        placeholder="Email"
      />
      <button type="button" onClick={() => dispatch({ type: 'reset' })}>
        Reset
      </button>
    </form>
  );
}
```

### Example 3: Shopping Cart
```jsx
function cartReducer(state, action) {
  switch (action.type) {
    case 'add':
      return [...state, action.item];
    case 'remove':
      return state.filter(item => item.id !== action.id);
    case 'clear':
      return [];
    default:
      return state;
  }
}

function Cart() {
  const [cart, dispatch] = useReducer(cartReducer, []);

  const addItem = (item) => {
    dispatch({ type: 'add', item });
  };

  return (
    <div>
      <button onClick={() => addItem({ id: 1, name: 'Apple', price: 1 })}>
        Add Apple
      </button>
      
      {cart.map(item => (
        <div key={item.id}>
          {item.name} - ${item.price}
          <button onClick={() => dispatch({ type: 'remove', id: item.id })}>
            Remove
          </button>
        </div>
      ))}
      
      <button onClick={() => dispatch({ type: 'clear' })}>Clear Cart</button>
      <p>Total: ${cart.reduce((sum, item) => sum + item.price, 0)}</p>
    </div>
  );
}
```

---

## When to Use Which:

**Use useState for:**
- Simple values (strings, numbers, booleans)
- Independent state updates
- Single piece of state

**Use useReducer for:**
- Multiple related state values
- Complex state logic
- State transitions that follow patterns
- When next state depends on previous state

---

## Key Interview Points:

1. **useReducer** is like useState but for complex state logic
2. **Reducer function** takes (state, action) and returns new state
3. **dispatch** function sends actions to reducer
4. **Actions** describe what happened, reducer decides how state changes
5. **Better for testing** - pure functions are easy to test
6. **Predictable** - same action always produces same state change