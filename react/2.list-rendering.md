# List Rendering and Conditional Operators in React

1. How does the map function work in React for rendering lists?
    - The map function iterates over an array and returns a new array of React elements, allowing dynamic rendering of lists.
    - Example:
      ```jsx
      {products.map(product => <li key={product.id}>{product.name}</li>)}
      ```

2. How can you filter products with a specific category?
    - Use the filter method to select products matching a category, then map to render them.
    - Example:
      ```jsx
      {products.filter(p => p.category === "Electronics").map(p => <li key={p.id}>{p.name}</li>)}
      ```

3. How can you render a summary of total prices for products?
    - Use the reduce method to sum up product prices and display the result.
    - Example:
      ```jsx
      {products.reduce((acc, p) => acc + p.price, 0)}
      ```

4. How do you add a discountedPrice key with 10% discount to all products with price more than $20 and render it?
    - Filter products with price > 20, map to add discountedPrice, then render.
    - Example:
      ```jsx
      {products.filter(p => p.price > 20).map(p => ({...p, discountedPrice: p.price * 0.9})).map(p => <li key={p.id}>{p.name} - ${p.discountedPrice}</li>)}
      ```

5. How can you filter and render unique elements from an array using filter in React?
    - Use filter with indexOf to keep only the first occurrence of each element.
    - Example:
      ```jsx
      {names.filter((name, idx) => names.indexOf(name) === idx).map(name => <li key={name}>{name}</li>)}
      ```

6. What is the difference between && and || in React (JSX)?
    - && (logical AND) renders the right side if the left side is truthy; || (logical OR) renders the right side if the left is falsy.
    - Example: `{isLoggedIn && <p>Welcome!</p>}` only renders if isLoggedIn is true.

7. What is the difference between ?. (optional chaining) and ?? (nullish coalescing) in JavaScript?
    - ?. safely accesses nested properties, returning undefined if any part is null/undefined; ?? returns the right side if the left is null or undefined.
    - Example: `user?.address?.city` vs `userInput ?? 'default'`
