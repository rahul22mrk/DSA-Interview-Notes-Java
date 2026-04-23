# Tree Problems — Striver + ProPeers

> **Language:** Java | **Total Problems: 44** (duplicates counted once)
> **Notes & Templates:** [01_tree_notes.md](./01_tree_notes.md)

---

## Table of Contents

### Binary Tree
- **Tree Traversal**
  - [1. Inorder Traversal](#1-inorder-traversal)
  - [2. Preorder Traversal](#2-preorder-traversal)
  - [3. Postorder Traversal](#3-postorder-traversal)
  - [4. Level Order Traversal](#4-level-order-traversal)
  - [5. ZigZag / Spiral Traversal](#5-zigzag--spiral-traversal)
  - [6. Level Order II — Bottom Up](#6-level-order-ii--bottom-up)
  - [7. Pre + Post + Inorder in One Traversal](#7-pre--post--inorder-in-one-traversal)

- **Mirror & Symmetry**
  - [8. Invert Binary Tree](#8-invert-binary-tree)
  - [9. Symmetric Tree](#9-symmetric-tree)
  - [10. Same Tree — Check if Two Trees are Identical](#10-same-tree--check-if-two-trees-are-identical)
  - [11. Subtree of Another Tree](#11-subtree-of-another-tree)
  - [12. Flip Equivalent Binary Trees](#12-flip-equivalent-binary-trees)

- **Medium Problems — BT Properties**
  - [13. Maximum Depth of Binary Tree](#13-maximum-depth-of-binary-tree)
  - [14. Minimum Depth of Binary Tree](#14-minimum-depth-of-binary-tree)
  - [15. Check for Balanced Binary Tree](#15-check-for-balanced-binary-tree)
  - [16. Diameter of Binary Tree](#16-diameter-of-binary-tree)
  - [17. Binary Tree Tilt](#17-binary-tree-tilt)
  - [18. Check Completeness of Binary Tree](#18-check-completeness-of-binary-tree)

- **Path Sum & Root to Leaf**
  - [19. Maximum Path Sum in BT](#19-maximum-path-sum-in-bt)
  - [20. Path Sum](#20-path-sum)
  - [21. Path Sum II](#21-path-sum-ii)
  - [22. Path Sum III](#22-path-sum-iii)
  - [23. Sum of Root to Leaf Numbers](#23-sum-of-root-to-leaf-numbers)
  - [24. Print Root to Leaf Paths](#24-print-root-to-leaf-paths)

- **FAQs — Views & Advanced BFS**
  - [25. Boundary Traversal of BT](#25-boundary-traversal-of-bt)
  - [26. Vertical Order Traversal of BT](#26-vertical-order-traversal-of-bt)
  - [27. Top View of BT](#27-top-view-of-bt)
  - [28. Bottom View of BT](#28-bottom-view-of-bt)
  - [29. Right / Left View of BT](#29-right--left-view-of-bt)
  - [30. LCA in Binary Tree](#30-lca-in-binary-tree)
  - [31. LCA of Deepest Leaves](#31-lca-of-deepest-leaves)
  - [32. Maximum Width of BT](#32-maximum-width-of-bt)
  - [33. All Nodes at Distance K in BT](#33-all-nodes-at-distance-k-in-bt)
  - [34. Minimum Time to Burn BT from a Node](#34-minimum-time-to-burn-bt-from-a-node)
  - [35. Count Total Nodes in a Complete BT](#35-count-total-nodes-in-a-complete-bt)

- **Construction Problems**
  - [36. Requirements to Construct a Unique BT](#36-requirements-to-construct-a-unique-bt)
  - [37. Construct BT from Preorder and Inorder](#37-construct-bt-from-preorder-and-inorder)
  - [38. Construct BT from Postorder and Inorder](#38-construct-bt-from-postorder-and-inorder)
  - [39. Construct BT from Preorder and Postorder](#39-construct-bt-from-preorder-and-postorder)
  - [40. Convert Sorted Array to BST](#40-convert-sorted-array-to-bst)
  - [41. Convert Sorted List to BST](#41-convert-sorted-list-to-bst)
  - [42. Serialize and Deserialize BT](#42-serialize-and-deserialize-bt)

- **Traversal in Constant Space — Morris**
  - [43. Morris Inorder Traversal](#43-morris-inorder-traversal)
  - [44. Morris Preorder Traversal](#44-morris-preorder-traversal)

### Binary Search Tree
- **Theory & Basics**
  - [45. Introduction to BST](#45-introduction-to-bst)
  - [46. Search in BST](#46-search-in-bst)
  - [47. Floor and Ceil in a BST](#47-floor-and-ceil-in-a-bst)

- **Medium**
  - [48. Insert a Node in BST](#48-insert-a-node-in-bst)
  - [49. Delete a Node in BST](#49-delete-a-node-in-bst)
  - [50. Kth Smallest and Largest Element in BST](#50-kth-smallest-and-largest-element-in-bst)
  - [51. Check if a Tree is a BST](#51-check-if-a-tree-is-a-bst)
  - [52. LCA in BST](#52-lca-in-bst)
  - [53. Construct BST from Preorder Traversal](#53-construct-bst-from-preorder-traversal)
  - [54. Inorder Successor and Predecessor in BST](#54-inorder-successor-and-predecessor-in-bst)

- **FAQs**
  - [55. BST Iterator](#55-bst-iterator)
  - [56. Two Sum in BST](#56-two-sum-in-bst)
  - [57. Correct BST with Two Nodes Swapped](#57-correct-bst-with-two-nodes-swapped)
  - [58. Largest BST in Binary Tree](#58-largest-bst-in-binary-tree)

---

## Binary Tree

---

## Tree Traversal

---

### 1. Inorder Traversal
**LeetCode #94 | Easy | Striver + ProPeers**

> Return inorder (Left → Root → Right) traversal of a binary tree.

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

```

```java
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

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        TreeNode node = root;
        Deque<TreeNode> st = new ArrayDeque<>();

        while(true){
            if(node!=null){
                st.push(node);
                node = node.left ;
            }else{
                if(st.isEmpty()) break;
                node = st.pop();
                ans.add(node.val);
                node = node.right;
            }
        }
        return ans;
        
    }
}
```

```
    1
     \
      2        Inorder: [1, 3, 2] ✓
     /
    3
```

---

### 2. Preorder Traversal
**LeetCode #144 | Easy | Striver + ProPeers**

> Return preorder (Root → Left → Right) traversal.

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
```

```java

// Iterative
public List<Integer> preorderIterative(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    if (root == null) return res;
    Deque<TreeNode> stack = new ArrayDeque<>();
    stack.push(root);
    while (!stack.isEmpty()) {
        TreeNode node = stack.pop();
        res.add(node.val);
        if (node.right != null) stack.push(node.right); // right first (LIFO)
        if (node.left  != null) stack.push(node.left);
    }
    return res;
}
```

---

### 3. Postorder Traversal
**LeetCode #145 | Easy | Striver + ProPeers**

> Return postorder (Left → Right → Root) traversal.

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
```

```java

// Iterative (reverse of modified preorder)
public List<Integer> postorderIterative(TreeNode root) {
    LinkedList<Integer> res = new LinkedList<>();
    if (root == null) return res;
    Deque<TreeNode> stack = new ArrayDeque<>();
    stack.push(root);
    while (!stack.isEmpty()) {
        TreeNode node = stack.pop();
        res.addFirst(node.val);          // prepend = reverse at end
        if (node.left  != null) stack.push(node.left);
        if (node.right != null) stack.push(node.right);
    }
    return res;
}
```

```java


class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        Deque<TreeNode> st = new ArrayDeque<>();
        if(root!=null) st.push(root);

        while(!st.isEmpty()){
            TreeNode node = st.pop();
            ans.add(node.val);

            if(node.left!=null){
                st.push(node.left);
            }
            
            if(node.right!=null){
                st.push(node.right);
            }
        }
        Collections.reverse(ans);
        return ans;
    }
}
```

---

### 4. Level Order Traversal
**LeetCode #102 | Medium | Striver + ProPeers**

> Return nodes level by level (BFS).

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> res = new ArrayList<>();
    if (root == null) return res;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    while (!q.isEmpty()) {
        int size = q.size();             // snapshot — critical!
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

```
    3
   / \
  9  20          Output: [[3],[9,20],[15,7]] ✓
    /  \
   15   7
```

---

### 5. ZigZag / Spiral Traversal
**LeetCode #103 | Medium | Striver + ProPeers**

> Level order but alternate left-to-right and right-to-left each level.

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
            else             level.addFirst(node.val);  // reverse direction
            if (node.left  != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
        res.add(level);
        leftToRight = !leftToRight;
    }
    return res;
}
```

```java
public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root==null) return res;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        boolean leftToRight = true;

        while(!q.isEmpty()){
            int size = q.size();
            
            List<Integer> level = new ArrayList<>(Collections.nCopies(size,0));

            for(int i=0;i<size;i++){
                TreeNode node = q.poll();
                int index = leftToRight ? i : size - i -1;

                level.set(index, node.val);

                if(node.left!=null){
                    q.offer(node.left);
                }

                if(node.right!=null){
                    q.offer(node.right);
                }
                
            }

            res.add(level);
            leftToRight = !leftToRight;
        }
        return res;
    }

```



---

### 6. Level Order II — Bottom Up
**LeetCode #107 | Easy | ProPeers**

> Same as level order but return bottom-up (deepest level first).

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
        res.addFirst(level);   // prepend each level → bottom-up
    }
    return res;
}

```

```java
 public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();

        if(root==null){
            return res;
        }

        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);

        while(!q.isEmpty()){
            int size = q.size();
            List<Integer> level = new ArrayList<>();

            for(int i=0;i<size;i++){
                TreeNode node = q.poll();
                level.add(node.val);

                if(node.left!=null){
                    q.offer(node.left);
                }

                if(node.right!=null){
                    q.offer(node.right);
                }
            }

            res.add(0,level);
        }
        return res;
        
    }
```

---

### 7. Pre + Post + Inorder in One Traversal
**No LeetCode | Medium | Striver**

> Print all three traversals in a single DFS pass using state per node.

**Core insight:** Each node visited 3 times. state=1 → preorder, state=2 → inorder, state=3 → postorder.

```java

 class NodeState{
    TreeNode node;
    int state;

    NodeState(TreeNode node, int state){
        this.node = node;
        this.state = state;
    }
 }

class Solution {
    List<List<Integer>> treeTraversal(TreeNode root) {
        //your code goes here
        List<Integer> in = new ArrayList<>();
        List<Integer> pre = new ArrayList<>();
        List<Integer> post = new ArrayList<>();

        if(root == null){
            return Arrays.asList(in,pre,post);
        }
        Deque<NodeState> st = new ArrayDeque<>();
        st.push(new NodeState(root,1));

        while(!st.isEmpty()){
            NodeState nodeState = st.poll();
            TreeNode node = nodeState.node;
            int state = nodeState.state;

            if(state==1){
                pre.add(node.data);
                st.push(new NodeState(node,2));
                if(node.left!=null){
                    st.push(new NodeState(node.left,1));
                }

            }else if(state==2){
                in.add(node.data);
                st.push(new NodeState(node,3));
                if(node.right!=null){
                    st.push(new NodeState(node.right,1));
                }
            }else{
                post.add(node.data);
            }
            
        }

        return Arrays.asList(in,pre,post);
    }
}

```

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
            pre.add(node.val);           // preorder: first visit
            top[1] = 2;
            if (node.left  != null) st.push(new Object[]{node.left, 1});
        } else if (state == 2) {
            in.add(node.val);            // inorder: second visit
            top[1] = 3;
            if (node.right != null) st.push(new Object[]{node.right, 1});
        } else {
            post.add(node.val);          // postorder: third visit
            st.pop();
        }
    }
}
```

```
    1
   / \         Pre:  [1, 2, 4, 5, 3]
  2   3         In:   [4, 2, 5, 1, 3]
 / \            Post: [4, 5, 2, 3, 1]
4   5
```

---

## Mirror & Symmetry

---

### 8. Invert Binary Tree
**LeetCode #226 | Easy | ProPeers**

> Mirror a binary tree — swap left and right children at every node.

```java
public TreeNode invertTree(TreeNode root) {
    if (root == null) return null;
    TreeNode tmp   = root.left;
    root.left      = invertTree(root.right);
    root.right     = invertTree(tmp);
    return root;
}
```

```java
// Approach 2 — BFS (Queue)
public TreeNode invertTree(TreeNode root) {
    if (root == null) return null;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    while (!q.isEmpty()) {
        TreeNode node = q.poll();
        // swap
        TreeNode tmp  = node.left;
        node.left     = node.right;
        node.right    = tmp;

        if (node.left  != null) q.offer(node.left);
        if (node.right != null) q.offer(node.right);
    }
    return root;
}

```

```java
// Approach 3 — DFS (Stack)
public TreeNode invertTree(TreeNode root) {
    if (root == null) return null;
    Deque<TreeNode> stack = new ArrayDeque<>();
    stack.push(root);
    while (!stack.isEmpty()) {
        TreeNode node = stack.pop();
        // swap
        TreeNode tmp  = node.left;
        node.left     = node.right;
        node.right    = tmp;

        if (node.left  != null) stack.push(node.left);
        if (node.right != null) stack.push(node.right);
    }
    return root;
}
```

```
     4               4
   /   \    →      /   \
  2     7         7     2
 / \   / \       / \   / \
1   3 6   9     9   6 3   1
```

---

### 9. Symmetric Tree
**LeetCode #101 | Easy | Striver + ProPeers**

> Check if a binary tree is a mirror image of itself.

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

### 10. Same Tree — Check if Two Trees are Identical
**LeetCode #100 | Easy | Striver + ProPeers**

> Check if two binary trees have same structure and values.

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

### 11. Subtree of Another Tree
**LeetCode #572 | Medium | ProPeers**

> Check if `subRoot` is a subtree of `root`.

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

---

### 12. Flip Equivalent Binary Trees
**LeetCode #951 | Medium | ProPeers**

> Two trees are flip equivalent if one can be obtained by flipping children at some nodes.

```java
public boolean flipEquiv(TreeNode r1, TreeNode r2) {
    if (r1 == null && r2 == null) return true;
    if (r1 == null || r2 == null) return false;
    if (r1.val != r2.val) return false;
    boolean noFlip = flipEquiv(r1.left, r2.left)   && flipEquiv(r1.right, r2.right);
    boolean flip   = flipEquiv(r1.left, r2.right)  && flipEquiv(r1.right, r2.left);
    return noFlip || flip;
}
```

---

## Medium Problems — BT Properties

---

### 13. Maximum Depth of Binary Tree
**LeetCode #104 | Easy | Striver + ProPeers**

> Find the maximum depth (height) of a binary tree.

```java
public int maxDepth(TreeNode root) {
    if (root == null) return 0;
    return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
```

---

### 14. Minimum Depth of Binary Tree
**LeetCode #111 | Easy | ProPeers**

> Find the minimum depth (root to nearest leaf). Handle one-child nodes carefully.

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

### 15. Check for Balanced Binary Tree
**LeetCode #110 | Easy | Striver + ProPeers**

> Check if every node's left and right heights differ by at most 1.

**Core insight:** Return -1 to signal "unbalanced" — single pass bottom-up, no recomputation.

```java
public boolean isBalanced(TreeNode root) {
    return checkHeight(root) != -1;
}
private int checkHeight(TreeNode node) {
    if (node == null) return 0;
    int left  = checkHeight(node.left);
    int right = checkHeight(node.right);
    if (left == -1 || right == -1)     return -1;  // propagate signal
    if (Math.abs(left - right) > 1)    return -1;  // unbalanced here
    return 1 + Math.max(left, right);
}
```

---

### 16. Diameter of Binary Tree
**LeetCode #543 | Easy | Striver + ProPeers**

> Longest path between any two nodes (may not pass through root).

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

```
      1
     / \
    2   3       diameter = 3 (4→2→1→3) ✓
   / \
  4   5
```

---

### 17. Binary Tree Tilt
**LeetCode #563 | Easy | ProPeers**

> Sum of every node's tilt. Tilt = |sum(left subtree) - sum(right subtree)|.

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

### 18. Check Completeness of Binary Tree
**LeetCode #958 | Medium | ProPeers**

> A complete BT has all levels full except possibly the last (filled left to right).

**Core insight:** BFS — once a null is seen, all remaining nodes must also be null.

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
            if (seenNull) return false;  // non-null after null → not complete
            q.offer(node.left);
            q.offer(node.right);
        }
    }
    return true;
}
```

---

## Path Sum & Root to Leaf

---

### 19. Maximum Path Sum in BT
**LeetCode #124 | Hard | Striver + ProPeers**

> Maximum path sum where path can start and end at any node.

**Core insight:** Update global max using BOTH sides. Return only ONE side to parent (path can't fork upward).

```java
private int maxSum = Integer.MIN_VALUE;

public int maxPathSum(TreeNode root) {
    dfs(root);
    return maxSum;
}
private int dfs(TreeNode node) {
    if (node == null) return 0;
    int left  = Math.max(0, dfs(node.left));   // ignore negatives
    int right = Math.max(0, dfs(node.right));
    maxSum = Math.max(maxSum, left + node.val + right);  // both sides: update global
    return node.val + Math.max(left, right);             // one side: return up
}
```

```
    -10
    /  \
   9   20          Max path: 15 → 20 → 7 = 42 ✓
      /  \
     15   7
```

---

### 20. Path Sum
**LeetCode #112 | Easy | ProPeers**

> Check if there is a root-to-leaf path with sum equal to targetSum.

```java
public boolean hasPathSum(TreeNode root, int targetSum) {
    if (root == null) return false;
    if (root.left == null && root.right == null) return root.val == targetSum;
    int rem = targetSum - root.val;
    return hasPathSum(root.left, rem) || hasPathSum(root.right, rem);
}
```

---

### 21. Path Sum II
**LeetCode #113 | Medium | ProPeers**

> Find all root-to-leaf paths where the sum equals targetSum.

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
        res.add(new ArrayList<>(path));    // copy — not reference
    dfs(node.left,  rem - node.val, path, res);
    dfs(node.right, rem - node.val, path, res);
    path.remove(path.size() - 1);          // backtrack
}
```

---

### 22. Path Sum III
**LeetCode #437 | Medium | ProPeers**

> Count paths (not necessarily root-to-leaf) where sum equals targetSum.

**Core insight:** Prefix sum + HashMap. At each node check how many past prefix sums equal `curr - target`. Backtrack after recursion.

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
    map.merge(curr, -1, Integer::sum);    // backtrack
    return count;
}
```

---

### 23. Sum of Root to Leaf Numbers
**LeetCode #129 | Medium | ProPeers**

> Each root-to-leaf path forms a number. Return total sum of all such numbers.

```java
public int sumNumbers(TreeNode root) {
    return dfs(root, 0);
}
private int dfs(TreeNode node, int curr) {
    if (node == null) return 0;
    curr = curr * 10 + node.val;
    if (node.left == null && node.right == null) return curr;   // leaf
    return dfs(node.left, curr) + dfs(node.right, curr);
}
```

```
    1
   / \       Paths: 12 + 13 = 25 ✓
  2   3
```

---

### 24. Print Root to Leaf Paths
**LeetCode #257 | Easy | Striver**

> Print all root-to-leaf paths.

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

```
    1
   / \       Output: ["1->2->5", "1->3"] ✓
  2   3
   \
    5
```

---

## FAQs — Views & Advanced BFS

---

### 25. Boundary Traversal of BT
**GFG | Medium | Striver**

> Left boundary (top-down, no leaves) + all leaves + right boundary (bottom-up, no leaves).

```java
public List<Integer> boundaryOfBinaryTree(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    if (root == null) return res;
    if (!isLeaf(root)) res.add(root.val);
    addLeftBoundary(root.left,  res);
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
private boolean isLeaf(TreeNode n) { return n.left == null && n.right == null; }
```

```
        1
       / \
      2   3        Boundary: [1, 2, 4, 5, 6, 7, 3] ✓
     / \ / \
    4  5 6  7
```

---

### 26. Vertical Order Traversal of BT
**LeetCode #987 | Hard | Striver**

> Nodes column by column. Same column+row → sort by value.

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
    for (var colMap : map.values()) {
        List<Integer> col = new ArrayList<>();
        for (var pq : colMap.values()) while (!pq.isEmpty()) col.add(pq.poll());
        res.add(col);
    }
    return res;
}
```

---

### 27. Top View of BT
**GFG | Medium | Striver**

> First node at each horizontal distance during BFS = top view.

```java
public List<Integer> topView(TreeNode root) {
    TreeMap<Integer, Integer> map = new TreeMap<>();
    Queue<Object[]> q = new LinkedList<>();
    q.offer(new Object[]{root, 0});
    while (!q.isEmpty()) {
        Object[] curr = q.poll();
        TreeNode node = (TreeNode) curr[0];
        int hd = (int) curr[1];
        map.putIfAbsent(hd, node.val);            // first node at HD = top view
        if (node.left  != null) q.offer(new Object[]{node.left,  hd - 1});
        if (node.right != null) q.offer(new Object[]{node.right, hd + 1});
    }
    return new ArrayList<>(map.values());
}
```

---

### 28. Bottom View of BT
**GFG | Medium | Striver**

> Last (deepest) node at each horizontal distance = bottom view.

```java
public List<Integer> bottomView(TreeNode root) {
    TreeMap<Integer, Integer> map = new TreeMap<>();
    Queue<Object[]> q = new LinkedList<>();
    q.offer(new Object[]{root, 0});
    while (!q.isEmpty()) {
        Object[] curr = q.poll();
        TreeNode node = (TreeNode) curr[0];
        int hd = (int) curr[1];
        map.put(hd, node.val);                    // overwrite = deepest wins
        if (node.left  != null) q.offer(new Object[]{node.left,  hd - 1});
        if (node.right != null) q.offer(new Object[]{node.right, hd + 1});
    }
    return new ArrayList<>(map.values());
}
```

```
         1  (hd=0)
        / \
       2   3            Top:    [4, 2, 1, 3, 6]
      / \   \           Bottom: [4, 2, 5, 3, 6]
     4   5   6
```

---

### 29. Right / Left View of BT
**LeetCode #199 | Medium | Striver**

> Right view = last node of each level. Left view = first node of each level.

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
            if (i == size - 1) res.add(node.val);   // last = right view
            if (node.left  != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
    }
    return res;
}
// Left view: change  i == size - 1  →  i == 0
```

---

### 30. LCA in Binary Tree
**LeetCode #236 | Medium | Striver + ProPeers**

> Find Lowest Common Ancestor in a general binary tree.

**Core insight:** Post-order DFS. If both left and right return non-null → current node is LCA.

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q) return root;
    TreeNode left  = lowestCommonAncestor(root.left,  p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);
    if (left != null && right != null) return root;   // p and q on different sides
    return left != null ? left : right;
}
```

```
        3
       / \
      5   1           LCA(5, 1) = 3 ✓
     / \ / \          LCA(5, 4) = 5 ✓
    6  2 0  8
      / \
     7   4
```

---

### 31. LCA of Deepest Leaves
**LeetCode #1123 | Medium | ProPeers**

> Find LCA of the deepest leaves.

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
        return new Pair(node, left.depth + 1);       // equal depth → LCA here
    return left.depth > right.depth
        ? new Pair(left.node,  left.depth  + 1)
        : new Pair(right.node, right.depth + 1);
}
```

---

### 32. Maximum Width of BT
**LeetCode #662 | Medium | Striver**

> Width of a level = distance between leftmost and rightmost non-null nodes (including nulls between).

**Core insight:** Assign index to each node: root=0, left=2i, right=2i+1. Normalize to prevent overflow.

```java
public int widthOfBinaryTree(TreeNode root) {
    Queue<TreeNode> nodes = new LinkedList<>();
    Queue<Long> indices = new LinkedList<>();
    nodes.offer(root); indices.offer(0L);
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

### 33. All Nodes at Distance K in BT
**LeetCode #863 | Medium | Striver**

> Find all nodes at distance K from a target node.

**Core insight:** Build parent map → BFS from target treating tree as undirected graph.

```java
public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
    Map<TreeNode, TreeNode> parent = new HashMap<>();
    buildParent(root, null, parent);

    Queue<TreeNode> q = new LinkedList<>();
    Set<TreeNode> visited = new HashSet<>();
    q.offer(target); visited.add(target);
    int dist = 0;

    while (!q.isEmpty()) {
        if (dist == k) {
            List<Integer> res = new ArrayList<>();
            for (TreeNode n : q) res.add(n.val);
            return res;
        }
        int size = q.size(); dist++;
        for (int i = 0; i < size; i++) {
            TreeNode node = q.poll();
            for (TreeNode next : new TreeNode[]{node.left, node.right, parent.get(node)}) {
                if (next != null && !visited.contains(next)) {
                    visited.add(next); q.offer(next);
                }
            }
        }
    }
    return new ArrayList<>();
}
private void buildParent(TreeNode node, TreeNode par, Map<TreeNode, TreeNode> parent) {
    if (node == null) return;
    parent.put(node, par);
    buildParent(node.left,  node, parent);
    buildParent(node.right, node, parent);
}
```

---

### 34. Minimum Time to Burn BT from a Node
**GFG | Hard | Striver**

> Fire starts at target node and spreads each second to adjacent nodes. Find minimum time to burn all nodes.

**Core insight:** Build parent map → BFS from target as undirected graph. Count BFS levels.

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

```
       1
      / \
     2   3       target=2 → t=0:{2}, t=1:{4,5,1}, t=2:{3}
    / \           Answer = 2 ✓
   4   5
```

---

### 35. Count Total Nodes in a Complete BT
**LeetCode #222 | Medium | Striver**

> Count nodes in O(log²n) using the complete BT property.

**Core insight:** If left height == right height → perfect subtree → `2^h - 1` nodes instantly. Otherwise recurse.

```java
public int countNodes(TreeNode root) {
    if (root == null) return 0;
    int leftH = 0, rightH = 0;
    TreeNode l = root, r = root;
    while (l != null) { leftH++;  l = l.left;  }
    while (r != null) { rightH++; r = r.right; }
    if (leftH == rightH) return (1 << leftH) - 1;   // perfect: 2^h - 1
    return 1 + countNodes(root.left) + countNodes(root.right);
}
```

---

## Construction Problems

---

### 36. Requirements to Construct a Unique BT
**Theory | Striver**

> Which pairs of traversals uniquely define a binary tree?

```
Inorder + Preorder   → Unique BT ✓   (preorder gives root, inorder splits L/R)
Inorder + Postorder  → Unique BT ✓   (postorder gives root from end)
Inorder + Level Order→ Unique BT ✓

Preorder + Postorder → NOT unique ✗  (can't determine left/right split)
Only Preorder        → NOT unique ✗
Only Inorder         → NOT unique ✗

KEY RULE: Inorder is MANDATORY in any pair for a unique BT.
```

---

### 37. Construct BT from Preorder and Inorder
**LeetCode #105 | Medium | Striver + ProPeers**

> preorder[0] = root. Find root in inorder → split left/right. Use HashMap for O(1) lookup.

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

```
preorder=[3,9,20,15,7], inorder=[9,3,15,20,7]
→       3
       / \
      9  20
        /  \
       15   7   ✓
```

---

### 38. Construct BT from Postorder and Inorder
**LeetCode #106 | Medium | Striver + ProPeers**

> postorder[last] = root. Find in inorder → build right FIRST (postorder is L,R,Root).

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
    root.right = build(postorder, mid + 1, inRight);   // right FIRST
    root.left  = build(postorder, inLeft,  mid - 1);
    return root;
}
```

---

### 39. Construct BT from Preorder and Postorder
**LeetCode #889 | Medium | ProPeers**

> Result may not be unique. preorder[preIdx+1] = left child root → find in postorder for left size.

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

### 40. Convert Sorted Array to BST
**LeetCode #108 | Easy | ProPeers**

> Mid element = root, recurse on left and right halves. Result is height-balanced BST.

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

---

### 41. Convert Sorted List to BST
**LeetCode #109 | Medium | ProPeers**

> Find mid using slow/fast pointers. Cut list, make mid = root, recurse.

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

### 42. Serialize and Deserialize BT
**LeetCode #297 | Hard | Striver + ProPeers**

> Preorder DFS with "null" markers. Queue-based rebuild on deserialize.

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

```
Tree:        1
            / \              Serialized: "1,2,null,null,3,4,null,null,5,null,null"
           2   3
              / \
             4   5
```

---

## Traversal in Constant Space — Morris

---

### 43. Morris Inorder Traversal
**No LeetCode | Medium | Striver**

> Inorder in O(1) space — no stack, no recursion. Thread rightmost of left subtree back to current node.

```java
public List<Integer> morrisInorder(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    TreeNode curr = root;
    while (curr != null) {
        if (curr.left == null) {
            res.add(curr.val);       // no left: visit and go right
            curr = curr.right;
        } else {
            TreeNode pred = curr.left;
            while (pred.right != null && pred.right != curr)
                pred = pred.right;  // find inorder predecessor
            if (pred.right == null) {
                pred.right = curr;   // thread: connect back
                curr = curr.left;
            } else {
                pred.right = null;   // remove thread: second visit
                res.add(curr.val);   // visit NOW (inorder)
                curr = curr.right;
            }
        }
    }
    return res;
}
```

---

### 44. Morris Preorder Traversal
**No LeetCode | Medium | Striver**

> Same threading as Morris Inorder but print on FIRST visit (before going left).

```java
public List<Integer> morrisPreorder(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    TreeNode curr = root;
    while (curr != null) {
        if (curr.left == null) {
            res.add(curr.val);       // no left: visit and go right
            curr = curr.right;
        } else {
            TreeNode pred = curr.left;
            while (pred.right != null && pred.right != curr)
                pred = pred.right;
            if (pred.right == null) {
                res.add(curr.val);   // FIRST visit → preorder (before going left)
                pred.right = curr;
                curr = curr.left;
            } else {
                pred.right = null;   // remove thread (second visit: don't print)
                curr = curr.right;
            }
        }
    }
    return res;
}
```

---

## Binary Search Tree

---

## Theory & Basics

---

### 45. Introduction to BST
**Theory | Striver**

> BST property: for every node, all left subtree values < node < all right subtree values. Inorder of BST = sorted ascending order.

```
BST:      8
         / \
        3  10
       / \    \
      1   6   14
         / \  /
        4   7 13

Inorder: [1, 3, 4, 6, 7, 8, 10, 13, 14]  ← sorted ✓

Search: O(log n) avg, O(n) worst (skewed)
Insert: O(log n) avg
Delete: O(log n) avg
```

---

### 46. Search in BST
**LeetCode #700 | Easy | Striver + ProPeers**

> Find node with value `val`. Use BST property to go left or right.

```java
public TreeNode searchBST(TreeNode root, int val) {
    if (root == null || root.val == val) return root;
    return val < root.val
        ? searchBST(root.left,  val)
        : searchBST(root.right, val);
}
```

---

### 47. Floor and Ceil in a BST
**GFG | Medium | Striver**

> Floor = largest value ≤ target. Ceil = smallest value ≥ target.

```java
public int floorBST(TreeNode root, int target) {
    int floor = -1;
    while (root != null) {
        if (root.val == target) return root.val;
        if (root.val < target) { floor = root.val; root = root.right; }  // candidate, try closer
        else root = root.left;
    }
    return floor;
}
public int ceilBST(TreeNode root, int target) {
    int ceil = -1;
    while (root != null) {
        if (root.val == target) return root.val;
        if (root.val > target) { ceil = root.val; root = root.left; }   // candidate, try closer
        else root = root.right;
    }
    return ceil;
}
```

```
BST:    8
       / \
      4  12        floor(5) = 4,  ceil(5) = 8 ✓
     / \
    2   6
```

---

## BST — Medium

---

### 48. Insert a Node in BST
**LeetCode #701 | Medium | Striver**

> Insert val at the correct position — always insert as a new leaf.

```java
public TreeNode insertIntoBST(TreeNode root, int val) {
    if (root == null) return new TreeNode(val);   // found insertion point
    if (val < root.val) root.left  = insertIntoBST(root.left,  val);
    else                root.right = insertIntoBST(root.right, val);
    return root;
}
```

---

### 49. Delete a Node in BST
**LeetCode #450 | Medium | Striver**

> 3 cases: leaf → remove. One child → replace. Two children → replace with inorder successor (min of right subtree).

```java
public TreeNode deleteNode(TreeNode root, int key) {
    if (root == null) return null;
    if (key < root.val)      root.left  = deleteNode(root.left,  key);
    else if (key > root.val) root.right = deleteNode(root.right, key);
    else {
        if (root.left  == null) return root.right;
        if (root.right == null) return root.left;
        TreeNode succ = root.right;
        while (succ.left != null) succ = succ.left;   // min of right subtree
        root.val   = succ.val;
        root.right = deleteNode(root.right, succ.val);
    }
    return root;
}
```

---

### 50. Kth Smallest and Largest Element in BST
**LeetCode #230 / GFG | Medium | Striver + ProPeers**

> Inorder = sorted ascending → kth smallest. Reverse inorder = descending → kth largest.

```java
private int k, result;

// Kth Smallest
public int kthSmallest(TreeNode root, int k) {
    this.k = k; inorder(root); return result;
}
private void inorder(TreeNode node) {
    if (node == null || k == 0) return;
    inorder(node.left);
    if (--k == 0) { result = node.val; return; }
    inorder(node.right);
}

// Kth Largest — reverse inorder
public int kthLargest(TreeNode root, int k) {
    this.k = k; reverseInorder(root); return result;
}
private void reverseInorder(TreeNode node) {
    if (node == null || k == 0) return;
    reverseInorder(node.right);
    if (--k == 0) { result = node.val; return; }
    reverseInorder(node.left);
}
```

---

### 51. Check if a Tree is a BST
**LeetCode #98 | Medium | Striver + ProPeers**

> Pass min and max bounds top-down. Every node must satisfy `min < val < max`. Use Long to avoid overflow.

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

### 52. LCA in BST
**LeetCode #235 | Medium | Striver + ProPeers**

> Both p,q < root → go left. Both > root → go right. Otherwise root is LCA.

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

### 53. Construct BST from Preorder Traversal
**LeetCode #1008 | Medium | Striver**

> Use upper bound: nodes > bound go to right subtree of some ancestor.

```java
int idx = 0;

public TreeNode bstFromPreorder(int[] preorder) {
    return build(preorder, Integer.MAX_VALUE);
}
private TreeNode build(int[] preorder, int bound) {
    if (idx == preorder.length || preorder[idx] > bound) return null;
    TreeNode root = new TreeNode(preorder[idx++]);
    root.left  = build(preorder, root.val);
    root.right = build(preorder, bound);
    return root;
}
```

---

### 54. Inorder Successor and Predecessor in BST
**GFG | Medium | Striver**

> Successor = leftmost in right subtree, or last ancestor where we went left. Predecessor = rightmost in left subtree, or last ancestor where we went right.

```java
public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
    TreeNode succ = null;
    while (root != null) {
        if (p.val < root.val) { succ = root; root = root.left; }   // candidate, go left for closer
        else root = root.right;
    }
    return succ;
}
public TreeNode inorderPredecessor(TreeNode root, TreeNode p) {
    TreeNode pred = null;
    while (root != null) {
        if (p.val > root.val) { pred = root; root = root.right; }  // candidate, go right for closer
        else root = root.left;
    }
    return pred;
}
```

```
BST:    20
       /  \
      8   22        successor(8)    = 12
     / \            predecessor(12) = 8
    4  12
```

---

## BST — FAQs

---

### 55. BST Iterator
**LeetCode #173 | Medium | Striver**

> next() gives smallest element, O(1) average time, O(h) space. Simulates iterative inorder.

```java
class BSTIterator {
    private Deque<TreeNode> stack = new ArrayDeque<>();
    public BSTIterator(TreeNode root) { pushLeft(root); }

    public int next() {
        TreeNode node = stack.pop();
        pushLeft(node.right);    // process right subtree's leftmost path
        return node.val;
    }
    public boolean hasNext() { return !stack.isEmpty(); }

    private void pushLeft(TreeNode node) {
        while (node != null) { stack.push(node); node = node.left; }
    }
}
```

---

### 56. Two Sum in BST
**LeetCode #653 | Easy | Striver + ProPeers**

> Find if two elements in BST sum to k.

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

### 57. Correct BST with Two Nodes Swapped
**LeetCode #99 | Hard | Striver + ProPeers**

> Two nodes swapped by mistake. Fix without changing structure.

**Core insight:** Inorder of valid BST is strictly increasing. Find the two out-of-order nodes → swap their values.

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
        if (first == null) first = prev;   // first violation: prev is wrong
        second = node;                      // always update second
    }
    prev = node;
    inorder(node.right);
}
```

```
Inorder (swapped): 1 → 6 → 3 → 4 → 5 → 2
                       ↑ first=6          ↑ second=2
After swap:        1 → 2 → 3 → 4 → 5 → 6  ✓
```

---

### 58. Largest BST in Binary Tree
**GFG / LeetCode #333 | Hard | Striver**

> Find the size of the largest subtree which is also a BST.

**Core insight:** Bottom-up DFS returning `{size, min, max}`. Return size=-1 if subtree is not a BST.

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

```
        10
       /  \
      5   15        Largest BST: subtree at 5 → [1,5,8]
     / \    \       size = 3 ✓
    1   8   7
```
