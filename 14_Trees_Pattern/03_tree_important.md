# Tree Pattern — Important Problems (Striver Sheet Curated)

> **Pattern family:** Binary Tree / BST  
> **Language:** Java  
> **Source:** Striver's Tree Sheet — must-do problems for interviews  
> **Full problems:** [02_tree_problems.md](./02_tree_problems.md) | **Notes & Templates:** [01_tree_notes.md](./01_tree_notes.md)

---

## Quick Index

### Binary Tree
| # | Problem | Difficulty | Pattern | P# in full file |
|---|---------|-----------|---------|-----------------|
| 1 | Inorder / Preorder / Postorder Traversal | Easy | DFS | P1, P2, P3 |
| 2 | Pre+Post+Inorder in One Traversal | Medium | DFS State Machine | P55 |
| 3 | Level Order Traversal | Medium | BFS | P4 |
| 4 | Zigzag / Spiral Traversal | Medium | BFS + flag | P5 |
| 5 | Maximum Depth | Easy | Bottom-up DFS | P20 |
| 6 | Check Identical Trees | Easy | Dual DFS | P9 |
| 7 | Check Balanced Binary Tree | Easy | Bottom-up DFS | P21 |
| 8 | Diameter of Binary Tree | Easy | Bottom-up + global | P22 |
| 9 | Maximum Path Sum | Hard | Bottom-up + global | P31 |
| 10 | Check Symmetrical BT | Easy | Dual DFS | P8 |
| 11 | Zigzag Traversal | Medium | BFS | P5 |
| 12 | Boundary Traversal | Medium | DFS (3 passes) | P60 |
| 13 | Vertical Order Traversal | Hard | BFS + TreeMap | P59 |
| 14 | Top View of BT | Medium | BFS + HD Map | P58 |
| 15 | Bottom View of BT | Medium | BFS + HD Map | P57 |
| 16 | Right/Left View of BT | Medium | BFS last node | P56 |
| 17 | Print Root to Leaf Paths | Easy | DFS backtrack | P61 |
| 18 | LCA in Binary Tree | Medium | Bottom-up DFS | P14 |
| 19 | Maximum Width of BT | Medium | BFS + index | P42 |
| 20 | All Nodes Distance K | Medium | BFS + parent map | P43 |
| 21 | Minimum Time to Burn BT | Hard | BFS + parent map | P62 |
| 22 | Count Nodes in Complete BT | Medium | Height trick O(log²n) | P63 |
| 23 | Construct from Preorder + Inorder | Medium | Divide & Conquer | P32 |
| 24 | Construct from Postorder + Inorder | Medium | Divide & Conquer | P33 |
| 25 | Serialize and Deserialize BT | Hard | Preorder + null markers | P37 |
| 26 | Morris Inorder Traversal | Medium | Threaded tree O(1) space | P1 (notes) |
| 27 | Morris Preorder Traversal | Medium | Threaded tree O(1) space | P64 |

### Binary Search Tree
| # | Problem | Difficulty | Pattern | P# in full file |
|---|---------|-----------|---------|-----------------|
| 28 | Search in BST | Easy | BST property | P12 |
| 29 | Floor and Ceil in BST | Medium | BST property | P65 |
| 30 | Insert a Node in BST | Medium | BST property | P54 |
| 31 | Delete a Node in BST | Medium | Inorder successor | P66 |
| 32 | Kth Smallest in BST | Medium | Inorder + counter | P18 |
| 33 | Kth Largest in BST | Medium | Reverse inorder | P67 |
| 34 | Check if Tree is BST | Medium | Top-down bounds | P25 |
| 35 | LCA in BST | Medium | BST property | P13 |
| 36 | Construct BST from Preorder | Medium | Divide & Conquer | P45 |
| 37 | Inorder Successor and Predecessor | Medium | BST traversal | P68 |
| 38 | BST Iterator | Medium | Simulated inorder stack | P69 |
| 39 | Two Sum in BST | Easy | DFS + HashSet | P17 |
| 40 | Correct BST with Two Nodes Swapped | Hard | Inorder find violations | P26 |
| 41 | Largest BST in Binary Tree | Hard | Bottom-up (size,min,max) | P70 |

---

## Must-Know Patterns (Cheat Sheet)

```
PROBLEM TYPE                          PATTERN                 KEY TRICK
─────────────────────────────────────────────────────────────────────────────
Views (Top/Bottom/Right/Left)    →   BFS + horizontal dist   TreeMap by HD
Vertical Order                   →   BFS + (row,col)          TreeMap<col,TreeMap<row,PQ>>
Boundary Traversal               →   3-pass DFS               left bdry + leaves + right bdry
Burn Tree / Distance K           →   Build parent map + BFS   tree becomes undirected graph
Count Nodes Complete BT          →   Height check             if leftH==rightH → 2^h - 1
One-pass 3 traversals            →   Stack + state (1/2/3)    state controls pre/in/post visit
Delete in BST                    →   Find inorder successor   min of right subtree
Floor/Ceil in BST                →   BST walk + candidate     save node, keep searching
BST Iterator                     →   Iterative inorder stack  pushLeft() helper
Largest BST subtree              →   Bottom-up (size,min,max) return -1 if not BST
Inorder Successor                →   BST walk                 last ancestor where we went left
```

---

## Problems with Full Solutions

---

### 1. Pre, Inorder, Postorder in One Traversal (P55)
**Difficulty: Medium | Pattern: DFS State Machine**

```java
public void allTraversals(TreeNode root) {
    List<Integer> pre = new ArrayList<>(), in = new ArrayList<>(), post = new ArrayList<>();
    Deque<Object[]> st = new ArrayDeque<>();
    if (root != null) st.push(new Object[]{root, 1});

    while (!st.isEmpty()) {
        Object[] top = st.peek();
        TreeNode node = (TreeNode) top[0];
        int state = (int) top[1];

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
}
// Each node visited exactly 3 times. O(n) time, O(n) space.
```

---

### 2. Right/Left View (P56)
**LeetCode #199 | Difficulty: Medium | Pattern: BFS**

```java
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
// Left view: change i == size - 1  →  i == 0
```

---

### 3. Top View (P58) & Bottom View (P57)
**GeeksforGeeks | Difficulty: Medium | Pattern: BFS + HD Map**

```java
// TOP VIEW — first node at each horizontal distance
public List<Integer> topView(TreeNode root) {
    TreeMap<Integer, Integer> map = new TreeMap<>();
    Queue<Object[]> q = new LinkedList<>();
    q.offer(new Object[]{root, 0});
    while (!q.isEmpty()) {
        Object[] curr = q.poll();
        TreeNode node = (TreeNode) curr[0];
        int hd = (int) curr[1];
        map.putIfAbsent(hd, node.val);           // first node at HD = top
        if (node.left  != null) q.offer(new Object[]{node.left,  hd - 1});
        if (node.right != null) q.offer(new Object[]{node.right, hd + 1});
    }
    return new ArrayList<>(map.values());
}

// BOTTOM VIEW — overwrite: deepest node at each HD wins
public List<Integer> bottomView(TreeNode root) {
    TreeMap<Integer, Integer> map = new TreeMap<>();
    Queue<Object[]> q = new LinkedList<>();
    q.offer(new Object[]{root, 0});
    while (!q.isEmpty()) {
        Object[] curr = q.poll();
        TreeNode node = (TreeNode) curr[0];
        int hd = (int) curr[1];
        map.put(hd, node.val);                   // overwrite = bottom view
        if (node.left  != null) q.offer(new Object[]{node.left,  hd - 1});
        if (node.right != null) q.offer(new Object[]{node.right, hd + 1});
    }
    return new ArrayList<>(map.values());
}
```

---

### 4. Vertical Order Traversal (P59)
**LeetCode #987 | Difficulty: Hard | Pattern: BFS + TreeMap**

```java
public List<List<Integer>> verticalTraversal(TreeNode root) {
    TreeMap<Integer, TreeMap<Integer, PriorityQueue<Integer>>> map = new TreeMap<>();
    Queue<Object[]> q = new LinkedList<>();
    q.offer(new Object[]{root, 0, 0});

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
    for (var colMap : map.values()) {
        List<Integer> col = new ArrayList<>();
        for (var pq : colMap.values()) while (!pq.isEmpty()) col.add(pq.poll());
        res.add(col);
    }
    return res;
}
```

---

### 5. Boundary Traversal (P60)
**GeeksforGeeks | Difficulty: Medium | Pattern: DFS 3-pass**

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
    if (node.left != null) addLeftBoundary(node.left, res);
    else                   addLeftBoundary(node.right, res);
}
private void addLeaves(TreeNode node, List<Integer> res) {
    if (node == null) return;
    if (isLeaf(node)) { res.add(node.val); return; }
    addLeaves(node.left, res); addLeaves(node.right, res);
}
private void addRightBoundary(TreeNode node, List<Integer> res) {
    if (node == null || isLeaf(node)) return;
    if (node.right != null) addRightBoundary(node.right, res);
    else                    addRightBoundary(node.left, res);
    res.add(node.val);   // bottom-up
}
private boolean isLeaf(TreeNode n) { return n.left == null && n.right == null; }
```

---

### 6. Minimum Time to Burn Binary Tree (P62)
**GeeksforGeeks | Difficulty: Hard | Pattern: BFS + Parent Map**

```java
public int minTimeToBurn(TreeNode root, int target) {
    Map<TreeNode, TreeNode> parent = new HashMap<>();
    TreeNode targetNode = buildParentMap(root, target, parent);
    Set<TreeNode> visited = new HashSet<>();
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(targetNode); visited.add(targetNode);
    int time = 0;
    while (!q.isEmpty()) {
        int size = q.size(); boolean spread = false;
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
```

---

### 7. Count Total Nodes in Complete BT (P63)
**LeetCode #222 | Difficulty: Medium | Pattern: Height trick**

```java
public int countNodes(TreeNode root) {
    if (root == null) return 0;
    int leftH = 0, rightH = 0;
    TreeNode l = root, r = root;
    while (l != null) { leftH++;  l = l.left;  }
    while (r != null) { rightH++; r = r.right; }
    if (leftH == rightH) return (1 << leftH) - 1;   // perfect subtree
    return 1 + countNodes(root.left) + countNodes(root.right);
}
// O(log²n) — much better than O(n) brute force
```

---

### 8. Floor and Ceil in BST (P65)
**GeeksforGeeks | Difficulty: Medium | Pattern: BST walk**

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

---

### 9. Delete a Node in BST (P66)
**LeetCode #450 | Difficulty: Medium | Pattern: Inorder successor**

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

### 10. Inorder Successor and Predecessor (P68)
**GeeksforGeeks | Difficulty: Medium | Pattern: BST walk + candidate**

```java
public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
    TreeNode successor = null;
    while (root != null) {
        if (p.val < root.val) { successor = root; root = root.left; }
        else root = root.right;
    }
    return successor;
}
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

### 11. BST Iterator (P69)
**LeetCode #173 | Difficulty: Medium | Pattern: Simulated inorder**

```java
class BSTIterator {
    private Deque<TreeNode> stack = new ArrayDeque<>();
    public BSTIterator(TreeNode root) { pushLeft(root); }
    public int next() {
        TreeNode node = stack.pop();
        pushLeft(node.right);
        return node.val;
    }
    public boolean hasNext() { return !stack.isEmpty(); }
    private void pushLeft(TreeNode node) {
        while (node != null) { stack.push(node); node = node.left; }
    }
}
// O(1) amortized next(), O(h) space
```

---

### 12. Largest BST in Binary Tree (P70)
**LeetCode #333 | Difficulty: Hard | Pattern: Bottom-up (size, min, max)**

```java
private int maxSize = 0;
public int largestBSTSubtree(TreeNode root) {
    dfs(root);
    return maxSize;
}
private int[] dfs(TreeNode node) {  // returns {size, min, max}; size=-1 if not BST
    if (node == null) return new int[]{0, Integer.MAX_VALUE, Integer.MIN_VALUE};
    int[] left = dfs(node.left), right = dfs(node.right);
    if (left[0] != -1 && right[0] != -1 && node.val > left[2] && node.val < right[1]) {
        int size = left[0] + right[0] + 1;
        maxSize = Math.max(maxSize, size);
        return new int[]{size, Math.min(node.val, left[1]), Math.max(node.val, right[2])};
    }
    return new int[]{-1, 0, 0};
}
```

---

## Complexity Quick Reference

| Problem | Time | Space | Key insight |
|---------|------|-------|-------------|
| All 3 traversals in one pass | O(n) | O(n) | state machine per node |
| Top / Bottom View | O(n log n) | O(n) | TreeMap by HD |
| Vertical Order Traversal | O(n log n) | O(n) | TreeMap col→row→PQ |
| Boundary Traversal | O(n) | O(h) | 3 separate DFS passes |
| Burn Tree | O(n) | O(n) | BFS from target on undirected graph |
| Count nodes complete BT | O(log²n) | O(log n) | height check shortcut |
| Floor / Ceil in BST | O(h) | O(1) | BST walk with candidate |
| Delete in BST | O(h) | O(h) | inorder successor replace |
| Inorder Successor | O(h) | O(1) | candidate on left turns |
| BST Iterator | O(1) amortized | O(h) | pushLeft trick |
| Largest BST in BT | O(n) | O(h) | return (size,min,max) |

---

*Focus on these 41 problems. They cover every pattern Striver tests in tree interviews.*
