# C++ Unordered Map (std::unordered_map) Documentation

**Unordered Key-Value Pairs**

> An associative container that contains a set of unique key-value pairs. Search, insertion, and removal have average constant-time complexity.

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
#include <unordered_map>
#include <string>

// Basic declaration
std::unordered_map<std::string, int> m;

// Initializer list (C++11)
std::unordered_map<std::string, int> m_list = {
    {"apple", 1},
    {"banana", 2},
    {"cherry", 3}
};

// Copy constructor
std::unordered_map<std::string, int> m_copy = m_list;
```

## Core Operations

| Operation | Syntax | Description | Time Complexity |
|-----------|--------|-------------|-----------------|
| **Insert** | `m.insert({key, value})` | Insert a key-value pair | O(1) average |
| **Access/Insert** | `m[key] = value` | Access or insert a key-value pair | O(1) average |
| **Erase** | `m.erase(key)` | Remove a key-value pair | O(1) average |
| **Find** | `m.find(key)` | Find a key-value pair | O(1) average |
| **Count** | `m.count(key)` | Check if a key exists | O(1) average |
| **Size** | `m.size()` | Get number of elements | O(1) |

## Basic Usage Example
```cpp
#include <iostream>
#include <unordered_map>
#include <string>

int main() {
    std::unordered_map<std::string, int> fruit_counts;
    fruit_counts["apple"] = 5;
    fruit_counts["banana"] = 2;
    fruit_counts["apple"] = 3; // Overwrites the previous value

    for (const auto& pair : fruit_counts) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }

    return 0;
}
```

## Iteration Patterns

- Iterator-based loops and range-based for loops are used to iterate over the key-value pairs in no particular order.

## Common Use Cases

- Storing a dictionary or a frequency map when order is not important.
- Fast lookups of values based on a key.

## Performance Characteristics

- **Insertion, Deletion, Search**: O(1) on average, O(n) in the worst case.
- **Unordered**: Elements are not stored in any particular order.

## Best Practices

- Use `std::unordered_map` when you need to store key-value pairs and do not require them to be sorted by key. It is generally faster than `std::map`.
- Use `.at(key)` for access if you want bounds checking (it throws an exception for non-existent keys).

---

**References:**
- [cppreference.com - std::unordered_map](https://en.cppreference.com/w/cpp/container/unordered_map)
- [C++ Standard Library Documentation](https://docs.microsoft.com/en-us/cpp/standard-library/)
