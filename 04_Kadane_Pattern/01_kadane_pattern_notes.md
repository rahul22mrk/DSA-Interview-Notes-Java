# Kadane's Algorithm — Notes & Templates

> **Pattern family:** Dynamic Programming / Array Optimization
> **Difficulty range:** Easy → Hard
> **Language:** Java
> **Problems file:** [02_kadane_pattern_problems.md](./02_kadane_pattern_problems.md)

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
| "maximum subarray sum" | classic Kadane |
| "minimum subarray sum" | Kadane with negation |
| "maximum product subarray" | Kadane tracking both max and min |
| "contiguous subarray" + "maximum / minimum" | Kadane candidate |
| "circular array" + "max subarray" | total sum − min subarray |
| "best time to buy and sell stock" | Kadane on price differences |
| "maximum sum after one deletion" | Kadane with DP state |
| "house robber / non-adjacent" | Kadane-style DP |
| "maximum sum rectangle in matrix" | 2D Kadane |
| "max sum submatrix ≤ k" | 2D Kadane + binary search |
| "maximum alternating subarray sum" | Kadane with sign flip |

### Brute force test

```
Brute force: check every subarray → O(n²) or O(n³)
→ If you want max/min of a contiguous subarray SUM or PRODUCT
  AND the problem has "optimal substructure" (best ending here depends only on best ending at i-1)
→ Kadane = O(n)

Key insight: at each position i, you have exactly 2 choices:
  1. Extend the previous subarray: currentSum + arr[i]
  2. Start fresh from here:        arr[i]
Take the max of the two. That's Kadane.
```

### The 5 confirming signals

**Signal 1 — "Maximum / minimum sum of contiguous subarray"**
> This is the textbook Kadane problem. Direct application.

**Signal 2 — "At each step, extend or restart"**
> If adding the current element to the previous result could make it worse, you should restart. This is the Kadane decision at every step.

**Signal 3 — "Circular array variant"**
> Two cases: max subarray doesn't wrap (normal Kadane) OR it wraps (total − min subarray). Take the max of both.

**Signal 4 — "Buy/sell stock" or "profit/loss sequence"**
> Convert prices to daily differences: `diff[i] = price[i] - price[i-1]`. Then max subarray sum on `diff` = max profit. Kadane in disguise.

**Signal 5 — "Matrix / 2D" + "max sum rectangle"**
> Fix left and right column boundaries, reduce each row to a 1D array by summing column-wise, run Kadane on that 1D array.

### Decision flowchart

```
Problem involves contiguous subarray/substring?
        │
        ├── YES → Is it sum-based?
        │              ├── Max sum          → Classic Kadane (Template A)
        │              ├── Min sum          → Kadane with min (Template A, track min)
        │              ├── Max sum circular → Kadane + (total − min subarray) (Template C)
        │              ├── Max sum + 1 del  → Kadane with forward/backward prefix (Template D)
        │              └── Max product      → Kadane tracking both max and min (Template B)
        │
        ├── YES → Is it 2D (matrix)?
        │              └── Max sum rectangle → fix columns, reduce to 1D, run Kadane (Template E)
        │
        ├── YES → Is it a sequence with choices (rob/skip)?
        │              └── House Robber style → Kadane-style DP (Template F)
        │
        └── NO → Not Kadane
```

---

## 2. What is this pattern?

Kadane's algorithm answers: **"What is the maximum sum subarray ending at position i?"**

At every index, you make one decision:
```
maxEndingHere = max(arr[i], maxEndingHere + arr[i])
```

Either **start fresh** at `arr[i]`, or **extend** the previous best subarray.

**Why it works — optimal substructure:**
The best subarray ending at `i` either:
- Starts at `i` (start fresh when previous sum is negative)
- Extends the best subarray ending at `i-1`

This means you only need to remember **one value** from the previous step → O(n) time, O(1) space.

```
arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]

maxEndingHere: -2 → 1 → -2 → 4 → 3 → 5 → 6 → 1 → 5
maxSoFar:      -2    1    1    4    4    5    6    6    6

Answer: 6  (subarray [4,-1,2,1])
```

**The core insight — negative prefix kills you:**
If `maxEndingHere < 0`, adding more elements can only decrease future sums. So restart from the next element.

---

## 3. Core rules

**Rule 1 — Kadane makes exactly one decision per element**
```java
// At each index, choose: restart OR extend
maxEndingHere = Math.max(arr[i], maxEndingHere + arr[i]);
maxSoFar = Math.max(maxSoFar, maxEndingHere);

// Alternative equivalent form:
if (maxEndingHere < 0) maxEndingHere = 0;  // restart implicitly
maxEndingHere += arr[i];
maxSoFar = Math.max(maxSoFar, maxEndingHere);
```

Both forms are correct. The first is more explicit (handles all-negative arrays correctly).

**Rule 2 — All-negative array: answer is the least negative element**
```java
// WRONG — returns 0 for all-negative arrays (empty subarray)
int maxSum = 0;
for (int n : arr) {
    maxSum = Math.max(maxSum, maxSum + n);  // never goes below 0
}
// For [-3,-1,-2], returns 0 — but problem usually asks for subarray (non-empty)

// CORRECT — initialise maxSoFar to first element
int maxEndingHere = arr[0], maxSoFar = arr[0];
for (int i = 1; i < arr.length; i++) {
    maxEndingHere = Math.max(arr[i], maxEndingHere + arr[i]);
    maxSoFar = Math.max(maxSoFar, maxEndingHere);
}
```

**Rule 3 — For product subarrays, track both max AND min**
```java
// Products: negative × negative = positive
// So the minimum so far can become the maximum when multiplied by a negative number
int maxProd = arr[0], minProd = arr[0], result = arr[0];
for (int i = 1; i < arr.length; i++) {
    if (arr[i] < 0) {
        int temp = maxProd;
        maxProd = minProd;
        minProd = temp;   // swap: multiplying by negative flips max/min
    }
    maxProd = Math.max(arr[i], maxProd * arr[i]);
    minProd = Math.min(arr[i], minProd * arr[i]);
    result = Math.max(result, maxProd);
}
```

---

## 4. 2-Question framework

### Question 1 — What are you optimising?

| Optimise | Approach |
|----------|----------|
| Maximum sum | Classic Kadane — track `maxEndingHere` |
| Minimum sum | Kadane with `min` instead of `max` |
| Maximum product | Kadane tracking both `maxProd` and `minProd` |
| Maximum sum circular | max(Kadane, total − minKadane) |
| Maximum sum with 1 deletion | Forward + backward prefix arrays |
| Maximum sum 2D rectangle | Fix columns + 1D Kadane |

### Question 2 — Are there constraints or modifications?

| Constraint | Modification |
|-----------|-------------|
| Array is circular | Use `total − minSubarray` for wrapping case |
| Can delete exactly one element | Precompute forward and backward Kadane arrays |
| Non-adjacent elements (House Robber) | `dp[i] = max(dp[i-1], dp[i-2] + arr[i])` |
| 2D matrix | Fix left/right column boundary, column-compress to 1D, run Kadane |
| Sum ≤ k constraint | 2D Kadane + sorted set binary search |

> **Decision shortcut:**
> - "max/min subarray sum" → classic Kadane
> - "max product" → track both max and min products
> - "circular" → total sum − min subarray
> - "one deletion allowed" → forward + backward prefix Kadane
> - "2D matrix" → column compression + 1D Kadane
> - "non-adjacent" → house robber DP

---

## 5. Variants table

> **Common core:** at each step, decide to extend or restart  
> **What differs:** what you track and the restart condition

| Variant | Track | Restart condition | Special logic |
|---------|-------|------------------|---------------|
| Max sum | `maxEndingHere` | previous sum < 0 | none |
| Min sum | `minEndingHere` | previous sum > 0 | negate or use min |
| Max product | `maxProd`, `minProd` | zero resets both | swap on negative |
| Circular max sum | both max and min | — | `total − minSubarray` |
| Max sum with 1 deletion | `forward[]`, `backward[]` | — | `forward[i-1] + backward[i+1]` |
| Max alternating sum | `maxEnd`, `minEnd` | — | toggle sign each step |
| House Robber | `dp[i-1]`, `dp[i-2]` | — | non-adjacent constraint |
| 2D max rectangle | 1D Kadane per column pair | — | O(n²m) overall |

---

## 5b. Pattern categories — all types covered

### Category 1 — Classic Kadane (Sum)
> Single decision at each step: extend or restart.

```java
int cur = arr[0], best = arr[0];
for (int i = 1; i < n; i++) {
    cur = Math.max(arr[i], cur + arr[i]);
    best = Math.max(best, cur);
}
```
**Problems:** Maximum Subarray Sum, Minimum Subarray Sum, Longest Positive Sum Subarray

---

### Category 2 — Product Kadane
> Multiplying by negative flips max to min. Track both.

```java
int maxP = arr[0], minP = arr[0], best = arr[0];
for (int i = 1; i < n; i++) {
    if (arr[i] < 0) { int t = maxP; maxP = minP; minP = t; }
    maxP = Math.max(arr[i], maxP * arr[i]);
    minP = Math.min(arr[i], minP * arr[i]);
    best = Math.max(best, maxP);
}
```
**Problems:** Maximum Product Subarray, Maximum Absolute Sum

---

### Category 3 — Circular Kadane
> Two cases: subarray doesn't wrap (normal Kadane) OR wraps (use total − min).

```java
int maxKadane = kadane_max(arr);
int minKadane = kadane_min(arr);
int total = sum(arr);
// If all negative: minKadane == total → circular result would be 0 (empty) → use maxKadane
int circularMax = (total == minKadane) ? maxKadane : Math.max(maxKadane, total - minKadane);
```
**Problems:** Maximum Sum Circular Subarray

---

### Category 4 — Kadane with State (DP)
> More than one state tracked per position.

```java
// One deletion: precompute forward and backward
int[] fwd = new int[n];  // max subarray sum ending AT i
int[] bwd = new int[n];  // max subarray sum starting FROM i

// Answer for deleting index i: fwd[i-1] + bwd[i+1]
```
**Problems:** Maximum Subarray Sum with One Deletion, House Robber

---

### Category 5 — 2D Kadane
> Fix left and right column boundaries. Sum each row between those columns.
> Run 1D Kadane on the resulting column-sum array.

```java
for (int left = 0; left < cols; left++) {
    int[] rowSum = new int[rows];
    for (int right = left; right < cols; right++) {
        for (int r = 0; r < rows; r++) rowSum[r] += matrix[r][right];
        maxSumSoFar = Math.max(maxSumSoFar, kadane(rowSum));
    }
}
```
**Problems:** Maximum Sum Rectangle in 2D Matrix, Max Sum Submatrix ≤ K

---

### Summary — all 5 categories

| # | Category | Core idea | Time |
|---|----------|-----------|------|
| 1 | Classic (sum) | extend or restart | O(n) |
| 2 | Product | track max AND min | O(n) |
| 3 | Circular | total − minKadane | O(n) |
| 4 | With state / DP | forward + backward arrays | O(n) |
| 5 | 2D matrix | column compression + 1D Kadane | O(n²m) |

---

## 6. Universal Java template

```java
// ─── TEMPLATE A: Classic Kadane — Max Subarray Sum ───────────────────────────
public int maxSubarraySum(int[] arr) {
    int maxEndingHere = arr[0];  // best subarray sum ENDING at current index
    int maxSoFar = arr[0];       // global best answer

    for (int i = 1; i < arr.length; i++) {
        maxEndingHere = Math.max(arr[i], maxEndingHere + arr[i]);
        maxSoFar = Math.max(maxSoFar, maxEndingHere);
    }
    return maxSoFar;
}

// ─── TEMPLATE A2: Classic Kadane — Min Subarray Sum ──────────────────────────
public int minSubarraySum(int[] arr) {
    int minEndingHere = arr[0];
    int minSoFar = arr[0];

    for (int i = 1; i < arr.length; i++) {
        minEndingHere = Math.min(arr[i], minEndingHere + arr[i]);
        minSoFar = Math.min(minSoFar, minEndingHere);
    }
    return minSoFar;
}

// ─── TEMPLATE A3: Kadane with subarray indices (track start/end) ──────────────
public int[] maxSubarrayWithIndices(int[] arr) {
    int maxEndingHere = arr[0], maxSoFar = arr[0];
    int start = 0, end = 0, tempStart = 0;

    for (int i = 1; i < arr.length; i++) {
        if (arr[i] > maxEndingHere + arr[i]) {
            maxEndingHere = arr[i];
            tempStart = i;                       // potential new start
        } else {
            maxEndingHere += arr[i];
        }
        if (maxEndingHere > maxSoFar) {
            maxSoFar = maxEndingHere;
            start = tempStart;
            end = i;
        }
    }
    return new int[]{maxSoFar, start, end};
}

// ─── TEMPLATE B: Product Kadane ───────────────────────────────────────────────
public int maxProductSubarray(int[] arr) {
    int maxProd = arr[0], minProd = arr[0], result = arr[0];

    for (int i = 1; i < arr.length; i++) {
        if (arr[i] < 0) {
            int temp = maxProd;      // swap: negative flips max ↔ min
            maxProd = minProd;
            minProd = temp;
        }
        maxProd = Math.max(arr[i], maxProd * arr[i]);  // extend or restart
        minProd = Math.min(arr[i], minProd * arr[i]);
        result = Math.max(result, maxProd);
    }
    return result;
}

// ─── TEMPLATE C: Circular Kadane ─────────────────────────────────────────────
public int maxCircularSubarraySum(int[] arr) {
    int maxKadane = kadaneMax(arr);
    int minKadane = kadaneMin(arr);
    int total = 0;
    for (int n : arr) total += n;

    // If all negative: total == minKadane → wrapping gives 0 (empty subarray) → invalid
    return (total == minKadane) ? maxKadane : Math.max(maxKadane, total - minKadane);
}

// ─── TEMPLATE D: Kadane with Forward/Backward arrays (one deletion) ───────────
public int maxSumAfterOneDeletion(int[] arr) {
    int n = arr.length;
    int[] fwd = new int[n];   // fwd[i] = max subarray sum ENDING at i
    int[] bwd = new int[n];   // bwd[i] = max subarray sum STARTING at i

    fwd[0] = arr[0];
    for (int i = 1; i < n; i++)
        fwd[i] = Math.max(arr[i], fwd[i-1] + arr[i]);

    bwd[n-1] = arr[n-1];
    for (int i = n-2; i >= 0; i--)
        bwd[i] = Math.max(arr[i], bwd[i+1] + arr[i]);

    int result = Arrays.stream(arr).max().getAsInt();  // single element (delete everything else)
    for (int i = 1; i < n-1; i++)
        result = Math.max(result, fwd[i-1] + bwd[i+1]);  // delete index i

    return result;
}

// ─── TEMPLATE E: 2D Kadane — Maximum Sum Rectangle ───────────────────────────
public int maxSumRectangle(int[][] matrix) {
    int rows = matrix.length, cols = matrix[0].length;
    int maxSum = Integer.MIN_VALUE;

    for (int left = 0; left < cols; left++) {
        int[] rowSum = new int[rows];            // compressed row sums

        for (int right = left; right < cols; right++) {
            for (int r = 0; r < rows; r++)
                rowSum[r] += matrix[r][right];   // add column `right` to compression

            maxSum = Math.max(maxSum, kadaneMax(rowSum));  // 1D Kadane on compressed array
        }
    }
    return maxSum;
}

// ─── TEMPLATE F: House Robber (Kadane-style DP, non-adjacent) ─────────────────
public int houseRobber(int[] nums) {
    if (nums.length == 1) return nums[0];
    int prev2 = nums[0];
    int prev1 = Math.max(nums[0], nums[1]);

    for (int i = 2; i < nums.length; i++) {
        int curr = Math.max(prev1, prev2 + nums[i]);
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```

---

## 7. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                         → VARIANT              → KEY OPERATION
────────────────────────────────────────────────────────────────────────────────────
"maximum subarray sum"                    → Classic Kadane       → max(arr[i], cur + arr[i])
"minimum subarray sum"                    → Min Kadane           → min(arr[i], cur + arr[i])
"maximum product subarray"                → Product Kadane       → track maxProd + minProd, swap on negative
"maximum sum circular subarray"           → Circular Kadane      → max(maxKadane, total - minKadane)
"max sum with one deletion"               → Forward + Backward   → fwd[i-1] + bwd[i+1]
"maximum sum rectangle in matrix"         → 2D Kadane            → fix columns, compress rows, 1D Kadane
"best time to buy sell stock"             → Kadane on diff array → profit[i] = price[i] - price[i-1]
"house robber / non-adjacent"             → DP Kadane            → max(prev1, prev2 + curr)
"maximum alternating subarray sum"        → Alternating Kadane   → toggle +/- each step
"max absolute sum of any subarray"        → Kadane dual          → max(maxKadane, -minKadane)
```

**The one decision Kadane makes at every step:**
```java
cur = Math.max(arr[i], cur + arr[i]);
//             ^restart   ^extend
// Restart when prev sum is negative (it only hurts us)
```

**Key formulas:**
```
Max sum            = Kadane(arr)
Min sum            = -Kadane(-arr)  OR  Kadane_min(arr)
Circular max       = max(Kadane_max, total - Kadane_min)
Max absolute sum   = max(Kadane_max, abs(Kadane_min))
Max profit (stock) = Kadane(diff[]) where diff[i] = price[i] - price[i-1]
```

---

## 8. Common mistakes

### Mistake 1 — Initialising maxSoFar to 0 (breaks all-negative arrays)

```java
// BUG — returns 0 for [-3,-1,-2] but answer is -1
int maxSum = 0;
for (int n : arr) maxSum = Math.max(maxSum, maxSum + n);

// FIX — initialise to arr[0], start loop from index 1
int cur = arr[0], best = arr[0];
for (int i = 1; i < arr.length; i++) {
    cur = Math.max(arr[i], cur + arr[i]);
    best = Math.max(best, cur);
}
```

### Mistake 2 — Not handling zero in product Kadane

```java
// BUG — zero in array: maxProd should reset, but swap logic breaks
// CORRECT: Math.max(arr[i], maxProd * arr[i]) handles zero because:
// if arr[i] == 0: max(0, anything*0=0) = 0 → correctly resets
// No special case needed for zero.
```

### Mistake 3 — Circular Kadane edge case (all negative)

```java
// BUG — if all elements negative, total == minKadane
// total - minKadane = 0 → but empty subarray is not valid
int circular = total - minKadane;
return Math.max(maxKadane, circular);  // WRONG for all-negative

// FIX — check if entire array is selected as minimum
if (total == minKadane) return maxKadane;  // all negative: can't wrap
return Math.max(maxKadane, total - minKadane);
```

### Mistake 4 — Not swapping in product Kadane before updating

```java
// BUG — swap AFTER update causes wrong result
maxProd = Math.max(arr[i], maxProd * arr[i]);
minProd = Math.min(arr[i], minProd * arr[i]);
if (arr[i] < 0) { int t = maxProd; maxProd = minProd; minProd = t; }  // WRONG: too late

// FIX — swap BEFORE computing new max/min
if (arr[i] < 0) { int t = maxProd; maxProd = minProd; minProd = t; }
maxProd = Math.max(arr[i], maxProd * arr[i]);
minProd = Math.min(arr[i], minProd * arr[i]);
```

### Mistake 5 — Wrong edge case in one-deletion Kadane

```java
// BUG — deleting first or last element not handled
for (int i = 1; i < n-1; i++)
    result = Math.max(result, fwd[i-1] + bwd[i+1]);
// Deleting index 0 → answer = sum of arr[1..n-1] starting fresh
// Deleting index n-1 → answer = fwd[n-2]

// FIX — also consider:
result = Math.max(result, bwd[1]);     // delete index 0
result = Math.max(result, fwd[n-2]);   // delete index n-1
```

### Mistake 6 — House Robber wrong initialisation for 2 elements

```java
// BUG
int prev2 = nums[0], prev1 = nums[1];  // if n=2, skips max(nums[0], nums[1])

// FIX
int prev2 = nums[0];
int prev1 = Math.max(nums[0], nums[1]);  // for 2 elements, take the larger one
```

---

## 9. Complexity summary

| Problem | Time | Space | Notes |
|---------|------|-------|-------|
| Maximum Subarray Sum | O(n) | O(1) | classic Kadane |
| Minimum Subarray Sum | O(n) | O(1) | min variant |
| Maximum Product Subarray | O(n) | O(1) | track max and min |
| Maximum Sum Circular Subarray | O(n) | O(1) | two Kadane passes |
| Longest Positive Sum Subarray | O(n) | O(1) | prefix sum variant |
| Max Subarray Sum with One Deletion | O(n) | O(n) | fwd + bwd arrays |
| Max Absolute Sum of Any Subarray | O(n) | O(1) | max(maxKadane, -minKadane) |
| Best Time to Buy and Sell Stock | O(n) | O(1) | Kadane on diff array |
| House Robber | O(n) | O(1) | two variables DP |
| Maximum Alternating Subarray Sum | O(n) | O(1) | toggle sign state |
| Max Sum Rectangle in 2D Matrix | O(n²m) | O(n) | n=cols, m=rows |
| Max Sum Submatrix ≤ K | O(n²m log m) | O(m) | + sorted set binary search |

**General rules:**
- 1D Kadane → always **O(n) time, O(1) space**
- 2D Kadane → **O(n²m)** — n column pairs × m rows per Kadane run
- Variants with extra arrays (one deletion) → **O(n) space**
- Product Kadane handles zeros and negatives in the same O(n) pass

---

## Solve order for interviews

```
Level 1 — Must do before any interview:
  LC 53  → Classic Kadane (foundation)
  LC 152 → Product Kadane (product variant)
  LC 918 → Circular Kadane (circular variant)
  LC 121 → Stock (Kadane in disguise)

Level 2 — Product-based company must:
  LC 1186 → One deletion (DP state)
  LC 198  → House Robber (non-adjacent DP)
  LC 363  → 2D Kadane (matrix variant)

Level 3 — Google / Hard:
  LC 363(K) → 2D + binary search
  LC 2036   → Alternating subarray sum
```
