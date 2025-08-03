# C++ List (std::list) Documentation

**Doubly-Linked List**

> A sequence container that allows constant time insert and erase operations anywhere within the sequence.

## 📋 Table of Contents
- [Declaration & Initialization](#declaration--initialization)
- [Core Operations](#core-operations)
- [Basic Usage Example](#basic-usage-example)
- [Iteration Patterns](#iteration-patterns)
- [Common Use Cases](#common-use-cases)
- [Performance Characteristics](#performance-characteristics)
- [Best Practices](#best-practices)

## Declaration & Initialization
```cpp
#include <list>

// Basic declaration
std::list<int> l;

// Initialization with size
std::list<int> l_sized(10); // 10 integers, value-initialized (to 0)

// Initialization with size and value
std::list<int> l_filled(10, 5); // 10 integers, all with value 5

// Initializer list (C++11)
std::list<int> l_list = {1, 2, 3, 4, 5};

// Copy constructor
std::list<int> l_copy = l_list;
```

## Core Operations

| Operation | Syntax | Description | Time Complexity |
|-----------|--------|-------------|-----------------|
| **Push Back** | `l.push_back(value)` | Add element to end | O(1) |
| **Pop Back** | `l.pop_back()` | Remove last element | O(1) |
| **Push Front**| `l.push_front(value)`| Add element to beginning | O(1) |
| **Pop Front** | `l.pop_front()` | Remove first element | O(1) |
| **Insert** | `l.insert(it, value)` | Insert element before iterator `it` | O(1) |
| **Erase** | `l.erase(it)` | Remove element at iterator `it` | O(1) |
| **Size** | `l.size()` | Get number of elements | O(1) |

## Basic Usage Example
```cpp
#include <iostream>
#include <list>

int main() {
    std::list<int> l = {1, 2, 3};
    l.push_front(0);
    l.push_back(4);

    for (int n : l) {
        std::cout << n << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

## Iteration Patterns

- Iterator-based loops and range-based for loops are common.
- Index-based loops are not possible as `std::list` does not support random access with `[]` or `.at()`.

## Common Use Cases

- When frequent insertions and deletions are needed in the middle of the sequence.

## Performance Characteristics

- **Insertion/Deletion**: O(1) anywhere in the list (once the position is known).
- **Access**: O(n) - no random access.
- **Not cache-friendly**: Elements are not stored contiguously.

## Best Practices

- Use `std::list` when you have a lot of insertions and deletions in the middle of the container.
- For simple storage and iteration, `std::vector` is usually better.

---

**References:**
- [cppreference.com - std::list](https://en.cppreference.com/w/cpp/container/list)
- [C++ Standard Library Documentation](https://docs.microsoft.com/en-us/cpp/standard-library/)
