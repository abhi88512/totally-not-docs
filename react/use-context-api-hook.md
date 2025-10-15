# React useContext Guide - Interview Questions

## Question 1: What is useContext in React?
- Used to consume values (like data or functions) from a context created by `createContext()`
- It allows functional components to access context values without prop drilling
- In scenarios where passing props through multiple levels of components is impractical

### Basic Syntax:
```jsx
const contextValue = useContext(MyContext);
```

### Simple Example:
```jsx
import React, { createContext, useContext, useState } from 'react';

// 1. Create Context
const UserContext = createContext();

// 2. Provider Component
function App() {
  const [user, setUser] = useState({ name: 'John', role: 'admin' });
  
  return (
    <UserContext.Provider value={{ user, setUser }}>
      <Header />
      <Profile />
    </UserContext.Provider>
  );
}

// 3. Consumer Component (without prop drilling)
function Header() {
  const { user } = useContext(UserContext);
  
  return <h1>Welcome, {user.name}!</h1>;
}

function Profile() {
  const { user, setUser } = useContext(UserContext);
  
  return (
    <div>
      <p>Name: {user.name}</p>
      <p>Role: {user.role}</p>
      <button onClick={() => setUser({ ...user, name: 'Jane' })}>
        Change Name
      </button>
    </div>
  );
}
```

---

## Question 2: What problem does useContext solve?

### Problem: Prop Drilling
```jsx
// Without Context - Prop Drilling
function App() {
  const [user, setUser] = useState({ name: 'John' });
  
  return <Level1 user={user} setUser={setUser} />;
}

function Level1({ user, setUser }) {
  return <Level2 user={user} setUser={setUser} />;
}

function Level2({ user, setUser }) {
  return <Level3 user={user} setUser={setUser} />;
}

function Level3({ user, setUser }) {
  return <div>{user.name}</div>; // Finally used here!
}
```

### Solution: useContext
```jsx
// With Context - No Prop Drilling
const UserContext = createContext();

function App() {
  const [user, setUser] = useState({ name: 'John' });
  
  return (
    <UserContext.Provider value={{ user, setUser }}>
      <Level1 />
    </UserContext.Provider>
  );
}

function Level1() {
  return <Level2 />; // No props needed
}

function Level2() {
  return <Level3 />; // No props needed
}

function Level3() {
  const { user } = useContext(UserContext); // Direct access!
  return <div>{user.name}</div>;
}
```

---

## Question 3: Can you have multiple contexts in a single component?

**Yes!** You can use multiple contexts in a single component.

### Multiple Contexts Example:
```jsx
import React, { createContext, useContext, useState } from 'react';

// Create multiple contexts
const UserContext = createContext();
const ThemeContext = createContext();
const LanguageContext = createContext();

function App() {
  const [user, setUser] = useState({ name: 'John' });
  const [theme, setTheme] = useState('dark');
  const [language, setLanguage] = useState('en');

  return (
    <UserContext.Provider value={{ user, setUser }}>
      <ThemeContext.Provider value={{ theme, setTheme }}>
        <LanguageContext.Provider value={{ language, setLanguage }}>
          <Dashboard />
        </LanguageContext.Provider>
      </ThemeContext.Provider>
    </UserContext.Provider>
  );
}

function Dashboard() {
  // Using multiple contexts in one component
  const { user } = useContext(UserContext);
  const { theme, setTheme } = useContext(ThemeContext);
  const { language } = useContext(LanguageContext);

  return (
    <div style={{ 
      backgroundColor: theme === 'dark' ? '#333' : '#fff',
      color: theme === 'dark' ? '#fff' : '#333'
    }}>
      <h1>Hello {user.name}!</h1>
      <p>Theme: {theme}</p>
      <p>Language: {language}</p>
      
      <button onClick={() => setTheme(theme === 'dark' ? 'light' : 'dark')}>
        Toggle Theme
      </button>
    </div>
  );
}
```

### Nested Providers (Alternative Pattern):
```jsx
function App() {
  return (
    <UserProvider>
      <ThemeProvider>
        <LanguageProvider>
          <Dashboard />
        </LanguageProvider>
      </ThemeProvider>
    </UserProvider>
  );
}

// Custom Provider Components
function UserProvider({ children }) {
  const [user, setUser] = useState({ name: 'John' });
  return (
    <UserContext.Provider value={{ user, setUser }}>
      {children}
    </UserContext.Provider>
  );
}

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('dark');
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}
```

### Custom Hooks for Cleaner Code:
```jsx
// Custom hooks for each context
const useUser = () => {
  const context = useContext(UserContext);
  if (!context) {
    throw new Error('useUser must be used within UserProvider');
  }
  return context;
};

const useTheme = () => {
  const context = useContext(ThemeContext);
  if (!context) {
    throw new Error('useTheme must be used within ThemeProvider');
  }
  return context;
};

// Usage in component
function Dashboard() {
  const { user } = useUser();
  const { theme, setTheme } = useTheme();
  const { language } = useContext(LanguageContext);

  return (
    <div>
      <h1>Hello {user.name}!</h1>
      <p>Theme: {theme}</p>
      <p>Language: {language}</p>
    </div>
  );
}
```

---

## Common useContext Patterns

### 1. Authentication Context:
```jsx
const AuthContext = createContext();

function AuthProvider({ children }) {
  const [user, setUser] = useState(null);
  
  const login = (userData) => setUser(userData);
  const logout = () => setUser(null);
  
  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
}

function LoginButton() {
  const { user, login, logout } = useContext(AuthContext);
  
  return (
    <button onClick={user ? logout : () => login({ name: 'John' })}>
      {user ? 'Logout' : 'Login'}
    </button>
  );
}
```

### 2. Shopping Cart Context:
```jsx
const CartContext = createContext();

function CartProvider({ children }) {
  const [items, setItems] = useState([]);
  
  const addItem = (item) => setItems(prev => [...prev, item]);
  const removeItem = (id) => setItems(prev => prev.filter(item => item.id !== id));
  const total = items.reduce((sum, item) => sum + item.price, 0);
  
  return (
    <CartContext.Provider value={{ items, addItem, removeItem, total }}>
      {children}
    </CartContext.Provider>
  );
}
```

---

## Key Points for Interviews:

### When to Use useContext:
- ✅ **Avoid prop drilling** through multiple component levels
- ✅ **Global state** needed by many components (theme, auth, language)
- ✅ **Provider pattern** for reusable logic

### When NOT to Use useContext:
- ❌ **Simple prop passing** (1-2 levels down)
- ❌ **Frequently changing data** (can cause unnecessary re-renders)
- ❌ **Complex state management** (consider Redux/Zustand instead)

### Performance Considerations:
- **Context value changes** cause all consuming components to re-render
- **Split contexts** to minimize re-renders
- **Memoize context values** when possible:

```jsx
const contextValue = useMemo(() => ({
  user,
  setUser
}), [user]);

return (
  <UserContext.Provider value={contextValue}>
    {children}
  </UserContext.Provider>
);
```