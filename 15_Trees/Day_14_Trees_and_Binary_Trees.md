# Day 14 — Trees and Binary Trees

## 1. Learning goals
- Understand root, parent, child, leaf, depth, and height.
- Represent a binary tree in Python.
- Perform preorder, inorder, postorder, and level-order traversal.
- Count nodes, calculate height, search, and count leaves.
- Analyze tree algorithms by node count and tree height.

## 2. What is a tree?

A **tree** is a hierarchical data structure made of nodes connected by edges.

```text
          A
        /   \
       B     C
      / \     \
     D   E     F
```

- **Root:** `A`, the top node.
- **Parent:** `B` is the parent of `D` and `E`.
- **Child:** `D` is a child of `B`.
- **Siblings:** `B` and `C` share a parent.
- **Leaf:** `D`, `E`, and `F` have no children.
- **Edge:** a connection between two nodes.
- **Depth:** number of edges from the root to a node. Root depth is `0`.
- **Height of a node:** number of edges on its longest downward path to a leaf. A leaf has height `0`.
- **Height of a tree:** height of its root.

A non-empty tree with `n` nodes has `n - 1` edges.

## 3. What is a binary tree?

A **binary tree** is a tree in which each node has at most two children: a left child and a right child. A node may have zero, one, or two children.

A binary tree is not necessarily a **Binary Search Tree (BST)**. A general binary tree has no required value ordering; a BST adds an ordering rule, which we will study later.

Common shapes:
- **Full:** every node has zero or two children.
- **Complete:** all levels are full except possibly the last, which fills from left to right.
- **Perfect:** every internal node has two children and all leaves are at the same depth.
- **Skewed:** each node has at most one child, forming a chain.

## 4. Representing a tree in Python

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

root = TreeNode("A")
root.left = TreeNode("B")
root.right = TreeNode("C")
root.left.left = TreeNode("D")
root.left.right = TreeNode("E")
root.right.right = TreeNode("F")
```

This creates the tree shown earlier. `None` means a child does not exist.

## 5. Tree traversal

**Traversal** means visiting every node in a defined order.

### A. Preorder: Root → Left → Right

```python
def preorder(node):
    if node is None:
        return
    print(node.value)
    preorder(node.left)
    preorder(node.right)
```

Output for the example tree: `A B D E C F`.

### B. Inorder: Left → Root → Right

```python
def inorder(node):
    if node is None:
        return
    inorder(node.left)
    print(node.value)
    inorder(node.right)
```

Output: `D B E A C F`.

Inorder traversal of a BST visits values in sorted order if the BST follows the usual ordering rule.

### C. Postorder: Left → Right → Root

```python
def postorder(node):
    if node is None:
        return
    postorder(node.left)
    postorder(node.right)
    print(node.value)
```

Output: `D E B F C A`.

Memory trick:
- **Preorder:** root first.
- **Inorder:** root between left and right.
- **Postorder:** root last.

## 6. Level-order traversal (BFS)

Level order visits nodes level by level, from left to right. It uses a queue.

```python
from collections import deque

def level_order(root):
    if root is None:
        return []

    result = []
    queue = deque([root])

    while queue:
        node = queue.popleft()
        result.append(node.value)

        if node.left is not None:
            queue.append(node.left)
        if node.right is not None:
            queue.append(node.right)

    return result

print(level_order(root))  # ['A', 'B', 'C', 'D', 'E', 'F']
```

Time: O(n). Extra space: O(w), where `w` is the maximum number of nodes at any level; worst case O(n).

## 7. Count nodes

Count the root plus the nodes in its left and right subtrees.

```python
def count_nodes(node):
    if node is None:
        return 0
    return 1 + count_nodes(node.left) + count_nodes(node.right)
```

For the example tree, the answer is `6`. Time: O(n). Recursive auxiliary space: O(h), where `h` is tree height.

## 8. Find the height

Here, height is measured in **edges**: an empty tree has height `-1`, and a leaf has height `0`.

```python
def height(node):
    if node is None:
        return -1
    return 1 + max(height(node.left), height(node.right))
```

The example tree has height `2`. Some courses count nodes instead of edges, so always use the definition specified in the question.

Time: O(n). Recursive auxiliary space: O(h).

## 9. Search for a value

A general binary tree has no ordering rule, so you may need to inspect every node.

```python
def contains(node, target):
    if node is None:
        return False
    if node.value == target:
        return True
    return contains(node.left, target) or contains(node.right, target)

print(contains(root, "E"))  # True
print(contains(root, "Z"))  # False
```

Worst-case time: O(n). Recursive auxiliary space: O(h).

## 10. Find the maximum value

This version assumes all node values are numeric.

```python
def tree_max(node):
    if node is None:
        raise ValueError("tree is empty")

    best = node.value
    if node.left is not None:
        best = max(best, tree_max(node.left))
    if node.right is not None:
        best = max(best, tree_max(node.right))
    return best
```

Time: O(n). Recursive auxiliary space: O(h). A general binary tree does not guarantee that the maximum is at the root or on the right.

## 11. Count leaf nodes

A leaf has no left or right child.

```python
def count_leaves(node):
    if node is None:
        return 0
    if node.left is None and node.right is None:
        return 1
    return count_leaves(node.left) + count_leaves(node.right)
```

Time: O(n). Recursive auxiliary space: O(h).

## 12. Iterative preorder traversal

Recursive DFS is clear, but very deep trees can exceed Python's recursion limit. An explicit stack avoids recursive calls.

```python
def preorder_iterative(root):
    if root is None:
        return []

    result = []
    stack = [root]

    while stack:
        node = stack.pop()
        result.append(node.value)

        # Push right first so left is processed first.
        if node.right is not None:
            stack.append(node.right)
        if node.left is not None:
            stack.append(node.left)

    return result
```

Time: O(n). Extra space: O(h) to O(n), depending on the tree shape.

## 13. Complexity summary

Let `n` be the number of nodes, `h` the tree height, and `w` the maximum width.

| Operation | Time | Extra/recursive space |
|---|---:|---:|
| Preorder traversal | O(n) | O(h) |
| Inorder traversal | O(n) | O(h) |
| Postorder traversal | O(n) | O(h) |
| Level-order traversal | O(n) | O(w), at most O(n) |
| Count nodes | O(n) | O(h) |
| Calculate height | O(n) | O(h) |
| Search general binary tree | O(n) | O(h) |
| Count leaves | O(n) | O(h) |

A balanced tree has height around O(log n), while a skewed tree can have height O(n).

## 14. Common mistakes

1. Confusing a binary tree with a BST: a binary tree is not automatically sorted.
2. Mixing traversal orders: remember where the root is visited.
3. Forgetting the `None` base case.
4. Enqueuing a child more than once during level-order traversal.
5. Assuming every tree has logarithmic height.
6. Mixing height definitions: check whether height counts edges or nodes.
7. Using a stack for level order: level order requires a queue; DFS commonly uses a stack or recursion.

## 15. Practice problems

### Beginner
1. Create a binary tree with at least seven nodes.
2. Write preorder traversal.
3. Write inorder traversal.
4. Write postorder traversal.
5. Write level-order traversal.
6. Count all nodes.
7. Count leaf nodes.
8. Find the tree height.
9. Search for a target value.
10. Find the maximum value in a numeric binary tree.

### Intermediate
11. Find the sum of all node values.
12. Count nodes with exactly one child.
13. Find the maximum number of nodes at any level.
14. Return each level as a list of values.
15. Check whether two binary trees are identical.
16. Mirror a binary tree by swapping left and right children.
17. Find the sum of values at each level.
18. Implement iterative preorder traversal.
19. Implement iterative inorder traversal.
20. Find the minimum depth from root to a leaf.

### Challenge
21. Check whether a binary tree is height-balanced.
22. Find the diameter of a binary tree.
23. Find the lowest common ancestor in a general binary tree when both targets exist.
24. Print the left view of a binary tree.
25. Perform zigzag level-order traversal.

## 16. Quick self-check
- What is the difference between a binary tree and a BST?
- What are the orders for preorder, inorder, and postorder?
- Why does level-order traversal use a queue?
- Why can recursion use O(n) stack space in a skewed tree?
- What is a leaf's height under the edge-counting convention used here?

**Day 14 checkpoint:** create a tree, implement all four traversals, count nodes, calculate height, and search for a value. Then solve at least five practice problems.
