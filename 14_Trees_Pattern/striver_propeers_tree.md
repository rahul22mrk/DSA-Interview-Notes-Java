# Tree Pattern — Solved Problems (Striver + Code with Pratush)

> **Pattern family:** Binary Tree / BST / Tree Traversal / Construction
> **Notes & Templates:** [01_tree_notes.md](./01_tree_notes.md)
> **Language:** Java

---

## Table of Contents

### Binary Tree

#### Tree Traversal
- [P1 — Inorder Traversal](#p1--inorder-traversal)
- [P2 — Preorder Traversal](#p2--preorder-traversal)
- [P3 — Postorder Traversal](#p3--postorder-traversal)
- [P4 — Level Order Traversal](#p4--level-order-traversal)
- [P5 — Pre + Post + Inorder in One Traversal](#p5--pre--post--inorder-in-one-traversal)

#### Medium Problems
- [P6 — Maximum Depth in BT](#p6--maximum-depth-in-bt)
- [P7 — Check if Two Trees are Identical](#p7--check-if-two-trees-are-identical)
- [P8 — Check for Balanced Binary Tree](#p8--check-for-balanced-binary-tree)
- [P9 — Diameter of Binary Tree](#p9--diameter-of-binary-tree)
- [P10 — Maximum Path Sum](#p10--maximum-path-sum)
- [P11 — Check for Symmetrical BTs](#p11--check-for-symmetrical-bts)

#### FAQs
- [P12 — Zigzag / Spiral Traversal](#p12--zigzag--spiral-traversal)
- [P13 — Boundary Traversal](#p13--boundary-traversal)
- [P14 — Vertical Order Traversal](#p14--vertical-order-traversal)
- [P15 — Top View of BT](#p15--top-view-of-bt)
- [P16 — Bottom View of BT](#p16--bottom-view-of-bt)
- [P17 — Right / Left View of BT](#p17--right--left-view-of-bt)
- [P18 — Print Root to Leaf Path](#p18--print-root-to-leaf-path)
- [P19 — LCA in BT](#p19--lca-in-bt)
- [P20 — Maximum Width of BT](#p20--maximum-width-of-bt)
- [P21 — All Nodes at Distance K in BT](#p21--all-nodes-at-distance-k-in-bt)
- [P22 — Minimum Time to Burn BT from a Node](#p22--minimum-time-to-burn-bt-from-a-node)
- [P23 — Count Total Nodes in a Complete BT](#p23--count-total-nodes-in-a-complete-bt)

#### Construction Problems
- [P24 — Requirements to Construct a Unique BT](#p24--requirements-to-construct-a-unique-bt)
- [P25 — Construct BT from Preorder and Inorder](#p25--construct-bt-from-preorder-and-inorder)
- [P26 — Construct BT from Postorder and Inorder](#p26--construct-bt-from-postorder-and-inorder)
- [P27 — Serialize and Deserialize BT](#p27--serialize-and-deserialize-bt)

#### Traversal in Constant Space
- [P28 — Morris Inorder Traversal](#p28--morris-inorder-traversal)
- [P29 — Morris Preorder Traversal](#p29--morris-preorder-traversal)

### Code with Pratush — Extra

#### Mirror and Symmetry
- [P30 — Invert Binary Tree](#p30--invert-binary-tree)
- [P31 — Subtree of Another Tree](#p31--subtree-of-another-tree)
- [P32 — Flip Equivalent Binary Trees](#p32--flip-equivalent-binary-trees)

#### Validation
- [P33 — Minimum Depth of Binary Tree](#p33--minimum-depth-of-binary-tree)
- [P34 — Binary Tree Tilt](#p34--binary-tree-tilt)
- [P35 — Check Completeness of Binary Tree](#p35--check-completeness-of-binary-tree)
- [P36 — Recover BST](#p36--recover-bst)

#### Search
- [P37 — LCA of Deepest Leaves](#p37--lca-of-deepest-leaves)

#### Path Sum
- [P38 — Path Sum](#p38--path-sum)
- [P39 — Path Sum II](#p39--path-sum-ii)
- [P40 — Path Sum III](#p40--path-sum-iii)
- [P41 — Sum of Root to Leaf Numbers](#p41--sum-of-root-to-leaf-numbers)

#### Construction (Pratush Extra)
- [P42 — Construct BT from Preorder and Postorder](#p42--construct-bt-from-preorder-and-postorder)
- [P43 — Convert Sorted Array to BST](#p43--convert-sorted-array-to-bst)
- [P44 — Convert Sorted List to BST](#p44--convert-sorted-list-to-bst)

### Binary Search Tree

#### Theory and Basics
- [P45 — Introduction to BST + Search in BST](#p45--introduction-to-bst--search-in-bst)
- [P46 — Floor and Ceil in a BST](#p46--floor-and-ceil-in-a-bst)

#### Medium
- [P47 — Insert a Node in BST](#p47--insert-a-node-in-bst)
- [P48 — Delete a Node in BST](#p48--delete-a-node-in-bst)
- [P49 — Kth Smallest and Largest in BST](#p49--kth-smallest-and-largest-in-bst)
- [P50 — Check if a Tree is a BST](#p50--check-if-a-tree-is-a-bst)
- [P51 — LCA in BST](#p51--lca-in-bst)
- [P52 — Construct BST from Preorder Traversal](#p52--construct-bst-from-preorder-traversal)
- [P53 — Inorder Successor and Predecessor in BST](#p53--inorder-successor-and-predecessor-in-bst)

#### FAQs
- [P54 — BST Iterator](#p54--bst-iterator)
- [P55 — Two Sum in BST](#p55--two-sum-in-bst)
- [P56 — Correct BST with Two Nodes Swapped](#p56--correct-bst-with-two-nodes-swapped)
- [P57 — Largest BST in Binary Tree](#p57--largest-bst-in-binary-tree)

---

## Binary Tree

---

## Tree Traversal

---

### P1 — Inorder Traversal
**LeetCode #94 | Difficulty: Easy | Source: Striver + Pratush**

> Return inorder traversal (Left → Root → Right) of a binary tree.

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

### P2 — Preorder Traversal
**LeetCode #144 | Difficulty: Easy | Source: Striver + Pratush**

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
    res.add(node.val);
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

### P3 — Postorder Traversal
**LeetCode #145 | Difficulty: Easy | Source: Striver + Pratush**

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
    res.add(node.val);
}

// Iterative (reverse of modified preorder)
public List<Integer> postorderIterative(TreeNode root) {
    LinkedList<Integer> res = new LinkedList<>();
    if (root == null) return res;
    Deque<TreeNode> stack = new ArrayDeque<>();
    stack.push(root);
    while (!stack.isEmpty()) {
        TreeNode node = stack.pop();
        res.addFirst(node.val);
        if (node.left  != null) stack.push(node.left);
        if (node.right != null) stack.push(node.right);
    }
    return res;
}
```

---

### P4 — Level Order Traversal
**LeetCode #102 | Difficulty: Medium | Source: Striver + Pratush**

> Return nodes level by level (BFS).

#### Java code

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> res = new ArrayList<>();
    if (root == null) return res;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    while (!q.isEmpty()) {
        int size = q.size();                    // snapshot — critical!
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

### P5 — Pre + Post + Inorder in One Traversal
**No LeetCode | Difficulty: Medium | Source: Striver**

> Print all three traversals in a single DFS pass using a state variable per node.

#### Core insight

Each node is visited 3 times using a stack of `(node, state)`:
- state=1 → preorder visit, go left
- state=2 → inorder visit, go right
- state=3 → postorder visit, pop

#### Java code

```java
public void allTraversals(TreeNode root) {
    List<Integer> pre = new ArrayList<>(), in = new ArrayList<>(), post = new ArrayList<>();
    Deque<Object[]> st = new ArrayDeque<>();
    if (root != null) st.push(new Object[]{root, 1});

    while (!st.isEmpty()) {
        Object[] top  = st.peek();
        TreeNode node = (TreeNode) top[0];
        int state     = (int) top[1];

        if (state == 1) {
            pre.add(node.val);          // preorder: first visit
            top[1] = 2;
            if (node.left  != null) st.push(new Object[]{node.left, 1});
        } else if (state == 2) {
            in.add(node.val);           // inorder: second visit
            top[1] = 3;
            if (node.right != null) st.push(new Object[]{node.right, 1});
        } else {
            post.add(node.val);         // postorder: third visit
            st.pop();
        }
    }
    System.out.println("Pre:  " + pre);
    System.out.println("In:   " + in);
    System.out.println("Post: " + post);
}
```

#### Example

```
    1
   / \
  2   3
 / \
4   5

Pre:  [1, 2, 4, 5, 3]
In:   [4, 2, 5, 1, 3]
Post: [4, 5, 2, 3, 1]
```

---

## Medium Problems

---

### P6 — Maximum Depth in BT
**LeetCode #104 | Difficulty: Easy | Source: Striver + Pratush**

> Find the maximum depth (height) of a binary tree.

#### Java code

```java
public int maxDepth(TreeNode root) {
    if (root == null) return 0;
    return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
```

---

### P7 — Check if Two Trees are Identical
**LeetCode #100 | Difficulty: Easy | Source: Striver + Pratush**

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

### P8 — Check for Balanced Binary Tree
**LeetCode #110 | Difficulty: Easy | Source: Striver + Pratush**

> Check if a binary tree is height-balanced (left and right heights differ by at most 1 at every node).

#### Core insight

Return `-1` to signal "unbalanced" — single pass bottom-up, no recomputing heights.

#### Java code

```java
public boolean isBalanced(TreeNode root) {
    return checkHeight(root) != -1;
}

private int checkHeight(TreeNode node) {
    if (node == null) return 0;
    int left  = checkHeight(node.left);
    int right = checkHeight(node.right);
    if (left == -1 || right == -1)       return -1;  // propagate
    if (Math.abs(left - right) > 1)      return -1;  // unbalanced here
    return 1 + Math.max(left, right);
}
```

---

### P9 — Diameter of Binary Tree
**LeetCode #543 | Difficulty: Easy | Source: Striver + Pratush**

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
    diameter = Math.max(diameter, left + right);  // path through this node
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
diameter = 3 (4→2→1→3) ✓
```

---

### P10 — Maximum Path Sum
**LeetCode #124 | Difficulty: Hard | Source: Striver + Pratush**

> Find the maximum path sum where the path can start and end at any node.

#### Core insight

At each node: update global max using BOTH children. But return only ONE side to parent (path cannot fork upward).

#### Java code

```java
private int maxSum = Integer.MIN_VALUE;

public int maxPathSum(TreeNode root) {
    dfs(root);
    return maxSum;
}

private int dfs(TreeNode node) {
    if (node == null) return 0;
    int left  = Math.max(0, dfs(node.left));   // ignore negative branches
    int right = Math.max(0, dfs(node.right));
    maxSum = Math.max(maxSum, left + node.val + right);  // global: both sides
    return node.val + Math.max(left, right);             // return: one side only
}
```

#### Example

```
    -10
    /  \
   9   20
      /  \
     15   7
Max path: 15→20→7 = 42 ✓
```

---

### P11 — Check for Symmetrical BTs
**LeetCode #101 | Difficulty: Easy | Source: Striver + Pratush**

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

## FAQs

---

### P12 — Zigzag / Spiral Traversal
**LeetCode #103 | Difficulty: Medium | Source: Striver + Pratush**

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
            else             level.addFirst(node.val);
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

### P13 — Boundary Traversal
**GeeksforGeeks | Difficulty: Medium | Source: Striver**

> Print: left boundary (top-down, no leaves) + all leaves (L→R) + right boundary (bottom-up, no leaves).

#### Java code

```java
public List<Integer> boundaryOfBinaryTree(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    if (root == null) return res;
    if (!isLeaf(root)) res.add(root.val);
    addLeftBoundary(root.left, res);
    addLeaves(root, res);
    addRightBoundary(root.right, res);
    return res;
}

private void addLeftBoundary(TreeNode node, List<Integer> res) {
    if (node == null || isLeaf(node)) return;
    res.add(node.val);
    if (node.left != null) addLeftBoundary(node.left,  res);
    else                   addLeftBoundary(node.right, res);
}

private void addLeaves(TreeNode node, List<Integer> res) {
    if (node == null) return;
    if (isLeaf(node)) { res.add(node.val); return; }
    addLeaves(node.left, res);
    addLeaves(node.right, res);
}

private void addRightBoundary(TreeNode node, List<Integer> res) {
    if (node == null || isLeaf(node)) return;
    if (node.right != null) addRightBoundary(node.right, res);
    else                    addRightBoundary(node.left,  res);
    res.add(node.val);   // add after recursion = bottom-up
}

private boolean isLeaf(TreeNode n) {
    return n.left == null && n.right == null;
}
```

#### Example

```
        1
       / \
      2   3
     / \ / \
    4  5 6  7
Boundary: [1, 2, 4, 5, 6, 7, 3] ✓
```

---

### P14 — Vertical Order Traversal
**LeetCode #987 | Difficulty: Hard | Source: Striver**

> Return nodes column by column. Within same column and row, sort by value.

#### Core insight

BFS with `(node, row, col)`. Group by col → TreeMap. Within same col+row, sort by value → PriorityQueue.

#### Java code

```java
public List<List<Integer>> verticalTraversal(TreeNode root) {
    TreeMap<Integer, TreeMap<Integer, PriorityQueue<Integer>>> map = new TreeMap<>();
    Queue<Object[]> q = new LinkedList<>();
    q.offer(new Object[]{root, 0, 0});   // node, row, col

    while (!q.isEmpty()) {
        Object[] curr = q.poll();
        TreeNode node = (TreeNode) curr[0];
        int row = (int) curr[1], col = (int) curr[2];

        map.computeIfAbsent(col, k -> new TreeMap<>())
           .computeIfAbsent(row, k -> new PriorityQueue<>())
           .offer(node.val);

        if (node.left  != null) q.offer(new Object[]{node.left,  row+1, col-1});
        if (node.right != null) q.offer(new Object[]{node.right, row+1, col+1});
    }

    List<List<Integer>> res = new ArrayList<>();
    for (TreeMap<Integer, PriorityQueue<Integer>> colMap : map.values()) {
        List<Integer> col = new ArrayList<>();
        for (PriorityQueue<Integer> pq : colMap.values())
            while (!pq.isEmpty()) col.add(pq.poll());
        res.add(col);
    }
    return res;
}
```

#### Example

```
      3
     / \
    9  20
       / \
      15   7

Output: [[9],[3,15],[20],[7]] ✓
```

---

### P15 — Top View of BT
**GeeksforGeeks | Difficulty: Medium | Source: Striver**

> For each horizontal distance (HD), print the FIRST node seen (shallowest level).

#### Java code

```java
public List<Integer> topView(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    if (root == null) return res;
    TreeMap<Integer, Integer> map = new TreeMap<>();
    Queue<Object[]> q = new LinkedList<>();
    q.offer(new Object[]{root, 0});

    while (!q.isEmpty()) {
        Object[] curr = q.poll();
        TreeNode node = (TreeNode) curr[0];
        int hd = (int) curr[1];

        map.putIfAbsent(hd, node.val);   // first node at HD = top view

        if (node.left  != null) q.offer(new Object[]{node.left,  hd - 1});
        if (node.right != null) q.offer(new Object[]{node.right, hd + 1});
    }
    res.addAll(map.values());
    return res;
}
```

#### Example

```
         1  (hd=0)
        / \
       2   3    (hd=-1, hd=1)
      / \   \
     4   5   6  (hd=-2, hd=0, hd=2)

Top view: [4, 2, 1, 3, 6]
(hd=0 → 1 stays, 5 is below it so ignored)
```

---

### P16 — Bottom View of BT
**GeeksforGeeks | Difficulty: Medium | Source: Striver**

> For each horizontal distance (HD), print the LAST (deepest) node seen.

#### Java code

```java
public List<Integer> bottomView(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    if (root == null) return res;
    TreeMap<Integer, Integer> map = new TreeMap<>();
    Queue<Object[]> q = new LinkedList<>();
    q.offer(new Object[]{root, 0});

    while (!q.isEmpty()) {
        Object[] curr = q.poll();
        TreeNode node = (TreeNode) curr[0];
        int hd = (int) curr[1];

        map.put(hd, node.val);   // overwrite = deepest node wins

        if (node.left  != null) q.offer(new Object[]{node.left,  hd - 1});
        if (node.right != null) q.offer(new Object[]{node.right, hd + 1});
    }
    res.addAll(map.values());
    return res;
}
```

#### Example

```
         1  (hd=0)
        / \
       2   3    (hd=-1, hd=1)
      / \   \
     4   5   6  (hd=-2, hd=0, hd=2)

Bottom view: [4, 2, 5, 3, 6]
(hd=0 → 5 overwrites 1)
```

---

### P17 — Right / Left View of BT
**LeetCode #199 | Difficulty: Medium | Source: Striver**

> Right view: last node of each level. Left view: first node of each level.

#### Java code

```java
// Right View
public List<Integer> rightSideView(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    if (root == null) return res;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    while (!q.isEmpty()) {
        int size = q.size();
        for (int i = 0; i < size; i++) {
            TreeNode node = q.poll();
            if (i == size - 1) res.add(node.val);   // last = rightmost
            if (node.left  != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
    }
    return res;
}

// Left View: change  i == size - 1  →  i == 0
```

#### Example

```
      1         ← 1
     / \
    2   3       ← 3
     \
      5         ← 5
Right view: [1, 3, 5] ✓
```

---

### P18 — Print Root to Leaf Path
**LeetCode #257 | Difficulty: Easy | Source: Striver**

> Print all root-to-leaf paths.

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
    if (node.left == null && node.right == null) {
        res.add(path);
        return;
    }
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

### P19 — LCA in BT
**LeetCode #236 | Difficulty: Medium | Source: Striver + Pratush**

> Find Lowest Common Ancestor in a general binary tree.

#### Core insight

Post-order DFS. If both left and right return non-null → current node is LCA.

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
LCA(5, 1) = 3 ✓
LCA(5, 4) = 5 ✓
```

---

### P20 — Maximum Width of BT
**LeetCode #662 | Difficulty: Medium | Source: Striver**

> Find the maximum width of any level (including null gaps between nodes).

#### Core insight

Assign index to each node: root=0, left=2*i, right=2*i+1. Width = rightmost - leftmost + 1. Normalize indices each level to prevent overflow.

#### Java code

```java
public int widthOfBinaryTree(TreeNode root) {
    Queue<TreeNode> nodes = new LinkedList<>();
    Queue<Long>   indices = new LinkedList<>();
    nodes.offer(root);
    indices.offer(0L);
    int maxWidth = 0;

    while (!nodes.isEmpty()) {
        int size = nodes.size();
        long left = indices.peek(), right = left;

        for (int i = 0; i < size; i++) {
            TreeNode node = nodes.poll();
            long idx = indices.poll() - left;   // normalize
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

### P21 — All Nodes at Distance K in BT
**LeetCode #863 | Difficulty: Medium | Source: Striver**

> Find all nodes at distance K from a target node.

#### Core insight

Build a parent map → BFS from target treating tree as undirected graph.

#### Java code

```java
public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
    Map<TreeNode, TreeNode> parent = new HashMap<>();
    buildParentMap(root, null, parent);

    Set<TreeNode> visited = new HashSet<>();
    Queue<TreeNode> q = new LinkedList<>();
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
            for (TreeNode next : new TreeNode[]{node.left, node.right, parent.get(node)}) {
                if (next != null && !visited.contains(next)) {
                    visited.add(next);
                    q.offer(next);
                }
            }
        }
        dist++;
    }
    return new ArrayList<>();
}

private void buildParentMap(TreeNode node, TreeNode par, Map<TreeNode, TreeNode> parent) {
    if (node == null) return;
    if (par != null) parent.put(node, par);
    buildParentMap(node.left,  node, parent);
    buildParentMap(node.right, node, parent);
}
```

---

### P22 — Minimum Time to Burn BT from a Node
**GeeksforGeeks | Difficulty: Hard | Source: Striver**

> Fire starts at target node, spreads to adjacent nodes each second. Find total time to burn the tree.

#### Core insight

Build parent map → BFS from target as undirected graph. Count levels until all nodes visited.

#### Java code

```java
public int minTimeToBurn(TreeNode root, int target) {
    Map<TreeNode, TreeNode> parent = new HashMap<>();
    TreeNode targetNode = buildParentMap(root, target, parent);

    Set<TreeNode> visited = new HashSet<>();
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(targetNode);
    visited.add(targetNode);
    int time = 0;

    while (!q.isEmpty()) {
        int size = q.size();
        boolean spread = false;
        for (int i = 0; i < size; i++) {
            TreeNode node = q.poll();
            for (TreeNode next : new TreeNode[]{node.left, node.right, parent.get(node)}) {
                if (next != null && !visited.contains(next)) {
                    visited.add(next); q.offer(next); spread = true;
                }
            }
        }
        if (spread) time++;
    }
    return time;
}

private TreeNode buildParentMap(TreeNode root, int target, Map<TreeNode, TreeNode> parent) {
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    TreeNode targetNode = null;
    while (!q.isEmpty()) {
        TreeNode node = q.poll();
        if (node.val == target) targetNode = node;
        if (node.left  != null) { parent.put(node.left,  node); q.offer(node.left);  }
        if (node.right != null) { parent.put(node.right, node); q.offer(node.right); }
    }
    return targetNode;
}
```

#### Example

```
       1
      / \
     2   3
    / \
   4   5
Target=2: t=0:{2}, t=1:{4,5,1}, t=2:{3} → answer=2 ✓
```

---

### P23 — Count Total Nodes in a Complete BT
**LeetCode #222 | Difficulty: Medium | Source: Striver**

> Count nodes in O(log²n) using the complete BT property.

#### Core insight

Find left height and right height. If equal → perfect subtree → `2^h - 1`. Else recurse both sides.

#### Java code

```java
public int countNodes(TreeNode root) {
    if (root == null) return 0;
    int leftH = 0, rightH = 0;
    TreeNode l = root, r = root;
    while (l != null) { leftH++;  l = l.left;  }
    while (r != null) { rightH++; r = r.right; }
    if (leftH == rightH) return (1 << leftH) - 1;   // perfect BT: 2^h - 1
    return 1 + countNodes(root.left) + countNodes(root.right);
}
```

#### Example

```
        1
       / \
      2   3
     / \  /
    4   5 6
leftH=3, rightH=2 → not equal → recurse → total=6 ✓
```

---

## Construction Problems

---

### P24 — Requirements to Construct a Unique BT
**Theory | Source: Striver**

> Which pairs of traversals can uniquely reconstruct a binary tree?

#### Key rules

```
Inorder + Preorder   → UNIQUE tree ✓
Inorder + Postorder  → UNIQUE tree ✓
Inorder + Level Order→ UNIQUE tree ✓

Preorder + Postorder → NOT unique (multiple trees possible)
Only Preorder alone  → NOT unique
Only Postorder alone → NOT unique
Only Inorder alone   → NOT unique

WHY: Inorder splits the tree into left/right subtrees.
     Without inorder, we can't determine the split point.
```

---

### P25 — Construct BT from Preorder and Inorder
**LeetCode #105 | Difficulty: Medium | Source: Striver + Pratush**

> Reconstruct binary tree given preorder and inorder arrays.

#### Core insight

`preorder[0]` = root. Find root in inorder → left subtree size = `mid - inStart`. Use HashMap for O(1) inorder lookup.

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
preorder=[3,9,20,15,7], inorder=[9,3,15,20,7]
root=3, left=[9], right=[20,15,7]
Output:    3
          / \
         9  20
           /  \
          15   7  ✓
```

---

### P26 — Construct BT from Postorder and Inorder
**LeetCode #106 | Difficulty: Medium | Source: Striver + Pratush**

> Reconstruct binary tree given inorder and postorder arrays.

#### Core insight

`postorder[last]` = root. Build right subtree FIRST (postorder reads R before Root).

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
    root.right = build(postorder, mid + 1, inRight);  // right FIRST
    root.left  = build(postorder, inLeft,  mid - 1);
    return root;
}
```

---

### P27 — Serialize and Deserialize BT
**LeetCode #297 | Difficulty: Hard | Source: Striver + Pratush**

> Design serialize (tree → string) and deserialize (string → tree).

#### Core insight

Preorder DFS with "null" markers. Deserialize reads values from a queue and rebuilds recursively.

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
Tree:    1
        / \
       2   3
          / \
         4   5
Serialized: "1,2,null,null,3,4,null,null,5,null,null"
Rebuilds original tree ✓
```

---

## Traversal in Constant Space

---

### P28 — Morris Inorder Traversal
**No LeetCode | Difficulty: Medium | Source: Striver**

> Inorder traversal in O(1) space — no stack, no recursion.

#### Core insight

Thread the tree: for each node, find its inorder predecessor and link predecessor's right → current node. On second visit, unlink and visit.

#### Java code

```java
public List<Integer> morrisInorder(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    TreeNode curr = root;

    while (curr != null) {
        if (curr.left == null) {
            res.add(curr.val);   // no left: visit and move right
            curr = curr.right;
        } else {
            TreeNode pred = curr.left;
            while (pred.right != null && pred.right != curr)
                pred = pred.right;

            if (pred.right == null) {
                pred.right = curr;   // create thread
                curr = curr.left;
            } else {
                pred.right = null;   // remove thread
                res.add(curr.val);   // VISIT on second encounter (inorder)
                curr = curr.right;
            }
        }
    }
    return res;
}
```

---

### P29 — Morris Preorder Traversal
**No LeetCode | Difficulty: Medium | Source: Striver**

> Preorder traversal in O(1) space using Morris threading.

#### Core insight

Same as Morris Inorder but **visit node on FIRST encounter** (before going left).

#### Java code

```java
public List<Integer> morrisPreorder(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    TreeNode curr = root;

    while (curr != null) {
        if (curr.left == null) {
            res.add(curr.val);   // no left: visit and move right
            curr = curr.right;
        } else {
            TreeNode pred = curr.left;
            while (pred.right != null && pred.right != curr)
                pred = pred.right;

            if (pred.right == null) {
                res.add(curr.val);   // VISIT on first encounter (preorder)
                pred.right = curr;
                curr = curr.left;
            } else {
                pred.right = null;   // remove thread (don't visit again)
                curr = curr.right;
            }
        }
    }
    return res;
}
```

---

## Code with Pratush — Extra

---

## Mirror and Symmetry

---

### P30 — Invert Binary Tree
**LeetCode #226 | Difficulty: Easy | Source: Pratush**

> Invert (mirror) a binary tree.

#### Java code

```java
public TreeNode invertTree(TreeNode root) {
    if (root == null) return null;
    TreeNode tmp  = root.left;
    root.left     = invertTree(root.right);
    root.right    = invertTree(tmp);
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

### P31 — Subtree of Another Tree
**LeetCode #572 | Difficulty: Medium | Source: Pratush**

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
    return p.val == q.val
        && isSameTree(p.left,  q.left)
        && isSameTree(p.right, q.right);
}
```

---

### P32 — Flip Equivalent Binary Trees
**LeetCode #951 | Difficulty: Medium | Source: Pratush**

> Two trees are flip equivalent if one can be obtained by flipping (swapping children) some nodes.

#### Java code

```java
public boolean flipEquiv(TreeNode root1, TreeNode root2) {
    if (root1 == null && root2 == null) return true;
    if (root1 == null || root2 == null) return false;
    if (root1.val != root2.val) return false;
    boolean noFlip = flipEquiv(root1.left,  root2.left)
                  && flipEquiv(root1.right, root2.right);
    boolean flip   = flipEquiv(root1.left,  root2.right)
                  && flipEquiv(root1.right, root2.left);
    return noFlip || flip;
}
```

---

## Validation

---

### P33 — Minimum Depth of Binary Tree
**LeetCode #111 | Difficulty: Easy | Source: Pratush**

> Find the minimum depth (root to nearest leaf).

#### Core insight

Handle the case where one child is null — don't return 0 for that side (it's not a leaf path).

#### Java code

```java
public int minDepth(TreeNode root) {
    if (root == null) return 0;
    if (root.left == null && root.right == null) return 1;
    if (root.left  == null) return 1 + minDepth(root.right);
    if (root.right == null) return 1 + minDepth(root.left);
    return 1 + Math.min(minDepth(root.left), minDepth(root.right));
}
```

---

### P34 — Binary Tree Tilt
**LeetCode #563 | Difficulty: Easy | Source: Pratush**

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

### P35 — Check Completeness of Binary Tree
**LeetCode #958 | Difficulty: Medium | Source: Pratush**

> Check if a binary tree is complete (all levels full except possibly last, filled left to right).

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

### P36 — Recover BST
**LeetCode #99 | Difficulty: Hard | Source: Pratush**

> Two nodes of a BST are swapped by mistake. Fix the BST.

#### Core insight

Inorder of valid BST is strictly increasing. Find two out-of-order nodes and swap their values.

#### Java code

```java
TreeNode first = null, second = null, prev = null;

public void recoverTree(TreeNode root) {
    inorder(root);
    int tmp   = first.val;
    first.val = second.val;
    second.val = tmp;
}

private void inorder(TreeNode node) {
    if (node == null) return;
    inorder(node.left);
    if (prev != null && prev.val > node.val) {
        if (first == null) first = prev;
        second = node;
    }
    prev = node;
    inorder(node.right);
}
```

---

## Search

---

### P37 — LCA of Deepest Leaves
**LeetCode #1123 | Difficulty: Medium | Source: Pratush**

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
        return new Pair(node, left.depth + 1);   // equal depth → LCA here
    return left.depth > right.depth
        ? new Pair(left.node,  left.depth  + 1)
        : new Pair(right.node, right.depth + 1);
}
```

---

## Path Sum

---

### P38 — Path Sum
**LeetCode #112 | Difficulty: Easy | Source: Pratush**

> Check if there is a root-to-leaf path with sum equal to `targetSum`.

#### Java code

```java
public boolean hasPathSum(TreeNode root, int targetSum) {
    if (root == null) return false;
    if (root.left == null && root.right == null) return root.val == targetSum;
    int rem = targetSum - root.val;
    return hasPathSum(root.left, rem) || hasPathSum(root.right, rem);
}
```

---

### P39 — Path Sum II
**LeetCode #113 | Difficulty: Medium | Source: Pratush**

> Find all root-to-leaf paths where sum equals `targetSum`.

#### Java code

```java
public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
    List<List<Integer>> res = new ArrayList<>();
    dfs(root, targetSum, new ArrayList<>(), res);
    return res;
}

private void dfs(TreeNode node, int rem, List<Integer> path, List<List<Integer>> res) {
    if (node == null) return;
    path.add(node.val);
    if (node.left == null && node.right == null && rem == node.val)
        res.add(new ArrayList<>(path));   // copy — don't add reference
    dfs(node.left,  rem - node.val, path, res);
    dfs(node.right, rem - node.val, path, res);
    path.remove(path.size() - 1);        // backtrack
}
```

---

### P40 — Path Sum III
**LeetCode #437 | Difficulty: Medium | Source: Pratush**

> Count paths (any node to any node, going downward) where sum equals `targetSum`.

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

---

### P41 — Sum of Root to Leaf Numbers
**LeetCode #129 | Difficulty: Medium | Source: Pratush**

> Each root-to-leaf path forms a number. Return total sum of all such numbers.

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
Paths: 12 + 13 = 25 ✓
```

---

## Construction (Pratush Extra)

---

### P42 — Construct BT from Preorder and Postorder
**LeetCode #889 | Difficulty: Medium | Source: Pratush**

> Reconstruct binary tree from preorder and postorder (result may not be unique).

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
    int leftRootVal = preorder[preIdx];
    int leftSize = postMap.get(leftRootVal) - postLeft + 1;
    root.left  = build(preorder, postLeft, postLeft + leftSize - 1);
    root.right = build(preorder, postLeft + leftSize, postRight - 1);
    return root;
}
```

---

### P43 — Convert Sorted Array to BST
**LeetCode #108 | Difficulty: Easy | Source: Pratush**

> Convert a sorted array to a height-balanced BST.

#### Java code

```java
public TreeNode sortedArrayToBST(int[] nums) {
    return build(nums, 0, nums.length - 1);
}

private TreeNode build(int[] nums, int left, int right) {
    if (left > right) return null;
    int mid = left + (right - left) / 2;
    TreeNode root = new TreeNode(nums[mid]);
    root.left  = build(nums, left,  mid - 1);
    root.right = build(nums, mid + 1, right);
    return root;
}
```

#### Example

```
nums = [-10,-3,0,5,9]  →  mid=0 (root)
Output:    0
          / \
        -3   9
        /   /
      -10  5  ✓
```

---

### P44 — Convert Sorted List to BST
**LeetCode #109 | Difficulty: Medium | Source: Pratush**

> Convert a sorted linked list to a height-balanced BST.

#### Java code

```java
public TreeNode sortedListToBST(ListNode head) {
    if (head == null) return null;
    if (head.next == null) return new TreeNode(head.val);

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

## Binary Search Tree

---

## Theory and Basics

---

### P45 — Introduction to BST + Search in BST
**LeetCode #700 | Difficulty: Easy | Source: Striver + Pratush**

> BST property: left subtree < root < right subtree. Search using this property in O(h).

#### Key properties

```
BST Property:   left < root < right  (for every node)
Inorder of BST: gives sorted (ascending) order
Search:         O(log n) average, O(n) worst (skewed)
Insert:         O(log n) average
Delete:         O(log n) average
```

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

### P46 — Floor and Ceil in a BST
**GeeksforGeeks | Difficulty: Medium | Source: Striver**

> Floor = largest value ≤ target. Ceil = smallest value ≥ target.

#### Java code

```java
public int floorBST(TreeNode root, int target) {
    int floor = -1;
    while (root != null) {
        if (root.val == target) return root.val;
        if (root.val < target) { floor = root.val; root = root.right; }
        else root = root.left;
    }
    return floor;
}

public int ceilBST(TreeNode root, int target) {
    int ceil = -1;
    while (root != null) {
        if (root.val == target) return root.val;
        if (root.val > target) { ceil = root.val; root = root.left; }
        else root = root.right;
    }
    return ceil;
}
```

#### Example

```
BST:    8
       / \
      4  12
     / \
    2   6
floor(5) → 4,  ceil(5) → 6 ✓
```

---

## BST — Medium

---

### P47 — Insert a Node in BST
**LeetCode #701 | Difficulty: Medium | Source: Striver**

> Insert a value into a BST. Return updated root.

#### Java code

```java
public TreeNode insertIntoBST(TreeNode root, int val) {
    if (root == null) return new TreeNode(val);   // found insertion point
    if (val < root.val) root.left  = insertIntoBST(root.left,  val);
    else                root.right = insertIntoBST(root.right, val);
    return root;
}
```

---

### P48 — Delete a Node in BST
**LeetCode #450 | Difficulty: Medium | Source: Striver**

> Delete a node with given key from BST.

#### Core insight

3 cases: (1) leaf → remove, (2) one child → replace, (3) two children → replace value with inorder successor (min of right subtree) then delete successor.

#### Java code

```java
public TreeNode deleteNode(TreeNode root, int key) {
    if (root == null) return null;
    if (key < root.val)       root.left  = deleteNode(root.left,  key);
    else if (key > root.val)  root.right = deleteNode(root.right, key);
    else {
        if (root.left  == null) return root.right;
        if (root.right == null) return root.left;
        TreeNode succ = root.right;
        while (succ.left != null) succ = succ.left;
        root.val   = succ.val;
        root.right = deleteNode(root.right, succ.val);
    }
    return root;
}
```

---

### P49 — Kth Smallest and Largest in BST
**LeetCode #230 | GFG | Difficulty: Medium | Source: Striver + Pratush**

> Kth smallest: inorder (L→Root→R). Kth largest: reverse inorder (R→Root→L).

#### Java code

```java
private int k, result;

// Kth Smallest
public int kthSmallest(TreeNode root, int k) {
    this.k = k;
    inorder(root);
    return result;
}
private void inorder(TreeNode node) {
    if (node == null || k == 0) return;
    inorder(node.left);
    if (--k == 0) { result = node.val; return; }
    inorder(node.right);
}

// Kth Largest — reverse inorder
public int kthLargest(TreeNode root, int k) {
    this.k = k;
    reverseInorder(root);
    return result;
}
private void reverseInorder(TreeNode node) {
    if (node == null || k == 0) return;
    reverseInorder(node.right);   // go right first
    if (--k == 0) { result = node.val; return; }
    reverseInorder(node.left);
}
```

---

### P50 — Check if a Tree is a BST
**LeetCode #98 | Difficulty: Medium | Source: Striver + Pratush**

> Determine if a binary tree is a valid BST.

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

---

### P51 — LCA in BST
**LeetCode #235 | Difficulty: Medium | Source: Striver + Pratush**

> Find LCA in BST using BST property.

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

### P52 — Construct BST from Preorder Traversal
**LeetCode #1008 | Difficulty: Medium | Source: Striver**

> Given preorder traversal of a BST, reconstruct the BST.

#### Core insight

Use upper bound: nodes greater than current bound belong to right subtree of some ancestor.

#### Java code

```java
int idx = 0;

public TreeNode bstFromPreorder(int[] preorder) {
    return build(preorder, Integer.MAX_VALUE);
}

private TreeNode build(int[] preorder, int bound) {
    if (idx == preorder.length || preorder[idx] > bound) return null;
    TreeNode root = new TreeNode(preorder[idx++]);
    root.left  = build(preorder, root.val);   // left subtree: values < root
    root.right = build(preorder, bound);      // right subtree: values < bound
    return root;
}
```

---

### P53 — Inorder Successor and Predecessor in BST
**GeeksforGeeks | Difficulty: Medium | Source: Striver**

> Find inorder successor (next larger) and predecessor (next smaller) of a given node.

#### Java code

```java
// Inorder Successor
public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
    TreeNode successor = null;
    while (root != null) {
        if (p.val < root.val) { successor = root; root = root.left; }
        else root = root.right;
    }
    return successor;
}

// Inorder Predecessor
public TreeNode inorderPredecessor(TreeNode root, TreeNode p) {
    TreeNode predecessor = null;
    while (root != null) {
        if (p.val > root.val) { predecessor = root; root = root.right; }
        else root = root.left;
    }
    return predecessor;
}
```

---

## BST — FAQs

---

### P54 — BST Iterator
**LeetCode #173 | Difficulty: Medium | Source: Striver**

> Iterator over BST giving next smallest element in O(1) average, O(h) space.

#### Java code

```java
class BSTIterator {
    private Deque<TreeNode> stack = new ArrayDeque<>();

    public BSTIterator(TreeNode root) { pushLeft(root); }

    public int next() {
        TreeNode node = stack.pop();
        pushLeft(node.right);   // process right subtree's leftmost path
        return node.val;
    }

    public boolean hasNext() { return !stack.isEmpty(); }

    private void pushLeft(TreeNode node) {
        while (node != null) { stack.push(node); node = node.left; }
    }
}
```

---

### P55 — Two Sum in BST
**LeetCode #653 | Difficulty: Easy | Source: Striver + Pratush**

> Find if two elements in BST sum to k.

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

### P56 — Correct BST with Two Nodes Swapped
**LeetCode #99 | Difficulty: Hard | Source: Striver + Pratush**

> Two nodes of a BST are swapped by mistake. Fix the BST without changing structure.

#### Java code

```java
TreeNode first = null, second = null, prev = null;

public void recoverTree(TreeNode root) {
    inorder(root);
    int tmp    = first.val;
    first.val  = second.val;
    second.val = tmp;
}

private void inorder(TreeNode node) {
    if (node == null) return;
    inorder(node.left);
    if (prev != null && prev.val > node.val) {
        if (first == null) first = prev;
        second = node;
    }
    prev = node;
    inorder(node.right);
}
```

---

### P57 — Largest BST in Binary Tree
**LeetCode #333 | Difficulty: Hard | Source: Striver**

> Find the size of the largest subtree which is also a BST.

#### Core insight

Bottom-up DFS. Each call returns `{size, min, max}`. Return size=-1 if not a BST.

#### Java code

```java
private int maxSize = 0;

public int largestBSTSubtree(TreeNode root) {
    dfs(root);
    return maxSize;
}

private int[] dfs(TreeNode node) {   // returns {size, min, max}
    if (node == null) return new int[]{0, Integer.MAX_VALUE, Integer.MIN_VALUE};

    int[] left  = dfs(node.left);
    int[] right = dfs(node.right);

    if (left[0] != -1 && right[0] != -1
            && node.val > left[2] && node.val < right[1]) {
        int size = left[0] + right[0] + 1;
        maxSize = Math.max(maxSize, size);
        return new int[]{size, Math.min(node.val, left[1]), Math.max(node.val, right[2])};
    }
    return new int[]{-1, 0, 0};   // not a BST
}
```

#### Example

```
        10
       /  \
      5   15
     / \    \
    1   8   7

Largest BST: subtree at 5 → [1,5,8], size=3 ✓
```

