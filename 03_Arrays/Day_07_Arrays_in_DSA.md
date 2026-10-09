# Day 07 — Arrays in DSA

> Goal: Learn array problem-solving patterns without repeating Python list basics from Day 3.

## 1. Array Traversal
An array stores ordered elements accessible by index. In Python, lists are commonly used for array practice.

```python
arr = [12, 5, 8, 20, 3]
for i in range(len(arr)):
    print(arr[i])
```

Visiting all elements takes **O(n)** time.

## 2. Largest and Smallest Elements

```python
def largest(arr):
    if not arr:
        return None
    best = arr[0]
    for value in arr[1:]:
        if value > best:
            best = value
    return best
```

```python
def smallest(arr):
    if not arr:
        return None
    best = arr[0]
    for value in arr[1:]:
        if value < best:
            best = value
    return best
```

Time: **O(n)**. Extra space: **O(1)**.

## 3. Second Largest Distinct Element

```python
def second_largest(arr):
    largest = None
    second = None

    for value in arr:
        if largest is None or value > largest:
            second = largest
            largest = value
        elif value != largest and (second is None or value > second):
            second = value

    return second
```

Returns `None` if there is no second distinct value. Time: **O(n)**; extra space: **O(1)**.

## 4. Linear Search

```python
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1
```

Returns the first matching index, or `-1` if absent. Worst-case time: **O(n)**; extra space: **O(1)**.

## 5. Reverse an Array In Place

```python
def reverse_array(arr):
    left, right = 0, len(arr) - 1

    while left < right:
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1

    return arr
```

Time: **O(n)**; extra space: **O(1)**.

Dry run for `[1, 2, 3, 4, 5]`:
- Swap indexes 0 and 4 → `[5, 2, 3, 4, 1]`
- Swap indexes 1 and 3 → `[5, 4, 3, 2, 1]`
- Stop when pointers meet or cross.

## 6. Check Whether an Array Is Sorted

```python
def is_sorted(arr):
    for i in range(len(arr) - 1):
        if arr[i] > arr[i + 1]:
            return False
    return True
```

Time: **O(n)**; extra space: **O(1)**.

## 7. Move All Zeros to the End

Keep non-zero values in their original relative order.

```python
def move_zeros(arr):
    position = 0

    for i in range(len(arr)):
        if arr[i] != 0:
            arr[position], arr[i] = arr[i], arr[position]
            position += 1

    return arr
```

Example: `[0, 1, 0, 3, 12]` becomes `[1, 3, 12, 0, 0]`.  
Time: **O(n)**; extra space: **O(1)**. This is a **two-pointer** pattern.

## 8. Remove Duplicates From a Sorted Array

```python
def remove_duplicates_sorted(arr):
    if len(arr) == 0:
        return 0

    write = 1
    for read in range(1, len(arr)):
        if arr[read] != arr[write - 1]:
            arr[write] = arr[read]
            write += 1

    return write
```

Example: `[1, 1, 2, 2, 3]` returns count `3`; the first three elements become `[1, 2, 3]`. The array must be sorted. Time: **O(n)**; extra space: **O(1)**.

## 9. Rotate Right by One

```python
def rotate_right_one(arr):
    if len(arr) <= 1:
        return arr

    last = arr[-1]
    for i in range(len(arr) - 1, 0, -1):
        arr[i] = arr[i - 1]
    arr[0] = last
    return arr
```

`[1, 2, 3, 4]` becomes `[4, 1, 2, 3]`. Time: **O(n)**; extra space: **O(1)**.

## 10. Rotate Right by K

```python
def rotate_right(arr, k):
    n = len(arr)
    if n == 0:
        return arr
    k %= n

    def reverse_part(left, right):
        while left < right:
            arr[left], arr[right] = arr[right], arr[left]
            left += 1
            right -= 1

    reverse_part(0, n - 1)
    reverse_part(0, k - 1)
    reverse_part(k, n - 1)
    return arr
```

Example: rotating `[1, 2, 3, 4, 5]` right by 2 gives `[4, 5, 1, 2, 3]`.

Why: reverse the entire array, reverse the first `k` values, then reverse the rest.  
Time: **O(n)**; extra space: **O(1)**.

## 11. Prefix Sums

A prefix sum stores the sum from the start through each index.

For `[2, 4, 1, 5]`, the prefix sums are `[2, 6, 7, 12]`.

```python
def build_prefix(arr):
    prefix = []
    running_sum = 0

    for value in arr:
        running_sum += value
        prefix.append(running_sum)

    return prefix
```

For an inclusive range `[left, right]`:

```python
def range_sum(prefix, left, right):
    if left == 0:
        return prefix[right]
    return prefix[right] - prefix[left - 1]
```

Preprocessing: **O(n)** time and space. Each range query: **O(1)** time.

## 12. Sliding Window — Maximum Sum of Size K

A subarray is a **contiguous** part of an array.

```python
def max_sum_subarray_k(arr, k):
    if k <= 0 or k > len(arr):
        return None

    window_sum = sum(arr[:k])
    best = window_sum

    for right in range(k, len(arr)):
        window_sum += arr[right] - arr[right - k]
        best = max(best, window_sum)

    return best
```

Example: `[2, 1, 5, 1, 3, 2]`, `k = 3` → `9`, from `[5, 1, 3]`.

Time: **O(n)**; extra space: **O(1)**. Each move removes the element leaving the window and adds the new one.

## 13. Two Pointers — Pair Sum in a Sorted Array

```python
def has_pair_sum_sorted(arr, target):
    left, right = 0, len(arr) - 1

    while left < right:
        total = arr[left] + arr[right]

        if total == target:
            return True
        if total < target:
            left += 1
        else:
            right -= 1

    return False
```

Example: `[1, 2, 4, 6, 8]`, target `10` → `True`. The array must be sorted.  
Time: **O(n)**; extra space: **O(1)**.

## 14. Kadane's Algorithm — Maximum Subarray Sum

Find the maximum sum of any non-empty contiguous subarray.

```python
def max_subarray_sum(arr):
    if not arr:
        return None

    current = best = arr[0]

    for value in arr[1:]:
        current = max(value, current + value)
        best = max(best, current)

    return best
```

Example: `[-2, 1, -3, 4, -1, 2, 1, -5, 4]` → `6`, from `[4, -1, 2, 1]`.

At each value, either start a new subarray or extend the current one.  
Time: **O(n)**; extra space: **O(1)**. Initializing with the first element correctly handles all-negative arrays.

## 15. Common Mistakes

1. Off-by-one errors when accessing `arr[i + 1]`.
2. Accessing `arr[0]` when the array may be empty.
3. Confusing an index with the value at that index.
4. Using a sorted-array technique on unsorted input.
5. Overwriting values before they are used.
6. Forgetting to clarify whether “second largest” means distinct.
7. Confusing a subarray (contiguous) with a subsequence (not necessarily contiguous).
8. Mixing up left and right rotation.

## 16. Complexity Reference

| Technique | Time | Extra space |
|---|---:|---:|
| Traversal | O(n) | O(1) |
| Min/max | O(n) | O(1) |
| Linear search | O(n) worst case | O(1) |
| Reverse in place | O(n) | O(1) |
| Check sorted | O(n) | O(1) |
| Move zeros | O(n) | O(1) |
| Remove duplicates from sorted array | O(n) | O(1) |
| Build prefix sums | O(n) | O(n) |
| Prefix range query | O(1) per query | O(1) |
| Fixed-size sliding window | O(n) | O(1) |
| Two-pointer pair sum (sorted) | O(n) | O(1) |
| Kadane's algorithm | O(n) | O(1) |

---

# Practice Problems

## Beginner
1. Find the largest element.
2. Find the smallest element.
3. Find the second largest distinct element.
4. Return the index of a target.
5. Reverse an array in place.
6. Check whether an array is sorted.
7. Count even and odd values.
8. Move all zeros to the end.
9. Rotate right by one.
10. Find the missing number from `0` through `n`, with one missing.

## Intermediate
11. Remove duplicates from a sorted array in place.
12. Rotate right by `k`.
13. Build prefix sums and answer range-sum queries.
14. Find whether a sorted array has a pair with a target sum.
15. Find the maximum sum of a subarray of size `k`.
16. Find maximum subarray sum using Kadane's algorithm.
17. Find the intersection of two sorted arrays.
18. Merge two sorted arrays.
19. Find a majority element if one exists.
20. Find the longest run of consecutive ones.

---

# Quick Revision

- Traversal and linear search take **O(n)** time.
- Two pointers reduce repeated work in suitable problems.
- Prefix sums speed up repeated range-sum queries.
- Sliding window is useful for contiguous ranges.
- Kadane's algorithm finds maximum subarray sum in linear time.
- Check assumptions: empty input, sorted order, duplicates, and rotation direction.

> **Golden rule:** Identify whether the problem calls for traversal, two pointers, prefix sums, sliding window, or a running best value before coding.

## Day 8 Preview
**Strings and String Problem-Solving Patterns** — focused on algorithms, not repeated basic Python string operations.
