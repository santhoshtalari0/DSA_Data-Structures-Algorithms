## 1. Learning goals
- Explain hashing at a practical level.
- Use Python dictionaries as hash maps and sets as hash sets.
- Count frequencies and detect duplicates efficiently.
- Solve Two Sum, anagrams, and prefix-sum counting problems.
- Understand average-case complexity and the limits of hash-based lookup.

## 2. What is hashing?
**Hashing** maps a value to a number called a hash. Hash-based data structures use it to help locate stored data quickly.

In Python:
- A **dictionary (`dict`)** stores key-value pairs.
- A **set (`set`)** stores unique values.
- Both use hashing internally for fast average-case lookup and membership checks.

```python
student_marks = {"Asha": 92, "Ravi": 85}
print(student_marks["Asha"])  # 92
print("Ravi" in student_marks)  # True
```

Dictionary keys and set elements must be hashable. Integers, strings, and tuples containing only hashable values are common examples. Lists and dictionaries are mutable, so they cannot be keys or set elements.

## 3. Hash map operations

```python
scores = {}
scores["Asha"] = 92       # insert
scores["Ravi"] = 85
scores["Asha"] = 95       # update
print(scores["Asha"])     # 95
print("Mina" in scores)   # False
del scores["Ravi"]        # delete
print(scores.get("Mina", 0))  # 0; does not insert Mina
```

| Operation | Average time | Worst case |
|---|---:|---:|
| Insert/update | O(1) | O(n) |
| Lookup | O(1) | O(n) |
| Delete | O(1) | O(n) |
| Set membership | O(1) | O(n) |

These are average-case expectations, not guarantees for every input. Worst-case behavior can occur when many keys collide.

## 4. Hash set: unique values

Use a set when you need to know whether a value exists, rather than associate it with another value.

```python
seen = set()
seen.add(10)
seen.add(20)
seen.add(10)  # set still contains only one 10

print(20 in seen)  # True
seen.remove(20)
seen.discard(999)  # no error if absent
```

Set order is not sorted or guaranteed. Use `sorted(seen)` if sorted output is required.

## 5. Pattern: frequency counting

```python
def frequencies(items):
    count = {}
    for item in items:
        count[item] = count.get(item, 0) + 1
    return count

print(frequencies(["a", "b", "a", "c", "b", "a"]))
# {'a': 3, 'b': 2, 'c': 1}
```

Time: O(n) average. Extra space: O(k), where `k` is the number of distinct items.

Python also offers `collections.Counter`, but learn the dictionary pattern first.

## 6. Pattern: detect duplicates

```python
def contains_duplicate(nums):
    seen = set()
    for value in nums:
        if value in seen:
            return True
        seen.add(value)
    return False

print(contains_duplicate([4, 2, 7, 2]))  # True
print(contains_duplicate([4, 2, 7, 9]))  # False
```

Time: O(n) average. Extra space: O(n). A sorting-based solution usually takes O(n log n) time.

## 7. Pattern: Two Sum

Given an array and a target, return indices of two distinct elements that add up to the target. Assume exactly one answer exists.

Example: `nums = [2, 7, 11, 15]`, `target = 9` → `[0, 1]`.

For each value `x`, the required partner is `target - x`. Check whether that partner appeared earlier; if not, store the current value and index.

```python
def two_sum(nums, target):
    index_by_value = {}
    for i, value in enumerate(nums):
        needed = target - value
        if needed in index_by_value:
            return [index_by_value[needed], i]
        index_by_value[value] = i
    return []

print(two_sum([2, 7, 11, 15], 9))  # [0, 1]
print(two_sum([3, 3], 6))          # [0, 1]
```

Time: O(n) average. Extra space: O(n). Checking before inserting ensures the two indices are distinct.

## 8. Pattern: anagram check

Two strings are anagrams when they contain the same characters with the same frequencies.

```python
from collections import Counter

def are_anagrams(first, second):
    return Counter(first) == Counter(second)

print(are_anagrams("listen", "silent"))  # True
print(are_anagrams("hello", "world"))    # False
```

Dictionary implementation:

```python
def are_anagrams(first, second):
    if len(first) != len(second):
        return False

    counts = {}
    for char in first:
        counts[char] = counts.get(char, 0) + 1

    for char in second:
        if char not in counts:
            return False
        counts[char] -= 1
        if counts[char] < 0:
            return False

    return True
```

This compares exact characters, including case and spaces. Normalize the strings first only if the problem asks you to ignore them.

Time: O(n) average. Extra space: O(k), where `k` is the number of distinct characters.

## 9. Pattern: first non-repeating character

Return the index of the first character with frequency one, or `-1` if none exists.

```python
def first_unique_index(text):
    count = {}
    for char in text:
        count[char] = count.get(char, 0) + 1

    for i, char in enumerate(text):
        if count[char] == 1:
            return i
    return -1

print(first_unique_index("leetcode"))  # 0
print(first_unique_index("aabb"))      # -1
```

Time: O(n) average. Extra space: O(k). The second pass preserves original order.

## 10. Pattern: intersection of two arrays

Return the distinct values present in both arrays.

```python
def intersection(nums1, nums2):
    values = set(nums1)
    result = set()
    for value in nums2:
        if value in values:
            result.add(value)
    return list(result)

print(sorted(intersection([1, 2, 2, 3], [2, 2, 4])))  # [2]
```

The returned order is not guaranteed. Time: O(n + m) average. Extra space: O(n + m).

## 11. Pattern: group anagrams

A sorted word can act as a shared key for words with the same letters.

```python
def group_anagrams(words):
    groups = {}
    for word in words:
        key = "".join(sorted(word))
        groups.setdefault(key, []).append(word)
    return list(groups.values())

print(group_anagrams(["eat", "tea", "tan", "ate", "nat", "bat"]))
# Example groups: [['eat', 'tea', 'ate'], ['tan', 'nat'], ['bat']]
```

Group order is not important unless specified. Sorting each word of length `L` costs O(L log L). With a fixed small alphabet, a character-frequency tuple can be used as a key instead.

## 12. Prefix sums plus hashing: subarray sum equals k

Count contiguous subarrays whose sum equals `k`. If the current prefix sum is `prefix`, a previous prefix sum equal to `prefix - k` identifies a subarray with sum `k`.

```python
def count_subarrays_sum_k(nums, k):
    prefix_count = {0: 1}
    prefix = 0
    answer = 0

    for value in nums:
        prefix += value
        answer += prefix_count.get(prefix - k, 0)
        prefix_count[prefix] = prefix_count.get(prefix, 0) + 1

    return answer

print(count_subarrays_sum_k([1, 1, 1], 2))  # 2
print(count_subarrays_sum_k([1, -1, 0], 0)) # 3
```

Time: O(n) average. Extra space: O(n). Starting with `{0: 1}` accounts for a valid subarray beginning at index zero. This technique also works with negative numbers.

## 13. Hash collisions: practical understanding

A **collision** occurs when different keys map to the same hash value or storage area. Hash tables handle collisions internally. A collision does not mean two values are equal; equality checks still matter.

In normal Python DSA work:
- Use built-in dictionaries and sets.
- Use immutable, hashable keys.
- Do not assume set iteration order is sorted.
- Expect average-case O(1) lookup, not a strict worst-case guarantee.
- Avoid changing an object's hash-relevant state while it is used as a key.

You generally do not need to implement a hash table from scratch unless the problem asks for it.

## 14. Common mistakes
1. Using a list for repeated membership checks: `value in list` is O(n); a set is usually better.
2. Overwriting a frequency instead of incrementing it: use `count[x] = count.get(x, 0) + 1`.
3. Inserting the current value before checking Two Sum: it may match itself.
4. Forgetting duplicate values: Two Sum still requires distinct indices.
5. Assuming set order: sort output if order matters.
6. Using mutable keys: lists and dictionaries cannot be keys or set elements.
7. Ignoring normalization rules: case, whitespace, and punctuation are ignored only if you explicitly normalize them.
8. Confusing average and worst-case complexity.

## 15. Complexity recap

| Pattern | Average time | Extra space |
|---|---:|---:|
| Frequency count | O(n) | O(k) |
| Duplicate detection | O(n) | O(n) |
| Two Sum | O(n) | O(n) |
| Anagram frequency check | O(n) | O(k) |
| First unique character | O(n) | O(k) |
| Array intersection | O(n + m) | O(n + m) |
| Subarray sum equals k | O(n) | O(n) |

Here `n` and `m` are input lengths; `k` is the number of distinct values or characters where applicable.

## Quick self-check
- When should you use a dictionary versus a set?
- Why are hash-map lookups average O(1)?
- How does Two Sum avoid using one index twice?
- Why does `{0: 1}` matter in prefix-sum counting?
- Why is a set not a replacement for a frequency map?
