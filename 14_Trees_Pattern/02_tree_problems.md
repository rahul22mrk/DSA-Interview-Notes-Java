# Tree Pattern — Solved Problems (54 Problems)

> **Pattern family:** Binary Tree / BST / Tree Traversal / Construction
> **Notes & Templates:** [01_tree_notes.md](./01_tree_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Traversal
- [P1 — Binary Tree Inorder Traversal](#problem-1--binary-tree-inorder-traversal)
- [P2 — Binary Tree Preorder Traversal](#problem-2--binary-tree-preorder-traversal)
- [P3 — Binary Tree Postorder Traversal](#problem-3--binary-tree-postorder-traversal)
- [P4 — Binary Tree Level Order Traversal](#problem-4--binary-tree-level-order-traversal)
- [P5 — Binary Tree Zigzag Level Order Traversal](#problem-5--binary-tree-zigzag-level-order-traversal)
- [P6 — Binary Tree Level Order Traversal II](#problem-6--binary-tree-level-order-traversal-ii)

### Category 2 — Mirror & Symmetry
- [P7 — Invert Binary Tree](#problem-7--invert-binary-tree)
- [P8 — Symmetric Tree](#problem-8--symmetric-tree)
- [P9 — Same Tree](#problem-9--same-tree)
- [P10 — Subtree of Another Tree](#problem-10--subtree-of-another-tree)
- [P11 — Flip Equivalent Binary Trees](#problem-11--flip-equivalent-binary-trees)

### Category 3 — Traversal & Search (BST)
- [P12 — Search in a Binary Search Tree](#problem-12--search-in-a-binary-search-tree)
- [P13 — Lowest Common Ancestor of BST](#problem-13--lowest-common-ancestor-of-bst)
- [P14 — Lowest Common Ancestor of Binary Tree](#problem-14--lowest-common-ancestor-of-binary-tree)
- [P15 — Lowest Common Ancestor of Deepest Leaves](#problem-15--lowest-common-ancestor-of-deepest-leaves)
- [P16 — Find Mode in BST](#problem-16--find-mode-in-bst)
- [P17 — Two Sum IV — BST](#problem-17--two-sum-iv--bst)
- [P18 — Kth Smallest Element in BST](#problem-18--kth-smallest-element-in-bst)

### Category 4 — Validation & Properties
- [P19 — Minimum Depth of Binary Tree](#problem-19--minimum-depth-of-binary-tree)
- [P20 — Maximum Depth of Binary Tree](#problem-20--maximum-depth-of-binary-tree)
- [P21 — Balanced Binary Tree](#problem-21--balanced-binary-tree)
- [P22 — Diameter of Binary Tree](#problem-22--diameter-of-binary-tree)
- [P23 — Binary Tree Tilt](#problem-23--binary-tree-tilt)
- [P24 — Check Completeness of Binary Tree](#problem-24--check-completeness-of-binary-tree)
- [P25 — Validate Binary Search Tree](#problem-25--validate-binary-search-tree)
- [P26 — Recover Binary Search Tree](#problem-26--recover-binary-search-tree)

### Category 5 — Path Sum & Root to Leaf
- [P27 — Path Sum](#problem-27--path-sum)
- [P28 — Path Sum II](#problem-28--path-sum-ii)
- [P29 — Path Sum III](#problem-29--path-sum-iii)
- [P30 — Sum Root to Leaf Numbers](#problem-30--sum-root-to-leaf-numbers)
- [P31 — Binary Tree Maximum Path Sum](#problem-31--binary-tree-maximum-path-sum)

### Category 6 — Construction
- [P32 — Construct BT from Preorder and Inorder](#problem-32--construct-bt-from-preorder-and-inorder)
- [P33 — Construct BT from Inorder and Postorder](#problem-33--construct-bt-from-inorder-and-postorder)
- [P34 — Construct BT from Preorder and Postorder](#problem-34--construct-bt-from-preorder-and-postorder)
- [P35 — Convert Sorted Array to BST](#problem-35--convert-sorted-array-to-bst)
- [P36 — Convert Sorted List to BST](#problem-36--convert-sorted-list-to-bst)
- [P37 — Serialize and Deserialize Binary Tree](#problem-37--serialize-and-deserialize-binary-tree)

### Category 1 (Extended) — Level Order BFS
- [P38 — Even Odd Tree](#problem-38--even-odd-tree)
- [P39 — Reverse Odd Levels of Binary Tree](#problem-39--reverse-odd-levels-of-binary-tree)
- [P40 — Deepest Leaves Sum](#problem-40--deepest-leaves-sum)
- [P41 — Add One Row to Tree](#problem-41--add-one-row-to-tree)
- [P42 — Maximum Width of Binary Tree](#problem-42--maximum-width-of-binary-tree)
- [P43 — All Nodes Distance K in Binary Tree](#problem-43--all-nodes-distance-k-in-binary-tree)

### Category 6 (Extended) — Construction
- [P44 — Maximum Binary Tree](#problem-44--maximum-binary-tree)
- [P45 — Construct BST from Preorder Traversal](#problem-45--construct-bst-from-preorder-traversal)

### Category 5 (Extended) — Root to Leaf Paths
- [P46 — Binary Tree Paths](#problem-46--binary-tree-paths)
- [P47 — Smallest String Starting from Leaf](#problem-47--smallest-string-starting-from-leaf)
- [P48 — Insufficient Nodes in Root to Leaf Paths](#problem-48--insufficient-nodes-in-root-to-leaf-paths)
- [P49 — Pseudo-Palindromic Paths in a Binary Tree](#problem-49--pseudo-palindromic-paths-in-a-binary-tree)

### Category 3 (Extended) — Ancestor Problems
- [P50 — Maximum Difference Between Node and Ancestor](#problem-50--maximum-difference-between-node-and-ancestor)
- [P51 — Kth Ancestor of a Tree Node](#problem-51--kth-ancestor-of-a-tree-node)

### Category 3 (BST Extended)
- [P52 — Range Sum of BST](#problem-52--range-sum-of-bst)
- [P53 — Minimum Absolute Difference in BST](#problem-53--minimum-absolute-difference-in-bst)
- [P54 — Insert into a BST](#problem-54--insert-into-a-bst)

---

## Category 1 — Traversal

---

### Problem 1 — Binary Tree Inorder Traversal
**LeetCode #94 | Difficulty: Easy | Company: Amazon, Microsoft | Category: Traversal**

> Return inorder traversal (Left → Root → Right) of a binary tree.

#### Approach table

| Variant | Key idea |
|---------|----------|
| Recursive | call left, visit root, call right |
| Iterative | push left until null, pop + visit, go right |

#### Java code

```java
// Recursive
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    inorder(root, res);
    return res;
}
private void inorder(TreeNode node, List<Integer> res) {
    if (node == null) return;
    inorder(node.left, res);
    res.add(node.val);
    inorder(node.right, res);
}

// Iterative (preferred in interviews)
public List<Integer> inorderIterative(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    Deque<TreeNode> stack = new ArrayDeque<>();
    TreeNode curr = root;
    while (curr != null || !stack.isEmpty()) {
        while (curr != null) { stack.push(curr); curr = curr.left; }
        curr = stack.pop();
        res.add(curr.val);
        curr = curr.right;
    }
    return res;
}
```

#### Example

```
    1
     \
      2
     /
    3
Inorder: [1, 3, 2] ✓
```

---

### Problem 2 — Binary Tree Preorder Traversal
**LeetCode #144 | Difficulty: Easy | Company: Amazon | Category: Traversal**

> Return preorder traversal (Root → Left → Right).

#### Java code

```java
// Recursive
public List<Integer> preorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    preorder(root, res);
    return res;
}
private void preorder(TreeNode node, List<Integer> res) {
    if (node == null) return;
    res.add(node.val);         // visit root first
    preorder(node.left, res);
    preorder(node.right, res);
}

// Iterative
public List<Integer> preorderIterative(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    if (root == null) return res;
    Deque<TreeNode> stack = new ArrayDeque<>();
    stack.push(root);
    while (!stack.isEmpty()) {
        TreeNode node = stack.pop();
        res.add(node.val);
        if (node.right != null) stack.push(node.right);  // right first (LIFO)
        if (node.left  != null) stack.push(node.left);
    }
    return res;
}
```

---

### Problem 3 — Binary Tree Postorder Traversal
**LeetCode #145 | Difficulty: Easy | Company: Amazon | Category: Traversal**

> Return postorder traversal (Left → Right → Root).

#### Java code

```java
// Recursive
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    postorder(root, res);
    return res;
}
private void postorder(TreeNode node, List<Integer> res) {
    if (node == null) return;
    postorder(node.left, res);
    postorder(node.right, res);
    res.add(node.val);         // visit root last
}

// Iterative (reverse of modified preorder)
public List<Integer> postorderIterative(TreeNode root) {
    LinkedList<Integer> res = new LinkedList<>();
    if (root == null) return res;
    Deque<TreeNode> stack = new ArrayDeque<>();
    stack.push(root);
    while (!stack.isEmpty()) {
        TreeNode node = stack.pop();
        res.addFirst(node.val);     // add to front (reverse at end)
        if (node.left  != null) stack.push(node.left);
        if (node.right != null) stack.push(node.right);
    }
    return res;
}
```

---

### Problem 4 — Binary Tree Level Order Traversal
**LeetCode #102 | Difficulty: Medium | Company: Amazon, Facebook, Google | Category: BFS**

> Return nodes level by level (BFS).

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Init | `q.offer(root)` | start with root |
| Each level | `int size = q.size()` | snapshot — critical! |
| Inner loop | poll, add children | process exactly this level |

#### Java code

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> res = new ArrayList<>();
    if (root == null) return res;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    while (!q.isEmpty()) {
        int size = q.size();
        List<Integer> level = new ArrayList<>();
        for (int i = 0; i < size; i++) {
            TreeNode node = q.poll();
            level.add(node.val);
            if (node.left  != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
        res.add(level);
    }
    return res;
}
```

#### Example

```
    3
   / \
  9  20
    /  \
   15   7

Output: [[3],[9,20],[15,7]] ✓
```

---

### Problem 5 — Binary Tree Zigzag Level Order Traversal
**LeetCode #103 | Difficulty: Medium | Company: Amazon, Facebook | Category: BFS**

> Level order but alternate left-to-right and right-to-left each level.

#### Java code

```java
public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
    List<List<Integer>> res = new ArrayList<>();
    if (root == null) return res;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    boolean leftToRight = true;
    while (!q.isEmpty()) {
        int size = q.size();
        LinkedList<Integer> level = new LinkedList<>();
        for (int i = 0; i < size; i++) {
            TreeNode node = q.poll();
            if (leftToRight) level.addLast(node.val);
            else             level.addFirst(node.val);   // reverse direction
            if (node.left  != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
        res.add(level);
        leftToRight = !leftToRight;
    }
    return res;
}
```

#### Example

```
    3
   / \
  9  20
    /  \
   15   7

Output: [[3],[20,9],[15,7]] ✓
```

---

### Problem 6 — Binary Tree Level Order Traversal II
**LeetCode #107 | Difficulty: Easy | Company: Amazon | Category: BFS**

> Same as level order but return bottom-up (deepest level first).

#### Java code

```java
public List<List<Integer>> levelOrderBottom(TreeNode root) {
    LinkedList<List<Integer>> res = new LinkedList<>();
    if (root == null) return res;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    while (!q.isEmpty()) {
        int size = q.size();
        List<Integer> level = new ArrayList<>();
        for (int i = 0; i < size; i++) {
            TreeNode node = q.poll();
            level.add(node.val);
            if (node.left  != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
        res.addFirst(level);   // prepend each level → bottom-up result
    }
    return res;
}
```

---

## Category 2 — Mirror & Symmetry

---

### Problem 7 — Invert Binary Tree
**LeetCode #226 | Difficulty: Easy | Company: Amazon, Google | Category: Mirror**

> Invert (mirror) a binary tree.

#### Java code

```java
public TreeNode invertTree(TreeNode root) {
    if (root == null) return null;
    TreeNode tmp   = root.left;
    root.left      = invertTree(root.right);
    root.right     = invertTree(tmp);
    return root;
}
```

#### Example

```
     4               4
   /   \    →      /   \
  2     7         7     2
 / \   / \       / \   / \
1   3 6   9     9   6 3   1
```

---

### Problem 8 — Symmetric Tree
**LeetCode #101 | Difficulty: Easy | Company: Amazon, Microsoft | Category: Symmetry**

> Check if a binary tree is a mirror image of itself.

#### Java code

```java
public boolean isSymmetric(TreeNode root) {
    return isMirror(root.left, root.right);
}

private boolean isMirror(TreeNode left, TreeNode right) {
    if (left == null && right == null) return true;
    if (left == null || right == null) return false;
    return left.val == right.val
        && isMirror(left.left,  right.right)   // outer pair
        && isMirror(left.right, right.left);   // inner pair
}
```

---

### Problem 9 — Same Tree
**LeetCode #100 | Difficulty: Easy | Company: Amazon | Category: Comparison**

> Check if two binary trees are identical (same structure and values).

#### Java code

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

### Problem 10 — Subtree of Another Tree
**LeetCode #572 | Difficulty: Medium | Company: Amazon, Facebook | Category: Comparison**

> Check if `subRoot` is a subtree of `root`.

#### Java code

```java
public boolean isSubtree(TreeNode root, TreeNode subRoot) {
    if (root == null) return false;
    if (isSameTree(root, subRoot)) return true;
    return isSubtree(root.left, subRoot) || isSubtree(root.right, subRoot);
}

private boolean isSameTree(TreeNode p, TreeNode q) {
    if (p == null && q == null) return true;
    if (p == null || q == null) return false;
    return p.val == q.val && isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
}
```

#### Example

```
root:           3          subRoot:  4
               / \                  / \
              4   5                1   2
             / \
            1   2
Output: true ✓
```

---

### Problem 11 — Flip Equivalent Binary Trees
**LeetCode #951 | Difficulty: Medium | Company: Google | Category: Mirror**

> Two trees are flip equivalent if one can be obtained by flipping (swapping children) some nodes of the other.

#### Java code

```java
public boolean flipEquiv(TreeNode root1, TreeNode root2) {
    if (root1 == null && root2 == null) return true;
    if (root1 == null || root2 == null) return false;
    if (root1.val != root2.val) return false;

    // Either no flip or flip at this node
    boolean noFlip = flipEquiv(root1.left,  root2.left)
                  && flipEquiv(root1.right, root2.right);
    boolean flip   = flipEquiv(root1.left,  root2.right)
                  && flipEquiv(root1.right, root2.left);
    return noFlip || flip;
}
```

---

## Category 3 — Traversal & Search (BST)

---

### Problem 12 — Search in a Binary Search Tree
**LeetCode #700 | Difficulty: Easy | Company: Amazon | Category: BST Search**

> Find the node with value `val` in BST, return its subtree.

#### Java code

```java
public TreeNode searchBST(TreeNode root, int val) {
    if (root == null || root.val == val) return root;
    return val < root.val
        ? searchBST(root.left,  val)
        : searchBST(root.right, val);
}
```

---

### Problem 13 — Lowest Common Ancestor of BST
**LeetCode #235 | Difficulty: Medium | Company: Amazon, Facebook | Category: BST LCA**

> Find LCA of two nodes in a BST using the BST property.

#### Core insight

If both `p` and `q` are less than `root` → LCA is in left subtree. If both greater → right. Otherwise `root` is the LCA.

#### Java code

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (p.val < root.val && q.val < root.val)
        return lowestCommonAncestor(root.left, p, q);
    if (p.val > root.val && q.val > root.val)
        return lowestCommonAncestor(root.right, p, q);
    return root;   // split point = LCA
}
```

---

### Problem 14 — Lowest Common Ancestor of Binary Tree
**LeetCode #236 | Difficulty: Medium | Company: Amazon, Facebook, Google | Category: LCA**

> Find LCA in a general binary tree (no BST property).

#### Core insight

Post-order DFS. If both left and right return non-null, current node is LCA. Otherwise propagate the non-null result up.

#### Java code

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q) return root;
    TreeNode left  = lowestCommonAncestor(root.left,  p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);
    if (left != null && right != null) return root;   // p and q on different sides
    return left != null ? left : right;
}
```

#### Example

```
        3
       / \
      5   1
     / \ / \
    6  2 0  8
      / \
     7   4
LCA(5, 1) = 3 ✓
LCA(5, 4) = 5 ✓  (5 is ancestor of 4)
```

---

### Problem 15 — Lowest Common Ancestor of Deepest Leaves
**LeetCode #1123 | Difficulty: Medium | Company: Google | Category: LCA**

> Find the LCA of the deepest leaves.

#### Java code

```java
public TreeNode lcaDeepestLeaves(TreeNode root) {
    return dfs(root).node;
}

record Pair(TreeNode node, int depth) {}

Pair dfs(TreeNode node) {
    if (node == null) return new Pair(null, 0);
    Pair left  = dfs(node.left);
    Pair right = dfs(node.right);
    if (left.depth == right.depth)
        return new Pair(node, left.depth + 1);      // both sides equal depth → LCA is here
    return left.depth > right.depth
        ? new Pair(left.node,  left.depth  + 1)
        : new Pair(right.node, right.depth + 1);
}
```

---

### Problem 16 — Find Mode in BST
**LeetCode #501 | Difficulty: Easy | Company: Amazon | Category: BST Traversal**

> Find the most frequently occurring value(s) in a BST.

#### Java code

```java
int maxCount = 0, currCount = 0, currVal = Integer.MIN_VALUE;

public int[] findMode(TreeNode root) {
    List<Integer> modes = new ArrayList<>();
    inorder(root, modes);
    return modes.stream().mapToInt(i -> i).toArray();
}

private void inorder(TreeNode node, List<Integer> modes) {
    if (node == null) return;
    inorder(node.left, modes);

    if (node.val == currVal) currCount++;
    else { currVal = node.val; currCount = 1; }

    if (currCount > maxCount) { maxCount = currCount; modes.clear(); modes.add(currVal); }
    else if (currCount == maxCount) modes.add(currVal);

    inorder(node.right, modes);
}
```

---

### Problem 17 — Two Sum IV — BST
**LeetCode #653 | Difficulty: Easy | Company: Amazon | Category: BST Search**

> Find if there exist two elements in BST that sum to `k`.

#### Java code

```java
public boolean findTarget(TreeNode root, int k) {
    Set<Integer> seen = new HashSet<>();
    return dfs(root, k, seen);
}

private boolean dfs(TreeNode node, int k, Set<Integer> seen) {
    if (node == null) return false;
    if (seen.contains(k - node.val)) return true;
    seen.add(node.val);
    return dfs(node.left, k, seen) || dfs(node.right, k, seen);
}
```

---

### Problem 18 — Kth Smallest Element in BST
**LeetCode #230 | Difficulty: Medium | Company: Amazon, Google | Category: BST Inorder**

> Find the kth smallest element in a BST. Inorder traversal of BST = sorted order.

#### Java code

```java
private int k, result;

public int kthSmallest(TreeNode root, int k) {
    this.k = k;
    inorder(root);
    return result;
}

private void inorder(TreeNode node) {
    if (node == null) return;
    inorder(node.left);
    if (--k == 0) { result = node.val; return; }
    inorder(node.right);
}
```

#### Example

```
    3
   / \
  1   4
   \
    2
k=1 → inorder: 1,2,3,4 → return 1 ✓
k=3 → return 3 ✓
```

---

## Category 4 — Validation & Properties

---

### Problem 19 — Minimum Depth of Binary Tree
**LeetCode #111 | Difficulty: Easy | Company: Amazon | Category: Depth**

> Find the minimum depth (root to nearest leaf).

#### Core insight

BFS is optimal — stops as soon as first leaf is found. DFS must handle the case where one child is null (don't return 0 for that side).

#### Java code

```java
public int minDepth(TreeNode root) {
    if (root == null) return 0;
    if (root.left == null && root.right == null) return 1;
    if (root.left  == null) return 1 + minDepth(root.right);  // can't go left
    if (root.right == null) return 1 + minDepth(root.left);   // can't go right
    return 1 + Math.min(minDepth(root.left), minDepth(root.right));
}
```

---

### Problem 20 — Maximum Depth of Binary Tree
**LeetCode #104 | Difficulty: Easy | Company: Amazon, Google | Category: Depth**

> Find the maximum depth (height) of a binary tree.

#### Java code

```java
public int maxDepth(TreeNode root) {
    if (root == null) return 0;
    return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
```

---

### Problem 21 — Balanced Binary Tree
**LeetCode #110 | Difficulty: Easy | Company: Amazon, Google | Category: Validation**

> Check if a binary tree is height-balanced (every node's left and right heights differ by at most 1).

#### Core insight

Return -1 to signal "unbalanced" — avoids recomputing heights. Single pass bottom-up.

#### Java code

```java
public boolean isBalanced(TreeNode root) {
    return checkHeight(root) != -1;
}

private int checkHeight(TreeNode node) {
    if (node == null) return 0;
    int left  = checkHeight(node.left);
    int right = checkHeight(node.right);
    if (left == -1 || right == -1) return -1;         // propagate unbalanced signal
    if (Math.abs(left - right) > 1)  return -1;       // this node is unbalanced
    return 1 + Math.max(left, right);
}
```

---

### Problem 22 — Diameter of Binary Tree
**LeetCode #543 | Difficulty: Easy | Company: Facebook, Amazon | Category: Properties**

> Find the length of the longest path between any two nodes (may not pass through root).

#### Java code

```java
private int diameter = 0;

public int diameterOfBinaryTree(TreeNode root) {
    height(root);
    return diameter;
}

private int height(TreeNode node) {
    if (node == null) return 0;
    int left  = height(node.left);
    int right = height(node.right);
    diameter = Math.max(diameter, left + right);   // path through this node
    return 1 + Math.max(left, right);
}
```

#### Example

```
      1
     / \
    2   3
   / \
  4   5
diameter = 3 (path: 4→2→1→3 or 5→2→1→3) ✓
```

---

### Problem 23 — Binary Tree Tilt
**LeetCode #563 | Difficulty: Easy | Company: Amazon | Category: Properties**

> Find the sum of every node's tilt. Tilt = |sum(left subtree) - sum(right subtree)|.

#### Java code

```java
private int totalTilt = 0;

public int findTilt(TreeNode root) {
    subtreeSum(root);
    return totalTilt;
}

private int subtreeSum(TreeNode node) {
    if (node == null) return 0;
    int left  = subtreeSum(node.left);
    int right = subtreeSum(node.right);
    totalTilt += Math.abs(left - right);
    return left + right + node.val;
}
```

---

### Problem 24 — Check Completeness of Binary Tree
**LeetCode #958 | Difficulty: Medium | Company: Amazon | Category: Validation**

> A complete binary tree has all levels full except possibly the last (filled left to right).

#### Core insight

BFS. Once we see a null node, all subsequent nodes must also be null. If a non-null appears after null → not complete.

#### Java code

```java
public boolean isCompleteTree(TreeNode root) {
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    boolean seenNull = false;

    while (!q.isEmpty()) {
        TreeNode node = q.poll();
        if (node == null) {
            seenNull = true;
        } else {
            if (seenNull) return false;   // non-null after null → not complete
            q.offer(node.left);
            q.offer(node.right);
        }
    }
    return true;
}
```

---

### Problem 25 — Validate Binary Search Tree
**LeetCode #98 | Difficulty: Medium | Company: Amazon, Google, Facebook | Category: BST Validation**

> Determine if a binary tree is a valid BST.

#### Core insight

Pass min and max bounds down. Every node must satisfy `min < node.val < max`. Use `Long` to handle `Integer.MIN/MAX_VALUE` edge cases.

#### Java code

```java
public boolean isValidBST(TreeNode root) {
    return validate(root, Long.MIN_VALUE, Long.MAX_VALUE);
}

private boolean validate(TreeNode node, long min, long max) {
    if (node == null) return true;
    if (node.val <= min || node.val >= max) return false;
    return validate(node.left,  min, node.val)
        && validate(node.right, node.val, max);
}
```

#### Example

```
    5
   / \
  1   4
     / \
    3   6
validate: 4 is in right subtree of 5 → must be > 5. But 4 < 5 → false ✓
```

---

### Problem 26 — Recover Binary Search Tree
**LeetCode #99 | Difficulty: Hard | Company: Amazon, Google | Category: BST Recovery**

> Two nodes of a BST are swapped. Fix the BST without changing its structure.

#### Core insight

Inorder traversal of a valid BST is strictly increasing. Find the two "out of order" nodes and swap their values.

#### Java code

```java
TreeNode first = null, second = null, prev = null;

public void recoverTree(TreeNode root) {
    inorder(root);
    int tmp = first.val;
    first.val = second.val;
    second.val = tmp;
}

private void inorder(TreeNode node) {
    if (node == null) return;
    inorder(node.left);
    if (prev != null && prev.val > node.val) {
        if (first == null) first = prev;   // first violation: prev is wrong
        second = node;                      // second violation: current is wrong
    }
    prev = node;
    inorder(node.right);
}
```

#### Example

```
Swapped:   1 → 3 → 2 → 4   (3 and 2 are swapped)
Inorder violation at (3,2): first=3, second=2
Swap values: 1 → 2 → 3 → 4 ✓
```

---

## Category 5 — Path Sum & Root to Leaf

---

### Problem 27 — Path Sum
**LeetCode #112 | Difficulty: Easy | Company: Amazon | Category: Path Sum**

> Check if there is a root-to-leaf path with sum equal to `targetSum`.

#### Java code

```java
public boolean hasPathSum(TreeNode root, int targetSum) {
    if (root == null) return false;
    if (root.left == null && root.right == null) return root.val == targetSum;
    int remaining = targetSum - root.val;
    return hasPathSum(root.left, remaining) || hasPathSum(root.right, remaining);
}
```

---

### Problem 28 — Path Sum II
**LeetCode #113 | Difficulty: Medium | Company: Amazon, Facebook | Category: Path Sum**

> Find all root-to-leaf paths where the sum equals `targetSum`.

#### Java code

```java
public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
    List<List<Integer>> res = new ArrayList<>();
    dfs(root, targetSum, new ArrayList<>(), res);
    return res;
}

private void dfs(TreeNode node, int remaining, List<Integer> path, List<List<Integer>> res) {
    if (node == null) return;
    path.add(node.val);
    if (node.left == null && node.right == null && remaining == node.val)
        res.add(new ArrayList<>(path));   // copy — don't add reference
    dfs(node.left,  remaining - node.val, path, res);
    dfs(node.right, remaining - node.val, path, res);
    path.remove(path.size() - 1);        // backtrack
}
```

---

### Problem 29 — Path Sum III
**LeetCode #437 | Difficulty: Medium | Company: Amazon, Google | Category: Path Sum**

> Count paths (not necessarily root-to-leaf) where sum equals `targetSum`.

#### Core insight

Prefix sum + HashMap. At each node, check how many previous prefix sums equal `currentSum - target`. Backtrack after returning.

#### Java code

```java
public int pathSum(TreeNode root, int targetSum) {
    Map<Long, Integer> prefixCount = new HashMap<>();
    prefixCount.put(0L, 1);
    return dfs(root, 0L, targetSum, prefixCount);
}

private int dfs(TreeNode node, long curr, int target, Map<Long, Integer> map) {
    if (node == null) return 0;
    curr += node.val;
    int count = map.getOrDefault(curr - target, 0);
    map.merge(curr, 1, Integer::sum);
    count += dfs(node.left,  curr, target, map);
    count += dfs(node.right, curr, target, map);
    map.merge(curr, -1, Integer::sum);   // backtrack
    return count;
}
```

#### Example

```
       10
      /  \
     5   -3
    / \    \
   3   2   11
  / \   \
 3  -2   1
target = 8
Paths: 10→-3→11, 5→3, 5→2→1, 10→5→-2→... → count = 3 ✓
```

---

### Problem 30 — Sum Root to Leaf Numbers
**LeetCode #129 | Difficulty: Medium | Company: Amazon, Google | Category: Path Sum**

> Each root-to-leaf path forms a number. Return the total sum of all such numbers.

#### Java code

```java
public int sumNumbers(TreeNode root) {
    return dfs(root, 0);
}

private int dfs(TreeNode node, int currentNum) {
    if (node == null) return 0;
    currentNum = currentNum * 10 + node.val;
    if (node.left == null && node.right == null) return currentNum;   // leaf
    return dfs(node.left, currentNum) + dfs(node.right, currentNum);
}
```

#### Example

```
    1
   / \
  2   3
Paths: 1→2 = 12, 1→3 = 13. Sum = 25 ✓
```

---

### Problem 31 — Binary Tree Maximum Path Sum
**LeetCode #124 | Difficulty: Hard | Company: Amazon, Facebook, Google | Category: Path Sum**

> Find the maximum path sum where the path can start and end at any node.

#### Core insight

At each node: update global max using BOTH children (path can go through both). But return only ONE side to parent (a path can't fork upward).

#### Java code

```java
private int maxSum = Integer.MIN_VALUE;

public int maxPathSum(TreeNode root) {
    dfs(root);
    return maxSum;
}

private int dfs(TreeNode node) {
    if (node == null) return 0;
    int left  = Math.max(0, dfs(node.left));    // ignore negative branches
    int right = Math.max(0, dfs(node.right));
    maxSum = Math.max(maxSum, left + node.val + right);  // update: use both sides
    return node.val + Math.max(left, right);             // return: only one side
}
```

#### Example

```
    -10
    /  \
   9   20
      /  \
     15   7
Max path: 15 → 20 → 7 = 42 ✓
```

---

## Category 6 — Construction

---

### Problem 32 — Construct BT from Preorder and Inorder
**LeetCode #105 | Difficulty: Medium | Company: Amazon, Google, Facebook | Category: Construction**

> Reconstruct binary tree given preorder and inorder traversal arrays.

#### Core insight

`preorder[0]` = root. Find root in inorder → left size = `mid - inStart`. Recurse on left and right halves. Use HashMap for O(1) inorder lookup.

#### Java code

```java
Map<Integer, Integer> inorderMap = new HashMap<>();
int preIdx = 0;

public TreeNode buildTree(int[] preorder, int[] inorder) {
    for (int i = 0; i < inorder.length; i++) inorderMap.put(inorder[i], i);
    return build(preorder, 0, inorder.length - 1);
}

private TreeNode build(int[] preorder, int inLeft, int inRight) {
    if (inLeft > inRight) return null;
    int rootVal = preorder[preIdx++];
    TreeNode root = new TreeNode(rootVal);
    int mid = inorderMap.get(rootVal);
    root.left  = build(preorder, inLeft,  mid - 1);
    root.right = build(preorder, mid + 1, inRight);
    return root;
}
```

#### Example

```
preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
root=3, mid=1. left=[9], right=[20,15,7]
Output:    3
          / \
         9  20
           /  \
          15   7  ✓
```

---

### Problem 33 — Construct BT from Inorder and Postorder
**LeetCode #106 | Difficulty: Medium | Company: Amazon | Category: Construction**

> Reconstruct binary tree given inorder and postorder traversal arrays.

#### Core insight

`postorder[last]` = root. Find root in inorder → right subtree first (postorder reads right before root).

#### Java code

```java
Map<Integer, Integer> inorderMap = new HashMap<>();
int postIdx;

public TreeNode buildTree(int[] inorder, int[] postorder) {
    for (int i = 0; i < inorder.length; i++) inorderMap.put(inorder[i], i);
    postIdx = postorder.length - 1;
    return build(postorder, 0, inorder.length - 1);
}

private TreeNode build(int[] postorder, int inLeft, int inRight) {
    if (inLeft > inRight) return null;
    int rootVal = postorder[postIdx--];
    TreeNode root = new TreeNode(rootVal);
    int mid = inorderMap.get(rootVal);
    root.right = build(postorder, mid + 1, inRight);   // right FIRST (postorder is L,R,Root)
    root.left  = build(postorder, inLeft,  mid - 1);
    return root;
}
```

---

### Problem 34 — Construct BT from Preorder and Postorder
**LeetCode #889 | Difficulty: Medium | Company: Google | Category: Construction**

> Reconstruct binary tree given preorder and postorder (result may not be unique).

#### Java code

```java
Map<Integer, Integer> postMap = new HashMap<>();
int preIdx = 0;

public TreeNode constructFromPrePost(int[] preorder, int[] postorder) {
    for (int i = 0; i < postorder.length; i++) postMap.put(postorder[i], i);
    return build(preorder, 0, postorder.length - 1);
}

private TreeNode build(int[] preorder, int postLeft, int postRight) {
    if (postLeft > postRight) return null;
    TreeNode root = new TreeNode(preorder[preIdx++]);
    if (postLeft == postRight) return root;

    int leftRootVal = preorder[preIdx];           // next in preorder = left child root
    int leftSize = postMap.get(leftRootVal) - postLeft + 1;

    root.left  = build(preorder, postLeft, postLeft + leftSize - 1);
    root.right = build(preorder, postLeft + leftSize, postRight - 1);
    return root;
}
```

---

### Problem 35 — Convert Sorted Array to BST
**LeetCode #108 | Difficulty: Easy | Company: Amazon, Google | Category: Construction**

> Convert a sorted array to a height-balanced BST.

#### Core insight

Midpoint = root. Recurse on left half (left subtree) and right half (right subtree).

#### Java code

```java
public TreeNode sortedArrayToBST(int[] nums) {
    return build(nums, 0, nums.length - 1);
}

private TreeNode build(int[] nums, int left, int right) {
    if (left > right) return null;
    int mid = left + (right - left) / 2;
    TreeNode root = new TreeNode(nums[mid]);
    root.left  = build(nums, left, mid - 1);
    root.right = build(nums, mid + 1, right);
    return root;
}
```

#### Example

```
nums = [-10,-3,0,5,9]
mid=0 → root=0. left=[-10,-3], right=[5,9]
Output:    0
          / \
        -3   9
        /   /
      -10  5  ✓
```

---

### Problem 36 — Convert Sorted List to BST
**LeetCode #109 | Difficulty: Medium | Company: Amazon | Category: Construction**

> Convert a sorted linked list to a height-balanced BST.

#### Core insight

Use slow/fast pointers to find mid of linked list. Split list, recurse. Or use inorder simulation with a global list pointer.

#### Java code

```java
public TreeNode sortedListToBST(ListNode head) {
    if (head == null) return null;
    if (head.next == null) return new TreeNode(head.val);

    // Find mid using slow/fast
    ListNode prev = null, slow = head, fast = head;
    while (fast != null && fast.next != null) {
        prev = slow; slow = slow.next; fast = fast.next.next;
    }
    prev.next = null;   // cut left half

    TreeNode root  = new TreeNode(slow.val);
    root.left  = sortedListToBST(head);
    root.right = sortedListToBST(slow.next);
    return root;
}
```

---

### Problem 37 — Serialize and Deserialize Binary Tree
**LeetCode #297 | Difficulty: Hard | Company: Amazon, Facebook, Google | Category: Serialization**

> Design an algorithm to serialize (tree → string) and deserialize (string → tree) a binary tree.

#### Core insight

Preorder DFS with "null" markers. Serialize writes node values with commas; null nodes write "null". Deserialize reads values from a queue and rebuilds recursively.

#### Java code

```java
public String serialize(TreeNode root) {
    if (root == null) return "null";
    return root.val + "," + serialize(root.left) + "," + serialize(root.right);
}

public TreeNode deserialize(String data) {
    Queue<String> q = new LinkedList<>(Arrays.asList(data.split(",")));
    return build(q);
}

private TreeNode build(Queue<String> q) {
    String val = q.poll();
    if (val.equals("null")) return null;
    TreeNode node = new TreeNode(Integer.parseInt(val));
    node.left  = build(q);
    node.right = build(q);
    return node;
}
```

#### Example

```
Tree:        1
            / \
           2   3
              / \
             4   5

Serialized: "1,2,null,null,3,4,null,null,5,null,null"
Deserialize: rebuilds original tree ✓
```

---

## Quick Pattern Reference

| Problem | Category | Direction | Key trick |
|---------|----------|-----------|-----------|
| Inorder / Pre / Postorder | Traversal | DFS | iterative with explicit stack |
| Level Order | BFS | level-by-level | snapshot `size = q.size()` |
| Zigzag Level Order | BFS + flag | level-by-level | `LinkedList.addFirst/addLast` |
| Level Order II | BFS | bottom-up | `res.addFirst(level)` |
| Invert Tree | Mirror | top-down | swap left/right, recurse |
| Symmetric Tree | Symmetry | dual DFS | compare outer+inner pairs |
| Same Tree | Comparison | dual DFS | check val + recurse both |
| Subtree | Comparison | DFS + isSame | isSameTree at every node |
| Flip Equivalent | Mirror | dual DFS | try both flip and no-flip |
| LCA BST | BST Search | top-down | both smaller → left; both larger → right |
| LCA Binary Tree | LCA | bottom-up | both sides non-null → root is LCA |
| LCA Deepest Leaves | LCA | bottom-up | equal depth → LCA here |
| Find Mode BST | BST Inorder | in-order | track prev, currCount, maxCount |
| Two Sum IV | BST | DFS + set | HashSet for complement lookup |
| Kth Smallest BST | BST Inorder | in-order | stop at kth, counter |
| Min/Max Depth | Depth | bottom-up | `1 + min/max(L, R)` |
| Balanced | Validation | bottom-up | return -1 on imbalance |
| Diameter | Properties | bottom-up + global | `L + R` at each node |
| Tilt | Properties | bottom-up + global | `|left - right|` sum |
| Check Completeness | BFS | level-by-level | null after non-null → false |
| Validate BST | Validation | top-down bounds | pass (min, max) as Long |
| Recover BST | BST Inorder | in-order | find 2 out-of-order nodes |
| Path Sum I | Path | top-down | leaf check + remaining |
| Path Sum II | Path | top-down + backtrack | copy list on leaf |
| Path Sum III | Path | prefix sum | HashMap + backtrack |
| Sum Root to Leaf | Path | top-down | `curr * 10 + val` |
| Max Path Sum | Path | bottom-up + global | ignore negatives; return one side |
| Construct Pre+In | Construction | divide & conquer | HashMap inorder index |
| Construct In+Post | Construction | divide & conquer | postIdx from end |
| Construct Pre+Post | Construction | divide & conquer | next preorder = left root |
| Sorted Array to BST | Construction | binary mid | mid as root |
| Sorted List to BST | Construction | slow/fast mid | cut list at mid |
| Serialize/Deserialize | Serialization | preorder + nulls | queue-based rebuild |

---

## Category 1 (Extended) — Level Order BFS

---

### Problem 38 — Even Odd Tree
**LeetCode #1609 | Difficulty: Medium | Company: Amazon | Category: BFS**

> In an "Even-Odd Tree": even-indexed levels have strictly increasing odd values; odd-indexed levels have strictly decreasing even values.

#### Java code

```java
public boolean isEvenOddTree(TreeNode root) {
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    boolean evenLevel = true;

    while (!q.isEmpty()) {
        int size = q.size();
        int prev = evenLevel ? Integer.MIN_VALUE : Integer.MAX_VALUE;

        for (int i = 0; i < size; i++) {
            TreeNode node = q.poll();
            int val = node.val;

            if (evenLevel && (val % 2 == 0 || val <= prev)) return false;  // must be odd, increasing
            if (!evenLevel && (val % 2 == 1 || val >= prev)) return false; // must be even, decreasing

            prev = val;
            if (node.left  != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
        evenLevel = !evenLevel;
    }
    return true;
}
```

---

### Problem 39 — Reverse Odd Levels of Binary Tree
**LeetCode #2415 | Difficulty: Medium | Company: Google | Category: BFS**

> Reverse the node values at each odd level of a perfect binary tree.

#### Java code

```java
public TreeNode reverseOddLevels(TreeNode root) {
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    int level = 0;

    while (!q.isEmpty()) {
        int size = q.size();
        List<TreeNode> nodes = new ArrayList<>();
        for (int i = 0; i < size; i++) {
            TreeNode node = q.poll();
            nodes.add(node);
            if (node.left  != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
        if (level % 2 == 1) {
            int l = 0, r = nodes.size() - 1;
            while (l < r) {
                int tmp = nodes.get(l).val;
                nodes.get(l).val = nodes.get(r).val;
                nodes.get(r).val = tmp;
                l++; r--;
            }
        }
        level++;
    }
    return root;
}
```

---

### Problem 40 — Deepest Leaves Sum
**LeetCode #1302 | Difficulty: Medium | Company: Amazon | Category: BFS**

> Return the sum of values of the deepest leaves.

#### Java code

```java
public int deepestLeavesSum(TreeNode root) {
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    int sum = 0;

    while (!q.isEmpty()) {
        int size = q.size();
        sum = 0;
        for (int i = 0; i < size; i++) {
            TreeNode node = q.poll();
            sum += node.val;
            if (node.left  != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
    }
    return sum;   // last level sum = deepest leaves sum
}
```

#### Example

```
        1
       / \
      2   3
     / \   \
    4   5   6
           / \
          7   8
Deepest level: [7, 8] → sum = 15 ✓
```

---

### Problem 41 — Add One Row to Tree
**LeetCode #623 | Difficulty: Medium | Company: Amazon | Category: BFS**

> At depth `d`, add a new row of nodes with value `val`. Original children become left/right children of new nodes.

#### Java code

```java
public TreeNode addOneRow(TreeNode root, int val, int depth) {
    if (depth == 1) {
        TreeNode newRoot = new TreeNode(val);
        newRoot.left = root;
        return newRoot;
    }
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    int currDepth = 1;

    while (!q.isEmpty()) {
        int size = q.size();
        if (currDepth == depth - 1) {
            for (int i = 0; i < size; i++) {
                TreeNode node = q.poll();
                TreeNode newLeft  = new TreeNode(val);
                TreeNode newRight = new TreeNode(val);
                newLeft.left   = node.left;
                newRight.right = node.right;
                node.left  = newLeft;
                node.right = newRight;
            }
            break;
        }
        for (int i = 0; i < size; i++) {
            TreeNode node = q.poll();
            if (node.left  != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
        currDepth++;
    }
    return root;
}
```

---

### Problem 42 — Maximum Width of Binary Tree
**LeetCode #662 | Difficulty: Medium | Company: Amazon, Google | Category: BFS**

> Find the maximum width of any level (width = distance between leftmost and rightmost non-null nodes, including nulls between them).

#### Core insight

Assign index to each node: root=0, left child = 2*i, right child = 2*i+1. Width of level = `rightmost - leftmost + 1`. Normalize indices to prevent overflow.

#### Java code

```java
public int widthOfBinaryTree(TreeNode root) {
    Queue<long[]> q = new LinkedList<>();  // [node_ptr_as_id, index]
    q.offer(new long[]{0, 0});  // use queue of (node placeholder) — actually store TreeNode
    // Better: use two parallel queues
    Queue<TreeNode> nodes = new LinkedList<>();
    Queue<Long> indices = new LinkedList<>();
    nodes.offer(root);
    indices.offer(0L);
    int maxWidth = 0;

    while (!nodes.isEmpty()) {
        int size = nodes.size();
        long left = indices.peek(), right = left;

        for (int i = 0; i < size; i++) {
            TreeNode node = nodes.poll();
            long idx = indices.poll() - left;   // normalize to prevent overflow
            right = idx;

            if (node.left  != null) { nodes.offer(node.left);  indices.offer(2 * idx); }
            if (node.right != null) { nodes.offer(node.right); indices.offer(2 * idx + 1); }
        }
        maxWidth = (int) Math.max(maxWidth, right + 1);
    }
    return maxWidth;
}
```

---

### Problem 43 — All Nodes Distance K in Binary Tree
**LeetCode #863 | Difficulty: Medium | Company: Amazon, Facebook | Category: BFS + Graph**

> Find all nodes at distance K from a target node.

#### Core insight

Build a parent map (each node → its parent). Then BFS from target, treating the tree as an undirected graph.

#### Java code

```java
public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
    Map<TreeNode, TreeNode> parent = new HashMap<>();
    buildParentMap(root, null, parent);

    Queue<TreeNode> q = new LinkedList<>();
    Set<TreeNode> visited = new HashSet<>();
    q.offer(target);
    visited.add(target);

    int dist = 0;
    while (!q.isEmpty()) {
        if (dist == k) {
            List<Integer> res = new ArrayList<>();
            for (TreeNode node : q) res.add(node.val);
            return res;
        }
        int size = q.size();
        for (int i = 0; i < size; i++) {
            TreeNode node = q.poll();
            for (TreeNode neighbor : new TreeNode[]{node.left, node.right, parent.get(node)}) {
                if (neighbor != null && !visited.contains(neighbor)) {
                    visited.add(neighbor);
                    q.offer(neighbor);
                }
            }
        }
        dist++;
    }
    return new ArrayList<>();
}

private void buildParentMap(TreeNode node, TreeNode par, Map<TreeNode, TreeNode> parent) {
    if (node == null) return;
    parent.put(node, par);
    buildParentMap(node.left,  node, parent);
    buildParentMap(node.right, node, parent);
}
```

---

## Category 6 (Extended) — Construction

---

### Problem 44 — Maximum Binary Tree
**LeetCode #654 | Difficulty: Medium | Company: Amazon | Category: Construction**

> Build the "maximum binary tree" — root is max element, left/right subtrees built from elements to left/right of max.

#### Java code

```java
public TreeNode constructMaximumBinaryTree(int[] nums) {
    return build(nums, 0, nums.length - 1);
}

private TreeNode build(int[] nums, int left, int right) {
    if (left > right) return null;
    int maxIdx = left;
    for (int i = left + 1; i <= right; i++)
        if (nums[i] > nums[maxIdx]) maxIdx = i;

    TreeNode root = new TreeNode(nums[maxIdx]);
    root.left  = build(nums, left, maxIdx - 1);
    root.right = build(nums, maxIdx + 1, right);
    return root;
}
```

#### Example

```
nums = [3,2,1,6,0,5]
max=6(idx3) → root=6
left=[3,2,1]: max=3 → left subtree
right=[0,5]: max=5 → right subtree
Output:       6
             / \
            3   5
             \  /
              2 0
               \
                1  ✓
```

---

### Problem 45 — Construct BST from Preorder Traversal
**LeetCode #1008 | Difficulty: Medium | Company: Amazon | Category: Construction**

> Reconstruct a BST given its preorder traversal.

#### Core insight

`preorder[0]` = root. Use upper bound to split left/right subtrees (all values < root go left).

#### Java code

```java
int idx = 0;

public TreeNode bstFromPreorder(int[] preorder) {
    return build(preorder, Integer.MAX_VALUE);
}

private TreeNode build(int[] preorder, int upperBound) {
    if (idx == preorder.length || preorder[idx] > upperBound) return null;
    TreeNode root = new TreeNode(preorder[idx++]);
    root.left  = build(preorder, root.val);         // left: < root.val
    root.right = build(preorder, upperBound);        // right: < upperBound
    return root;
}
```

#### Example

```
preorder = [8,5,1,7,10,12]
root=8. left: [5,1,7] (all<8), right: [10,12] (all>8)
Output:    8
          / \
         5  10
        / \   \
       1   7  12  ✓
```

---

## Category 5 (Extended) — Root to Leaf Paths

---

### Problem 46 — Binary Tree Paths
**LeetCode #257 | Difficulty: Easy | Company: Apple, Google | Category: Root to Leaf**

> Return all root-to-leaf paths as strings like "1->2->5".

#### Java code

```java
public List<String> binaryTreePaths(TreeNode root) {
    List<String> res = new ArrayList<>();
    dfs(root, "", res);
    return res;
}

private void dfs(TreeNode node, String path, List<String> res) {
    if (node == null) return;
    path += node.val;
    if (node.left == null && node.right == null) { res.add(path); return; }
    dfs(node.left,  path + "->", res);
    dfs(node.right, path + "->", res);
}
```

#### Example

```
    1
   / \
  2   3
   \
    5
Output: ["1->2->5", "1->3"] ✓
```

---

### Problem 47 — Smallest String Starting from Leaf
**LeetCode #988 | Difficulty: Medium | Company: Amazon | Category: Root to Leaf**

> Find the lexicographically smallest string formed by concatenating node values (a=0, b=1...) from leaf to root.

#### Java code

```java
String result = null;

public String smallestFromLeaf(TreeNode root) {
    dfs(root, new StringBuilder());
    return result;
}

private void dfs(TreeNode node, StringBuilder sb) {
    if (node == null) return;
    sb.insert(0, (char)('a' + node.val));   // prepend (leaf→root order)

    if (node.left == null && node.right == null) {
        String s = sb.toString();
        if (result == null || s.compareTo(result) < 0) result = s;
    }
    dfs(node.left,  sb);
    dfs(node.right, sb);
    sb.deleteCharAt(0);   // backtrack
}
```

---

### Problem 48 — Insufficient Nodes in Root to Leaf Paths
**LeetCode #1080 | Difficulty: Medium | Company: Google | Category: Root to Leaf**

> Remove all nodes where every root-to-leaf path through that node has sum < limit.

#### Java code

```java
public TreeNode sufficientSubset(TreeNode root, int limit) {
    if (root == null) return null;
    if (root.left == null && root.right == null)
        return root.val < limit ? null : root;   // leaf: remove if insufficient

    root.left  = sufficientSubset(root.left,  limit - root.val);
    root.right = sufficientSubset(root.right, limit - root.val);

    return (root.left == null && root.right == null) ? null : root;  // remove if both children removed
}
```

---

### Problem 49 — Pseudo-Palindromic Paths in a Binary Tree
**LeetCode #1457 | Difficulty: Medium | Company: Amazon | Category: Root to Leaf**

> Count root-to-leaf paths where digits can be rearranged to form a palindrome.

#### Core insight

A path is pseudo-palindromic if at most one digit has odd frequency. Use XOR bitmask — each bit represents whether a digit has odd count. Path is valid if bitmask has at most one set bit: `bitmask == 0 || (bitmask & (bitmask-1)) == 0`.

#### Java code

```java
public int pseudoPalindromicPaths(TreeNode root) {
    return dfs(root, 0);
}

private int dfs(TreeNode node, int mask) {
    if (node == null) return 0;
    mask ^= (1 << node.val);   // toggle this digit's bit

    if (node.left == null && node.right == null)
        return (mask == 0 || (mask & (mask - 1)) == 0) ? 1 : 0;   // at most one odd digit

    return dfs(node.left, mask) + dfs(node.right, mask);
}
```

#### Example

```
       2
      / \
     3   1
    / \   \
   3   1   1
Paths: 2→3→3 (mask: 2,3,3→only 2 odd) → palindrome ✓
       2→3→1 (mask: 2,3,1→three odd) → no
       2→1→1 (mask: 2,1,1→only 2 odd) → palindrome ✓
Output: 2 ✓
```

---

## Category 3 (Extended) — Ancestor Problems

---

### Problem 50 — Maximum Difference Between Node and Ancestor
**LeetCode #1026 | Difficulty: Medium | Company: Amazon | Category: Ancestor**

> Find the maximum value of `|node.val - ancestor.val|` for any node and its ancestor.

#### Core insight

Pass the current path's min and max down. At each node, the max difference is `max(|node - currMin|, |node - currMax|)`.

#### Java code

```java
public int maxAncestorDiff(TreeNode root) {
    return dfs(root, root.val, root.val);
}

private int dfs(TreeNode node, int currMin, int currMax) {
    if (node == null) return currMax - currMin;
    currMin = Math.min(currMin, node.val);
    currMax = Math.max(currMax, node.val);
    return Math.max(dfs(node.left, currMin, currMax),
                    dfs(node.right, currMin, currMax));
}
```

#### Example

```
       8
      / \
     3   10
    / \    \
   1   6   14
      / \  /
     4   7 13
Max diff: |8-1|=7, |10-14|=4... → 7 ✓
```

---

### Problem 51 — Kth Ancestor of a Tree Node
**LeetCode #1483 | Difficulty: Hard | Company: Amazon, Google | Category: Ancestor**

> Given a tree with n nodes, answer multiple queries: find the kth ancestor of node `node`.

#### Core insight

Binary Lifting — precompute `ancestor[node][j]` = 2^j-th ancestor of `node`. Each query answered in O(log n) by jumping in powers of 2.

#### Java code

```java
class TreeAncestor {
    private int[][] dp;
    private static final int LOG = 16;

    public TreeAncestor(int n, int[] parent) {
        dp = new int[n][LOG];
        for (int[] row : dp) Arrays.fill(row, -1);
        for (int i = 0; i < n; i++) dp[i][0] = parent[i];  // 2^0 = direct parent

        for (int j = 1; j < LOG; j++)
            for (int i = 0; i < n; i++)
                if (dp[i][j-1] != -1)
                    dp[i][j] = dp[dp[i][j-1]][j-1];  // 2^j ancestor = 2^(j-1) of 2^(j-1)
    }

    public int getKthAncestor(int node, int k) {
        for (int j = 0; j < LOG; j++) {
            if ((k >> j & 1) == 1) {   // if jth bit set, jump 2^j steps
                node = dp[node][j];
                if (node == -1) return -1;
            }
        }
        return node;
    }
}
```

---

## Category 3 (BST Extended) — Binary Search Tree

---

### Problem 52 — Range Sum of BST
**LeetCode #938 | Difficulty: Easy | Company: Amazon | Category: BST**

> Return the sum of all node values in BST within the range `[low, high]`.

#### Java code

```java
public int rangeSumBST(TreeNode root, int low, int high) {
    if (root == null) return 0;
    int sum = 0;
    if (root.val >= low && root.val <= high) sum += root.val;
    if (root.val > low)  sum += rangeSumBST(root.left,  low, high);  // left only if > low
    if (root.val < high) sum += rangeSumBST(root.right, low, high);  // right only if < high
    return sum;
}
```

#### Example

```
BST:      10
         /  \
        5   15
       / \    \
      3   7   18
low=7, high=15
Valid nodes: 7+10+15 = 32 ✓
```

---

### Problem 53 — Minimum Absolute Difference in BST
**LeetCode #530 | Difficulty: Easy | Company: Amazon | Category: BST Inorder**

> Find the minimum absolute difference between values of any two different nodes in a BST.

#### Core insight

Inorder traversal of BST is sorted. Minimum difference is always between adjacent nodes in inorder.

#### Java code

```java
int minDiff = Integer.MAX_VALUE, prev = -1;

public int getMinimumDifference(TreeNode root) {
    inorder(root);
    return minDiff;
}

private void inorder(TreeNode node) {
    if (node == null) return;
    inorder(node.left);
    if (prev != -1) minDiff = Math.min(minDiff, node.val - prev);
    prev = node.val;
    inorder(node.right);
}
```

---

### Problem 54 — Insert into a BST
**LeetCode #701 | Difficulty: Medium | Company: Amazon | Category: BST Insert**

> Insert a value into a BST and return the updated root.

#### Java code

```java
public TreeNode insertIntoBST(TreeNode root, int val) {
    if (root == null) return new TreeNode(val);   // found insertion point
    if (val < root.val) root.left  = insertIntoBST(root.left,  val);
    else                root.right = insertIntoBST(root.right, val);
    return root;
}
```

#### Example

```
BST:   4        Insert 5:    4
      / \                   / \
     2   7       →         2   7
    / \                   / \ /
   1   3                 1  3 5  ✓
```

