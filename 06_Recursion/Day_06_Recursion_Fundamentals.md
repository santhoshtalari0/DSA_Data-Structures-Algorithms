# Day 06 — Recursion Fundamentals

> **Goal:** Learn how recursion works, how to trace recursive calls, and how to write simple recursive solutions.

---

## 1. What is Recursion?

**Recursion** is a technique where a function calls itself to solve a smaller version of the same problem.

A recursive solution normally has two parts:

1. **Base Case** — tells the function when to stop.
2. **Recursive Case** — calls the same function with a smaller/simpler problem.

```python
def function(n):
    if base_condition:
        return base_value

    return function(smaller_problem)
```

---

## 2. Base Case

The **base case** is the stopping condition.

```python
def count(n):
    if n == 0:
        return

    print(n)
    count(n - 1)
```

Here:

```python
if n == 0:
```

is the base case.

Without a proper base case, recursion can continue until Python raises `RecursionError`.

---

## 3. Recursive Case

The recursive case is where the function calls itself.

```python
count(n - 1)
```

The problem becomes smaller:

```text
n → n-1 → n-2 → n-3 → ...
```

A recursive function should move toward its base case.

---

## 4. How Recursion Works

For:

```python
def count(n):
    if n == 0:
        return

    print(n)
    count(n - 1)
```

Calling:

```python
count(3)
```

creates:

```text
count(3)
   ↓
count(2)
   ↓
count(1)
   ↓
count(0)
```

At `count(0)`, the base case is reached.

Then the calls return one by one.

---

## 5. Call Stack

Every active function call is stored in the **call stack**.

For `count(3)`:

```text
TOP
┌──────────┐
│ count(0) │
├──────────┤
│ count(1) │
├──────────┤
│ count(2) │
├──────────┤
│ count(3) │
└──────────┘
BOTTOM
```

The last call added is completed first.

This follows:

**LIFO — Last In, First Out**

---

## 6. Going Down and Coming Back

Consider:

```python
def show(n):
    if n == 0:
        return

    print("Down", n)
    show(n - 1)
    print("Up", n)
```

For:

```python
show(3)
```

Output:

```text
Down 3
Down 2
Down 1
Up 1
Up 2
Up 3
```

### Important pattern

```text
Before recursive call → happens while going down
After recursive call  → happens while coming back
```

---

## 7. Factorial Using Recursion

Factorial:

```text
n! = n × (n-1) × ... × 1
0! = 1
```

Recursive definition:

```text
n! = n × (n-1)!
```

Code:

```python
def factorial(n):
    if n == 0:
        return 1

    return n * factorial(n - 1)
```

For `factorial(4)`:

```text
4 × 3 × 2 × 1 × 1
= 24
```

---

## 8. Sum of First N Numbers

We want:

```text
1 + 2 + 3 + ... + n
```

Recursive idea:

```text
sum(n) = n + sum(n-1)
```

Base case:

```text
sum(0) = 0
```

Code:

```python
def sum_n(n):
    if n == 0:
        return 0

    return n + sum_n(n - 1)
```

For `n = 4`:

```text
sum_n(4)
= 4 + sum_n(3)
= 4 + 3 + sum_n(2)
= 4 + 3 + 2 + sum_n(1)
= 4 + 3 + 2 + 1 + sum_n(0)
= 10
```

---

## 9. Increasing vs Decreasing Order

### Decreasing

```python
def print_decreasing(n):
    if n == 0:
        return

    print(n)
    print_decreasing(n - 1)
```

Output for `5`:

```text
5
4
3
2
1
```

### Increasing

```python
def print_increasing(n):
    if n == 0:
        return

    print_increasing(n - 1)
    print(n)
```

Output:

```text
1
2
3
4
5
```

### Key idea

```text
Before recursive call → decreasing order
After recursive call  → increasing order
```

---

## 10. Reverse a String Recursively

```python
def reverse_string(s, i):
    if i < 0:
        return

    print(s[i], end="")
    reverse_string(s, i - 1)
```

Example:

```python
reverse_string("hello", 4)
```

Output:

```text
olleh
```

The recursion moves from the last index toward the first.

---

## 11. Recursive Search

We can check whether a target exists in an array.

```python
def contains(arr, index, target):
    if index == len(arr):
        return False

    if arr[index] == target:
        return True

    return contains(arr, index + 1, target)
```

Example:

```python
arr = [4, 7, 2, 9]

print(contains(arr, 0, 9))
```

Output:

```text
True
```

Flow:

```text
index 0 → index 1 → index 2 → index 3
                           ↓
                         found
```

---

## 12. Branching Recursion

A function can call itself more than once.

```python
def tree(n):
    if n == 0:
        return

    print(n)
    tree(n - 1)
    tree(n - 1)
```

For `n = 3`:

```text
             3
           /             2     2
         / \   /         1   1 1   1
```

This is called **branching recursion**.

It is important for understanding trees, backtracking, and divide-and-conquer algorithms.

---

## 13. Direct Recursion

When a function directly calls itself:

```python
def f(n):
    if n == 0:
        return

    f(n - 1)
```

This is **direct recursion**.

---

## 14. Indirect Recursion

Two or more functions can call each other.

```python
def odd(n):
    if n == 0:
        return

    even(n - 1)


def even(n):
    if n == 0:
        return

    odd(n - 1)
```

Flow:

```text
odd → even → odd → even
```

This is **indirect recursion**.

---

## 15. Recursion Depth

Every active recursive call uses call-stack memory.

If there are about `n` active calls:

```text
Auxiliary Space = O(n)
```

Example:

```python
def f(n):
    if n == 0:
        return

    f(n - 1)
```

This has approximately `n` recursive calls.

Therefore:

```text
Time  = O(n)
Space = O(n)
```

---

## 16. Recursion Error

Bad recursion:

```python
def infinite(n):
    return infinite(n + 1)
```

There is no reachable stopping condition.

Eventually Python raises:

```text
RecursionError
```

Always check:

1. Is there a base case?
2. Does every recursive call move toward it?

---

## 17. Tail Recursion

A recursive call is **tail recursive** when it is the final operation.

```python
def count(n):
    if n == 0:
        return

    print(n)
    count(n - 1)
```

The recursive call is the final operation.

### Python note

Python does **not** perform tail-call optimization.

So tail recursion still uses the call stack.

---

## 18. Recursion vs Iteration

Many problems can be solved using either approach.

Recursive:

```python
def sum_n(n):
    if n == 0:
        return 0

    return n + sum_n(n - 1)
```

Iterative:

```python
def sum_n(n):
    total = 0

    for i in range(1, n + 1):
        total += i

    return total
```

Use recursion when the problem naturally has recursive structure, such as:

- Trees
- Graph traversal
- Divide and conquer
- Backtracking
- Recursive definitions

Do not use recursion simply because it is possible.

---

## 19. Multiple Recursive Calls and Complexity

Consider:

```python
def f(n):
    if n <= 1:
        return

    f(n - 1)
    f(n - 1)
```

Each call creates two more calls.

The number of calls grows rapidly:

```text
1
↓
2
↓
4
↓
8
↓
...
```

This gives exponential growth in the number of calls.

### Important intuition

> One recursive branch can be roughly linear; multiple branching calls can become exponential.

---

## 20. How to Trace Any Recursive Function

Use this method:

### Step 1 — Find the base case

Ask:

```text
When does it stop?
```

### Step 2 — Find the recursive call

Ask:

```text
How does the problem become smaller?
```

### Step 3 — Write the calls

Example:

```text
f(4)
f(3)
f(2)
f(1)
```

### Step 4 — Stop at the base case

### Step 5 — Trace the return

```text
f(1) returns
f(2) returns
f(3) returns
f(4) returns
```

This is the easiest way to understand recursion traces.

---

## 21. Recursive Maximum

Find the maximum element recursively.

```python
def maximum(arr, index):
    if index == len(arr) - 1:
        return arr[index]

    rest_max = maximum(arr, index + 1)

    return max(arr[index], rest_max)
```

Example:

```python
arr = [3, 8, 2, 6]

print(maximum(arr, 0))
```

Output:

```text
8
```

### Idea

The function asks:

> What is the maximum of the remaining elements?

Then compares it with the current element.

---

## 22. Common Recursion Mistakes

### 1. No base case

```python
def f(n):
    return f(n - 1)
```

### 2. Moving away from the base case

```python
def f(n):
    if n == 0:
        return

    f(n + 1)
```

### 3. Wrong base-case value

For factorial:

```python
if n == 0:
    return 1
```

not:

```python
return 0
```

### 4. Forgetting `return`

Incorrect:

```python
n + sum_n(n - 1)
```

Correct:

```python
return n + sum_n(n - 1)
```

### 5. Unnecessary recursion depth

If a simple loop solves the problem more safely, recursion may not be the best choice.

---

## 23. Recursion Template

Use this mental template:

```python
def solve(problem):

    # Base case
    if smallest_case:
        return answer

    # Solve smaller problem
    result = solve(smaller_problem)

    # Build current answer
    return ...
```

The important question is not the template itself.

The important question is:

> **What is the smaller problem?**

---

## 24. Recursive Thinking

For any recursion problem, ask:

```text
1. What is the smallest possible problem?
2. What is its answer?
3. How can I reduce the current problem?
4. Can recursion solve that smaller problem?
5. How do I use that smaller answer for the current problem?
```

This is the core of recursive problem solving.

---

# Practice Problems

## Beginner

1. Print numbers from `1` to `N` using recursion.
2. Print numbers from `N` to `1`.
3. Find the sum of the first `N` numbers.
4. Find `N!`.
5. Count digits in a positive integer.
6. Find the sum of digits of a number.
7. Calculate `a^b` recursively.
8. Check whether a string is a palindrome.
9. Find the maximum element of an array.
10. Find the minimum element of an array.

## Intermediate

11. Count occurrences of a target in an array.
12. Find the first occurrence of a target.
13. Find the last occurrence of a target.
14. Reverse an array recursively.
15. Check whether an array is sorted.
16. Find GCD recursively using the Euclidean idea.
17. Implement binary search recursively.
18. Generate all subsequences of a string.
19. Generate all subsets of a small array.
20. Solve the Tower of Hanoi problem.

---

# Day 6 Quick Revision

```text
Recursion
   ↓
Function calls itself
   ↓
Base Case
   ↓
Stops recursion
   ↓
Recursive Case
   ↓
Smaller problem
   ↓
Call Stack
   ↓
Stores active calls
```

### Golden Rule

> **Every recursive solution needs a stopping condition and a way to move toward it.**

---

# Day 7 Preview

**Day 7 — Arrays**

The focus will be on array problem-solving patterns, not the basic Python list operations already covered in Day 3.
