# C++ Stack (std::stack) Documentation

**Last In, First Out (LIFO)**

> A container adapter that provides stack functionality - elements are inserted and removed from the top only.

## 📋 Table of Contents
- [Declaration & Initialization](#declaration--initialization)
- [Core Operations](#core-operations)
- [Basic Usage Example](#basic-usage-example)
- [Iteration Patterns](#iteration-patterns)
- [Common Use Cases](#common-use-cases)
- [Performance Characteristics](#performance-characteristics)
- [Error Handling](#error-handling)
- [Best Practices](#best-practices)

## Declaration & Initialization
```cpp
#include <stack>
#include <vector>
#include <list>
#include <string>

// Basic declaration (uses std::deque by default)
std::stack<int> s;

// With specific underlying container
std::stack<int, std::vector<int>> s_vector;
std::stack<int, std::list<int>> s_list;

// Stack with custom types
std::stack<std::string> str_stack;
```

## Core Operations

| Operation | Syntax | Description | Time Complexity |
|-----------|--------|-------------|-----------------|
| **Push** | `s.push(value)` | Add element to top | O(1) |
| **Pop** | `s.pop()` | Remove top element | O(1) |
| **Top** | `s.top()` | Access top element | O(1) |
| **Size** | `s.size()` | Get number of elements | O(1) |
| **Empty** | `s.empty()` | Check if stack is empty | O(1) |

## Basic Usage Example
```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> s;
    
    s.push(10); // Stack: [10]
    s.push(20); // Stack: [10, 20]
    s.push(30); // Stack: [10, 20, 30]
    
    std::cout << "Top element: " << s.top() << std::endl; // 30
    
    s.pop(); // Removes 30. Stack: [10, 20]
    
    std::cout << "New top element: " << s.top() << std::endl; // 20
    
    std::cout << "Stack size: " << s.size() << std::endl; // 2
    
    std::cout << "Is stack empty? " << (s.empty() ? "Yes" : "No") << std::endl; // No
    
    return 0;
}
```

## Iteration Patterns

> ⚠️ **Important:** `std::stack` is a container adapter and does not provide iterators for direct looping. To access all elements, you must pop them one by one, which is a destructive process.

### Destructive Iteration
```cpp
// This process empties the original stack
std::cout << "Stack elements (LIFO): ";
while(!s.empty()) {
    std::cout << s.top() << " ";
    s.pop();
}
std::cout << std::endl;
// s is now empty
```

### Non-Destructive Iteration (using a copy)
```cpp
// Create a copy to preserve the original stack
std::stack<int> temp = s;
std::cout << "Stack elements (non-destructive): ";
while(!temp.empty()) {
    std::cout << temp.top() << " ";
    temp.pop();
}
std::cout << std::endl;
// s remains unchanged
```

## Common Use Cases

- **Expression Parsing**: Evaluating mathematical expressions, especially for handling operator precedence and parentheses.
- **Backtracking Algorithms**: Such as solving mazes or in Depth-First Search (DFS) on a graph.
- **Undo Functionality**: In applications like text editors, storing previous states to revert to.
- **Function Call Simulation**: Managing activation records in recursion simulation.

## Performance Characteristics

- **Push/Pop operations**: O(1) for all underlying containers (`std::deque`, `std::vector`, `std::list`).
- **Memory Usage**: Depends on the underlying container. `std::vector` is the most memory-efficient, while `std::list` has higher per-element overhead. `std::deque` (the default) is a balance between the two.

## Error Handling

- Calling `s.top()` or `s.pop()` on an empty stack results in **undefined behavior**.
- Always check if the stack is empty using `s.empty()` before attempting to access or pop elements.
```cpp
if (!s.empty()) {
    // It's safe to call s.top() and s.pop()
    int top_element = s.top();
    s.pop();
}
```

## Best Practices

- Use `std::stack` when you strictly need LIFO behavior.
- Choose the underlying container based on performance needs, though the default `std::deque` is suitable for most cases.
- Pass stacks by `const&` to functions if they only need to be read (requires making a copy inside for iteration).
- Do not use `std::stack` if you need to access elements other than the top one.

---

**References:**
- [cppreference.com - std::stack](https://en.cppreference.com/w/cpp/container/stack)
- [C++ Standard Library Documentation](https://docs.microsoft.com/en-us/cpp/standard-library/)