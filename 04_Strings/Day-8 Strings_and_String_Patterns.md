
## 1. String Problem-Solving
A string is an ordered sequence of characters. In Python, strings are immutable, so algorithms usually create a new string or use a list of characters when modifications are needed.

## 2. Character Frequency
```python
def character_frequency(text):
    freq = {}
    for ch in text:
        freq[ch] = freq.get(ch, 0) + 1
    return freq
```
`character_frequency("banana")` → `{'b': 1, 'a': 3, 'n': 2}`.  
Time: **O(n)** average; extra space: **O(k)**, where `k` is the number of distinct characters.

## 3. Count Vowels and Consonants
This counts English letters and ignores spaces, digits, and punctuation.

```python
def count_vowels_consonants(text):
    vowels = set("aeiouAEIOU")
    vowel_count = consonant_count = 0

    for ch in text:
        if ch.isalpha():
            if ch in vowels:
                vowel_count += 1
            else:
                consonant_count += 1

    return vowel_count, consonant_count
```
`count_vowels_consonants("Hello World!")` → `(3, 7)`.  
Time: **O(n)**; extra space: **O(1)**.

## 4. Reverse a String With Two Pointers
```python
def reverse_string(text):
    chars = list(text)
    left, right = 0, len(chars) - 1

    while left < right:
        chars[left], chars[right] = chars[right], chars[left]
        left += 1
        right -= 1

    return "".join(chars)
```
`reverse_string("hello")` → `"olleh"`.  
Time: **O(n)**; extra space: **O(n)** for the character list and output.

## 5. Exact Palindrome Check
A palindrome reads the same forward and backward, such as `"level"`.

```python
def is_palindrome(text):
    left, right = 0, len(text) - 1

    while left < right:
        if text[left] != text[right]:
            return False
        left += 1
        right -= 1

    return True
```
This version is case-sensitive and includes spaces/punctuation.  
Time: **O(n)** worst case; extra space: **O(1)**.

## 6. Palindrome Ignoring Case and Punctuation
```python
def clean_palindrome(text):
    left, right = 0, len(text) - 1

    while left < right:
        while left < right and not text[left].isalnum():
            left += 1
        while left < right and not text[right].isalnum():
            right -= 1

        if text[left].lower() != text[right].lower():
            return False

        left += 1
        right -= 1

    return True
```
`clean_palindrome("A man, a plan, a canal: Panama")` → `True`.  
Time: **O(n)**; extra space: **O(1)**.

## 7. Anagram Check
Anagrams contain the same characters with the same frequencies, ignoring order.

```python
def are_anagrams(a, b):
    if len(a) != len(b):
        return False

    freq = {}
    for ch in a:
        freq[ch] = freq.get(ch, 0) + 1

    for ch in b:
        if ch not in freq:
            return False
        freq[ch] -= 1
        if freq[ch] < 0:
            return False

    return True
```
`are_anagrams("listen", "silent")` → `True`. This version is case-sensitive and treats spaces as characters.  
Time: **O(n)** average; extra space: **O(k)**.

## 8. First Non-Repeating Character
Return the index of the first character appearing exactly once.

```python
def first_unique(text):
    freq = {}
    for ch in text:
        freq[ch] = freq.get(ch, 0) + 1

    for i, ch in enumerate(text):
        if freq[ch] == 1:
            return i

    return -1
```
`first_unique("swiss")` → `1` (the character is `"w"`). Returns `-1` if none exists.  
Time: **O(n)** average; extra space: **O(k)**.

## 9. Remove Duplicate Characters, Preserving Order
```python
def remove_duplicate_chars(text):
    seen = set()
    result = []

    for ch in text:
        if ch not in seen:
            seen.add(ch)
            result.append(ch)

    return "".join(result)
```
`remove_duplicate_chars("banana")` → `"ban"`.  
Time: **O(n)** average; extra space: **O(k)**.

## 10. Check String Rotation
Two strings are rotations if one can be shifted around to produce the other.

```python
def is_rotation(a, b):
    if len(a) != len(b):
        return False
    return b in (a + a)
```
`is_rotation("waterbottle", "erbottlewat")` → `True`.  
The concatenated string uses **O(n)** extra space; substring-search details depend on the implementation.

## 11. Longest Common Prefix
```python
def longest_common_prefix(words):
    if not words:
        return ""

    prefix = words[0]
    for word in words[1:]:
        while not word.startswith(prefix):
            prefix = prefix[:-1]
            if prefix == "":
                return ""
    return prefix
```
`longest_common_prefix(["flower", "flow", "flight"])` → `"fl"`.

## 12. Run-Length Encoding
Compress consecutive equal characters into a character followed by its count.

```python
def run_length_encode(text):
    if not text:
        return ""

    result = []
    count = 1

    for i in range(1, len(text)):
        if text[i] == text[i - 1]:
            count += 1
        else:
            result.append(text[i - 1] + str(count))
            count = 1

    result.append(text[-1] + str(count))
    return "".join(result)
```
`run_length_encode("aaabbc")` → `"a3b2c1"`.  
Time: **O(n)**; output space: **O(n)**.

## 13. Substring vs Subsequence
- **Substring:** a contiguous block of characters.
- **Subsequence:** characters kept in order but not necessarily next to each other.

For `"abc"`, `"ab"` is both a substring and subsequence; `"ac"` is a subsequence but not a substring.

A string of length `n` has `n(n+1)/2` non-empty substrings and `2^n` subsequences including the empty subsequence.

## 14. Generate All Substrings
```python
def all_substrings(text):
    result = []
    for start in range(len(text)):
        for end in range(start + 1, len(text) + 1):
            result.append(text[start:end])
    return result
```
For `"abc"` → `['a', 'ab', 'abc', 'b', 'bc', 'c']`.  
There are O(n²) substrings; storing copied substrings can require O(n³) total character space in the worst case.

## 15. Check All Characters Are Unique
```python
def all_unique(text):
    seen = set()
    for ch in text:
        if ch in seen:
            return False
        seen.add(ch)
    return True
```
Time: **O(n)** average; extra space: **O(k)**.

## 16. Common Mistakes
1. Forgetting Python strings are immutable.
2. Ignoring case sensitivity when it matters.
3. Removing punctuation/spaces when the problem says to preserve them.
4. Confusing substring with subsequence.
5. Returning a character when an index is required.
6. Not deciding what to return when no match exists.
7. Repeated string concatenation in a large loop instead of collecting pieces and joining.
8. Comparing only character sets for anagram problems; frequencies must match.

## 17. Complexity Reference

| Pattern | Time | Extra space |
|---|---:|---:|
| Character frequency | O(n) average | O(k) |
| Vowel/consonant count | O(n) | O(1) |
| Reverse with character list | O(n) | O(n) |
| Exact palindrome check | O(n) | O(1) |
| Anagram frequency method | O(n) average | O(k) |
| First unique character | O(n) average | O(k) |
| Remove duplicate characters | O(n) average | O(k) |
| Run-length encoding | O(n) | O(n) |
| Generate/store all substrings | O(n³) total copied output | O(n³) |

Here, `n` is the string length and `k` is the number of distinct characters.

---

# Practice Problems

## Beginner
1. Count vowels and consonants.
2. Reverse a string.
3. Check whether a string is a palindrome.
4. Count each character's frequency.
5. Check whether two strings are anagrams.
6. Find the first non-repeating character.
7. Remove duplicate characters while preserving order.
8. Check whether all characters are unique.
9. Find the longest common prefix.
10. Compress consecutive repeated characters.

## Intermediate
11. Check whether two strings are rotations.
12. Count words in a sentence.
13. Find the most frequent character.
14. Find characters shared by two strings.
15. Generate all substrings.
16. Find the longest substring without repeating characters.
17. Find the longest palindromic substring.
18. Group words into anagram groups.
19. Check whether one string is a subsequence of another.
20. Find the first index where a pattern occurs in a text.

---

# Quick Revision
- Frequency counting solves many character-count problems.
- Two pointers are useful for palindrome checks.
- Anagrams need matching character frequencies.
- Sets help detect duplicates.
- Substrings are contiguous; subsequences need not be.
- Read carefully for case, punctuation, spaces, and return values.

> **Golden rule:** Clarify what counts as a character match: case, spaces, punctuation, and order.

## Day 9 Preview
**Searching Algorithms** — linear search, binary search, boundary patterns, and choosing the right method.
