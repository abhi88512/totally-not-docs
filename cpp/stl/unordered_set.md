# C++ Unordered Set (std::unordered_set) Documentation

**Unordered Unique Elements**

> An associative container that contains a set of unique objects of type Key. Search, insertion, and removal have average constant-time complexity.

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
#include <unordered_set>

// Basic declaration
std::unordered_set<int> s;

// Initializer list (C++11)
std::unordered_set<int> s_list = {3, 1, 4, 1, 5, 9, 2, 6};

// Copy constructor
std::unordered_set<int> s_copy = s_list;
```

## Core Operations

| Operation | Syntax | Description | Time Complexity |
|-----------|--------|-------------|-----------------|
| **Insert** | `s.insert(value)` | Insert a unique element | O(1) average |
| **Erase** | `s.erase(value)` | Remove an element | O(1) average |
| **Find** | `s.find(value)` | Find an element | O(1) average |
| **Count** | `s.count(value)` | Check if an element exists | O(1) average |
| **Size** | `s.size()` | Get number of elements | O(1) |

## Basic Usage Example
```cpp
#include <iostream>
#include <unordered_set>

int main() {
    std::unordered_set<int> s;
    s.insert(30);
    s.insert(10);
    s.insert(20);
    s.insert(10); // Duplicate, will be ignored

    for (int n : s) {
        std::cout << n << " ";
    }
    std::cout << std::endl;

    if (s.count(20)) {
        std::cout << "20 is in the set." << std::endl;
    }

    return 0;
}
```

## Iteration Patterns

- Iterator-based loops and range-based for loops are used to iterate over the elements in no particular order.

## Common Use Cases

- Storing a collection of unique items when order is not important.
- Fast checking for the presence of an item in a collection.

## Performance Characteristics

- **Insertion, Deletion, Search**: O(1) on average, O(n) in the worst case.
- **Unordered**: Elements are not stored in any particular order.

## Best Practices

- Use `std::unordered_set` when you need to store unique elements and do not require them to be sorted. It is generally faster than `std::set`.

---

**References:**
- [cppreference.com - std::unordered_set](https://en.cppreference.com/w/cpp/container/unordered_set)
- [C++ Standard Library Documentation](https://docs.microsoft.com/en-us/cpp/standard-library/)
