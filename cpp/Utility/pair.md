# C++ Pair (std::pair) Documentation

**A pair of values**

> `std::pair` is a struct template that provides a way to store two heterogeneous objects as a single unit.

## 📋 Table of Contents
- [Declaration & Initialization](#declaration--initialization)
- [Accessing Elements](#accessing-elements)
- [Relational Operators](#relational-operators)
- [std::make_pair](#stdmake_pair)
- [Structured Binding (C++17)](#structured-binding-c17)
- [Common Use Cases](#common-use-cases)
- [Best Practices](#best-practices)

## Declaration & Initialization
```cpp
#include <utility> // Required for std::pair
#include <string>

// Basic declaration
std::pair<int, std::string> p1;

// Initialization with values
std::pair<int, std::string> p2(1, "hello");

// Uniform initialization (C++11)
std::pair<int, std::string> p3{2, "world"};

// Copy initialization
std::pair<int, std::string> p4 = p2;

// Using std::make_pair
auto p5 = std::make_pair(3, "foo");
```

## Accessing Elements

Elements of a `std::pair` are accessed through its public members `first` and `second`.

```cpp
#include <iostream>
#include <utility>
#include <string>

int main() {
    std::pair<int, std::string> p(10, "test");

    std::cout << "First element: " << p.first << std::endl;   // 10
    std::cout << "Second element: " << p.second << std::endl; // "test"

    // Modifying elements
    p.first = 20;
    p.second = "new test";

    std::cout << "Modified first element: " << p.first << std::endl;   // 20
    std::cout << "Modified second element: " << p.second << std::endl; // "new test"

    return 0;
}
```

## Relational Operators

`std::pair` supports relational operators (`==`, `!=`, `<`, `>`, `<=`, `>=`). The comparison is done lexicographically.

```cpp
#include <iostream>
#include <utility>

int main() {
    std::pair<int, int> p1(1, 2);
    std::pair<int, int> p2(1, 3);
    std::pair<int, int> p3(2, 1);

    if (p1 < p2) {
        std::cout << "p1 is less than p2" << std::endl;
    }
    if (p3 > p2) {
        std::cout << "p3 is greater than p2" << std::endl;
    }
    if (p1 == std::make_pair(1, 2)) {
        std::cout << "p1 is equal to (1, 2)" << std::endl;
    }

    return 0;
}
```

## std::make_pair

`std::make_pair` is a helper function that creates a `std::pair` object, deducing the types from the arguments.

```cpp
auto p = std::make_pair(10, "hello"); // p is of type std::pair<int, const char*>
```

## Structured Binding (C++17)

Since C++17, you can use structured bindings to unpack the elements of a pair into separate variables.

```cpp
#include <iostream>
#include <utility>
#include <string>

int main() {
    std::pair<int, std::string> p(1, "example");

    auto [id, name] = p;

    std::cout << "ID: " << id << ", Name: " << name << std::endl;

    return 0;
}
```

## Common Use Cases

- **Returning multiple values from a function**.
- **As the `value_type` in associative containers** like `std::map` and `std::unordered_map`.
- **Storing a key-value association** in various algorithms.

## Best Practices

- Prefer `std::make_pair` for creating pairs to leverage type deduction.
- Use structured bindings (C++17 and later) for cleaner and more readable code when accessing pair elements.
- When used as a return type for a function, consider if a more descriptive `struct` or `class` would be more appropriate for clarity, especially if the pair represents more than just a simple key-value relationship.

---

**References:**
- [cppreference.com - std::pair](https://en.cppreference.com/w/cpp/utility/pair)
- [C++ Standard Library Documentation](https://docs.microsoft.com/en-us/cpp/standard-library/)
