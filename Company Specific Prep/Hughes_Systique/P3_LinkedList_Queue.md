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
https://www.geeksforgeeks.org/dsa/circular-linked-list/
https://www.geeksforgeeks.org/dsa/insertion-at-the-beginning-in-circular-linked-list/
https://www.geeksforgeeks.org/dsa/insertion-at-the-end-in-circular-linked-list/
https://www.geeksforgeeks.org/dsa/insertion-at-specific-position-in-circular-linked-list-1/
https://www.geeksforgeeks.org/dsa/deletion-circular-linked-list/
https://www.geeksforgeeks.org/problems/circular-linked-list-traversal/1

```

```java
//Insertion at the beginning in circular linked list
static Node insertAtBeginning(Node last, int key) {
        Node newNode = new Node(key);

        if (last == null) {
            newNode.next = newNode;
            return newNode;
        }

        newNode.next = last.next;
        last.next = newNode;

        return last;
    }
Time Complexity: O(1)
Auxiliary Space: O(1)
```

```java
//Insertion at the End in Circular Linked List - O(n) Time and O(1) Space
public static Node insertAtEnd(Node head, int key) {

        // Create a new node with the given key.
        Node newNode = new Node(key);

        // If the circular linked list is empty,
        // make the new node point to itself.
        if (head == null) {
            newNode.next = newNode;
            return newNode;
        }

        // Find the tail of the circular linked list.
        Node tail = head;
        while (tail.next != head) {
            tail = tail.next;
        }

        // Insert the new node after the tail
        // and before the head.
        newNode.next = head;
        tail.next = newNode;

        // Head remains unchanged.
        return head;
    }
```

```java
//Insertion at specific position in circular linked list
// Function to insert a node at a specific position in a circular linked list
    public static Node insertAtPosition(Node last, int data, int pos) {
        if (last == null) {
            // If the list is empty
            if (pos != 1) {
                System.out.println("Invalid position!");
                return last;
            }
            // Create a new node and make it point to itself
            Node newNode = new Node(data);
            last = newNode;
            last.next = last;
            return last;
        }

        // Create a new node with the given data
        Node newNode = new Node(data);

        // curr will point to head initially
        Node curr = last.next;

        if (pos == 1) {
            // Insert at the beginning
            newNode.next = curr;
            last.next = newNode;
            return last;
        }

        // Traverse the list to find the insertion point
        for (int i = 1; i < pos - 1; ++i) {
            curr = curr.next;
            // If position is out of bounds (beyond the circular linked list)
            if (curr == last) {
                System.out.println("Invalid position!");
                return last;
            }
        }
        // Insert the new node at the desired position
        newNode.next = curr.next;
        curr.next = newNode;

        // Update last if the new node is inserted at the end
        if (curr == last) {
            last = newNode;
        }

        return last;
    }

Time Complexity: O(n), we have to traverse the list to find the specific position.
Auxiliary Space: O(1)
```

```java
//Deletion from the beginning of the circular linked list - O(1) Time and O(1) Space

public static Node deleteFirstNode(Node last) {
        if (last == null) {
            
            // If the list is empty
            System.out.println("List is empty");
            return null;
        }

        Node head = last.next;

        if (head == last) {
        
            // If there is only one node in the list
            last = null;
        } else {
        
            // More than one node in the list
            last.next = head.next;
        }

        return last;
    }
```

```java
//Deletion at specific position in circular linked list - O(n) Time and O(1) Space
public static Node deleteSpecificNode(Node last,
                                          int key){
        if (last == null) {
            return null;
        }
        Node curr = last.next;
        Node prev = last;

        // If the node to be deleted is the only node in the
        // list
        if (curr == last && curr.data == key) {
            last = null;
            return last;
        }

        // If the node to be deleted is the first node
        if (curr.data == key) {
            last.next = curr.next;
            return last;
        }

        // Traverse the list to find the node to be deleted
        while (curr != last && curr.data != key) {
            prev = curr;
            curr = curr.next;
        }

        // If the node to be deleted is found
        if (curr.data == key) {
            prev.next = curr.next;
            if (curr == last) {
                last = prev;
            }
        }
      
        return last;
    }


```

```java
//Deletion at the end of Circular linked list - O(n) Time and O(1) Space
public static Node deleteLastNode(Node last){
        if (last == null) {
            return null;
        }
        Node head = last.next;

        // If there is only one node in the list
        if (head == last) {
            last = null;
            return last;
        }
        // Traverse the list to find the second last node
        Node curr = head;
        while (curr.next != last) {
            curr = curr.next;
        }
        // Update the second last node's next pointer to
        // point to head
        curr.next = head;
        last = curr;

        return last;
    }

```

```java
//Circular Linked List Traversal Using Iterative Method - O(n) Time and O(1) Space:
public static void printList(Node head) {

        // return if list is empty
        if (head == null)
            return;

        // initialize current node as head
        Node curr = head;

        // loop through the circular linked list
        do {

            // print the data of current node
            System.out.print(curr.data + " ");

            // move to the next node
            curr = curr.next;

        } while (curr!= head);
    }
```

```java
//Circular Linked List Traversal Using Recursion - O(n) Time and O(n) Space:

  public static void print(Node curr, Node head) {

      // return if list is empty
      if (head == null)
          return;

      System.out.print(curr.data + " ");

      if (curr.next == head)
          return;

      print(curr.next, head);
  }

  public static void printList(Node head){
      print(head, head);
  }
```
5. Merge Two Sorted Lists
```
https://takeuforward.org/practice/dsa/merge-sorted-lists-
https://leetcode.com/problems/merge-two-sorted-lists/description/
```

```java

```

```java

```

```java

```

5.2. Merge K Sorted Linked Lists
```
https://takeuforward.org/blogs/data-structure-and-algorithm/merge-k-sorted-linked-lists
```

```java

```

```java

```

```java

```
