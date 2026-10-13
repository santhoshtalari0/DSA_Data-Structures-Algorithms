# Day 11 — Linked Lists in DSA

> Goal: Understand nodes, references, traversal, insertion, deletion, and common linked-list patterns.

## 1. What Is a Linked List?
A linked list stores values in **nodes**. Each node holds a value and a reference to the next node.

```text
head
 ↓
[10 | next] → [20 | next] → [30 | None]
```

- **Node:** holds a value and a link.
- **Head:** first node.
- **Tail:** final node in a singly linked list.
- **None:** no next node.
- **Traversal:** visiting nodes by following links.

Unlike arrays, nodes need not sit next to each other in memory. Reaching a later node requires following links from the head.

## 2. Create a Node in Python

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None
```

Build a list manually:

```python
first = Node(10)
second = Node(20)
third = Node(30)
first.next = second
second.next = third
head = first
```

Now `head` refers to `10 → 20 → 30 → None`.

## 3. Traverse a Linked List

```python
def print_list(head):
    current = head
    while current is not None:
        print(current.value)
        current = current.next
```

Time: **O(n)**; extra space: **O(1)**. Use `current` so you do not lose the original head reference.

## 4. Convert a Python List to a Linked List

```python
def build_linked_list(values):
    dummy = Node(0)
    tail = dummy

    for value in values:
        tail.next = Node(value)
        tail = tail.next

    return dummy.next
```

The dummy node is temporary; `dummy.next` is the first real node.

## 5. Convert a Linked List to a Python List

```python
def to_list(head):
    result = []
    current = head

    while current is not None:
        result.append(current.value)
        current = current.next

    return result
```

Time: **O(n)**; output space: **O(n)**.

## 6. Insert at the Beginning

```python
def insert_front(head, value):
    node = Node(value)
    node.next = head
    return node
```

Use `head = insert_front(head, 10)` because the head changes. Time: **O(1)**.

## 7. Insert at the End

```python
def insert_end(head, value):
    node = Node(value)

    if head is None:
        return node

    current = head
    while current.next is not None:
        current = current.next

    current.next = node
    return head
```

Time: **O(n)** without a tail reference; extra space: **O(1)**.

## 8. Insert After a Given Node

```python
def insert_after(node, value):
    if node is None:
        return

    new_node = Node(value)
    new_node.next = node.next
    node.next = new_node
```

First link the new node to the old next node, then link the current node to the new node. Time: **O(1)** when the node reference is already known.

## 9. Delete the First Node

```python
def delete_front(head):
    if head is None:
        return None
    return head.next
```

Time: **O(1)**. The caller should assign the returned head.

## 10. Delete the First Matching Value

```python
def delete_value(head, target):
    if head is None:
        return None

    if head.value == target:
        return head.next

    current = head
    while current.next is not None:
        if current.next.value == target:
            current.next = current.next.next
            return head
        current = current.next

    return head
```

Deletes only the first match. If the target is absent, the list remains unchanged. Time: **O(n)**; extra space: **O(1)**.

## 11. Search for a Value

```python
def contains(head, target):
    current = head
    while current is not None:
        if current.value == target:
            return True
        current = current.next
    return False
```

Time: **O(n)**; extra space: **O(1)**). There is no direct indexed access; reaching a position requires traversal.

## 12. Find the Length

```python
def length(head):
    count = 0
    current = head
    while current is not None:
        count += 1
        current = current.next
    return count
```

Time: **O(n)**; extra space: **O(1)**.

## 13. Reverse a Singly Linked List

Use three references:
- `previous`: node before the current node.
- `current`: node being processed.
- `next_node`: saved next node, so the rest of the list is not lost.

```python
def reverse_list(head):
    previous = None
    current = head

    while current is not None:
        next_node = current.next
        current.next = previous
        previous = current
        current = next_node

    return previous
```

Dry run:

```text
Before: 10 → 20 → 30 → None
Step 1: None ← 10    20 → 30
Step 2: None ← 10 ← 20    30
Step 3: None ← 10 ← 20 ← 30
New head: 30
```

Time: **O(n)**; extra space: **O(1)**. Save `current.next` before changing the link.

## 14. Find the Middle — Slow and Fast Pointers

```python
def middle_node(head):
    slow = fast = head

    while fast is not None and fast.next is not None:
        slow = slow.next
        fast = fast.next.next

    return slow
```

For an even number of nodes, this returns the **second middle**. Time: **O(n)**; extra space: **O(1)**.

## 15. Detect a Cycle — Floyd's Algorithm

A cycle means following links can return to a previously visited node instead of reaching `None`.

```python
def has_cycle(head):
    slow = fast = head

    while fast is not None and fast.next is not None:
        slow = slow.next
        fast = fast.next.next

        if slow is fast:
            return True

    return False
```

Inside a cycle, the fast pointer eventually catches the slow pointer. Use `is` to test whether both references point to the same node.

Time: **O(n)**; extra space: **O(1)**.

## 16. Merge Two Sorted Linked Lists

```python
def merge_sorted_lists(a, b):
    dummy = Node(0)
    tail = dummy

    while a is not None and b is not None:
        if a.value <= b.value:
            tail.next = a
            a = a.next
        else:
            tail.next = b
            b = b.next
        tail = tail.next

    tail.next = a if a is not None else b
    return dummy.next
```

Example:
```text
A: 1 → 3 → 7
B: 2 → 4 → 6
Merged: 1 → 2 → 3 → 4 → 6 → 7
```

Time: **O(n + m)**; auxiliary space: **O(1)** because existing nodes are reused.

## 17. Remove Duplicates From a Sorted Linked List

```python
def remove_duplicates_sorted(head):
    current = head

    while current is not None and current.next is not None:
        if current.value == current.next.value:
            current.next = current.next.next
        else:
            current = current.next

    return head
```

Assumes sorted input. Time: **O(n)**; extra space: **O(1)**.

## 18. Singly vs Doubly Linked Lists

Singly linked list:
```text
10 → 20 → 30 → None
```

Doubly linked list:
```text
None ← 10 ⇄ 20 ⇄ 30 → None
```

| Feature | Singly linked | Doubly linked |
|---|---|---|
| Link fields | Next | Next and previous |
| Forward traversal | Yes | Yes |
| Backward traversal | No | Yes |
| Memory per node | Lower | Higher |
| Delete a known node | May need previous node | Can relink neighbors if links are valid |

With doubly linked lists, keep both `next` and `prev` links consistent.

## 19. Linked List vs Array

| Operation | Array / Python list | Singly linked list |
|---|---:|---:|
| Access by index | O(1) | O(n) |
| Search by value | O(n) | O(n) |
| Insert at front | O(n) for shifting | O(1) |
| Insert after a known node | Not generally O(1) | O(1) |
| Delete front | O(n) for shifting | O(1) |
| Traverse all | O(n) | O(n) |

Appending to a linked list is **O(1)** only if a tail reference is maintained; otherwise it is **O(n)**.

## 20. Common Mistakes

1. Overwriting `current.next` before saving the rest of the list.
2. Forgetting to return the new head.
3. Not handling an empty list.
4. Accessing `current.next` when `current` is `None`.
5. Moving `head` during traversal instead of using another reference.
6. Confusing node identity with equal values.
7. Assuming direct indexed access.
8. Forgetting that a cycle prevents traversal from reaching `None`.
9. Updating `next` but forgetting `prev` in a doubly linked list.

---

# Practice Problems

## Beginner
1. Build a linked list from a Python list.
2. Print every node value.
3. Count the nodes.
4. Search for a value.
5. Insert at the beginning.
6. Insert at the end.
7. Delete the first node.
8. Delete the first occurrence of a value.
9. Find the middle node.
10. Reverse a singly linked list iteratively.

## Intermediate
11. Detect a cycle.
12. Find the node where a cycle begins.
13. Merge two sorted linked lists.
14. Remove duplicates from a sorted list.
15. Find the kth node from the end.
16. Remove the nth node from the end.
17. Check whether a linked list is a palindrome.
18. Add two numbers represented by linked lists.
19. Sort a linked list using merge sort.
20. Design a doubly linked list with insertion and deletion.

---

# Quick Revision

- A node stores a value and one or more links.
- `head` is the entry point.
- Traversal follows links until `None`.
- Front insertion and deletion take **O(1)**.
- Reversal uses `previous`, `current`, and `next_node`.
- Slow/fast pointers find the middle and detect cycles.
- Merging sorted lists takes **O(n + m)**.
- Linked lists trade fast indexed access for flexible link changes.

> **Golden rule:** Before changing a link, ask: “Have I saved the reference to the rest of the list?”

## Day 12 Preview
**Stacks and Queues** — LIFO/FIFO, core operations, implementations, and common DSA patterns.
