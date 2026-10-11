# Day 09 — Searching Algorithms

> Goal: Learn how to find values efficiently, especially in sorted arrays. Earlier array and recursion basics are assumed.

## 1. What Is Searching?
Searching means finding whether a target exists and, often, returning its index.

- **Linear search:** checks elements one by one; works on sorted or unsorted data.
- **Binary search:** repeatedly halves the search range; requires sorted data or another valid monotonic condition.

## 2. Linear Search
```python
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1
```
Example: `linear_search([7, 4, 9, 2], 9)` → `2`.

- Best time: `O(1)`.
- Worst time: `O(n)`.
- Extra space: `O(1)`.

Use it for unsorted data, small inputs, or when only one search is needed.

## 3. Binary Search: Core Idea
Binary search works on sorted arrays. Check the middle:
- Equal to target → found.
- Middle value smaller → continue right.
- Middle value larger → continue left.

Each step removes about half the candidates. Time: **O(log n)**.

## 4. Iterative Binary Search
```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```
Example: `binary_search([2, 4, 7, 9, 12, 15], 9)` → `3`.

Dry run:
```text
left=0, right=5, mid=2 → value 7 < 9 → left=3
left=3, right=5, mid=4 → value 12 > 9 → right=3
left=3, right=3, mid=3 → value 9 → found
```

Time: **O(log n)**; extra space: **O(1)**. `left <= right` is used because both endpoints are included.

## 5. Binary Search Boundary Rules
- Start with `left = 0`, `right = len(arr) - 1`.
- For a closed interval, use `while left <= right`.
- If middle is too small, set `left = mid + 1`.
- If middle is too large, set `right = mid - 1`.
- Return `-1` when the target is absent.

Not moving past `mid` can cause an infinite loop.

## 6. Recursive Binary Search
This applies the recursion concepts from Day 6.

```python
def binary_search_recursive(arr, target, left, right):
    if left > right:
        return -1

    mid = left + (right - left) // 2

    if arr[mid] == target:
        return mid
    if arr[mid] < target:
        return binary_search_recursive(arr, target, mid + 1, right)

    return binary_search_recursive(arr, target, left, mid - 1)
```
Call:
```python
arr = [2, 4, 7, 9, 12, 15]
print(binary_search_recursive(arr, 9, 0, len(arr) - 1))
```
Output: `3`. Time: **O(log n)**; call-stack space: **O(log n)**.

## 7. First Occurrence
Ordinary binary search may return any matching duplicate. Save a match and continue left.

```python
def first_occurrence(arr, target):
    left, right = 0, len(arr) - 1
    answer = -1

    while left <= right:
        mid = left + (right - left) // 2
        if arr[mid] == target:
            answer = mid
            right = mid - 1
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return answer
```
`first_occurrence([1, 2, 2, 2, 4, 6], 2)` → `1`. Time: **O(log n)**; space: **O(1)**.

## 8. Last Occurrence
Save a match and continue right.

```python
def last_occurrence(arr, target):
    left, right = 0, len(arr) - 1
    answer = -1

    while left <= right:
        mid = left + (right - left) // 2
        if arr[mid] == target:
            answer = mid
            left = mid + 1
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return answer
```
`last_occurrence([1, 2, 2, 2, 4, 6], 2)` → `3`. Time: **O(log n)**; space: **O(1)**.

## 9. Lower Bound
The **lower bound** is the first index whose value is `>= target`. If none exists, return `len(arr)`.

```python
def lower_bound(arr, target):
    left, right = 0, len(arr)

    while left < right:
        mid = left + (right - left) // 2
        if arr[mid] < target:
            left = mid + 1
        else:
            right = mid

    return left
```
Examples:
```python
lower_bound([1, 3, 3, 5, 8], 3)  # 1
lower_bound([1, 3, 3, 5, 8], 4)  # 3
lower_bound([1, 3, 3, 5, 8], 9)  # 5
```
Time: **O(log n)**; space: **O(1)**.

## 10. Upper Bound
The **upper bound** is the first index whose value is `> target`.

```python
def upper_bound(arr, target):
    left, right = 0, len(arr)

    while left < right:
        mid = left + (right - left) // 2
        if arr[mid] <= target:
            left = mid + 1
        else:
            right = mid

    return left
```
`upper_bound([1, 3, 3, 5, 8], 3)` → `3`.

For a sorted array:
```text
count(target) = upper_bound(target) - lower_bound(target)
```
```python
def count_occurrences(arr, target):
    return upper_bound(arr, target) - lower_bound(arr, target)
```

## 11. Search Insert Position
Return the existing target index, or where it should be inserted to keep the array sorted. This is the lower-bound position.

```python
def search_insert_position(arr, target):
    return lower_bound(arr, target)
```
For `[1, 3, 5, 6]` and target `2`, the answer is `1`.

## 12. Search in a Rotated Sorted Array
Example rotated array: `[4, 5, 6, 7, 0, 1, 2]`. With distinct values, one half around the midpoint is sorted.

```python
def search_rotated(arr, target):
    left, right = 0, len(arr) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if arr[mid] == target:
            return mid

        if arr[left] <= arr[mid]:
            if arr[left] <= target < arr[mid]:
                right = mid - 1
            else:
                left = mid + 1
        else:
            if arr[mid] < target <= arr[right]:
                left = mid + 1
            else:
                right = mid - 1

    return -1
```
`search_rotated([4, 5, 6, 7, 0, 1, 2], 0)` → `4`.  
Assumption: distinct values. Time: **O(log n)**; extra space: **O(1)**.

## 13. Binary Search on an Answer
Sometimes we search for the smallest or largest answer that satisfies a condition, not for an array value.

This requires a **monotonic condition**: once it changes from false to true (or true to false), it does not change back.

```text
candidate:  1  2  3  4  5  6  7
works?:     F  F  F  T  T  T  T
                     ↑ first valid answer
```
Binary search can find the boundary in **O(log n)** condition checks if each check is efficient. Examples include minimum feasible capacity or minimum time needed.

## 14. Common Mistakes
1. Applying binary search to unsorted data without a monotonic condition.
2. Mixing up interval conventions (`left <= right` vs `left < right`).
3. Forgetting `mid + 1` or `mid - 1`, causing a stalled loop.
4. Returning any match when first/last occurrence is requested.
5. Confusing lower bound (`>= target`) with upper bound (`> target`).
6. Not defining the result when the target is absent.
7. Forgetting duplicate values when designing boundaries.
8. Using a distinct-value rotated-array algorithm on inputs with duplicates.

## 15. Complexity Comparison

| Algorithm | Requirement | Time | Extra space |
|---|---|---:|---:|
| Linear search | Any array | O(n) worst case | O(1) |
| Iterative binary search | Sorted array | O(log n) | O(1) |
| Recursive binary search | Sorted array | O(log n) | O(log n) |
| First/last occurrence | Sorted array | O(log n) | O(1) |
| Lower/upper bound | Sorted array | O(log n) | O(1) |
| Rotated-array search | Rotated sorted array, distinct values | O(log n) | O(1) |

---

# Practice Problems

## Beginner
1. Implement linear search.
2. Implement iterative binary search.
3. Implement recursive binary search.
4. Find the first occurrence of a target in a sorted array.
5. Find the last occurrence of a target.
6. Count target occurrences in a sorted array.
7. Find the lower bound of a target.
8. Find the upper bound of a target.
9. Find the search-insert position.
10. Find the first index whose value is greater than a target.

## Intermediate
11. Search in a rotated sorted array with distinct elements.
12. Find the minimum in a rotated sorted array.
13. Find a peak element.
14. Find the integer square root of a non-negative integer using binary search.
15. Find the first true value in a monotonic condition.
16. Find the smallest feasible capacity for a shipping problem.
17. Search a sorted 2D matrix.
18. Find the first and last positions of a target.
19. Find the single element in a sorted array where all others appear twice.
20. Find the median of two sorted arrays (challenge).

---

# Quick Revision
- Linear search works on sorted or unsorted data and takes **O(n)** worst-case time.
- Binary search requires sorted data or a monotonic condition.
- Binary search halves the candidate range, giving **O(log n)** time.
- Lower bound: first value `>= target`.
- Upper bound: first value `> target`.
- First/last occurrence are boundary-search patterns.
- Binary search on an answer requires monotonic feasibility.

> **Golden rule:** Before using binary search, identify the sorted order or monotonic condition that lets you safely discard half the search space.

## Day 10 Preview
**Sorting Algorithms** — bubble, selection, insertion, merge, and quick sort, with dry runs and complexity comparisons.
