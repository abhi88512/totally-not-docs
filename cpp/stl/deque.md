# C++ Deque (std::deque) Documentation

**Double-Ended Queue**

> A sequence container that allows fast insertion and deletion at both its beginning and its end.

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
#include <deque>

// Basic declaration
std::deque<int> dq;

// Initialization with size
std::deque<int> dq_sized(10); // 10 integers, value-initialized (to 0)

// Initialization with size and value
std::deque<int> dq_filled(10, 5); // 10 integers, all with value 5

// Initializer list (C++11)
std::deque<int> dq_list = {1, 2, 3, 4, 5};

// Copy constructor
std::deque<int> dq_copy = dq_list;
```

## Core Operations

| Operation | Syntax | Description | Time Complexity |
|-----------|--------|-------------|-----------------|
| **Push Back** | `dq.push_back(value)` | Add element to end | O(1) |
| **Pop Back** | `dq.pop_back()` | Remove last element | O(1) |
| **Push Front** | `dq.push_front(value)` | Add element to beginning | O(1) |
| **Pop Front** | `dq.pop_front()` | Remove first element | O(1) |
| **Access** | `dq[i]`, `dq.at(i)` | Access element at index `i` | O(1) |
| **Size** | `dq.size()` | Get number of elements | O(1) |
| **Empty** | `dq.empty()` | Check if deque is empty | O(1) |

## Basic Usage Example
```cpp
#include <iostream>
#include <deque>

int main() {
    std::deque<int> d;
    d.push_back(10);
    d.push_front(20);
    d.push_back(30);
    d.push_front(40);

    std::cout << "Deque elements: ";
    for (int n : d) {
        std::cout << n << " ";
    }
    std::cout << std::endl;

    d.pop_front();
    d.pop_back();

    std::cout << "After pops: ";
    for (int n : d) {
        std::cout << n << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

## Iteration Patterns

- Same as `std::vector` (index-based, iterator-based, range-based for loops).

## Common Use Cases

- Implementing a queue or a double-ended queue.
- When insertions and deletions are needed at both ends.

## Performance Characteristics

- **Insertion/Deletion at ends**: O(1).
- **Insertion/Deletion in the middle**: O(n).
- **Access**: O(1).
- **Not cache-friendly**: Unlike `std::vector`, `std::deque` is not stored in a contiguous block of memory.

## Error Handling

- `dq.at(i)` provides bounds-checked access and throws `std::out_of_range` if `i` is out of bounds.
- `dq[i]` does not perform bounds checking.

## Best Practices

- Use `std::deque` when you need to perform insertions and deletions at both the front and back.
- If you only need to add/remove from the back, `std::vector` is generally more efficient.

---

**References:**
- [cppreference.com - std::deque](https://en.cppreference.com/w/cpp/container/deque)
- [C++ Standard Library Documentation](https://docs.microsoft.com/en-us/cpp/standard-library/)
