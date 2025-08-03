# Bubble Sort Algorithm

> A simple sorting algorithm that repeatedly steps through the list, compares adjacent elements and swaps them if they are in the wrong order.

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

Bubble sort is a basic algorithm that is easy to understand. It works by comparing adjacent elements and swapping them if they are in the wrong order. The largest element "bubbles up" to the end of the list in each pass.

## 
 Algorithm Steps

Given a vector `arr`:

1.  Iterate from `i = 0` to `n-2`, where `n` is the size of the array. This is for the number of passes.
2.  In each pass, iterate from `j = 0` to `n-i-2`. This is for comparing adjacent elements.
3.  If `arr[j]` is greater than `arr[j+1]`, swap them.
4.  After `n-1` passes, the array will be sorted.

**Step-by-Step Example: `[64, 34, 25, 12]`**
- Pass 1: `[34, 25, 12, 64]`  -> 64 bubbled to end
- Pass 2: `[25, 12, 34, 64]`  -> 34 bubbled to position
- Pass 3: `[12, 25, 34, 64]`  -> 25 bubbled to position

---

## 
 Example Usage

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // For std::swap

void bubbleSort(std::vector<int>& arr);

int main() {
    std::vector<int> numbers = {64, 34, 25, 12, 22, 11, 90};

    bubbleSort(numbers);

    std::cout << "Sorted array: \n";
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << "\n";

    return 0;
}
```

---

## 
 Time & Space Complexity

*   **Time Complexity**: O(n
) - Slow but easy to understand.
    *   Best Case: O(n) - if the array is already sorted.
    *   Worst Case: O(n
)
    *   Average Case: O(n
)
*   **Space Complexity**: O(1) - In-place sorting.

---

## 
 Key Characteristics

*   **Simplicity**: One of the simplest sorting algorithms to understand and implement.
*   **Stability**: Bubble sort is a stable sorting algorithm.
*   **In-place**: It does not require any extra space.

---

## 
 Class Implementation

```cpp
#include <vector>
#include <algorithm> // For std::swap

void bubbleSort(std::vector<int>& arr) {
    int n = arr.size();
    
    for(int i = 0; i < n-1; i++) {              // n-1 passes
        for(int j = 0; j < n-i-1; j++) {        // Compare adjacent elements
            if(arr[j] > arr[j+1]) {             // If wrong order
                std::swap(arr[j], arr[j+1]);         // Swap them
            }
        }
    }
}
```