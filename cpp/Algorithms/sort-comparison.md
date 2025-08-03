# Sorting Algorithm Comparison

This file provides a comparison of different sorting algorithms and links to their detailed explanations.

## Comparison Table

| Algorithm | Time Complexity (Best) | Time Complexity (Average) | Time Complexity (Worst) | Space Complexity | Stable |
|---|---|---|---|---|---|
| [Bubble Sort](./bubble-sort.md) | O(n) | O(n²) | O(n²) | O(1) | Yes |
| [Selection Sort](./selection-sort.md) | O(n²) | O(n²) | O(n²) | O(1) | No |
| [Insertion Sort](./insertion-sort.md) | O(n) | O(n²) | O(n²) | O(1) | Yes |
| [Merge Sort](./merge-sort.md) | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| [Quick Sort](./quick-sort.md) | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| [Heap Sort](./heap-sort.md) | O(n log n) | O(n log n) | O(n log n) | O(1) | No |
| [Bucket Sort](./bucket-sort.md) | O(n + k) | O(n + k) | O(n²) | O(k) | No |

**Note:**
*   `k` = number of buckets for bucket sort
*   **Stable** = preserves relative order of equal elements

## When to Use Which Algorithm?

| Scenario | Best Choice |
|---|---|
| Small arrays (< 50) | [Insertion Sort](./insertion-sort.md) |
| Nearly sorted | [Insertion Sort](./insertion-sort.md) |
| Large random data | [Quick Sort](./quick-sort.md) |
| Worst-case guarantee | [Merge Sort](./merge-sort.md) |
| Memory limited | [Heap Sort](./heap-sort.md) |
| Stable sorting | [Merge Sort](./merge-sort.md) |
| Known small range | [Bucket Sort](./bucket-sort.md) |

---

**Last Updated:** 2025-08-02
