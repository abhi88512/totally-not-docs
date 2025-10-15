# React State Management - Interview Questions

## Question 1: What is useState in React?
useState is a hook in React that allows functional components to manage state by declaring state variables and providing a function to update them.

### Simple Example:
```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
}
```

---

## Question 2: What is Two Way Data Binding and How can you achieve it in React?
- It is a concept that allows the synchronization of data between the model (or state) and the view in both directions.
- You can achieve it by combining state management with controlled components.

### Simple Example:
```jsx
function TwoWayBinding() {
  const [text, setText] = useState('');

  return (
    <div>
      <input 
        value={text} 
        onChange={(e) => setText(e.target.value)} 
      />
      <p>You typed: {text}</p>
    </div>
  );
}
```

---

## Question 3: Build a Form containing First name, Last name and Email. Use only one state to manage all fields.

### Simple Example:
```jsx
function UserForm() {
  const [formData, setFormData] = useState({
    firstName: '',
    lastName: '',
    email: ''
  });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: value
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(formData);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        name="firstName"
        value={formData.firstName}
        onChange={handleChange}
        placeholder="First Name"
      />
      <input
        name="lastName"
        value={formData.lastName}
        onChange={handleChange}
        placeholder="Last Name"
      />
      <input
        name="email"
        type="email"
        value={formData.email}
        onChange={handleChange}
        placeholder="Email"
      />
      <button type="submit">Submit</button>
    </form>
  );
}
```