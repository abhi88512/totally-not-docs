# C++ Set (std::set) Documentation

**Sorted Unique Elements**

> An associative container that contains a sorted set of unique objects of type Key.

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
#include <set>

// Basic declaration
std::set<int> s;

// Initializer list (C++11)
std::set<int> s_list = {3, 1, 4, 1, 5, 9, 2, 6};

// Copy constructor
std::set<int> s_copy = s_list;
```

## Core Operations

| Operation | Syntax | Description | Time Complexity |
|-----------|--------|-------------|-----------------|
| **Insert** | `s.insert(value)` | Insert a unique element | O(log n) |
| **Erase** | `s.erase(value)` | Remove an element | O(log n) |
| **Find** | `s.find(value)` | Find an element | O(log n) |
| **Count** | `s.count(value)` | Check if an element exists | O(log n) |
| **Size** | `s.size()` | Get number of elements | O(1) |

## Basic Usage Example
```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> s;
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

- Iterator-based loops and range-based for loops are used to iterate over the sorted elements.

## Common Use Cases

- Storing a collection of unique items.
- Checking for the presence of an item in a collection.

## Performance Characteristics

- **Insertion, Deletion, Search**: O(log n).
- **Sorted**: Elements are always kept in sorted order.

## Best Practices

- Use `std::set` when you need to store unique elements and require them to be sorted.
- If you don't need sorting, `std::unordered_set` is generally faster.

---

**References:**
- [cppreference.com - std::set](https://en.cppreference.com/w/cpp/container/set)
- [C++ Standard Library Documentation](https://docs.microsoft.com/en-us/cpp/standard-library/)
