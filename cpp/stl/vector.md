# C++ Vector (std::vector) Documentation

**Dynamic Contiguous Array**

> A sequence container that encapsulates dynamic size arrays.

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
#include <vector>

// Basic declaration
std::vector<int> vec;

// Initialization with size
std::vector<int> vec_sized(10); // 10 integers, value-initialized (to 0)

// Initialization with size and value
std::vector<int> vec_filled(10, 5); // 10 integers, all with value 5

// Initializer list (C++11)
std::vector<int> vec_list = {1, 2, 3, 4, 5};

// Copy constructor
std::vector<int> vec_copy = vec_list;
```

## Core Operations

| Operation | Syntax | Description | Time Complexity |
|-----------|--------|-------------|-----------------|
| **Push Back** | `vec.push_back(value)` | Add element to end | O(1) amortized |
| **Pop Back** | `vec.pop_back()` | Remove last element | O(1) |
| **Access** | `vec[i]`, `vec.at(i)` | Access element at index `i` | O(1) |
| **Size** | `vec.size()` | Get number of elements | O(1) |
| **Empty** | `vec.empty()` | Check if vector is empty | O(1) |
| **Clear** | `vec.clear()` | Remove all elements | O(n) |
| **Resize** | `vec.resize(new_size)` | Change the number of elements | O(n) |
| **Reserve**| `vec.reserve(n)` | Request a change in capacity | O(n) |


## Basic Usage Example
```cpp
#include <iostream>
#include <vector>
#include <algorithm> // For std::sort

int main() {
    std::vector<int> numbers;
    numbers.push_back(30);
    numbers.push_back(10);
    numbers.push_back(20);

    std::cout << "Vector elements: ";
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    std::sort(numbers.begin(), numbers.end());

    std::cout << "Sorted elements: ";
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

## Iteration Patterns

### Index-based Loop
```cpp
for (size_t i = 0; i < vec.size(); ++i) {
    std::cout << vec[i] << " ";
}
```

### Iterator-based Loop
```cpp
for (auto it = vec.begin(); it != vec.end(); ++it) {
    std::cout << *it << " ";
}
```

### Range-based For Loop (C++11)
```cpp
for (const auto& elem : vec) {
    std::cout << elem << " ";
}
```

## Common Use Cases

- Storing collections of elements where the size may change.
- Passing sequences of data to functions.
- As a building block for other data structures.

## Performance Characteristics

- **Insertion/Deletion at the end**: O(1) amortized.
- **Insertion/Deletion in the middle or beginning**: O(n).
- **Access**: O(1).
- **Cache-friendly**: Elements are stored contiguously in memory, which is good for performance.

## Error Handling

- `vec.at(i)` provides bounds-checked access and throws `std::out_of_range` if `i` is out of bounds.
- `vec[i]` does not perform bounds checking.

## Best Practices

- Use `reserve()` when the number of elements is known beforehand to avoid reallocations.
- Prefer `emplace_back()` over `push_back()` for objects to avoid extra copy/move operations.
- Pass vectors by `const&` to functions to avoid unnecessary copies.

---

**References:**
- [cppreference.com - std::vector](https://en.cppreference.com/w/cpp/container/vector)
- [C++ Standard Library Documentation](https://docs.microsoft.com/en-us/cpp/standard-library/)
