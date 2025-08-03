# C++ Map (std::map) Documentation

**Sorted Key-Value Pairs**

> An associative container that contains a sorted set of unique key-value pairs.

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
#include <map>
#include <string>

// Basic declaration
std::map<std::string, int> m;

// Initializer list (C++11)
std::map<std::string, int> m_list = {
    {"apple", 1},
    {"banana", 2},
    {"cherry", 3}
};

// Copy constructor
std::map<std::string, int> m_copy = m_list;
```

## Core Operations

| Operation | Syntax | Description | Time Complexity |
|-----------|--------|-------------|-----------------|
| **Insert** | `m.insert({key, value})` | Insert a key-value pair | O(log n) |
| **Access/Insert** | `m[key] = value` | Access or insert a key-value pair | O(log n) |
| **Erase** | `m.erase(key)` | Remove a key-value pair | O(log n) |
| **Find** | `m.find(key)` | Find a key-value pair | O(log n) |
| **Count** | `m.count(key)` | Check if a key exists | O(log n) |
| **Size** | `m.size()` | Get number of elements | O(1) |

## Basic Usage Example
```cpp
#include <iostream>
#include <map>
#include <string>

int main() {
    std::map<std::string, int> fruit_counts;
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

- Iterator-based loops and range-based for loops are used to iterate over the key-value pairs, sorted by key.

## Common Use Cases

- Storing a dictionary or a frequency map.
- When you need to associate a value with a unique key and require the keys to be sorted.

## Performance Characteristics

- **Insertion, Deletion, Search**: O(log n).
- **Sorted**: Elements are always kept in sorted order by key.

## Best Practices

- Use `std::map` when you need to store key-value pairs and require them to be sorted by key.
- If you don't need sorting, `std::unordered_map` is generally faster.
- Use `.at(key)` for access if you want bounds checking (it throws an exception for non-existent keys).

---

**References:**
- [cppreference.com - std::map](https://en.cppreference.com/w/cpp/container/map)
- [C++ Standard Library Documentation](https://docs.microsoft.com/en-us/cpp/standard-library/)
