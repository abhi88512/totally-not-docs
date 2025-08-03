# C++ Priority Queue (std::priority_queue) Documentation

**Highest Priority Element First**

> A container adapter that provides priority queue functionality. Elements are ordered by priority, with the highest priority element always accessible at the top.

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
#include <queue> // For std::priority_queue
#include <vector>
#include <functional> // For std::greater

// Max-heap (default, largest element has highest priority)
std::priority_queue<int> pq_max;

// Min-heap (smallest element has highest priority)
std::priority_queue<int, std::vector<int>, std::greater<int>> pq_min;

// With a custom comparator for a user-defined type
struct Task {
    int priority;
    std::string name;
};

struct CompareTasks {
    bool operator()(const Task& a, const Task& b) {
        // Max-heap based on priority value
        return a.priority < b.priority;
    }
};
std::priority_queue<Task, std::vector<Task>, CompareTasks> task_queue;
```

## Core Operations

| Operation | Syntax | Description | Time Complexity |
|-----------|--------|-------------|-----------------|
| **Push** | `pq.push(value)` | Add element to the queue | O(log n) |
| **Pop** | `pq.pop()` | Remove the top element | O(log n) |
| **Top** | `pq.top()` | Access the top element | O(1) |
| **Size** | `pq.size()` | Get number of elements | O(1) |
| **Empty** | `pq.empty()` | Check if queue is empty | O(1) |

## Basic Usage Example
```cpp
#include <iostream>
#include <queue>
#include <string>

int main() {
    // By default, std::priority_queue is a max-heap
    std::priority_queue<int> pq;
    
    pq.push(10);
    pq.push(50);
    pq.push(20);
    
    std::cout << "Processing elements (max-heap order):" << std::endl;
    while (!pq.empty()) {
        std::cout << "Top: " << pq.top() << ", Size: " << pq.size() << std::endl;
        pq.pop();
    }
    
    return 0;
}
```

## Iteration Patterns

> ⚠️ **Important:** Like `std::stack` and `std::queue`, `std::priority_queue` is a container adapter and does not provide iterators. Accessing all elements requires destructively popping them.

### Destructive Iteration
```cpp
// This process empties the original priority queue
std::cout << "Priority queue elements: ";
while(!pq.empty()) {
    std::cout << pq.top() << " ";
    pq.pop();
}
std::cout << std::endl;
// pq is now empty
```

### Non-Destructive Iteration (using a copy)
```cpp
// Create a copy to preserve the original
std::priority_queue<int> temp = pq;
std::cout << "Priority queue elements (non-destructive): ";
while(!temp.empty()) {
    std::cout << temp.top() << " ";
    temp.pop();
}
std::cout << std::endl;
// pq remains unchanged
```

## Common Use Cases

- **Graph Algorithms**: Essential in Dijkstra's shortest path and Prim's minimum spanning tree algorithms.
- **Event-Driven Simulation**: Managing events in a simulation, processing the one with the highest priority next.
- **Task Scheduling**: Scheduling tasks based on priority levels.
- **Finding Kth Largest/Smallest Element**: Efficiently finding the Kth element without a full sort.

## Performance Characteristics

- **Insertion (`push`)**: O(log n) due to the heap property maintenance.
- **Deletion (`pop`)**: O(log n) for the same reason.
- **Access (`top`)**: O(1) as the highest priority element is always at the root of the heap.
- **Memory**: Uses `std::vector` by default, which is cache-friendly and memory-efficient.

## Error Handling

- Calling `pq.top()` or `pq.pop()` on an empty priority queue results in **undefined behavior**.
- Always check if the priority queue is empty using `pq.empty()` before access.
```cpp
if (!pq.empty()) {
    // It's safe to call pq.top() and pq.pop()
    int highest_priority_element = pq.top();
    pq.pop();
}
```

## Best Practices

- Use `std::priority_queue` when you need efficient access to the highest (or lowest) priority element.
- For custom types, provide a strict weak ordering via a custom comparator or by overloading `operator<`.
- The default underlying container (`std::vector`) and comparator (`std::less`) are suitable for most max-heap use cases.
- Do not use `std::priority_queue` if you need to iterate over elements or access elements other than the top one.

---

**References:**
- [cppreference.com - std::priority_queue](https://en.cppreference.com/w/cpp/container/priority_queue)
- [C++ Standard Library Documentation](https://docs.microsoft.com/en-us/cpp/standard-library/)
