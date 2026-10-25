Priority 4: Trees + BFS
Ek candidate ne explicitly tree-based BFS report kiya tha.

Questions:
1. Binary Tree Level Order Traversal
2. Maximum Depth of Binary Tree
3. Binary Tree Right Side View
4. Binary Tree Zigzag Level Order Traversal
Resources:
- LeetCode 102 — Binary Tree Level Order Traversal
- LeetCode — Tree problems

1. Binary Tree Level Order Traversal
```
https://takeuforward.org/practice/dsa/level-order-traversal
https://leetcode.com/problems/binary-tree-level-order-traversal/description/
```

```java
public List<List<Integer>> levelOrder(TreeNode root) {
        // Create a list to store the levels
        List<List<Integer>> ans = new ArrayList<>();
        if (root == null) {
            // If the tree is empty, return an empty list
            return ans;
        }
        
        // Create a queue to store nodes for level-order traversal
        Queue<TreeNode> q = new LinkedList<>();
        // Add the root node to the queue
        q.add(root);
        
        while (!q.isEmpty()) {
            // Get the size of the current level
            int size = q.size();
            // Create a list to store nodes at the current level
            List<Integer> level = new ArrayList<>();
            
            for (int i = 0; i < size; i++) {
                // Get the front node from the queue
                TreeNode node = q.poll();
                // Add the node value to the current level list
                level.add(node.data);
                
                // Enqueue the child nodes if they exist
                if (node.left != null) {
                    q.add(node.left);
                }
                if (node.right != null) {
                    q.add(node.right);
                }
            }
            // Add the current level to the answer list
            ans.add(level);
        }
        // Return the level-order traversal of the tree
        return ans;
    }
Time Complexity: O(N)
Space Complexity: O(N) 
```

2. Maximum Depth of Binary Tree
```
https://leetcode.com/problems/maximum-depth-of-binary-tree/description/
https://takeuforward.org/practice/dsa/maximum-depth-in-bt
```

```java
public int maxDepth(TreeNode root) {
        // Base case: if the node is null, return 0
        if (root == null) {
            return 0;
        }
        // Recursively find the depth of the left and right subtrees
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        // The depth of the tree is 1 current node + the maximum depth of the subtrees
        return 1 + Math.max(left, right);
    }
Time Complexity: O(N),
Space Complexity: O(h)
```

```java
public int maxDepth(TreeNode root) {
        // If the tree is empty, return 0
        if (root == null) {
            return 0;
        }
 
        // Create a queue to hold nodes to be processed
        Queue<TreeNode> q = new LinkedList<>();
        // Push the root node into the queue
        q.add(root);
        // Initialize level to 0
        int level = 0;
 
        // While there are nodes in the queue
        while (!q.isEmpty()) {
            // Get the number of nodes at the current level
            int size = q.size();
 
            // Process all nodes at the current level
            for (int i = 0; i < size; i++) {
                // Get the front node in the queue
                TreeNode front = q.poll();
 
                // Enqueue left child if it exists
                if (front.left != null) {
                    q.add(front.left);
                }
 
                // Enqueue right child if it exists
                if (front.right != null) {
                    q.add(front.right);
                }
            }
            // Increment level to move to the next level
            level++;
        }
 
        // Return the maximum depth
        return level;
    }
Time Complexity: O(N), the iterative solution processes each node once, resulting in O(n) time complexity.

Space Complexity: O(w), where w is the maximum width of the tree
```


3. Binary Tree Right Side View
```
https://leetcode.com/problems/binary-tree-right-side-view/description/
https://takeuforward.org/practice/dsa/right-left-view-of-bt
```

```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> ans = new ArrayList<>();

        if(root == null){
            return ans;
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while(!queue.isEmpty()){
            int size = queue.size();

            for(int i=0; i<size; i++){
                TreeNode node = queue.poll();

                if(i == size-1){
                    ans.add(node.val);
                }

                if(node.left != null){
                    queue.offer(node.left);
                }

                if(node.right != null){
                    queue.offer(node.right);
                }

            }
        }

        return ans;
    }
}
```

```java
public List<Integer> rightSideView(TreeNode root) {
        List<Integer> res = new ArrayList<>();

        // Get the level order traversal of the tree
        List<List<Integer>> levelTraversal = levelOrder(root);

        // Iterate through each level and add the last element to the result
        for (List<Integer> level : levelTraversal) {
            res.add(level.get(level.size() - 1));
        }

        return res;
    }

    // Function to return the Left view of the binary tree
    public List<Integer> leftSideView(TreeNode root) {
        List<Integer> res = new ArrayList<>();

        // Get the level order traversal of the tree
        List<List<Integer>> levelTraversal = levelOrder(root);

        // Iterate through each level and add the first element to the result
        for (List<Integer> level : levelTraversal) {
            res.add(level.get(0));
        }

        return res;
    }

    // Function that returns the level order traversal of a Binary tree 
    private List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ans = new ArrayList<>();

        // Return an empty list if the tree is empty
        if (root == null) {
            return ans;
        }

        // Use a queue to perform level order traversal
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);

        while (!q.isEmpty()) {
            int size = q.size();
            List<Integer> level = new ArrayList<>();

            // Process each node in the current level
            for (int i = 0; i < size; i++) {
                TreeNode top = q.poll();
                level.add(top.data);

                // Enqueue the left child if it exists
                if (top.left != null) {
                    q.add(top.left);
                }

                // Enqueue the right child if it exists
                if (top.right != null) {
                    q.add(top.right);
                }
            }

            // Add the current level to the result
            ans.add(level);
        }

        return ans;
    }
Time Complexity: O(N)
Space Complexity: O(N)
```

```java
public List<Integer> rightSideView(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        
        // Call the recursive function to populate the right-side view
        recursionRight(root, 0, res);
        
        return res;
    }
 
    // Function to return the Left view of the binary tree
    public List<Integer> leftSideView(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        
        // Call the recursive function to populate the left-side view
        recursionLeft(root, 0, res);
        
        return res;
    }
 
    // Recursive function to traverse the binary tree and populate the left-side view
    private void recursionLeft(TreeNode root, int level, List<Integer> res) {
        // Check if the current node is NULL
        if (root == null) {
            return;
        }
        
        // Check if the size of the result list is equal to the current level
        if (res.size() == level) {
            // If equal, add the value of the current node to the result list
            res.add(root.data);
        }
        
        // Recursively call the function for the left child with an increased level
        recursionLeft(root.left, level + 1, res);
        
        // Recursively call the function for the right child with an increased level
        recursionLeft(root.right, level + 1, res);
    }
 
    // Recursive function to traverse the binary tree and populate the right-side view
    private void recursionRight(TreeNode root, int level, List<Integer> res) {
        // Check if the current node is NULL
        if (root == null) {
            return;
        }
        
        // Check if the size of the result list is equal to the current level
        if (res.size() == level) {
            // If equal, add the value of the current node to the result list
            res.add(root.data);
        }
        
        // Recursively call the function for the right child with an increased level
        recursionRight(root.right, level + 1, res);
        
        // Recursively call the function for the left child with an increased level
        recursionRight(root.left, level + 1, res);
    }
Time Complexity: O(N)
Space Complexity: O(H),
```




4. Binary Tree Zigzag Level Order Traversal
```
https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/description/
https://www.geeksforgeeks.org/problems/zigzag-tree-traversal/1
```

```java

```

```java

```

```java

```

