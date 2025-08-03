# Bucket Sort Algorithm

> A sorting algorithm that works by distributing the elements of an array into a number of buckets.

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

Bucket sort, or bin sort, is a sorting algorithm that works by distributing the elements of an array into a number of buckets. Each bucket is then sorted individually, either using a different sorting algorithm, or by recursively applying the bucket sorting algorithm.

## 
 Algorithm Steps

Given a vector `arr`:

1.  **Create Buckets**: Create a number of empty buckets.
2.  **Distribute**: Scatter the elements of the input array into the buckets. Each bucket has a range of values.
3.  **Sort Buckets**: Sort each non-empty bucket.
4.  **Concatenate**: Concatenate the sorted buckets to get the final sorted array.

**Step-by-Step Example: `[2, 1, 2, 0, 0, 2]`**
- Step 1: Count frequencies
  - Original: `[2, 1, 2, 0, 0, 2]`
  - Buckets:  `counts[0] = 2`, `counts[1] = 1`, `counts[2] = 3`
- Step 2: Reconstruct array
  - n=0: Place 0 two times     → `[0, 0, _, _, _, _]`
  - n=1: Place 1 one time      → `[0, 0, 1, _, _, _]`
  - n=2: Place 2 three times   → `[0, 0, 1, 2, 2, 2]`

---

## 
 Example Usage

```cpp
#include <iostream>
#include <vector>

std::vector<int> bucketSort(std::vector<int>& arr);

int main() {
    std::vector<int> numbers = {2, 1, 2, 0, 0, 2};

    bucketSort(numbers);

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
    *   Best Case: O(n + k) - where k is the number of buckets.
    *   Worst Case: O(n
) - when all elements are in the same bucket.
    *   Average Case: O(n + k)
*   **Space Complexity**: O(n + k) - where k is the number of buckets.

---

## 
 Key Characteristics

*   **Distribution Sort**: It's a distribution sort.
*   **Not In-place**: It requires extra space for the buckets.
*   **Unstable**: Bucket sort is not a stable sorting algorithm.

---

## 
 Class Implementation

```cpp
#include <vector>

std::vector<int> bucketSort(std::vector<int>& arr) {
    // Assuming arr only contains values 0, 1, or 2
    int counts[] = {0, 0, 0};                   // Buckets for 0, 1, 2
    
    // Count frequency of each value in arr
    for (int n : arr) {
        counts[n]++;                            // Increment bucket for value n
    }
    
    // Reconstruct sorted array from buckets
    int i = 0;                                  // Position in original array
    for (int n = 0; n < 3; n++) {               // For each possible value
        for (int j = 0; j < counts[n]; j++) {   // For each occurrence
            arr[i] = n;                         // Place value in array
            i++;
        }
    }
    
    return arr;
}
```

---

**Last Updated:** 2025-08-02
