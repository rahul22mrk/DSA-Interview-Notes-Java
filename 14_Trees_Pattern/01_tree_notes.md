# Tree Pattern — Complete Notes

> **Pattern family:** Binary Tree / BST / Tree Traversal / Construction
> **Difficulty range:** Easy → Hard
> **Language:** Java

---

## Table of Contents

1. [How to identify this pattern](#1-how-to-identify-this-pattern) ← **start here**
2. [What is this pattern?](#2-what-is-this-pattern)
3. [Core rules](#3-core-rules)
4. [2-Question framework](#4-2-question-framework)
5. [Variants table](#5-variants-table)
6. [Universal Java template](#6-universal-java-template)
7. [Quick reference cheatsheet](#7-quick-reference-cheatsheet)
8. [Common mistakes](#8-common-mistakes)
9. [Complexity summary](#9-complexity-summary)

---

## 1. How to identify this pattern

### Keyword scanner

| If you see this... | It means |
|--------------------|----------|
| "inorder / preorder / postorder traversal" | DFS traversal — recursive or iterative |
| "level order / BFS traversal" | BFS — queue-based level by level |
| "zigzag / spiral order" | BFS + direction flag per level |
| "invert / mirror / symmetric" | swap left and right children recursively |
| "lowest common ancestor" | LCA — path meeting point |
| "validate BST" | inorder must be strictly increasing |
| "path sum / root to leaf" | DFS with running sum |
| "maximum path sum" | DFS with local max, update global max on return |
| "construct tree from traversals" | preorder/inorder → find root, split, recurse |
| "serialize / deserialize tree" | BFS or preorder + null markers |
| "diameter / depth / balanced" | DFS returning height, check condition |
| "Kth smallest in BST" | inorder traversal = sorted order |
| "recover / validate BST" | find out-of-order nodes in inorder |
| "convert sorted array/list to BST" | binary mid as root, recurse halves |

### Brute force test

```
Brute force: collect all nodes → sort → answer.
→ O(n log n) time, O(n) space.
→ BST property gives O(log n) search for free — use it.
→ Tree structure = natural recursion → subproblem at every node.

Key insight: most tree problems decompose as:
  solve(root) = f(solve(root.left), solve(root.right), root.val)
This is the post-order return pattern — solve children first, combine at root.
```

### The 5 confirming signals

**Signal 1 — Input is a tree node / root**
> All tree problems start with `TreeNode root`. Recursion is almost always the right approach.

**Signal 2 — "Left and right" appear symmetrically in the problem**
> Invert, symmetric, same tree — swap/compare left and right at every node.

**Signal 3 — "Path" from root to leaf or any node to any node**
> Root-to-leaf: pass running sum down. Any-to-any: track max at each node, return single branch up.

**Signal 4 — BST + "search / insert / kth smallest / validate"**
> Use BST property: left < root < right. Inorder = sorted. No need to visit all nodes.

**Signal 5 — "Construct tree from" two traversal arrays**
> Preorder[0] = root. Find root in inorder → split into left/right subtrees. Recurse.

### Decision flowchart

```
Problem involves a Binary Tree?
        │
        ▼
What are you doing?
        │
        ├── VISIT all nodes in order → Traversal (DFS/BFS)
        │       ├── Inorder/Pre/Post     → DFS recursive or stack-based iterative
        │       └── Level order          → BFS with queue
        │
        ├── COMPARE or TRANSFORM structure → Mirror & Symmetry
        │       └── Invert, Same Tree, Symmetric, Subtree
        │
        ├── SEARCH or USE BST property → BST Operations
        │       └── Search, LCA of BST, Kth smallest, Validate, Recover
        │
        ├── CHECK a property → Validation & Properties
        │       └── Balanced, Diameter, Depth, Completeness, Tilt
        │
        ├── ACCUMULATE along a path → Path Sum
        │       └── Pass sum down (root→leaf) or return max up (any path)
        │
        └── BUILD a tree → Construction
                └── From traversals, sorted array/list, serialize/deserialize
```

---

## 2. What is this pattern?

**TreeNode structure:**
```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}
```

**Three core traversal orders:**
```
        1
       / \
      2   3
     / \
    4   5

Inorder  (L, Root, R): 4 2 5 1 3  ← BST gives sorted order
Preorder (Root, L, R): 1 2 4 5 3  ← root first → used for construction
Postorder(L, R, Root): 4 5 2 3 1  ← children before root → used for cleanup/height
Level order (BFS):     1 2 3 4 5  ← row by row
```

**Two fundamental recursive patterns:**

```java
// Pattern 1: TOP-DOWN (pass info down)
// Use when: parent needs to tell children something (running sum, bounds)
void dfs(TreeNode node, int param) {
    if (node == null) return;
    // use param at this node
    dfs(node.left,  newParam);
    dfs(node.right, newParam);
}

// Pattern 2: BOTTOM-UP (return info up)
// Use when: parent needs result from children first (height, max path)
int dfs(TreeNode node) {
    if (node == null) return base;
    int left  = dfs(node.left);
    int right = dfs(node.right);
    // combine left + right + node.val
    return result;
}
```

**BFS (Level Order):**
```java
Queue<TreeNode> q = new LinkedList<>();
q.offer(root);
while (!q.isEmpty()) {
    int size = q.size();             // snapshot of current level size
    for (int i = 0; i < size; i++) {
        TreeNode node = q.poll();
        if (node.left  != null) q.offer(node.left);
        if (node.right != null) q.offer(node.right);
    }
}
```

---

## 3. Core rules

**Rule 1 — Always handle `null` first**
```java
// WRONG — NullPointerException when node is null
int height(TreeNode node) {
    return 1 + Math.max(height(node.left), height(node.right));  // crashes on null

// CORRECT — base case first
int height(TreeNode node) {
    if (node == null) return 0;   // base case
    return 1 + Math.max(height(node.left), height(node.right));
}
```

**Rule 2 — For BST problems, use BST property (avoid full scan)**
```java
// WRONG — O(n) scan, ignores BST structure
boolean search(TreeNode root, int target) {
    if (root == null) return false;
    return search(root.left, target) || root.val == target || search(root.right, target);

// CORRECT — O(log n) using BST property
boolean search(TreeNode root, int target) {
    if (root == null) return false;
    if (root.val == target) return true;
    return target < root.val
        ? search(root.left, target)    // go left
        : search(root.right, target);  // go right
}
```

**Rule 3 — For "maximum path sum" use a global variable, return single branch**
```java
// The path can go through any node. At each node:
//   - update global max using BOTH branches (left + root + right)
//   - return only ONE branch up (can't take both directions to parent)
int maxSum = Integer.MIN_VALUE;

int dfs(TreeNode node) {
    if (node == null) return 0;
    int left  = Math.max(0, dfs(node.left));   // ignore negative branches
    int right = Math.max(0, dfs(node.right));
    maxSum = Math.max(maxSum, left + node.val + right);  // update global (both sides)
    return node.val + Math.max(left, right);             // return single side up
}
```

**Rule 4 — For construction from traversals, use a HashMap for inorder indices**
```java
// WRONG — O(n) search in inorder array for each root → O(n²) total
int rootIdx = 0;
for (int i = 0; i < inorder.length; i++)
    if (inorder[i] == root) { rootIdx = i; break; }

// CORRECT — O(1) lookup with HashMap → O(n) total
Map<Integer, Integer> inorderMap = new HashMap<>();
for (int i = 0; i < inorder.length; i++) inorderMap.put(inorder[i], i);
```

**Rule 5 — Use iterative inorder with stack for BST in-place operations**
```java
// Iterative inorder = Morris traversal alternative; clean with explicit stack
Deque<TreeNode> stack = new ArrayDeque<>();
TreeNode curr = root;
while (curr != null || !stack.isEmpty()) {
    while (curr != null) { stack.push(curr); curr = curr.left; }
    curr = stack.pop();
    // process curr here
    curr = curr.right;
}
```

---

## 4. 2-Question framework

### Question 1 — What are you doing at each node?

| Answer | Pattern |
|--------|---------|
| Visit in a specific order | Traversal (DFS/BFS) |
| Compare left and right subtrees | Mirror & Symmetry |
| Use left < root < right | BST Operations |
| Check height/balance/depth | Validation & Properties (bottom-up) |
| Accumulate along path | Path Sum (top-down or bottom-up) |
| Build the tree structure | Construction |

### Question 2 — Which direction does information flow?

| Direction | Pattern | Example |
|-----------|---------|---------|
| **Top-down** (parent → children) | Pass constraints/state down | Validate BST (pass min/max bounds), Path Sum (pass remaining sum) |
| **Bottom-up** (children → parent) | Return computed result up | Height, diameter, max path sum |
| **Both** | Combine results at every node | LCA (return node if found), balanced check |
| **Level by level** (BFS) | Process row by row | Level order, zigzag, check completeness |

> **Decision shortcut:**
> - "check / validate property" → bottom-up, return from children
> - "path from root" → top-down, pass running sum
> - "any path between two nodes" → bottom-up + global variable
> - "BST operation" → use left < root < right, O(log n)
> - "level by level" → BFS with queue, snapshot level size
> - "construct tree" → preorder root + inorder split

---

## 5. Variants table

> **Common core:** `TreeNode` with left/right children, recursive traversal
> **What differs:** traversal order, what you pass down, what you return up

| Variant | Direction | Data structure | Key operation | Return |
|---------|-----------|---------------|---------------|--------|
| Inorder / Pre / Post | DFS (bottom-up or top-down) | call stack | visit at right moment | void or list |
| Level Order | BFS | Queue | snapshot `q.size()` per level | list of lists |
| Zigzag | BFS | Queue + flag | reverse alternate levels | list of lists |
| Invert / Mirror | top-down | call stack | swap left/right | root |
| Same Tree / Symmetric | both-directions | call stack | compare pair of nodes | boolean |
| LCA Binary Tree | bottom-up | call stack | return node if found | TreeNode |
| LCA BST | top-down | — | use BST property | TreeNode |
| Validate BST | top-down | — | pass (min, max) bounds | boolean |
| Recover BST | inorder scan | two pointers | find swapped pair | void |
| Height / Depth | bottom-up | call stack | `1 + max(L, R)` | int |
| Diameter | bottom-up + global | global int | `L + R` at each node | int |
| Balanced | bottom-up | call stack | return -1 on imbalance | int (-1 or height) |
| Path Sum (root→leaf) | top-down | call stack | pass `sum - node.val` | boolean |
| Path Sum II | top-down | backtrack list | add/remove node | list of lists |
| Path Sum III | prefix sum + map | HashMap | `map.get(curr - target)` | int count |
| Max Path Sum | bottom-up + global | global int | update global, return one side | int |
| Construct from traversals | divide & conquer | HashMap | root in preorder, split inorder | TreeNode |
| Serialize / Deserialize | BFS or preorder | Queue/string | null markers | string / TreeNode |
| Kth Smallest BST | inorder | counter | stop at kth | int |

---

## 6. Universal Java template

```java
// ─── TEMPLATE A: DFS Traversals ──────────────────────────────────────────────
// Recursive
void inorder(TreeNode node, List<Integer> res) {
    if (node == null) return;
    inorder(node.left, res);
    res.add(node.val);       // ← move this line for pre/post order
    inorder(node.right, res);
}

// Iterative Inorder (interview-safe — no recursion stack overflow)
List<Integer> inorderIterative(TreeNode root) {
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


// ─── TEMPLATE B: BFS Level Order ─────────────────────────────────────────────
List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> res = new ArrayList<>();
    if (root == null) return res;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    while (!q.isEmpty()) {
        int size = q.size();                          // snapshot — critical!
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


// ─── TEMPLATE C: Bottom-Up (return height / property) ────────────────────────
int height(TreeNode node) {
    if (node == null) return 0;
    int left  = height(node.left);
    int right = height(node.right);
    return 1 + Math.max(left, right);
}


// ─── TEMPLATE D: Top-Down with bounds (Validate BST) ─────────────────────────
boolean isValidBST(TreeNode node, long min, long max) {
    if (node == null) return true;
    if (node.val <= min || node.val >= max) return false;
    return isValidBST(node.left,  min, node.val)
        && isValidBST(node.right, node.val, max);
}
// Call: isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE)


// ─── TEMPLATE E: Path Sum (top-down, root→leaf) ──────────────────────────────
boolean hasPathSum(TreeNode node, int target) {
    if (node == null) return false;
    if (node.left == null && node.right == null) return node.val == target;  // leaf
    return hasPathSum(node.left,  target - node.val)
        || hasPathSum(node.right, target - node.val);
}


// ─── TEMPLATE F: Max Path Sum (bottom-up + global) ───────────────────────────
int maxSum = Integer.MIN_VALUE;
int maxPathSum(TreeNode node) {
    if (node == null) return 0;
    int left  = Math.max(0, maxPathSum(node.left));   // ignore negative
    int right = Math.max(0, maxPathSum(node.right));
    maxSum = Math.max(maxSum, left + node.val + right); // update: can use both sides
    return node.val + Math.max(left, right);            // return: only one side
}


// ─── TEMPLATE G: LCA Binary Tree ─────────────────────────────────────────────
TreeNode lca(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q) return root;
    TreeNode left  = lca(root.left,  p, q);
    TreeNode right = lca(root.right, p, q);
    if (left != null && right != null) return root;  // p in one side, q in other
    return left != null ? left : right;              // both in same side
}


// ─── TEMPLATE H: Construct from Preorder + Inorder ───────────────────────────
Map<Integer, Integer> inorderMap = new HashMap<>();
int preIdx = 0;

TreeNode build(int[] preorder, int left, int right) {
    if (left > right) return null;
    int rootVal = preorder[preIdx++];
    TreeNode root = new TreeNode(rootVal);
    int mid = inorderMap.get(rootVal);
    root.left  = build(preorder, left, mid - 1);
    root.right = build(preorder, mid + 1, right);
    return root;
}


// ─── TEMPLATE I: Path Sum III (prefix sum) ───────────────────────────────────
int pathSumIII(TreeNode root, int target) {
    Map<Long, Integer> prefixCount = new HashMap<>();
    prefixCount.put(0L, 1);   // empty path
    return dfs(root, 0L, target, prefixCount);
}

int dfs(TreeNode node, long curr, int target, Map<Long, Integer> map) {
    if (node == null) return 0;
    curr += node.val;
    int count = map.getOrDefault(curr - target, 0);
    map.merge(curr, 1, Integer::sum);
    count += dfs(node.left,  curr, target, map);
    count += dfs(node.right, curr, target, map);
    map.merge(curr, -1, Integer::sum);   // backtrack
    return count;
}


// ─── TEMPLATE J: Serialize / Deserialize (Preorder + nulls) ──────────────────
public String serialize(TreeNode root) {
    if (root == null) return "null";
    return root.val + "," + serialize(root.left) + "," + serialize(root.right);
}

public TreeNode deserialize(String data) {
    Queue<String> q = new LinkedList<>(Arrays.asList(data.split(",")));
    return buildTree(q);
}

TreeNode buildTree(Queue<String> q) {
    String val = q.poll();
    if (val.equals("null")) return null;
    TreeNode node = new TreeNode(Integer.parseInt(val));
    node.left  = buildTree(q);
    node.right = buildTree(q);
    return node;
}


// ─── TEMPLATE K: Kth Smallest in BST ─────────────────────────────────────────
int k, result;
void kthSmallest(TreeNode node) {
    if (node == null) return;
    kthSmallest(node.left);
    if (--k == 0) { result = node.val; return; }
    kthSmallest(node.right);
}


// ─── TEMPLATE L: Convert Sorted Array to BST ─────────────────────────────────
TreeNode sortedArrayToBST(int[] nums, int left, int right) {
    if (left > right) return null;
    int mid = left + (right - left) / 2;
    TreeNode root = new TreeNode(nums[mid]);
    root.left  = sortedArrayToBST(nums, left, mid - 1);
    root.right = sortedArrayToBST(nums, mid + 1, right);
    return root;
}
```

---

## 7. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                         → PATTERN               → KEY CODE
──────────────────────────────────────────────────────────────────────────────────────
"inorder / preorder / postorder"          → DFS traversal         → recursive or iterative with stack
"level order / row by row"                → BFS                   → queue + snapshot size each level
"zigzag / spiral order"                   → BFS + flag            → reverse alternate levels
"invert / mirror binary tree"             → top-down swap         → swap left/right, recurse both
"symmetric tree / same tree"              → dual DFS              → compare pair of nodes simultaneously
"lowest common ancestor"                  → bottom-up LCA         → return root if found on both sides
"LCA of BST"                              → BST property          → go left/right based on values
"validate BST"                            → top-down bounds       → pass (min, max), check at each node
"kth smallest in BST"                     → inorder + counter     → inorder is sorted; stop at k
"path sum root to leaf"                   → top-down              → pass target - node.val down
"path sum any node to any node"           → prefix sum + map      → map.get(curr - target)
"maximum path sum"                        → bottom-up + global    → update global (L+root+R); return max one side
"diameter of binary tree"                 → bottom-up + global    → L+R at each node, return 1+max(L,R)
"balanced binary tree"                    → bottom-up             → return -1 on imbalance, height otherwise
"construct from traversals"               → divide & conquer      → preorder[0]=root; split inorder; recurse
"serialize / deserialize"                 → preorder + null mark  → "1,2,null,null,3,null,null"
"convert sorted array/list to BST"        → binary mid as root    → mid=root, recurse left/right halves
```

**Burn these into memory:**
```java
// Base case — ALWAYS handle null first
if (node == null) return 0/false/null;

// Level order — snapshot size BEFORE loop
int size = q.size();
for (int i = 0; i < size; i++) { ... }

// Validate BST — pass Long bounds, not int
isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE)

// Max path sum — ignore negative children
int left = Math.max(0, dfs(node.left));

// Path Sum III — backtrack after recursion
map.merge(curr, -1, Integer::sum);  // undo after left+right

// LCA — both sides found means current node IS the LCA
if (left != null && right != null) return root;
```

---

## 8. Common mistakes

### Mistake 1 — Forgetting null base case

```java
// BUG — NullPointerException
int height(TreeNode node) {
    return 1 + Math.max(height(node.left), height(node.right));  // node could be null!

// FIX
int height(TreeNode node) {
    if (node == null) return 0;
    return 1 + Math.max(height(node.left), height(node.right));
}
```

### Mistake 2 — Not snapshotting queue size in level order

```java
// BUG — processes more than one level per iteration
while (!q.isEmpty()) {
    TreeNode node = q.poll();   // doesn't separate levels!

// FIX — snapshot size before inner loop
while (!q.isEmpty()) {
    int size = q.size();        // how many nodes in this level
    for (int i = 0; i < size; i++) {
        TreeNode node = q.poll();
        ...
    }
}
```

### Mistake 3 — Using int bounds for Validate BST (overflow)

```java
// BUG — Integer.MIN_VALUE and MAX_VALUE can equal node values
boolean isValidBST(TreeNode node, int min, int max) { ... }

// FIX — use Long
boolean isValidBST(TreeNode node, long min, long max) {
    if (node == null) return true;
    if (node.val <= min || node.val >= max) return false;
    ...
}
```

### Mistake 4 — Returning wrong side in Max Path Sum

```java
// BUG — trying to return both sides to parent (invalid path)
return node.val + left + right;   // a path cannot fork at two nodes above

// FIX — return only the better single branch
maxSum = Math.max(maxSum, left + node.val + right);  // update global with both
return node.val + Math.max(left, right);             // return one side only
```

### Mistake 5 — Not using HashMap for tree construction (O(n²))

```java
// BUG — O(n) search in inorder for every recursive call → O(n²)
for (int i = 0; i < inorder.length; i++)
    if (inorder[i] == rootVal) { mid = i; break; }

// FIX — precompute HashMap → O(1) lookup → O(n) total
Map<Integer, Integer> map = new HashMap<>();
for (int i = 0; i < inorder.length; i++) map.put(inorder[i], i);
int mid = map.get(rootVal);
```

### Mistake 6 — Not backtracking in Path Sum III

```java
// BUG — prefixCount keeps growing, counts paths from previous branches
dfs(node.left, curr, target, map);
dfs(node.right, curr, target, map);
// forgot to remove curr from map after visiting!

// FIX — backtrack after both children return
map.merge(curr, -1, Integer::sum);   // undo this node's contribution
```

### Mistake 7 — LCA: forgetting to handle when both p and q are in same subtree

```java
// BUG — if both p and q are in left subtree, right returns null but left returns LCA
// Actually this is handled correctly by:
return left != null ? left : right;
// But the mistake is checking root == p before searching:

// WRONG — returns p even if q is deeper in p's subtree
if (root == null || root == p || root == q) return root;
// This is actually CORRECT for LCA — if we find p (or q), we return it
// The calling code handles the rest. This is a valid approach.
```

---

## 9. Complexity summary

| Problem | Time | Space | Notes |
|---------|------|-------|-------|
| Any DFS traversal | O(n) | O(h) | h = height; O(log n) balanced, O(n) skewed |
| BFS level order | O(n) | O(w) | w = max width; O(n) worst case |
| Invert / Same / Symmetric | O(n) | O(h) | visit every node once |
| LCA Binary Tree | O(n) | O(h) | may visit all nodes |
| LCA BST | O(h) | O(h) | BST property; O(log n) balanced |
| Validate BST | O(n) | O(h) | visit every node once |
| Recover BST | O(n) | O(h) | inorder scan for two swapped nodes |
| Kth Smallest BST | O(h + k) | O(h) | stop early in inorder |
| Height / Depth | O(n) | O(h) | post-order |
| Diameter | O(n) | O(h) | post-order with global max |
| Balanced | O(n) | O(h) | post-order; early exit with -1 |
| Path Sum I | O(n) | O(h) | top-down; stop at leaf |
| Path Sum II | O(n²) | O(n) | O(n) paths × O(n) copy each |
| Path Sum III | O(n) | O(n) | prefix sum + HashMap |
| Max Path Sum | O(n) | O(h) | post-order with global max |
| Construct from traversals | O(n) | O(n) | HashMap for O(1) inorder lookup |
| Serialize / Deserialize | O(n) | O(n) | preorder with null markers |
| Convert Sorted Array to BST | O(n) | O(log n) | binary mid recursion |
| Convert Sorted List to BST | O(n) | O(log n) | inorder simulation |

**General rules:**
- Space is **O(h)** for DFS — O(log n) balanced tree, O(n) worst case (skewed).
- BFS space is **O(w)** — O(n/2) = O(n) for the last level of a complete tree.
- BST operations are **O(log n)** average for balanced trees.
- Path Sum III uses prefix sum → **O(n)** vs O(n²) naive approach.
- Construction from traversals: HashMap makes it **O(n)** vs O(n²) linear search.

---

*Trees appear in 20–25% of FAANG interview problems.*
*Master the 4-line BFS template and the bottom-up DFS return pattern — they cover 80% of all tree problems.*
