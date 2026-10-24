# Priority 3: Linked List + Queue
## Questions:
```
1. Reverse Linked List
2. Detect Cycle in Linked List
3. Implement Queue using Linked List
4. Circular Linked List
5. Merge Two Sorted Lists
```

```
Resources:
- LeetCode — Linked List problems
- GeeksforGeeks — Queue using Linked List
```

1. Reverse Linked List
```
https://leetcode.com/problems/reverse-linked-list/description/
https://takeuforward.org/practice/dsa/reverse-a-ll
```

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null, curr = head;

        while(curr != null){
            ListNode next = curr.next;

            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
}
Time Complexity: O(N) 
Space Complexity: O(1)
```

```java
//Recursive Approach
public ListNode reverseList(ListNode head) {
        /* Base case:
        If the linked list is empty or has only one node,
        return the head as it is already reversed. */
        if (head == null || head.next == null) {
            return head;
        }
        
        /* Recursive step:
        Reverse the linked list starting 
        from the second node (head.next). */
        ListNode newHead = reverseList(head.next);
        
        /* Save a reference to the node following
        the current 'head' node. */
        ListNode front = head.next;
        
        /* Make the 'front' node point 
        to the current
        'head' node in the 
        reversed order. */
        front.next = head;
        
        /* Break the link from 
        the current 'head' node
        to the 'front' node 
        to avoid cycles. */
        head.next = null;
        
        /* Return the 'newHead,' 
        which is the new
        head of the reversed 
        linked list. */
        return newHead;
    }
Time Complexity: O(N)
Space Complexity: O(N)
```

2. Detect Cycle in Linked List

```
https://leetcode.com/problems/linked-list-cycle/description/
https://takeuforward.org/practice/dsa/detect-a-loop-in-ll
```

```java
Brute:
// Function to detect a loop in the linked list
    public boolean hasCycle(ListNode head) {
        // Initialize a pointer 'temp'
        // At the head of the linked list
        ListNode temp = head;  
 
        // Create a set to keep track of
        // Encountered nodes
        HashSet<ListNode> nodeSet = new HashSet<>();  
 
        // Traverse the linked list
        while (temp != null) {
            // If the node is already in the
            // Set, there is a loop
            if (nodeSet.contains(temp)) {
                return true;
            }
            // Store the current node
            // In the set
            nodeSet.add(temp);
            
            // Move to the next node
            temp = temp.next;  
        }
 
        // If the list is successfully traversed 
        // Without a loop, return false
        return false;
    }
Time Complexity: O(N)
Space Complexity: O(N)
```

```java
Optimal:
public boolean hasCycle(ListNode head) {
        // Initialize two pointers, slow and fast,
        // to the head of the linked list
        ListNode slow = head;
        ListNode fast = head;
 
        // Step 2: Traverse the linked list with
        // the slow and fast pointers
        while (fast != null && fast.next != null) {
            // Move slow one step
            slow = slow.next;
            // Move fast two steps
            fast = fast.next.next;
 
            // Check if slow and fast pointers meet
            if (slow == fast) {
                return true;  // Loop detected
            }
        }
 
        // If fast reaches the end of the list,
        // there is no loop
        return false;
    }
Time Complexity: O(N)
Space Complexity: O(1)
```

3. Implement Queue using Linked List
```

```

```java

```

```java

```

```java

```

4. Circular Linked List
```

```

```java

```

```java

```

```java

```

5. Merge Two Sorted Lists
```

```

```java

```

```java

```

```java

```
