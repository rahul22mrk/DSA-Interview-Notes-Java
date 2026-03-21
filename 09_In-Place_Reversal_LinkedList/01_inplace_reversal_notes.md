# In-Place Reversal of a LinkedList — Complete Notes

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
7. [Quick reference cheatsheet](#7-quick-reference-cheatsheet)
8. [Common mistakes](#8-common-mistakes)
9. [Complexity summary](#9-complexity-summary)

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

## 7. Quick reference cheatsheet

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

## 8. Common mistakes

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

## 9. Complexity summary

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
