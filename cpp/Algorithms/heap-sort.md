# Heap Sort Algorithm

> A comparison-based sorting algorithm that uses a binary heap data structure.

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

Heap sort is a comparison-based sorting technique based on a binary heap data structure. It is similar to selection sort where we first find the maximum element and place the maximum element at the end. We repeat the same process for the remaining elements.

## 
 Algorithm Steps

Given a vector `arr`:

1.  **Build Max Heap**: Build a max heap from the input data. A max heap is a complete binary tree where the value of each node is greater than or equal to the value of its children.
2.  **Heapify**: The process of rearranging the heap to maintain the heap property.
3.  **Sort**: Repeatedly extract the maximum element from the heap (which is always the root) and place it at the end of the array. After extracting the maximum element, we heapify the remaining heap.

---

## 
 Example Usage

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // For std::swap

void heapify(std::vector<int>& arr, int n, int i);
void heapSort(std::vector<int>& arr);

int main() {
    std::vector<int> numbers = {12, 11, 13, 5, 6, 7};

    heapSort(numbers);

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

*   **Time Complexity**: O(n log n) - in all cases.
    *   Best Case: O(n log n)
    *   Worst Case: O(n log n)
    *   Average Case: O(n log n)
*   **Space Complexity**: O(1) - In-place sorting.

---

## 
 Key Characteristics

*   **Comparison-based**: It is a comparison-based sorting algorithm.
*   **In-place**: It does not require any extra space.
*   **Not Stable**: Heap sort is not a stable sorting algorithm.

---

## 
 Class Implementation

```cpp
#include <vector>
#include <algorithm> // For std::swap

void heapify(std::vector<int>& arr, int n, int i) {
    int largest = i;                           // Initialize largest as root
    int left = 2 * i + 1;                      // Left child
    int right = 2 * i + 2;                     // Right child
    
    if(left < n && arr[left] > arr[largest])   // If left child is larger
        largest = left;
    
    if(right < n && arr[right] > arr[largest]) // If right child is larger
        largest = right;
    
    if(largest != i) {                         // If largest is not root
        std::swap(arr[i], arr[largest]);
        heapify(arr, n, largest);              // Recursively heapify affected subtree
    }
}

void heapSort(std::vector<int>& arr) {
    int n = arr.size();
    
    // Build max heap
    for(int i = n / 2 - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }
    
    // Extract elements from heap one by one
    for(int i = n - 1; i > 0; i--) {
        std::swap(arr[0], arr[i]);                  // Move current root to end
        heapify(arr, i, 0);                    // Heapify reduced heap
    }
}
```

---

**Last Updated:** 2025-08-02
