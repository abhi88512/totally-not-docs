
### LeetCode Pattern Identification

* **Stack Patterns**:
    * **Optimization of $O(N^2)$ Brute Force**: Occurs when an $O(N^2)$ solution involves nested loops where `j`'s value or condition depends on `i` (e.g., `j = f(i)` for `j > i` or `j < i`). Stacks often optimize this to $O(N)$.

* **Binary Search Patterns**:
    * **Sorted/Nearly Sorted Data**: The input array/list/collection is sorted or comprises sorted segments (e.g., rotated sorted array).

* **Heap Patterns**:
    * **Two Keypoints**: Problems involve K and finding the Smallest or Largest elements.
    * **Which Heap min or max?**: For "K smallest" elements, use a max-heap; for "K largest" elements, use a min-heap.


