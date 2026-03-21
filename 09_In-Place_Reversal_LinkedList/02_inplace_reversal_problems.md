# In-Place Reversal of a LinkedList — Solved Problems (14 Problems)

> **Pattern family:** LinkedList Manipulation
> **Notes & Templates:** [01_inplace_reversal_notes.md](./01_inplace_reversal_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Full Reversal
- [P1 — Reverse a LinkedList](#problem-1--reverse-a-linkedlist)

### Category 2 — Partial / Sub-list Reversal
- [P2 — Reverse a Sub-list](#problem-2--reverse-a-sub-list)

### Category 3 — K-Group Reversal
- [P3 — Reverse List in Pairs](#problem-3--reverse-list-in-pairs)
- [P4 — Reverse Every K-element Sub-list](#problem-4--reverse-every-k-element-sub-list)
- [P7 — Reverse Alternate K Elements](#problem-7--reverse-alternate-k-elements)

### Category 4 — Conditional Reversal
- [P5 — Reverse Nodes in Even Length Groups](#problem-5--reverse-nodes-in-even-length-groups)

### Category 5 — Rotation / Reconnect
- [P6 — Rotate a LinkedList](#problem-6--rotate-a-linkedlist)

### Category 6 — Reversal as a Tool
- [P8 — Palindrome LinkedList](#problem-8--palindrome-linkedlist)
- [P9 — Reorder List](#problem-9--reorder-list)

### Category 7 — FAANG / Hard
- [P10 — Sort List](#problem-10--sort-list)
- [P11 — Remove Nth Node From End of List](#problem-11--remove-nth-node-from-end-of-list)
- [P12 — Add Two Numbers](#problem-12--add-two-numbers)
- [P13 — Copy List with Random Pointer](#problem-13--copy-list-with-random-pointer)
- [P14 — Merge Two Sorted Lists](#problem-14--merge-two-sorted-lists)

---

## Category 1 — Full Reversal

---

---

### Problem 1 — Reverse a LinkedList
**LeetCode #206 | Difficulty: Easy | Variant: Full reversal**

#### Approach table

| Step | Loop over | Condition | Result |
|------|-----------|-----------|--------|
| 1 | `curr` from head to null | always | save next, flip, advance both |
| 2 | — | `curr == null` | return `prev` as new head |

#### Java code

```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode curr = head;

    while (curr != null) {
        ListNode next = curr.next;   // Step 1: save
        curr.next = prev;            // Step 2: flip
        prev = curr;                 // Step 3: advance prev
        curr = next;                 // Step 4: advance curr
    }
    return prev;   // new head of reversed list
}
```

#### Example

```
Input:  1 → 2 → 3 → 4 → 5 → null

Trace:
  prev=null, curr=1 → next=2, 1.next=null, prev=1, curr=2
  prev=1,    curr=2 → next=3, 2.next=1,    prev=2, curr=3
  prev=2,    curr=3 → next=4, 3.next=2,    prev=3, curr=4
  prev=3,    curr=4 → next=5, 4.next=3,    prev=4, curr=5
  prev=4,    curr=5 → next=null, 5.next=4, prev=5, curr=null
  curr==null → stop

Output: 5 → 4 → 3 → 2 → 1 → null
```

---


## Category 2 — Partial / Sub-list Reversal

---

### Problem 2 — Reverse a Sub-list
**LeetCode #92 | Difficulty: Medium | Variant: Partial reversal with skip and reconnect**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Walk to node at position (p-1), save as `beforeP` | needed for left reconnect |
| 2 | `curr` is now the start of reversal (position p) | save as `tailOfSegment` |
| 3 | Reverse (q-p+1) nodes with 4-line loop | |
| 4 | `beforeP.next = newHead` | connect left to reversed segment |
| 5 | `tailOfSegment.next = curr` | connect reversed tail to right part |

#### Java code

```java
public ListNode reverseBetween(ListNode head, int p, int q) {
    if (head == null || p == q) return head;

    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode beforeP = dummy;

    // Step 1: walk to the node just before position p
    for (int i = 1; i < p; i++)
        beforeP = beforeP.next;

    // Step 2: curr is now at position p (start of reversal)
    ListNode tailOfSegment = beforeP.next;   // after reversal this becomes the tail
    ListNode curr = tailOfSegment;

    // Step 3: reverse (q - p + 1) nodes
    ListNode prev = null;
    for (int i = 0; i <= q - p; i++) {
        ListNode next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }

    // Step 4: reconnect
    beforeP.next         = prev;    // left part → new head of reversed segment
    tailOfSegment.next   = curr;    // tail of reversed segment → right part

    return dummy.next;
}
```

#### Example

```
Input:  1 → 2 → 3 → 4 → 5 → null,  p=2, q=4

Walk to beforeP (position 1): beforeP = node(1)
tailOfSegment = node(2)
Reverse 3 nodes [2,3,4]: prev = node(4)→node(3)→node(2)→null, curr = node(5)
Reconnect: node(1).next = node(4),  node(2).next = node(5)

Output: 1 → 4 → 3 → 2 → 5 → null
```

---


## Category 3 — K-Group Reversal

---

### Problem 3 — Reverse List in Pairs
**LeetCode #24 | Difficulty: Medium | Variant: K=2 group reversal**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Use dummy node, `prevGroupTail = dummy` | anchor for reconnection |
| 2 | While 2 nodes exist: save `first` and `second` | the pair to reverse |
| 3 | Reverse the pair: `first.next=second.next`, `second.next=first` | simple swap for k=2 |
| 4 | `prevGroupTail.next = second`, `prevGroupTail = first` | reconnect and advance |

#### Java code

```java
public ListNode swapPairs(ListNode head) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode prevGroupTail = dummy;

    while (prevGroupTail.next != null && prevGroupTail.next.next != null) {
        ListNode first  = prevGroupTail.next;         // 1st node of pair
        ListNode second = prevGroupTail.next.next;    // 2nd node of pair

        // Reverse the pair
        first.next          = second.next;   // detach first from second
        second.next         = first;         // second points to first
        prevGroupTail.next  = second;        // connect left part to second

        prevGroupTail = first;   // first is now the tail of this pair
    }
    return dummy.next;
}
```

#### Example

```
Input:  1 → 2 → 3 → 4 → null

Iteration 1: pair=(1,2) → swap → 2 → 1, prevGroupTail=node(1)
Iteration 2: pair=(3,4) → swap → 4 → 3, prevGroupTail=node(3)
No more pairs.

Output: 2 → 1 → 4 → 3 → null
```

---

### Problem 4 — Reverse Every K-element Sub-list
**LeetCode #25 | Difficulty: Hard | Variant: K-group reversal**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Check if k nodes exist ahead | if fewer than k remain, stop |
| 2 | Save `segmentTail = curr` (will be tail after reversal) | for reconnection |
| 3 | Reverse k nodes | use `reverseSegment(curr, k)` |
| 4 | `prevGroupTail.next = newHead` | connect left to this group |
| 5 | `segmentTail.next = curr` | connect this group's tail to next |
| 6 | Advance `prevGroupTail = segmentTail`, repeat | |

#### Java code

```java
public ListNode reverseKGroup(ListNode head, int k) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode prevGroupTail = dummy;

    while (true) {
        // Check if k nodes exist from current position
        ListNode check = prevGroupTail;
        for (int i = 0; i < k; i++) {
            check = check.next;
            if (check == null) return dummy.next;   // fewer than k nodes left
        }

        ListNode segmentTail = prevGroupTail.next;  // will become tail after reverse
        ListNode curr        = prevGroupTail.next;  // start of this group

        // Reverse k nodes
        ListNode prev = null;
        for (int i = 0; i < k; i++) {
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }

        // Reconnect
        prevGroupTail.next = prev;          // left part → new head of group
        segmentTail.next   = curr;          // group tail → start of next group
        prevGroupTail      = segmentTail;   // advance boundary
    }
}
```

#### Example

```
Input:  1 → 2 → 3 → 4 → 5 → null,  k=3

Check: 3 nodes exist (1,2,3) → reverse → 3 → 2 → 1, curr=node(4)
Connect: dummy→3, node(1)→node(4)

Check from node(1): only 2 nodes (4,5) → fewer than k=3 → stop

Output: 3 → 2 → 1 → 4 → 5 → null
```

---


## Category 4 — Conditional Reversal

---

### Problem 5 — Reverse Nodes in Even Length Groups
**LeetCode #2074 | Difficulty: Hard | Variant: Conditional group reversal**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Traverse group by group (group sizes: 1,2,3,4,...) | actual size may be less at end |
| 2 | Count actual nodes in this group | may be less than expected group size |
| 3 | If actual size is even → reverse this group | use standard reversal + reconnect |
| 4 | If actual size is odd → skip (leave as is) | just advance `prevGroupTail` |
| 5 | Repeat for next group | |

#### Java code

```java
public ListNode reverseEvenLengthGroups(ListNode head) {
    ListNode prevGroupTail = head;   // first group (size=1) always stays
    int groupSize = 2;               // start from group 2

    while (prevGroupTail.next != null) {
        // Count actual nodes in this group (may be less than groupSize)
        ListNode node = prevGroupTail;
        int actualSize = 0;
        for (int i = 0; i < groupSize && node.next != null; i++) {
            actualSize++;
            node = node.next;
        }

        if (actualSize % 2 == 0) {
            // Reverse this group
            ListNode segmentTail = prevGroupTail.next;
            ListNode curr = prevGroupTail.next;
            ListNode prev = null;

            for (int i = 0; i < actualSize; i++) {
                ListNode next = curr.next;
                curr.next = prev;
                prev = curr;
                curr = next;
            }
            prevGroupTail.next = prev;
            segmentTail.next   = curr;
            prevGroupTail      = segmentTail;
        } else {
            // Skip odd-size group — just advance prevGroupTail
            for (int i = 0; i < actualSize; i++)
                prevGroupTail = prevGroupTail.next;
        }
        groupSize++;
    }
    return head;
}
```

#### Example

```
Input:  5 → 2 → 6 → 3 → 9 → 1 → 7 → 3 → 8 → null

Groups: [5](size=1,odd→skip), [2,6](size=2,even→reverse→6,2), [3,9,1](size=3,odd→skip), [7,3,8](size=3,odd→skip)

Output: 5 → 6 → 2 → 3 → 9 → 1 → 7 → 3 → 8 → null
```

---


## Category 5 — Rotation / Reconnect

---

### Problem 6 — Rotate a LinkedList
**LeetCode #61 | Difficulty: Medium | Variant: Reconnect (no flip)**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Find length of list and tail node | one pass |
| 2 | `k = k % len` — handle k > len | if k==0, return head unchanged |
| 3 | Walk to node at position `(len - k)` — this becomes new tail | |
| 4 | `newHead = newTail.next` | the node after new tail is new head |
| 5 | `tail.next = head` then `newTail.next = null` | form circle then break it |

#### Java code

```java
public ListNode rotateRight(ListNode head, int k) {
    if (head == null || head.next == null || k == 0) return head;

    // Step 1: find length and tail
    int len = 1;
    ListNode tail = head;
    while (tail.next != null) {
        tail = tail.next;
        len++;
    }

    // Step 2: reduce k
    k = k % len;
    if (k == 0) return head;   // no rotation needed

    // Step 3: find new tail at position (len - k)
    ListNode newTail = head;
    for (int i = 1; i < len - k; i++)
        newTail = newTail.next;

    // Step 4 & 5: reconnect
    ListNode newHead   = newTail.next;
    newTail.next       = null;    // break the link
    tail.next          = head;    // old tail → old head (connect the circle)

    return newHead;
}
```

#### Example

```
Input:  1 → 2 → 3 → 4 → 5 → null,  k=2

len=5, k=2%5=2
New tail at position (5-2)=3: node(3)
newHead = node(4)
tail(5).next = head(1) → circle
node(3).next = null    → break

Output: 4 → 5 → 1 → 2 → 3 → null
```

---


## Category 3 (continued) — K-Group Reversal

---

### Problem 7 — Reverse Alternate K Elements (bonus pattern)
**Difficulty: Medium | Variant: Alternate reverse and skip**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Reverse k nodes | standard reversal |
| 2 | Reconnect reversed group to list | `prevTail.next = newHead`, `segTail.next = curr` |
| 3 | Skip k nodes (leave in place) | advance curr by k |
| 4 | Repeat from step 1 | |

#### Java code

```java
public ListNode reverseAlternateKElements(ListNode head, int k) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode prevGroupTail = dummy;
    ListNode curr = head;

    while (curr != null) {
        // Reverse k nodes
        ListNode segTail = curr;
        ListNode prev = null;
        int count = k;
        while (curr != null && count-- > 0) {
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        prevGroupTail.next = prev;
        segTail.next = curr;
        prevGroupTail = segTail;

        // Skip k nodes
        count = k;
        while (curr != null && count-- > 0) {
            prevGroupTail = curr;
            curr = curr.next;
        }
    }
    return dummy.next;
}
```

#### Example

```
Input:  1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → null,  k=2

Reverse [1,2] → [2,1], skip [3,4], reverse [5,6] → [6,5], skip [7,8]

Output: 2 → 1 → 3 → 4 → 6 → 5 → 7 → 8 → null
```

---


## Category 6 — Reversal as a Tool

---

### Problem 8 — Palindrome LinkedList (uses reversal)
**LeetCode #234 | Difficulty: Easy | Variant: Reversal as a tool**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Find middle using slow/fast pointers | slow = middle |
| 2 | Reverse second half from `slow.next` | standard reversal |
| 3 | Compare first half and reversed second half | both must match |
| 4 | (Optional) Restore the list | reverse second half back |

#### Java code

```java
public boolean isPalindrome(ListNode head) {
    if (head == null || head.next == null) return true;

    // Step 1: find middle
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    // Step 2: reverse second half
    ListNode secondHalfHead = reverse(slow.next);

    // Step 3: compare
    ListNode p1 = head, p2 = secondHalfHead;
    while (p2 != null) {
        if (p1.val != p2.val) return false;
        p1 = p1.next;
        p2 = p2.next;
    }
    return true;
}

private ListNode reverse(ListNode head) {
    ListNode prev = null, curr = head;
    while (curr != null) {
        ListNode next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```

#### Example

```
Input:  1 → 2 → 2 → 1 → null

Middle = node(2) (second one)
Reverse second half [2,1] → [1,2]
Compare: 1==1, 2==2 → true

Output: true
```

---


## Category 7 — FAANG / Hard

---

### Problem 9 — Reorder List
**LeetCode #143 | Difficulty: Medium | Company: Amazon, Facebook | Category: Reversal as Tool**

> Reorder `L0 → L1 → ... → Ln` to `L0 → Ln → L1 → Ln-1 → ...` in-place.

#### Core insight

3-step approach: (1) Find middle, (2) Reverse second half, (3) Merge alternately. Classic reversal-as-tool problem.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Find middle with slow/fast pointers | `slow = mid` |
| 2 | Reverse second half from `slow.next` | standard reversal |
| 3 | `slow.next = null` — cut at middle | separates two halves |
| 4 | Merge alternately: first→last→second→second-last... | interleave |

#### Java code

```java
public void reorderList(ListNode head) {
    if (head == null || head.next == null) return;

    // Step 1: find middle
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    // Step 2: reverse second half
    ListNode second = reverse(slow.next);
    slow.next = null;   // cut first half cleanly
    ListNode first = head;

    // Step 3: merge alternately
    while (second != null) {
        ListNode tmp1 = first.next;
        ListNode tmp2 = second.next;
        first.next  = second;
        second.next = tmp1;
        first  = tmp1;
        second = tmp2;
    }
}

private ListNode reverse(ListNode head) {
    ListNode prev = null, curr = head;
    while (curr != null) {
        ListNode next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```

#### Example

```
Input: 1 → 2 → 3 → 4 → 5

Step 1: middle = node(3)
Step 2: reverse [4,5] → 5 → 4. cut: first=[1,2,3], second=[5,4]
Step 3: merge:
  1→5→2→3, tmp1=2, tmp2=4
  2→4→3, tmp1=3, tmp2=null → done

Output: 1 → 5 → 2 → 4 → 3 ✓
```

---

### Problem 10 — Sort List
**LeetCode #148 | Difficulty: Medium | Company: Amazon, Google | Category: Reversal as Tool (Merge Sort)**

> Sort a linked list in O(n log n) time and O(1) space using merge sort.

#### Core insight

Bottom-up merge sort on linked list. Find middle (split point), sort each half recursively, then merge. The reversal pattern's "find middle" technique enables O(1) space.

#### Java code

```java
public ListNode sortList(ListNode head) {
    if (head == null || head.next == null) return head;

    // Find middle and split
    ListNode slow = head, fast = head.next;  // fast=head.next → left-middle
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    ListNode second = slow.next;
    slow.next = null;   // cut

    // Sort both halves
    ListNode left  = sortList(head);
    ListNode right = sortList(second);

    // Merge
    return merge(left, right);
}

private ListNode merge(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0), curr = dummy;
    while (l1 != null && l2 != null) {
        if (l1.val <= l2.val) { curr.next = l1; l1 = l1.next; }
        else                  { curr.next = l2; l2 = l2.next; }
        curr = curr.next;
    }
    curr.next = (l1 != null) ? l1 : l2;
    return dummy.next;
}
```

#### Example

```
Input: 4 → 2 → 1 → 3

Split: [4,2] and [1,3]
Sort:  [2,4] and [1,3]
Merge: 1 → 2 → 3 → 4 ✓

Time: O(n log n), Space: O(log n) recursion stack
```

---

### Problem 11 — Remove Nth Node From End of List
**LeetCode #19 | Difficulty: Medium | Company: Amazon, Microsoft | Category: Two-Pointer Gap**

> Remove the nth node from the end of the list in one pass.

#### Core insight

Gap technique: advance fast pointer n+1 steps ahead. When fast reaches null, slow is one node before the target. `slow.next = slow.next.next` removes the target.

#### Java code

```java
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode slow = dummy, fast = dummy;

    // Advance fast n+1 steps (so slow lands BEFORE the target)
    for (int i = 0; i <= n; i++) fast = fast.next;

    // Move both until fast reaches null
    while (fast != null) {
        slow = slow.next;
        fast = fast.next;
    }

    // slow is one node before the nth-from-end
    slow.next = slow.next.next;
    return dummy.next;
}
```

#### Example

```
Input: 1 → 2 → 3 → 4 → 5, n=2

fast advances n+1=3 steps: fast=node(3)
Move until fast=null:
  slow=1, fast=4 → slow=2, fast=5 → slow=3, fast=null
slow.next = slow.next.next → remove node(4)

Output: 1 → 2 → 3 → 5 ✓
```

---

### Problem 12 — Add Two Numbers
**LeetCode #2 | Difficulty: Medium | Company: Amazon, Google, Microsoft | Category: LinkedList Simulation**

> Two non-empty linked lists represent non-negative integers in reverse order. Add them and return result as linked list.

#### Core insight

Traverse both lists simultaneously, add digit by digit with carry. Build result list. Handle remaining carry at end.

#### Java code

```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;
    int carry = 0;

    while (l1 != null || l2 != null || carry != 0) {
        int sum = carry;
        if (l1 != null) { sum += l1.val; l1 = l1.next; }
        if (l2 != null) { sum += l2.val; l2 = l2.next; }

        carry = sum / 10;
        curr.next = new ListNode(sum % 10);
        curr = curr.next;
    }
    return dummy.next;
}
```

#### Example

```
l1 = 2 → 4 → 3  (represents 342)
l2 = 5 → 6 → 4  (represents 465)

pos0: 2+5=7, carry=0 → node(7)
pos1: 4+6=10, carry=1 → node(0)
pos2: 3+4+1=8, carry=0 → node(8)

Output: 7 → 0 → 8  (represents 807 = 342+465) ✓
```

---

### Problem 13 — Copy List with Random Pointer
**LeetCode #138 | Difficulty: Medium | Company: Amazon, Facebook, Google | Category: LinkedList Clone**

> Deep copy a linked list where each node has a `next` and a `random` pointer.

#### Core insight

HashMap approach: map each original node to its clone. First pass: create all clone nodes. Second pass: set `next` and `random` pointers using the map.

#### Java code

```java
public Node copyRandomList(Node head) {
    if (head == null) return null;

    Map<Node, Node> map = new HashMap<>();

    // Pass 1: create all clone nodes
    Node curr = head;
    while (curr != null) {
        map.put(curr, new Node(curr.val));
        curr = curr.next;
    }

    // Pass 2: set next and random pointers
    curr = head;
    while (curr != null) {
        if (curr.next   != null) map.get(curr).next   = map.get(curr.next);
        if (curr.random != null) map.get(curr).random = map.get(curr.random);
        curr = curr.next;
    }

    return map.get(head);
}
```

#### O(1) space approach (interleaving)

```java
public Node copyRandomList(Node head) {
    if (head == null) return null;

    // Step 1: interleave clones — A → A' → B → B' → ...
    Node curr = head;
    while (curr != null) {
        Node clone = new Node(curr.val);
        clone.next = curr.next;
        curr.next  = clone;
        curr = clone.next;
    }

    // Step 2: set random pointers for clones
    curr = head;
    while (curr != null) {
        if (curr.random != null)
            curr.next.random = curr.random.next;
        curr = curr.next.next;
    }

    // Step 3: separate the two lists
    Node dummy = new Node(0);
    Node cloneCurr = dummy;
    curr = head;
    while (curr != null) {
        cloneCurr.next = curr.next;
        curr.next = curr.next.next;
        cloneCurr = cloneCurr.next;
        curr = curr.next;
    }
    return dummy.next;
}
```

#### Example

```
Original: 1 → 2 → 3
random:   1.random=3, 2.random=1, 3.random=2

After pass 1 (HashMap): map={1:1', 2:2', 3:3'}
After pass 2: 1'.next=2', 1'.random=3', 2'.next=3', 2'.random=1', etc.

Output: deep copy with all pointers correctly mapped ✓
```

---

### Problem 14 — Merge Two Sorted Lists
**LeetCode #21 | Difficulty: Easy | Company: Amazon, Microsoft, Google | Category: LinkedList Merge**

> Merge two sorted linked lists and return the merged list.

#### Core insight

Dummy head approach. Compare heads of both lists, attach smaller node to result, advance that pointer. Attach remaining list at end.

#### Java code

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;

    while (l1 != null && l2 != null) {
        if (l1.val <= l2.val) { curr.next = l1; l1 = l1.next; }
        else                  { curr.next = l2; l2 = l2.next; }
        curr = curr.next;
    }
    curr.next = (l1 != null) ? l1 : l2;   // attach remaining
    return dummy.next;
}
```

#### Example

```
l1 = 1 → 2 → 4
l2 = 1 → 3 → 4

1≤1 → take l1(1). l1=2→4
1≤3 → take l2(1). l2=3→4? No: l1.val=2 > l2.val=1 → take l2(1). l2=3→4
2≤3 → take l1(2). l1=4
3≤4 → take l2(3). l2=4
4≤4 → take l1(4). l1=null
Attach l2: 4→null

Output: 1 → 1 → 2 → 3 → 4 → 4 ✓
```

---

## Quick Pattern Reference

| Problem | Category | Key technique |
|---------|----------|---------------|
| Reverse LinkedList | Full Reversal | `prev=null`; 4-line flip; return `prev` |
| Reverse Sub-list | Partial | walk to p-1; save tail; reverse (q-p+1); reconnect |
| Reverse in Pairs | k=2 Group | dummy; swap adjacent pairs; `prevTail = first` |
| Reverse K-Group | K-Group | check k exist; save tail; reverse; reconnect; repeat |
| Reverse Even Groups | Conditional | count actual group size; reverse only if even |
| Rotate List | Reconnect | find len+tail; `k%=len`; connect tail→head; break at len-k |
| Reverse Alternate K | K-Group + Skip | reverse k; skip k; repeat |
| Palindrome LL | Reversal Tool | find mid; reverse half; compare; restore |
| Reorder List | Reversal Tool | find mid; reverse half; merge alternately |
| Sort List | Reversal Tool | find mid; split; sort; merge (merge sort) |
| Remove Nth From End | Gap Technique | dummy; fast n+1 ahead; slow lands before target |
| Add Two Numbers | Simulation | digit-by-digit with carry; dummy head |
| Copy Random Pointer | HashMap / Interleave | map orig→clone; set pointers; or interleave+separate |
| Merge Two Sorted | Merge | dummy; compare heads; attach smaller; append rest |
