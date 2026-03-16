# In-place Reversal of a LinkedList — Complete Notes

> **Pattern family:** LinkedList Manipulation  
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
7. [Solved problems](#7-solved-problems)
8. [Quick reference cheatsheet](#8-quick-reference-cheatsheet)
9. [Common mistakes](#9-common-mistakes)
10. [Complexity summary](#10-complexity-summary)

---

## 1. How to identify this pattern

### Keyword scanner

Scan the problem statement for these phrases first.

| If you see this... | It means |
|--------------------|----------|
| "reverse a linked list" | full reversal |
| "reverse between positions p and q" | partial reversal with skip |
| "reverse in pairs" | k=2 chunked reversal |
| "reverse every k elements" | k-group reversal |
| "reverse nodes in even-length groups" | conditional group reversal |
| "rotate a linked list by k" | rotation = reconnect, no flip |
| "in-place" + linked list | O(1) space = pointer manipulation |
| "do not use extra space" | no stack, no recursion = 3-pointer approach |

### Brute force test

```
Brute force approach: copy all values into an array, reverse the array, rewrite node values.
→ This uses O(n) extra space.
→ The interviewer says "in-place" or "O(1) space" → you cannot do this.
→ You must flip the .next pointers directly = In-place Reversal pattern.
```

If the problem involves **reordering nodes** (not values) of a linked list → this pattern.

### The 5 confirming signals

**Signal 1 — The problem mentions "reverse" + "linked list" together**
> Almost a guaranteed match. 95% of reverse + linked list problems use this exact 3-pointer technique.

**Signal 2 — You need O(1) extra space**
> No array copy. No stack. No recursion. Only constant-space pointer manipulation possible.

**Signal 3 — You are asked to reverse a segment, not the full list**
> Sub-list reversal = same core loop, just add skip-to-start and reconnect logic around it.

**Signal 4 — The problem says "groups of k" or "every k nodes"**
> K-group reversal = run the core loop in chunks of k, repeatedly.

**Signal 5 — The problem says "rotate" a linked list**
> Rotation is disguised reversal — find tail, connect to head, break at new position. No actual flipping needed.

### Decision flowchart

```
Problem involves a Linked List?
        │
        ▼
Does it ask to reverse order of nodes?
        │
        ├── YES → Is it the full list?
        │              ├── YES → Problem 1 (full reversal)
        │              └── NO  → Is it a sub-list [p,q]?
        │                             ├── YES → Problem 2 (sub-list reversal)
        │                             └── NO  → Is it groups of k?
        │                                           ├── k=2 → Problem 3 (pairs)
        │                                           ├── k=N → Problem 4 (k-groups)
        │                                           └── conditional → Problem 5 (even groups)
        │
        └── NO → Does it ask to "rotate" the list?
                       └── YES → Problem 6 (rotation)
```

---

## 2. What is this pattern?

Every node in a singly linked list has one `.next` pointer that points **forward**. In-place reversal means flipping those pointers to point **backward** — one node at a time — using only 3 pointer variables and no extra data structure.

```
Before:   1 → 2 → 3 → 4 → 5 → null
After:    5 → 4 → 3 → 2 → 1 → null
```

**Why "in-place"?**
You are not creating new nodes. You are not copying values. You are only changing where `.next` points. Memory usage = O(1) regardless of list size.

**Core mechanic — one iteration:**
```
prev ← curr → next → (rest)
         ↑
    flip this arrow: curr.next = prev
```

When you write `curr.next = prev`, you lose access to the rest of the list. That is why you must save `curr.next` into a temporary `next` variable BEFORE flipping. This is the single most important thing to understand about this pattern.

---

## 3. Core rules

**Rule 1 — Always save `next` BEFORE flipping**
```java
// WRONG — you lose the rest of the list
curr.next = prev;
next = curr.next;   // curr.next is now prev, not the original next — BUG

// CORRECT — save first, then flip
next = curr.next;   // save the rest of the list
curr.next = prev;   // now safe to flip
```

**Rule 2 — After reversing a segment, the original head becomes the tail**
```java
// When you reverse  [A → B → C]  it becomes  [C → B → A]
// The node you passed in as `head` (A) is now the TAIL.
// Use this to reconnect: headOfSegment.next = nextSegmentStart;

ListNode segmentTail = segmentHead;   // save before reversing
ListNode newHead = reverse(segmentHead, count);
segmentTail.next = nextPart;          // reconnect using the now-tail
```

**Rule 3 — For sub-list problems, always save the node BEFORE the reversal starts**
```java
// You need `beforeP` to reconnect the left part to the reversed segment.
// Walk to position (p-1) and save that node.
ListNode beforeP = null;
ListNode curr = head;
for (int i = 1; i < p; i++) {
    beforeP = curr;
    curr = curr.next;
}
// After reversal: beforeP.next = newHead of reversed segment
```

---

## 4. 2-Question framework

Ask these two questions to identify exactly which variant you need.

### Question 1 — How much of the list do you reverse?

| Answer | Variant |
|--------|---------|
| The entire list | Full reversal |
| A fixed window from index p to q | Sub-list reversal |
| Every 2 nodes (pairs) | Pair reversal (k=2) |
| Every k nodes | K-group reversal |
| Only even-length groups | Conditional reversal |
| None — just reposition the tail | Rotation |

### Question 2 — What do you do between reversed segments?

| Answer | What it means |
|--------|---------------|
| Nothing — one continuous reversal | Full reversal or sub-list |
| Advance k nodes, reverse k nodes, repeat | K-group reversal |
| Check group size before reversing | Conditional (even groups) |
| Find tail, connect head, break link | Rotation |

> **Decision shortcut:**
> - "reverse all" → full reversal
> - "reverse [p..q]" → skip + partial reversal + reconnect
> - "groups of k" → loop the reversal k at a time
> - "rotate" → find tail + reconnect, no flip
> - "even groups" → reverse only when group size is even

---

## 5. Variants table

> **Common core:** `prev`, `curr`, `next` + 4-line flip loop  
> **What differs:** how much you reverse, and how you reconnect

| Variant | Setup before loop | Loop reverses | Reconnection after |
|---------|-------------------|---------------|--------------------|
| Full reversal | `prev=null, curr=head` | All nodes | None — return `prev` |
| Sub-list [p,q] | Walk to p-1, save `beforeP` and `tailOfSegment` | (q-p+1) nodes | `beforeP.next = newHead` and `tailOfSegment.next = curr` |
| Pairs (k=2) | `dummy → head`, work on pairs | 2 nodes at a time | Connect each pair to next pair |
| K-groups | Check k nodes exist, save segment tail | k nodes at a time | Connect segment tail to next group's new head |
| Even groups | Track group number and size | Only even-sized groups | Skip odd groups, reverse even groups, reconnect |
| Rotation | Find length and tail | Nothing reversed | `tail.next = head`, break at `(len - k%len)` |

---

## 6. Universal Java template

```java
// ─── NODE DEFINITION ──────────────────────────────────────────────────────────
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

// ─── CORE 4-LINE FLIP (memorise this — every problem uses it) ─────────────────
// Reverses `count` nodes starting from `head`.
// Returns: new head of the reversed segment.
// After return: original `head` is now the TAIL of the reversed segment.
private ListNode reverseSegment(ListNode head, int count) {
    ListNode prev = null;
    ListNode curr = head;

    while (curr != null && count > 0) {
        ListNode next = curr.next;   // Step 1: SAVE  — never lose the rest
        curr.next     = prev;        // Step 2: FLIP  — reverse the arrow
        prev          = curr;        // Step 3: ADVANCE prev forward
        curr          = next;        // Step 4: ADVANCE curr forward
        count--;
    }
    // prev  = new head of reversed segment
    // curr  = first node AFTER the reversed segment (use for reconnection)
    return prev;
}

// ─── HOW TO STITCH SEGMENTS TOGETHER ─────────────────────────────────────────
// Pattern for connecting reversed chunk back to the rest of the list:
//
//   ListNode segmentTail = segmentStart;      // save tail BEFORE reversing
//   ListNode newHead = reverseSegment(segmentStart, k);
//   prevGroupTail.next = newHead;              // left side connects to new head
//   segmentTail.next   = curr;                // new tail connects to remainder
//   prevGroupTail      = segmentTail;         // advance the "left boundary"
//
// ─── DUMMY NODE TRICK (for problems where head might change) ──────────────────
//   ListNode dummy = new ListNode(0);
//   dummy.next = head;
//   // Work with dummy as the anchor.
//   // Return dummy.next as the final head.
```

---

## 7. Solved problems

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

## 8. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                        → VARIANT                  → KEY TRICK
─────────────────────────────────────────────────────────────────────────────────
"reverse the whole list"                 → Full reversal            → prev=null, loop, return prev
"reverse between p and q"               → Sub-list reversal        → skip (p-1), save beforeP, reverse (q-p+1), reconnect
"swap pairs / reverse in pairs"         → k=2 group                → swap adjacent pairs, advance by 2
"reverse every k nodes"                 → k-group reversal         → check k exist, reverse, reconnect, repeat
"reverse even-length groups"            → Conditional reversal     → check actual group size, reverse only if even
"rotate right by k"                     → Rotation                 → find tail+len, k%=len, connect tail→head, break at (len-k)
```

**The 4-line flip — burn this into memory:**
```java
ListNode next = curr.next;   // SAVE
curr.next     = prev;        // FLIP
prev          = curr;        // ADVANCE prev
curr          = next;        // ADVANCE curr
```

**Reconnection pattern — always the same structure:**
```java
ListNode segmentTail = segmentStart;          // save tail BEFORE reversing
ListNode newHead = reverse(segmentStart, k);  // reverse returns new head
prevTail.next    = newHead;                   // left → new head
segmentTail.next = curr;                      // new tail → right
prevTail         = segmentTail;               // slide the left boundary
```

**Dummy node — use whenever head might change:**
```java
ListNode dummy = new ListNode(0);
dummy.next = head;
// ... work ...
return dummy.next;
```

---

## 9. Common mistakes

### Mistake 1 — Saving `next` after flipping (loses the list)

```java
// BUG — curr.next is already prev after flip, not the original next
curr.next = prev;
next = curr.next;   // this is now prev, not the original next — list is lost

// FIX — always save BEFORE flipping
next = curr.next;   // save first
curr.next = prev;   // then flip
```

### Mistake 2 — Forgetting to reconnect the segment tail

```java
// BUG — reversed segment floats with null at its tail
ListNode newHead = reverse(start, k);
prevTail.next = newHead;
// start.next is still null from the reversal — list is broken

// FIX — always reconnect the tail
ListNode segTail = start;           // save BEFORE reversing
ListNode newHead = reverse(start, k);
prevTail.next = newHead;
segTail.next  = curr;               // tail connects to the rest
```

### Mistake 3 — Not using k % len in rotation

```java
// BUG — k=7 on a list of length 5 → 7 full rotations = wasteful
rotateRight(head, 7);   // without mod, you walk 7 nodes back

// FIX — always reduce k first
k = k % len;
if (k == 0) return head;   // no-op after reduction
```

### Mistake 4 — Off-by-one when walking to position p

```java
// BUG — for p=3, you need to stop at node 2 (beforeP)
// Loop condition must be i < p, not i <= p
for (int i = 1; i <= p; i++)   // WRONG — goes one too far
    beforeP = curr;

for (int i = 1; i < p; i++)    // CORRECT — stops at p-1
    beforeP = curr;
```

### Mistake 5 — Not checking if k nodes exist before reversing a k-group

```java
// BUG — reverses the last group even if it has fewer than k nodes
while (curr != null) {
    reverse(curr, k);   // WRONG — partial group gets reversed

// FIX — check k nodes exist first
ListNode check = prevGroupTail;
for (int i = 0; i < k; i++) {
    check = check.next;
    if (check == null) return dummy.next;   // stop — fewer than k nodes
}
```

### Mistake 6 — Not using dummy node when head might change

```java
// BUG — if the head is part of a reversed segment, returning `head` is wrong
return head;   // head might now be in the middle of the list

// FIX — always use dummy, return dummy.next
ListNode dummy = new ListNode(0);
dummy.next = head;
// ...
return dummy.next;   // always correct regardless of how head changes
```

---

## 10. Complexity summary

| Problem | Time | Space | Notes |
|---------|------|-------|-------|
| Reverse whole list | O(n) | O(1) | single pass |
| Reverse sub-list [p,q] | O(n) | O(1) | walk to p + reverse segment |
| Reverse in pairs | O(n) | O(1) | one pass, swap each pair |
| Reverse k-groups | O(n) | O(1) | each node processed once |
| Reverse even-length groups | O(n) | O(1) | each node visited once |
| Rotate by k | O(n) | O(1) | find tail + reconnect |
| Reverse alternate k | O(n) | O(1) | one pass |
| Palindrome check | O(n) | O(1) | find middle + reverse half + compare |

**General rule:**
- All in-place reversal problems run in **O(n) time** — every node is touched a constant number of times.
- Space is always **O(1)** — only `prev`, `curr`, `next` are used regardless of list size.
- If you see O(n) space in a reversal solution (e.g., using a stack), it can always be reduced to O(1) with the 3-pointer technique.

---

*In-place Reversal is one of the most tested LinkedList patterns in interviews.*
*Master the 4-line flip and the reconnection template — everything else is just where you start and stop.*
