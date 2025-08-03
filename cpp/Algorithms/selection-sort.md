# Selection Sort Algorithm

> A simple sorting algorithm that repeatedly finds the minimum element from the unsorted part and puts it at the beginning.

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

Selection sort is a simple sorting algorithm that works by repeatedly finding the minimum element from the unsorted part of the array and putting it at the beginning. The algorithm maintains two subarrays in a given array: the subarray which is already sorted, and the remaining subarray which is unsorted.

## 
 Algorithm Steps

Given a vector `arr`:

1.  Iterate from `i = 0` to `n-2`, where `n` is the size of the array. This is for the number of passes.
2.  In each pass, assume the first element of the unsorted part is the minimum.
3.  Iterate through the unsorted part of the array to find the actual minimum element.
4.  Swap the found minimum element with the first element of the unsorted part.

**Step-by-Step Example: `[64, 25, 12, 22, 11]`**
- Pass 1: Find min (11), swap with first  → `[11, 25, 12, 22, 64]`
- Pass 2: Find min (12), swap with second → `[11, 12, 25, 22, 64]`
- Pass 3: Find min (22), swap with third  → `[11, 12, 22, 25, 64]`
- Pass 4: Find min (25), already in place → `[11, 12, 22, 25, 64]`

---

## 
 Example Usage

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // For std::swap

void selectionSort(std::vector<int>& arr);

int main() {
    std::vector<int> numbers = {64, 25, 12, 22, 11, 90};

    selectionSort(numbers);

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
) - The number of comparisons is high.
    *   Best Case: O(n
)
    *   Worst Case: O(n
)
    *   Average Case: O(n
)
*   **Space Complexity**: O(1) - In-place sorting.

---

## 
 Key Characteristics

*   **Simplicity**: Easy to understand and implement.
*   **In-place**: It does not require any extra space.
*   **Fewer Swaps**: Compared to bubble sort, it performs fewer swaps.

---

## 
 Class Implementation

```cpp
#include <vector>
#include <algorithm> // For std::swap

void selectionSort(std::vector<int>& arr) {
    int n = arr.size();
    
    for(int i = 0; i < n-1; i++) {              // For each position
        int minIndex = i;                       // Assume current is minimum
        
        for(int j = i+1; j < n; j++) {          // Find actual minimum
            if(arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        
        std::swap(arr[i], arr[minIndex]);            // Place minimum at position i
    }
}
```

---

**Last Updated:** 2025-08-02
