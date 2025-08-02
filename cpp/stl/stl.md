# C++ Standard Template Library (STL) Documentation

**A comprehensive guide to C++ STL containers, algorithms, and utilities**

> The STL provides a set of common classes and interfaces that greatly extend the core C++ language.

## 📋 Table of Contents
- [STL Overview](#stl-overview)
- [Container Categories](#container-categories)
- [Container Quick Reference](#container-quick-reference)
- [Time Complexity Comparison](#time-complexity-comparison)
- [Container Selection Guide](#container-selection-guide)
- [Memory Usage Comparison](#memory-usage-comparison)
- [Common Usage Patterns](#common-usage-patterns)
- [Best Practices](#best-practices)

## STL Overview

The Standard Template Library consists of four main components:

### 1. **Containers**
Data structures that store collections of objects
- **Sequence Containers**: `vector`, `deque`, `list`, `array`, `forward_list`
- **Associative Containers**: `set`, `map`, `multiset`, `multimap`
- **Unordered Associative**: `unordered_set`, `unordered_map`, `unordered_multiset`, `unordered_multimap`
- **Container Adapters**: `stack`, `queue`, `priority_queue`

### 2. **Iterators**
Objects that point to elements in containers and provide navigation

### 3. **Algorithms**
Functions that perform operations on containers (sort, search, etc.)

### 4. **Function Objects**
Objects that can be called like functions (functors, lambdas)

## Container Categories

### Sequence Containers
```cpp
#include <vector>
#include <deque>
#include <list>
#include <array>

vector<int> vec = {1, 2, 3, 4, 5};        // Dynamic array
deque<int> dq = {1, 2, 3, 4, 5};          // Double-ended queue
list<int> lst = {1, 2, 3, 4, 5};          // Doubly linked list
array<int, 5> arr = {1, 2, 3, 4, 5};      // Fixed-size array
```

### Associative Containers
```cpp
#include <set>
#include <map>

set<int> s = {3, 1, 4, 1, 5};             // Unique sorted elements
map<string, int> m = {{"apple", 5}, {"banana", 3}};  // Key-value pairs
multiset<int> ms = {3, 1, 4, 1, 5};       // Allows duplicates
multimap<string, int> mm;                  // Multiple values per key
```

### Unordered Containers
```cpp
#include <unordered_set>
#include <unordered_map>

unordered_set<int> us = {3, 1, 4, 1, 5};  // Hash set
unordered_map<string, int> um = {{"apple", 5}};  // Hash map
```

### Container Adapters
```cpp
#include <stack>
#include <queue>

stack<int> stk;                            // LIFO
queue<int> q;                              // FIFO
priority_queue<int> pq;                    // Max heap (default)
priority_queue<int, vector<int>, greater<int>> min_pq;  // Min heap
```

## Container Quick Reference

| Container | Header | Access | Insert | Delete | Search | Sorted | Duplicates |
|-----------|--------|--------|--------|--------|---------|--------|------------|
| `vector` | `<vector>` | O(1) | O(1) amortized end | O(n) | O(n) | ❌ | ✅ |
| `deque` | `<deque>` | O(1) | O(1) both ends | O(1) both ends | O(n) | ❌ | ✅ |
| `list` | `<list>` | O(n) | O(1) anywhere | O(1) anywhere | O(n) | ❌ | ✅ |
| `set` | `<set>` | O(log n) | O(log n) | O(log n) | O(log n) | ✅ | ❌ |
| `map` | `<map>` | O(log n) | O(log n) | O(log n) | O(log n) | ✅ by key | ❌ keys |
| `unordered_set` | `<unordered_set>` | O(1) avg | O(1) avg | O(1) avg | O(1) avg | ❌ | ❌ |
| `unordered_map` | `<unordered_map>` | O(1) avg | O(1) avg | O(1) avg | O(1) avg | ❌ | ❌ keys |
| `stack` | `<stack>` | O(1) top only | O(1) top | O(1) top | ❌ | ❌ | ✅ |
| `queue` | `<queue>` | O(1) front/back | O(1) back | O(1) front | ❌ | ❌ | ✅ |
| `priority_queue` | `<queue>` | O(1) top | O(log n) | O(log n) top | ❌ | ✅ heap | ✅ |

## Time Complexity Comparison

### Common Operations

| Operation | vector | deque | list | set/map | unordered_set/map | stack | queue | priority_queue |
|-----------|--------|-------|------|---------|-------------------|-------|-------|----------------|
| **Insert at end** | O(1)* | O(1) | O(1) | O(log n) | O(1)* | O(1) | O(1) | O(log n) |
| **Insert at beginning** | O(n) | O(1) | O(1) | O(log n) | O(1)* | ❌ | ❌ | ❌ |
| **Insert at middle** | O(n) | O(n) | O(1) | O(log n) | O(1)* | ❌ | ❌ | ❌ |
| **Delete at end** | O(1) | O(1) | O(1) | O(log n) | O(1)* | O(1) | ❌ | O(log n) |
| **Delete at beginning** | O(n) | O(1) | O(1) | O(log n) | O(1)* | ❌ | O(1) | ❌ |
| **Random access** | O(1) | O(1) | O(n) | O(log n) | O(1)* | ❌ | ❌ | ❌ |
| **Search** | O(n) | O(n) | O(n) | O(log n) | O(1)* | ❌ | ❌ | ❌ |

*Amortized time complexity

### Space Complexity

| Container | Space per Element | Additional Overhead | Total Space |
|-----------|-------------------|-------------------|-------------|
| `vector` | sizeof(T) | ~24 bytes (capacity, size, data ptr) | O(n) |
| `deque` | sizeof(T) | ~40 bytes + block overhead | O(n) |
| `list` | sizeof(T) + 16 bytes | ~24 bytes (head, tail, size) | O(n) |
| `set/map` | sizeof(T) + 24 bytes | ~24 bytes (root, size, etc.) | O(n) |
| `unordered_set/map` | sizeof(T) + 8 bytes | ~56 bytes + bucket array | O(n) |

## Container Selection Guide

### Choose Based on Primary Operation

| Primary Need | Best Container | Alternative | Reason |
|--------------|----------------|-------------|---------|
| **Random access** | `vector` | `deque` | O(1) indexing |
| **Fast insertion/deletion at ends** | `deque` | `vector` | O(1) both ends |
| **Fast insertion/deletion anywhere** | `list` | `deque` | O(1) with iterator |
| **Sorted unique elements** | `set` | `vector` + sort | Automatic sorting |
| **Key-value mapping** | `map`/`unordered_map` | `vector<pair>` | O(1) or O(log n) lookup |
| **Fast lookup** | `unordered_set` | `set` | O(1) average |
| **LIFO operations** | `stack` | `vector` | Push/pop at end |
| **FIFO operations** | `queue` | `deque` | Push back, pop front |
| **Priority-based access** | `priority_queue` | `multiset` | Heap operations |

### Decision Tree

```
Do you need random access to elements?
├─ YES → Do you modify size frequently?
│  ├─ YES → vector (if mostly append) or deque (if both ends)
│  └─ NO → array (fixed size) or vector
│
└─ NO → Do you need fast search/lookup?
   ├─ YES → Do you need sorted order?
   │  ├─ YES → set/map
   │  └─ NO → unordered_set/unordered_map
   │
   └─ NO → What access pattern?
      ├─ LIFO → stack
      ├─ FIFO → queue
      ├─ Priority → priority_queue
      └─ Sequential → list
```

## Memory Usage Comparison

### Cache Performance

| Container | Cache Locality | Memory Layout | Performance Impact |
|-----------|----------------|---------------|-------------------|
| `vector` | Excellent | Contiguous | Best for iteration |
| `array` | Excellent | Contiguous | Best for fixed-size data |
| `deque` | Good | Block-based | Good compromise |
| `list` | Poor | Scattered nodes | Slow iteration |
| `set/map` | Poor | Tree nodes | Good for search, poor iteration |
| `unordered_*` | Fair | Hash buckets | Good for lookup |

### Memory Efficiency Examples

```cpp
// Most memory efficient for large datasets
vector<int> data;
data.reserve(1000000); // Pre-allocate to avoid reallocations

// Balanced memory and performance
deque<int> balanced_data;

// Memory overhead but fast operations
unordered_set<int> fast_lookup;

// High memory overhead but maintains order
set<int> ordered_unique;
```

## Common Usage Patterns

### Container Adapters Patterns

#### Stack Patterns
```cpp
// Pattern 1: Balanced parentheses checking
bool isBalanced(string s) {
    stack<char> stk;
    for (char c : s) {
        if (c == '(' || c == '[' || c == '{') {
            stk.push(c);
        } else {
            if (stk.empty()) return false;
            char top = stk.top();
            stk.pop();
            if ((c == ')' && top != '(') ||
                (c == ']' && top != '[') ||
                (c == '}' && top != '{')) {
                return false;
            }
        }
    }
    return stk.empty();
}

// Pattern 2: Monotonic stack for next greater element
vector<int> nextGreater(vector<int>& nums) {
    vector<int> result(nums.size(), -1);
    stack<int> stk;
    
    for (int i = 0; i < nums.size(); i++) {
        while (!stk.empty() && nums[i] > nums[stk.top()]) {
            result[stk.top()] = nums[i];
            stk.pop();
        }
        stk.push(i);
    }
    return result;
}
```

#### Queue Patterns
```cpp
// Pattern 1: Level-order processing
void levelOrder(TreeNode* root) {
    if (!root) return;
    queue<TreeNode*> q;
    q.push(root);
    
    while (!q.empty()) {
        int size = q.size();
        for (int i = 0; i < size; i++) {
            TreeNode* node = q.front();
            q.pop();
            
            cout << node->val << " ";
            
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        cout << endl; // New level
    }
}

// Pattern 2: Sliding window with deque
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    deque<int> dq; // Store indices
    vector<int> result;
    
    for (int i = 0; i < nums.size(); i++) {
        // Remove out of window
        while (!dq.empty() && dq.front() < i - k + 1) {
            dq.pop_front();
        }
        
        // Maintain decreasing order
        while (!dq.empty() && nums[dq.back()] < nums[i]) {
            dq.pop_back();
        }
        
        dq.push_back(i);
        
        if (i >= k - 1) {
            result.push_back(nums[dq.front()]);
        }
    }
    return result;
}
```

#### Priority Queue Patterns
```cpp
// Pattern 1: K largest elements using min heap
vector<int> kLargest(vector<int>& nums, int k) {
    priority_queue<int, vector<int>, greater<int>> minHeap;
    
    for (int num : nums) {
        minHeap.push(num);
        if (minHeap.size() > k) {
            minHeap.pop();
        }
    }
    
    vector<int> result;
    while (!minHeap.empty()) {
        result.push_back(minHeap.top());
        minHeap.pop();
    }
    return result;
}

// Pattern 2: Custom comparator
struct Task {
    int priority;
    string name;
};

struct TaskComparator {
    bool operator()(const Task& a, const Task& b) {
        return a.priority < b.priority; // Max heap by priority
    }
};

priority_queue<Task, vector<Task>, TaskComparator> taskQueue;
```

### Associative Container Patterns

```cpp
// Frequency counting
unordered_map<int, int> countFrequency(vector<int>& nums) {
    unordered_map<int, int> freq;
    for (int num : nums) {
        freq[num]++;
    }
    return freq;
}

// Group by key
map<string, vector<string>> groupAnagrams(vector<string>& strs) {
    map<string, vector<string>> groups;
    for (string& str : strs) {
        string key = str;
        sort(key.begin(), key.end());
        groups[key].push_back(str);
    }
    return groups;
}

// Range queries with set
set<int> data = {1, 3, 5, 7, 9, 11};
auto it = data.lower_bound(6); // First element >= 6
auto it2 = data.upper_bound(9); // First element > 9
```

## Best Practices

### 1. **Performance Optimization**
```cpp
// Reserve space when size is known
vector<int> vec;
vec.reserve(1000000); // Avoid reallocations

// Use emplace for in-place construction
priority_queue<pair<int, string>> pq;
pq.emplace(1, "hello"); // Better than push(make_pair(1, "hello"))

// Prefer move semantics
vector<string> source = {"a", "b", "c"};
vector<string> dest = std::move(source); // Move instead of copy
```

### 2. **Memory Management**
```cpp
// Shrink vector capacity
vector<int> vec(1000000);
vec.resize(10);
vector<int>(vec).swap(vec); // C++03 way
vec.shrink_to_fit();        // C++11 way

// Use appropriate container for memory efficiency
vector<bool> flags;         // Specialized for space efficiency
bitset<1000> bits;         // Even more space efficient for fixed size
```

### 3. **Iterator Best Practices**
```cpp
// Use auto for iterator types
auto it = map.find(key);
auto it2 = vec.begin();

// Range-based loops when possible
for (const auto& [key, value] : map) {
    // Process key-value pairs
}

// Prefer algorithms over manual loops
auto it = find(vec.begin(), vec.end(), target);
bool found = binary_search(sorted_vec.begin(), sorted_vec.end(), target);
```

### 4. **Common Mistakes to Avoid**
```cpp
// ❌ Wrong: Using vector for frequent front operations
vector<int> vec;
vec.insert(vec.begin(), value); // O(n)

// ✅ Right: Use deque for both-end operations
deque<int> dq;
dq.push_front(value); // O(1)

// ❌ Wrong: Forgetting to check bounds
if (stk.top() > 0) { /* may crash if empty */ }

// ✅ Right: Always check before access
if (!stk.empty() && stk.top() > 0) { /* safe */ }

// ❌ Wrong: Inefficient string concatenation in loops
string result;
for (string& s : strings) {
    result += s; // Inefficient for many strings
}

// ✅ Right: Use appropriate method
stringstream ss;
for (string& s : strings) {
    ss << s;
}
string result = ss.str();
```

### 5. **Template for Common Operations**
```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <queue>
#include <deque>
#include <set>
#include <map>
#include <unordered_set>
#include <unordered_map>
#include <algorithm>
using namespace std;

// Utility function for printing containers
template<typename T>
void print(const T& container) {
    for (const auto& elem : container) {
        cout << elem << " ";
    }
    cout << endl;
}

// Common operations template
class STLOperations {
public:
    // Vector operations
    static void vectorOps() {
        vector<int> vec = {1, 2, 3};
        vec.push_back(4);           // Add to end
        vec.pop_back();             // Remove from end
        sort(vec.begin(), vec.end()); // Sort
        auto it = lower_bound(vec.begin(), vec.end(), 2); // Binary search
    }
    
    // Map operations
    static void mapOps() {
        map<string, int> m;
        m["key"] = 42;              // Insert/update
        auto it = m.find("key");    // Find
        if (it != m.end()) {        // Check if found
            cout << it->second;     // Access value
        }
    }
    
    // Set operations
    static void setOps() {
        set<int> s = {3, 1, 4, 1, 5};
        s.insert(2);                // Insert
        s.erase(1);                 // Remove
        bool exists = s.count(3);   // Check existence
    }
};
```

---

## **Container-Specific Documentation:**

### Container Adapters
- [Stack Documentation](./stack.md)
- [Queue Documentation](./queue.md)
- [Priority Queue Documentation](./priority_queue.md)

### Sequence Containers
- [Vector Documentation](./vector.md)
- [Deque Documentation](./deque.md)
- [List Documentation](./list.md)

### Associative Containers
- [Set Documentation](./set.md)
- [Map Documentation](./map.md)

### Unordered Containers
- [Unordered Set Documentation](./unordered_set.md)
- [Unordered Map Documentation](./unordered_map.md)

### Algorithms
- [STL Algorithms Documentation](./algorithms.md)

**External References:**
- [cppreference.com](https://en.cppreference.com/w/cpp/container)
- [C++ STL Documentation](https://docs.microsoft.com/en-us/cpp/standard-library/)