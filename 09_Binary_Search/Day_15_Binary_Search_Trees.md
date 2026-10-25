
## 1. Learning goals
- Understand the BST ordering rule.
- Search, insert, and delete values.
- Find minimum, maximum, predecessor, and successor.
- Validate whether a tree is a BST.
- Understand balanced versus skewed BST complexity.

## 2. What is a BST?

A **Binary Search Tree (BST)** is a binary tree organized by value. In this lesson, duplicate values are not inserted:
- Values smaller than a node go into its left subtree.
- Values larger than a node go into its right subtree.
- The rule applies to the entire subtree, not just immediate children.

```text
          8
        /   \\
       3     10
      / \\      \\
     1   6      14
        / \\     /
       4   7   13
```

A **binary tree** allows up to two children but has no required value ordering. A **BST** is a binary tree that follows the ordering rule.

## 3. Node structure

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None
```

## 4. Search

Compare the target with each current node. Go left if the target is smaller, right if larger, and stop when found or a `None` child is reached.

```python
def search(root, target):
    current = root
    while current is not None:
        if target == current.value:
            return True
        elif target < current.value:
            current = current.left
        else:
            current = current.right
    return False
```

Searching for `7` in the example follows `8 → 3 → 6 → 7`.

Time: O(h), where `h` is tree height. Extra space: O(1) for this iterative version.

## 5. Insert

Move left or right according to the ordering rule until an empty child position is found. This implementation ignores duplicates.

```python
def insert(root, value):
    if root is None:
        return TreeNode(value)
    if value < root.value:
        root.left = insert(root.left, value)
    elif value > root.value:
        root.right = insert(root.right, value)
    return root

root = None
for value in [8, 3, 10, 1, 6, 14, 4, 7, 13]:
    root = insert(root, value)
```

Time: O(h). Recursive auxiliary space: O(h). Reassign the returned root: `root = insert(root, value)`.

## 6. Minimum and maximum

The minimum is the leftmost node; the maximum is the rightmost.

```python
def find_min(root):
    if root is None:
        return None
    current = root
    while current.left is not None:
        current = current.left
    return current.value


def find_max(root):
    if root is None:
        return None
    current = root
    while current.right is not None:
        current = current.right
    return current.value
```

For the example, minimum is `1` and maximum is `14`. Time: O(h), extra space: O(1).

## 7. Delete

Deletion has three cases:
1. **Leaf:** remove it.
2. **One child:** replace it with its child.
3. **Two children:** replace its value with its inorder successor (minimum in its right subtree), then delete that successor.

```python
def delete(root, value):
    if root is None:
        return None

    if value < root.value:
        root.left = delete(root.left, value)
    elif value > root.value:
        root.right = delete(root.right, value)
    else:
        if root.left is None:       # zero or one child
            return root.right
        if root.right is None:      # one child
            return root.left

        successor = root.right
        while successor.left is not None:
            successor = successor.left

        root.value = successor.value
        root.right = delete(root.right, successor.value)

    return root
```

Time: O(h). Recursive auxiliary space: O(h). Reassign the root: `root = delete(root, value)`.

The successor is the next larger value and preserves BST ordering when used to replace a node with two children.

## 8. Inorder traversal

Inorder means **Left → Root → Right**. For a BST with distinct values, this returns values in ascending order.

```python
def inorder_values(root):
    result = []

    def visit(node):
        if node is None:
            return
        visit(node.left)
        result.append(node.value)
        visit(node.right)

    visit(root)
    return result
```

Time: O(n). Recursive auxiliary space: O(h), excluding the returned result.

## 9. Validate a BST

Checking only a node's immediate children is insufficient. Every node must satisfy bounds inherited from all its ancestors.

```python
def is_valid_bst(root):
    def validate(node, low, high):
        if node is None:
            return True
        if not (low < node.value < high):
            return False
        return (
            validate(node.left, low, node.value)
            and validate(node.right, node.value, high)
        )

    return validate(root, float("-inf"), float("inf"))
```

This assumes distinct values and strict ordering. Time: O(n). Recursive auxiliary space: O(h).

## 10. Inorder successor and predecessor

- **Successor:** the next larger value.
- **Predecessor:** the next smaller value.
- If a node has a right subtree, its successor is the minimum in that subtree.
- If a node has a left subtree, its predecessor is the maximum in that subtree.
- If the relevant subtree is absent, the answer may require searching from the root or moving up using parent pointers.

These ideas are useful in deletion and ordered queries.

## 11. Balanced vs skewed BST

A balanced-ish tree has relatively small height. A skewed tree can look like a linked list:

```text
1
 \\
  2
   \\
    3
     \\
      4
       \\
        5
```

Let `n` be the number of nodes and `h` the height.

| Operation | Balanced tree (typical) | Worst case |
|---|---:|---:|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |
| Find minimum/maximum | O(log n) | O(n) |
| Validate BST | O(n) | O(n) |

A plain BST does not automatically rebalance. AVL and Red-Black trees maintain height bounds through additional rules.

## 12. Common mistakes
1. Checking only direct children instead of whole subtrees.
2. Forgetting to reassign the root after insert or delete.
3. Handling only leaf deletion, not one-child and two-child cases.
4. Using an incorrect replacement for a two-child deletion.
5. Assuming all BST operations are O(log n); skewed trees can take O(n).
6. Ignoring the duplicate-value policy.
7. Applying BST rules to an ordinary binary tree.

## 13. Practice problems

### Beginner
1. Build a BST from a list of distinct values.
2. Search for a value.
3. Find minimum and maximum.
4. Print values in ascending order with inorder traversal.
5. Count nodes in a BST.
6. Insert values and draw the resulting tree.

### Intermediate
7. Delete a leaf.
8. Delete a node with one child.
9. Delete a node with two children.
10. Validate whether a tree is a BST.
11. Find the inorder successor and predecessor.
12. Find the kth smallest value.
13. Find the kth largest value.
14. Find all values in a range `[low, high]`.
15. Find the lowest common ancestor of two values in a BST.
16. Convert a sorted array into a height-balanced BST.

### Challenge
17. Recover a BST where two values have been swapped.
18. Find the closest value to a target.
19. Build a BST from its preorder traversal.
20. Check whether one tree is a subtree of another.
21. Design an iterator that yields values in ascending order.
22. Explain how self-balancing BSTs improve worst-case operations.
