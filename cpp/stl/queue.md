# C++ Queue (std::queue) Documentation

**First In, First Out (FIFO)**

> A container adapter that provides queue functionality - elements are inserted at the back and removed from the front.

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
#include <queue>
#include <list>   // Can be used as an underlying container
#include <deque>  // Default underlying container

// Basic declaration
std::queue<int> q;

// With specific underlying container
std::queue<int, std::list<int>> q_list; // Using list as underlying container

// Template with custom types
std::queue<std::string> str_queue;
std::queue<std::pair<int, std::string>> pair_queue;
```

## Core Operations

| Operation | Syntax | Description | Time Complexity |
|-----------|--------|-------------|-----------------|
| **Push** | `q.push(value)` | Add element to back | O(1) |
| **Pop** | `q.pop()` | Remove front element | O(1) |
| **Front** | `q.front()` | Access front element | O(1) |
| **Back** | `q.back()` | Access back element | O(1) |
| **Size** | `q.size()` | Get number of elements | O(1) |
| **Empty** | `q.empty()` | Check if queue is empty | O(1) |

### Detailed Operation Examples
```cpp
std::queue<int> q;

// Push operations
q.push(10);                          // Queue: [10]
q.push(20);                          // Queue: [10, 20]
q.push(30);                          // Queue: [10, 20, 30]

// Access operations
int front_element = q.front();         // front_element = 10
int back_element = q.back();           // back_element = 30
size_t queue_size = q.size();          // queue_size = 3
bool is_empty = q.empty();             // is_empty = false

// Pop operations
q.pop();                               // Queue: [20, 30]
std::cout << "Front after pop: " << q.front() << std::endl; // 20
```

## Basic Usage Example
```cpp
#include <iostream>
#include <queue>

int main() {
    std::queue<std::string> tasks;
    
    // Adding tasks
    tasks.push("Task 1");
    tasks.push("Task 2");
    tasks.push("Task 3");
    
    std::cout << "Processing tasks (FIFO order):
";
    while (!tasks.empty()) {
        std::cout << "Processing: " << tasks.front() << std::endl;
        tasks.pop();
    }
    
    return 0;
}
```

## Iteration Patterns

> ⚠️ **Important:** Queues, like stacks, do not support iterators. The only way to access all elements is by popping them.

### Destructive Iteration
```cpp
// WARNING: This destroys the original queue
while(!q.empty()) {
    std::cout << q.front() << " "; // Access front element
    q.pop();                       // Remove front element
}
// Output: 10 20 30 (FIFO order)
// Queue is now empty!
```

### Non-Destructive Iteration
```cpp
// Safe method: Copy queue first
std::queue<int> temp = q;            // Create copy
while(!temp.empty()) {
    std::cout << temp.front() << " "; // Access front of copy
    temp.pop();                      // Remove from copy only
}
// Original queue remains unchanged
```

## Common Use Cases

### Breadth-First Search (BFS)
```cpp
void bfs(const std::vector<std::vector<int>>& graph, int start) {
    std::vector<bool> visited(graph.size(), false);
    std::queue<int> q;
    
    q.push(start);
    visited[start] = true;
    
    while(!q.empty()) {
        int current = q.front();
        q.pop();
        
        std::cout << current << " ";
        
        for(int neighbor : graph[current]) {
            if(!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}
```

### Resource Sharing / Task Scheduling
```cpp
// Simulate a printer queue
std::queue<std::string> printer_jobs;
printer_jobs.push("DocumentA.pdf");
printer_jobs.push("ImageB.png");
printer_jobs.push("ReportC.docx");

// Process jobs in the order they were received
while(!printer_jobs.empty()) {
    std::cout << "Printing: " << printer_jobs.front() << std::endl;
    printer_jobs.pop();
}
```

## Performance Characteristics

| Underlying Container | Push/Pop | Memory | Use Case |
|-----------|----------|--------|----------|
| `deque` (default) | O(1) | Moderate | General purpose, good balance |
| `list` | O(1) | Higher overhead | Guaranteed O(1), better for very large elements |

## Error Handling

### Basic Error Checking
```cpp
template<typename T>
bool safeFront(std::queue<T>& q, T& result) {
    if(q.empty()) {
        return false;
    }
    result = q.front();
    return true;
}

template<typename T>
bool safePop(std::queue<T>& q) {
    if(q.empty()) {
        return false;
    }
    q.pop();
    return true;
}
```

### Safe Queue Wrapper
```cpp
#include <stdexcept>

template<typename T>
class SafeQueue {
private:
    std::queue<T> q;
    
public:
    void push(const T& value) {
        q.push(value);
    }
    
    T pop() {
        if(q.empty()) {
            throw std::runtime_error("Queue is empty - cannot pop");
        }
        T value = q.front();
        q.pop();
        return value;
    }
    
    const T& front() const {
        if(q.empty()) {
            throw std::runtime_error("Queue is empty - no front element");
        }
        return q.front();
    }
    
    bool empty() const { return q.empty(); }
    size_t size() const { return q.size(); }
};
```

## Best Practices

### ✅ Do:
- Always check `empty()` before calling `front()`, `back()`, or `pop()`.
- Use `std::queue` for problems that naturally follow a FIFO pattern.
- Choose the underlying container (`deque` or `list`) based on performance needs.

### ❌ Don't:
- Call `front()`, `back()`, or `pop()` on an empty queue (undefined behavior).
- Assume queues are directly iterable.
- Use a queue when you need random access or LIFO behavior.

---

**References:**
- [cppreference.com - std::queue](https://en.cppreference.com/w/cpp/container/queue)
- [C++ Standard Library Documentation](https://docs.microsoft.com/en-us/cpp/standard-library/)