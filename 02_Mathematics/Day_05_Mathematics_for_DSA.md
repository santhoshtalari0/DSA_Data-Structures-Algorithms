# 🚀 Day 05 - Mathematics for DSA

Welcome to **Day 5 of my DSA Journey**! 🚀

So far:

``` text
Day 01 → Introduction to DSA
Day 02 → Problem-Solving Fundamentals
Day 03 → Python Essentials for DSA
Day 04 → Time & Space Complexity
```

Today we build the mathematical foundation needed for many DSA problems.

> **Goal: Recognize mathematical patterns and turn them into efficient
> algorithms.**

------------------------------------------------------------------------

# 📌 What Will We Learn Today?

-   Divisibility and factors
-   Factor pairs and optimized factor finding
-   Prime numbers and optimized prime checking
-   Sieve of Eratosthenes
-   Prime factorization
-   GCD and Euclidean Algorithm
-   LCM and GCD/LCM relationship
-   Powers and Binary Exponentiation
-   Modular arithmetic and modular exponentiation
-   Arithmetic and geometric series
-   Counting pairs
-   Combinations and permutations
-   Parity
-   XOR properties
-   Overflow awareness
-   Mathematical optimization
-   DSA practice problems

------------------------------------------------------------------------

# 1️⃣ Divisibility

A number `a` is divisible by `b` when:

``` text
a % b == 0
```

Example:

``` text
20 % 5 = 0
```

Therefore, 20 is divisible by 5.

------------------------------------------------------------------------

# 2️⃣ Useful Divisibility Rules

### Divisible by 2

The last digit is:

``` text
0, 2, 4, 6, 8
```

### Divisible by 5

The last digit is:

``` text
0 or 5
```

### Divisible by 10

The last digit is:

``` text
0
```

### Divisible by 3

The sum of the digits is divisible by 3.

Example:

``` text
123
1 + 2 + 3 = 6
```

Since:

``` text
6 % 3 = 0
```

123 is divisible by 3.

------------------------------------------------------------------------

# 3️⃣ Factors

A factor of `n` divides `n` exactly.

For:

``` text
12
```

the factors are:

``` text
1, 2, 3, 4, 6, 12
```

A straightforward solution checks every number from 1 to `n`, which
takes:

``` text
O(n)
```

------------------------------------------------------------------------

# 4️⃣ Factor Pairs

Factors occur in pairs.

For:

``` text
36
```

we have:

``` text
1 × 36
2 × 18
3 × 12
4 × 9
6 × 6
```

After:

``` text
√36 = 6
```

the pairs repeat in reverse.

Therefore, we only need to check up to:

``` text
√n
```

------------------------------------------------------------------------

# 5️⃣ Optimized Factor Finding

``` python
n = 36

for i in range(1, int(n ** 0.5) + 1):
    if n % i == 0:
        print(i, n // i)
```

Complexity:

``` text
Time → O(√n)
Space → O(1)
```

------------------------------------------------------------------------

# 6️⃣ Why √n Works

If:

``` text
a × b = n
```

both `a` and `b` cannot be greater than `√n`, because then:

``` text
a × b > n
```

Therefore every factor pair has at least one factor:

``` text
≤ √n
```

This is why checking up to `√n` is sufficient.

------------------------------------------------------------------------

# 7️⃣ Prime Numbers

A prime number has exactly two positive factors:

``` text
1
itself
```

Examples:

``` text
2, 3, 5, 7, 11, 13
```

Important:

``` text
1 is NOT prime.
```

------------------------------------------------------------------------

# 8️⃣ Optimized Prime Checking

``` python
def is_prime(n):
    if n < 2:
        return False

    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False

    return True
```

Complexity:

``` text
Time → O(√n)
Space → O(1)
```

We can skip even divisors after checking 2:

``` python
def is_prime(n):
    if n < 2:
        return False

    if n == 2:
        return True

    if n % 2 == 0:
        return False

    i = 3

    while i * i <= n:
        if n % i == 0:
            return False
        i += 2

    return True
```

The asymptotic complexity remains:

``` text
O(√n)
```

------------------------------------------------------------------------

# 9️⃣ Sieve of Eratosthenes

If we need **all prime numbers from 1 to N**, checking every number
separately is inefficient.

The **Sieve of Eratosthenes** works by marking multiples of each prime
as non-prime.

For:

``` text
N = 20
```

start with all numbers and process:

``` text
2 → mark multiples
3 → mark multiples
5 → mark multiples
...
```

Only primes remain unmarked.

## Python

``` python
def sieve(n):
    is_prime = [True] * (n + 1)

    if n >= 0:
        is_prime[0] = False
    if n >= 1:
        is_prime[1] = False

    p = 2

    while p * p <= n:
        if is_prime[p]:
            for multiple in range(p * p, n + 1, p):
                is_prime[multiple] = False
        p += 1

    return is_prime
```

Complexity:

``` text
Time → O(n log log n)
Space → O(n)
```

------------------------------------------------------------------------

# 🔟 Prime Factorization

Prime factorization represents a number as a product of prime numbers.

Example:

``` text
60 = 2 × 2 × 3 × 5
```

Python:

``` python
def prime_factors(n):
    factors = []
    p = 2

    while p * p <= n:
        while n % p == 0:
            factors.append(p)
            n //= p
        p += 1

    if n > 1:
        factors.append(n)

    return factors
```

Example:

``` python
print(prime_factors(60))
```

Output:

``` text
[2, 2, 3, 5]
```

------------------------------------------------------------------------

# 1️⃣1️⃣ GCD

GCD means **Greatest Common Divisor**.

Example:

``` text
12 and 18
```

Common factors:

``` text
1, 2, 3, 6
```

Therefore:

``` text
GCD(12, 18) = 6
```

------------------------------------------------------------------------

# 1️⃣2️⃣ Euclidean Algorithm

The key property is:

``` text
gcd(a, b) = gcd(b, a % b)
```

Continue until:

``` text
b = 0
```

Then `a` is the GCD.

Example:

``` text
GCD(48, 18)

48 % 18 = 12
18 % 12 = 6
12 % 6  = 0

Answer = 6
```

Python:

``` python
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a
```

Complexity:

``` text
Time → O(log(min(a, b)))
Space → O(1)
```

------------------------------------------------------------------------

# 1️⃣3️⃣ LCM

LCM means **Least Common Multiple**.

Example:

``` text
4 → 4, 8, 12, 16, ...
6 → 6, 12, 18, ...
```

Therefore:

``` text
LCM(4, 6) = 12
```

Relationship:

``` text
a × b = GCD(a, b) × LCM(a, b)
```

So:

``` text
LCM(a, b) = (a / GCD(a, b)) × b
```

Python:

``` python
def lcm(a, b):
    g = gcd(a, b)
    return abs(a // g * b)
```

Dividing before multiplying is a useful habit in fixed-width integer
languages because it can reduce overflow risk.

------------------------------------------------------------------------

# 1️⃣4️⃣ Powers

A power represents repeated multiplication.

``` text
2⁵ = 2 × 2 × 2 × 2 × 2 = 32
```

Simple implementation:

``` python
def power(a, b):
    result = 1

    for _ in range(b):
        result *= a

    return result
```

Complexity:

``` text
O(b)
```

------------------------------------------------------------------------

# 1️⃣5️⃣ Binary Exponentiation

We can calculate:

``` text
a^b
```

in:

``` text
O(log b)
```

Instead of multiplying `a` repeatedly, we repeatedly square the base and
divide the exponent by 2.

``` python
def power(a, b):
    result = 1

    while b > 0:
        if b % 2 == 1:
            result *= a

        a *= a
        b //= 2

    return result
```

Example:

``` python
print(power(2, 10))
```

Output:

``` text
1024
```

Complexity:

``` text
Time → O(log b)
Space → O(1)
```

------------------------------------------------------------------------

# 1️⃣6️⃣ Modular Arithmetic

Sometimes we only need:

``` text
result % m
```

rather than the complete result.

Example:

``` text
17 % 5 = 2
```

For addition:

``` text
(a + b) % m
=
((a % m) + (b % m)) % m
```

For multiplication:

``` text
(a × b) % m
=
((a % m) × (b % m)) % m
```

This is useful when intermediate values become very large.

------------------------------------------------------------------------

# 1️⃣7️⃣ Modular Exponentiation

To calculate:

``` text
a^b % m
```

efficiently, combine:

``` text
Binary Exponentiation
+
Modulo
```

``` python
def mod_power(a, b, m):
    result = 1
    a %= m

    while b > 0:
        if b % 2 == 1:
            result = (result * a) % m

        a = (a * a) % m
        b //= 2

    return result
```

Example:

``` python
print(mod_power(2, 10, 1000))
```

Output:

``` text
24
```

Complexity:

``` text
O(log b)
```

------------------------------------------------------------------------

# 1️⃣8️⃣ Arithmetic Series

The sum of the first `n` natural numbers is:

``` text
1 + 2 + 3 + ... + n
```

Formula:

``` text
n(n + 1) / 2
```

Example:

``` text
1 + 2 + 3 + 4 + 5 = 15
```

Formula:

``` text
5 × 6 / 2 = 15
```

A loop is `O(n)`, while the formula is `O(1)`.

------------------------------------------------------------------------

# 1️⃣9️⃣ Sum of Squares

Formula:

``` text
1² + 2² + ... + n²
=
n(n + 1)(2n + 1) / 6
```

Example:

``` text
1² + 2² + 3²
= 14
```

Formula:

``` text
3 × 4 × 7 / 6 = 14
```

------------------------------------------------------------------------

# 2️⃣0️⃣ Sum of First N Odd Numbers

The sum of the first `n` odd numbers is:

``` text
n²
```

Example:

``` text
1 + 3 + 5 + 7 + 9 = 25
```

There are 5 terms:

``` text
5² = 25
```

------------------------------------------------------------------------

# 2️⃣1️⃣ Geometric Series

A geometric sequence has a constant ratio.

Example:

``` text
2, 4, 8, 16, 32
```

For:

``` text
1 + r + r² + ... + r^(n-1)
```

when `r != 1`:

``` text
Sum = (r^n - 1) / (r - 1)
```

Example:

``` text
1 + 2 + 4 + 8 = 15
```

``` text
(2⁴ - 1) / (2 - 1)
= 15
```

------------------------------------------------------------------------

# 2️⃣2️⃣ Counting Pairs

Suppose we have `n` elements and want the number of unique pairs.

Formula:

``` text
n(n - 1) / 2
```

For:

``` text
n = 4
```

pairs are:

``` text
AB
AC
AD
BC
BD
CD
```

Total:

``` text
4 × 3 / 2 = 6
```

This can replace an `O(n²)` pair-enumeration loop when only the count is
needed.

------------------------------------------------------------------------

# 2️⃣3️⃣ Combinations

A combination selects items where **order does not matter**.

Formula:

``` text
nCr = n! / (r!(n-r)!)
```

Example:

``` text
4C2 = 4! / (2! × 2!)
     = 6
```

Use combinations when:

``` text
AB and BA
```

represent the same selection.

------------------------------------------------------------------------

# 2️⃣4️⃣ Permutations

A permutation considers **order**.

Formula:

``` text
nPr = n! / (n-r)!
```

Example:

``` text
4P2 = 4! / 2!
     = 12
```

Here:

``` text
AB ≠ BA
```

because order matters.

------------------------------------------------------------------------

# 2️⃣5️⃣ Combination vs Permutation

``` text
Combination
→ Order does NOT matter

Permutation
→ Order DOES matter
```

Example:

``` text
Choose 2 students for a team
→ Combination

Choose President and Secretary
→ Permutation
```

------------------------------------------------------------------------

# 2️⃣6️⃣ Parity

Parity tells us whether a number is:

``` text
Even
or
Odd
```

Useful properties:

``` text
Even + Even = Even
Even + Odd  = Odd
Odd + Odd   = Even
```

and:

``` text
Even × Anything = Even
Odd × Odd = Odd
```

These properties can sometimes solve a problem without processing every
element.

------------------------------------------------------------------------

# 2️⃣7️⃣ XOR Properties

XOR is:

``` text
^
```

Important properties:

``` text
x ^ x = 0
x ^ 0 = x
```

Therefore equal values cancel when XORed.

Example:

``` text
[4, 1, 2, 1, 2]
```

Every number except 4 occurs twice.

``` python
numbers = [4, 1, 2, 1, 2]

answer = 0

for x in numbers:
    answer ^= x

print(answer)
```

Output:

``` text
4
```

Because:

``` text
1 ^ 1 = 0
2 ^ 2 = 0
4 ^ 0 = 4
```

------------------------------------------------------------------------

# 2️⃣8️⃣ Overflow Awareness

Python integers automatically grow as needed.

But languages such as C++ and Java use fixed-size integer types.

For example:

``` text
a × b
```

can exceed the maximum value of an integer type.

This is why DSA solutions sometimes use:

``` text
long long
long
modular arithmetic
```

or change the order of calculations.

For example:

``` text
(a / gcd(a, b)) × b
```

is safer than:

``` text
(a × b) / gcd(a, b)
```

when fixed-width overflow is a concern.

------------------------------------------------------------------------

# 2️⃣9️⃣ Mathematical Optimization

Problem:

``` text
Find 1 + 2 + ... + n
```

### Loop

``` python
total = 0

for i in range(1, n + 1):
    total += i
```

Complexity:

``` text
O(n)
```

### Formula

``` python
total = n * (n + 1) // 2
```

Complexity:

``` text
O(1)
```

Same result.

Different efficiency.

> **Before writing a loop, ask whether a mathematical formula can give
> the answer directly.**

------------------------------------------------------------------------

# 3️⃣0️⃣ Choosing the Right Mathematical Tool

When you see a problem:

``` text
Divisibility?
    ↓
Modulo

Factors?
    ↓
√n

Prime?
    ↓
√n

Many primes?
    ↓
Sieve

Common divisor?
    ↓
GCD

Common multiple?
    ↓
LCM

Huge power?
    ↓
Binary Exponentiation

Huge power with modulo?
    ↓
Modular Exponentiation

Count unique pairs?
    ↓
n(n - 1) / 2

Repeated addition?
    ↓
Look for a formula

Pairs canceling except one value?
    ↓
XOR
```

------------------------------------------------------------------------

# 🧪 3️⃣1️⃣ Practice Problems

## Beginner

``` text
1. Check whether a number is divisible by K.

2. Print all factors of N.

3. Count the factors of N.

4. Check whether N is prime.

5. Find GCD of two numbers.

6. Find LCM of two numbers.

7. Calculate a^b using a loop.

8. Find the sum of the first N natural numbers.
```

## Intermediate

``` text
9. Find all primes up to N.

10. Implement the Sieve of Eratosthenes.

11. Find the prime factorization of N.

12. Calculate a^b in O(log b).

13. Calculate a^b % m efficiently.

14. Count the number of unique pairs among N elements.

15. Calculate nCr for small values.

16. Calculate nPr for small values.
```

## Thinking Problems

``` text
17. Find the GCD of an array.

18. Find the LCM of an array.

19. Find whether a number has exactly three factors.

20. Find the number of divisors using prime factorization.

21. Find the only number that occurs once when every other number occurs twice.

22. Count pairs without using nested loops.

23. Determine whether a sum must be odd or even using parity.

24. Replace an O(n) summation with a mathematical formula.
```

------------------------------------------------------------------------

# 🧠 3️⃣2️⃣ Important Patterns

``` text
Factor Search
→ Check up to √n

Prime Check
→ Check divisors up to √n

Many Primes
→ Sieve of Eratosthenes

GCD
→ Euclidean Algorithm

LCM
→ (a / GCD) × b

Power
→ Binary Exponentiation

Power + Modulo
→ Modular Exponentiation

Pair Count
→ n(n - 1) / 2

Natural Sum
→ n(n + 1) / 2

Square Sum
→ n(n + 1)(2n + 1) / 6

First N Odd Sum
→ n²

Equal Pairs Except One
→ XOR
```

------------------------------------------------------------------------

# 🎯 Key Takeaways

-   Use divisibility properties to reduce unnecessary work.
-   Factor pairs allow factor searching in `O(√n)`.
-   Prime checking can be done in `O(√n)`.
-   Sieve of Eratosthenes efficiently finds many primes.
-   Prime factorization breaks numbers into prime factors.
-   Euclidean Algorithm finds GCD efficiently.
-   LCM can be calculated using GCD.
-   Binary Exponentiation calculates powers in `O(log n)`.
-   Modular arithmetic helps control large values.
-   Mathematical formulas can replace loops.
-   Combinations ignore order.
-   Permutations consider order.
-   Parity gives useful even/odd properties.
-   XOR can cancel equal pairs.
-   Always look for a mathematical pattern before choosing brute force.

------------------------------------------------------------------------

# 🚀 DSA Progress

``` text
Day 01 → Introduction to DSA ✅

Day 02 → Problem-Solving Fundamentals ✅

Day 03 → Python Essentials for DSA ✅

Day 04 → Time & Space Complexity ✅

Day 05 → Mathematics for DSA ✅

Day 06 → Recursion Fundamentals 🔜

Day 07 → Arrays
```

> **The best mathematical trick in DSA is recognizing when you don't
> need to loop.**

🚀 **The DSA journey continues...**
