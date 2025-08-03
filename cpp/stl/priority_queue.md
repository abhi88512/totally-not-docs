
````markdown
# C++ Priority Queue (std::priority_queue) Documentation

**Highest Priority First (Max-Heap by default)**

> A container adapter that provides priority queue functionality - elements are ordered by priority, with the highest priority element always accessible at the top. It uses a heap data structure internally to maintain this order.

## Declaration & Initialization
```cpp
#include <queue>    // Required for std::priority_queue
#include <vector>   // Default underlying container for std::priority_queue
#include <functional> // Required for std::greater, std::less (for custom comparators)

// Basic declaration (max-heap by default - largest element has highest priority)
std::priority_queue<int> pq_max;

// Min-heap declaration (smallest element has highest priority)
// Syntax: priority_queue<Type, Container, Comparator>
std::priority_queue<int, std::vector<int>, std::greater<int>> pq_min;

// With custom types and custom comparator struct
struct Task {
    std::string name;
    int priority; // Higher value means higher priority
};

// Custom comparator for max-heap (Task with highest priority value is top)
struct CompareTasks {
    bool operator()(const Task& a, const Task& b) {
        return a.priority < b.priority; // 'a' has lower priority than 'b' if true (for max-heap)
    }
};
std::priority_queue<Task, std::vector<Task>, CompareTasks> task_pq;

// Initialize with elements from another container (C++11 onwards)
std::vector<int> v = {30, 10, 50, 20};
std::priority_queue<int> pq_init(v.begin(), v.end()); // pq_init contains {50, 30, 20, 10}
````

## Core Operations

| Operation | Syntax | Description | Time Complexity |
|-----------|--------|-------------|-----------------|
| **Push** | `pq.push(value)` | Add element to the queue (maintains heap property) | O($\\log N$) |
| **Pop** | `pq.pop()` | Remove the top (highest priority) element | O($\\log N$) |
| **Top** | `pq.top()` | Access the top (highest priority) element | O(1) |
| **Size** | `pq.size()` | Get number of elements | O(1) |
| **Empty** | `pq.empty()` | Check if queue is empty | O(1) |

### Detailed Operation Examples

```cpp
#include <iostream>
#include <queue>
#include <vector>
#include <functional> // For std::greater

void demonstratePriorityQueueOps() {
    std::priority_queue<int> pq; // Default max-heap

    // Push operations
    pq.push(10); // PQ: [10]
    pq.push(30); // PQ: [30, 10] (log N cost)
    pq.push(20); // PQ: [30, 10, 20] (log N cost)
    pq.push(50); // PQ: [50, 30, 20, 10] (log N cost)

    // Access operations
    int top_element = pq.top(); // top_element = 50 (O(1) cost)
    size_t pq_size = pq.size(); // pq_size = 4
    bool is_empty = pq.empty(); // is_empty = false

    std::cout << "Top element: " << top_element << "\n";
    std::cout << "Priority Queue size: " << pq_size << ", Is empty: " << is_empty << "\n";

    // Pop operations (removes 50)
    pq.pop(); // PQ: [30, 20, 10] (log N cost)
    std::cout << "Top after pop: " << pq.top() << "\n"; // 30
    
    // Demonstrate min-heap
    std::priority_queue<int, std::vector<int>, std::greater<int>> min_pq;
    min_pq.push(10); min_pq.push(30); min_pq.push(20);
    std::cout << "Min-heap top: " << min_pq.top() << "\n"; // 10
}

int main() {
    demonstratePriorityQueueOps();
    return 0;
}
```

## Basic Usage Example

```cpp
#include <iostream>
#include <queue>
#include <vector>
#include <functional> // For std::greater
using namespace std; // Using namespace std as in stack example

int main() {
    // Max-heap: tasks with higher priority numbers are processed first
    priority_queue<pair<int, string>> urgentTasks; // pair sorts by first element by default

    urgentTasks.push({5, "Emergency Fix"});
    urgentTasks.push({3, "Regular Bug Report"});
    urgentTasks.push({10, "Critical System Alert"});
    urgentTasks.push({1, "Minor UI Tweak"});
    
    cout << "Processing urgent tasks (highest priority first):\n";
    while (!urgentTasks.empty()) {
        pair<int, string> currentTask = urgentTasks.top();
        urgentTasks.pop();
        cout << "Priority: " << currentTask.first << ", Task: " << currentTask.second << endl;
    }

    cout << "\n";

    // Min-heap: tasks with lower priority numbers are processed first
    priority_queue<int, vector<int>, greater<int>> processOrder; // Used for min-heap

    processOrder.push(3);
    processOrder.push(1);
    processOrder.push(5);
    processOrder.push(2);

    cout << "Processing numbers (smallest first):\n";
    while(!processOrder.empty()){
        cout << processOrder.top() << " ";
        processOrder.pop();
    }
    cout << endl; // Output: 1 2 3 5

    return 0;
}
```

## Iteration Patterns

> ⚠️ **Important:** Priority queues, like `std::stack` and `std::queue`, are container adapters and do not expose iterators to their underlying elements. Elements can only be accessed via `top()` and removed via `pop()`. Iterating through a priority queue is inherently destructive.

### Destructive Iteration

```cpp
// WARNING: This destroys the original priority queue
#include <iostream>
#include <queue>

void destructiveIteratePQ(std::priority_queue<int> pq) { // Pass by value for a copy
    std::cout << "Priority Queue elements (top to bottom, destructive): ";
    while (!pq.empty()) {
        std::cout << pq.top() << " "; // Access top element
        pq.pop();                     // Remove top element
    }
    std::cout << "\n";
}

int main() {
    std::priority_queue<int> myPQ;
    myPQ.push(10); myPQ.push(30); myPQ.push(20);
    destructiveIteratePQ(myPQ); // Output: 30 20 10 (for max-heap)
    // myPQ is still {10,30,20} if passed by value, but empty if passed by reference.
    return 0;
}
```

### Non-Destructive Iteration (via Copy)

```cpp
// Safe method: Copy priority queue first
#include <iostream>
#include <queue>

void nonDestructiveIteratePQ(std::priority_queue<int> original_pq) { // Pass by value to get a copy
    std::priority_queue<int> temp_pq = original_pq; // Explicitly copy if original_pq was passed by reference
    
    std::cout << "Priority Queue elements (top to bottom, non-destructive): ";
    while(!temp_pq.empty()) {
        std::cout << temp_pq.top() << " "; // Access top of copy
        temp_pq.pop();                      // Remove from copy only
    }
    std::cout << "\n";
    // Original priority queue remains unchanged
}

int main() {
    std::priority_queue<int> myPQ;
    myPQ.push(10); myPQ.push(30); myPQ.push(20);
    nonDestructiveIteratePQ(myPQ); // Output: 30 20 10
    std::cout << "Original PQ size after non-destructive iteration: " << myPQ.size() << "\n"; // Still 3
    return 0;
}
```

## Common Use Cases

### Dijkstra's Algorithm / Prim's Algorithm (Graph Algorithms)

```cpp
// Conceptual use for Dijkstra's shortest path
#include <queue>
#include <vector>
#include <utility> // For std::pair

// pair: {distance, vertex}
// std::priority_queue by default is a max-heap, so we store negative distance
// to simulate a min-heap for shortest path (smallest distance has highest priority).
std::priority_queue<std::pair<int, int>> pq_dijkstra; 

// Or, use custom comparator for min-heap
// std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int>>, std::greater<std::pair<int, int>>> pq_dijkstra;

// pq_dijkstra.push({0, start_node}); // Push starting node with distance 0

// Inside loop:
// auto [dist, u] = pq_dijkstra.top(); pq_dijkstra.pop();
// if (dist > distances[u]) continue; // Already found shorter path

// For each neighbor v:
// if (new_dist < distances[v]) {
//    distances[v] = new_dist;
//    pq_dijkstra.push({-new_dist, v}); // For max-heap simulation
// }
```

### Huffman Coding

```cpp
// Conceptual use for building Huffman tree
#include <queue>
#include <map>
#include <string>

struct Node {
    char data;
    int frequency;
    Node *left, *right;

    // Constructor, etc.
};

struct CompareNodes {
    bool operator()(Node* a, Node* b) {
        return a->frequency > b->frequency; // Min-heap based on frequency
    }
};

std::priority_queue<Node*, std::vector<Node*>, CompareNodes> huffman_tree_builder;

// Insert leaf nodes:
// for (auto const& [char_val, freq] : frequencies) {
//     huffman_tree_builder.push(new Node(char_val, freq));
// }

// Build tree:
// while (huffman_tree_builder.size() > 1) {
//     Node *left = huffman_tree_builder.top(); huffman_tree_builder.pop();
//     Node *right = huffman_tree_builder.top(); huffman_tree_builder.pop();
//     Node *newNode = new Node('$', left->frequency + right->frequency, left, right);
//     huffman_tree_builder.push(newNode);
// }
// Node* root = huffman_tree_builder.top();
```

### K-th Largest/Smallest Element Problems

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <functional> // For std::greater

// Find Kth largest element using a min-heap
int findKthLargest(std::vector<int>& nums, int k) {
    std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap;

    for (int num : nums) {
        minHeap.push(num);
        if (minHeap.size() > k) {
            minHeap.pop(); // Keep only K largest elements
        }
    }
    return minHeap.top(); // The Kth largest is at the top of the min-heap
}

// Find Kth smallest element using a max-heap
int findKthSmallest(std::vector<int>& nums, int k) {
    std::priority_queue<int> maxHeap;

    for (int num : nums) {
        maxHeap.push(num);
        if (maxHeap.size() > k) {
            maxHeap.pop(); // Keep only K smallest elements
        }
    }
    return maxHeap.top(); // The Kth smallest is at the top of the max-heap
}

/*
int main() {
    std::vector<int> nums = {3,2,1,5,6,4};
    std::cout << "Kth largest (2nd): " << findKthLargest(nums, 2) << "\n"; // Output: 5
    std::cout << "Kth smallest (2nd): " << findKthSmallest(nums, 2) << "\n"; // Output: 2
    return 0;
}
*/
```

## Performance Characteristics

| Underlying Container | Push (`O(log N)`) | Pop (`O(log N)`) | Top (`O(1)`) | Memory Efficiency | Notes |
|----------------------|--------------------|-------------------|----------------|-------------------|-------|
| `std::vector` (Default) | ✅ Fast heap ops | ✅ Fast heap ops | ✅ Direct access | Compact | Optimal choice for heap-based operations. |

**Note**: `std::priority_queue` is designed to work with containers that provide random access iterators and `push_back`/`pop_back` operations, making `std::vector` the natural and default underlying container. Its internal implementation relies on `std::make_heap`, `std::push_heap`, and `std::pop_heap` algorithms.

## Error Handling

### Basic Error Checking

```cpp
#include <iostream>
#include <queue>

template<typename T, typename Container, typename Compare>
bool safeTop(std::priority_queue<T, Container, Compare>& pq, T& result) {
    if (pq.empty()) {
        std::cout << "Error: Priority Queue is empty. Cannot access top.\n";
        return false;
    }
    result = pq.top();
    return true;
}

template<typename T, typename Container, typename Compare>
bool safePop(std::priority_queue<T, Container, Compare>& pq) {
    if (pq.empty()) {
        std::cout << "Error: Priority Queue is empty. Cannot pop.\n";
        return false;
    }
    pq.pop();
    return true;
}

// Example usage
/*
int main() {
    std::priority_queue<int> myPQ;
    myPQ.push(10);
    int value;
    if (safeTop(myPQ, value)) {
        std::cout << "Top: " << value << "\n";
    }
    safePop(myPQ);
    safePop(myPQ); // This will show an error message
    return 0;
}
*/
```

### Safe Priority Queue Wrapper

```cpp
#include <stdexcept> // Required for std::runtime_error
#include <queue>
#include <vector>
#include <functional> // For std::less (default comparator)

template<typename T, typename Container = std::vector<T>, typename Compare = std::less<T>>
class SafePriorityQueue {
private:
    std::priority_queue<T, Container, Compare> pq;
    
public:
    void push(const T& value) {
        pq.push(value);
    }
    
    T pop() {
        if (pq.empty()) {
            throw std::runtime_error("Priority Queue is empty - cannot pop");
        }
        T value = pq.top();
        pq.pop();
        return value;
    }
    
    const T& top() const {
        if (pq.empty()) {
            throw std::runtime_error("Priority Queue is empty - no top element");
        }
        return pq.top();
    }
    
    bool empty() const { return pq.empty(); }
    size_t size() const { return pq.size(); }
};

// Example usage
/*
int main() {
    SafePriorityQueue<int> mySafePQ; // Max-heap
    mySafePQ.push(10);
    std::cout << mySafePQ.top() << "\n";
    mySafePQ.pop();
    try {
        mySafePQ.pop(); // Throws an exception
    } catch (const std::runtime_error& e) {
        std::cerr << "Caught exception: " << e.what() << "\n";
    }
    
    SafePriorityQueue<int, std::vector<int>, std::greater<int>> mySafeMinPQ; // Min-heap
    mySafeMinPQ.push(5);
    mySafeMinPQ.push(2);
    std::cout << "Min-PQ top: " << mySafeMinPQ.top() << "\n"; // Output: 2
    return 0;
}
*/
```

## Best Practices

### ✅ Do:

  - Always check `empty()` before calling `top()` or `pop()` to avoid undefined behavior.
  - Choose the correct comparator (`std::less<T>` for max-heap, `std::greater<T>` for min-heap) or write a custom one for complex types.
  - Understand the `O(log N)` complexity for `push` and `pop` operations.
  - Use `std::priority_queue` when you need efficient access to the highest (or lowest) priority element and don't need full sorting or random access.
  - For custom types, ensure your comparator (or `operator<` if using default) is correctly defined.

### ❌ Don't:

  - Call `top()` or `pop()` on an empty priority queue.
  - Assume priority queues are directly iterable; they are not.
  - Expect `std::priority_queue` to keep all elements sorted in a linear fashion; it only guarantees the `top` element is the highest priority.
  - Use `std::priority_queue` when you need fast random access to elements or need to remove elements other than the highest priority one.

### Code Style Guidelines

```cpp
// Good: Clear variable names
std::priority_queue<std::pair<int, std::string>> eventQueue; // Pair {priority, data}
std::priority_queue<int, std::vector<int>, std::greater<int>> smallestNumbers;

// Good: Check before operations
if (!eventQueue.empty()) {
    auto topEvent = eventQueue.top();
    eventQueue.pop();
}

// Good: Define clear custom comparators for complex types
struct CustomType { int value; };
struct CustomTypeComparator {
    bool operator()(const CustomType& a, const CustomType& b) {
        return a.value < b.value; // For max-heap based on value
    }
};
std::priority_queue<CustomType, std::vector<CustomType>, CustomTypeComparator> myCustomPQ;

// Bad: No error checking
// int topVal = myPQ.top(); // Could crash if empty
// myPQ.pop();
```

## Key Concepts Summary

**Highest Priority First Principle:** The element with the highest priority is always at the top (accessible via `top()`). By default, for primitive types, "highest priority" means the largest value (max-heap).

```cpp
pq.push(10); // PQ: [10]
pq.push(30); // PQ: [30, 10]
pq.push(20); // PQ: [30, 10, 20] (Internal heap structure: 30 at root)
pq.top();    // Returns 30
pq.pop();    // Removes 30, PQ: [20, 10] (Internal heap structure: 20 at root)
```

**No Iterators:** Direct iteration is not supported. Elements can only be accessed via `top()` and removed via `pop()`, or by creating a copy and destructively iterating.

**Container Adapter:** `std::priority_queue` is not a container itself but an interface built on top of other sequence containers (e.g., `std::vector` by default). It uses heap algorithms to maintain its ordering property.

**Common Applications:**

  - Dijkstra's shortest path algorithm
  - Prim's minimum spanning tree algorithm
  - Huffman coding for data compression
  - Event simulators
  - Finding Kth largest/smallest elements efficiently
  - Task scheduling where tasks have priorities

**Memory Characteristics:**

  - Automatic memory management handled by the underlying container (`std::vector`).
  - RAII (Resource Acquisition Is Initialization) compliance.
  - Exception safety guarantees provided by the underlying container operations.

-----

**Last Updated:** August 3, 2025
**Documentation Source:** [cppreference.com - std::priority\_queue](https://en.cppreference.com/w/cpp/container/priority_queue)
**Documentation Source:** [C++ Standard Library Documentation](https://docs.microsoft.com/en-us/cpp/standard-library/)

```
```