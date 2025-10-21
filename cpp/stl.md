# C++ STL (Standard Template Library) - Complete Guide

The STL is a powerful library providing ready-made data structures and algorithms for efficient C++ programming.

## Main Components

1. **Containers** - Data structures to store data
2. **Algorithms** - Common operations on data
3. **Iterators** - Navigate through containers
4. **Functions** - Utility functions

---

## 1. CONTAINERS

### Vector (Dynamic Array)

**Description:** Resizable array that can grow/shrink dynamically.

```cpp
#include <vector>

vector<int> v = {1, 2, 3};
v.push_back(4);              // Add to end - O(1)
v.pop_back();                // Remove from end - O(1)
v.size();                    // Get size - O(1)
v.empty();                   // Check if empty - O(1)
v.clear();                   // Remove all elements - O(n)
v.front();                   // First element - O(1)
v.back();                    // Last element - O(1)
v[0] = 10;                   // Access by index - O(1)
v.at(0);                     // Access with bounds checking - O(1)
v.insert(v.begin() + 2, 99); // Insert at position - O(n)
v.erase(v.begin() + 1);      // Erase at position - O(n)
v.resize(10);                // Resize vector - O(n)
v.reserve(100);              // Reserve capacity - O(n)

// 2D Vector
vector<vector<int>> matrix(3, vector<int>(4, 0)); // 3x4 matrix filled with 0

// Iterate
for(int i = 0; i < v.size(); i++) {
    cout << v[i] << " ";
}

// Range-based for loop
for(int x : v) {
    cout << x << " ";
}

// Iterator
for(auto it = v.begin(); it != v.end(); it++) {
    cout << *it << " ";
}
```

**When to use:** Default choice for dynamic arrays, random access needed.

---

### Set (Unique Sorted Elements)

**Description:** Stores unique elements in sorted order (uses Red-Black Tree).

```cpp
#include <set>

set<int> s = {3, 1, 2};      // Auto-sorted: {1, 2, 3}
s.insert(4);                 // Add element - O(log n)
s.erase(2);                  // Remove element - O(log n)
s.count(3);                  // Check if exists (returns 0 or 1) - O(log n)
s.find(3);                   // Find element (returns iterator) - O(log n)
s.size();                    // Get size - O(1)
s.clear();                   // Remove all - O(n)
s.empty();                   // Check if empty - O(1)

// Check if element exists
if(s.find(3) != s.end()) {
    cout << "Found";
}

// Get smallest and largest
int smallest = *s.begin();
int largest = *s.rbegin();

// Iterate (always sorted)
for(int x : s) {
    cout << x << " ";
}

// Erase by iterator
auto it = s.find(3);
if(it != s.end()) {
    s.erase(it);
}
```

**When to use:** Need unique elements in sorted order, frequent insertions/deletions.

---

### Unordered_set (Unique Unsorted Elements)

**Description:** Stores unique elements without sorting (uses Hash Table).

```cpp
#include <unordered_set>

unordered_set<int> us = {3, 1, 2};  // No sorting
us.insert(4);                       // Add element - O(1) average
us.count(3);                        // Check if exists - O(1) average
us.erase(2);                        // Remove element - O(1) average
us.find(3);                         // Find element - O(1) average
us.size();                          // Get size - O(1)
us.clear();                         // Remove all - O(n)

// Check if element exists
if(us.find(3) != us.end()) {
    cout << "Found";
}

// Iterate (order is unpredictable)
for(int x : us) {
    cout << x << " ";
}
```

**When to use:** Need unique elements, don't care about order, want fast operations.

---

### Map (Key-Value Pairs, Sorted by Key)

**Description:** Stores key-value pairs in sorted order by key (uses Red-Black Tree).

```cpp
#include <map>

map<string, int> m;
m["apple"] = 5;              // Insert/update - O(log n)
m["banana"] = 3;
m.insert({"orange", 7});     // Alternative insert
m.count("apple");            // Check if key exists (0 or 1) - O(log n)
m.erase("banana");           // Remove by key - O(log n)
m.size();                    // Get size - O(1)
m.clear();                   // Remove all - O(n)
m.empty();                   // Check if empty - O(1)

// Access (creates key with default value if doesn't exist)
int val = m["orange"];       // Creates with value 0 if not exists

// Safe access without creating key
if(m.find("apple") != m.end()) {
    cout << m["apple"];
}

// Iterate (sorted by key)
for(auto& pair : m) {
    cout << pair.first << ": " << pair.second << endl;
}

// Get first and last
auto first = m.begin();      // Smallest key
auto last = m.rbegin();      // Largest key
```

**When to use:** Need key-value pairs in sorted order, range queries on keys.

---

### Unordered_map (Key-Value Pairs, Unsorted)

**Description:** Stores key-value pairs without sorting (uses Hash Table).

```cpp
#include <unordered_map>

unordered_map<int, int> um;
um[1] = 100;                 // Insert/update - O(1) average
um.insert({2, 200});         // Alternative insert
um.count(1);                 // Check if key exists - O(1) average
um.find(1);                  // Find key - O(1) average
um.erase(1);                 // Remove by key - O(1) average
um.size();                   // Get size - O(1)
um.clear();                  // Remove all - O(n)

// Safe access
if(um.find(1) != um.end()) {
    cout << um[1];
}

// Iterate (order is unpredictable)
for(auto& [key, value] : um) {
    cout << key << ": " << value << endl;
}

// Common pattern: frequency counter
unordered_map<int, int> freq;
for(int num : nums) {
    freq[num]++;
}
```

**When to use:** Most common choice for key-value pairs, fast operations, don't need sorting.

---

### Stack (LIFO - Last In First Out)

**Description:** Container adapter where elements are inserted and removed from one end only.

```cpp
#include <stack>

stack<int> st;
st.push(1);                  // Add to top - O(1)
st.push(2);
st.push(3);
st.top();                    // Access top element (3) - O(1)
st.pop();                    // Remove top - O(1)
st.empty();                  // Check if empty - O(1)
st.size();                   // Get size - O(1)

// Process all elements
while(!st.empty()) {
    cout << st.top() << " ";
    st.pop();
}
```

**When to use:** Depth-first search, expression evaluation, undo operations, backtracking.

---

### Queue (FIFO - First In First Out)

**Description:** Container adapter where elements are inserted at back and removed from front.

```cpp
#include <queue>

queue<int> q;
q.push(1);                   // Add to back - O(1)
q.push(2);
q.push(3);
q.front();                   // Access front (1) - O(1)
q.back();                    // Access back (3) - O(1)
q.pop();                     // Remove front - O(1)
q.empty();                   // Check if empty - O(1)
q.size();                    // Get size - O(1)

// Process all elements
while(!q.empty()) {
    cout << q.front() << " ";
    q.pop();
}
```

**When to use:** Breadth-first search, level-order traversal, task scheduling.

---

### Priority Queue (Heap)

**Description:** Container adapter where elements are stored in heap order (max heap by default).

```cpp
#include <queue>

// Max heap (default)
priority_queue<int> maxPq;
maxPq.push(3);               // Add element - O(log n)
maxPq.push(1);
maxPq.push(5);
maxPq.top();                 // Get max (5) - O(1)
maxPq.pop();                 // Remove max - O(log n)
maxPq.size();                // Get size - O(1)
maxPq.empty();               // Check if empty - O(1)

// Min heap
priority_queue<int, vector<int>, greater<int>> minPq;
minPq.push(3);
minPq.push(1);
minPq.push(5);
minPq.top();                 // Get min (1) - O(1)
minPq.pop();                 // Remove min - O(log n)

// Priority queue with pairs (sorts by first element)
priority_queue<pair<int, int>> pqPair;
pqPair.push({5, 100});
pqPair.push({3, 200});
pqPair.top();                // {5, 100}

// Custom comparator for min heap with pairs
auto cmp = [](pair<int,int> a, pair<int,int> b) { return a.first > b.first; };
priority_queue<pair<int,int>, vector<pair<int,int>>, decltype(cmp)> customPq(cmp);
```

**When to use:** Finding kth largest/smallest, Dijkstra's algorithm, task scheduling by priority.

---

### Deque (Double-ended Queue)

**Description:** Allows fast insertion/deletion at both ends.

```cpp
#include <deque>

deque<int> dq;
dq.push_back(1);             // Add to back - O(1)
dq.push_front(0);            // Add to front - O(1)
dq.pop_back();               // Remove from back - O(1)
dq.pop_front();              // Remove from front - O(1)
dq.front();                  // Access front - O(1)
dq.back();                   // Access back - O(1)
dq[0];                       // Access by index - O(1)
dq.size();                   // Get size - O(1)
dq.clear();                  // Remove all - O(n)

// Iterate
for(int x : dq) {
    cout << x << " ";
}
```

**When to use:** Sliding window problems, need fast operations at both ends.

---

### Pair (Store Two Values)

**Description:** Simple container to hold two values together.

```cpp
#include <utility>

pair<int, string> p = {1, "apple"};
p.first;                     // 1
p.second;                    // "apple"

// Make pair
auto p2 = make_pair(2, "banana");

// Comparison (compares first, then second)
pair<int, int> a = {1, 2};
pair<int, int> b = {1, 3};
cout << (a < b);             // true (because 2 < 3)

// Vector of pairs
vector<pair<int, int>> vp = {{1, 2}, {3, 4}};

// Sort by second element
sort(vp.begin(), vp.end(), [](auto& a, auto& b) {
    return a.second < b.second;
});

// Iterate
for(auto& [x, y] : vp) {     // Structured binding (C++17)
    cout << x << " " << y << endl;
}
```

**When to use:** Store coordinate pairs, key-value in vectors, multiple return values.

---

## 2. ALGORITHMS

```cpp
#include <algorithm>
```

### Sorting

```cpp
vector<int> v = {5, 2, 8, 1, 9};

// Ascending order
sort(v.begin(), v.end());                    // {1, 2, 5, 8, 9}

// Descending order
sort(v.begin(), v.end(), greater<int>());    // {9, 8, 5, 2, 1}

// Custom comparator (sort by absolute value)
sort(v.begin(), v.end(), [](int a, int b) {
    return abs(a) < abs(b);
});

// Sort pairs by second element
vector<pair<int, int>> vp = {{1, 5}, {2, 3}, {3, 4}};
sort(vp.begin(), vp.end(), [](auto& a, auto& b) {
    return a.second < b.second;
});

// Partial sort (sort first k elements)
partial_sort(v.begin(), v.begin() + 3, v.end());

// Check if sorted
bool isSorted = is_sorted(v.begin(), v.end());
```

### Searching

```cpp
vector<int> v = {1, 2, 5, 8, 9};

// Binary search (array must be sorted)
bool found = binary_search(v.begin(), v.end(), 5);  // true

// Lower bound (first element >= value)
auto it = lower_bound(v.begin(), v.end(), 5);
int index = it - v.begin();                         // 2

// Upper bound (first element > value)
auto it2 = upper_bound(v.begin(), v.end(), 5);
int index2 = it2 - v.begin();                       // 3

// Find element (linear search)
auto it3 = find(v.begin(), v.end(), 5);
if(it3 != v.end()) {
    cout << "Found at index: " << it3 - v.begin();
}

// Find if (with condition)
auto it4 = find_if(v.begin(), v.end(), [](int x) { 
    return x > 5; 
});

// Count occurrences
int cnt = count(v.begin(), v.end(), 5);

// Count if (with condition)
int cntIf = count_if(v.begin(), v.end(), [](int x) { 
    return x > 5; 
});
```

### Min/Max

```cpp
vector<int> v = {5, 2, 8, 1, 9};

// Find max element
int maxVal = *max_element(v.begin(), v.end());      // 9
auto maxIt = max_element(v.begin(), v.end());
int maxIndex = maxIt - v.begin();

// Find min element
int minVal = *min_element(v.begin(), v.end());      // 1
auto minIt = min_element(v.begin(), v.end());
int minIndex = minIt - v.begin();

// Min/max of two values
int smaller = min(5, 10);                           // 5
int larger = max(5, 10);                            // 10

// Min/max of multiple values
int minimum = min({5, 2, 8, 1, 9});                 // 1
int maximum = max({5, 2, 8, 1, 9});                 // 9

// Clamp (constrain value between min and max)
int clamped = clamp(15, 0, 10);                     // 10
```

### Reverse and Rotate

```cpp
vector<int> v = {1, 2, 3, 4, 5};

// Reverse
reverse(v.begin(), v.end());                        // {5, 4, 3, 2, 1}

// Rotate left
rotate(v.begin(), v.begin() + 2, v.end());          // {3, 4, 5, 1, 2}

// Rotate right
rotate(v.rbegin(), v.rbegin() + 2, v.rend());       // {4, 5, 1, 2, 3}
```

### Permutations

```cpp
vector<int> v = {1, 2, 3};

// Next permutation
next_permutation(v.begin(), v.end());               // {1, 3, 2}

// Previous permutation
prev_permutation(v.begin(), v.end());               // {1, 2, 3}

// Generate all permutations
sort(v.begin(), v.end());
do {
    for(int x : v) cout << x << " ";
    cout << endl;
} while(next_permutation(v.begin(), v.end()));
```

### Fill and Transform

```cpp
vector<int> v(5);

// Fill with value
fill(v.begin(), v.end(), 10);                       // {10, 10, 10, 10, 10}

// Fill with sequence
iota(v.begin(), v.end(), 1);                        // {1, 2, 3, 4, 5}

// Transform (apply function to each element)
transform(v.begin(), v.end(), v.begin(), [](int x) {
    return x * 2;
});                                                 // {2, 4, 6, 8, 10}

// Replace value
replace(v.begin(), v.end(), 5, 99);                 // Replace all 5 with 99

// Replace if (with condition)
replace_if(v.begin(), v.end(), [](int x) { 
    return x > 5; 
}, 0);
```

### Remove and Unique

```cpp
vector<int> v = {1, 2, 3, 2, 4, 1, 5};

// Remove value (moves to end, doesn't delete)
auto it = remove(v.begin(), v.end(), 2);
v.erase(it, v.end());                               // {1, 3, 4, 1, 5}

// Remove if (with condition)
auto it2 = remove_if(v.begin(), v.end(), [](int x) { 
    return x > 3; 
});
v.erase(it2, v.end());                              // {1, 3, 1}

// Remove duplicates (must sort first)
sort(v.begin(), v.end());                           // {1, 1, 3}
auto it3 = unique(v.begin(), v.end());
v.erase(it3, v.end());                              // {1, 3}
```

### Accumulate and Reduce

```cpp
#include <numeric>

vector<int> v = {1, 2, 3, 4, 5};

// Sum of elements
int sum = accumulate(v.begin(), v.end(), 0);        // 15

// Product of elements
int product = accumulate(v.begin(), v.end(), 1, multiplies<int>());  // 120

// Custom operation
int result = accumulate(v.begin(), v.end(), 0, [](int acc, int x) {
    return acc + x * x;  // Sum of squares
});                                                 // 55
```

### Partition

```cpp
vector<int> v = {1, 5, 3, 7, 2, 9, 4};

// Partition (move elements satisfying condition to front)
partition(v.begin(), v.end(), [](int x) { 
    return x % 2 == 0; 
});                                                 // {4, 2, 3, 7, 5, 9, 1}

// Stable partition (maintains relative order)
stable_partition(v.begin(), v.end(), [](int x) { 
    return x % 2 == 0; 
});
```

### Swap

```cpp
int a = 5, b = 10;
swap(a, b);                                         // a=10, b=5

vector<int> v1 = {1, 2}, v2 = {3, 4};
swap(v1, v2);                                       // v1={3,4}, v2={1,2}

// Swap ranges
vector<int> v = {1, 2, 3, 4, 5};
swap_ranges(v.begin(), v.begin() + 2, v.begin() + 3);  // {4, 5, 3, 1, 2}
```

---

## 3. ITERATORS

```cpp
vector<int> v = {1, 2, 3, 4, 5};

// Begin and end
auto it1 = v.begin();                    // Points to first element
auto it2 = v.end();                      // Points past last element

// Reverse iterators
auto rit1 = v.rbegin();                  // Points to last element
auto rit2 = v.rend();                    // Points before first element

// Constant iterators
auto cit = v.cbegin();                   // Const iterator

// Access element
cout << *it1;                            // 1

// Move iterator
it1++;                                   // Move to next
it1--;                                   // Move to previous
it1 += 2;                                // Move forward by 2
it1 -= 1;                                // Move backward by 1

// Distance between iterators
int dist = distance(v.begin(), v.end()); // 5

// Advance iterator
advance(it1, 3);                         // Move forward by 3
```

---

## 4. STRING OPERATIONS

```cpp
#include <string>

string s = "hello";

// Basic operations
s.length();                              // Get length
s.size();                                // Same as length
s.empty();                               // Check if empty
s.clear();                               // Clear string
s[0];                                    // Access character
s.at(0);                                 // Access with bounds check
s.front();                               // First character
s.back();                                // Last character

// Modification
s.push_back('!');                        // Add character - "hello!"
s.pop_back();                            // Remove last character - "hello"
s += " world";                           // Concatenate - "hello world"
s.append(" world");                      // Append - "hello world"
s.insert(5, "!");                        // Insert at position - "hello! world"
s.erase(5, 1);                           // Erase from position - "hello world"
s.replace(0, 5, "hi");                   // Replace - "hi world"

// Substring
string sub = s.substr(0, 5);             // "hello"
string sub2 = s.substr(6);               // "world"

// Search
size_t pos = s.find("world");            // Find substring (returns position or npos)
if(pos != string::npos) {
    cout << "Found at: " << pos;
}
size_t rpos = s.rfind("o");              // Find last occurrence

// Compare
int cmp = s.compare("hello");            // 0 if equal, <0 if less, >0 if greater
bool equal = (s == "hello");             // Direct comparison

// Convert
int num = stoi("123");                   // String to int
long lnum = stol("123");                 // String to long
float fnum = stof("12.3");               // String to float
double dnum = stod("12.3");              // String to double
string str = to_string(123);             // Number to string

// Case conversion
transform(s.begin(), s.end(), s.begin(), ::tolower);  // To lowercase
transform(s.begin(), s.end(), s.begin(), ::toupper);  // To uppercase

// Split string (no built-in function, use stringstream)
#include <sstream>
stringstream ss("hello world how are you");
string word;
vector<string> words;
while(ss >> word) {
    words.push_back(word);
}

// Join strings
vector<string> parts = {"hello", "world"};
string joined = "";
for(int i = 0; i < parts.size(); i++) {
    joined += parts[i];
    if(i < parts.size() - 1) joined += " ";
}

// Trim whitespace (no built-in, use erase)
s.erase(0, s.find_first_not_of(" \t\n"));              // Trim left
s.erase(s.find_last_not_of(" \t\n") + 1);              // Trim right

// Reverse
reverse(s.begin(), s.end());

// Check if substring
bool hasSubstr = (s.find("world") != string::npos);

// Count character occurrences
int cnt = count(s.begin(), s.end(), 'o');
```

---

## 5. COMMON LEETCODE PATTERNS

### Pattern 1: Two Sum with Hash Map
```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> map;
    for(int i = 0; i < nums.size(); i++) {
        int complement = target - nums[i];
        if(map.count(complement)) {
            return {map[complement], i};
        }
        map[nums[i]] = i;
    }
    return {};
}
```

### Pattern 2: Frequency Counter
```cpp
unordered_map<int, int> freq;
for(int num : nums) {
    freq[num]++;
}

// Find most frequent
int maxFreq = 0;
int mostFrequent;
for(auto& [num, count] : freq) {
    if(count > maxFreq) {
        maxFreq = count;
        mostFrequent = num;
    }
}
```

### Pattern 3: Sliding Window with Deque
```cpp
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    deque<int> dq;
    vector<int> result;
    
    for(int i = 0; i < nums.size(); i++) {
        // Remove elements outside window
        if(!dq.empty() && dq.front() == i - k) {
            dq.pop_front();
        }
        
        // Remove smaller elements
        while(!dq.empty() && nums[i] >= nums[dq.back()]) {
            dq.pop_back();
        }
        
        dq.push_back(i);
        
        if(i >= k - 1) {
            result.push_back(nums[dq.front()]);
        }
    }
    return result;
}
```

### Pattern 4: K Largest with Min Heap
```cpp
priority_queue<int, vector<int>, greater<int>> minHeap;
for(int num : nums) {
    minHeap.push(num);
    if(minHeap.size() > k) {
        minHeap.pop();
    }
}
// minHeap.top() is kth largest
```

### Pattern 5: Graph BFS with Queue
```cpp
queue<int> q;
vector<bool> visited(n, false);

q.push(start);
visited[start] = true;

while(!q.empty()) {
    int node = q.front();
    q.pop();
    
    for(int neighbor : graph[node]) {
        if(!visited[neighbor]) {
            visited[neighbor] = true;
            q.push(neighbor);
        }
    }
}
```

### Pattern 6: Graph DFS with Stack
```cpp
stack<int> st;
vector<bool> visited(n, false);

st.push(start);

while(!st.empty()) {
    int node = st.top();
    st.pop();
    
    if(visited[node]) continue;
    visited[node] = true;
    
    for(int neighbor : graph[node]) {
        if(!visited[neighbor]) {
            st.push(neighbor);
        }
    }
}
```

### Pattern 7: Intervals Merge
```cpp
vector<vector<int>> merge(vector<vector<int>>& intervals) {
    sort(intervals.begin(), intervals.end());
    vector<vector<int>> result;
    
    for(auto& interval : intervals) {
        if(result.empty() || result.back()[1] < interval[0]) {
            result.push_back(interval);
        } else {
            result.back()[1] = max(result.back()[1], interval[1]);
        }
    }
    return result;
}
```

### Pattern 8: Top K Frequent Elements
```cpp
unordered_map<int, int> freq;
for(int num : nums) {
    freq[num]++;
}

priority_queue<pair<int, int>> maxHeap;
for(auto& [num, count] : freq) {
    maxHeap.push({count, num});
}

vector<int> result;
for(int i = 0; i < k; i++) {
    result.push_back(maxHeap.top().second);
    maxHeap.pop();
}
```

---

## 6. TIME COMPLEXITIES

| Container | Insert | Delete | Access | Search | Space |
|-----------|--------|--------|--------|--------|-------|
| vector | O(1) amortized end, O(n) middle | O(1) end, O(n) middle | O(1) | O(n) | O(n) |
| set | O(log n) | O(log n) | - | O(log n) | O(n) |
| unordered_set | O(1) average, O(n) worst | O(1) average, O(n) worst | - | O(1) average, O(n) worst | O(n) |
| map | O(log n) | O(log n) | O(log n) | O(log n) | O(n) |
| unordered_map | O(1) average, O(n) worst | O(1) average, O(n) worst | O(1) average, O(n) worst | O(1) average, O(n) worst | O(n) |
| stack | O(1) | O(1) | O(1) top only | - | O(n) |
| queue | O(1) | O(1) | O(1) front/back | - | O(n) |
| priority_queue | O(log n) | O(log n) | O(1) top only | - | O(n) |
| deque | O(1) both ends, O(n) middle | O(1) both ends, O(n) middle | O(1) | O(n) | O(n) |

### Algorithm Time Complexities

| Algorithm | Time Complexity | Space Complexity |
|-----------|----------------|------------------|
| sort | O(n log n) | O(log n) |
| binary_search | O(log n) | O(1) |
| lower_bound/upper_bound | O(log n) | O(1) |
| find | O(n) | O(1) |
| reverse | O(n) | O(1) |
| unique | O(n) | O(1) |
| accumulate | O(n) | O(1) |
| next_permutation | O(n) | O(1) |

---

## 7. QUICK REFERENCE TEMPLATE

```cpp
// Most commonly used includes
#include <iostream>
#include <vector>
#include <string>
#include <unordered_map>
#include <unordered_set>
#include <map>
#include <set>
#include <queue>
#include <stack>
#include <deque>
#include <algorithm>
#include <numeric>
#include <utility>
#include <climits>

using namespace std;

// Fast I/O (for competitive programming)
ios_base::sync_with_stdio(false);
cin.tie(NULL);

// Common typedefs
typedef long long ll;
typedef pair<int, int> pii;
typedef vector<int> vi;
typedef vector<vector<int>> vvi;
```

---

## 8. TIPS AND BEST PRACTICES

### When to Use Which Container?

**Use vector when:**
- Need dynamic array with random access
- Mostly adding/removing from end
- Default choice for most problems

**Use set when:**
- Need unique elements in sorted order
- Frequent insertions and deletions
- Need to find smallest/largest efficiently

**Use unordered_set when:**
- Need unique elements
- Don't care about order
- Want O(1) operations

**Use map when:**
- Need key-value pairs in sorted order
- Need range queries on keys
- Want ordered iteration

**Use unordered_map when:**
- Need key-value pairs
- Don't care about order
- Want O(1) operations (most common choice)

**Use stack when:**
- Need LIFO behavior
- Depth-first search
- Expression evaluation
- Backtracking

**Use queue when:**
- Need FIFO behavior
- Breadth-first search
- Level-order traversal

**Use priority_queue when:**
- Need min/max efficiently
- Kth largest/smallest problems
- Dijkstra's algorithm

**Use deque when:**
- Need fast operations at both ends
- Sliding window problems

---

## 9. COMMON MISTAKES TO AVOID

### Mistake 1: Using map[key] to Check Existence
```cpp
// WRONG - creates key if doesn't exist
if(map[key]) { }

// CORRECT
if(map.find(key) != map.end()) { }
if(map.count(key)) { }
```

### Mistake 2: Modifying Container While Iterating
```cpp
// WRONG
for(auto it = v.begin(); it != v.end(); it++) {
    if(*it == 5) {
        v.erase(it);  // Iterator invalidated
    }
}

// CORRECT
for(auto it = v.begin(); it != v.end(); ) {
    if(*it == 5) {
        it = v.erase(it);  // erase returns next valid iterator
    } else {
        it++;
    }
}
```

### Mistake 3: Not Checking Empty Before pop/top
```cpp
// WRONG
stack.pop();  // Undefined behavior if empty

// CORRECT
if(!stack.empty()) {
    stack.pop();
}
```

### Mistake 4: Using . instead of -> for Iterators
```cpp
// WRONG
auto it = map.begin();
cout << it.first;  // Error

// CORRECT
cout << it->first;  // Correct
```

### Mistake 5: Forgetting to Sort Before binary_search
```cpp
vector<int> v = {5, 2, 8, 1};

// WRONG
binary_search(v.begin(), v.end(), 5);  // Undefined behavior

// CORRECT
sort(v.begin(), v.end());
binary_search(v.begin(), v.end(), 5);
```

### Mistake 6: Comparing with .end() After Modification
```cpp
// WRONG
auto it = v.end();
v.push_back(10);
if(it == v.end()) { }  // it may be invalidated

// CORRECT
// Get .end() fresh every time after modification
if(some_iterator == v.end()) { }
```

---

## 10. ADVANCED TIPS

### Lambda Functions
```cpp
// Sort with custom comparator
sort(v.begin(), v.end(), [](int a, int b) {
    return a > b;  // Descending order
});

// For_each with lambda
for_each(v.begin(), v.end(), [](int x) {
    cout << x << " ";
});

// Find_if with lambda
auto it = find_if(v.begin(), v.end(), [](int x) {
    return x > 5;
});

// Lambda with capture
int threshold = 10;
auto it2 = find_if(v.begin(), v.end(), [threshold](int x) {
    return x > threshold;
});
```

### Auto Keyword
```cpp
// Instead of writing long types
unordered_map<string, vector<int>>::iterator it = map.begin();

// Use auto
auto it = map.begin();

// With structured bindings (C++17)
for(auto& [key, value] : map) {
    cout << key << ": " << value;
}
```

### Emplace vs Push
```cpp
// push_back creates object then copies
v.push_back(pair<int, int>(1, 2));

// emplace_back constructs in-place (more efficient)
v.emplace_back(1, 2);

// Similarly for other containers
map.emplace("key", 100);
set.emplace(5);
```

### Reserve for Vectors
```cpp
// Avoid reallocations when you know size
vector<int> v;
v.reserve(1000);  // Reserve space for 1000 elements
for(int i = 0; i < 1000; i++) {
    v.push_back(i);  // No reallocation needed
}
```

### Custom Comparator for Set/Map
```cpp
// Custom comparator for set
struct Compare {
    bool operator()(int a, int b) const {
        return a > b;  // Descending order
    }
};
set<int, Compare> s;

// Lambda comparator (C++11)
auto cmp = [](int a, int b) { return a > b; };
set<int, decltype(cmp)> s2(cmp);
```

### Erase-Remove Idiom
```cpp
// Remove all occurrences of value
v.erase(remove(v.begin(), v.end(), value), v.end());

// Remove all elements satisfying condition
v.erase(remove_if(v.begin(), v.end(), [](int x) {
    return x > 5;
}), v.end());
```

---

## 11. USEFUL CODE SNIPPETS

### Read Input Until EOF
```cpp
int n;
while(cin >> n) {
    // Process n
}

string line;
while(getline(cin, line)) {
    // Process line
}
```

### Read 2D Array
```cpp
int rows, cols;
cin >> rows >> cols;
vector<vector<int>> matrix(rows, vector<int>(cols));

for(int i = 0; i < rows; i++) {
    for(int j = 0; j < cols; j++) {
        cin >> matrix[i][j];
    }
}
```

### Print Vector
```cpp
// Simple
for(int x : v) {
    cout << x << " ";
}
cout << endl;

// With iterator
for(auto it = v.begin(); it != v.end(); it++) {
    cout << *it << " ";
}
cout << endl;

// Copy to output
copy(v.begin(), v.end(), ostream_iterator<int>(cout, " "));
```

### Deep Copy vs Shallow Copy
```cpp
// Shallow copy (both point to same memory)
vector<int>* v1 = new vector<int>{1, 2, 3};
vector<int>* v2 = v1;  // Same object

// Deep copy (separate objects)
vector<int> v3 = {1, 2, 3};
vector<int> v4 = v3;  // Different objects
```

### Check if All Elements Satisfy Condition
```cpp
// Check if all even
bool allEven = all_of(v.begin(), v.end(), [](int x) {
    return x % 2 == 0;
});

// Check if any even
bool anyEven = any_of(v.begin(), v.end(), [](int x) {
    return x % 2 == 0;
});

// Check if none even
bool noneEven = none_of(v.begin(), v.end(), [](int x) {
    return x % 2 == 0;
});
```

### Generate Random Numbers
```cpp
#include <random>

random_device rd;
mt19937 gen(rd());
uniform_int_distribution<> dis(1, 100);

int randomNum = dis(gen);  // Random number between 1 and 100
```

### Measure Execution Time
```cpp
#include <chrono>

auto start = chrono::high_resolution_clock::now();

// Code to measure

auto end = chrono::high_resolution_clock::now();
auto duration = chrono::duration_cast<chrono::milliseconds>(end - start);
cout << "Time: " << duration.count() << "ms" << endl;
```

---

## 12. PROBLEM-SPECIFIC PATTERNS

### Two Pointers
```cpp
// Remove duplicates from sorted array
int j = 0;
for(int i = 1; i < nums.size(); i++) {
    if(nums[i] != nums[j]) {
        j++;
        nums[j] = nums[i];
    }
}
return j + 1;
```

### Sliding Window
```cpp
// Maximum sum subarray of size k
int maxSum = 0, windowSum = 0;
for(int i = 0; i < k; i++) {
    windowSum += arr[i];
}
maxSum = windowSum;

for(int i = k; i < n; i++) {
    windowSum += arr[i] - arr[i - k];
    maxSum = max(maxSum, windowSum);
}
```

### Prefix Sum
```cpp
// Build prefix sum array
vector<int> prefix(n + 1, 0);
for(int i = 0; i < n; i++) {
    prefix[i + 1] = prefix[i] + arr[i];
}

// Sum of range [l, r]
int rangeSum = prefix[r + 1] - prefix[l];
```

### Binary Search Template
```cpp
int left = 0, right = n - 1;
while(left <= right) {
    int mid = left + (right - left) / 2;  // Avoid overflow
    
    if(arr[mid] == target) {
        return mid;
    } else if(arr[mid] < target) {
        left = mid + 1;
    } else {
        right = mid - 1;
    }
}
return -1;
```

### Backtracking Template
```cpp
void backtrack(vector<int>& nums, vector<int>& current, vector<vector<int>>& result) {
    // Base case
    if(current.size() == nums.size()) {
        result.push_back(current);
        return;
    }
    
    // Recursive case
    for(int i = 0; i < nums.size(); i++) {
        // Choose
        current.push_back(nums[i]);
        
        // Explore
        backtrack(nums, current, result);
        
        // Unchoose
        current.pop_back();
    }
}
```

### DFS Recursion Template
```cpp
void dfs(int node, vector<vector<int>>& graph, vector<bool>& visited) {
    visited[node] = true;
    
    // Process node
    
    for(int neighbor : graph[node]) {
        if(!visited[neighbor]) {
            dfs(neighbor, graph, visited);
        }
    }
}
```

### Dynamic Programming Template
```cpp
// 1D DP
vector<int> dp(n);
dp[0] = base_case;

for(int i = 1; i < n; i++) {
    dp[i] = /* recurrence relation */;
}

// 2D DP
vector<vector<int>> dp(m, vector<int>(n));
dp[0][0] = base_case;

for(int i = 0; i < m; i++) {
    for(int j = 0; j < n; j++) {
        dp[i][j] = /* recurrence relation */;
    }
}
```

### Trie Template
```cpp
struct TrieNode {
    unordered_map<char, TrieNode*> children;
    bool isEnd = false;
};

class Trie {
    TrieNode* root;
public:
    Trie() {
        root = new TrieNode();
    }
    
    void insert(string word) {
        TrieNode* node = root;
        for(char c : word) {
            if(!node->children.count(c)) {
                node->children[c] = new TrieNode();
            }
            node = node->children[c];
        }
        node->isEnd = true;
    }
    
    bool search(string word) {
        TrieNode* node = root;
        for(char c : word) {
            if(!node->children.count(c)) {
                return false;
            }
            node = node->children[c];
        }
        return node->isEnd;
    }
};
```

### Union Find Template
```cpp
class UnionFind {
    vector<int> parent, rank;
public:
    UnionFind(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for(int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }
    
    int find(int x) {
        if(parent[x] != x) {
            parent[x] = find(parent[x]);  // Path compression
        }
        return parent[x];
    }
    
    void unite(int x, int y) {
        int px = find(x), py = find(y);
        if(px == py) return;
        
        // Union by rank
        if(rank[px] < rank[py]) {
            parent[px] = py;
        } else if(rank[px] > rank[py]) {
            parent[py] = px;
        } else {
            parent[py] = px;
            rank[px]++;
        }
    }
    
    bool connected(int x, int y) {
        return find(x) == find(y);
    }
};
```

---

## 13. COMPARISON: ORDERED VS UNORDERED

### Set vs Unordered_set

| Feature | set | unordered_set |
|---------|-----|---------------|
| Ordering | Sorted | No order |
| Implementation | Red-Black Tree | Hash Table |
| Insert | O(log n) | O(1) average |
| Search | O(log n) | O(1) average |
| Delete | O(log n) | O(1) average |
| Iteration | Sorted order | Random order |
| Memory | Less overhead | More overhead |
| When to use | Need sorted order, range queries | Just need fast lookup |

### Map vs Unordered_map

| Feature | map | unordered_map |
|---------|-----|---------------|
| Ordering | Sorted by key | No order |
| Implementation | Red-Black Tree | Hash Table |
| Insert | O(log n) | O(1) average |
| Search | O(log n) | O(1) average |
| Delete | O(log n) | O(1) average |
| Iteration | Sorted by key | Random order |
| Memory | Less overhead | More overhead |
| When to use | Need sorted keys, range queries | Just need fast key-value lookup |

**Rule of Thumb:** Use unordered versions unless you specifically need ordering!

---

## 14. MEMORY MANAGEMENT

### Stack vs Heap Allocation
```cpp
// Stack allocation (automatic, faster)
vector<int> v1 = {1, 2, 3};

// Heap allocation (manual, slower)
vector<int>* v2 = new vector<int>{1, 2, 3};
delete v2;  // Must manually delete

// Smart pointers (C++11) - automatic cleanup
unique_ptr<vector<int>> v3 = make_unique<vector<int>>(vector<int>{1, 2, 3});
shared_ptr<vector<int>> v4 = make_shared<vector<int>>(vector<int>{1, 2, 3});
```

### Size vs Capacity
```cpp
vector<int> v;
cout << v.size();      // Number of elements (0)
cout << v.capacity();  // Allocated space (0)

v.push_back(1);
cout << v.size();      // 1
cout << v.capacity();  // Usually 1

v.push_back(2);
cout << v.size();      // 2
cout << v.capacity();  // Usually 2

v.push_back(3);
cout << v.size();      // 3
cout << v.capacity();  // Usually 4 (doubled)

// Reserve space to avoid reallocations
v.reserve(100);
cout << v.capacity();  // 100

// Shrink capacity to fit size
v.shrink_to_fit();
cout << v.capacity();  // 3 (same as size)
```

---

## 15. FINAL TIPS

### Performance Optimization
1. Use `unordered_map` and `unordered_set` for O(1) operations
2. Reserve space in vectors when size is known: `v.reserve(n)`
3. Use `emplace_back` instead of `push_back` for complex objects
4. Pass large objects by reference: `void func(const vector<int>& v)`
5. Use `'\n'` instead of `endl` (endl flushes buffer)

### Debugging Tips
1. Print container contents to verify
2. Check for off-by-one errors in loops
3. Verify iterator validity after modifications
4. Check for empty containers before accessing
5. Use assertions: `assert(condition)`

### Code Style
1. Use meaningful variable names
2. Add comments for complex logic
3. Keep functions small and focused
4. Use const correctness
5. Follow consistent naming convention

### Common Interview Patterns
1. Two pointers for sorted arrays
2. Sliding window for subarray problems
3. Hash map for frequency/lookup problems
4. Stack for parentheses/monotonic problems
5. Queue for BFS/level-order problems
6. Priority queue for kth largest/smallest
7. Set for uniqueness problems
8. Prefix sum for range queries

### Last Resort Checks
- Did you sort before binary_search?
- Did you check if container is empty?
- Are you using the right container for the job?
- Is your comparison function correct?
- Did you initialize all variables?
- Are you modifying while iterating correctly?

---

## SUMMARY

The C++ STL is powerful and essential for competitive programming and interviews. Master these key points:

1. **Vector** is your default array choice
2. **Unordered_map/set** for fast O(1) operations
3. **Map/set** when you need sorted order
4. **Stack/Queue** for DFS/BFS
5. **Priority_queue** for heap operations
6. **Sort** before using binary_search
7. **Lambda functions** for custom comparisons
8. **Auto** keyword for cleaner code
9. **Iterators** for container traversal
10. **Know time complexities** of all operations

Practice these patterns and STL will become second nature!