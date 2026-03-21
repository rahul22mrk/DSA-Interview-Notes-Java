# Tree Traversal — Complete Reference

> **One place for all tree traversal patterns before your interview**
> **Language:** Java | **Covers:** DFS (Iterative + Recursive) | BFS | Views | Boundary

---

## Table of Contents

1. [DFS — Iterative Traversal](#1-dfs--iterative-traversal)
2. [DFS — Recursive Traversal](#2-dfs--recursive-traversal)
3. [BFS — Level Order Traversal](#3-bfs--level-order-traversal)
4. [Depth Problems](#4-depth-problems)
5. [Tree Comparison](#5-tree-comparison)
6. [Side Views of Binary Tree](#6-side-views-of-binary-tree)
7. [Boundary Traversal](#7-boundary-traversal)
8. [Quick Comparison Table](#8-quick-comparison-table)

---

## 1. DFS — Iterative Traversal

> Use explicit stack instead of recursion — avoids stack overflow for large trees.

---

### Inorder Iterative (Left → Root → Right)

```java
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<>();
    Deque<TreeNode> stack = new ArrayDeque<>();

    while (!stack.isEmpty() || root != null) {
        while (root != null) {
            stack.push(root);
            root = root.left;        // go as far left as possible
        }
        root = stack.pop();
        list.add(root.val);          // visit
        root = root.right;           // move right
    }
    return list;
}
```

```
Tree:     1
           \
            2
           /
          3
Output: [1, 3, 2]
```

---

### Preorder Iterative (Root → Left → Right)

```java
public List<Integer> preorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<>();
    if (root == null) return list;
    Deque<TreeNode> stack = new ArrayDeque<>();
    stack.push(root);

    while (!stack.isEmpty()) {
        root = stack.pop();
        list.add(root.val);              // visit root first
        if (root.right != null) stack.push(root.right);  // right pushed first (LIFO)
        if (root.left  != null) stack.push(root.left);   // left processed first
    }
    return list;
}
```

```
Tree:   1
       / \
      2   3
Output: [1, 2, 3]
```

---

### Postorder Iterative — Method 1 (True Postorder)

```java
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<>();
    Deque<TreeNode> stack = new ArrayDeque<>();

    while (!stack.isEmpty() || root != null) {
        if (root != null) {
            stack.push(root);
            root = root.left;
        } else {
            TreeNode temp = stack.peek().right;
            if (temp == null) {
                temp = stack.pop();
                list.add(temp.val);
                while (!stack.isEmpty() && temp == stack.peek().right) {
                    temp = stack.pop();
                    list.add(temp.val);
                }
            } else {
                root = temp;
            }
        }
    }
    return list;
}
```

### Postorder Iterative — Method 2 (Reverse Preorder — Simpler ✅)

> Reverse the steps of preorder (push left before right), then reverse the result.

```java
public List<Integer> postorderTraversal(TreeNode root) {
    LinkedList<Integer> list = new LinkedList<>();
    if (root == null) return list;
    Deque<TreeNode> stack = new ArrayDeque<>();
    stack.push(root);

    while (!stack.isEmpty()) {
        root = stack.pop();
        list.addFirst(root.val);         // prepend instead of append
        if (root.left  != null) stack.push(root.left);   // left first (reversed)
        if (root.right != null) stack.push(root.right);
    }
    return list;
}
```

```
Tree:   1
       / \
      2   3
Output: [2, 3, 1]
```

> **Trick to remember Method 2:**
> Preorder = Root→Left→Right. Reverse pushes: Root→Right→Left. Reverse result: Left→Right→Root = Postorder ✓

---

## 2. DFS — Recursive Traversal

> Clean and concise — move `list.add(root.val)` to change order.

---

### The 3 Recursive Templates — Only ONE Line Changes

```java
// INORDER: Left → Root → Right
void inorder(TreeNode root, List<Integer> list) {
    if (root == null) return;
    inorder(root.left, list);
    list.add(root.val);        // ← ROOT visited MIDDLE
    inorder(root.right, list);
}

// PREORDER: Root → Left → Right
void preorder(TreeNode root, List<Integer> list) {
    if (root == null) return;
    list.add(root.val);        // ← ROOT visited FIRST
    preorder(root.left, list);
    preorder(root.right, list);
}

// POSTORDER: Left → Right → Root
void postorder(TreeNode root, List<Integer> list) {
    if (root == null) return;
    postorder(root.left, list);
    postorder(root.right, list);
    list.add(root.val);        // ← ROOT visited LAST
}
```

```
       4
      / \
     2   5
    / \
   1   3

Inorder:   [1, 2, 3, 4, 5]  ← BST gives sorted order
Preorder:  [4, 2, 1, 3, 5]  ← root first (used for construction)
Postorder: [1, 3, 2, 5, 4]  ← children before root (used for deletion/height)
```

---

## 3. BFS — Level Order Traversal

---

### Level Order — Flat (all nodes in one list)

```java
public List<Integer> levelOrder(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if (root == null) return result;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);

    while (!q.isEmpty()) {
        root = q.poll();
        result.add(root.val);
        if (root.left  != null) q.offer(root.left);
        if (root.right != null) q.offer(root.right);
    }
    return result;
}
```

---

### Level Order — Level by Level ✅ (most useful)
**LeetCode #102**

> Key: snapshot `size = q.size()` BEFORE inner loop to separate levels.

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);

    while (!q.isEmpty()) {
        int size = q.size();                  // ← snapshot size = current level count
        List<Integer> level = new ArrayList<>();
        while (size-- > 0) {
            root = q.poll();
            level.add(root.val);
            if (root.left  != null) q.offer(root.left);
            if (root.right != null) q.offer(root.right);
        }
        result.add(level);
    }
    return result;
}
```

```
       3
      / \
     9  20
       /  \
      15   7

Output: [[3], [9,20], [15,7]]
```

---

### Zigzag Level Order
**LeetCode #103**

> Same as level by level, add `Collections.reverse(level)` for odd levels.

```java
public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    boolean isOddLevel = false;

    while (!q.isEmpty()) {
        int size = q.size();
        List<Integer> level = new ArrayList<>();
        while (size-- > 0) {
            root = q.poll();
            level.add(root.val);
            if (root.left  != null) q.offer(root.left);
            if (root.right != null) q.offer(root.right);
        }
        if (isOddLevel) Collections.reverse(level);  // ← only this line added
        result.add(level);
        isOddLevel = !isOddLevel;
    }
    return result;
}
```

```
       3
      / \
     9  20
       /  \
      15   7

Output: [[3], [20,9], [15,7]]
         L→R  R→L     L→R
```

---

## 4. Depth Problems

---

### Minimum Depth
**LeetCode #111**

> Important: a node with one null child is NOT a leaf — don't return 0 for that side.

```java
public int minDepth(TreeNode root) {
    if (root == null) return 0;
    if (root.left  == null) return 1 + minDepth(root.right);  // can't go left
    if (root.right == null) return 1 + minDepth(root.left);   // can't go right
    return 1 + Math.min(minDepth(root.left), minDepth(root.right));
}
```

```
     1
    /
   2
minDepth = 2  (not 1 — node 1 is NOT a leaf because it has a left child)
```

---

### Maximum Depth
**LeetCode #104**

```java
public int maxDepth(TreeNode root) {
    if (root == null) return 0;
    return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
```

---

### Balanced Binary Tree
**LeetCode #110**

```java
// O(N²) — naive
public boolean isBalanced(TreeNode root) {
    if (root == null) return true;
    int lh = height(root.left), rh = height(root.right);
    return Math.abs(lh - rh) <= 1 && isBalanced(root.left) && isBalanced(root.right);
}
private int height(TreeNode node) {
    if (node == null) return 0;
    return Math.max(height(node.left), height(node.right)) + 1;
}

// O(N) — optimal: return -1 as "unbalanced" signal
public boolean isBalancedOptimal(TreeNode root) {
    return height(root) != -1;
}
private int heightOptimal(TreeNode node) {
    if (node == null) return 0;
    int left  = heightOptimal(node.left);
    int right = heightOptimal(node.right);
    if (left == -1 || right == -1 || Math.abs(left - right) > 1) return -1;
    return Math.max(left, right) + 1;
}
```

---

## 5. Tree Comparison

---

### Same Tree
**LeetCode #100**

```java
public boolean isSameTree(TreeNode p, TreeNode q) {
    if (p == null && q == null) return true;
    if (p == null || q == null) return false;
    return p.val == q.val
        && isSameTree(p.left,  q.left)
        && isSameTree(p.right, q.right);
}
```

---

### Symmetric Tree
**LeetCode #101**

> Compare OUTER pair (left.left vs right.right) and INNER pair (left.right vs right.left).

```java
public boolean isSymmetric(TreeNode root) {
    if (root == null) return true;
    return isMirror(root.left, root.right);
}

private boolean isMirror(TreeNode p, TreeNode q) {
    if (p == null && q == null) return true;
    if (p == null || q == null) return false;
    return p.val == q.val
        && isMirror(p.left,  q.right)   // outer pair
        && isMirror(p.right, q.left);   // inner pair
}
```

---

## 6. Side Views of Binary Tree

---

### Left Side View

**BFS approach** — first node of each level:

```java
public List<Integer> leftSideView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if (root == null) return result;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);

    while (!q.isEmpty()) {
        int size = q.size();
        result.add(q.peek().val);        // ← peek = leftmost of this level
        while (size-- > 0) {
            root = q.poll();
            if (root.left  != null) q.offer(root.left);
            if (root.right != null) q.offer(root.right);
        }
    }
    return result;
}
```

**DFS approach** — first visit at each level:

```java
public List<Integer> leftSideViewDFS(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    dfs(root, result, 0);
    return result;
}
private void dfs(TreeNode node, List<Integer> result, int level) {
    if (node == null) return;
    if (result.size() == level) result.add(node.val);  // first visit at this level
    dfs(node.left,  result, level + 1);   // left first for left view
    dfs(node.right, result, level + 1);
}
```

---

### Right Side View
**LeetCode #199**

**BFS approach** — last node of each level:

```java
public List<Integer> rightSideView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if (root == null) return result;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);

    while (!q.isEmpty()) {
        int size = q.size();
        result.add(q.peek().val);         // ← peek = rightmost (right added first below)
        while (size-- > 0) {
            root = q.poll();
            if (root.right != null) q.offer(root.right);  // right first!
            if (root.left  != null) q.offer(root.left);
        }
    }
    return result;
}
```

**DFS approach** — right subtree first:

```java
public List<Integer> rightSideViewDFS(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    dfs(root, result, 0);
    return result;
}
private void dfs(TreeNode node, List<Integer> result, int level) {
    if (node == null) return;
    if (result.size() == level) result.add(node.val);
    dfs(node.right, result, level + 1);   // right first for right view
    dfs(node.left,  result, level + 1);
}
```

---

### Bottom View
**GFG | Uses horizontal distance (HD)**

> BFS + TreeMap. For each node, track HD: root=0, left child=HD-1, right child=HD+1.
> Last node at each HD (overwrite) = bottom view.

```java
class TreeNodeWithHD {
    TreeNode node; int hd;
    TreeNodeWithHD(TreeNode node, int hd) { this.node = node; this.hd = hd; }
}

public List<Integer> bottomView(TreeNode root) {
    if (root == null) return new ArrayList<>();
    TreeMap<Integer, Integer> map = new TreeMap<>();  // HD → value (sorted by HD)
    Queue<TreeNodeWithHD> q = new LinkedList<>();
    q.offer(new TreeNodeWithHD(root, 0));

    while (!q.isEmpty()) {
        TreeNodeWithHD curr = q.poll();
        map.put(curr.hd, curr.node.val);              // overwrite → last = bottom
        if (curr.node.left  != null) q.offer(new TreeNodeWithHD(curr.node.left,  curr.hd - 1));
        if (curr.node.right != null) q.offer(new TreeNodeWithHD(curr.node.right, curr.hd + 1));
    }
    return new ArrayList<>(map.values());
}
```

```
          20
         /  \
        8   22
       / \
      5  3
        / \
       10  14

HD:  -2  -1   0   1   2
      5   8  10  14  22
Bottom View: [5, 8, 10, 14, 22]
```

---

### Top View
**GFG | Same as Bottom View — only store FIRST occurrence at each HD**

**BFS approach:**

```java
public List<Integer> topView(TreeNode root) {
    if (root == null) return new ArrayList<>();
    TreeMap<Integer, Integer> map = new TreeMap<>();
    Queue<TreeNodeWithHD> q = new LinkedList<>();
    q.offer(new TreeNodeWithHD(root, 0));

    while (!q.isEmpty()) {
        TreeNodeWithHD curr = q.poll();
        if (!map.containsKey(curr.hd))               // ← only first occurrence (top)
            map.put(curr.hd, curr.node.val);
        if (curr.node.left  != null) q.offer(new TreeNodeWithHD(curr.node.left,  curr.hd - 1));
        if (curr.node.right != null) q.offer(new TreeNodeWithHD(curr.node.right, curr.hd + 1));
    }
    return new ArrayList<>(map.values());
}
```

**DFS approach** — track level to pick topmost:

```java
public List<Integer> topViewDFS(TreeNode root) {
    TreeMap<Integer, int[]> map = new TreeMap<>();  // HD → [val, level]
    dfs(root, 0, 0, map);
    List<Integer> result = new ArrayList<>();
    for (int[] v : map.values()) result.add(v[0]);
    return result;
}
private void dfs(TreeNode node, int hd, int level, TreeMap<Integer, int[]> map) {
    if (node == null) return;
    if (!map.containsKey(hd) || level < map.get(hd)[1])  // keep topmost (smallest level)
        map.put(hd, new int[]{node.val, level});
    dfs(node.left,  hd - 1, level + 1, map);
    dfs(node.right, hd + 1, level + 1, map);
}
```

> **Bottom vs Top View — only one line different:**
> - Bottom: `map.put(hd, val)` — always overwrite → last (bottom) wins
> - Top:    `if (!map.containsKey(hd)) map.put(hd, val)` — first wins

---

## 7. Boundary Traversal

**LeetCode #545 | Anticlockwise: Root → Left boundary → Leaf nodes → Right boundary (reverse)**

```java
public List<Integer> boundaryOfBinaryTree(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if (root == null) return result;

    result.add(root.val);           // root (not a leaf)
    leftBoundary(root.left,  result);
    leafNodes(root.left,   result);
    leafNodes(root.right,  result);
    rightBoundary(root.right, result);
    return result;
}

// Left boundary: top-down, excluding leaf
private void leftBoundary(TreeNode node, List<Integer> result) {
    if (node == null) return;
    if (node.left != null) {
        result.add(node.val);
        leftBoundary(node.left, result);
    } else if (node.right != null) {
        result.add(node.val);
        leftBoundary(node.right, result);
    }
    // if leaf: skip (handled by leafNodes)
}

// All leaf nodes: left to right
private void leafNodes(TreeNode node, List<Integer> result) {
    if (node == null) return;
    leafNodes(node.left, result);
    if (node.left == null && node.right == null) result.add(node.val);
    leafNodes(node.right, result);
}

// Right boundary: bottom-up (add AFTER recursion), excluding leaf
private void rightBoundary(TreeNode node, List<Integer> result) {
    if (node == null) return;
    if (node.right != null) {
        rightBoundary(node.right, result);
        result.add(node.val);           // add after recursion → bottom-up
    } else if (node.left != null) {
        rightBoundary(node.left, result);
        result.add(node.val);
    }
    // if leaf: skip
}
```

```
           1
          / \
         2   3
        / \ / \
       4  5 6  7
          |
         8 9

Boundary (anticlockwise):
  Root:          [1]
  Left boundary: [2]      (4 is leaf, 5 is leaf → skip)
  Leaves L→R:    [4,8,9,6,7]
  Right boundary:[3]      (reverse bottom-up)
Output: [1, 2, 4, 8, 9, 6, 7, 3]
```

---

## 8. Quick Comparison Table

### DFS — When to use which order?

| Order | Visit sequence | Use case |
|-------|---------------|----------|
| **Inorder** | Left → Root → Right | BST sorted order, Kth smallest, Validate BST |
| **Preorder** | Root → Left → Right | Tree construction, serialization, copy tree |
| **Postorder** | Left → Right → Root | Delete tree, height/depth, Max path sum, evaluate expression tree |

### Iterative vs Recursive — when to choose?

| Approach | Pros | Cons | Use when |
|----------|------|------|----------|
| **Recursive** | Clean, easy to write | Stack overflow on large trees | Interview (clean code) |
| **Iterative** | No overflow, O(h) explicit stack | More complex code | Follow-up: "without recursion" |

### BFS Patterns — One template, many problems

| Problem | Modification |
|---------|-------------|
| Level Order | snapshot `size = q.size()` |
| Zigzag | + `Collections.reverse(level)` on odd levels |
| Level Order II (bottom-up) | `result.addFirst(level)` with LinkedList |
| Right Side View | first node of each level (right child pushed first) |
| Left Side View | first node of each level (left child pushed first) |
| Average of Levels | sum / size instead of list |
| Max Width | track indices `2*i` and `2*i+1` |

### Views — Key Differences

| View | What you take | Direction |
|------|--------------|-----------|
| **Left Side** | First node at each level | Add left child first to queue |
| **Right Side** | First node at each level | Add right child first to queue |
| **Top View** | First node at each horizontal distance | BFS + TreeMap + if (!contains) |
| **Bottom View** | Last node at each horizontal distance | BFS + TreeMap + always overwrite |
| **Boundary** | Left edge + leaves + right edge (reverse) | Three separate DFS passes |

---

*Use this file as a 10-minute revision before any tree interview.*
*The BFS template (snapshot size) + 3 recursive DFS templates cover 80% of tree traversal questions.*
