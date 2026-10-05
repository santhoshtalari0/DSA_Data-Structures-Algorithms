# 🚀 Day 04 - Time & Space Complexity

Welcome to **Day 4 of my DSA Journey**! 🚀

Day 1 introduced DSA, Day 2 introduced problem-solving fundamentals, and
Day 3 covered Python essentials for DSA.

Day 2 already introduced the basic idea of Time and Space Complexity.
Today we go deeper into **how to actually analyze code**, without
repeating the earlier fundamentals.

> **Goal: Learn how to calculate, compare, and improve algorithm
> efficiency.**

------------------------------------------------------------------------

# 📌 What Will We Learn Today?

-   Input size `n`
-   Time Complexity
-   Space Complexity
-   Asymptotic analysis
-   Big O, Big Omega, Big Theta
-   `O(1)`
-   `O(log n)`
-   `O(n)`
-   `O(n log n)`
-   `O(n²)`
-   `O(n³)`
-   `O(2ⁿ)`
-   `O(n!)`
-   Sequential loops
-   Nested loops
-   Dependent loops
-   Halving and doubling patterns
-   Constants and dominant terms
-   Best, average, and worst case
-   Auxiliary space
-   Time-space tradeoff
-   Complexity analysis of real code

------------------------------------------------------------------------

# 1️⃣ What is Input Size?

We usually represent the size of input using:

``` text
n
```

Example:

``` python
numbers = [10, 20, 30, 40, 50]
```

Here:

``` text
n = 5
```

If the list contains 10,000 elements:

``` text
n = 10,000
```

Complexity tells us how the required work or memory changes as `n`
grows.

------------------------------------------------------------------------

# 2️⃣ What is Time Complexity?

Time Complexity describes how the **amount of computational work** grows
with input size.

It does not mean exact seconds because execution time depends on:

``` text
Hardware
Programming Language
Implementation
System
```

Instead, we study the growth of operations.

------------------------------------------------------------------------

# 3️⃣ What is Space Complexity?

Space Complexity describes how memory usage grows with input size.

Example:

``` python
total = 0

for x in numbers:
    total += x
```

Only a few extra variables are used.

So the additional space is:

``` text
O(1)
```

------------------------------------------------------------------------

# 4️⃣ Why Complexity Matters

Suppose two solutions are:

``` text
Solution A → O(n)

Solution B → O(n²)
```

For small input, both may work.

For very large input, `O(n²)` can become much slower.

Therefore:

> **A correct solution is not always an efficient solution.**

------------------------------------------------------------------------

# 5️⃣ Big O Notation

Big O is the notation most commonly used to describe an algorithm's
asymptotic upper-bound growth.

Common complexities:

``` text
O(1)
O(log n)
O(n)
O(n log n)
O(n²)
O(n³)
O(2ⁿ)
O(n!)
```

------------------------------------------------------------------------

# 6️⃣ O(1) --- Constant Time

The amount of work does not grow with `n`.

Example:

``` python
def first(numbers):
    return numbers[0]
```

Whether there are:

``` text
10 elements
1,000 elements
1,000,000 elements
```

we access one position.

Therefore:

``` text
Time → O(1)
```

------------------------------------------------------------------------

# 7️⃣ O(n) --- Linear Time

The work grows approximately in proportion to `n`.

``` python
for x in numbers:
    print(x)
```

If:

``` text
n = 100
```

we process about 100 elements.

If:

``` text
n = 1,000
```

we process about 1,000 elements.

Therefore:

``` text
O(n)
```

------------------------------------------------------------------------

# 8️⃣ O(n²) --- Quadratic Time

Consider:

``` python
for i in range(n):
    for j in range(n):
        print(i, j)
```

The outer loop runs `n` times.

For every outer iteration, the inner loop runs `n` times.

Therefore:

``` text
n × n = n²
```

So:

``` text
O(n²)
```

------------------------------------------------------------------------

# 9️⃣ O(n³) --- Cubic Time

Three full nested loops:

``` python
for i in range(n):
    for j in range(n):
        for k in range(n):
            print(i, j, k)
```

Work:

``` text
n × n × n
```

Therefore:

``` text
O(n³)
```

------------------------------------------------------------------------

# 🔟 O(log n) --- Logarithmic Time

A common logarithmic pattern repeatedly divides the problem size by a
constant.

Example:

``` python
i = n

while i > 1:
    i //= 2
```

The values look like:

``` text
n
n/2
n/4
n/8
n/16
...
1
```

Therefore:

``` text
O(log n)
```

The same idea appears when a value repeatedly doubles until it reaches
`n`.

------------------------------------------------------------------------

# 1️⃣1️⃣ O(n log n)

Suppose we perform `n` work at each of `log n` levels.

Then:

``` text
n × log n
```

Therefore:

``` text
O(n log n)
```

This is a common complexity for efficient sorting algorithms such as
Merge Sort.

------------------------------------------------------------------------

# 1️⃣2️⃣ O(2ⁿ) --- Exponential

A recursive process that branches into two subproblems at each level can
produce exponential growth.

Example pattern:

``` python
def solve(n):
    if n <= 1:
        return

    solve(n - 1)
    solve(n - 1)
```

The number of calls grows roughly like:

``` text
2ⁿ
```

Therefore:

``` text
O(2ⁿ)
```

Such growth becomes expensive very quickly.

------------------------------------------------------------------------

# 1️⃣3️⃣ O(n!) --- Factorial

Factorial:

``` text
n! = n × (n-1) × ... × 1
```

Example:

``` text
5! = 120
```

Trying every possible permutation can require:

``` text
O(n!)
```

This becomes extremely expensive even for relatively small `n`.

------------------------------------------------------------------------

# 1️⃣4️⃣ Complexity Growth Order

For large input, a useful general order is:

``` text
O(1)
   ↓
O(log n)
   ↓
O(n)
   ↓
O(n log n)
   ↓
O(n²)
   ↓
O(n³)
   ↓
O(2ⁿ)
   ↓
O(n!)
```

Generally, slower-growing complexity is preferable.

------------------------------------------------------------------------

# 1️⃣5️⃣ Ignore Constants

Suppose:

``` python
for i in range(n):
    print(i)

for i in range(n):
    print(i)
```

Total work:

``` text
2n
```

We write:

``` text
O(2n)
```

But Big O ignores constant multipliers:

``` text
O(2n) → O(n)
```

Similarly:

``` text
O(5n) → O(n)
O(100n) → O(n)
```

------------------------------------------------------------------------

# 1️⃣6️⃣ Ignore Lower-Order Terms

Suppose an algorithm has:

``` text
n² + n + 10
```

For large `n`, the `n²` term dominates.

Therefore:

``` text
O(n² + n + 10)
```

becomes:

``` text
O(n²)
```

Example:

``` text
5n² + 3n + 20
```

becomes:

``` text
O(n²)
```

------------------------------------------------------------------------

# 1️⃣7️⃣ Sequential Loops

Consider:

``` python
for i in range(n):
    print(i)

for j in range(n):
    print(j)
```

First loop:

``` text
O(n)
```

Second loop:

``` text
O(n)
```

Together:

``` text
O(n + n)
= O(2n)
= O(n)
```

> **Sequential work is added.**

------------------------------------------------------------------------

# 1️⃣8️⃣ Nested Loops

Consider:

``` python
for i in range(n):
    for j in range(n):
        print(i, j)
```

The loops are nested.

Therefore:

``` text
O(n × n)
= O(n²)
```

> **Nested work is usually multiplied.**

------------------------------------------------------------------------

# 1️⃣9️⃣ Different Input Sizes

Consider:

``` python
for i in range(n):
    for j in range(m):
        print(i, j)
```

The complexity is:

``` text
O(n × m)
```

Do not automatically write `O(n²)`.

Use `O(n²)` only when both loops are controlled by the same input size.

------------------------------------------------------------------------

# 2️⃣0️⃣ Dependent Nested Loops

Consider:

``` python
for i in range(n):
    for j in range(i):
        print(i, j)
```

The inner loop runs:

``` text
0 + 1 + 2 + ... + (n-1)
```

This sum is:

``` text
n(n-1)/2
```

which grows as:

``` text
O(n²)
```

Therefore:

``` text
Time → O(n²)
```

------------------------------------------------------------------------

# 2️⃣1️⃣ Doubling Pattern

Consider:

``` python
i = 1

while i < n:
    i *= 2
```

Values:

``` text
1
2
4
8
16
32
...
```

The number of iterations is logarithmic:

``` text
O(log n)
```

------------------------------------------------------------------------

# 2️⃣2️⃣ Halving Pattern

Consider:

``` python
i = n

while i > 1:
    i //= 2
```

Values:

``` text
n
n/2
n/4
n/8
...
```

Therefore:

``` text
O(log n)
```

------------------------------------------------------------------------

# 2️⃣3️⃣ O(n log n) Example

``` python
i = 1

while i < n:
    for j in range(n):
        print(j)

    i *= 2
```

Outer loop:

``` text
O(log n)
```

Inner loop:

``` text
O(n)
```

Together:

``` text
O(n log n)
```

------------------------------------------------------------------------

# 2️⃣4️⃣ Best, Average and Worst Case

An algorithm may behave differently for different inputs.

We commonly discuss:

``` text
Best Case
Average Case
Worst Case
```

Consider Linear Search:

``` python
numbers = [10, 20, 30, 40, 50]
```

### Best Case

Search for:

``` text
10
```

Only one comparison may be needed.

``` text
Best Case → O(1)
```

### Worst Case

Search for:

``` text
50
```

We may check every element.

``` text
Worst Case → O(n)
```

### Average Case

The element may appear somewhere in the middle.

Under common assumptions:

``` text
Average Case → O(n)
```

------------------------------------------------------------------------

# 2️⃣5️⃣ Big Omega --- Ω

Big Omega represents an asymptotic **lower bound**.

Symbol:

``` text
Ω
```

For Linear Search, the best-case lower-bound behavior is:

``` text
Ω(1)
```

Do not simply treat Omega as a synonym for "best case"; it describes a
lower bound.

------------------------------------------------------------------------

# 2️⃣6️⃣ Big Theta --- Θ

Big Theta represents a **tight asymptotic bound**.

Symbol:

``` text
Θ
```

If an operation always processes every element, its growth can be:

``` text
Θ(n)
```

For example, traversing all elements of a list is tightly linear.

------------------------------------------------------------------------

# 2️⃣7️⃣ O vs Ω vs Θ

Remember:

``` text
O(f(n))
    ↓
Upper Bound

Ω(f(n))
    ↓
Lower Bound

Θ(f(n))
    ↓
Tight Bound
```

Big O is the notation you will encounter most often in normal DSA
problem discussions.

------------------------------------------------------------------------

# 2️⃣8️⃣ Auxiliary Space

Auxiliary space means the **extra memory used by the algorithm**,
excluding the input itself.

Example:

``` python
def total(numbers):
    answer = 0

    for x in numbers:
        answer += x

    return answer
```

Only a fixed number of extra variables are used.

Therefore:

``` text
Auxiliary Space → O(1)
```

------------------------------------------------------------------------

# 2️⃣9️⃣ Extra List

Consider:

``` python
def double_values(numbers):
    result = []

    for x in numbers:
        result.append(x * 2)

    return result
```

The `result` list grows with `n`.

Therefore:

``` text
Time → O(n)
Auxiliary Space → O(n)
```

------------------------------------------------------------------------

# 3️⃣0️⃣ Two-Dimensional Extra Space

Consider:

``` python
matrix = [[0] * n for _ in range(n)]
```

There are approximately:

``` text
n × n
```

elements.

Therefore:

``` text
Auxiliary Space → O(n²)
```

------------------------------------------------------------------------

# 3️⃣1️⃣ Time-Space Tradeoff

Sometimes we use more memory to make a solution faster.

Example: duplicate detection.

### Approach 1 --- Compare Pairs

``` text
Time → O(n²)
Space → O(1)
```

### Approach 2 --- Use a Set

``` python
seen = set()

for x in numbers:
    if x in seen:
        print("Duplicate")
        break
    seen.add(x)
```

Typical average-case complexity:

``` text
Time → O(n)
Space → O(n)
```

So we trade:

``` text
More Space
     ↓
Less Time
```

This is a **time-space tradeoff**.

------------------------------------------------------------------------

# 3️⃣2️⃣ Complexity of Common Operations

  Operation                        Typical Complexity
  ------------------------------ --------------------
  List index access                            `O(1)`
  List traversal                               `O(n)`
  Search in a list                             `O(n)`
  Set membership                       `O(1)` average
  Dictionary key lookup                `O(1)` average
  Efficient comparison sorting           `O(n log n)`
  Binary Search                            `O(log n)`

These are common patterns; exact behavior can depend on the data
structure and implementation.

------------------------------------------------------------------------

# 3️⃣3️⃣ Complexity and Constraints

Constraints help us decide whether an approach is practical.

For example:

``` text
n ≤ 20
```

An exponential solution may sometimes be possible.

But for:

``` text
n ≤ 100,000
```

an `O(n²)` solution may be too slow depending on the problem.

For:

``` text
n ≤ 1,000,000
```

we generally look for approximately:

``` text
O(n)
```

or:

``` text
O(n log n)
```

The exact acceptable complexity depends on the problem and its time
limit.

------------------------------------------------------------------------

# 3️⃣4️⃣ Complete Code Analysis Example

``` python
def example(numbers):
    n = len(numbers)

    for i in range(n):
        print(numbers[i])

    for i in range(n):
        for j in range(n):
            print(i, j)
```

First section:

``` text
O(n)
```

Second section:

``` text
O(n²)
```

Total:

``` text
O(n + n²)
```

Keep the dominant term:

``` text
O(n²)
```

No growing extra data structure is created, so auxiliary space is:

``` text
O(1)
```

------------------------------------------------------------------------

# 3️⃣5️⃣ Another Complete Example

``` python
def example(n):
    i = 1

    while i < n:
        for j in range(n):
            print(j)

        i *= 2
```

Outer loop:

``` text
O(log n)
```

Inner loop:

``` text
O(n)
```

Therefore:

``` text
Time → O(n log n)
Space → O(1)
```

------------------------------------------------------------------------

# 3️⃣6️⃣ Common Mistakes

### Mistake 1 --- Two loops always means `O(n²)`

Not true.

``` python
for i in range(n):
    ...

for j in range(n):
    ...
```

is:

``` text
O(n)
```

after simplification.

------------------------------------------------------------------------

### Mistake 2 --- Every nested loop is automatically `O(n²)`

Not necessarily.

You must check how many times the inner loop actually runs.

------------------------------------------------------------------------

### Mistake 3 --- Forgetting logarithmic loops

``` python
i = 1

while i < n:
    i *= 2
```

is:

``` text
O(log n)
```

not `O(n)`.

------------------------------------------------------------------------

### Mistake 4 --- Keeping constants

``` text
O(5n)
```

becomes:

``` text
O(n)
```

------------------------------------------------------------------------

### Mistake 5 --- Keeping smaller terms

``` text
O(n² + n)
```

becomes:

``` text
O(n²)
```

------------------------------------------------------------------------

### Mistake 6 --- Ignoring extra memory

If an algorithm creates:

``` text
List
Set
Dictionary
Matrix
```

whose size grows with `n`, space complexity may also grow.

------------------------------------------------------------------------

# 🧠 3️⃣7️⃣ How to Analyze Any Code

Follow this checklist:

``` text
1. Identify the input size.
        ↓
2. Find repeated operations.
        ↓
3. Count loop iterations.
        ↓
4. Check sequential loops.
        ↓
5. Check nested loops.
        ↓
6. Check doubling/halving.
        ↓
7. Add sequential work.
        ↓
8. Multiply nested work.
        ↓
9. Remove constants.
        ↓
10. Keep the dominant term.
        ↓
11. Check extra memory.
```

------------------------------------------------------------------------

# 🧪 3️⃣8️⃣ Practice Problems

Analyze the **Time Complexity and Auxiliary Space**.

### Beginner

``` text
1. Find the first element of a list.

2. Print every element of a list.

3. Find the maximum element using one loop.

4. Search for a value using Linear Search.

5. Copy all elements into a new list.
```

### Intermediate

``` text
6. Two sequential loops, each running n times.

7. Two nested loops, each running n times.

8. A loop where i doubles each iteration.

9. A loop where i is divided by 2 each iteration.

10. A loop of n iterations containing an O(log n) loop.
```

### Thinking Problems

``` text
11. Analyze:

for i in range(n):
    for j in range(i):
        print(i, j)

12. Analyze:

for i in range(n):
    for j in range(n):
        for k in range(n):
            print(i, j, k)

13. Analyze:

i = 1
while i < n:
    for j in range(n):
        print(j)
    i *= 2

14. Compare O(n²) and O(n log n).

15. Explain the time-space tradeoff in duplicate detection.
```

------------------------------------------------------------------------

# 🧠 3️⃣9️⃣ Quick Revision

``` text
O(1)
↓
Constant

O(log n)
↓
Repeated halving/doubling

O(n)
↓
One full traversal

O(n log n)
↓
n work × log n levels

O(n²)
↓
Two full nested loops

O(n³)
↓
Three full nested loops

O(2ⁿ)
↓
Exponential branching

O(n!)
↓
Factorial growth
```

------------------------------------------------------------------------

# 🎯 Key Takeaways

-   Complexity describes how resource usage grows with input size.
-   `n` usually represents input size.
-   Time Complexity focuses on computational work.
-   Space Complexity focuses on memory usage.
-   Big O describes an asymptotic upper bound.
-   Big Omega describes an asymptotic lower bound.
-   Big Theta describes a tight asymptotic bound.
-   Sequential work is added.
-   Nested work is usually multiplied.
-   Repeated halving or doubling often gives `O(log n)`.
-   Constants are ignored.
-   Lower-order terms are ignored.
-   Always consider best, average, and worst cases where relevant.
-   Auxiliary space means extra memory used by the algorithm.
-   Extra memory can sometimes reduce running time.
-   Constraints help determine whether a complexity is practical.
-   Always analyze both time and space before finalizing a DSA solution.

------------------------------------------------------------------------

# 🚀 DSA Progress

``` text
Day 01 → Introduction to DSA ✅

Day 02 → Problem-Solving Fundamentals ✅

Day 03 → Python Essentials for DSA ✅

Day 04 → Time & Space Complexity ✅

Day 05 → Mathematics for DSA 🔜

Day 06 → Recursion Fundamentals

Day 07 → Arrays
```

> **Don't just ask whether your code works. Ask how efficiently it
> works.**

🚀 **The DSA journey continues...**
