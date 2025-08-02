# Binary Search Algorithm (Vector Implementation)

> An efficient algorithm to find a target value within a **sorted** list (or array) by repeatedly dividing the search interval in half.

## 📋 Table of Contents
- [Description](#description)
- [Prerequisites](#prerequisites)
- [Algorithm Steps](#algorithm-steps)
- [Example Usage](#example-usage)
- [Time & Space Complexity](#time--space-complexity)
- [Key Characteristics](#key-characteristics)
- [Class Implementation](#class-implementation)

---

## 📝 Description

Binary search is a divide-and-conquer algorithm for locating the position of a target value within a sorted collection. It works by comparing the target value to the middle element of the collection. If they are not equal, the half in which the target cannot lie is eliminated, and the search continues on the remaining half until the target is found or the interval becomes empty.

## ✅ Prerequisites

* The collection (e.g., `std::vector`) must be **sorted** in ascending (non-decreasing) order.
* The elements must support comparison operations (e.g., `==`, `<`, `>`).

---

## 🚶 Algorithm Steps

Given a sorted vector `arr` and a `target` value:

1.  Initialize two pointers, `left` to the first index (0) and `right` to the last index (`arr.size() - 1`).

2.  While `left` is less than or equal to `right`:

    a.  Calculate the `mid` index: `mid = left + (right - left) / 2`. 
    
    (This helps prevent potential integer overflow compared to `(left + right) / 2` for very large `left` and `right` values).

    
    b.  Compare `arr[mid]` with `target`:

        i.  If `arr[mid] == target`, the target is found. Return `mid`.
        ii. If `arr[mid] < target`, the target must be in the right half. Update `left = mid + 1`.
        iii. If `arr[mid] > target`, the target must be in the left half. Update `right = mid - 1`.

3.  If the loop finishes, it means `target` was not found in the vector. Return -1 (or an appropriate indicator for "not found").

---

## 💻 Example Usage

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // Required for std::sort (if input isn't guaranteed to be sorted)

// Function declaration (full implementation provided in Class Implementation section)
int binarySearch(const std::vector<int>& arr, int target);

int main() {
    std::vector<int> numbers = {10, 20, 30, 40, 50, 60, 70, 80, 90};
    // In a real application, ensure the vector is sorted:
    // std::sort(numbers.begin(), numbers.end()); 

    int target1 = 40;
    int index1 = binarySearch(numbers, target1);
    if (index1 != -1) {
        std::cout << "Target " << target1 << " found at index: " << index1 << "\n"; 
    } else {
        std::cout << "Target " << target1 << " not found.\n";
    }

    int target2 = 75;
    int index2 = binarySearch(numbers, target2);
    if (index2 != -1) {
        std::cout << "Target " << target2 << " found at index: " << index2 << "\n";
    } else {
        std::cout << "Target " << target2 << " not found.\n"; 
    }

    return 0;
}
````

-----

## ⏱️ Time & Space Complexity

  * **Time Complexity**: $O(\\log N)$, where $N$ is the number of elements in the vector. This logarithmic complexity is achieved because the algorithm effectively halves the remaining search space in each iteration.
  * **Space Complexity**: $O(1)$, as the iterative implementation uses a constant amount of auxiliary space for variables (e.g., `left`, `right`, `mid`), regardless of the input size. (Note: A recursive implementation would incur $O(\\log N)$ stack space due to function call overhead).

-----

## 🔑 Key Characteristics

  * **Efficiency**: Extremely efficient for searching in large, sorted collections.
  * **Sorted Input Requirement**: This is a strict prerequisite for the algorithm's correctness.
  * **Divide and Conquer Principle**: The algorithm's core mechanism involves breaking down the problem into smaller, similar sub-problems.
  * **Direct Index Return**: Typically, the implementation returns the exact index of the found element, or a conventional value (like -1) if the element is not present.

-----

## 💻 Class Implementation

```cpp
#include <vector> // Required for std::vector

// Function to perform binary search on a sorted vector
// Returns the index of the target if found, otherwise -1.
int binarySearch(const std::vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    // Continue searching as long as the left pointer does not cross the right pointer
    while (left <= right) {
        // Calculate mid index. Using (right - left) / 2 + left prevents overflow.
        int mid = left + (right - left) / 2;

        if (arr[mid] == target) {
            return mid; // Target found at mid index
        } else if (arr[mid] < target) {
            // If the middle element is less than the target,
            // the target must be in the right half of the current search space.
            left = mid + 1; 
        } else { // arr[mid] > target
            // If the middle element is greater than the target,
            // the target must be in the left half of the current search space.
            right = mid - 1; 
        }
    }

    return -1; // Target not found in the vector
}
```

-----

**Last Updated:** 2025-08-02

```
```