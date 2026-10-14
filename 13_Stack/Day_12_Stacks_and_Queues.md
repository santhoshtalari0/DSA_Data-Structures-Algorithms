## 1. Learning goals

By the end of this lesson, you should be able to:
- Explain **LIFO** and **FIFO**.
- Implement a stack with a Python list.
- Use `collections.deque` for an efficient queue.
- Solve bracket-matching and next-greater-element problems.
- Recognize when a stack or queue is the right tool.

---

## 2. Stack: Last In, First Out (LIFO)

A **stack** is a linear data structure where the most recently added item is removed first. Think of a pile of plates: you add and remove plates from the top.

| Operation | Meaning | Typical time |
|---|---|---:|
| `push(x)` | Add `x` to the top | O(1) amortized |
| `pop()` | Remove and return the top item | O(1) amortized |
| `peek()` | Read the top without removing it | O(1) |
| `is_empty()` | Check whether empty | O(1) |

Python lists support stack operations efficiently at the end:

```python
stack = []
stack.append(10)  # push
stack.append(20)
stack.append(30)

print(stack[-1])  # peek: 30
print(stack.pop())  # pop: 30
print(stack)  # [10, 20]
```

A reusable implementation:

```python
class Stack:
    def __init__(self):
        self.items = []

    def push(self, value):
        self.items.append(value)

    def pop(self):
        if not self.items:
            raise IndexError("pop from empty stack")
        return self.items.pop()

    def peek(self):
        if not self.items:
            raise IndexError("peek from empty stack")
        return self.items[-1]

    def is_empty(self):
        return len(self.items) == 0

    def size(self):
        return len(self.items)
```

Avoid `list.pop(0)` for stack operations. Removing from the front shifts remaining elements and takes O(n).

---

## 3. Queue: First In, First Out (FIFO)

A **queue** removes items in the order they were added. Think of people waiting in a line.

| Operation | Meaning | Typical time |
|---|---|---:|
| `enqueue(x)` | Add `x` to the rear | O(1) |
| `dequeue()` | Remove the front item | O(1) with `deque` |
| `front()` | Read the first item | O(1) |
| `is_empty()` | Check whether empty | O(1) |

Use `collections.deque`:

```python
from collections import deque

queue = deque()
queue.append(10)       # enqueue
queue.append(20)
queue.append(30)

print(queue[0])        # front: 10
print(queue.popleft()) # dequeue: 10
print(queue)           # deque([20, 30])
```

For a queue, use `append()` at the rear and `popleft()` at the front.

Avoid this for large queues:

```python
queue = []
queue.append(10)
queue.pop(0)  # O(n): elements must shift
```

---

## 4. Stack vs queue

| Feature | Stack | Queue |
|---|---|---|
| Ordering rule | LIFO | FIFO |
| Add operation | Push | Enqueue |
| Remove operation | Pop from top | Dequeue from front |
| Common use | Undo, nested structures, DFS | Task scheduling, BFS |
| Python choice | `list` | `collections.deque` |

Choose the structure based on **which item must be processed next**.

---

## 5. Application: balanced brackets

A bracket string is balanced when every opening bracket has a matching closing bracket in the correct order.

Examples: `([{}])` is balanced; `([)]` and `((` are not.

### Approach
1. Push each opening bracket.
2. For a closing bracket, the stack must contain its matching opening bracket on top.
3. Pop the match.
4. At the end, the stack must be empty.

```python
def is_balanced(text):
    stack = []
    matching_open = {")": "(", "]": "[", "}": "{"}

    for char in text:
        if char in "([{":
            stack.append(char)
        elif char in matching_open:
            if not stack or stack[-1] != matching_open[char]:
                return False
            stack.pop()

    return len(stack) == 0


print(is_balanced("([{}])"))  # True
print(is_balanced("([)]"))    # False
print(is_balanced("((()))"))  # True
```

**Complexity:** O(n) time and O(n) worst-case auxiliary space, where `n` is the string length.

Why does `([)]` fail? When `)` arrives, `[` is on top, so it cannot match.

---

## 6. Application: next greater element

For each element, find the first element to its right that is strictly greater. If none exists, use `-1`.

```text
Input:  [2, 1, 2, 4, 3]
Output: [4, 2, 4, -1, -1]
```

The brute-force method scans to the right for every element and can take O(n²) time.

### Efficient approach: monotonic stack

Keep indices whose next greater element has not been found. The stack stores indices in decreasing order of their values from bottom to top. When a larger value appears, it resolves pending indices.

```python
def next_greater_elements(nums):
    result = [-1] * len(nums)
    stack = []  # indices waiting for a greater value

    for i, value in enumerate(nums):
        while stack and nums[stack[-1]] < value:
            previous_index = stack.pop()
            result[previous_index] = value
        stack.append(i)

    return result


print(next_greater_elements([2, 1, 2, 4, 3]))
# [4, 2, 4, -1, -1]
```

**Complexity:** O(n) time and O(n) extra space. Each index is pushed once and popped at most once, so total stack operations are O(n), despite the nested `while` loop.

---

## 7. Reverse data with a stack

A stack reverses order because items come out in the opposite order from which they went in.

```python
def reverse_with_stack(items):
    stack = []
    for item in items:
        stack.append(item)

    reversed_items = []
    while stack:
        reversed_items.append(stack.pop())

    return reversed_items


print(reverse_with_stack([1, 2, 3, 4]))  # [4, 3, 2, 1]
```

This takes O(n) time and O(n) extra space. In real Python code, `items[::-1]` or `list(reversed(items))` is usually simpler; this example demonstrates the stack.

---

## 8. Circular queue: the idea

A **circular queue** treats the final array position as connected to the first. After the rear reaches the last index, it can wrap around to index `0` if space is available.

```python
next_index = (current_index + 1) % capacity
```

Modulo wraps the index around. A circular queue avoids shifting all elements on each dequeue.

A correct implementation must distinguish an empty queue from a full one. Common designs store the current size or reserve one array slot.

---

## 9. Where stacks and queues are useful

**Stacks**
- Bracket matching and expression parsing
- Undo/redo histories
- Depth-first search (DFS)
- Next-greater-element and other monotonic-stack problems

**Queues**
- Breadth-first search (BFS), visiting tree or graph nodes level by level
- Task scheduling and arrival-order processing
- Buffers between producers and consumers
- Simulations of people or jobs waiting in line

---

## 10. Complexity recap

| Operation | Recommended structure | Time |
|---|---|---:|
| Stack push | `list.append(x)` | O(1) amortized |
| Stack pop | `list.pop()` | O(1) amortized |
| Stack peek | `stack[-1]` | O(1) |
| Queue enqueue | `deque.append(x)` | O(1) |
| Queue dequeue | `deque.popleft()` | O(1) |
| Queue front | `queue[0]` | O(1) |
| Balanced brackets | Stack | O(n) |
| Next greater element | Monotonic stack | O(n) |

---

## 11. Common mistakes

1. **Using `pop(0)` for a queue:** O(n), because later elements shift.
2. **Popping an empty stack:** check emptiness when input may be invalid.
3. **Checking only bracket counts:** `([)]` has matching counts but incorrect order.
4. **Forgetting the final stack check:** leftover opening brackets mean the string is unbalanced.
5. **Using values instead of indices in next-greater-element problems:** indices identify which result position to update and handle duplicates.
6. **Assuming every nested loop is O(n²):** each item in the monotonic-stack algorithm is pushed once and popped at most once.
7. **Choosing the wrong structure:** use a stack for newest-first processing and a queue for oldest-first processing.

---

## 12. Practice problems

Try these without looking at a solution first.

### Beginner
1. Implement a stack with `push`, `pop`, `peek`, `is_empty`, and `size`.
2. Implement a queue using `collections.deque`.
3. Reverse a string using a stack.
4. Check whether a string containing only `(` and `)` is balanced.
5. Check balanced `()`, `[]`, and `{}` in a mixed string.
6. Design a stack that supports retrieving the minimum element.
7. Simulate a queue of people being served in arrival order.

### Intermediate
8. Evaluate a postfix expression such as `2 3 + 4 *`.
9. Convert a decimal number to binary using a stack.
10. Find the next greater element for every array element.
11. Find the next smaller element for every array element.
12. Find the previous greater element for every array element.
13. Remove adjacent duplicate characters using a stack.
14. Simplify a Unix-style path such as `/a/./b/../c`.
15. Calculate the stock span for each day from a list of prices.
16. Implement a fixed-capacity circular queue.
17. Use a queue to generate binary numbers from `1` through `n`.

### Challenge
18. Find the largest rectangle in a histogram using a monotonic stack.
19. Find the maximum value in every sliding window of size `k` using a deque.
20. Implement a queue using two stacks.
21. Implement a stack using two queues.
22. Perform level-order traversal of a binary tree using a queue.
23. Perform iterative depth-first traversal using a stack.
24. Find the next greater element in a circular array.

---

## 13. Quick self-check

Make sure you can answer:
- What is the difference between LIFO and FIFO?
- Why is `deque.popleft()` preferable to `list.pop(0)` for a queue?
- Why must a bracket checker verify bracket order?
- Why does the next-greater-element algorithm run in O(n)?
- When would you choose a queue instead of a stack?

**Day 12 checkpoint:** implement a stack, implement a queue with `deque`, solve balanced brackets, and solve next greater element. Then attempt at least five practice problems.
