# 🚀 Day 03 - Mathematics for DSA

Welcome to **Day 3 of my DSA Journey**! 🚀

In Day 1, I learned the basic concepts of Data Structures and
Algorithms.

In Day 2, I learned how to approach programming problems using:

``` text
Input
Output
Constraints
Logic
Pseudocode
Dry Run
Time Complexity
Space Complexity
Optimization
```

Now it is time to build another important foundation:

> **Mathematics for DSA**

Mathematics appears everywhere in DSA. We use it for numbers, loops,
counting, divisibility, factors, primes, GCD, LCM, modular arithmetic,
powers, digits, and many optimization problems.

------------------------------------------------------------------------

# 📌 What Will We Learn Today?

In this part, we will understand:

-   Why Mathematics is important in DSA
-   Number basics
-   Positive and negative numbers
-   Even and odd numbers
-   Divisibility
-   Remainder and modulus
-   Factors
-   Multiples
-   Prime numbers
-   Composite numbers
-   Prime factorization
-   Greatest Common Divisor (GCD)
-   Least Common Multiple (LCM)
-   Euclidean Algorithm
-   Sum of digits
-   Count digits
-   Reverse a number
-   Palindrome number
-   Armstrong number
-   Perfect number
-   Power of a number
-   Fast exponentiation
-   Modular arithmetic
-   Basic logarithm idea
-   Mathematical patterns in loops
-   Brute Force vs optimized mathematical solutions
-   Time and space complexity
-   Practice problems

------------------------------------------------------------------------

# 1️⃣ Why Mathematics is Important in DSA?

DSA is not only about data structures.

Many problems can become much easier when we recognize a mathematical
pattern.

For example:

``` text
Problem:
Check whether a number is even.
```

We do not need a complicated algorithm.

We can simply use:

``` text
n % 2 == 0
```

Another example:

``` text
Problem:
Find the GCD of two numbers.
```

Instead of checking every possible divisor, we can use the:

``` text
Euclidean Algorithm
```

Mathematics helps us:

``` text
Understand Patterns
       ↓
Reduce Unnecessary Work
       ↓
Design Better Algorithms
       ↓
Improve Time Complexity
```

> **A good DSA programmer learns to recognize mathematical patterns.**

------------------------------------------------------------------------

# 2️⃣ Number Basics

A number is a mathematical value used for counting, measuring, or
identifying quantities.

Examples:

``` text
0
1
2
3
10
25
100
```

Numbers can be classified in different ways.

------------------------------------------------------------------------

# 3️⃣ Positive, Negative and Zero

## Positive Numbers

Numbers greater than zero are positive.

Examples:

``` text
1
2
5
10
100
```

Condition:

``` text
n > 0
```

------------------------------------------------------------------------

## Negative Numbers

Numbers smaller than zero are negative.

Examples:

``` text
-1
-5
-10
-100
```

Condition:

``` text
n < 0
```

------------------------------------------------------------------------

## Zero

Zero is neither positive nor negative.

``` text
n = 0
```

------------------------------------------------------------------------

## Python Example

``` python
n = -10

if n > 0:
    print("Positive")
elif n < 0:
    print("Negative")
else:
    print("Zero")
```

Output:

``` text
Negative
```

Time Complexity:

``` text
O(1)
```

Space Complexity:

``` text
O(1)
```

------------------------------------------------------------------------

# 4️⃣ Even and Odd Numbers

An even number is divisible by 2.

Examples:

``` text
2
4
6
8
10
12
```

An odd number is not divisible by 2.

Examples:

``` text
1
3
5
7
9
11
```

The easiest way to check this is the modulus operator:

``` text
n % 2
```

If:

``` text
n % 2 == 0
```

then the number is even.

Otherwise:

``` text
Odd
```

------------------------------------------------------------------------

## Python Example

``` python
n = 17

if n % 2 == 0:
    print("Even")
else:
    print("Odd")
```

Output:

``` text
Odd
```

------------------------------------------------------------------------

# 5️⃣ Understanding Remainder

The remainder is what is left after division.

Example:

``` text
10 ÷ 3
```

We can write:

``` text
3 × 3 = 9
```

So:

``` text
10 - 9 = 1
```

Therefore:

``` text
10 % 3 = 1
```

Another example:

``` text
20 % 5 = 0
```

because 20 is completely divisible by 5.

------------------------------------------------------------------------

# 6️⃣ Modulus Operator

The `%` operator gives the remainder.

Examples:

``` text
10 % 3 = 1
15 % 4 = 3
20 % 5 = 0
7 % 2 = 1
```

The modulus operator is extremely important in DSA.

It is commonly used for:

``` text
Even/Odd
Digit Extraction
Divisibility
Circular Arrays
Hashing
Modular Arithmetic
```

------------------------------------------------------------------------

# 7️⃣ Extracting the Last Digit

Suppose:

``` text
n = 12345
```

The last digit can be obtained using:

``` text
n % 10
```

Therefore:

``` text
12345 % 10 = 5
```

So the last digit is:

``` text
5
```

Python:

``` python
n = 12345

last_digit = n % 10

print(last_digit)
```

Output:

``` text
5
```

------------------------------------------------------------------------

# 8️⃣ Removing the Last Digit

To remove the last digit, we can use integer division by 10.

For example:

``` text
12345 // 10 = 1234
```

Again:

``` text
1234 // 10 = 123
```

Again:

``` text
123 // 10 = 12
```

Again:

``` text
12 // 10 = 1
```

Again:

``` text
1 // 10 = 0
```

This is extremely useful for digit-based problems.

------------------------------------------------------------------------

# 9️⃣ Digit Extraction Pattern

A very important DSA pattern is:

``` text
last_digit = n % 10
n = n // 10
```

For example:

``` python
n = 12345

while n > 0:
    digit = n % 10
    print(digit)
    n = n // 10
```

Output:

``` text
5
4
3
2
1
```

Notice that the digits are processed from right to left.

------------------------------------------------------------------------

# 🔟 Counting Digits

Problem:

``` text
Count the number of digits in a number.
```

Example:

``` text
12345
```

There are:

``` text
5 digits
```

We can repeatedly divide by 10.

------------------------------------------------------------------------

## Dry Run

Start:

``` text
n = 12345
count = 0
```

Step 1:

``` text
12345 // 10 = 1234
count = 1
```

Step 2:

``` text
1234 // 10 = 123
count = 2
```

Step 3:

``` text
123 // 10 = 12
count = 3
```

Step 4:

``` text
12 // 10 = 1
count = 4
```

Step 5:

``` text
1 // 10 = 0
count = 5
```

Stop.

Answer:

``` text
5
```

------------------------------------------------------------------------

## Python

``` python
n = 12345
count = 0

while n > 0:
    count += 1
    n //= 10

print(count)
```

Output:

``` text
5
```

Time Complexity:

``` text
O(log₁₀ n)
```

Space Complexity:

``` text
O(1)
```

------------------------------------------------------------------------

# 1️⃣1️⃣ Sum of Digits

Problem:

``` text
Find the sum of digits of a number.
```

Example:

``` text
12345
```

Calculation:

``` text
1 + 2 + 3 + 4 + 5 = 15
```

------------------------------------------------------------------------

## Logic

Repeatedly:

``` text
digit = n % 10
sum = sum + digit
n = n // 10
```

------------------------------------------------------------------------

## Dry Run

For:

``` text
n = 1234
```

Start:

``` text
sum = 0
```

First digit:

``` text
1234 % 10 = 4
sum = 4
```

Remove digit:

``` text
1234 // 10 = 123
```

Next:

``` text
123 % 10 = 3
sum = 7
```

Next:

``` text
12 % 10 = 2
sum = 9
```

Next:

``` text
1 % 10 = 1
sum = 10
```

Answer:

``` text
10
```

------------------------------------------------------------------------

## Python

``` python
n = 1234
total = 0

while n > 0:
    digit = n % 10
    total += digit
    n //= 10

print(total)
```

Output:

``` text
10
```

------------------------------------------------------------------------

# 1️⃣2️⃣ Reverse a Number

Problem:

``` text
Reverse the digits of a number.
```

Example:

``` text
12345
```

Answer:

``` text
54321
```

------------------------------------------------------------------------

## Important Formula

We can build the reversed number using:

``` text
reverse = reverse * 10 + digit
```

where:

``` text
digit = n % 10
```

Then:

``` text
n = n // 10
```

------------------------------------------------------------------------

## Dry Run

Input:

``` text
123
```

Start:

``` text
reverse = 0
```

First:

``` text
digit = 3
reverse = 0 * 10 + 3
reverse = 3
```

Second:

``` text
digit = 2
reverse = 3 * 10 + 2
reverse = 32
```

Third:

``` text
digit = 1
reverse = 32 * 10 + 1
reverse = 321
```

Answer:

``` text
321
```

------------------------------------------------------------------------

## Python

``` python
n = 123

reverse = 0

while n > 0:
    digit = n % 10
    reverse = reverse * 10 + digit
    n //= 10

print(reverse)
```

Output:

``` text
321
```

------------------------------------------------------------------------

# 1️⃣3️⃣ Palindrome Number

A palindrome reads the same from left to right and right to left.

Examples:

``` text
121
1221
1331
555
```

Not palindromes:

``` text
123
1234
120
```

------------------------------------------------------------------------

## Example

Input:

``` text
121
```

Reverse:

``` text
121
```

Since:

``` text
original == reverse
```

the number is a palindrome.

------------------------------------------------------------------------

## Python

``` python
n = 121

original = n
reverse = 0

while n > 0:
    digit = n % 10
    reverse = reverse * 10 + digit
    n //= 10

if original == reverse:
    print("Palindrome")
else:
    print("Not Palindrome")
```

Output:

``` text
Palindrome
```

------------------------------------------------------------------------

# 1️⃣4️⃣ Factors

A factor of a number divides the number exactly.

Example:

``` text
12
```

Factors of 12 are:

``` text
1
2
3
4
6
12
```

because:

``` text
12 % 1 = 0
12 % 2 = 0
12 % 3 = 0
12 % 4 = 0
12 % 6 = 0
12 % 12 = 0
```

------------------------------------------------------------------------

# 1️⃣5️⃣ Finding Factors Using Brute Force

We can check every number from:

``` text
1 to n
```

Example:

``` python
n = 12

for i in range(1, n + 1):
    if n % i == 0:
        print(i)
```

Output:

``` text
1
2
3
4
6
12
```

Time Complexity:

``` text
O(n)
```

This works, but it can be improved.

------------------------------------------------------------------------

# 1️⃣6️⃣ Optimizing Factor Search

If:

``` text
i × j = n
```

then at least one of `i` or `j` must be less than or equal to:

``` text
√n
```

Therefore, we only need to check up to:

``` text
√n
```

Example:

``` text
n = 36
√36 = 6
```

We can check:

``` text
1
2
3
4
5
6
```

and find factor pairs.

------------------------------------------------------------------------

## Python

``` python
n = 36

for i in range(1, int(n ** 0.5) + 1):
    if n % i == 0:
        print(i, n // i)
```

Possible output:

``` text
1 36
2 18
3 12
4 9
6 6
```

Time Complexity:

``` text
O(√n)
```

This is much better than:

``` text
O(n)
```

------------------------------------------------------------------------

# 1️⃣7️⃣ Prime Numbers

A prime number has exactly two positive factors:

``` text
1
itself
```

Examples:

``` text
2
3
5
7
11
13
17
19
```

For example:

``` text
7
```

Factors:

``` text
1
7
```

Therefore, 7 is prime.

------------------------------------------------------------------------

# 1️⃣8️⃣ Is 1 a Prime Number?

No.

The number:

``` text
1
```

has only one positive factor:

``` text
1
```

A prime number must have exactly two positive factors.

Therefore:

``` text
1 → Not Prime
```

------------------------------------------------------------------------

# 1️⃣9️⃣ Composite Numbers

A composite number has more than two positive factors.

Examples:

``` text
4
6
8
9
10
12
```

For example:

``` text
12
```

has factors:

``` text
1, 2, 3, 4, 6, 12
```

Therefore, it is composite.

------------------------------------------------------------------------

# 2️⃣0️⃣ Checking Prime Number

A simple approach is to count factors.

But we can optimize using:

``` text
√n
```

Why?

If a number has a factor greater than √n, it must have a corresponding
factor smaller than √n.

Therefore, if no number from:

``` text
2 to √n
```

divides `n`, then `n` is prime.

------------------------------------------------------------------------

## Python

``` python
n = 29

if n < 2:
    print("Not Prime")
else:
    is_prime = True

    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            is_prime = False
            break

    if is_prime:
        print("Prime")
    else:
        print("Not Prime")
```

Output:

``` text
Prime
```

Time Complexity:

``` text
O(√n)
```

Space Complexity:

``` text
O(1)
```

------------------------------------------------------------------------

# 2️⃣1️⃣ Prime Factorization

Prime factorization means representing a number as a product of prime
numbers.

Example:

``` text
12
```

We can write:

``` text
12 = 2 × 2 × 3
```

Therefore:

``` text
Prime Factors = 2, 2, 3
```

Another example:

``` text
60 = 2 × 2 × 3 × 5
```

------------------------------------------------------------------------

## Python

``` python
n = 60

factor = 2

while factor * factor <= n:
    while n % factor == 0:
        print(factor)
        n //= factor

    factor += 1

if n > 1:
    print(n)
```

Output:

``` text
2
2
3
5
```

------------------------------------------------------------------------

# 2️⃣2️⃣ GCD

GCD means:

> **Greatest Common Divisor**

It is the largest number that divides two numbers exactly.

Example:

``` text
12 and 18
```

Factors of 12:

``` text
1, 2, 3, 4, 6, 12
```

Factors of 18:

``` text
1, 2, 3, 6, 9, 18
```

Common factors:

``` text
1, 2, 3, 6
```

Largest common factor:

``` text
6
```

Therefore:

``` text
GCD(12, 18) = 6
```

------------------------------------------------------------------------

# 2️⃣3️⃣ Euclidean Algorithm

A very important mathematical algorithm is the:

``` text
Euclidean Algorithm
```

It finds GCD efficiently.

The main idea is:

``` text
GCD(a, b) = GCD(b, a % b)
```

Continue until:

``` text
b = 0
```

Then:

``` text
GCD = a
```

------------------------------------------------------------------------

## Example

Find:

``` text
GCD(48, 18)
```

Step 1:

``` text
48 % 18 = 12
```

So:

``` text
GCD(48, 18)
= GCD(18, 12)
```

Step 2:

``` text
18 % 12 = 6
```

So:

``` text
GCD(18, 12)
= GCD(12, 6)
```

Step 3:

``` text
12 % 6 = 0
```

Therefore:

``` text
GCD = 6
```

------------------------------------------------------------------------

## Python

``` python
a = 48
b = 18

while b != 0:
    a, b = b, a % b

print(a)
```

Output:

``` text
6
```

Time Complexity:

``` text
O(log(min(a, b)))
```

Space Complexity:

``` text
O(1)
```

------------------------------------------------------------------------

# 2️⃣4️⃣ LCM

LCM means:

> **Least Common Multiple**

It is the smallest positive number that is divisible by both numbers.

Example:

``` text
4 and 6
```

Multiples of 4:

``` text
4, 8, 12, 16, 20, 24...
```

Multiples of 6:

``` text
6, 12, 18, 24...
```

The smallest common multiple is:

``` text
12
```

Therefore:

``` text
LCM(4, 6) = 12
```

------------------------------------------------------------------------

# 2️⃣5️⃣ GCD and LCM Relationship

For two positive integers:

``` text
a × b = GCD(a, b) × LCM(a, b)
```

Therefore:

``` text
LCM(a, b) = |a × b| / GCD(a, b)
```

Example:

``` text
a = 12
b = 18
```

We know:

``` text
GCD = 6
```

Therefore:

``` text
LCM = (12 × 18) / 6
```

``` text
LCM = 36
```

------------------------------------------------------------------------

## Python

``` python
import math

a = 12
b = 18

gcd = math.gcd(a, b)
lcm = abs(a * b) // gcd

print("GCD:", gcd)
print("LCM:", lcm)
```

Output:

``` text
GCD: 6
LCM: 36
```

------------------------------------------------------------------------

# 2️⃣6️⃣ Power of a Number

Suppose:

``` text
2³
```

This means:

``` text
2 × 2 × 2
```

Answer:

``` text
8
```

Another example:

``` text
5² = 25
```

In Python:

``` python
print(2 ** 3)
```

Output:

``` text
8
```

------------------------------------------------------------------------

# 2️⃣7️⃣ Calculating Power Using a Loop

We can calculate:

``` text
a^b
```

by multiplying `a`, `b` times.

Example:

``` python
a = 2
b = 5

result = 1

for _ in range(b):
    result *= a

print(result)
```

Output:

``` text
32
```

Time Complexity:

``` text
O(b)
```

------------------------------------------------------------------------

# 2️⃣8️⃣ Fast Exponentiation

If the exponent is very large, repeatedly multiplying can be slow.

We can use:

``` text
Binary Exponentiation
```

The main idea is to repeatedly divide the exponent by 2.

For example:

``` text
a^10
```

Instead of multiplying 10 times, we can use:

``` text
a^10
= (a^5)^2
```

and:

``` text
a^5
= a × a^4
```

This reduces the number of operations significantly.

------------------------------------------------------------------------

## Python

``` python
def power(a, b):
    result = 1

    while b > 0:
        if b % 2 == 1:
            result *= a

        a *= a
        b //= 2

    return result

print(power(2, 10))
```

Output:

``` text
1024
```

Time Complexity:

``` text
O(log b)
```

Space Complexity:

``` text
O(1)
```

------------------------------------------------------------------------

# 2️⃣9️⃣ Modular Arithmetic

Sometimes numbers become extremely large.

Instead of storing the entire result, we can work with the remainder.

For example:

``` text
17 % 5 = 2
```

Modular arithmetic is commonly used in DSA and competitive programming.

------------------------------------------------------------------------

## Basic Properties

For addition:

``` text
(a + b) % m
```

can be calculated using:

``` text
((a % m) + (b % m)) % m
```

For multiplication:

``` text
(a × b) % m
```

can be calculated using:

``` text
((a % m) × (b % m)) % m
```

This helps keep numbers smaller.

------------------------------------------------------------------------

# 3️⃣0️⃣ Example of Modular Arithmetic

Suppose:

``` text
a = 17
b = 23
m = 5
```

We want:

``` text
(a + b) % m
```

Directly:

``` text
(17 + 23) % 5
= 40 % 5
= 0
```

Using remainders:

``` text
17 % 5 = 2
23 % 5 = 3
```

Then:

``` text
(2 + 3) % 5
= 5 % 5
= 0
```

Same answer.

------------------------------------------------------------------------

# 3️⃣1️⃣ Armstrong Number

An Armstrong number is a number that equals the sum of its digits raised
to the power of the number of digits.

For a 3-digit number:

``` text
153
```

Calculation:

``` text
1³ + 5³ + 3³
```

``` text
1 + 125 + 27
= 153
```

Therefore:

``` text
153 → Armstrong Number
```

Another example:

``` text
370
371
407
```

------------------------------------------------------------------------

## Python

``` python
n = 153

original = n
digits = len(str(n))
total = 0

while n > 0:
    digit = n % 10
    total += digit ** digits
    n //= 10

if total == original:
    print("Armstrong Number")
else:
    print("Not Armstrong Number")
```

Output:

``` text
Armstrong Number
```

------------------------------------------------------------------------

# 3️⃣2️⃣ Perfect Number

A perfect number is a number whose proper divisors add up to the number
itself.

Example:

``` text
6
```

Proper divisors:

``` text
1
2
3
```

Sum:

``` text
1 + 2 + 3 = 6
```

Therefore:

``` text
6 → Perfect Number
```

Another perfect number is:

``` text
28
```

because:

``` text
1 + 2 + 4 + 7 + 14 = 28
```

------------------------------------------------------------------------

## Python

``` python
n = 28
total = 0

for i in range(1, n):
    if n % i == 0:
        total += i

if total == n:
    print("Perfect Number")
else:
    print("Not Perfect Number")
```

Output:

``` text
Perfect Number
```

The straightforward solution takes:

``` text
O(n)
```

It can be optimized using factor pairs and `√n`.

------------------------------------------------------------------------

# 3️⃣3️⃣ Sum of First N Natural Numbers

Suppose:

``` text
N = 5
```

Then:

``` text
1 + 2 + 3 + 4 + 5 = 15
```

A loop takes:

``` text
O(n)
```

But mathematics gives us a direct formula:

``` text
sum = n × (n + 1) / 2
```

For:

``` text
n = 5
```

we get:

``` text
5 × 6 / 2
= 15
```

------------------------------------------------------------------------

## Python

``` python
n = 5

total = n * (n + 1) // 2

print(total)
```

Output:

``` text
15
```

Time Complexity:

``` text
O(1)
```

Space Complexity:

``` text
O(1)
```

This is an important example of mathematical optimization.

------------------------------------------------------------------------

# 3️⃣4️⃣ Sum of Squares

The sum of squares from 1 to `n` is:

``` text
1² + 2² + 3² + ... + n²
```

Formula:

``` text
n × (n + 1) × (2n + 1) / 6
```

Example:

``` text
n = 3
```

Then:

``` text
1² + 2² + 3²
= 1 + 4 + 9
= 14
```

Formula:

``` text
3 × 4 × 7 / 6
= 14
```

------------------------------------------------------------------------

# 3️⃣5️⃣ Sum of First N Odd Numbers

Consider:

``` text
1 + 3 + 5 + 7 + 9
```

The first 5 odd numbers sum to:

``` text
25
```

Formula:

``` text
n²
```

Therefore:

``` text
1st odd number → 1² = 1
2nd odd numbers → 2² = 4
3rd odd numbers → 3² = 9
5th odd numbers → 5² = 25
```

This is a useful mathematical pattern.

------------------------------------------------------------------------

# 3️⃣6️⃣ Logarithm --- Basic DSA Idea

You will frequently see:

``` text
O(log n)
```

in DSA.

The basic idea is repeated division.

For example:

``` text
16
↓ divide by 2
8
↓
4
↓
2
↓
1
```

We divided 16 by 2 four times.

Therefore:

``` text
log₂(16) = 4
```

Similarly:

``` text
log₂(8) = 3
log₂(32) = 5
log₂(64) = 6
```

This concept appears in:

``` text
Binary Search
Binary Exponentiation
Balanced Trees
Divide and Conquer
```

------------------------------------------------------------------------

# 3️⃣7️⃣ Why O(log n) is Fast

Suppose:

``` text
n = 1,000,000
```

An:

``` text
O(n)
```

algorithm may need roughly:

``` text
1,000,000 operations
```

But an:

``` text
O(log₂ n)
```

algorithm needs only around:

``` text
20 operations
```

because:

``` text
2²⁰ ≈ 1,048,576
```

This is why logarithmic algorithms are powerful.

------------------------------------------------------------------------

# 3️⃣8️⃣ Mathematical Patterns in DSA

Many DSA problems can be solved by recognizing patterns.

Examples:

``` text
Even/Odd
    ↓
Modulo

Digits
    ↓
% 10 and // 10

Prime
    ↓
Check divisors up to √n

GCD
    ↓
Euclidean Algorithm

LCM
    ↓
GCD relationship

Power
    ↓
Binary Exponentiation

Search in sorted data
    ↓
Logarithmic thinking
```

------------------------------------------------------------------------

# 3️⃣9️⃣ Brute Force vs Mathematical Optimization

Suppose we need:

``` text
Sum from 1 to 1,000,000
```

### Brute Force

``` python
total = 0

for i in range(1, 1_000_001):
    total += i
```

Time Complexity:

``` text
O(n)
```

### Mathematical Formula

``` python
n = 1_000_000

total = n * (n + 1) // 2
```

Time Complexity:

``` text
O(1)
```

Same answer.

Very different efficiency.

> **The goal is not only to get the correct answer. The goal is to find
> an efficient way to get it.**

------------------------------------------------------------------------

# 4️⃣0️⃣ Important Mathematical DSA Formulas

Keep these formulas in your notes.

## Sum of First N Natural Numbers

``` text
n(n + 1) / 2
```

## Sum of Squares

``` text
n(n + 1)(2n + 1) / 6
```

## Sum of First N Odd Numbers

``` text
n²
```

## GCD and LCM

``` text
a × b = GCD(a, b) × LCM(a, b)
```

Therefore:

``` text
LCM(a, b) = |a × b| / GCD(a, b)
```

## Last Digit

``` text
n % 10
```

## Remove Last Digit

``` text
n // 10
```

## Reverse Number

``` text
reverse = reverse × 10 + digit
```

------------------------------------------------------------------------

# 4️⃣1️⃣ Important Number Patterns

## Pattern 1 --- Even Number

``` text
n % 2 == 0
```

## Pattern 2 --- Divisible by K

``` text
n % k == 0
```

## Pattern 3 --- Last Digit

``` text
n % 10
```

## Pattern 4 --- Remove Last Digit

``` text
n // 10
```

## Pattern 5 --- Digit Processing

``` python
while n > 0:
    digit = n % 10
    n //= 10
```

## Pattern 6 --- Prime Checking

``` text
Check divisors up to √n
```

## Pattern 7 --- GCD

``` text
a, b = b, a % b
```

------------------------------------------------------------------------

# 4️⃣2️⃣ Complete Example: Count Even Digits

Problem:

``` text
Count how many even digits are present in a number.
```

Input:

``` text
123456
```

Even digits:

``` text
2
4
6
```

Answer:

``` text
3
```

------------------------------------------------------------------------

## Python

``` python
n = 123456
count = 0

while n > 0:
    digit = n % 10

    if digit % 2 == 0:
        count += 1

    n //= 10

print(count)
```

Output:

``` text
3
```

Time Complexity:

``` text
O(log n)
```

Space Complexity:

``` text
O(1)
```

------------------------------------------------------------------------

# 4️⃣3️⃣ Complete Example: Largest Digit

Problem:

``` text
Find the largest digit in a number.
```

Input:

``` text
58329
```

Digits:

``` text
5, 8, 3, 2, 9
```

Largest:

``` text
9
```

------------------------------------------------------------------------

## Python

``` python
n = 58329
largest = 0

while n > 0:
    digit = n % 10

    if digit > largest:
        largest = digit

    n //= 10

print(largest)
```

Output:

``` text
9
```

Time Complexity:

``` text
O(log n)
```

Space Complexity:

``` text
O(1)
```

------------------------------------------------------------------------

# 4️⃣4️⃣ Complete Example: Smallest Digit

Input:

``` text
58329
```

Digits:

``` text
5, 8, 3, 2, 9
```

Smallest:

``` text
2
```

Python:

``` python
n = 58329

smallest = 9

while n > 0:
    digit = n % 10

    if digit < smallest:
        smallest = digit

    n //= 10

print(smallest)
```

Output:

``` text
2
```

------------------------------------------------------------------------

# 4️⃣5️⃣ Complete Example: Product of Digits

Problem:

``` text
Find the product of all digits.
```

Input:

``` text
1234
```

Calculation:

``` text
1 × 2 × 3 × 4 = 24
```

Python:

``` python
n = 1234
product = 1

while n > 0:
    digit = n % 10
    product *= digit
    n //= 10

print(product)
```

Output:

``` text
24
```

------------------------------------------------------------------------

# 4️⃣6️⃣ Important Edge Cases

When solving mathematical problems, always consider:

``` text
0
1
Negative numbers
Single-digit numbers
Repeated digits
Very large numbers
Numbers ending in zero
Prime numbers
Perfect squares
```

For example:

``` text
Reverse 120
```

Mathematically:

``` text
021
```

But as an integer:

``` text
21
```

The leading zero disappears.

Always understand what the problem expects.

------------------------------------------------------------------------

# 4️⃣7️⃣ DSA Problem-Solving Framework for Mathematics

Whenever I see a mathematical DSA problem, I will follow:

``` text
Read the Problem
        ↓
Identify the Number/Values
        ↓
Understand the Required Output
        ↓
Check Constraints
        ↓
Look for Mathematical Patterns
        ↓
Try a Simple Solution
        ↓
Find a Formula or Optimization
        ↓
Write Pseudocode
        ↓
Dry Run
        ↓
Write Code
        ↓
Test Edge Cases
        ↓
Analyze Time Complexity
        ↓
Analyze Space Complexity
```

------------------------------------------------------------------------

# 🧪 4️⃣8️⃣ Practice Problems

## Beginner Problems

``` text
1. Check Positive, Negative or Zero

2. Check Even or Odd

3. Find the Remainder

4. Find the Last Digit

5. Count Digits

6. Find Sum of Digits

7. Find Product of Digits

8. Find Largest Digit

9. Find Smallest Digit

10. Reverse a Number
```

------------------------------------------------------------------------

## Intermediate Problems

``` text
11. Check Palindrome Number

12. Check Prime Number

13. Print All Factors

14. Count Factors

15. Find Prime Factors

16. Find GCD

17. Find LCM

18. Check Armstrong Number

19. Check Perfect Number

20. Calculate Power
```

------------------------------------------------------------------------

## Thinking Problems

``` text
21. Find the Sum of First N Natural Numbers

22. Find the Sum of Squares from 1 to N

23. Find the Sum of First N Odd Numbers

24. Count Even Digits

25. Count Odd Digits

26. Find the Frequency of a Digit

27. Find the Second Largest Digit

28. Find the Difference Between Largest and Smallest Digit

29. Check Whether a Number Contains Zero

30. Find the Number of Factors of N
```

------------------------------------------------------------------------

# 🧠 4️⃣9️⃣ Questions I Should Ask Myself

When I see a number problem, I should ask:

``` text
Is it asking about divisibility?

        ↓

Can I use % ?

        ↓

Is it asking about digits?

        ↓

Can I use % 10 and // 10?

        ↓

Is it asking about factors?

        ↓

Can I stop at √n?

        ↓

Is it asking for GCD?

        ↓

Can I use the Euclidean Algorithm?

        ↓

Is there a mathematical formula?

        ↓

Can I reduce O(n) to O(1) or O(log n)?
```

This way of thinking will become very useful in future DSA problems.

------------------------------------------------------------------------

# 🎯 Key Takeaways

-   Mathematics is an important foundation for DSA.
-   `%` gives the remainder.
-   `//` performs integer division in Python.
-   `n % 10` extracts the last digit.
-   `n // 10` removes the last digit.
-   Digit problems often use `% 10` and `// 10`.
-   Even numbers satisfy `n % 2 == 0`.
-   Prime numbers have exactly two positive factors.
-   Checking divisors up to `√n` improves prime checking.
-   GCD can be found efficiently using the Euclidean Algorithm.
-   LCM can be calculated using the relationship between GCD and LCM.
-   Mathematical formulas can reduce an `O(n)` solution to `O(1)`.
-   Binary exponentiation reduces power calculation from `O(n)` to
    `O(log n)`.
-   Logarithms are important for understanding algorithms such as Binary
    Search.
-   Always check edge cases.
-   Always look for mathematical patterns before writing unnecessary
    loops.

------------------------------------------------------------------------

# 🚀 Day 3 Progress

``` text
Day 01 → Introduction to DSA ✅

Day 02 → Problem-Solving Fundamentals ✅

Day 03 → Mathematics for DSA ✅

Day 04 → Arrays 🔜
```

> **First learn how to think. Then learn how to recognize patterns. Then
> learn how to optimize.**

🚀 **The DSA journey continues...**
