# Test 3 Study Guide

## Binary Search Trees and AVL Trees

This test covers sorting and searching efficiency, binary tree properties, binary search trees (BSTs), tree traversals, recursive methods, BST insertion and deletion, and AVL tree balancing.

**How to prepare:** Do more than memorize definitions. Practice drawing trees, tracing recursive calls, and explaining why a particular rotation is necessary.

## 1. Sorting and Searching Efficiency

### Big-O notation

Know the efficiency categories of these algorithms:

| Algorithm     | Typical efficiency          |
| ------------- | --------------------------- |
| Linear search | $O(n)$                      |
| Binary search | $O(\log_2 n)$               |
| Merge sort    | $O(n\log_2 n)$              |
| Quick sort    | $O(n\log_2 n)$ average case |

Be able to:

- Recognize which algorithms belong to the same efficiency category.
- Explain why binary search is faster than linear search for large, sorted lists.
- Explain why binary search requires sorted data, while linear search does not.

**Important:** Binary search repeatedly eliminates approximately half of the remaining search space. Linear search examines elements one at a time.

### Practice questions

1. What is the typical efficiency of merge sort?
2. What is the main requirement for using binary search?
3. If a list is not sorted, which searching algorithm can still be used without sorting the list first?

## 2. Binary Tree Fundamentals

Understand the basic terminology and properties of binary trees.

### Important terminology

- **Root:** The topmost node of a tree.
- **Parent:** A node that has one or more children.
- **Child:** A node directly below another node.
- **Leaf:** A node with no children.
- **Subtree:** A node and all its descendants.
- **Level:** The distance from the root, measured in edges. The root is at level 0.
- **Height:** The number of edges on the longest path from a node to a leaf.

### Full and complete binary trees

A **full binary tree** is a tree in which every node has either zero or two children.

A **complete binary tree** is a tree in which every level is completely filled except possibly the last, and the last level is filled from left to right.

For a full and complete binary tree:

- Level 0 has 1 node.
- Level 1 has 2 nodes.
- Level 2 has 4 nodes.
- Level 3 has 8 nodes.

In general, level $k$ has:

$$2^k$$

nodes when that level is completely filled.

### Practice

1. How many nodes are on level 5?
2. How many nodes are on level 7?
3. How many nodes are in a completely filled binary tree with levels 0 through 3?

## 3. Binary Search Trees (BSTs)

A binary search tree is a binary tree that maintains an ordering property.

For every node:

- All keys in its left subtree are smaller than the node's key.
- All keys in its right subtree are greater than the node's key.

Assume keys are unique unless otherwise specified.

### Inserting nodes into a BST

To insert a new key:

1. Start at the root.
2. Compare the new key with the current node.
3. If the new key is smaller, move left.
4. If the new key is greater, move right.
5. Continue until you reach an empty child position.
6. Insert the new node there.

**Important:** The order of insertion matters. Inserting the same keys in a different order can produce a different BST.

### Practice

Draw the BST produced by inserting these letters in order:

`M, C, P, X, N, D, O, B, R, Z`

Show every node in its correct position. Do not simply sort the letters and draw them from left to right.

### Searching a BST

To search for a key:

1. Start at the root.
2. Compare the target with the current node.
3. Move left if the target is smaller.
4. Move right if the target is greater.
5. Stop when the key is found or you reach an empty position.

For a reasonably balanced BST, searching takes $O(\log n)$ time.

For a badly unbalanced BST, searching can take $O(n)$ time.

**Remember:** A BST is not necessarily balanced. Its performance depends on its shape.

### Successors and predecessors

- A **successor** of a key is a key that comes after it in sorted (inorder) order.
- A **predecessor** is a key that comes before it in sorted (inorder) order.

For a node containing key $K$:

- Every key in its right subtree is greater than $K$.
- Every key in its left subtree is smaller than $K$.

Be careful when interpreting statements about all successors or predecessors versus those specifically in the left or right subtree.

## 4. Tree Traversals

You should be able to trace all three common depth-first traversal orders.

Remember the order in which each traversal visits the root, left subtree, and right subtree.

| Traversal | Order               |
| --------- | ------------------- |
| Preorder  | Root → Left → Right |
| Inorder   | Left → Root → Right |
| Postorder | Left → Right → Root |

### Memory tips

- **Preorder:** Visit the root first.
- **Inorder:** Visit the root in the middle.
- **Postorder:** Visit the root last.

**Important BST property:** An inorder traversal of a BST visits the keys in ascending order.

### Practice

For the following tree, write the preorder, inorder, and postorder sequences.

```
        M
       / \
      C   P
     / \   \
    A   D   R
       /   /
      B   Q
```

Trace each traversal recursively. Do not guess the sequence based on the appearance of the tree.

## 5. Removing Nodes from a BST

There are three cases to understand when removing a node.

### Case 1: Removing a leaf

A leaf has no children.

Simply remove the node by setting the appropriate parent reference to `null`.

### Case 2: Removing a node with one child

Replace the node with its only child.

The child takes the removed node's place in the tree.

### Case 3: Removing a node with two children

You cannot simply remove the node without preserving the BST ordering property.

A common approach is:

1. Find the node's inorder successor (the smallest node in its right subtree).
2. Copy the successor's key into the node being removed.
3. Remove the successor from its original position.

Alternatively, you can use the inorder predecessor (the largest node in the left subtree).

**Practice:** For each removal problem:

1. Identify which of the three cases applies.
2. Find the appropriate replacement, if necessary.
3. Redraw the entire tree.
4. Verify that the BST ordering property is still satisfied.

## 6. Recursion

You should be able to trace a recursive method and determine its return value.

Consider this method:

```
public static int mystery(int n) {
    if (n <= 1) {
        return 1;
    } else {
        int result = mystery(n - 1) + mystery(n - 2);
        return result;
    }
}
```

### How to trace recursive calls

1. Identify the base case. When does the method stop making recursive calls?
2. Expand each recursive call.
3. Work from the base cases upward.
4. Substitute the returned values into the expressions.
5. Determine the final result.

For example, start with:

```
mystery(3)
```

The calls expand as follows:

```
mystery(3)
    mystery(2) + mystery(1)
        mystery(1) + mystery(0)
```

Both `mystery(1)` and `mystery(0)` reach the base case.

**Practice:** Trace `mystery(4)` by hand. Write down each call and its return value.

## 7. AVL Trees

An AVL tree is a self-balancing binary search tree.

Like an ordinary BST, it maintains the ordering property. In addition, it keeps the heights of the left and right subtrees sufficiently close to prevent the tree from becoming excessively unbalanced.

### Balance factor

The balance factor measures the difference between the heights of a node's two subtrees.

$$BF(node)=height(right)-height(left)$$

Under this convention:

- `BF = 0`: Left and right subtrees have equal heights.
- `BF = +1`: The right subtree is one level taller.
- `BF = -1`: The left subtree is one level taller.
- `BF = +2`: The node is too right-heavy.
- `BF = -2`: The node is too left-heavy.

An AVL tree must maintain a balance factor of -1, 0, or +1 at every node.

### Four types of AVL rotations

You must recognize the four imbalance cases and know how to correct them.

**1. LL (Left-Left) case**

A node becomes too left-heavy because a new key was inserted into the left subtree of its left child.

Correction: Single right rotation.

**2. RR (Right-Right) case**

A node becomes too right-heavy because a new key was inserted into the right subtree of its right child.

Correction: Single left rotation.

**3. LR (Left-Right) case**

A node becomes too left-heavy because a new key was inserted into the right subtree of its left child.

Correction:

1. Left rotation on the left child.
2. Right rotation on the unbalanced node.

**4. RL (Right-Left) case**

A node becomes too right-heavy because a new key was inserted into the left subtree of its right child.

Correction:

1. Right rotation on the right child.
2. Left rotation on the unbalanced node.

### Rotation summary

| Imbalance | Correction                         |
| --------- | ---------------------------------- |
| LL        | Single right rotation              |
| RR        | Single left rotation               |
| LR        | Left rotation, then right rotation |
| RL        | Right rotation, then left rotation |

### How to solve an AVL insertion problem

Follow these steps every time you insert a key:

1. Insert the key using the ordinary BST insertion rules.
2. Move upward from the inserted node toward the root.
3. Update the height of each affected node.
4. Calculate the balance factor of each affected node.
5. Find the first unbalanced node.
6. Identify the LL, RR, LR, or RL case.
7. Perform the required rotation(s).
8. Update the heights and balance factors.
9. Draw the resulting tree.

**Important:** A rotation changes the structure of the tree, but it must preserve the BST ordering property.

### Practice: AVL insertion

Practice inserting the following keys in exactly this order:

"M, F, T, D, J, H"

After every insertion:

- Draw the entire tree.
- Label every node with its balance factor.
- Identify any unbalanced node.
- Name the rotation case, if one is needed.
- Show the rotation and explain why it is necessary.
- Draw the resulting tree after rebalancing.

Do not skip intermediate trees. The purpose is to demonstrate that you understand how an AVL tree changes after each insertion.
