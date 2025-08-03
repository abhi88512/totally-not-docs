# Insertion Sort Algorithm

> A simple sorting algorithm that builds the final sorted array one item at a time.

## 
 Table of Contents
- [Description](#description)
- [Algorithm Steps](#algorithm-steps)
- [Example Usage](#example-usage)
- [Time & Space Complexity](#time--space-complexity)
- [Key Characteristics](#key-characteristics)
- [Class Implementation](#class-implementation)

---

## 
 Description

Insertion sort iterates through an input array and removes one element per iteration, finds the location it belongs within the sorted part of the array, and inserts it there. It repeats until no input elements remain.

## 
 Algorithm Steps

Given a vector `arr`:

1.  Iterate from `i = 1` to `n-1`, where `n` is the size of the array. The first element is already considered sorted.
2.  Take the element `arr[i]` and store it in a temporary variable.
3.  Shift elements of the sorted part of the array that are greater than the temporary variable to the right.
4.  Insert the temporary variable in the correct position.

**Step-by-Step Example: `[2, 3, 4, 1, 6]`**
- i=1: `[2,3,4,1,6]` → `[2,3,4,1,6]` (3 >= 2, no swap)
- i=2: `[2,3,4,1,6]` → `[2,3,4,1,6]` (4 >= 3, no swap)  
- i=3: `[2,3,4,1,6]` → `[1,2,3,4,6]` (1 swaps left until position 0)
- i=4: `[1,2,3,4,6]` → `[1,2,3,4,6]` (6 >= 4, no swap)

---

## 
 Example Usage

```cpp
#include <iostream>
#include <vector>

void insertionSort(std::vector<int>& arr);

int main() {
    std::vector<int> numbers = {2, 3, 4, 1, 6};

    insertionSort(numbers);

    std::cout << "Sorted array: 
";
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << "
";

    return 0;
}
```

---

## 
 Time & Space Complexity

*   **Time Complexity**: O(n
)
    *   Best Case: O(n) - if the array is already sorted.
    *   Worst Case: O(n
)
    *   Average Case: O(n
)
*   **Space Complexity**: O(1) - In-place sorting.

---

## 
 Key Characteristics

*   **Simplicity**: Easy to understand and implement.
*   **Stability**: Insertion sort is a stable sorting algorithm.
*   **In-place**: It does not require any extra space.
*   **Efficient for small data**: It is one of the fastest algorithms for sorting very small arrays.

---

## 
 Class Implementation

```cpp
#include <vector>

std::vector<int> insertionSort(std::vector<int>& arr) {
    for (int i = 1; i < arr.size(); i++) {      // Start from second element
        int j = i - 1;                          // Pointer to compare with
        
        while (j >= 0 && arr[j + 1] < arr[j]) { // Swap until correct position
            int tmp = arr[j + 1];               // Three-way swap
            arr[j + 1] = arr[j];
            arr[j] = tmp;
            j--;                                // Move j left
        }
    }
    return arr;
}
```

---

**Last Updated:** 2025-08-02
