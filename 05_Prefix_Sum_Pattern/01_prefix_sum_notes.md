# Prefix Sum Pattern — Complete Notes

> **Pattern family:** Array / Subarray / Range Query  
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
| "subarray sum equals k" | prefix sum + HashMap lookup |
| "number of subarrays with sum / count" | prefix sum + frequency map |
| "find pivot index / equilibrium index" | left sum == right sum |
| "subarray sum divisible by k" | prefix sum + modulo + HashMap |
| "contiguous subarray with equal 0s and 1s" | remap 0→-1, prefix sum |
| "range sum query" | precompute prefix array, O(1) query |
| "2D matrix sum query" | 2D prefix sum |
| "shortest subarray with sum ≥ k" | prefix sum + monotonic deque |
| "count range sum" | prefix sum + merge sort / BIT |
| "max sum rectangle no larger than k" | 2D prefix + sorted set |
| "running total / cumulative sum" | prefix sum array |

### Brute force test

```
Brute force: two nested loops — for every (i, j) pair compute sum(i..j) from scratch.
→ O(n²) or O(n³) time — too slow for large inputs.
→ Interviewer says "O(n)" or "O(n log n)" → cannot recompute sum every time.
→ Use Prefix Sum: precompute once in O(n), answer any range query in O(1).
```

### The 5 confirming signals

**Signal 1 — "Subarray sum equals / divisible by / at least K"**
> Any problem asking about a property of a subarray SUM (not max/min element)
> is a prefix sum problem. The key identity: `sum(i..j) = prefix[j+1] - prefix[i]`.

**Signal 2 — "Count of subarrays" with some sum condition**
> When you need to COUNT how many subarrays satisfy a sum condition,
> store prefix sums in a HashMap. Each lookup is O(1).

**Signal 3 — "Pivot / equilibrium index"**
> Left sum == right sum → prefix sum from left and right simultaneously,
> or use total sum minus left prefix.

**Signal 4 — "Equal count of two elements" (0s and 1s, X and Y)**
> Remap one element to -1. Now "equal count" = "subarray sum = 0".
> This converts the problem to subarray sum = 0 → prefix sum + HashMap.

**Signal 5 — "Range sum query" (multiple queries on same array)**
> If the array is static and you have many queries, precompute prefix array.
> Each query `sum(l, r)` = `prefix[r+1] - prefix[l]` in O(1).

### Decision flowchart

```
Problem involves subarray / range SUM?
        │
        ▼
Single query or multiple queries?
        │
        ├── MULTIPLE QUERIES (static array) → Prefix array, O(1) per query
        │
        ├── COUNT subarrays with sum = k? → prefix + HashMap {sum → count}
        │
        ├── COUNT subarrays with sum % k = 0? → prefix + modulo + HashMap
        │
        ├── EQUAL count of two values? → remap to ±1, sum = 0 → HashMap
        │
        ├── PIVOT / EQUILIBRIUM index? → leftSum == totalSum - leftSum - nums[i]
        │
        ├── SHORTEST subarray with sum ≥ k? → prefix + monotonic deque (HARD)
        │
        ├── COUNT range sums in [lo, hi]? → prefix + merge sort / BIT (HARD)
        │
        └── MAX sum rectangle ≤ k? → 2D prefix + sorted set (HARD)
```

---

## 2. What is this pattern?

Build a `prefix[]` array where `prefix[i]` = sum of `nums[0..i-1]`.

```java
int[] prefix = new int[n + 1];   // prefix[0] = 0
for (int i = 0; i < n; i++)
    prefix[i + 1] = prefix[i] + nums[i];
```

**Core identity:**
```
sum(i, j)  =  prefix[j+1] - prefix[i]
              (sum from index i to j inclusive)
```

**Why it works:**
```
nums    =  [3,  1,  4,  1,  5]
prefix  =  [0,  3,  4,  8,  9, 14]

sum(1, 3) = prefix[4] - prefix[1] = 9 - 3 = 6  ✓  (1+4+1)
sum(0, 4) = prefix[5] - prefix[0] = 14 - 0 = 14 ✓  (3+1+4+1+5)
```

**The HashMap extension (for counting):**
Instead of finding a specific range, we ask:
> "How many previous prefix sums equal `currentSum - k`?"

If `prefix[j] - prefix[i] = k`, then subarray `(i, j]` has sum `k`.
Store every prefix sum in a HashMap as you go → each lookup is O(1).

```java
Map<Integer, Integer> map = new HashMap<>();
map.put(0, 1);   // empty prefix has sum 0 — count = 1
int sum = 0, count = 0;

for (int num : nums) {
    sum += num;
    count += map.getOrDefault(sum - k, 0);   // how many prefixes equal sum-k?
    map.put(sum, map.getOrDefault(sum, 0) + 1);
}
```

---

## 3. Core rules

**Rule 1 — Always initialise `map.put(0, 1)` before the loop**
```java
// WRONG — misses subarrays starting from index 0
Map<Integer, Integer> map = new HashMap<>();
// map is empty — if sum == k on first element, count += map.get(0) = null → NPE or 0

// CORRECT — seed the map with sum=0 having count=1
Map<Integer, Integer> map = new HashMap<>();
map.put(0, 1);   // represents the empty prefix before index 0
```
This handles the case where a subarray starting from index `0` sums to exactly `k`.

**Rule 2 — For modulo problems, handle negative remainders in Java**
```java
// WRONG — Java % can return negative for negative sums
int rem = sum % k;

// CORRECT — always normalise to positive remainder
int rem = ((sum % k) + k) % k;
```
Java's `%` operator returns a result with the sign of the dividend.
`-7 % 3 = -1` in Java, but we want `2`. The `+k) % k` trick fixes this.

**Rule 3 — For "equal 0s and 1s" problems, remap 0 → -1 first**
```java
// Remap before building prefix sum
for (int i = 0; i < nums.length; i++)
    if (nums[i] == 0) nums[i] = -1;

// Now "equal 0s and 1s" = "subarray sum = 0"
// Apply standard prefix + HashMap with target k = 0
```
After remapping, any subarray with sum = 0 has equal counts of +1 and -1
(original 1s and 0s). This converts the problem to a standard prefix sum lookup.

---

## 4. 2-Question framework

### Question 1 — What are you computing over the subarray?

| Answer | Variant |
|--------|---------|
| Fixed sum `k` — does it exist? | Prefix + HashMap (existence check) |
| Fixed sum `k` — count subarrays | Prefix + HashMap (frequency count) |
| Sum divisible by `k` | Prefix + modulo + HashMap |
| Equal count of two values | Remap to ±1, sum = 0, HashMap |
| Range query on static array | Precompute prefix array |
| Shortest subarray with sum ≥ k | Prefix + monotonic deque |
| Count sums in range [lo, hi] | Prefix + merge sort / Fenwick tree |
| Max rectangle sum ≤ k | 2D prefix + sorted set |

### Question 2 — Is the array 1D or 2D?

| Dimension | Approach |
|-----------|----------|
| **1D** | `prefix[i+1] = prefix[i] + nums[i]` |
| **2D** | `prefix[i][j] = nums[i][j] + prefix[i-1][j] + prefix[i][j-1] - prefix[i-1][j-1]` |

```java
// 2D prefix sum — rectangle sum query
int rectSum = prefix[r2+1][c2+1]
            - prefix[r1][c2+1]
            - prefix[r2+1][c1]
            + prefix[r1][c1];
```

> **Decision shortcut:**
> - "count subarrays with sum = k" → HashMap, seed with `{0:1}`
> - "sum divisible by k" → modulo map, `((sum%k)+k)%k`
> - "equal 0s and 1s" → remap 0→-1, then sum=0
> - "pivot index" → `leftSum == total - leftSum - nums[i]`
> - "shortest with sum ≥ k" → deque (prefix values must be negative allowed)
> - "range query, many queries" → prefix array

---

## 5. Variants table

> **Common core:** `prefix[i] = prefix[i-1] + nums[i-1]`  
> **What differs:** what you store in HashMap, what you look up

| Variant | HashMap key | HashMap value | Lookup target |
|---------|-------------|---------------|---------------|
| Count subarrays sum=k | prefix sum | frequency | `sum - k` |
| Sum divisible by k | `sum % k` (normalised) | frequency | same remainder |
| Equal 0s and 1s | prefix sum (after remap) | first index seen | same sum (longest) |
| Pivot index | — (no map) | — | `2 * leftSum + nums[i] == total` |
| Shortest sum ≥ k | — (deque) | — | deque front |
| Count range sum | prefix sum | sorted list | binary search in [lo,hi] |

---

## 6. Universal Java template

```java
// ─── TEMPLATE A: Prefix Array (Range Sum Query) ───────────────────────────────
int[] prefix = new int[n + 1];
for (int i = 0; i < n; i++)
    prefix[i + 1] = prefix[i] + nums[i];

// Query sum(l, r) inclusive:
int rangeSum = prefix[r + 1] - prefix[l];


// ─── TEMPLATE B: Count Subarrays with Sum = k (HashMap) ──────────────────────
public int subarraySum(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, 1);          // ← ALWAYS seed this first
    int sum = 0, count = 0;

    for (int num : nums) {
        sum += num;
        count += map.getOrDefault(sum - k, 0);   // subarrays ending here with sum=k
        map.merge(sum, 1, Integer::sum);          // increment frequency of sum
    }
    return count;
}


// ─── TEMPLATE C: Sum Divisible by k (Modulo HashMap) ─────────────────────────
public int subarraysDivByK(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, 1);
    int sum = 0, count = 0;

    for (int num : nums) {
        sum += num;
        int rem = ((sum % k) + k) % k;   // ← normalise negative remainder
        count += map.getOrDefault(rem, 0);
        map.merge(rem, 1, Integer::sum);
    }
    return count;
}


// ─── TEMPLATE D: Equal 0s and 1s (Remap + First-seen index) ──────────────────
public int findMaxLength(int[] nums) {
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, -1);         // ← seed with index -1 (before array starts)
    int sum = 0, maxLen = 0;

    for (int i = 0; i < nums.length; i++) {
        sum += (nums[i] == 0) ? -1 : 1;   // remap 0→-1
        if (map.containsKey(sum)) {
            maxLen = Math.max(maxLen, i - map.get(sum));
        } else {
            map.put(sum, i);   // store FIRST occurrence only (for max length)
        }
    }
    return maxLen;
}


// ─── TEMPLATE E: Pivot Index ─────────────────────────────────────────────────
public int pivotIndex(int[] nums) {
    int total = 0;
    for (int n : nums) total += n;

    int leftSum = 0;
    for (int i = 0; i < nums.length; i++) {
        // leftSum == rightSum  →  leftSum == total - leftSum - nums[i]
        if (2 * leftSum + nums[i] == total) return i;
        leftSum += nums[i];
    }
    return -1;
}


// ─── TEMPLATE F: Shortest Subarray with Sum ≥ k (Deque) ──────────────────────
public int shortestSubarray(int[] nums, int k) {
    int n = nums.length;
    long[] prefix = new long[n + 1];
    for (int i = 0; i < n; i++) prefix[i + 1] = prefix[i] + nums[i];

    int res = Integer.MAX_VALUE;
    Deque<Integer> deque = new ArrayDeque<>();   // stores indices, monotone increasing prefix

    for (int i = 0; i <= n; i++) {
        // Remove from front: if prefix[i] - prefix[front] >= k → valid, try to shrink
        while (!deque.isEmpty() && prefix[i] - prefix[deque.peekFirst()] >= k) {
            res = Math.min(res, i - deque.pollFirst());
        }
        // Remove from back: maintain increasing order of prefix values
        while (!deque.isEmpty() && prefix[i] <= prefix[deque.peekLast()]) {
            deque.pollLast();
        }
        deque.addLast(i);
    }
    return res == Integer.MAX_VALUE ? -1 : res;
}


// ─── TEMPLATE G: 2D Prefix Sum ────────────────────────────────────────────────
int[][] prefix2D = new int[m + 1][n + 1];
for (int i = 1; i <= m; i++)
    for (int j = 1; j <= n; j++)
        prefix2D[i][j] = mat[i-1][j-1]
                       + prefix2D[i-1][j]
                       + prefix2D[i][j-1]
                       - prefix2D[i-1][j-1];

// Rectangle sum (r1,c1) to (r2,c2) inclusive:
int rectSum = prefix2D[r2+1][c2+1]
            - prefix2D[r1][c2+1]
            - prefix2D[r2+1][c1]
            + prefix2D[r1][c1];
```

---

## 7. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                            → VARIANT                → KEY CODE
─────────────────────────────────────────────────────────────────────────────────────────
"subarray sum equals k"                      → HashMap count          → map.put(0,1); count += map.get(sum-k)
"sum divisible by k"                         → Modulo HashMap         → rem = ((sum%k)+k)%k
"equal 0s and 1s / equal X and Y"           → Remap + HashMap        → 0→-1, find sum=0
"pivot / equilibrium index"                 → Left/right total       → 2*leftSum + nums[i] == total
"range sum query (multiple)"                → Prefix array           → prefix[r+1] - prefix[l]
"shortest subarray sum ≥ k"                 → Prefix + deque         → monotone deque on prefix array
"count range sums in [lo,hi]"               → Prefix + merge sort    → count inversions in prefix array
"max rectangle sum ≤ k"                     → 2D prefix + TreeSet    → fix rows, binary search in set
"2D rectangle sum query"                    → 2D prefix array        → inclusion-exclusion formula
```

**The rules — burn these into memory:**
```java
// ALWAYS seed the map before the loop
map.put(0, 1);

// ALWAYS normalise modulo for negative sums
int rem = ((sum % k) + k) % k;

// ALWAYS remap 0 → -1 for "equal count" problems
sum += (nums[i] == 0) ? -1 : 1;

// Range sum identity
sum(l, r) = prefix[r+1] - prefix[l]

// Pivot condition (no HashMap needed)
2 * leftSum + nums[i] == total
```

---

## 8. Common mistakes

### Mistake 1 — Forgetting to seed `map.put(0, 1)`

```java
// BUG — misses subarrays that start from index 0
Map<Integer, Integer> map = new HashMap<>();
// If nums = [3], k = 3: sum=3, look for 3-3=0 → not in map → count=0 (WRONG, answer is 1)

// FIX — always seed before the loop
map.put(0, 1);
// Now sum=3, look for 0 → found with count 1 → count=1 ✓
```

### Mistake 2 — Negative modulo in Java

```java
// BUG — Java % keeps the sign of the dividend
int sum = -7, k = 3;
int rem = sum % k;   // rem = -1 (WRONG — we want 2, since -7 = (-3)*3 + 2)

// FIX — normalise to positive
int rem = ((sum % k) + k) % k;   // (-1 + 3) % 3 = 2 ✓
```

### Mistake 3 — Using last index instead of first index for "longest" variant

```java
// BUG — overwriting the first occurrence loses the longest subarray
map.put(sum, i);   // always update → shortest subarray, not longest

// FIX — only store first occurrence
if (!map.containsKey(sum)) map.put(sum, i);   // keep earliest index → longest subarray ✓
```

### Mistake 4 — Off-by-one in prefix array indexing

```java
// BUG — prefix array of size n (should be n+1)
int[] prefix = new int[n];
prefix[0] = nums[0];
// sum(0, j) = prefix[j] — inconsistent, easy to get wrong bounds

// FIX — size n+1, prefix[0] = 0 always
int[] prefix = new int[n + 1];   // prefix[0] = 0 (implicit)
for (int i = 0; i < n; i++) prefix[i + 1] = prefix[i] + nums[i];
// sum(l, r) = prefix[r+1] - prefix[l]  — clean and consistent
```

### Mistake 5 — Using Sliding Window instead of Prefix Sum when negatives exist

```java
// BUG — sliding window only works for non-negative arrays
// For "shortest subarray with sum ≥ k" with negatives present:
// shrinking the window doesn't guarantee sum decreases → wrong answer

// FIX — use prefix sum + monotonic deque
// Deque handles negative numbers correctly because it doesn't assume monotone sums
```

### Mistake 6 — Wrong 2D prefix formula (forgetting to add back the overlap)

```java
// BUG — double-subtracts the top-left corner
prefix[i][j] = nums[i-1][j-1] + prefix[i-1][j] + prefix[i][j-1];
// (i-1,j) and (i,j-1) both include (i-1,j-1) → subtracted twice

// FIX — add back the overlap
prefix[i][j] = nums[i-1][j-1]
             + prefix[i-1][j]
             + prefix[i][j-1]
             - prefix[i-1][j-1];   // ← add back once
```

---

## 9. Complexity summary

| Problem | Time | Space | Notes |
|---------|------|-------|-------|
| Range Sum Query (static) | O(n) build, O(1) query | O(n) | precompute once, answer many |
| Subarray Sum Equals K | O(n) | O(n) | single pass + HashMap |
| Find Pivot Index | O(n) | O(1) | total sum − left prefix, no map needed |
| Subarray Sums Divisible by K | O(n) | O(k) | modulo map has at most k distinct keys |
| Contiguous Array (equal 0s/1s) | O(n) | O(n) | remap + first-seen HashMap |
| Shortest Subarray Sum ≥ K | O(n) | O(n) | prefix + monotonic deque |
| Count Range Sum | O(n log n) | O(n) | prefix + merge sort or BIT |
| Max Sum Rectangle ≤ K | O(m² · n log n) | O(n) | fix row pair, 1D problem per pair |

**General rules:**
- Prefix sum array build is always **O(n)** time, **O(n)** space.
- HashMap-based variants are **O(n)** time, **O(n)** space — one pass.
- Hard variants (deque, merge sort, BIT) are **O(n log n)** time.
- 2D variants multiply by the extra dimension: O(m·n) build, O(1) query.
- When array has **only non-negatives** and you need min/max subarray → consider sliding window first (O(1) space). Use prefix sum when negatives are present or you need counts.

---

*Prefix Sum is one of the most quietly powerful patterns in DSA.*
*Master the HashMap extension — it converts O(n²) brute force into O(n) elegantly.*
