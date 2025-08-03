# Quick Sort Algorithm

> A divide-and-conquer algorithm that picks an element as a pivot and partitions the given array around the picked pivot.

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

Quick sort is a highly efficient sorting algorithm. It works by picking an element as a pivot and partitioning the array around the pivot. The key process in quick sort is the `partition()` function. The target of partitions is to place the pivot at its correct position in the sorted array and put all smaller elements to the left of the pivot, and all greater elements to the right of the pivot.

## 
 Algorithm Steps

Given a vector `arr`:

1.  **Pivot Selection**: Choose a pivot element from the array. Different strategies can be used, such as picking the first element, the last element, a random element, or the median.
2.  **Partitioning**: Rearrange the array so that all elements smaller than the pivot are on the left side of the pivot, and all elements greater than the pivot are on the right side. The pivot is now in its final sorted position.
3.  **Recursion**: Recursively apply the above steps to the subarrays of elements with smaller and greater values.

**Partitioning Example: `[6, 2, 4, 1, 3]` (pivot = 3)**
- Initial:  `[6, 2, 4, 1, 3]`  pivot=3, left=0
- i=0: 6≮3  `[6, 2, 4, 1, 3]`  left=0 (no swap)
- i=1: 2<3  `[2, 6, 4, 1, 3]`  left=1 (swap 2,6)
- i=2: 4≮3  `[2, 6, 4, 1, 3]`  left=1 (no swap)  
- i=3: 1<3  `[2, 1, 4, 6, 3]`  left=2 (swap 1,6)

- Final: Place pivot at left position
       `[2, 1, 3, 6, 4]`  ← 3 in correct position

---

## 
 Example Usage

```cpp
#include <iostream>
#include <vector>

void quickSort(std::vector<int>& arr, int s, int e);

int main() {
    std::vector<int> numbers = {6, 2, 4, 1, 3};

    quickSort(numbers, 0, numbers.size() - 1);

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

*   **Time Complexity**: 
    *   Best Case: O(n log n) - when the pivot is the median.
    *   Worst Case: O(n
) - when the pivot is the smallest or largest element.
    *   Average Case: O(n log n)
*   **Space Complexity**: O(log n) - for the recursion stack.

---

## 
 Key Characteristics

*   **Divide and Conquer**: It's a divide-and-conquer algorithm.
*   **In-place**: It does not require any extra space.
*   **Unstable**: Quick sort is not a stable sorting algorithm.

---

## 
 Class Implementation

```cpp
#include <vector>

std::vector<int> quickSort(std::vector<int>& arr, int s, int e) {
    if (e - s + 1 <= 1) {                       // Base case: array size ≤ 1
        return arr;
    }
    
    int pivot = arr[e];                         // Choose last element as pivot
    int left = s;                               // Pointer for left partition
    
    // Partition: elements smaller than pivot on left side
    for (int i = s; i < e; i++) {
        if (arr[i] < pivot) {                   // If element < pivot
            int tmp = arr[left];                // Swap with left pointer
            arr[left] = arr[i];
            arr[i] = tmp;
            left++;                             // Move left boundary
        }
    }
    
    // Move pivot between left & right partitions
    arr[e] = arr[left];                         // Swap pivot to correct position
    arr[left] = pivot;
    
    // Recursively sort both partitions
    quickSort(arr, s, left - 1);               // Sort left partition
    quickSort(arr, left + 1, e);               // Sort right partition
    
    return arr;
}
```

---

**Last Updated:** 2025-08-02
