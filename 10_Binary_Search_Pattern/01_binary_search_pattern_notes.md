# Binary Search — Notes & Templates

> **Pattern family:** Divide and Conquer / Search
> **Difficulty range:** Easy → Hard
> **Language:** Java
> **Problems file:** [02_binary_search_problems.md](./02_binary_search_problems.md)

---

## Table of Contents

1. [How to identify this pattern](#1-how-to-identify-this-pattern) ← **start here**
2. [What is this pattern?](#2-what-is-this-pattern)
3. [Core rules](#3-core-rules)
4. [2-Question framework](#4-2-question-framework)
5. [Variants table](#5-variants-table)
5b. [Pattern categories — all 5 covered](#5b-pattern-categories--all-5-covered)
6. [Universal Java template](#6-universal-java-template)
7. [Quick reference cheatsheet](#7-quick-reference-cheatsheet)
8. [Common mistakes](#8-common-mistakes)
9. [Complexity summary](#9-complexity-summary)

---

---

## 1. How to identify this pattern

### Keyword scanner

| If you see this... | It means |
|--------------------|----------|
| "sorted array" + "find target" | classic binary search |
| "find first / last occurrence" | left-boundary / right-boundary search |
| "find minimum / maximum" in sorted/rotated | range binary search |
| "search in rotated sorted array" | rotated array search |
| "peak element / mountain array" | peak finding |
| "minimize the maximum" OR "maximize the minimum" | binary search on answer |
| "minimum days / capacity / speed to achieve X" | binary search on answer |
| "kth smallest / largest" | binary search on value |
| "allocate / split / distribute among k groups" | binary search on answer |
| "infinite sorted array" | exponential search + binary search |
| "2D matrix sorted row and column wise" | 2D binary search |
| "median of two sorted arrays" | binary search on partition |

### Brute force test

```
Brute force: linear scan O(n) — check every element one by one.
→ If input is SORTED (or can be made monotone), you can eliminate half the search space each step.
→ That elimination = Binary Search = O(log n).

Key insight: if you can write a function f(x) such that:
  f(x) = true  for all x in one half
  f(x) = false for all x in the other half
→ Binary search can find the boundary in O(log n).
```

### The 5 confirming signals

**Signal 1 — Sorted input (array, matrix, implicit sequence)**
> Sorted = you can eliminate half. If input is sorted and you need to find something → Binary Search.

**Signal 2 — "Minimize the maximum" or "Maximize the minimum"**
> Classic binary search on answer. The answer space is a range [lo, hi]. Check if mid is feasible.

**Signal 3 — O(log n) time required**
> Interviewer hints "can you do better than O(n)?" on a sorted input → Binary Search.

**Signal 4 — Monotone feasibility function**
> You can write `boolean canDo(int x)` where all values ≤ threshold are true (or false). → Binary search the threshold.

**Signal 5 — "Kth smallest/largest" in sorted structure**
> Binary search on the value range, count how many elements ≤ mid.

### Decision flowchart

```
Is the search space sorted or monotone?
        │
        ├── YES → Are you searching for an exact value?
        │              ├── YES → Classic Binary Search
        │              └── NO  → Are you searching for a boundary (first/last true)?
        │                             ├── YES → Left-boundary or Right-boundary search
        │                             └── NO  → Is it rotated / has a peak?
        │                                           ├── Rotated → Rotated Array Search
        │                                           └── Peak    → Peak Finding
        │
        └── NO  → Can you define a feasibility function on an answer range?
                       ├── YES → Binary Search on Answer (allocate/ship/speed problems)
                       └── NO  → Not Binary Search
```

---

## 2. What is this pattern?

Binary search eliminates half the search space in every iteration. Instead of checking every element, you check the **middle** and decide which half cannot contain the answer.

```
Search space: [lo ────────────── mid ────────────── hi]
                    eliminate left        or        eliminate right
```

**The fundamental invariant:**
At every step, the answer lies in `[lo, hi]`. When `lo > hi` (or `lo == hi`), you've found it.

**Two types of binary search:**

**Type 1 — Search for a value** (exact match)
```
Find target in sorted array.
Loop: while lo <= hi
```

**Type 2 — Search for a boundary** (first true / last true)
```
Find the leftmost position where condition is true.
Loop: while lo < hi  (lo and hi converge to the answer)
```

**Type 3 — Binary search on answer** (not on array index)
```
lo = minimum possible answer, hi = maximum possible answer.
Check: canAchieve(mid) → shrink lo or hi.
```

---

## 3. Core rules

**Rule 1 — Choose the right loop condition**
```java
// Type 1: searching for exact value — loop while range is non-empty
while (lo <= hi) {
    int mid = lo + (hi - lo) / 2;
    if (arr[mid] == target) return mid;
    else if (arr[mid] < target) lo = mid + 1;
    else hi = mid - 1;
}
return -1;

// Type 2: searching for boundary — loop until lo and hi meet
while (lo < hi) {
    int mid = lo + (hi - lo) / 2;
    if (condition(mid)) hi = mid;      // mid could be answer, don't exclude it
    else lo = mid + 1;                 // mid is not answer, exclude it
}
return lo;   // lo == hi == answer
```

**Rule 2 — Always compute mid as `lo + (hi - lo) / 2` to prevent overflow**
```java
// WRONG — overflows when lo + hi > Integer.MAX_VALUE
int mid = (lo + hi) / 2;

// CORRECT — never overflows
int mid = lo + (hi - lo) / 2;
```

**Rule 3 — Update lo/hi correctly based on what you're searching**
```java
// Searching for LEFTMOST (first occurrence / lower bound):
if (arr[mid] >= target) hi = mid;      // keep mid as candidate
else lo = mid + 1;

// Searching for RIGHTMOST (last occurrence / upper bound):
if (arr[mid] <= target) lo = mid;      // keep mid as candidate, but use mid+1 guard
else hi = mid - 1;
// Note: when lo = mid (not mid+1), use mid = lo + (hi - lo + 1) / 2 to avoid infinite loop
```

---

## 4. 2-Question framework

### Question 1 — What is your search space?

| Answer | Search space | lo / hi |
|--------|-------------|---------|
| Sorted array index | array indices | `lo=0, hi=n-1` |
| Value in a range | value range | `lo=min_val, hi=max_val` |
| Answer to an optimization | answer range | `lo=min_ans, hi=max_ans` |
| 2D matrix | row × col mapped to 1D | `lo=0, hi=m*n-1` |

### Question 2 — What is your condition / predicate?

| Condition type | Example | Search for |
|---------------|---------|-----------|
| Exact match | `arr[mid] == target` | the index |
| First true | `arr[mid] >= target` | leftmost index |
| Last true | `arr[mid] <= target` | rightmost index |
| Feasibility | `canShip(mid, days)` | minimum mid where true |
| Count ≥ k | `countLE(mid) >= k` | smallest mid satisfying count |

> **Decision shortcut:**
> - "find index of value" → exact match, `while lo <= hi`
> - "first/last occurrence" → boundary search, `while lo < hi`
> - "minimize X such that condition holds" → binary search on answer, `while lo < hi`
> - "rotated array" → check which half is sorted, search in sorted half
> - "peak / mountain" → compare mid with neighbors

---

## 5. Variants table

> **Common core:** compute `mid`, eliminate half the search space  
> **What differs:** what lo/hi represent, the condition, and how you update lo/hi

| Variant | lo / hi | Condition | Update rule | Return |
|---------|---------|-----------|-------------|--------|
| Classic search | array indices | `arr[mid] == target` | `lo=mid+1` or `hi=mid-1` | `mid` or `-1` |
| Lower bound (first ≥ target) | array indices | `arr[mid] >= target` | `hi=mid` or `lo=mid+1` | `lo` |
| Upper bound (last ≤ target) | array indices | `arr[mid] <= target` | `lo=mid` or `hi=mid-1` | `lo` |
| Count occurrences | array indices | lower + upper bound | — | `upper - lower + 1` |
| Rotated array | array indices | which half sorted? | search sorted half | `mid` or `-1` |
| Peak element | array indices | `arr[mid] < arr[mid+1]` | `lo=mid+1` or `hi=mid` | `lo` |
| Binary search on answer | answer range | `feasible(mid)` | `lo=mid+1` or `hi=mid` | `lo` |
| 2D matrix | `[0, m*n-1]` | map mid to `[row][col]` | standard | `mid` or `-1` |
| Kth smallest | value range | `countLE(mid) >= k` | `lo=mid+1` or `hi=mid` | `lo` |

---

## 5b. Pattern categories — all 5 covered

### Category 1 — Basic Binary Search
> Exact value search in a sorted array. The foundation — everything else builds on this.

| Problems covered |
|-----------------|
| Binary Search (basic) |
| Search Insert Position (Upper Bound / Ceiling) |
| First and Last Position |
| Search in 2D Matrix (row-first sorted) |

---

### Category 2 — Range Search (Rotated / Infinite / Boundary)
> Array is sorted but modified (rotated, infinite, or needs boundary detection).

| Problems covered |
|-----------------|
| Search in Rotated Sorted Array |
| Find Minimum in Rotated Sorted Array |
| Find Number of Rotations |
| Search in Infinite Sorted Array |
| Count Number of Occurrences (lower + upper bound) |

---

### Category 3 — Allocate Problems (Binary Search on Answer)
> You don't search in the array — you search in the **answer space**. Classic "minimize the maximum" or "maximize the minimum" problems. All use a `feasible(mid)` check.

| Problems covered |
|-----------------|
| Koko Eating Bananas |
| Capacity to Ship Packages in D Days |
| Book Allocation Problem |
| Split Array Largest Sum |
| Aggressive Cows |
| Min Days to Make M Bouquets |
| Maximum Candies to K Children |
| H-Index II |

**The universal feasibility pattern:**
```java
// "Can we achieve the goal if the answer is mid?"
boolean feasible(int[] arr, int mid) {
    int groups = 1, current = 0;
    for (int x : arr) {
        if (current + x > mid) { groups++; current = 0; }
        current += x;
    }
    return groups <= k;   // k = number of parts/students/ships/days
}
```

---

### Category 4 — Counting Occurrences
> Use left boundary + right boundary to count how many times a value appears in a sorted array.

| Problems covered |
|-----------------|
| Count Number of Occurrences |
| First and Last Position (foundation) |
| Kth Smallest in Sorted Matrix (count ≤ mid) |
| Kth Smallest in Multiplication Table (count ≤ mid) |
| Median of Two Sorted Arrays (partition count) |

**The counting pattern:**
```java
int count = findLast(arr, target) - findFirst(arr, target) + 1;

// OR: for kth-smallest problems — count how many elements ≤ mid
int countLE(int mid) {
    // return number of elements ≤ mid
}
// Binary search: find smallest mid where countLE(mid) >= k
```

---

### Category 5 — Bitonic Array Search (Mountain / Peak)
> Array increases then decreases (bitonic). Find the peak, or search in either half.

| Problems covered |
|-----------------|
| Peak Index in Mountain Array (find peak) |
| Find Peak Element (any local peak) |
| Search in Bitonic / Mountain Array (search value) |

**The bitonic pattern:**
```java
// Step 1: find peak
int peak = findPeak(arr);

// Step 2: binary search in ascending half [0..peak]
int result = binarySearch(arr, 0, peak, target);

// Step 3: if not found, binary search in descending half [peak..n-1]
if (result == -1) result = binarySearchDescending(arr, peak, arr.length - 1, target);
```

**Peak finding — the core:**
```java
while (lo < hi) {
    int mid = lo + (hi - lo) / 2;
    if (arr[mid] < arr[mid + 1]) lo = mid + 1;  // ascending → peak is right
    else hi = mid;                                // descending → peak ≤ mid
}
// lo == peak index
```

---

### Summary — 5 patterns at a glance

| # | Pattern | Search space | Key operation | Template |
|---|---------|-------------|---------------|----------|
| 1 | Basic Binary Search | Array indices | `arr[mid] == target` | `while lo <= hi` |
| 2 | Range Search | Modified sorted array | Compare mid with neighbors or hi | `while lo <= hi` or `lo < hi` |
| 3 | Allocate (BS on Answer) | Answer value range | `feasible(mid)` | `while lo < hi` |
| 4 | Counting Occurrences | Array indices | `findFirst + findLast` | two boundary searches |
| 5 | Bitonic Array | Array indices | Find peak first, then search halves | `while lo < hi` for peak |

---

## 6. Universal Java template

```java
// ─── TEMPLATE A: Classic Binary Search (exact match) ─────────────────────────
public int binarySearch(int[] arr, int target) {
    int lo = 0, hi = arr.length - 1;

    while (lo <= hi) {                         // non-empty range
        int mid = lo + (hi - lo) / 2;          // overflow-safe mid

        if (arr[mid] == target) return mid;     // found
        else if (arr[mid] < target) lo = mid + 1;  // target in right half
        else hi = mid - 1;                     // target in left half
    }
    return -1;   // not found
}

// ─── TEMPLATE B: Left Boundary (first position where arr[mid] >= target) ──────
public int lowerBound(int[] arr, int target) {
    int lo = 0, hi = arr.length;   // hi = n (one past end — target may not exist)

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (arr[mid] >= target) hi = mid;      // mid is a candidate → shrink right
        else lo = mid + 1;                     // mid too small → shrink left
    }
    return lo;   // first index where arr[lo] >= target  (lo==hi)
}

// ─── TEMPLATE C: Right Boundary (last position where arr[mid] <= target) ───────
public int upperBound(int[] arr, int target) {
    int lo = 0, hi = arr.length;

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (arr[mid] <= target) lo = mid + 1;  // mid is a candidate → shrink left
        else hi = mid;
    }
    return lo - 1;   // last index where arr[lo-1] <= target
}

// ─── TEMPLATE D: Binary Search on Answer ─────────────────────────────────────
// "Find minimum X such that feasible(X) is true"
public int searchOnAnswer(int[] arr, int lo, int hi) {
    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (feasible(arr, mid)) hi = mid;      // mid works → try smaller
        else lo = mid + 1;                     // mid doesn't work → need larger
    }
    return lo;   // minimum feasible value
}

private boolean feasible(int[] arr, int mid) {
    // Problem-specific: can we achieve the goal with value = mid?
    return true;  // replace with actual logic
}

// ─── TEMPLATE E: Rotated Array Search ────────────────────────────────────────
public int searchRotated(int[] arr, int target) {
    int lo = 0, hi = arr.length - 1;

    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if (arr[mid] == target) return mid;

        if (arr[lo] <= arr[mid]) {             // left half is sorted
            if (target >= arr[lo] && target < arr[mid]) hi = mid - 1;
            else lo = mid + 1;
        } else {                               // right half is sorted
            if (target > arr[mid] && target <= arr[hi]) lo = mid + 1;
            else hi = mid - 1;
        }
    }
    return -1;
}
```

---

## 7. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                              → VARIANT                → KEY CODE
──────────────────────────────────────────────────────────────────────────────────────
"find target in sorted array"                  → Classic search         → lo<=hi, return mid or -1
"first/last occurrence / count"                → Boundary search        → lo<hi, hi=mid or lo=mid+1
"search insert position / ceiling"             → Lower bound            → lo<hi, hi=mid if >=target
"minimum in rotated sorted"                    → Rotated minimum        → compare mid with hi
"search in rotated sorted"                     → Rotated search         → find sorted half, check range
"peak element / mountain"                      → Peak finding           → lo<hi, compare mid with mid+1
"minimize maximum / maximize minimum"          → Binary search answer   → feasible(mid), hi=mid or lo=mid+1
"ship packages / eating bananas / days"        → Binary search answer   → canDo(mid) feasibility check
"allocate books / split array"                 → Binary search answer   → minimize max, canAllocate check
"kth smallest in sorted matrix"                → Count ≤ mid            → countLE(mid) >= k
"median of two sorted arrays"                  → Partition search       → binary search on partition index
"2D matrix sorted rows+cols"                   → Staircase search       → top-right corner, O(m+n)
"2D matrix row-first sorted"                   → 1D binary search       → mid/n, mid%n mapping
"rotated array with duplicates"                → Shrink on equal        → lo++/hi-- when ambiguous
"single non-duplicate in sorted"               → Parity check           → nums[mid]==nums[mid^1]?
"k closest elements to x"                      → Window binary search   → x-arr[mid] vs arr[mid+k]-x
"timestamp get latest ≤ t"                     → Right boundary         → find largest timestamp <= t
"kth missing positive"                         → Missing count          → arr[mid]-(mid+1) >= k
"minimum speed / arrival time"                 → Binary search answer   → canArrive(mid, hour)
"minimize max gas station distance"            → Decimal binary search  → hi-lo > 1e-6 precision
```

**Template picker:**
```
Exact value in sorted array   →  while (lo <= hi)   +  return mid / -1
First/last position           →  while (lo < hi)    +  hi=mid or lo=mid (boundary)
Minimize feasible answer      →  while (lo < hi)    +  hi=mid (feasible) or lo=mid+1
Maximize feasible answer      →  while (lo < hi)    +  lo=mid (use upper mid!) or hi=mid-1
```

**Upper mid vs Lower mid:**
```java
int mid = lo + (hi - lo) / 2;       // lower mid — use when lo=mid+1 in false branch
int mid = lo + (hi - lo + 1) / 2;   // upper mid — use when lo=mid in true branch (maximize)
```

---

## 8. Common mistakes

### Mistake 1 — Wrong loop condition causes infinite loop or missed answer

```java
// BUG: for boundary search, lo <= hi may loop forever when lo = hi
while (lo <= hi) {
    if (condition) hi = mid;   // lo=hi=mid → infinite loop
}

// FIX: use lo < hi for boundary search
while (lo < hi) {
    if (condition) hi = mid;   // guaranteed to shrink
}
```

### Mistake 2 — Integer overflow in mid calculation

```java
// BUG — overflows when lo + hi > 2^31 - 1
int mid = (lo + hi) / 2;

// FIX — overflow-safe
int mid = lo + (hi - lo) / 2;
```

### Mistake 3 — Wrong mid for "maximize" problems (lower mid causes infinite loop)

```java
// BUG — infinite loop when lo=3, hi=4, lo=mid
int mid = lo + (hi - lo) / 2;      // lower mid = 3
if (feasible(mid)) lo = mid;        // lo stays 3 → stuck

// FIX — use upper mid when lo=mid
int mid = lo + (hi - lo + 1) / 2;  // upper mid = 4 → lo becomes 4 → terminates
```

### Mistake 4 — Off-by-one in hi for lower/upper bound

```java
// BUG — if target is larger than all elements, lo goes out of bounds
int hi = arr.length - 1;
// lo becomes arr.length which is out of bounds

// FIX — set hi = arr.length (one past end) for insertion point problems
int hi = arr.length;
```

### Mistake 5 — Wrong lo/hi for binary search on answer

```java
// BUG — wrong range misses the actual answer
int lo = 0, hi = Integer.MAX_VALUE;   // too large, wastes iterations

// FIX — tightly bound lo and hi to the actual answer range
int lo = maxSingle;   // minimum possible answer
int hi = total;       // maximum possible answer
```

### Mistake 6 — Not handling edge cases in rotated array

```java
// BUG — misses the case when lo=mid (only 2 elements)
if (arr[lo] < arr[mid])   // strict: fails when lo==mid (2 elements, left part = 1 element)

// FIX — use <= to handle 2-element edge cases
if (arr[lo] <= arr[mid])
```

### Mistake 7 — Ceiling formula for integer division

```java
// WRONG — integer division floors
int hours = pile / speed;   // misses partial hour

// CORRECT — ceiling division
int hours = (pile + speed - 1) / speed;
// or equivalently:
int hours = (int) Math.ceil((double) pile / speed);
```

---

## 9. Complexity summary

| Problem | Time | Space | Notes |
|---------|------|-------|-------|
| Basic Binary Search | O(log n) | O(1) | |
| Upper Bound / Ceiling | O(log n) | O(1) | |
| First and Last Position | O(log n) | O(1) | two binary searches |
| Count Occurrences | O(log n) | O(1) | last − first + 1 |
| Infinite Sorted Array | O(log n) | O(1) | exponential window + binary search |
| Peak Index in Mountain | O(log n) | O(1) | |
| Find Peak Element | O(log n) | O(1) | any local peak |
| Find Min in Rotated | O(log n) | O(1) | |
| Count Rotations | O(log n) | O(1) | same as find min |
| Search in Rotated | O(log n) | O(1) | |
| Koko Eating Bananas | O(n log m) | O(1) | m = max pile |
| Min Days for Bouquets | O(n log m) | O(1) | m = max bloomDay |
| Aggressive Cows | O(n log n + n log d) | O(1) | d = max distance |
| H-Index II | O(log n) | O(1) | |
| Max Candies | O(n log m) | O(1) | m = max pile |
| Ship in D Days | O(n log s) | O(1) | s = total weight |
| Book Allocation | O(n log s) | O(1) | s = total pages |
| Split Array | O(n log s) | O(1) | s = total sum |
| Search 2D Matrix | O(log mn) | O(1) | treated as 1D |
| Search 2D Matrix II | O(m + n) | O(1) | staircase, not binary search |
| Kth Smallest in Matrix | O(n log(max−min)) | O(1) | |
| Kth in Multiplication Table | O(m log mn) | O(1) | |
| Median of Two Sorted Arrays | O(log(min(m,n))) | O(1) | binary search on shorter array |

**General rules:**
- Pure binary search on array index → **O(log n)**
- Binary search on answer with O(n) feasibility check → **O(n log(answer_range))**
- 2D matrix binary search → **O(log(m×n))** if row-first sorted, **O(m+n)** if independently sorted
- Always **O(1) space** — no extra data structure needed

---

*Binary Search is the most underestimated pattern in interviews.*
*The key shift: stop thinking "search in array" and start thinking "eliminate half the search space."*
*Once you see binary search on answer, 60% of Hard problems become Medium.*
