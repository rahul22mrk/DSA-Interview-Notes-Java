# Fast & Slow Pointers (Floyd's Algorithm) — Complete Notes

> **Pattern family:** LinkedList Manipulation / Cycle Detection  
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

| If you see this... | It means |
|--------------------|----------|
| "detect a cycle in linked list" | cycle detection |
| "find start / entry point of cycle" | cycle start |
| "middle of linked list" | find middle |
| "palindrome linked list" | find middle + reverse |
| "reorder / rearrange linked list" | find middle + reverse + merge |
| "happy number" | implicit cycle in number sequence |
| "find duplicate number" | implicit cycle via index mapping |
| "cycle in circular array" | implicit cycle via jump mapping |
| "kth node from end" | fast starts k steps ahead |
| "does linked list intersect" | find intersection node |

### Brute force test

```
Brute force: use a HashSet — store every visited node, check if seen again.
→ This works but uses O(n) extra space.
→ Interviewer says "O(1) space" → you cannot use HashSet.
→ Use Fast & Slow pointers instead = O(1) space, O(n) time.
```

### The 5 confirming signals

**Signal 1 — "Detect cycle" + "O(1) space"**
> HashSet approach is obvious. O(1) space constraint forces Fast & Slow.

**Signal 2 — "Find middle" of a linked list**
> When fast reaches end, slow is exactly at middle. Classic use.

**Signal 3 — The problem involves a sequence that might loop back**
> Happy number, Find Duplicate, Circular Array — all have implicit cycles.
> Numbers/indices act as nodes, the next value/jump acts as `.next`.

**Signal 4 — "Kth node from end" or "remove nth node from end"**
> Fast pointer starts k steps ahead of slow. When fast hits null, slow is at target.

**Signal 5 — Problem involves finding a "meeting point" or "entry point"**
> Two pointers moving at different speeds will always meet inside a cycle.
> Meeting point math tells you the cycle start.

### Decision flowchart

```
Problem involves a sequence (linked list, numbers, array indices)?
        │
        ▼
Does the sequence possibly loop / cycle?
        │
        ├── YES → Do you just need to detect it?
        │              └── YES → Cycle Detection (Problem 1)
        │              └── NO  → Do you need the cycle start?
        │                             └── YES → Cycle Start (Problem 2)
        │
        ├── FIND MIDDLE → slow/fast, when fast=null, slow=middle (Problem 4)
        │
        ├── KTH FROM END → fast starts k ahead, both move together (Problem 9)
        │
        ├── PALINDROME → find middle + reverse second half (Problem 5)
        │
        ├── REORDER LIST → find middle + reverse + merge (Problem 6)
        │
        └── IMPLICIT CYCLE (Happy Number, Duplicate, Circular Array)
               → map problem to linked list, apply Floyd's algorithm
```

---

## 2. What is this pattern?

Two pointers move through a sequence at **different speeds** — one moves one step at a time (slow), the other moves two steps at a time (fast).

```java
slow = slow.next;        // moves 1 step
fast = fast.next.next;   // moves 2 steps
```

**Core insight — if a cycle exists:**
Fast gains 1 step on slow every iteration. Eventually fast "laps" slow and they meet inside the cycle. This is guaranteed — it is mathematically impossible for fast to skip over slow inside a cycle.

**Core insight — for finding middle:**
When fast reaches the end (null), slow has traveled exactly half the distance → slow is at the middle.

```
List:  1 → 2 → 3 → 4 → 5
iter1: slow=2, fast=3
iter2: slow=3, fast=5
iter3: fast=null → slow=3 = middle ✓
```

**Why this pattern generalises beyond linked lists:**
Any sequence where each element maps to exactly one "next" element can be modelled as a linked list. Happy Number: `n → sum_of_squares(n)`. Find Duplicate: `n → nums[n]`. Circular Array: `i → i + arr[i]`. Floyd's algorithm works on all of them.

---

## 3. Core rules

**Rule 1 — Always check `fast != null && fast.next != null` together**
```java
// WRONG — crashes with NullPointerException on even-length lists
while (fast.next != null) {
    fast = fast.next.next;   // fast.next.next may be null → NPE

// CORRECT — both conditions required
while (fast != null && fast.next != null) {
    fast = fast.next.next;   // safe
```
`fast != null` prevents NPE when list has even length (fast lands exactly on null).  
`fast.next != null` prevents NPE when trying to do `fast.next.next`.

**Rule 2 — Cycle start formula: reset one pointer to head after meeting**
```java
// After slow == fast (they meet inside cycle):
slow = head;          // reset slow to head
// keep fast at meeting point
while (slow != fast) {
    slow = slow.next;
    fast = fast.next;  // both move 1 step now
}
// slow == fast == cycle start node
```
Mathematical proof: if cycle starts at distance `F` from head, and cycle length is `C`, the meeting point is exactly `F` steps from the cycle start. Resetting one pointer to head and moving both at speed 1 brings them to the start simultaneously.

**Rule 3 — For "find middle", slow starts at head (not head.next)**
```java
// WRONG — slow starts one ahead, gives wrong middle
ListNode slow = head.next;
ListNode fast = head;

// CORRECT — both start at head
ListNode slow = head;
ListNode fast = head;
// When fast reaches end, slow is at middle
```
For odd-length lists: slow lands on exact middle.  
For even-length lists: slow lands on the **second** of the two middle nodes (right-middle).  
If you need the left-middle (for palindrome check), use `fast = head.next` as starting condition or `fast.next != null && fast.next.next != null`.

---

## 4. 2-Question framework

### Question 1 — What kind of cycle / traversal do you need?

| Answer | Variant |
|--------|---------|
| Just detect if cycle exists | Cycle Detection |
| Find where the cycle starts | Cycle Start (Floyd's Phase 2) |
| Find the middle node | Middle of LinkedList |
| Find kth node from end | Gap technique (fast k ahead) |
| Palindrome check | Middle + Reverse second half |
| Reorder list | Middle + Reverse + Merge |
| Cycle in non-linked-list sequence | Map to implicit linked list |

### Question 2 — Is the cycle explicit or implicit?

| Type | Example | How to apply |
|------|---------|-------------|
| **Explicit** | Actual linked list with `.next` | Direct: `slow=slow.next`, `fast=fast.next.next` |
| **Implicit** | Happy Number, Find Duplicate, Circular Array | Define a `getNext(n)` function that acts as `.next` |

```java
// Implicit cycle template
int slow = head, fast = head;
while (true) {
    slow = getNext(slow);           // 1 step
    fast = getNext(getNext(fast));  // 2 steps
    if (slow == fast) break;        // cycle detected
}
```

> **Decision shortcut:**
> - "cycle exists?" → detect only
> - "where does cycle start?" → detect + phase 2 reset
> - "middle?" → fast/slow, check `fast == null`
> - "kth from end?" → gap technique
> - number/array problem loops → implicit cycle

---

## 5. Variants table

> **Common core:** `slow = slow.next`, `fast = fast.next.next`  
> **What differs:** starting condition, termination condition, what you return

| Variant | Slow starts | Fast starts | Loop ends when | Return / Use |
|---------|-------------|-------------|----------------|--------------|
| Cycle detection | `head` | `head` | `slow == fast` (cycle) or `fast == null` (no cycle) | `true` / `false` |
| Cycle start | `head` (reset after meet) | `meeting point` | `slow == fast` again | `slow` = cycle start |
| Find middle | `head` | `head` | `fast == null \|\| fast.next == null` | `slow` = middle |
| Kth from end | `head` | `head + k steps` | `fast == null` | `slow` = kth from end |
| Palindrome | `head` | `head` | `fast == null` | reverse from `slow`, compare |
| Reorder list | `head` | `head` | `fast == null` | split at `slow`, reverse 2nd half, merge |
| Happy number | `n` | `n` | `slow == fast` | `slow == 1` → happy |
| Find duplicate | `nums[0]` | `nums[0]` | `slow == fast` | cycle start = duplicate |
| Circular array | index `0` | index `0` | `slow == fast` | detect cycle |

---

## 6. Universal Java template

```java
// ─── TEMPLATE A: Cycle Detection ─────────────────────────────────────────────
public boolean hasCycle(ListNode head) {
    ListNode slow = head, fast = head;

    while (fast != null && fast.next != null) {  // always check BOTH
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true;            // met inside cycle
    }
    return false;   // fast hit null → no cycle
}

// ─── TEMPLATE B: Find Cycle Start (Phase 2 after detection) ──────────────────
// After slow == fast inside cycle:
slow = head;                   // reset one pointer to head
while (slow != fast) {         // both move 1 step now
    slow = slow.next;
    fast = fast.next;
}
// slow == fast == cycle start node

// ─── TEMPLATE C: Find Middle ──────────────────────────────────────────────────
ListNode slow = head, fast = head;
while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
}
// slow = middle (right-middle for even length)

// ─── TEMPLATE D: Kth Node From End ───────────────────────────────────────────
ListNode slow = head, fast = head;
for (int i = 0; i < k; i++)   // advance fast by k steps first
    fast = fast.next;
while (fast != null) {         // move both at same speed
    slow = slow.next;
    fast = fast.next;
}
// slow = kth node from end

// ─── TEMPLATE E: Implicit Cycle (Happy Number, Find Duplicate) ───────────────
int slow = start, fast = start;
do {
    slow = getNext(slow);
    fast = getNext(getNext(fast));
} while (slow != fast);
// Phase 2 for finding cycle start:
slow = start;
while (slow != fast) {
    slow = getNext(slow);
    fast = getNext(fast);
}
// slow == fast == cycle entry
```

---

## 7. Solved problems

---

### Problem 1 — LinkedList Cycle
**LeetCode #141 | Difficulty: Easy | Variant: Cycle Detection**

#### Approach table

| Step | Loop over | Condition | Result |
|------|-----------|-----------|--------|
| 1 | `fast` and `slow` from head | `fast != null && fast.next != null` | move both |
| 2 | inside loop | `slow == fast` | return `true` |
| 3 | loop exits | `fast == null` | return `false` |

#### Java code

```java
// ── Your solution ─────────────────────────────────────────────────────────────
public boolean hasCycle(ListNode head) {
    ListNode slow = head, fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow == fast) {
            return true;
        }
    }
    return false;
}

// ── Reference solution ────────────────────────────────────────────────────────
public boolean hasCycle(ListNode head) {
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true;   // met inside cycle
    }
    return false;   // fast hit null — no cycle
}
```

> **Note:** Both solutions are identical in logic — only formatting differs. Checking `slow == fast` after moving is correct since both start at head.

#### Example

```
Input:  1 → 2 → 3 → 4 → 2 (cycle back to node 2)

iter1: slow=2, fast=3
iter2: slow=3, fast=2  (fast jumped 3→4→2)
iter3: slow=4, fast=4  → slow==fast → return true ✓

Input:  1 → 2 → 3 → null
iter1: slow=2, fast=3
iter2: slow=3, fast=null → loop exits → return false ✓
```

---

### Problem 2 — Start of LinkedList Cycle
**LeetCode #142 | Difficulty: Medium | Variant: Cycle Start (Floyd's Phase 2)**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Detect cycle using slow/fast | if no cycle, return null |
| 2 | Reset `slow = head`, keep `fast` at meeting point | Phase 2 |
| 3 | Move both 1 step until `slow == fast` | |
| 4 | Return `slow` | = cycle start node |

#### Java code

```java
// ── Your solution — Phase 1 and Phase 2 nested inside the same loop ───────────
public ListNode detectCycle(ListNode head) {
    ListNode slow = head, fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow == fast) {
            slow = head;                 // Phase 2: reset slow to head

            while (slow != fast) {
                slow = slow.next;
                fast = fast.next;        // both move 1 step
            }
            return fast;                 // cycle start
        }
    }
    return null;   // no cycle
}

// ── Reference solution — Phase 1 and Phase 2 as separate blocks ───────────────
public ListNode detectCycle(ListNode head) {
    ListNode slow = head, fast = head;

    // Phase 1: detect cycle
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) break;   // met inside cycle
    }

    // No cycle
    if (fast == null || fast.next == null) return null;

    // Phase 2: find cycle start
    slow = head;                   // reset slow to head
    while (slow != fast) {         // both move 1 step
        slow = slow.next;
        fast = fast.next;
    }
    return slow;   // cycle start
}
```

> **Note:** Your solution is slightly cleaner — the early `return fast` inside the `if` avoids the extra null check after the loop. Both are correct.

#### Why does Phase 2 work?

```
Let:
  F = distance from head to cycle start
  C = cycle length
  k = distance from cycle start to meeting point

When they meet: slow traveled (F + k), fast traveled (F + k + C)
Since fast = 2 × slow:  2(F+k) = F+k+C  →  F = C - k

So: F == distance from meeting point back to cycle start.
Resetting slow to head and moving both at speed 1 brings them
to the cycle start at the same time.
```

#### Example

```
Input: 3 → 1 → 2 → 4 → 2 (cycle at node with val=2, index 1)

Phase 1: slow=1,fast=2 → slow=2,fast=2 → meet at node(2)
Phase 2: slow=head=3, fast=node(2)
  slow=1, fast=4
  slow=2, fast=2 → slow==fast → return node(2) ✓
```

---

### Problem 3 — Happy Number
**LeetCode #202 | Difficulty: Medium | Variant: Implicit Cycle Detection**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Define `getNext(n)` = sum of squares of digits | acts as `.next` |
| 2 | Run slow/fast on this implicit sequence | |
| 3 | If `slow == 1` at meeting → happy | |
| 4 | If `slow != 1` → cycle on non-1 number → not happy | |

#### Java code

```java
// ── Your solution — loop exits when fast reaches 1 ────────────────────────────
class Solution {
    public boolean isHappy(int n) {
        int slow = n, fast = n;

        while (fast != 1) {
            slow = funSum(slow);           // 1 step
            fast = funSum(fast);
            fast = funSum(fast);           // 2 steps

            if (slow == fast && fast != 1) {
                return false;              // met in non-1 cycle → not happy
            }
        }
        return true;   // fast reached 1
    }

    private int funSum(int n) {
        int sum = 0;
        while (n != 0) {
            int d = n % 10;
            n /= 10;
            sum = sum + d * d;
        }
        return sum;
    }
}

// ── Reference solution — do-while, returns based on meeting point value ────────
public boolean isHappy(int n) {
    int slow = n;
    int fast = n;

    do {
        slow = getNext(slow);           // 1 step
        fast = getNext(getNext(fast));  // 2 steps
    } while (slow != fast);

    return slow == 1;   // met at 1 → happy; met elsewhere → cycle → not happy
}

private int getNext(int n) {
    int sum = 0;
    while (n > 0) {
        int digit = n % 10;
        sum += digit * digit;
        n /= 10;
    }
    return sum;
}
```

> **Note:** Your `while(fast != 1)` approach short-circuits as soon as fast hits 1 — it's slightly more direct. The `fast != 1` guard inside correctly prevents false negatives when slow and fast both land on 1 simultaneously.

#### Example

```
Input: n = 19

Sequence: 19 → 82 → 68 → 100 → 1 → 1 → ... (cycle at 1)

slow: 19→82→68→100→1
fast: 19→68→1→1→1

slow==fast==1 → return true ✓

Input: n = 2
Sequence eventually cycles: 2→4→16→37→58→89→145→42→20→4 (cycle, never hits 1)
slow==fast != 1 → return false ✓
```

---

### Problem 4 — Find the Duplicate Number
**LeetCode #287 | Difficulty: Medium | Variant: Implicit Cycle (Array as LinkedList)**

#### Core insight

Array `nums` of length `n+1`, values in `[1,n]`. Treat each value as a pointer: `i → nums[i]`. Since one value is duplicated, two indices point to the same "next" → a cycle exists. Find the cycle start = duplicate number.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | `slow = nums[slow]`, `fast = nums[nums[fast]]` | implicit linked list traversal |
| 2 | Detect meeting point | Phase 1 |
| 3 | Reset slow to `nums[0]`, move both 1 step | Phase 2 |
| 4 | Return `slow` at meeting | = duplicate |

#### Java code

```java
// ── Your solution — start from index 0 as entry point ────────────────────────
class Solution {
    public int findDuplicate(int[] nums) {
        int slow = 0, fast = 0;

        while (true) {
            slow = nums[slow];           // 1 step
            fast = nums[nums[fast]];     // 2 steps

            if (slow == fast) {
                slow = 0;                // Phase 2: reset slow to entry index

                while (slow != fast) {
                    slow = nums[slow];
                    fast = nums[fast];   // both 1 step
                }
                return slow;            // duplicate number
            }
        }
    }
}

// ── Reference solution — start from nums[0] ───────────────────────────────────
public int findDuplicate(int[] nums) {
    int slow = nums[0];
    int fast = nums[0];

    // Phase 1: find meeting point
    do {
        slow = nums[slow];
        fast = nums[nums[fast]];
    } while (slow != fast);

    // Phase 2: find cycle start = duplicate number
    slow = nums[0];
    while (slow != fast) {
        slow = nums[slow];
        fast = nums[fast];
    }
    return slow;
}
```

> **Note:** Your approach starts both pointers at index `0` — a clean entry point since `nums[0]` is always in `[1,n]`, guaranteed to enter the cycle. The reference starts at `nums[0]` (the value, skipping index 0). Both are correct Floyd's applications.

#### Example

```
Input: nums = [1, 3, 4, 2, 2]

Implicit list:  0→1→3→2→4→2→4→2... (cycle at index 2, value 2)

Phase 1: slow=nums[1]=3, fast=nums[nums[1]]=nums[3]=2
         slow=nums[3]=2, fast=nums[nums[2]]=nums[4]=2 → meet at 2

Phase 2: slow=nums[0]=1, fast=2
         slow=nums[1]=3, fast=nums[2]=4
         slow=nums[3]=2, fast=nums[4]=2 → slow==fast==2

Output: 2 ✓
```

---

### Problem 5 — Middle of the LinkedList
**LeetCode #876 | Difficulty: Easy | Variant: Find Middle**

#### Approach table

| Step | Loop over | Condition | Result |
|------|-----------|-----------|--------|
| 1 | slow 1 step, fast 2 steps | `fast != null && fast.next != null` | keep moving |
| 2 | loop exits | `fast == null` or `fast.next == null` | `slow` = middle |

#### Java code

```java
// ── Your solution ─────────────────────────────────────────────────────────────
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode slow = head, fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;
    }
}

// ── Reference solution ────────────────────────────────────────────────────────
public ListNode middleNode(ListNode head) {
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;   // middle node (right-middle for even length)
}
```

> **Note:** Both solutions are identical — your solution wraps it in the class definition. Returns right-middle for even-length lists.

#### Example

```
Odd:  1 → 2 → 3 → 4 → 5
  iter1: slow=2, fast=3
  iter2: slow=3, fast=5
  iter3: fast.next=null → stop → return node(3) ✓

Even: 1 → 2 → 3 → 4
  iter1: slow=2, fast=3
  iter2: slow=3, fast=null → stop → return node(3)  (right-middle) ✓
```

---

### Problem 6 — Palindrome LinkedList
**LeetCode #234 | Difficulty: Medium | Variant: Find Middle + Reverse**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Find middle using slow/fast | slow = middle |
| 2 | Reverse second half from `slow` | standard reversal |
| 3 | Compare `p1` from head, `p2` from reversed head | both advance together |
| 4 | Return `true` if all match | |

#### Java code

```java
// ── Your solution ─────────────────────────────────────────────────────────────
class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) {
            return true;
        }
        ListNode fast = head;
        ListNode slow = head;

        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }

        ListNode secondGroupHead = reverse(slow);
        ListNode p1 = head;
        ListNode p2 = secondGroupHead;

        while (p2 != null) {
            if (p1.val != p2.val) {
                return false;
            }
            p1 = p1.next;
            p2 = p2.next;
        }
        return true;
    }

    private ListNode reverse(ListNode head) {
        ListNode curr = head;
        ListNode prev = null;

        while (curr != null) {
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
}

// ── Reference solution ────────────────────────────────────────────────────────
public boolean isPalindrome(ListNode head) {
    if (head == null || head.next == null) return true;

    // Step 1: find middle
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    // Step 2: reverse second half from slow
    ListNode secondHead = reverse(slow);

    // Step 3: compare
    ListNode p1 = head, p2 = secondHead;
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

> **Note:** `slow.next = null` is NOT needed here (unlike Reorder List) — you are only comparing, not interleaving nodes. Middle node compares with itself in odd-length lists (always equal). Both solutions are logically identical.

#### Example

```
Input: 1 → 2 → 2 → 1

slow = node(2) [second 2], fast = null
reverse from node(2): secondHead = 1 → 2

p1=1, p2=1 → ✓
p1=2, p2=2 → ✓
p2=null → return true ✓

Input: 1 → 2 → 3
slow = node(2), reverse: secondHead = 3 → 2
p1=1, p2=3 → 1≠3 → return false ✓
```

---

### Problem 7 — Reorder List
**LeetCode #143 | Difficulty: Medium | Variant: Find Middle + Reverse + Merge**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Find middle using slow/fast | slow = middle |
| 2 | `second = reverse(slow.next)` | reverse second half |
| 3 | `slow.next = null` | cut list at middle |
| 4 | Merge `first` and `second` alternately | interleave |

#### Java code

```java
// ── Your solution — reverse(slow.next), middle stays in first half ────────────
class Solution {
    public void reorderList(ListNode head) {
        if (head == null || head.next == null) {
            return;
        }
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }

        ListNode second = reverse(slow.next);   // reverse AFTER middle
        slow.next = null;                        // cut first half cleanly
        ListNode first = head;

        while (second != null) {
            ListNode temp1 = first.next;
            ListNode temp2 = second.next;

            first.next  = second;
            second.next = temp1;

            first  = temp1;
            second = temp2;
        }
    }

    private ListNode reverse(ListNode head) {
        ListNode curr = head;
        ListNode prev = null;

        while (curr != null) {
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
}

// ── Reference solution — same approach with both-null guard in merge loop ──────
public void reorderList(ListNode head) {
    if (head == null || head.next == null) return;

    // Step 1: find middle
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    // Step 2: reverse second half (from slow.next)
    ListNode second = reverse(slow.next);
    slow.next = null;   // cut first half
    ListNode first = head;

    // Step 3: merge alternately
    while (first != null && second != null) {
        ListNode temp1 = first.next;
        ListNode temp2 = second.next;
        first.next  = second;
        second.next = temp1;
        first  = temp1;
        second = temp2;
    }
}
```

> **Note:** Your `while(second != null)` is safe here — first half is always ≥ second half in length so first never hits null before second does. The reference uses `while(first != null && second != null)` as a defensive guard — both are correct for this problem.

#### Example

```
Input: 1 → 2 → 3 → 4 → 5

Middle: slow=3
second = reverse(4→5) = 5→4→null
slow.next=null → first=1→2→3→null

Merge:
  1→5→2→3,  first=2, second=4
  2→4→3,    first=3, second=null → done

Output: 1 → 5 → 2 → 4 → 3 ✓
```

---

### Problem 8 — Cycle in a Circular Array
**LeetCode #457 | Difficulty: Hard | Variant: Implicit Cycle in Array**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | For each index, start slow/fast | try every starting index |
| 2 | `getNext(i)` = `((i + nums[i]) % n + n) % n` | handles negative jumps |
| 3 | Check direction consistency: all steps same sign | no direction change allowed |
| 4 | Check cycle length > 1 | single-node cycle not valid |
| 5 | If `slow == fast` with valid cycle → return `true` | |

#### Java code

```java
public boolean circularArrayLoop(int[] nums) {
    int n = nums.length;

    for (int i = 0; i < n; i++) {
        boolean isForward = nums[i] > 0;
        int slow = i, fast = i;

        do {
            slow = getNext(nums, slow, isForward, n);
            fast = getNext(nums, fast, isForward, n);
            if (fast == -1) break;
            fast = getNext(nums, fast, isForward, n);
            if (fast == -1) break;
        } while (slow != -1 && slow != fast);

        if (slow != -1 && slow == fast) return true;
    }
    return false;
}

private int getNext(int[] nums, int i, boolean isForward, int n) {
    boolean direction = nums[i] > 0;
    if (direction != isForward) return -1;   // direction changed — invalid

    int next = ((i + nums[i]) % n + n) % n;
    if (next == i) return -1;   // single-element cycle — invalid

    return next;
}
```

#### Example

```
Input: nums = [2, -1, 1, 2, 2]

Start i=0, forward=true:
  slow: 0→2→3→0 (cycle!)
  fast: 0→3→0 → slow==fast=0
  Valid direction (all positive at these indices) → return true ✓
```

---

### Problem 9 — Remove Nth Node From End of List (bonus)
**LeetCode #19 | Difficulty: Medium | Variant: Gap technique (kth from end)**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Advance `fast` by `n` steps | creates gap of n between fast and slow |
| 2 | Move both until `fast == null` | slow is now at the node BEFORE the target |
| 3 | `slow.next = slow.next.next` | remove the target node |

#### Java code

```java
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode slow = dummy, fast = dummy;

    // Advance fast by n+1 steps (n+1 so slow lands BEFORE the target)
    for (int i = 0; i <= n; i++)
        fast = fast.next;

    // Move both until fast hits null
    while (fast != null) {
        slow = slow.next;
        fast = fast.next;
    }

    // slow is now one node before the nth-from-end node
    slow.next = slow.next.next;
    return dummy.next;
}
```

#### Example

```
Input: 1 → 2 → 3 → 4 → 5,  n=2

dummy → 1 → 2 → 3 → 4 → 5
fast advances n+1=3 steps: fast=node(3)
Move both until fast=null:
  slow=1, fast=4
  slow=2, fast=5
  slow=3, fast=null
slow.next = slow.next.next → node(3).next = node(5)
Output: 1 → 2 → 3 → 5 ✓
```

---

### Problem 10 — Intersection of Two Linked Lists (bonus)
**LeetCode #160 | Difficulty: Easy | Variant: Two-pointer length equalisation**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | `p1` on list A, `p2` on list B, both move 1 step | |
| 2 | When `p1` reaches end, redirect to head of B | |
| 3 | When `p2` reaches end, redirect to head of A | |
| 4 | They meet at intersection or both reach null together | |

#### Java code

```java
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    ListNode p1 = headA, p2 = headB;

    while (p1 != p2) {
        p1 = (p1 == null) ? headB : p1.next;   // redirect to other list on null
        p2 = (p2 == null) ? headA : p2.next;
    }
    return p1;   // intersection node, or null if no intersection
}
```

#### Why it works

```
List A length = a + c  (a = before intersection, c = common part)
List B length = b + c

p1 travels: a + c + b  steps to reach intersection
p2 travels: b + c + a  steps to reach intersection
Both travel same total distance → meet at intersection ✓
```

---

## 8. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                        → VARIANT              → KEY CODE
───────────────────────────────────────────────────────────────────────────────────
"detect cycle"                           → Cycle detection      → slow==fast inside loop
"find cycle start / entry point"         → Floyd Phase 2        → reset slow=head, move both 1 step
"middle of linked list"                  → Find middle          → fast==null → slow=middle
"kth from end / remove nth from end"     → Gap technique        → fast starts k ahead
"palindrome linked list"                 → Middle + Reverse     → reverse from slow, compare
"reorder / rearrange linked list"        → Middle+Reverse+Merge → reverse(slow.next), slow.next=null, merge
"happy number"                           → Implicit cycle       → getNext = sum of squares
"find duplicate in array"               → Implicit cycle       → getNext = nums[i]
"cycle in circular array"               → Implicit cycle       → getNext = (i+nums[i])%n
"intersection of two lists"             → Redirect technique   → redirect to other list on null
```

**The two pointer rules — burn these into memory:**
```java
// Always check BOTH conditions
while (fast != null && fast.next != null)

// Phase 2 for cycle start — reset ONE pointer only
slow = head;
while (slow != fast) { slow = slow.next; fast = fast.next; }

// Right-middle (standard)
while (fast != null && fast.next != null)  →  slow = right-middle

// Left-middle (for palindrome / reorder — want to split evenly)
// Use slow.next for second half start instead of slow
ListNode second = reverse(slow.next);
slow.next = null;
```

---

## 9. Common mistakes

### Mistake 1 — Checking only one null condition

```java
// BUG — NPE on even-length list when fast lands exactly on null
while (fast.next != null) {
    fast = fast.next.next;   // fast is null, .next.next crashes

// FIX — always check both
while (fast != null && fast.next != null) {
    fast = fast.next.next;   // safe
```

### Mistake 2 — Wrong Phase 2 start for cycle detection

```java
// BUG — resetting BOTH pointers to head finds nothing
slow = head;
fast = head;    // WRONG — fast should stay at meeting point
while (slow != fast) { slow=slow.next; fast=fast.next; }

// FIX — reset only slow, keep fast at meeting point
slow = head;    // reset only slow
// fast stays at meeting point
while (slow != fast) { slow=slow.next; fast=fast.next; }
```

### Mistake 3 — Using slow for second half in reorder (causes cycle)

```java
// BUG — middle node shared between both halves → cycle in merge
ListNode second = reverse(slow);    // slow included in second half
// node(slow) still connected from first half → cycle

// FIX — start second half from slow.next, cut at slow
ListNode second = reverse(slow.next);
slow.next = null;   // cut first half cleanly
```

### Mistake 4 — Wrong modulo for circular array getNext

```java
// BUG — negative modulo in Java gives negative result
int next = (i + nums[i]) % n;   // nums[i] negative → next can be negative

// FIX — add n before taking mod to handle negative jumps
int next = ((i + nums[i]) % n + n) % n;   // always positive
```

### Mistake 5 — Not handling single-node cycle in circular array

```java
// BUG — a node pointing to itself counts as cycle (but problem says length > 1)
int next = ((i + nums[i]) % n + n) % n;
// if next == i, it's a self-loop → invalid, should return -1

// FIX
if (next == i) return -1;   // single-element cycle not valid
```

### Mistake 6 — Forgetting dummy node for kth-from-end removal

```java
// BUG — if target is the head node, slow has no .next to work with
ListNode slow = head, fast = head;

// FIX — use dummy so slow always has a node before the target
ListNode dummy = new ListNode(0);
dummy.next = head;
ListNode slow = dummy, fast = dummy;
// advance fast n+1 steps (not n) so slow lands BEFORE target
```

---

## 10. Complexity summary

| Problem | Time | Space | Notes |
|---------|------|-------|-------|
| LinkedList Cycle | O(n) | O(1) | fast catches slow in at most one full cycle |
| Start of LinkedList Cycle | O(n) | O(1) | Phase 1 + Phase 2, both O(n) |
| Happy Number | O(log n) | O(1) | digit sum reduces fast; cycle detected in O(log n) |
| Find Duplicate Number | O(n) | O(1) | treats array as implicit linked list |
| Middle of LinkedList | O(n) | O(1) | single pass |
| Palindrome LinkedList | O(n) | O(1) | find middle + reverse + compare |
| Reorder List | O(n) | O(1) | find middle + reverse + merge |
| Cycle in Circular Array | O(n²) | O(1) | outer loop O(n), inner Floyd O(n) per start |
| Remove Nth From End | O(n) | O(1) | single pass with gap |
| Intersection of Two Lists | O(m+n) | O(1) | both pointers travel same total distance |

**General rule:**
- Fast & Slow always gives **O(1) space** — only 2 pointer variables regardless of input size.
- Time is always **O(n)** for linked list problems.
- For implicit cycle problems (Happy Number, Find Duplicate), time depends on the sequence — typically O(n) or O(log n).
- If interviewer asks for O(n) space solution: use HashSet (simpler). O(1) space: use Fast & Slow.

---

*Fast & Slow Pointers (Floyd's Algorithm) is one of the most elegant patterns in DSA.*
*Master the two-phase cycle detection — it appears in disguised form in many non-obvious problems.*
