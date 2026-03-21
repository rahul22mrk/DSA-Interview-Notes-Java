# Heap / Priority Queue Pattern — Complete Notes

> **Pattern family:** Heap / Priority Queue / Greedy
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

| If you see this... | It means |
|--------------------|----------|
| "Kth largest / smallest element" | min-heap of size k |
| "top K frequent elements / words" | freq map + min-heap of size k |
| "K closest points / elements" | min-heap by distance, size k |
| "merge K sorted lists / arrays" | min-heap as pointer across lists |
| "find median from data stream" | two heaps (max-heap + min-heap) |
| "sliding window median" | two heaps with lazy deletion |
| "task scheduler / reorganize string" | max-heap by frequency (greedy) |
| "minimum cost / maximize profit with constraints" | greedy + heap |
| "K pairs with smallest sums" | min-heap, expand from smallest |
| "smallest range covering K lists" | min-heap across list pointers |
| "design Twitter / feed / leaderboard" | top-k with heap |
| "IPO / maximize capital" | two heaps (sorted profit + capital) |
| "course scheduler with deadline" | max-heap + greedy |

### Brute force test

```
Brute force: sort entire array / collect all elements → O(n log n).
→ Interviewer says "O(n log k)" → cannot sort everything.
→ Key insight: you only need the TOP k or BOTTOM k elements.
→ Heap of size k keeps only what you need → O(n log k) time.

Brute force for median: sort after each insert → O(n²) total.
→ Two heaps maintain sorted halves incrementally → O(log n) per insert.
```

### The 5 confirming signals

**Signal 1 — "Kth" in the problem statement**
> Any "Kth largest", "Kth smallest", "top K" = heap of size k.
> Min-heap for Kth largest (pop when size > k, top = answer).
> Max-heap for Kth smallest (pop when size > k, top = answer).

**Signal 2 — "Top K" with frequency, distance, or any comparator**
> Build a frequency/distance map, then use a min-heap of size k.
> When heap exceeds k, pop the minimum → keeps top k largest.

**Signal 3 — "Merge K sorted" structures**
> Use min-heap as a pointer — store (value, list_index, element_index).
> Always pop the global minimum, then push the next from same list.

**Signal 4 — "Median" or "running median" or "sliding window median"**
> Two heaps: max-heap for lower half, min-heap for upper half.
> Balance them so sizes differ by at most 1.
> Median = top of larger heap, or average of both tops.

**Signal 5 — "Maximum profit/activity with constraints" (Greedy)**
> Sort by one dimension, use a heap for the other.
> IPO: sort by capital, greedily pick max profit projects affordable.
> Course Scheduler: sort by deadline, greedily drop min-duration course when over.

### Decision flowchart

```
Problem involves ordering / ranking elements?
        │
        ▼
What do you need?
        │
        ├── Kth LARGEST → min-heap of size k (pop excess, top = answer)
        │
        ├── Kth SMALLEST → max-heap of size k (pop excess, top = answer)  
        │       └── OR: min-heap push all, pop k times
        │
        ├── TOP K (frequent, closest, etc.)
        │       └── freq/dist map + min-heap size k → O(n log k)
        │
        ├── MERGE K sorted lists/arrays
        │       └── min-heap with (val, list_idx, elem_idx) as pointer
        │
        ├── RUNNING MEDIAN / SLIDING WINDOW MEDIAN
        │       └── two heaps: maxHeap (lower) + minHeap (upper)
        │           balance so |maxHeap.size - minHeap.size| ≤ 1
        │
        ├── GREEDY + HEAP (maximize profit, minimize cost)
        │       ├── Sort by constraint (capital, deadline)
        │       └── Push eligible elements to heap, greedily pick best
        │
        └── DESIGN (Twitter feed, leaderboard, food rating)
                └── Per-entity heap OR global top-k query with heap
```

---

## 2. What is this pattern?

**Java's PriorityQueue is a min-heap by default.** The smallest element is always at the top.

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();              // min-heap
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder()); // max-heap
```

**Core heap operations:**
```
offer(x)  → insert x        → O(log n)
poll()    → remove and return the top (min or max)  → O(log n)
peek()    → read top without removing  → O(1)
size()    → number of elements  → O(1)
```

### Why heaps beat sorting for top-k problems

```
Sort all n elements: O(n log n) — unnecessary if we only need k
Heap of size k:      O(n log k) — only track k elements at any time

For n = 10^6, k = 100:
  Sort: 10^6 × 20 = 20,000,000 operations
  Heap: 10^6 × 7  = 7,000,000  operations  ← ~3× faster
```

### The two-heap invariant (for median)

```
maxHeap (lower half)   minHeap (upper half)
[1, 2, 3, 4]          [5, 6, 7, 8]
      ↑                      ↑
   top = 4               top = 5

Invariants:
  1. maxHeap.peek() ≤ minHeap.peek()   (all lower ≤ all upper)
  2. |maxHeap.size() - minHeap.size()| ≤ 1   (sizes balanced)

Median:
  If sizes equal → (maxHeap.peek() + minHeap.peek()) / 2.0
  If maxHeap larger → maxHeap.peek()
  If minHeap larger → minHeap.peek()
```

---

## 3. Core rules

**Rule 1 — Min-heap for Kth LARGEST, Max-heap for Kth SMALLEST**
```java
// Kth LARGEST — keep k largest, top of min-heap = kth largest
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
for (int num : nums) {
    minHeap.offer(num);
    if (minHeap.size() > k) minHeap.poll();   // evict smallest
}
return minHeap.peek();   // top = kth largest ✓

// Kth SMALLEST — keep k smallest, top of max-heap = kth smallest
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
for (int num : nums) {
    maxHeap.offer(num);
    if (maxHeap.size() > k) maxHeap.poll();   // evict largest
}
return maxHeap.peek();   // top = kth smallest ✓
```

**Rule 2 — Custom comparator syntax in Java**
```java
// By second element of int[]
PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);

// By distance (avoid overflow with Integer.compare)
PriorityQueue<int[]> pq = new PriorityQueue<>(
    (a, b) -> Integer.compare(a[0]*a[0] + a[1]*a[1], b[0]*b[0] + b[1]*b[1])
);

// Max-heap by frequency
PriorityQueue<Map.Entry<Integer,Integer>> pq = new PriorityQueue<>(
    (a, b) -> b.getValue() - a.getValue()
);
```

**Rule 3 — Two-heap balance: always add to maxHeap first, then rebalance**
```java
// Standard two-heap insert sequence:
public void addNum(int num) {
    maxHeap.offer(num);                        // 1. always add to lower half first

    if (!minHeap.isEmpty() && maxHeap.peek() > minHeap.peek()) {
        minHeap.offer(maxHeap.poll());         // 2. fix ordering if violated
    }

    // 3. rebalance sizes
    if (maxHeap.size() > minHeap.size() + 1)
        minHeap.offer(maxHeap.poll());
    else if (minHeap.size() > maxHeap.size())
        maxHeap.offer(minHeap.poll());
}
```

**Rule 4 — For merge K lists, store enough info to find the "next" element**
```java
// Store: (value, list_index, element_index)
// After popping (val, i, j), push (nums[i][j+1], i, j+1) if exists
PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[0] - b[0]);
// int[0] = value, int[1] = which list, int[2] = index in that list
```

---

## 4. 2-Question framework

### Question 1 — What are you selecting from?

| Answer | Variant |
|--------|---------|
| A single array/stream | Kth element → heap of size k |
| Multiple sorted lists | Merge K lists → heap as pointer |
| A frequency distribution | Top K frequent → freq map + heap |
| A sliding window | Window median → two heaps + lazy delete |
| Eligible candidates (greedy) | Max profit → sort + heap |
| Two halves of a stream | Running median → two heaps |

### Question 2 — What heap size / structure do you need?

| Need | Heap type | Size | Returns |
|------|-----------|------|---------|
| Kth largest | min-heap | k | peek() |
| Kth smallest | max-heap | k | peek() |
| Top k largest | min-heap | k | all elements |
| Top k smallest | max-heap | k | all elements |
| Global minimum repeatedly | min-heap | unlimited | poll() |
| Running median | two heaps | n total | computed |
| Greedy max pick | max-heap | unlimited | poll() |

> **Decision shortcut:**
> - "Kth largest" → min-heap size k, peek is answer
> - "Kth smallest" → max-heap size k, peek is answer
> - "Top K" → min-heap size k (for largest), poll excess
> - "Merge K" → min-heap as cursor, push next after pop
> - "Median" → two heaps balanced
> - "Greedy max" → max-heap, sort by constraint first

---

## 5. Variants table

> **Common core:** `PriorityQueue<>` with appropriate comparator
> **What differs:** heap type, size limit, what triggers a poll, what you return

| Variant | Heap | Size | Push | Pop when | Return |
|---------|------|------|------|----------|--------|
| Kth Largest | min-heap | k | every element | size > k | `peek()` |
| Kth Smallest | max-heap | k | every element | size > k | `peek()` |
| Top K Frequent | min-heap by freq | k | each distinct element | size > k | all in heap |
| K Closest | min-heap by dist | k | every point | size > k | all in heap |
| Merge K Lists | min-heap by val | ≤ k | next from same list | always | `poll()` |
| Running Median | two heaps | n | every number | rebalance | computed |
| Greedy (IPO) | max-heap by profit | n | all affordable | always pick max | running sum |
| Task Scheduler | max-heap by freq | 26 | all tasks | per cycle | count |
| Sliding Window Median | two heaps | window | window element | lazy delete | computed |

---

## 6. Universal Java template

```java
// ─── TEMPLATE A: Kth Largest Element ─────────────────────────────────────────
public int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();  // min-heap of size k
    for (int num : nums) {
        minHeap.offer(num);
        if (minHeap.size() > k) minHeap.poll();  // evict smallest → keep k largest
    }
    return minHeap.peek();   // top = kth largest
}


// ─── TEMPLATE B: Top K Frequent Elements ─────────────────────────────────────
public int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> freq = new HashMap<>();
    for (int n : nums) freq.merge(n, 1, Integer::sum);

    // Min-heap by frequency — evict least frequent, keep top k
    PriorityQueue<Integer> minHeap = new PriorityQueue<>(
        (a, b) -> freq.get(a) - freq.get(b)
    );
    for (int num : freq.keySet()) {
        minHeap.offer(num);
        if (minHeap.size() > k) minHeap.poll();
    }
    int[] res = new int[k];
    for (int i = k - 1; i >= 0; i--) res[i] = minHeap.poll();
    return res;
}


// ─── TEMPLATE C: K Closest Points (by distance) ──────────────────────────────
public int[][] kClosest(int[][] points, int k) {
    // Max-heap by distance — evict farthest, keep k closest
    PriorityQueue<int[]> maxHeap = new PriorityQueue<>(
        (a, b) -> (b[0]*b[0] + b[1]*b[1]) - (a[0]*a[0] + a[1]*a[1])
    );
    for (int[] point : points) {
        maxHeap.offer(point);
        if (maxHeap.size() > k) maxHeap.poll();  // remove farthest
    }
    return maxHeap.toArray(new int[k][]);
}


// ─── TEMPLATE D: Merge K Sorted Lists ────────────────────────────────────────
public ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> minHeap = new PriorityQueue<>(
        (a, b) -> a.val - b.val
    );
    for (ListNode node : lists)
        if (node != null) minHeap.offer(node);

    ListNode dummy = new ListNode(0), curr = dummy;
    while (!minHeap.isEmpty()) {
        ListNode node = minHeap.poll();
        curr.next = node;
        curr = curr.next;
        if (node.next != null) minHeap.offer(node.next);  // push next from same list
    }
    return dummy.next;
}


// ─── TEMPLATE E: Find Median from Data Stream (Two Heaps) ─────────────────────
class MedianFinder {
    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder()); // lower half
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();                            // upper half

    public void addNum(int num) {
        maxHeap.offer(num);                                      // always add to lower first
        if (!minHeap.isEmpty() && maxHeap.peek() > minHeap.peek())
            minHeap.offer(maxHeap.poll());                       // fix ordering
        if (maxHeap.size() > minHeap.size() + 1)
            minHeap.offer(maxHeap.poll());                       // rebalance
        else if (minHeap.size() > maxHeap.size())
            maxHeap.offer(minHeap.poll());                       // rebalance
    }

    public double findMedian() {
        if (maxHeap.size() == minHeap.size())
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        return maxHeap.peek();   // maxHeap has the extra element
    }
}


// ─── TEMPLATE F: Greedy + Heap (IPO / Max Profit) ────────────────────────────
public int findMaximizedCapital(int k, int w, int[] profits, int[] capital) {
    int n = profits.length;
    int[][] projects = new int[n][2];
    for (int i = 0; i < n; i++) projects[i] = new int[]{capital[i], profits[i]};
    Arrays.sort(projects, (a, b) -> a[0] - b[0]);   // sort by capital required

    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    int idx = 0;
    for (int i = 0; i < k; i++) {
        while (idx < n && projects[idx][0] <= w)     // push all affordable projects
            maxHeap.offer(projects[idx++][1]);
        if (maxHeap.isEmpty()) break;
        w += maxHeap.poll();                          // pick most profitable
    }
    return w;
}


// ─── TEMPLATE G: Two Heaps for Sliding Window Median ─────────────────────────
public double[] medianSlidingWindow(int[] nums, int k) {
    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    double[] result = new double[nums.length - k + 1];

    for (int i = 0; i < nums.length; i++) {
        // Add new element
        maxHeap.offer(nums[i]);
        minHeap.offer(maxHeap.poll());
        if (maxHeap.size() < minHeap.size()) maxHeap.offer(minHeap.poll());

        // Remove element leaving window
        if (i >= k) {
            int remove = nums[i - k];
            if (remove <= maxHeap.peek()) maxHeap.remove(remove);
            else minHeap.remove(remove);
            // Rebalance
            if (maxHeap.size() < minHeap.size()) maxHeap.offer(minHeap.poll());
            else if (maxHeap.size() > minHeap.size() + 1) minHeap.offer(maxHeap.poll());
        }

        if (i >= k - 1)
            result[i - k + 1] = k % 2 == 0
                ? ((double)maxHeap.peek() + minHeap.peek()) / 2.0
                : maxHeap.peek();
    }
    return result;
}


// ─── TEMPLATE H: Kth Smallest in Sorted Matrix ───────────────────────────────
public int kthSmallest(int[][] matrix, int k) {
    int n = matrix.length;
    // Min-heap: (value, row, col)
    PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> a[0] - b[0]);
    for (int r = 0; r < Math.min(n, k); r++)
        minHeap.offer(new int[]{matrix[r][0], r, 0});   // first element of each row

    int result = 0;
    for (int i = 0; i < k; i++) {
        int[] curr = minHeap.poll();
        result = curr[0];
        if (curr[2] + 1 < n)
            minHeap.offer(new int[]{matrix[curr[1]][curr[2]+1], curr[1], curr[2]+1});
    }
    return result;
}
```

---

## 7. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                            → VARIANT                  → KEY CODE
─────────────────────────────────────────────────────────────────────────────────────────
"Kth largest"                                → min-heap size k          → offer; if size>k poll; return peek()
"Kth smallest"                               → max-heap size k          → offer; if size>k poll; return peek()
"Top K frequent / closest / heaviest"        → min-heap size k          → freq/dist map + min-heap; poll excess
"Merge K sorted lists/arrays"                → min-heap as pointer      → (val, listIdx, elemIdx); push next after pop
"Find median from stream"                    → two heaps                → maxHeap(lower) + minHeap(upper); balance sizes
"Sliding window median"                      → two heaps + remove       → lazy delete with heap.remove()
"Maximize profit with capital constraint"    → greedy + two heaps       → sort by capital; max-heap for profit
"Task scheduler / reorganize string"         → max-heap by frequency    → always pick most frequent task
"Course schedule with deadline"              → max-heap + greedy        → sort by deadline; drop min-duration if over
"K pairs with smallest sums"                 → min-heap + expand        → push (a[0]+b[0], 0, 0); expand along both
"Smallest range covering K lists"            → min-heap + track max     → heap of (val, listIdx, elemIdx); update range
```

**Burn these into memory:**
```java
// Min-heap (Java default):
PriorityQueue<Integer> pq = new PriorityQueue<>();

// Max-heap:
PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());

// Custom comparator (NEVER use subtraction for large values — use Integer.compare):
PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> Integer.compare(a[0], b[0]));

// Kth largest trick: MIN-heap of size k → peek() = kth largest
// Kth smallest trick: MAX-heap of size k → peek() = kth smallest

// Two-heap median: maxHeap.size() ≥ minHeap.size() always
// → median = maxHeap.peek() if odd total, or average of both tops if even
```

---

## 8. Common mistakes

### Mistake 1 — Wrong heap type for Kth problem

```java
// BUG — max-heap for Kth largest keeps largest at top,
// but you'd need to pop k times to find the kth — O(k log n), not O(n log k)
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
// ...then poll k times → works but WRONG approach for streaming data

// CORRECT — min-heap of size k: top IS the kth largest continuously
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
for (int num : nums) {
    minHeap.offer(num);
    if (minHeap.size() > k) minHeap.poll();  // always evict smallest
}
return minHeap.peek();   // kth largest ✓
```

### Mistake 2 — Integer overflow in comparator

```java
// BUG — a[0]-b[0] can overflow for large negative numbers
PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[0] - b[0]);
// e.g. a[0] = Integer.MIN_VALUE, b[0] = 1 → MIN_VALUE - 1 = Integer.MAX_VALUE (wrong!)

// FIX — always use Integer.compare for safety
PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> Integer.compare(a[0], b[0]));
```

### Mistake 3 — Not rebalancing two heaps after removal (sliding window)

```java
// BUG — after removing an element from one heap, sizes may be unbalanced
maxHeap.remove(outgoing);   // removed from lower half
// forgot to rebalance → median calculation wrong

// FIX — always rebalance after removal
if (maxHeap.size() < minHeap.size()) maxHeap.offer(minHeap.poll());
else if (maxHeap.size() > minHeap.size() + 1) minHeap.offer(maxHeap.poll());
```

### Mistake 4 — Two-heap: adding to wrong heap first

```java
// BUG — adding to minHeap first can violate the ordering invariant
minHeap.offer(num);
maxHeap.offer(minHeap.poll());  // this doesn't guarantee maxHeap.peek() ≤ minHeap.peek()

// CORRECT — always add to maxHeap (lower half) first, then fix
maxHeap.offer(num);
if (!minHeap.isEmpty() && maxHeap.peek() > minHeap.peek())
    minHeap.offer(maxHeap.poll());   // move oversized element up
```

### Mistake 5 — Null pointer in merge K lists (not checking null before push)

```java
// BUG — pushing null node into heap crashes on comparison
for (ListNode node : lists) minHeap.offer(node);  // some may be null!

// FIX — null check before offering
for (ListNode node : lists)
    if (node != null) minHeap.offer(node);
// Also after poll: if (node.next != null) minHeap.offer(node.next);
```

### Mistake 6 — heap.remove() is O(n) — avoid in tight loops

```java
// WARNING — PriorityQueue.remove(element) is O(n) not O(log n)
// For sliding window median with large windows, this causes TLE

// FIX — use lazy deletion with a separate "to-remove" map
Map<Integer, Integer> toRemove = new HashMap<>();
// When element should be removed, mark it; skip it when it comes to top
while (!maxHeap.isEmpty() && toRemove.getOrDefault(maxHeap.peek(), 0) > 0) {
    toRemove.merge(maxHeap.poll(), -1, Integer::sum);
}
```

---

## 9. Complexity summary

| Problem | Time | Space | Notes |
|---------|------|-------|-------|
| Kth Largest / Smallest | O(n log k) | O(k) | heap of size k |
| Top K Frequent | O(n log k) | O(n) | freq map + heap |
| K Closest Points | O(n log k) | O(k) | distance comparator |
| Find K Closest Elements | O(log n + k) | O(k) | binary search + expansion |
| Merge K Sorted Lists | O(n log k) | O(k) | n total nodes, k lists |
| Kth Smallest in Matrix | O(k log k) | O(k) | row-pointer heap |
| Find Median from Stream | O(log n) per add, O(1) query | O(n) | two heaps |
| Sliding Window Median | O(n log k) | O(k) | lazy deletion variant |
| Task Scheduler | O(n log 26) = O(n) | O(26) = O(1) | at most 26 unique tasks |
| Reorganize String | O(n log 26) = O(n) | O(26) = O(1) | same as task scheduler |
| IPO | O(n log n) | O(n) | sort + heap |
| Course Scheduler 3 | O(n log n) | O(n) | sort by deadline + heap |
| K Pairs Smallest Sums | O(k log k) | O(k) | bounded expansion |
| Smallest Range K Lists | O(n log k) | O(k) | n total elements |
| Design Twitter | O(k log k) per getNewsFeed | O(follows + tweets) | per-user heap |

**General rules:**
- Heap gives **O(log n)** insert/delete, **O(1)** peek.
- For top-k problems: **O(n log k)** beats **O(n log n)** sort when k << n.
- Two-heap median: **O(log n)** per operation — best possible for streaming median.
- `PriorityQueue.remove(element)` is **O(n)** — use lazy deletion for sliding window.
- Heap space is **O(k)** for top-k problems, **O(n)** for two-heap median.

---

*Heap is the backbone of streaming and top-k problems in FAANG interviews.*
*Master the "min-heap for Kth largest" trick and the two-heap median — they cover 70% of heap problems.*
