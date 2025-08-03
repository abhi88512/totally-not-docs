# Merge Sort Algorithm

> A divide-and-conquer algorithm that divides the array into two halves, sorts them, and then merges them back together.

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

Merge sort is a classic divide-and-conquer algorithm. It works by recursively breaking down the array into two halves until each subarray has only one element. Then, it merges the sorted subarrays back together to produce a single sorted array.

## 
 Algorithm Steps

Given a vector `arr`:

1.  **Divide**: Recursively divide the array into two halves until the size of the subarray is 1.
2.  **Conquer**: Merge the two sorted subarrays back together. This is the key part of the algorithm.
3.  **Merge**: To merge two sorted subarrays, we use a temporary array and two pointers, one for each subarray. We compare the elements at the pointers and copy the smaller element to the temporary array. We repeat this until one of the subarrays is empty. Then, we copy the remaining elements from the other subarray.

**Visual Example: `[3, 2, 4, 1, 6]`**
           `[3, 2, 4, 1, 6]`
           /               \
      `[3, 2, 4]`           `[1, 6]`
      /       \           /     \
   `[3, 2]`    `[4]`       `[1]`     `[6]`
   /    \      |        |       |
  `[3]`   `[2]`   `[4]`      `[1]`     `[6]`
   \    /      |        |       |
   `[2, 3]`     `[4]`      `[1]`     `[6]`
      \        /        \       /
      `[2, 3, 4]`         `[1, 6]`
           \               /
           `[1, 2, 3, 4, 6]`

---

## 
 Example Usage

```cpp
#include <iostream>
#include <vector>

void mergeSort(std::vector<int>& arr, int s, int e);
void merge(std::vector<int>& arr, int s, int m, int e);

int main() {
    std::vector<int> numbers = {3, 2, 4, 1, 6};

    mergeSort(numbers, 0, numbers.size() - 1);

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
*   **Space Complexity**: O(n) - Requires temporary arrays for merging.

---

## 
 Key Characteristics

*   **Divide and Conquer**: A classic example of this algorithmic paradigm.
*   **Stability**: Merge sort is a stable sorting algorithm.
*   **Not In-place**: It requires extra space for the temporary arrays.

---

## 
 Class Implementation

```cpp
#include <vector>

void merge(std::vector<int>& arr, int s, int m, int e) {
    // Copy sorted left & right halves to temp arrays
    std::vector<int> L = {arr.begin() + s, arr.begin() + m + 1};
    std::vector<int> R = {arr.begin() + m + 1, arr.begin() + e + 1};
    
    int i = 0;      // Index for L (left subarray)
    int j = 0;      // Index for R (right subarray)  
    int k = s;      // Index for arr (main array)
    
    // Merge using two-pointer technique
    while (i < L.size() && j < R.size()) {
        if (L[i] <= R[j]) {                     // ≤ ensures stability
            arr[k] = L[i++];
        } else {
            arr[k] = R[j++];
        }
        k++;
    }
    
    // Copy remaining elements (if any)
    while (i < L.size()) {
        arr[k++] = L[i++];
    }
    while (j < R.size()) {
        arr[k++] = R[j++];
    }
}

std::vector<int> mergeSort(std::vector<int>& arr, int s, int e) {
    if (e - s + 1 <= 1) {                       // Base case: array size ≤ 1
        return arr;
    }
    
    int m = s + (e - s) / 2;                        // Find middle index
    
    mergeSort(arr, s, m);                       // Sort left half
    mergeSort(arr, m + 1, e);                   // Sort right half
    merge(arr, s, m, e);                        // Merge sorted halves
    
    return arr;
}
```

---

**Last Updated:** 2025-08-02
