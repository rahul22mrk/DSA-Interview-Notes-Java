# Slow & Fast Pointers (Floyd's Algorithm) — Notes & Templates

> **Pattern family:** LinkedList / Cycle Detection / Sequence Traversal
> **Difficulty range:** Easy → Hard
> **Language:** Java
> **Problems file:** [02_slow_fast_pointers_problems.md](./02_slow_fast_pointers_problems.md)

---

## Table of Contents

1. [How to identify this pattern](#1-how-to-identify-this-pattern) ← **start here**
2. [What is this pattern?](#2-what-is-this-pattern)
3. [Core rules](#3-core-rules)
4. [2-Question framework](#4-2-question-framework)
5. [Variants table](#5-variants-table)
6. [Pattern categories — all types covered](#6-pattern-categories--all-types-covered)
7. [Universal Java template](#7-universal-java-template)
8. [Quick reference cheatsheet](#8-quick-reference-cheatsheet)
9. [Common mistakes](#9-common-mistakes)
10. [Complexity summary](#10-complexity-summary)

---

## 1. How to identify this pattern

### Keyword scanner

| If you see this... | It means |
|--------------------|----------|
| `"detect cycle in linked list"` | Cycle detection |
| `"find start / entry point of cycle"` | Cycle start (Floyd Phase 2) |
| `"middle of linked list"` | Find middle |
| `"palindrome linked list"` | Find middle + reverse |
| `"reorder / rearrange linked list"` | Find middle + reverse + merge |
| `"happy number"` | Implicit cycle in number sequence |
| `"find duplicate in array"` | Implicit cycle via index mapping |
| `"cycle in circular array"` | Implicit cycle via jump mapping |
| `"kth node / remove nth from end"` | Gap technique (fast starts k ahead) |
| `"intersection of two linked lists"` | Redirect technique |
| `"rotate linked list / rotate array"` | Find split point + reconnect |
| `"string compression"` | Slow writes, fast reads |
| `"remove duplicates in-place"` | Slow/fast same direction |
| `"O(1) space"` + any sequence problem | Cannot use HashSet → Fast & Slow |

### Brute force test

```
Brute force: use HashSet — store every visited node, check if seen again → O(n) space.
→ Interviewer says "O(1) space" → Cannot use HashSet → Use Fast & Slow pointers.

Key insight: two pointers moving at different speeds will ALWAYS meet inside a cycle.
Fast gains exactly 1 step on slow per iteration → guaranteed meeting.
```

### The 5 confirming signals

**Signal 1 — "Detect cycle" + "O(1) space"**
> HashSet is obvious but O(n) space. Fast & Slow = O(1) space, O(n) time.

**Signal 2 — "Find middle" of a linked list**
> When fast reaches end (null), slow has traveled exactly half → slow is at middle.

**Signal 3 — Sequence that might loop back (implicit cycle)**
> Happy Number: `n → sum_of_squares(n)`. Find Duplicate: `n → nums[n]`.
> Circular Array: `i → i + arr[i]`. Floyd's works on ALL of these.

**Signal 4 — "Kth from end" or "remove nth from end"**
> Fast starts k steps ahead of slow. When fast hits null, slow is exactly at target.

**Signal 5 — "Slow writes, fast reads" (string/array compression)**
> Slow pointer = write position. Fast pointer = read position.
> Only advance slow when fast finds a "keepable" element.

### Decision flowchart

```
Problem involves a sequence (linked list / numbers / array indices)?
        │
        ├── Cycle exists?
        │       ├── Just detect it?         → Cycle Detection
        │       └── Find entry point?       → Floyd Phase 2 (reset + move 1 step each)
        │
        ├── Find middle?                    → fast/slow from head, stop when fast=null
        │
        ├── Kth from end?                   → fast starts k steps ahead
        │
        ├── Palindrome check?               → find middle + reverse second half + compare
        │
        ├── Reorder list?                   → find middle + reverse second half + merge
        │
        ├── Implicit cycle (numbers/array)? → define getNext(), apply Floyd's
        │
        ├── In-place compress/remove?       → slow=write, fast=read
        │
        └── Rotate / split + reconnect?     → find tail/split point + relink
```

---

## 2. What is this pattern?

Two pointers move through a sequence at **different speeds** — slow moves 1 step, fast moves 2 steps.

```java
slow = slow.next;        // 1 step
fast = fast.next.next;   // 2 steps
```

**Why cycle detection works:**
Fast gains 1 step on slow every iteration. Inside a cycle, fast eventually "laps" slow — guaranteed to meet. Mathematically impossible for fast to skip over slow inside a cycle.

**Why find-middle works:**
When fast reaches the end (null), slow has traveled exactly half the distance.

```
List:  1 → 2 → 3 → 4 → 5
iter1: slow=2, fast=3
iter2: slow=3, fast=5
iter3: fast=null → slow=3 = middle ✓
```

**Why this generalises beyond linked lists:**
Any sequence where each element maps to exactly one "next" forms an implicit linked list.
Floyd's algorithm works on all of them — just define `getNext()`.

```
Happy Number:    getNext(n) = sum of squares of digits of n
Find Duplicate:  getNext(i) = nums[i]
Circular Array:  getNext(i) = ((i + nums[i]) % n + n) % n
```

---

## 3. Core rules

**Rule 1 — Always check BOTH null conditions**
```java
// WRONG — NPE on even-length list when fast lands exactly on null
while (fast.next != null) {
    fast = fast.next.next;   // fast could be null here → crashes
}

// CORRECT — both conditions required
while (fast != null && fast.next != null) {
    fast = fast.next.next;   // safe
}
// fast != null       → prevents NPE when fast lands on null (even-length list)
// fast.next != null  → prevents NPE when trying fast.next.next
```

**Rule 2 — Cycle start: reset ONE pointer to head, keep other at meeting point**
```java
// After slow == fast (meeting point inside cycle):
slow = head;              // reset slow to head ONLY
// fast stays at meeting point

while (slow != fast) {
    slow = slow.next;     // both move 1 step
    fast = fast.next;
}
// slow == fast == cycle start node

// WHY IT WORKS:
// Let F = distance head → cycle start
//     C = cycle length
//     k = distance cycle start → meeting point
// At meeting: slow traveled F+k, fast traveled F+k+C
// Since fast = 2×slow: F+k = C → F = C-k
// So distance from meeting point to cycle start = F (same as head to cycle start)
// Moving both at speed 1: they meet at cycle start ✓
```

**Rule 3 — For find-middle: right-middle vs left-middle**
```java
// Standard: both start at head → gives RIGHT-MIDDLE (for even length)
ListNode slow = head, fast = head;
while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
}
// slow = right-middle

// For LEFT-MIDDLE (use when splitting for palindrome/reorder):
// Use slow.next as start of second half
ListNode second = slow.next;
slow.next = null;   // cut here → slow is left-middle, second starts right-middle
```

---

## 4. 2-Question framework

### Question 1 — What kind of traversal do you need?

| Goal | Variant | Key code |
|------|---------|----------|
| Detect cycle | Cycle detection | `slow==fast` inside loop |
| Find where cycle starts | Floyd Phase 2 | reset slow=head after meeting |
| Find middle node | Find middle | check `fast==null` |
| Remove kth from end | Gap technique | fast starts k steps ahead |
| Check/process palindrome | Middle + Reverse | reverse from `slow.next` |
| Restructure list | Middle + Reverse + Merge | split at slow, reverse, merge |
| Non-linked-list loop | Implicit cycle | define `getNext()` |
| Compress / deduplicate | Slow writes, fast reads | advance slow only on valid |

### Question 2 — Is the cycle explicit or implicit?

| Type | Example | How to apply |
|------|---------|-------------|
| **Explicit** | Actual linked list with `.next` | Direct: `slow=slow.next`, `fast=fast.next.next` |
| **Implicit** | Happy Number, Find Duplicate, Circular Array | Define `getNext(n)` function that acts as `.next` |

```java
// Implicit cycle template
int slow = start, fast = start;
do {
    slow = getNext(slow);
    fast = getNext(getNext(fast));
} while (slow != fast);
// met → check if 1 (happy) or reset for start
```

> **Decision shortcut:**
> - "cycle exists?" → detect only
> - "where does it start?" → detect + Phase 2 reset
> - "middle?" → check fast==null
> - "kth from end?" → gap technique with dummy node
> - "number/array loops?" → implicit cycle

---

## 5. Variants table

> **Common core:** slow moves 1 step, fast moves 2 steps
> **What differs:** starting conditions, loop termination, what you return

| Variant | Slow starts | Fast starts | Loop ends when | Return |
|---------|-------------|-------------|----------------|--------|
| Cycle detection | `head` | `head` | `slow==fast` or `fast==null` | `true`/`false` |
| Cycle start | reset to `head` after meeting | `meeting point` | `slow==fast` | `slow` = cycle start |
| Find middle | `head` | `head` | `fast==null \|\| fast.next==null` | `slow` = middle |
| Kth from end | `dummy` | `dummy + k+1 steps` | `fast==null` | `slow.next` = target |
| Palindrome | `head` | `head` | `fast==null` | reverse from `slow`, compare |
| Reorder list | `head` | `head` | `fast==null` | reverse `slow.next`, cut, merge |
| Happy number | `n` | `n` | `slow==fast` | `slow==1` → happy |
| Find duplicate | `nums[0]` | `nums[0]` | `slow==fast` | Phase 2 reset → `slow` |
| Slow write / fast read | `0` | `0` | `fast == n` | `slow` = new length |

---

## 6. Pattern categories — all types covered

### Category 1 — Classic Floyd's (Linked List Cycle)
> slow and fast on actual linked list nodes. Meet inside cycle → detect / find start.

```java
// Detect
while (fast != null && fast.next != null) {
    slow = slow.next; fast = fast.next.next;
    if (slow == fast) return true;
}
return false;

// Find start (after detection)
slow = head;
while (slow != fast) { slow = slow.next; fast = fast.next; }
return slow;   // cycle start
```
**Problems:** LinkedList Cycle, Start of Cycle, Rotate List (find tail)

---

### Category 2 — Find Middle + Process
> Use find-middle as step 1, then do something with both halves.

```java
// Find middle
while (fast != null && fast.next != null) {
    slow = slow.next; fast = fast.next.next;
}
// For palindrome:   reverse from slow, compare
// For reorder:      reverse slow.next, cut at slow, merge alternately
// For split-merge:  second half = slow.next; slow.next = null
```
**Problems:** Middle of LinkedList, Palindrome LinkedList, Reorder List, Sort List

---

### Category 3 — Gap Technique (Kth from End)
> Fast pointer starts k steps ahead. When fast hits null, slow is k steps from end.

```java
ListNode dummy = new ListNode(0); dummy.next = head;
ListNode slow = dummy, fast = dummy;
for (int i = 0; i <= k; i++) fast = fast.next;   // advance fast k+1 steps
while (fast != null) { slow = slow.next; fast = fast.next; }
// slow is now one before the kth-from-end node
```
**Problems:** Remove Nth from End, Find Kth from End

---

### Category 4 — Implicit Cycle (Number / Array)
> No linked list. Define getNext() to model the problem as a linked list.

```java
// Template
int slow = start, fast = start;
do {
    slow = getNext(slow);
    fast = getNext(getNext(fast));
} while (slow != fast);
// Use Phase 2 if you need the cycle start
```

| Problem | getNext definition |
|---------|-------------------|
| Happy Number | `sum of squares of digits` |
| Find Duplicate | `nums[i]` |
| Circular Array Cycle | `((i + nums[i]) % n + n) % n` |

**Problems:** Happy Number, Find Duplicate Number, Circular Array Loop

---

### Category 5 — Slow Write / Fast Read (Compression / Deduplication)
> Slow = write pointer. Fast = read pointer. O(1) space, O(n) time.
> Advance slow only when fast finds a valid element to keep.

```java
int slow = 0;
for (int fast = 0; fast < n; fast++) {
    if (shouldKeep(arr[fast])) {
        arr[slow++] = arr[fast];
    }
}
return slow;   // new length

// For string compression:
int slow = 0, fast = 0;
while (fast < n) {
    char ch = s[fast]; int count = 0;
    while (fast < n && s[fast] == ch) { fast++; count++; }
    result[slow++] = ch;
    if (count > 1) { /* write count digits */ }
}
```
**Problems:** String Compression, Remove Duplicates I & II, Duplicate Zeros, Last Substring

---

### Category 6 — Rotate / Split + Reconnect
> Find the split point (kth from end or cycle tail), then relink.

```java
// Rotate List by k:
// Step 1: find length and tail
// Step 2: effective rotation = k % length
// Step 3: find new tail = (length - k%length) from start
// Step 4: new head = newTail.next; newTail.next = null; tail.next = head
```
**Problems:** Rotate List, Rotate Array

---

### Category 7 — Two-Pointer on Strings (Same Direction)
> Used for partition_labels, string problems where one pointer scans, other tracks boundary.

```java
// Partition Labels pattern:
// fast scans to find last occurrence of each char
// slow marks start of current partition
int[] last = new int[26];
for (int i = 0; i < s.length(); i++) last[s.charAt(i)-'a'] = i;

int slow = 0, maxReach = 0;
for (int fast = 0; fast < s.length(); fast++) {
    maxReach = Math.max(maxReach, last[s.charAt(fast)-'a']);
    if (fast == maxReach) {
        result.add(fast - slow + 1);
        slow = fast + 1;
    }
}
```
**Problems:** Partition Labels, Counting Binary Substrings

---

### Summary — all 7 categories

| # | Category | Pointer speeds | Key idea |
|---|----------|---------------|---------|
| 1 | Classic Floyd's | slow=1, fast=2 | meet in cycle |
| 2 | Find middle + process | slow=1, fast=2 | fast=null → slow=middle |
| 3 | Gap technique | same speed, different start | k-step gap maintained |
| 4 | Implicit cycle | slow=1, fast=2 | define getNext() |
| 5 | Slow write / fast read | slow writes, fast reads all | slow advances only on valid |
| 6 | Rotate / reconnect | varies | find split point, relink |
| 7 | String two-pointer | fast scans, slow marks | partition boundary tracking |

---

## 7. Universal Java template

```java
// ─── TEMPLATE A: Cycle Detection ─────────────────────────────────────────────
public boolean hasCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true;
    }
    return false;
}

// ─── TEMPLATE B: Cycle Start (Floyd Phase 2) ─────────────────────────────────
public ListNode detectCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next; fast = fast.next.next;
        if (slow == fast) {
            slow = head;                // reset slow to head only
            while (slow != fast) { slow = slow.next; fast = fast.next; }
            return slow;               // cycle start
        }
    }
    return null;
}

// ─── TEMPLATE C: Find Middle ──────────────────────────────────────────────────
public ListNode findMiddle(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;   // right-middle (use slow.next for second half in split)
}

// ─── TEMPLATE D: Gap Technique (Kth from end) ────────────────────────────────
public ListNode kthFromEnd(ListNode head, int k) {
    ListNode dummy = new ListNode(0); dummy.next = head;
    ListNode slow = dummy, fast = dummy;
    for (int i = 0; i <= k; i++) fast = fast.next;  // advance k+1 steps
    while (fast != null) { slow = slow.next; fast = fast.next; }
    return slow.next;   // kth from end node
}

// ─── TEMPLATE E: Implicit Cycle ──────────────────────────────────────────────
public boolean isHappy(int n) {
    int slow = n, fast = n;
    do {
        slow = getNext(slow);
        fast = getNext(getNext(fast));
    } while (slow != fast);
    return slow == 1;
}
private int getNext(int n) {
    int sum = 0;
    while (n > 0) { int d = n % 10; sum += d * d; n /= 10; }
    return sum;
}

// ─── TEMPLATE F: Slow Write / Fast Read ──────────────────────────────────────
public int compress(char[] chars) {
    int slow = 0, fast = 0, n = chars.length;
    while (fast < n) {
        char ch = chars[fast]; int count = 0;
        while (fast < n && chars[fast] == ch) { fast++; count++; }
        chars[slow++] = ch;
        if (count > 1) {
            for (char c : String.valueOf(count).toCharArray())
                chars[slow++] = c;
        }
    }
    return slow;
}

// ─── TEMPLATE G: Find Middle + Split + Reverse + Merge ───────────────────────
public void reorderList(ListNode head) {
    // Step 1: find middle
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next; fast = fast.next.next;
    }
    // Step 2: reverse second half
    ListNode second = reverse(slow.next);
    slow.next = null;   // cut
    // Step 3: merge alternately
    ListNode first = head;
    while (second != null) {
        ListNode t1 = first.next, t2 = second.next;
        first.next = second; second.next = t1;
        first = t1; second = t2;
    }
}
private ListNode reverse(ListNode head) {
    ListNode prev = null, curr = head;
    while (curr != null) {
        ListNode next = curr.next; curr.next = prev; prev = curr; curr = next;
    }
    return prev;
}
```

---

## 8. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                        → CATEGORY          → KEY CODE
──────────────────────────────────────────────────────────────────────────────
"detect cycle"                           → Cat 1             → slow==fast inside loop
"find cycle start / entry point"         → Cat 1 Phase 2     → reset slow=head, both move 1 step
"middle of linked list"                  → Cat 2             → fast==null → slow=middle
"palindrome linked list"                 → Cat 2             → reverse from slow.next, compare
"reorder / rearrange linked list"        → Cat 2             → reverse slow.next, cut, merge
"kth from end / remove nth"              → Cat 3             → dummy + fast k+1 ahead
"happy number"                           → Cat 4             → getNext = sum of digit squares
"find duplicate in array"                → Cat 4             → getNext = nums[i]
"cycle in circular array"                → Cat 4             → getNext = ((i+nums[i])%n+n)%n
"string compression"                     → Cat 5             → slow writes, fast reads
"remove duplicates in-place"             → Cat 5             → slow writes new value only
"rotate linked list"                     → Cat 6             → find new tail, relink
"partition labels"                       → Cat 7             → last occurrence array + boundary
"intersection of two linked lists"       → Redirect          → redirect to other list on null
```

**The 3 lines to memorise:**
```java
// 1. Always check BOTH conditions
while (fast != null && fast.next != null)

// 2. Phase 2: reset ONLY slow, fast stays at meeting point
slow = head;
while (slow != fast) { slow = slow.next; fast = fast.next; }

// 3. For second half: start from slow.next, cut at slow
ListNode second = reverse(slow.next); slow.next = null;
```

---

## 9. Common mistakes

### Mistake 1 — Only one null condition → NPE

```java
// BUG
while (fast.next != null) { fast = fast.next.next; }   // NPE on even list

// FIX
while (fast != null && fast.next != null) { ... }
```

### Mistake 2 — Resetting BOTH pointers in Phase 2

```java
// BUG — resets fast too, logic fails
slow = head; fast = head;   // WRONG

// FIX — reset slow only, fast stays at meeting point
slow = head;   // fast stays where it is
```

### Mistake 3 — Including middle in second half (reorder list)

```java
// BUG — cycle in merge because node(slow) shared
ListNode second = reverse(slow);

// FIX — start second half from slow.next, cut at slow
ListNode second = reverse(slow.next);
slow.next = null;
```

### Mistake 4 — Negative modulo in circular array getNext

```java
// BUG — Java % returns negative for negative nums[i]
int next = (i + nums[i]) % n;

// FIX — always positive
int next = ((i + nums[i]) % n + n) % n;
```

### Mistake 5 — No dummy node for remove nth from end

```java
// BUG — fails when removing head node (slow has nothing before it)
ListNode slow = head, fast = head;

// FIX — dummy ensures slow is always one node before the target
ListNode dummy = new ListNode(0); dummy.next = head;
ListNode slow = dummy, fast = dummy;
for (int i = 0; i <= n; i++) fast = fast.next;  // n+1 steps, not n
```

### Mistake 6 — Self-loop in circular array is invalid

```java
// BUG — self-loop treated as a valid cycle
// The problem says cycle length must be > 1

// FIX — check if next == current before accepting
int next = ((i + nums[i]) % n + n) % n;
if (next == i) break;   // self-loop → not a valid cycle
```

---

## 10. Complexity summary

| Problem | Time | Space | Notes |
|---------|------|-------|-------|
| LinkedList Cycle (detect) | O(n) | O(1) | fast catches slow in ≤ one cycle |
| Start of LinkedList Cycle | O(n) | O(1) | Phase 1 + Phase 2, both O(n) |
| Middle of LinkedList | O(n) | O(1) | single pass |
| Palindrome LinkedList | O(n) | O(1) | find middle + reverse + compare |
| Reorder List | O(n) | O(1) | find middle + reverse + merge |
| Remove Nth from End | O(n) | O(1) | single pass with gap |
| Happy Number | O(log n) | O(1) | digit sum reduces quickly |
| Find Duplicate Number | O(n) | O(1) | implicit linked list |
| Circular Array Loop | O(n²) | O(1) | O(n) per start, O(n) starts |
| Intersection of Two Lists | O(m+n) | O(1) | travel same total distance |
| String Compression | O(n) | O(1) | single pass slow/fast |
| Remove Duplicates | O(n) | O(1) | single pass slow/fast |
| Rotate List | O(n) | O(1) | find tail + relink |
| Partition Labels | O(n) | O(1) | last occurrence + boundary scan |

**General rules:**
- Fast & Slow → always **O(1) space**, only 2 pointer variables
- Linked list problems → **O(n) time**
- Implicit cycle (Happy Number) → **O(log n)** — digit sum converges fast
- O(n) space alternative: HashSet (simpler but not optimal)
