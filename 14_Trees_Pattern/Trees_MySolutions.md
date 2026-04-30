# Tree Problems — Solved Solutions

> **Language:** Java | **Source:** Striver + Code with Pratush
> **Main Notes File:** [striver_pratush_tree.md](./striver_pratush_tree.md)

---

## Table of Contents

### Binary Tree — Tree Traversal
- [1. Binary Tree Inorder Traversal — #94](#1-binary-tree-inorder-traversal--94)
- [2. Binary Tree Preorder Traversal — #144](#2-binary-tree-preorder-traversal--144)
- [3. Binary Tree Postorder Traversal — #145](#3-binary-tree-postorder-traversal--145)
- [4. Binary Tree Level Order Traversal — #102](#4-binary-tree-level-order-traversal--102)
- [5. Pre + Post + Inorder in One Traversal](#5-pre--post--inorder-in-one-traversal)
- [6. Binary Tree Zigzag Level Order Traversal — #103](#6-binary-tree-zigzag-level-order-traversal--103)
- [7. Binary Tree Level Order Traversal II — #107](#7-binary-tree-level-order-traversal-ii--107)

### Binary Tree — Mirror & Symmetry
- [8. Invert Binary Tree — #226](#8-invert-binary-tree--226)
- [9. Symmetric Tree — #101](#9-symmetric-tree--101)
- [10. Same Tree — #100](#10-same-tree--100)
- [11. Subtree of Another Tree — #572](#11-subtree-of-another-tree--572)

---

## Binary Tree — Tree Traversal

---

### 1. Binary Tree Inorder Traversal — #94
**Difficulty: Easy | Striver + Pratush**

> Return inorder traversal (Left → Root → Right) of a binary tree.

#### Approach 1 — Recursive
| TC | SC |
|----|----|
| O(n) | O(h) — recursion stack, h = height |

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        solve(root, ans);
        return ans;
    }

    private void solve(TreeNode node, List<Integer> ans) {
        if (node == null) return;
        solve(node.left, ans);
        ans.add(node.val);
        solve(node.right, ans);
    }
}
```

#### Approach 2 — Iterative using Stack (while true style)
| TC | SC |
|----|----|
| O(n) | O(h) — stack size |

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        TreeNode node = root;
        Deque<TreeNode> st = new ArrayDeque<>();

        while (true) {
            if (node != null) {
                st.push(node);
                node = node.left;
            } else {
                if (st.isEmpty()) break;
                node = st.pop();
                ans.add(node.val);
                node = node.right;
            }
        }
        return ans;
    }
}
```

#### Approach 3 — Iterative using Stack (cleaner while condition)
| TC | SC |
|----|----|
| O(n) | O(h) — stack size |

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        TreeNode node = root;
        Deque<TreeNode> st = new ArrayDeque<>();

        while (node != null || !st.isEmpty()) {
            while (node != null) {
                st.push(node);
                node = node.left;
            }
            node = st.pop();
            ans.add(node.val);
            node = node.right;
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

> **Note:** Approach 2 and 3 are same logic — Approach 3 is cleaner to read and preferred in interviews.

---

### 2. Binary Tree Preorder Traversal — #144
**Difficulty: Easy | Striver + Pratush**

> Return preorder traversal (Root → Left → Right) of a binary tree.

#### Approach 1 — Recursive
| TC | SC |
|----|----|
| O(n) | O(h) — recursion stack |

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        solve(root, ans);
        return ans;
    }

    private void solve(TreeNode node, List<Integer> ans) {
        if (node == null) return;
        ans.add(node.val);
        solve(node.left, ans);
        solve(node.right, ans);
    }
}
```

#### Approach 2 — Iterative using Stack
| TC | SC |
|----|----|
| O(n) | O(h) — stack size |

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        if (root == null) return ans;

        Deque<TreeNode> st = new ArrayDeque<>();
        st.push(root);

        while (!st.isEmpty()) {
            TreeNode node = st.pop();
            ans.add(node.val);

            if (node.right != null) st.push(node.right);  // right first (LIFO → left processed first)
            if (node.left  != null) st.push(node.left);
        }
        return ans;
    }
}
```

```
    1
   / \
  2   3        Preorder: [1, 2, 4, 5, 3] ✓
 / \
4   5
```

> **Key trick:** Push right before left in stack — since stack is LIFO, left gets processed first.

---

### 3. Binary Tree Postorder Traversal — #145
**Difficulty: Easy | Striver + Pratush**

> Return postorder traversal (Left → Right → Root) of a binary tree.

#### Approach 1 — Recursive
| TC | SC |
|----|----|
| O(n) | O(h) — recursion stack |

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        solve(root, ans);
        return ans;
    }

    private void solve(TreeNode node, List<Integer> ans) {
        if (node == null) return;
        solve(node.left, ans);
        solve(node.right, ans);
        ans.add(node.val);
    }
}
```

#### Approach 2 — Iterative using Stack + Collections.reverse()
| TC | SC |
|----|----|
| O(n) | O(n) — stack + result list |

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        Deque<TreeNode> st = new ArrayDeque<>();
        if (root != null) st.push(root);

        while (!st.isEmpty()) {
            TreeNode node = st.pop();
            ans.add(node.val);

            if (node.left  != null) st.push(node.left);   // left first → right processed first
            if (node.right != null) st.push(node.right);
        }
        Collections.reverse(ans);   // Root→Right→Left reversed = Left→Right→Root (postorder)
        return ans;
    }
}
```

#### Approach 3 — Iterative using Stack + addFirst() (no reverse needed)
| TC | SC |
|----|----|
| O(n) | O(n) — stack + result list |

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        LinkedList<Integer> ans = new LinkedList<>();
        Deque<TreeNode> st = new ArrayDeque<>();
        if (root != null) st.push(root);

        while (!st.isEmpty()) {
            TreeNode node = st.pop();
            ans.addFirst(node.val);    // prepend = same as reverse at end

            if (node.left  != null) st.push(node.left);
            if (node.right != null) st.push(node.right);
        }
        return ans;
    }
}
```

```
    1
   / \
  2   3        Postorder: [4, 5, 2, 3, 1] ✓
 / \
4   5
```

> **Core insight:** Postorder = reverse of (Root → Right → Left). So do a modified preorder (push left before right) and reverse the result. Approach 3 avoids the extra reverse using `addFirst()`.

---

### 4. Binary Tree Level Order Traversal — #102
**Difficulty: Medium | Striver + Pratush**

> Return nodes level by level (BFS).

#### Approach — BFS using Queue
| TC | SC |
|----|----|
| O(n) | O(n) — queue holds at most one full level at a time |

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ans = new ArrayList<>();
        Queue<TreeNode> q = new LinkedList<>();

        if (root != null) q.offer(root);

        while (!q.isEmpty()) {
            int size = q.size();             // snapshot of current level size — critical!
            List<Integer> level = new ArrayList<>();

            for (int i = 0; i < size; i++) {
                TreeNode node = q.poll();
                level.add(node.val);

                if (node.left  != null) q.offer(node.left);
                if (node.right != null) q.offer(node.right);
            }
            ans.add(level);
        }
        return ans;
    }
}
```

```
    3
   / \
  9  20          Output: [[3], [9,20], [15,7]] ✓
    /  \
   15   7
```

> **Key trick:** Snapshot `size = q.size()` before the inner loop — this separates one level from the next.

---

### 5. Pre + Post + Inorder in One Traversal
**Difficulty: Medium | Striver**

> Print all three traversals in a single DFS pass using a state variable per node.

#### Approach — Stack with NodeState (state = 1/2/3)
| TC | SC |
|----|----|
| O(n) | O(n) — stack holds all nodes |

```java
class NodeState {
    TreeNode node;
    int state;
    NodeState(TreeNode node, int state) {
        this.node = node;
        this.state = state;
    }
}

class Solution {
    List<List<Integer>> treeTraversal(TreeNode root) {
        List<Integer> pre  = new ArrayList<>();
        List<Integer> in   = new ArrayList<>();
        List<Integer> post = new ArrayList<>();

        if (root == null) return Arrays.asList(in, pre, post);

        Deque<NodeState> st = new ArrayDeque<>();
        st.push(new NodeState(root, 1));

        while (!st.isEmpty()) {
            NodeState curr = st.peek();
            TreeNode node  = curr.node;
            int state      = curr.state;

            if (state == 1) {
                pre.add(node.val);           // preorder: first visit
                curr.state = 2;
                if (node.left != null) st.push(new NodeState(node.left, 1));

            } else if (state == 2) {
                in.add(node.val);            // inorder: second visit
                curr.state = 3;
                if (node.right != null) st.push(new NodeState(node.right, 1));

            } else {
                post.add(node.val);          // postorder: third visit
                st.pop();
            }
        }
        return Arrays.asList(in, pre, post);
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

> **Core insight:** Each node is visited exactly 3 times. State controls which traversal it contributes to. State machine: 1 → preorder, 2 → inorder, 3 → postorder.

> **Note:** Uses `st.peek()` not `st.poll()` — we modify state in-place and only pop at state 3.

---

### 6. Binary Tree Zigzag Level Order Traversal — #103
**Difficulty: Medium | Striver + Pratush**

> Level order but alternate left-to-right and right-to-left each level.

#### Approach 1 — BFS + Index trick (nCopies + set by index)
| TC | SC |
|----|----|
| O(n) | O(n) — queue + level list |

```java
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;

        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        boolean leftToRight = true;

        while (!q.isEmpty()) {
            int size = q.size();
            List<Integer> level = new ArrayList<>(Collections.nCopies(size, 0));

            for (int i = 0; i < size; i++) {
                TreeNode node = q.poll();
                int index = leftToRight ? i : size - i - 1;   // place at correct position
                level.set(index, node.val);

                if (node.left  != null) q.offer(node.left);
                if (node.right != null) q.offer(node.right);
            }
            res.add(level);
            leftToRight = !leftToRight;
        }
        return res;
    }
}
```

#### Approach 2 — BFS + LinkedList addFirst/addLast (cleaner)
| TC | SC |
|----|----|
| O(n) | O(n) — queue + level list |

```java
class Solution {
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
                else             level.addFirst(node.val);  // reverse: prepend

                if (node.left  != null) q.offer(node.left);
                if (node.right != null) q.offer(node.right);
            }
            res.add(level);
            leftToRight = !leftToRight;
        }
        return res;
    }
}
```

```
    3
   / \
  9  20        Output: [[3], [20,9], [15,7]] ✓
    /  \
   15   7
```

> **Approach 2 preferred** — cleaner and avoids pre-allocating with nCopies.

---

### 7. Binary Tree Level Order Traversal II — #107
**Difficulty: Easy | Pratush**

> Same as level order but return bottom-up (deepest level first).

#### Approach 1 — BFS + add at index 0
| TC | SC |
|----|----|
| O(n²) | O(n) — ArrayList insert at 0 is O(n) each time |

```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
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
            res.add(0, level);   // prepend — O(n) per call
        }
        return res;
    }
}
```

#### Approach 2 — BFS + LinkedList addFirst (preferred — O(1) prepend)
| TC | SC |
|----|----|
| O(n) | O(n) |

```java
class Solution {
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
            res.addFirst(level);   // O(1) prepend using LinkedList
        }
        return res;
    }
}
```

> **Approach 2 preferred** — `LinkedList.addFirst()` is O(1) vs `ArrayList.add(0, x)` which is O(n).

---

## Binary Tree — Mirror & Symmetry

---

### 8. Invert Binary Tree — #226
**Difficulty: Easy | Pratush**

> Mirror a binary tree — swap left and right children at every node.

#### Approach 1 — Recursive (DFS)
| TC | SC |
|----|----|
| O(n) | O(h) — recursion stack |

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        TreeNode tmp  = root.left;
        root.left     = invertTree(root.right);
        root.right    = invertTree(tmp);
        return root;
    }
}
```

#### Approach 2 — Iterative BFS (Queue)
| TC | SC |
|----|----|
| O(n) | O(n) — queue holds one level at a time |

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);

        while (!q.isEmpty()) {
            TreeNode node = q.poll();

            TreeNode tmp  = node.left;
            node.left     = node.right;
            node.right    = tmp;

            if (node.left  != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
        return root;
    }
}
```

#### Approach 3 — Iterative DFS (Stack)
| TC | SC |
|----|----|
| O(n) | O(h) — stack |

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        Deque<TreeNode> stack = new ArrayDeque<>();
        stack.push(root);

        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();

            TreeNode tmp  = node.left;
            node.left     = node.right;
            node.right    = tmp;

            if (node.left  != null) stack.push(node.left);
            if (node.right != null) stack.push(node.right);
        }
        return root;
    }
}
```

```
     4                    4
   /   \      →         /   \
  2     7              7     2
 / \   / \            / \   / \
1   3 6   9          9   6 3   1
```

> **All 3 approaches do the same thing** — just swap left/right at every node. BFS and DFS differ only in traversal order, not correctness.

---

### 9. Symmetric Tree — #101
**Difficulty: Easy | Striver + Pratush**

> Check if a binary tree is a mirror image of itself.

#### Approach 1 — Recursive
| TC | SC |
|----|----|
| O(n) | O(h) — recursion stack |

```java
class Solution {
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
}
```

#### Approach 2 — Iterative BFS (Queue)
| TC | SC |
|----|----|
| O(n) | O(n) — queue |

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root.left);
        q.offer(root.right);

        while (!q.isEmpty()) {
            TreeNode left  = q.poll();
            TreeNode right = q.poll();

            if (left == null && right == null) continue;
            if (left == null || right == null) return false;
            if (left.val != right.val)         return false;

            q.offer(left.left);    // outer pair
            q.offer(right.right);

            q.offer(left.right);   // inner pair
            q.offer(right.left);
        }
        return true;
    }
}
```

#### Approach 3 — Iterative DFS (Stack)
| TC | SC |
|----|----|
| O(n) | O(h) — stack |

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        Deque<TreeNode> stack = new ArrayDeque<>();
        stack.push(root.left);
        stack.push(root.right);

        while (!stack.isEmpty()) {
            TreeNode right = stack.pop();
            TreeNode left  = stack.pop();

            if (left == null && right == null) continue;
            if (left == null || right == null) return false;
            if (left.val != right.val)         return false;

            // outer pair (pushed first, popped last)
            stack.push(left.left);
            stack.push(right.right);

            // inner pair
            stack.push(left.right);
            stack.push(right.left);
        }
        return true;
    }
}
```

```
        1
       / \
      2   2
     / \ / \        Symmetric ✓
    3  4 4  3

        1
       / \
      2   2
       \   \        Not Symmetric ✗
        3   3
```

> **Key trick:** Always process nodes in **pairs** — one from left side, one from right side. Queue/Stack always has an even number of elements.

---

### 10. Same Tree — #100
**Difficulty: Easy | Striver + Pratush**

> Check if two binary trees have same structure and node values.

#### Approach 1 — Recursive (verbose null check)
| TC | SC |
|----|----|
| O(n) | O(h) — recursion stack |

```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;
        if (p == null || q == null) return false;
        return p.val == q.val
            && isSameTree(p.left,  q.left)
            && isSameTree(p.right, q.right);
    }
}
```

#### Approach 2 — Recursive (compact null check)
| TC | SC |
|----|----|
| O(n) | O(h) |

```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null || q == null) return p == q;   // both null → true, one null → false
        return p.val == q.val
            && isSameTree(p.left,  q.left)
            && isSameTree(p.right, q.right);
    }
}
```

#### Approach 3 — Iterative DFS (Stack)
| TC | SC |
|----|----|
| O(n) | O(h) — stack |

```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        Deque<TreeNode> stack = new ArrayDeque<>();
        stack.push(p);
        stack.push(q);

        while (!stack.isEmpty()) {
            TreeNode n2 = stack.pop();
            TreeNode n1 = stack.pop();

            if (n1 == null && n2 == null) continue;
            if (n1 == null || n2 == null) return false;
            if (n1.val != n2.val)         return false;

            stack.push(n1.left);
            stack.push(n2.left);
            stack.push(n1.right);
            stack.push(n2.right);
        }
        return true;
    }
}
```

#### Approach 4 — Iterative BFS (Queue)
| TC | SC |
|----|----|
| O(n) | O(n) — queue |

```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(p);
        queue.offer(q);

        while (!queue.isEmpty()) {
            TreeNode n1 = queue.poll();
            TreeNode n2 = queue.poll();

            if (n1 == null && n2 == null) continue;
            if (n1 == null || n2 == null) return false;
            if (n1.val != n2.val)         return false;

            queue.offer(n1.left);
            queue.offer(n2.left);
            queue.offer(n1.right);
            queue.offer(n2.right);
        }
        return true;
    }
}
```

> **Approach 2 preferred** for interviews — compact and clean. Approach 3/4 show iterative thinking.

---

### 11. Subtree of Another Tree — #572
**Difficulty: Medium | Pratush**

> Check if `subRoot` is a subtree of `root`.

#### Approach 1 — Recursive DFS
| TC | SC |
|----|----|
| O(n × m) | O(h1 + h2) — two recursion stacks |

> n = nodes in root, m = nodes in subRoot, h1/h2 = heights

```java
class Solution {
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if (subRoot == null) return true;
        if (root == null)    return false;

        return isSameTree(root, subRoot)
            || isSubtree(root.left,  subRoot)
            || isSubtree(root.right, subRoot);
    }

    private boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null || q == null) return p == q;
        return p.val == q.val
            && isSameTree(p.left,  q.left)
            && isSameTree(p.right, q.right);
    }
}
```

#### Approach 2 — Iterative BFS (outer) + BFS (isSameTree)
| TC | SC |
|----|----|
| O(n × m) | O(n + m) — two queues |

```java
class Solution {
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if (subRoot == null) return true;
        if (root == null)    return false;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            if (isSameTree(node, subRoot)) return true;
            if (node.left  != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }
        return false;
    }

    private boolean isSameTree(TreeNode p, TreeNode q) {
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(p);
        queue.offer(q);

        while (!queue.isEmpty()) {
            TreeNode n1 = queue.poll();
            TreeNode n2 = queue.poll();
            if (n1 == null && n2 == null) continue;
            if (n1 == null || n2 == null) return false;
            if (n1.val != n2.val)         return false;
            queue.offer(n1.left);  queue.offer(n2.left);
            queue.offer(n1.right); queue.offer(n2.right);
        }
        return true;
    }
}
```

#### Approach 3 — Iterative DFS (outer) + DFS (isSameTree)
| TC | SC |
|----|----|
| O(n × m) | O(n + m) — two stacks |

```java
class Solution {
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if (subRoot == null) return true;
        if (root == null)    return false;

        Deque<TreeNode> stack = new ArrayDeque<>();
        stack.push(root);

        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            if (isSameTree(node, subRoot)) return true;
            if (node.right != null) stack.push(node.right);
            if (node.left  != null) stack.push(node.left);
        }
        return false;
    }

    private boolean isSameTree(TreeNode p, TreeNode q) {
        Deque<TreeNode> stack = new ArrayDeque<>();
        stack.push(p);
        stack.push(q);

        while (!stack.isEmpty()) {
            TreeNode n2 = stack.pop();
            TreeNode n1 = stack.pop();
            if (n1 == null && n2 == null) continue;
            if (n1 == null || n2 == null) return false;
            if (n1.val != n2.val)         return false;
            stack.push(n1.right); stack.push(n2.right);
            stack.push(n1.left);  stack.push(n2.left);
        }
        return true;
    }
}
```

```
root:           subRoot:
     3               4
    / \             / \
   4   5           1   2
  / \
 1   2

isSubtree(root, subRoot) = true ✓  (subtree rooted at 4 matches)
```

> **Approach 1 preferred** — cleaner and easier to explain in interviews.
> All three are O(n × m) — no way to avoid checking every node of root against subRoot.


12. 951. Flip Equivalent Binary Trees


class Solution {
    public boolean flipEquiv(TreeNode root1, TreeNode root2) {
        if(root1==null || root2==null) {
            return root1 == root2;
        }

        if(root1.val != root2.val){
            return false;
        }

        boolean noFlip = flipEquiv(root1.left,root2.left) && flipEquiv(root1.right, root2.right);
        boolean flip = flipEquiv(root1.left,root2.right) && flipEquiv(root1.right,root2.left);

        return flip || noFlip;
        
    }
}

//Iterative BFS (Queue)
class Solution {
    public boolean flipEquiv(TreeNode root1, TreeNode root2) {

        Queue<TreeNode[]> queue = new LinkedList<>();
        queue.offer(new TreeNode[]{root1, root2});

        while (!queue.isEmpty()) {

            TreeNode[] pair = queue.poll();

            TreeNode a = pair[0];
            TreeNode b = pair[1];

            if (a == null && b == null) continue;
            if (a == null || b == null) return false;
            if (a.val != b.val) return false;

            boolean noFlip =
                isMatch(a.left, b.left) &&
                isMatch(a.right, b.right);

            boolean flip =
                isMatch(a.left, b.right) &&
                isMatch(a.right, b.left);

            if (!noFlip && !flip) return false;

            if (noFlip) {
                queue.offer(new TreeNode[]{a.left, b.left});
                queue.offer(new TreeNode[]{a.right, b.right});
            } else {
                queue.offer(new TreeNode[]{a.left, b.right});
                queue.offer(new TreeNode[]{a.right, b.left});
            }
        }

        return true;
    }

    private boolean isMatch(TreeNode x, TreeNode y) {
        if (x == null && y == null) return true;
        if (x == null || y == null) return false;
        return x.val == y.val;
    }
}

//Iterative DFS (Stack)
class Solution {
    public boolean flipEquiv(TreeNode root1, TreeNode root2) {
        Deque<TreeNode[]> stack = new ArrayDeque<>();
        stack.push(new TreeNode[]{root1, root2});

        while (!stack.isEmpty()) {

            TreeNode[] pair = stack.pop();

            TreeNode a = pair[0];
            TreeNode b = pair[1];

            if (a == null && b == null) continue;
            if (a == null || b == null) return false;
            if (a.val != b.val) return false;

            // Check no-flip possibility
            boolean noFlip =
                isMatch(a.left, b.left) &&
                isMatch(a.right, b.right);

            // Check flip possibility
            boolean flip =
                isMatch(a.left, b.right) &&
                isMatch(a.right, b.left);

            if (!noFlip && !flip) return false;

            if (noFlip) {
                stack.push(new TreeNode[]{a.left, b.left});
                stack.push(new TreeNode[]{a.right, b.right});
            } else {
                stack.push(new TreeNode[]{a.left, b.right});
                stack.push(new TreeNode[]{a.right, b.left});
            }
        }

        return true;
    }

    private boolean isMatch(TreeNode x, TreeNode y) {
        if (x == null && y == null) return true;
        if (x == null || y == null) return false;
        return x.val == y.val;
    }
}

13. 104. Maximum Depth of Binary Tree
class Solution {
    public int maxDepth(TreeNode root) {
        if(root==null) return 0;

        int lh = maxDepth(root.left);
        int rh = maxDepth(root.right);

        return 1+Math.max(lh,rh);
        
    }
}

class Solution {
    public int maxDepth(TreeNode root) {
        if(root==null) return 0;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int depth = 0;

        while(!queue.isEmpty()){
            int size = queue.size();
            depth++;
            for(int i=0;i<size;i++){
                TreeNode node = queue.poll();

                if(node.left!=null) queue.offer(node.left);
                if(node.right!=null) queue.offer(node.right);
            }
        }
        return depth;
        
    }
}


14. Check for balanced binary tree


class Solution {
    public boolean isBalanced(TreeNode root) {
        if(root==null) return true;
        int lh = height(root.left);
        int rh = height(root.right);

        if(Math.abs(rh-lh)>1) return false;

        return isBalanced(root.left) && isBalanced(root.right);
	}


    private int height(TreeNode node){
        if(node==null) return 0;

        return 1+Math.max(height(node.left),height(node.right));  
    }
}


class Solution {
    public boolean isBalanced(TreeNode root) {

        return dfsHeight(root)!=-1;
	}


    private int dfsHeight(TreeNode node){
        if(node==null)return 0;
        int lh = dfsHeight(node.left);
        if(lh==-1) return -1;
        int rh = dfsHeight(node.right);
        if(rh==-1) return -1;

        if(Math.abs(lh-rh)>1) return -1;
        return 1+Math.max(lh,rh);
    
    }
}


15. Diameter of Binary Tree

class Solution {
    int diameter = 0;
    public int diameterOfBinaryTree(TreeNode root) {
        height(root);
        return diameter;
    }

    private int height(TreeNode root){
        if(root==null) return 0;

        int lh = height(root.left);
        int rh = height(root.right);

        diameter = Math.max(lh+rh, diameter);

        return 1+ Math.max(lh,rh);
    }
}

class Solution {
    public int diameterOfBinaryTree(TreeNode root) {
        if(root==null) return 0;

        int lh = height(root.left);
        int rh = height(root.right);
        
        int ld = diameterOfBinaryTree(root.left);
        int rd = diameterOfBinaryTree(root.right);

        return Math.max(lh+rh, Math.max(ld,rd));

        
    }

    private int height(TreeNode node){
        if(node==null) return 0;

        return 1+ Math.max(height(node.left),height(node.right));
    }
}


class Solution {
    public int diameterOfBinaryTree(TreeNode root) {
       int ans [] = new int[1];
       ans[0] = 0;
       height(root,ans);
       return ans[0];     
    }

    private int height(TreeNode node, int ans[]){
        if(node==null) return 0;

        int lh[] = new int[1];
        int rh[] = new int[1];

        lh[0] = height(node.left,ans);
        rh[0] = height(node.right,ans);

        ans[0] = Math.max(lh[0]+rh[0],ans[0]);

        return 1+ Math.max(lh[0],rh[0]);
    }
}
16. 124. Binary Tree Maximum Path Sum

class Solution {
    int maxSum = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        findMaxPathSum(root);
        return maxSum;
        
    }

    private int findMaxPathSum(TreeNode root){
        if(root == null) return 0;

        int leftSum = Math.max(0, findMaxPathSum(root.left));
        int rightSum = Math.max(0, findMaxPathSum(root.right));

        maxSum = Math.max(maxSum, leftSum + rightSum + root.val);

        return root.val + Math.max(leftSum, rightSum);
    }
}


17. Boundary Traversal

class Solution {
    public List<Integer> boundary(TreeNode root) {
        //your code goes here
        List<Integer> ans = new ArrayList<>();
        if(root==null) return ans;

        if(!isLeaf(root)){
            ans.add(root.data);
        }
        addLeftBoundary(root,ans);
        addLeaves(root, ans);
        addRightBoundary(root,ans);

        return ans;
    }

    private void addLeftBoundary(TreeNode root, List<Integer> ans){
        TreeNode curr = root.left;

        while(curr!=null){
            if(!isLeaf(curr)) {
                ans.add(curr.data);
            }

            if(curr.left!=null){
                curr = curr.left;
            }else{
                curr = curr.right;
            }
        }
    }

    private void addRightBoundary(TreeNode root, List<Integer>ans){
        TreeNode curr = root.right;

        List<Integer> temp = new ArrayList<>();
        while(curr!=null){
            if(!isLeaf(curr)){
                temp.add(curr.data);
            }

            if(curr.right!=null){
                curr = curr.right;
            }else{
                curr = curr.left;
            }
        }

        for(int i=temp.size()-1;i>=0;i--){
            ans.add(temp.get(i));
        }
    }

    private void addLeaves(TreeNode root, List<Integer> ans){
        if(isLeaf(root)){
            ans.add(root.data);
            return ;
        }

        if(root.left!=null){
            addLeaves(root.left,ans);
        }

        if(root.right!=null){
            addLeaves(root.right,ans);
        }
    }

    public boolean isLeaf(TreeNode node){
        return node.left==null && node.right==null;
    }
}


18. 987. Vertical Order Traversal of a Binary Tree


 class Tuple{
    TreeNode node;
    int x; // vertical distance
    int y; // level

    Tuple(TreeNode node, int x, int y){
        this.node = node;
        this.x = x;
        this.y = y;
    }
 }
class Solution {
    public List<List<Integer>> verticalTraversal(TreeNode root) {
        List<List<Integer>> ans = new ArrayList<>();

        if(root == null) return ans;

        TreeMap<Integer, TreeMap<Integer, PriorityQueue<Integer>>> nodesMap = new TreeMap<>();

        Queue<Tuple> queue = new LinkedList<>();
        queue.offer(new Tuple(root, 0, 0));

        while(!queue.isEmpty()){
            Tuple tuple = queue.poll();
            TreeNode node = tuple.node;
            int x = tuple.x;
            int y = tuple.y;

            nodesMap.putIfAbsent(x,new TreeMap<>());
            nodesMap.get(x).putIfAbsent(y, new PriorityQueue<>());

            nodesMap.get(x).get(y).offer(node.val);

            if(node.left != null){
                queue.offer(new Tuple(node.left, x-1, y+1));
            }

            if(node.right != null){
                queue.offer(new Tuple(node.right, x+1, y+1));
            }
        }

        for(TreeMap<Integer, PriorityQueue<Integer>> yMap : nodesMap.values()){
            List<Integer> cols = new ArrayList<>();

            for(PriorityQueue<Integer> nodes : yMap.values()){
                while(!nodes.isEmpty()){
                    cols.add(nodes.poll());
                }
            }
            ans.add(cols);
        }

        return ans;
        
    }
}

19. Bottom view of BT


class Solution {
    static class Pair< K, V >{
        private K key;
        private V value;

        public Pair(K key, V value){
            this.key = key;
            this.value = value;
        }

        public K getKey(){
            return key;
        }

        public V getValue(){
            return value;
        }
    }
    public List<Integer> topView(TreeNode root) {
        //your code goes here
        List<Integer> ans = new ArrayList<>();

        if(root==null){
            return ans;
        }

        Map<Integer,Integer> map = new TreeMap<>();

        Queue<Pair<TreeNode, Integer>> q = new LinkedList<>();

        q.offer(new Pair<>(root,0));

        while(!q.isEmpty()){
            Pair<TreeNode, Integer> it = q.poll();
            TreeNode node = it.getKey();
            int line = it.getValue();

            if(!map.containsKey(line)){
                map.put(line, node.data);
            }

            if(node.left!=null){
                q.offer(new Pair<>(node.left, line-1));
            }

            if(node.right!=null){
                q.offer(new Pair<>(node.right, line+1));
            }
        }

        for(Integer value : map.values()){
            ans.add(value);
        }

        return ans;
    }   
}

20. Bottom view of BT


class Solution {
       static class Pair<K, V>{
        private K key;
        private V value;
        
        public Pair(K key, V value){
            this.key = key;
            this.value = value;
        }
        
        public K getKey(){
            return key;
        }
        
        public V getValue(){
            return value;
        }
    }

    public List<Integer> bottomView(TreeNode root) {
        //your code goes here
        ArrayList<Integer> ans = new ArrayList<>();
        
        if(root == null){
            return ans;
        }
        
        Map<Integer, Integer> map = new TreeMap<>();
        
        Queue<Pair<TreeNode, Integer>> queue = new LinkedList<>();
        queue.offer(new Pair<>(root,0));
        
        while(!queue.isEmpty()){
            Pair<TreeNode, Integer> it = queue.poll();
            TreeNode node = it.getKey();
            int line = it.getValue();
            
            map.put(line, node.data);
            
            if(node.left!=null){
                queue.offer(new Pair<>(node.left, line-1));
            }
            
            if(node.right!=null){
                queue.offer(new Pair<>(node.right, line+1));
            }
        }
        
        for(Integer value : map.values()){
            ans.add(value);
        }
        return ans;
    }
}


class Solution {

    public List<Integer> bottomView(TreeNode root) {
        //your code goes here
        ArrayList<Integer> ans = new ArrayList<>();
        
        if(root == null){
            return ans;
        }
        
        Map<Integer, Integer> map = new TreeMap<>();
        
        Queue<Map.Entry<TreeNode, Integer>> queue = new LinkedList<>();
        queue.offer(new AbstractMap.SimpleEntry<>(root,0));
        
        while(!queue.isEmpty()){
            Map.Entry<TreeNode, Integer> it = queue.poll();
            TreeNode node = it.getKey();
            int line = it.getValue();
            
            map.put(line, node.data);
            
            if(node.left!=null){
                queue.offer(new AbstractMap.SimpleEntry<>(node.left, line-1));
            }
            
            if(node.right!=null){
                queue.offer(new AbstractMap.SimpleEntry<>(node.right, line+1));
            }
        }
        
        for(Integer value : map.values()){
            ans.add(value);
        }
        return ans;
    }
}

21. Right View of BT


class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        rightView(root, ans, 0);
        return ans;
        
    }

    private void rightView(TreeNode node, List<Integer> ans, int currDepth){
        if(node == null){
            return ;
        }

        if(currDepth == ans.size()){
            ans.add(node.val);
        }

        rightView(node.right, ans, currDepth+1);
        rightView(node.left, ans, currDepth+1);
    }
}

22. Left View of BT

class Solution {
    public ArrayList<Integer> leftView(Node root) {
        // code here
        ArrayList<Integer> ans = new ArrayList<>();
        
        leftSideView(root, ans, 0);
        
        return ans;
    }
    
    private void leftSideView(Node node, ArrayList<Integer> ans, int currDepth){
        if(node == null ){
            return ;
        }
        
        if(currDepth == ans.size()){
            ans.add(node.data);
        }
        
        leftSideView(node.left, ans, currDepth+1);
        leftSideView(node.right, ans, currDepth+1);
    }
}

23. Print root to leaf path in BT

class Solution {
    public List<List<Integer>> allRootToLeaf(TreeNode root) {
        //your code goes here
        List<List<Integer>> allPaths = new ArrayList<>();

        List<Integer> path = new ArrayList<>();

        dfs(root,path,allPaths);
        return allPaths;
    }

    private void dfs(TreeNode node, List<Integer> path, List<List<Integer>> allPaths){
        if(node==null) {
            return ;
        }

        path.add(node.data);

        if(node.left==null && node.right==null){
            allPaths.add(new ArrayList<>(path));
        }else{
            dfs(node.left, path, allPaths);
            dfs(node.right, path, allPaths);
        }

        path.remove(path.size()-1);
    }
}

24. LCA in BT
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // base case
        if (root == null || root == p || root == q) {
            return root;
        }

        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);

        // if one side is null → return the other
        if (left == null) return right;
        if (right == null) return left;

        // both sides non-null → this is LCA
        return root;
    }
}

25. Maximum Width of BT
class Pair {
    TreeNode node;
    int index;

    Pair(TreeNode node, int index) {
        this.node = node;
        this.index = index;
    }
}

class Solution {
    public int widthOfBinaryTree(TreeNode root) {
        if (root == null) return 0;

        long ans = 0;
        Queue<Pair> queue = new LinkedList<>();
        queue.offer(new Pair(root, 0));

        while (!queue.isEmpty()) {
            int size = queue.size();
            int min = queue.peek().index;

            long first = 0, last = 0;

            for (int i = 0; i < size; i++) {
                Pair p = queue.poll();
                TreeNode node = p.node;
                int curr = p.index - min;

                if (i == 0) first = curr;
                if (i == size - 1) last = curr;

                if (node.left != null) {
                    queue.offer(new Pair(node.left, 2 * curr + 1));
                }
                if (node.right != null) {
                    queue.offer(new Pair(node.right, 2 * curr + 2));
                }
            }

            ans = Math.max(ans, last - first + 1);
        }

        return (int) ans;
    }
}

 import java.util.AbstractMap;
class Solution {
    public int widthOfBinaryTree(TreeNode root) {
        int ans = 0;

        Queue<Map.Entry<TreeNode, Integer>> queue = new LinkedList<>();

        if(root != null ){
            queue.offer(new AbstractMap.SimpleEntry<>(root,0));
        }

        while(!queue.isEmpty()){
            int size = queue.size();
            int minLine = queue.peek().getValue();
            int first = 0, last = 0;

            for(int i=0; i<size; i++){
                Map.Entry<TreeNode,Integer> entry = queue.poll();

                TreeNode node = entry.getKey();
                int currLine = entry.getValue() - minLine;

                if(i == 0) first = currLine;
                if(i == size-1) last = currLine;

                if(node.left!=null){
                    queue.offer(new AbstractMap.SimpleEntry<>(node.left, 2*currLine + 1));
                }

                if(node.right!=null){
                    queue.offer(new AbstractMap.SimpleEntry<>(node.right, 2*currLine + 2));
                }
            }
            ans = Math.max(ans, last-first+1);
        }
        return ans; 
    }
}

26. Print all nodes at a distance of K in BT

27. Minimum time taken to burn the BT from a given Node

28. Count total nodes in a complete BT

29. Requirements needed to construct a unique BT

30. Construct a BT from Preorder and Inorder

31. Construct a BT from Postorder and Inorder

32. Serialize and De-serialize BT

33. Morris Inorder Traversal

34. Morris Preorder Traversal

35. Search in BST


36. Floor in a BST

37. Ceil in a BST

38. Insert a given node in BST

39. Delete a node in BST

40. Kth Smallest element in BST (Kth Smallest and Largest element in BST)

41. Kth Largest element in BST

42. Check if a tree is a BST or not

43. LCA in BST

44. Construct a BST from a preorder traversal

45. Inorder successor and predecessor in BST

46. BST iterator

47. Two sum in BST

48. Correct BST with two nodes swapped

49. Largest BST in Binary Tree

50.

