```markdown
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

// Basic declaration
stack<int> stk;

// With specific underlying container
stack<int, vector<int>> stk_vector;    // Using vector as underlying container
stack<int, deque<int>> stk_deque;      // Using deque (default)
stack<int, list<int>> stk_list;        // Using list

// Template with custom types
stack<string> str_stack;
stack<pair<int, string>> pair_stack;
```

## Core Operations

| Operation | Syntax | Description | Time Complexity |
|-----------|--------|-------------|-----------------|
| **Push** | `stk.push(value)` | Add element to top | O(1) |
| **Pop** | `stk.pop()` | Remove top element | O(1) |
| **Top** | `stk.top()` | Access top element | O(1) |
| **Size** | `stk.size()` | Get number of elements | O(1) |
| **Empty** | `stk.empty()` | Check if stack is empty | O(1) |

### Detailed Operation Examples
```cpp
stack<int> stk;

// Push operations
stk.push(10);                          // Stack: [10]
stk.push(20);                          // Stack: [10, 20]
stk.push(30);                          // Stack: [10, 20, 30]

// Access operations
int top_element = stk.top();           // top_element = 30
size_t stack_size = stk.size();        // stack_size = 3
bool is_empty = stk.empty();           // is_empty = false

// Pop operations
stk.pop();                             // Stack: [10, 20]
cout << "Top after pop: " << stk.top() << endl; // 20
```

## Basic Usage Example
```cpp
#include <iostream>
#include <stack>
using namespace std;

int main() {
    stack<int> stk;
    
    // Adding elements
    stk.push(3);
    stk.push(2);
    stk.push(1);                       // Stack: [3, 2, 1] (top to bottom)
    
    // Accessing elements
    cout << "Top element: " << stk.top() << endl;  // → 1
    
    // Removing elements
    stk.pop();                         // Remove top element (1)
    cout << "New top: " << stk.top() << endl;      // → 2
    
    // Size operations
    cout << "Size: " << stk.size() << endl;        // → 2
    cout << "Empty: " << stk.empty() << endl;      // → false (0)
    
    return 0;
}
```

## Iteration Patterns

> ⚠️ **Important:** Stacks don't support iterators. The only way to access all elements is by popping them.

### Destructive Iteration
```cpp
// WARNING: This destroys the original stack
while(!stk.empty()) {
    cout << stk.top() << " ";          // Access top element
    stk.pop();                         // Remove top element
}
// Output: 1 2 3 (LIFO order)
// Stack is now empty!
```

### Non-Destructive Iteration
```cpp
// Safe method: Copy stack first
stack<int> temp = stk;                 // Create copy
while(!temp.empty()) {
    cout << temp.top() << " ";         // Access top of copy
    temp.pop();                        // Remove from copy only
}
// Original stack remains unchanged
```

### Print Stack Function
```cpp
template<typename T>
void printStack(stack<T> s) {
    cout << "Stack (top to bottom): ";
    vector<T> elements;
    
    // Extract elements
    while(!s.empty()) {
        elements.push_back(s.top());
        s.pop();
    }
    
    // Print in order
    for(const T& elem : elements) {
        cout << elem << " ";
    }
    cout << endl;
}
```

## Common Use Cases

### Expression Evaluation (Parentheses Matching)
```cpp
bool isValidParentheses(string s) {
    stack<char> stk;
    
    for(char c : s) {
        if(c == '(' || c == '[' || c == '{') {
            stk.push(c);
        } else {
            if(stk.empty()) return false;
            
            char top = stk.top();
            stk.pop();
            
            if((c == ')' && top != '(') ||
               (c == ']' && top != '[') ||
               (c == '}' && top != '{')) {
                return false;
            }
        }
    }
    
    return stk.empty();
}
```

### Undo Operations
```cpp
class TextEditor {
private:
    string text;
    stack<string> undoStack;
    
public:
    void type(string newText) {
        undoStack.push(text);          // Save current state
        text += newText;
    }
    
    void undo() {
        if(!undoStack.empty()) {
            text = undoStack.top();    // Restore previous state
            undoStack.pop();
        }
    }
    
    string getText() { return text; }
};
```

### Function Call Stack Simulation
```cpp
void simulateRecursion() {
    stack<int> callStack;
    
    // Simulate function calls
    for(int i = 1; i <= 5; i++) {
        callStack.push(i);
        cout << "Calling function " << i << endl;
    }
    
    // Simulate function returns
    while(!callStack.empty()) {
        cout << "Returning from function " << callStack.top() << endl;
        callStack.pop();
    }
}
```

### Depth-First Search (DFS)
```cpp
void dfsIterative(vector<vector<int>>& graph, int start) {
    vector<bool> visited(graph.size(), false);
    stack<int> stk;
    
    stk.push(start);
    
    while(!stk.empty()) {
        int current = stk.top();
        stk.pop();
        
        if(!visited[current]) {
            visited[current] = true;
            cout << current << " ";
            
            // Add neighbors to stack
            for(int neighbor : graph[current]) {
                if(!visited[neighbor]) {
                    stk.push(neighbor);
                }
            }
        }
    }
}
```

## Performance Characteristics

| Container | Push/Pop | Memory | Use Case |
|-----------|----------|--------|----------|
| `deque` (default) | O(1) | Moderate | General purpose |
| `vector` | O(1) amortized | Compact | Memory-efficient |
| `list` | O(1) | Higher overhead | Guaranteed O(1) |

## Error Handling

### Basic Error Checking
```cpp
template<typename T>
bool safePop(stack<T>& stk, T& result) {
    if(stk.empty()) {
        return false;
    }
    result = stk.top();
    stk.pop();
    return true;
}

template<typename T>
bool safeTop(stack<T>& stk, T& result) {
    if(stk.empty()) {
        return false;
    }
    result = stk.top();
    return true;
}
```

### Safe Stack Wrapper
```cpp
#include <stdexcept>

template<typename T>
class SafeStack {
private:
    stack<T> stk;
    
public:
    void push(const T& value) {
        stk.push(value);
    }
    
    T pop() {
        if(stk.empty()) {
            throw runtime_error("Stack is empty - cannot pop");
        }
        T value = stk.top();
        stk.pop();
        return value;
    }
    
    const T& top() const {
        if(stk.empty()) {
            throw runtime_error("Stack is empty - no top element");
        }
        return stk.top();
    }
    
    bool empty() const { return stk.empty(); }
    size_t size() const { return stk.size(); }
};
```

## Best Practices

### ✅ Do:
- Always check `empty()` before calling `top()` or `pop()`
- Use appropriate underlying container for your use case
- Consider creating wrapper classes for error handling
- Use `const` references when possible to avoid unnecessary copies
- Use stack for algorithms that naturally follow LIFO pattern

### ❌ Don't:
- Call `top()` or `pop()` on empty stack (undefined behavior)
- Assume stacks are iterable like other containers
- Forget that `pop()` doesn't return the removed element
- Use stack when you need random access to elements
- Mix up LIFO (stack) and FIFO (queue) concepts

### Code Style Guidelines
```cpp
// Good: Clear variable names
stack<int> operatorStack;
stack<string> functionCallStack;

// Good: Check before operations
if (!stk.empty()) {
    int value = stk.top();
    stk.pop();
}

// Good: Use const when possible
void processStack(const stack<int>& stk) {
    stack<int> temp = stk; // Copy for processing
    // ... process temp
}

// Bad: No error checking
int value = stk.top(); // Could crash if empty
stk.pop();
```

## Key Concepts Summary

**LIFO Principle:** Last element pushed is the first element popped
```cpp
stk.push(1);  // Stack: [1]
stk.push(2);  // Stack: [1, 2]
stk.push(3);  // Stack: [1, 2, 3]
stk.pop();    // Removes 3, Stack: [1, 2]
```

**No Iterators:** Direct iteration not supported - must copy or destructively iterate

**Container Adapter:** Built on top of other containers (deque by default)

**Common Applications:**
- Expression parsing and evaluation
- Function call management
- Undo/Redo operations
- Depth-First Search algorithms
- Backtracking algorithms

**Memory Characteristics:**
- Automatic memory management
- RAII compliance
- Exception safety guarantees

---

**References:**
- [cppreference.com - std::stack](https://en.cppreference.com/w/cpp/container/stack)
- [C++ Standard Library Documentation](https://docs.microsoft.com/en-us/cpp/standard-library/)
