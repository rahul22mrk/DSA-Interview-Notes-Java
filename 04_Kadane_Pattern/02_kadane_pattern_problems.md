# Kadane's Algorithm — Solved Problems (12 Problems)

> **Pattern family:** Dynamic Programming / Array Optimization
> **Notes & Templates:** [01_kadane_pattern_notes.md](./01_kadane_pattern_notes.md)
> **Language:** Java

---

## Table of Contents

### Level 1 — Must Do (Classic Kadane)
- [P1 — Maximum Subarray Sum](#problem-1--maximum-subarray-sum)
- [P2 — Minimum Subarray Sum](#problem-2--minimum-subarray-sum)
- [P3 — Maximum Product Subarray](#problem-3--maximum-product-subarray)
- [P4 — Maximum Sum Circular Subarray](#problem-4--maximum-sum-circular-subarray)
- [P5 — Best Time to Buy and Sell Stock](#problem-5--best-time-to-buy-and-sell-stock)

### Level 2 — Product Based Must Do
- [P6 — Maximum Subarray Sum with One Deletion](#problem-6--maximum-subarray-sum-with-one-deletion)
- [P7 — Longest Subarray with Positive Sum](#problem-7--longest-subarray-with-positive-sum)
- [P8 — Maximum Absolute Sum of Any Subarray](#problem-8--maximum-absolute-sum-of-any-subarray)
- [P9 — House Robber](#problem-9--house-robber)

### Level 3 — Hard / FAANG
- [P10 — Maximum Sum Rectangle in 2D Matrix](#problem-10--maximum-sum-rectangle-in-2d-matrix)
- [P11 — Maximum Sum of Submatrix No Larger than K](#problem-11--maximum-sum-of-submatrix-no-larger-than-k)
- [P12 — Maximum Alternating Subarray Sum](#problem-12--maximum-alternating-subarray-sum)

---

## Level 1 — Must Do (Classic Kadane)

---

### Problem 1 — Maximum Subarray Sum
**LeetCode #53 | Difficulty: Easy | Company: Amazon, Google | Pattern: Classic Kadane**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | `cur = max(arr[i], cur + arr[i])` | restart or extend |
| 2 | `best = max(best, cur)` | track global best |
| Init | `cur = best = arr[0]` | handles all-negative arrays |

#### Java code

```java
public int maxSubArray(int[] nums) {
    int cur = nums[0], best = nums[0];

    for (int i = 1; i < nums.length; i++) {
        cur = Math.max(nums[i], cur + nums[i]);   // restart or extend
        best = Math.max(best, cur);               // track global max
    }
    return best;
}
```

#### Example

```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]

i=1: cur=max(1,-2+1)=max(1,-1)=1,    best=1
i=2: cur=max(-3,1-3)=max(-3,-2)=-2,  best=1
i=3: cur=max(4,-2+4)=max(4,2)=4,     best=4
i=4: cur=max(-1,4-1)=max(-1,3)=3,    best=4
i=5: cur=max(2,3+2)=max(2,5)=5,      best=5
i=6: cur=max(1,5+1)=max(1,6)=6,      best=6
i=7: cur=max(-5,6-5)=max(-5,1)=1,    best=6
i=8: cur=max(4,1+4)=max(4,5)=5,      best=6

Output: 6  (subarray [4,-1,2,1]) ✓
```

---

### Problem 2 — Minimum Subarray Sum
**GFG | Difficulty: Easy | Pattern: Min Kadane**

> Find the contiguous subarray with the minimum sum.

#### Java code

```java
public int minSubarraySum(int[] nums) {
    int cur = nums[0], best = nums[0];

    for (int i = 1; i < nums.length; i++) {
        cur = Math.min(nums[i], cur + nums[i]);   // restart or extend (min version)
        best = Math.min(best, cur);
    }
    return best;
}
```

#### Example

```
Input: nums = [3,-4,2,-3,-1,7,-5]

Trace: cur → 3,-4,-2,-5,-6,1,-5
best = -6  (subarray [-4,2,-3,-1]) ✓
```

> **Use case:** directly used inside Circular Kadane (total − minSubarray = max wrapping subarray)

---

### Problem 3 — Maximum Product Subarray
**LeetCode #152 | Difficulty: Medium | Company: Amazon, Microsoft | Pattern: Product Kadane**

#### Core insight

Negative × negative = positive. So a large negative product can become the maximum after another negative number. Track both `maxProd` (best so far) and `minProd` (worst so far, could flip to best). Swap them when current element is negative.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | If `arr[i] < 0` → swap `maxProd` and `minProd` | negative flips max↔min |
| 2 | `maxProd = max(arr[i], maxProd * arr[i])` | restart or extend max |
| 3 | `minProd = min(arr[i], minProd * arr[i])` | restart or extend min |
| 4 | `result = max(result, maxProd)` | track global best |

#### Java code

```java
public int maxProduct(int[] nums) {
    int maxProd = nums[0], minProd = nums[0], result = nums[0];

    for (int i = 1; i < nums.length; i++) {
        if (nums[i] < 0) {
            int temp = maxProd;     // swap before multiplying
            maxProd = minProd;
            minProd = temp;
        }
        maxProd = Math.max(nums[i], maxProd * nums[i]);
        minProd = Math.min(nums[i], minProd * nums[i]);
        result = Math.max(result, maxProd);
    }
    return result;
}
```

#### Example

```
Input: nums = [2,3,-2,4]

i=1(3):  maxP=max(3,2*3)=6,  minP=min(3,2*3)=3  → result=6
i=2(-2): swap→maxP=3,minP=6
         maxP=max(-2,3*-2)=max(-2,-6)=-2
         minP=min(-2,6*-2)=min(-2,-12)=-12  → result=6
i=3(4):  maxP=max(4,-2*4)=max(4,-8)=4
         minP=min(4,-12*4)=min(4,-48)=-48  → result=6

Output: 6  ([2,3]) ✓

Input: nums = [-2,0,-1]
i=1(0): maxP=max(0,-2*0)=0, minP=0  → result=0
i=2(-1): swap→maxP=0,minP=0
         maxP=max(-1,0)=0  → result=0
Output: 0  (single element 0) ✓
```

---

### Problem 4 — Maximum Sum Circular Subarray
**LeetCode #918 | Difficulty: Medium | Company: Google, Facebook | Pattern: Circular Kadane**

#### Core insight

Two possible cases:
- **Case 1 — No wrap:** max subarray is in the middle → normal Kadane
- **Case 2 — Wrap:** max subarray wraps around → `total − min subarray`

Take the max of both cases. Edge case: if all elements are negative, `total == minKadane` — the "wrap" case would give 0 (empty subarray) which is invalid. Return `maxKadane`.

```
Case 2 visual:
arr = [5,-3,5]
total = 7
minSubarray = [-3] = -3
wrapping max = 7 - (-3) = 10  → [5,5] wrapping around
```

#### Java code

```java
public int maxSubarraySumCircular(int[] nums) {
    int maxKadane = nums[0], minKadane = nums[0];
    int curMax = nums[0], curMin = nums[0];
    int total = nums[0];

    for (int i = 1; i < nums.length; i++) {
        total += nums[i];

        curMax = Math.max(nums[i], curMax + nums[i]);
        maxKadane = Math.max(maxKadane, curMax);

        curMin = Math.min(nums[i], curMin + nums[i]);
        minKadane = Math.min(minKadane, curMin);
    }

    // All negative edge case: total == minKadane → wrap gives 0 (invalid)
    return (total == minKadane) ? maxKadane : Math.max(maxKadane, total - minKadane);
}
```

#### Example

```
Input: nums = [1,-2,3,-2]
total = 0
maxKadane = 3  (subarray [3])
minKadane = -4 (subarray [-2,3,-2]... wait: curMin trace below)
  i=1(-2): curMin=min(-2,1-2)=-2, minKadane=-2
  i=2(3):  curMin=min(3,-2+3)=1,  minKadane=-2
  i=3(-2): curMin=min(-2,1-2)=-2, minKadane=-2
total - minKadane = 0 - (-2) = 2
Output: max(3, 2) = 3 ✓

Input: nums = [5,-3,5]
total=7, maxKadane=7, minKadane=-3
Output: max(7, 7-(-3)) = max(7,10) = 10 ✓ (wrapping [5,5])
```

---

### Problem 5 — Best Time to Buy and Sell Stock
**LeetCode #121 | Difficulty: Easy | Company: Amazon, Adobe | Pattern: Kadane on difference array**

#### Core insight

`profit = price[sell] - price[buy]`. Transform: let `diff[i] = price[i] - price[i-1]`. Then maximum profit = maximum subarray sum of `diff`. This is Kadane on the difference array.

Or equivalently: track `minPrice` seen so far, compute `profit = currentPrice - minPrice`, track max profit.

#### Java code

```java
// Approach A: track minPrice (cleaner, same logic as Kadane)
public int maxProfit(int[] prices) {
    int minPrice = prices[0], maxProfit = 0;

    for (int i = 1; i < prices.length; i++) {
        maxProfit = Math.max(maxProfit, prices[i] - minPrice);  // sell today
        minPrice = Math.min(minPrice, prices[i]);               // update cheapest buy
    }
    return maxProfit;
}

// Approach B: explicit Kadane on diff array
public int maxProfitKadane(int[] prices) {
    int cur = 0, best = 0;
    for (int i = 1; i < prices.length; i++) {
        cur = Math.max(0, cur + prices[i] - prices[i-1]);  // restart at 0 (not buy at loss)
        best = Math.max(best, cur);
    }
    return best;
}
```

#### Example

```
Input: prices = [7,1,5,3,6,4]

Approach A:
i=1: minPrice=1, profit=max(0,1-7)=0
i=2: minPrice=1, profit=max(0,5-1)=4
i=3: minPrice=1, profit=max(4,3-1)=4
i=4: minPrice=1, profit=max(4,6-1)=5
i=5: minPrice=1, profit=max(5,4-1)=5

Output: 5  (buy at 1, sell at 6) ✓
```

---

## Level 2 — Product Based Must Do

---

### Problem 6 — Maximum Subarray Sum with One Deletion
**LeetCode #1186 | Difficulty: Medium | Company: Google | Pattern: Forward + Backward Kadane**

#### Core insight

Delete exactly one element at index `i`. The remaining subarray has two parts:
- Best subarray ending at `i-1` (forward Kadane)
- Best subarray starting at `i+1` (backward Kadane)

Precompute both, then for each `i`: `result = max(result, fwd[i-1] + bwd[i+1])`.

#### Java code

```java
public int maximumSum(int[] arr) {
    int n = arr.length;
    int[] fwd = new int[n];   // fwd[i] = max subarray sum ending AT i (inclusive)
    int[] bwd = new int[n];   // bwd[i] = max subarray sum starting FROM i (inclusive)

    // Build forward array
    fwd[0] = arr[0];
    for (int i = 1; i < n; i++)
        fwd[i] = Math.max(arr[i], fwd[i-1] + arr[i]);

    // Build backward array
    bwd[n-1] = arr[n-1];
    for (int i = n-2; i >= 0; i--)
        bwd[i] = Math.max(arr[i], bwd[i+1] + arr[i]);

    // Without deletion: best of fwd
    int result = Arrays.stream(fwd).max().getAsInt();

    // With deletion of index i: fwd[i-1] + bwd[i+1]
    for (int i = 1; i < n-1; i++)
        result = Math.max(result, fwd[i-1] + bwd[i+1]);

    return result;
}
```

#### Example

```
Input: arr = [1,-2,0,3]

fwd: [1,-1,0,3]      (max subarray ending at each index)
bwd: [2,-2,3,3]      (max subarray starting at each index... wait:
  bwd[3]=3, bwd[2]=max(0,0+3)=3, bwd[1]=max(-2,-2+3)=1, bwd[0]=max(1,1+1)=2)

No deletion: max(fwd) = 3
Delete index 1(-2): fwd[0]+bwd[2] = 1+3 = 4
Delete index 2(0):  fwd[1]+bwd[3] = -1+3 = 2

Output: 4 ✓  (delete -2: subarray [1,0,3])
```

---

### Problem 7 — Longest Subarray with Positive Sum
**GFG | Difficulty: Medium | Company: Flipkart | Pattern: Prefix Sum + HashMap**

> Find the longest subarray with sum > 0 (or sum ≥ 1).

#### Core insight

Use prefix sums. For sum > 0: find the longest subarray where `prefix[j] - prefix[i] > 0`, i.e., `prefix[j] > prefix[i]`. Use a map to store the first occurrence of each prefix sum.

#### Java code

```java
public int longestSubarrayPositiveSum(int[] nums) {
    Map<Integer, Integer> firstOccurrence = new HashMap<>();
    firstOccurrence.put(0, -1);   // prefix sum 0 seen before index 0
    int prefix = 0, maxLen = 0;

    for (int i = 0; i < nums.length; i++) {
        prefix += nums[i];

        // To have positive sum: we need a previous prefix < current prefix
        // Greedy: iterate from prefix-1 down... OR: note that any prefix < current works
        // Simplification: if prefix > 0, entire [0..i] is valid
        if (prefix > 0) {
            maxLen = Math.max(maxLen, i + 1);
        } else {
            // Find if there's a smaller prefix sum seen before
            // We want FIRST occurrence of a sum < prefix (e.g., prefix-1, prefix-2...)
            // But for max LENGTH: we want the EARLIEST index with prefix < current
            // Store first occurrence; check if (prefix - 1) was seen earlier
            if (firstOccurrence.containsKey(prefix - 1)) {
                maxLen = Math.max(maxLen, i - firstOccurrence.get(prefix - 1));
            }
        }
        firstOccurrence.putIfAbsent(prefix, i);   // only store first occurrence
    }
    return maxLen;
}
```

#### Example

```
Input: nums = [-3, 4, -1, 2, 1]
Prefix:       -3  1   0   2  3

prefix>0 at i=1: maxLen=2
prefix>0 at i=2? no (0). firstOccurrence has: {0:-1,-3:0,1:1}
prefix>0 at i=3: maxLen=4  (entire [0..3])
prefix>0 at i=4: maxLen=5
Output: 5 ✓
```

---

### Problem 8 — Maximum Absolute Sum of Any Subarray
**LeetCode #1749 | Difficulty: Medium | Company: Google | Pattern: Dual Kadane**

> Maximum of |subarray sum|. This equals max(maxSubarraySum, |minSubarraySum|).

#### Java code

```java
public int maxAbsoluteSum(int[] nums) {
    int maxCur = 0, maxSum = 0;   // max subarray sum
    int minCur = 0, minSum = 0;   // min subarray sum

    for (int n : nums) {
        maxCur = Math.max(n, maxCur + n);
        maxSum = Math.max(maxSum, maxCur);

        minCur = Math.min(n, minCur + n);
        minSum = Math.min(minSum, minCur);
    }
    return Math.max(maxSum, Math.abs(minSum));
}
```

#### Example

```
Input: nums = [1,-3,2,3,-4]
maxKadane = 5  ([2,3])
minKadane = -5 ([-3,2,3,-4]... wait: trace)
  minCur: 1,-3,-1,2,-4 → wait
  i=1(-3): minCur=min(-3,1-3)=-3, minSum=-3
  i=2(2):  minCur=min(2,-3+2)=-1, minSum=-3
  i=3(3):  minCur=min(3,-1+3)=2,  minSum=-3
  i=4(-4): minCur=min(-4,2-4)=-4, minSum=-4
maxSum=5, |minSum|=4
Output: max(5,4) = 5 ✓
```

---

### Problem 9 — House Robber
**LeetCode #198 | Difficulty: Medium | Company: Amazon, Google | Pattern: Non-adjacent Kadane DP**

#### Core insight

At each house you either rob it (take `nums[i] + best from i-2`) or skip it (keep `best from i-1`). This is Kadane with a gap constraint — you can't take adjacent elements.

#### Java code

```java
public int rob(int[] nums) {
    if (nums.length == 1) return nums[0];

    int prev2 = nums[0];
    int prev1 = Math.max(nums[0], nums[1]);   // best of first two

    for (int i = 2; i < nums.length; i++) {
        int curr = Math.max(prev1,              // skip house i
                            prev2 + nums[i]);   // rob house i
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```

#### Example

```
Input: nums = [2,7,9,3,1]

prev2=2, prev1=max(2,7)=7
i=2(9): curr=max(7,2+9)=11, prev2=7, prev1=11
i=3(3): curr=max(11,7+3)=11, prev2=11, prev1=11
i=4(1): curr=max(11,11+1)=12, prev2=11, prev1=12

Output: 12  (rob houses 0,2,4 → 2+9+1=12) ✓
```

---

## Level 3 — Hard / FAANG

---

### Problem 10 — Maximum Sum Rectangle in 2D Matrix
**LeetCode #363 | Difficulty: Hard | Company: Google, Amazon | Pattern: 2D Kadane**

#### Core insight

Fix the left and right column boundaries. For each pair (left, right), compress all rows between those columns into a 1D array (row-wise sum). Run Kadane on that 1D array. This gives the max sum rectangle with those column boundaries.

```
Matrix:
 1  2 -1 -4 -20
-8 -3  4  2   1
 3  8 10  1   3
-4 -1  1  7  -6

Fix left=1, right=3:
rowSum = [2+(-1)+(-4), -3+4+2, 8+10+1, -1+1+7] = [-3, 3, 19, 7]
Kadane on [-3,3,19,7] = 29 (subarray [3,19,7])
This corresponds to rows 1-3, cols 1-3.
```

#### Java code

```java
public int maxSumSubmatrix(int[][] matrix, int k) {
    // For this problem: max sum ≤ k (see Problem 11)
    // For unconstrained: call kadane directly
    int rows = matrix.length, cols = matrix[0].length;
    int maxSum = Integer.MIN_VALUE;

    for (int left = 0; left < cols; left++) {
        int[] rowSum = new int[rows];

        for (int right = left; right < cols; right++) {
            // Add column `right` to row sums
            for (int r = 0; r < rows; r++)
                rowSum[r] += matrix[r][right];

            // Run 1D Kadane on compressed row sums
            maxSum = Math.max(maxSum, kadane(rowSum));
        }
    }
    return maxSum;
}

private int kadane(int[] arr) {
    int cur = arr[0], best = arr[0];
    for (int i = 1; i < arr.length; i++) {
        cur = Math.max(arr[i], cur + arr[i]);
        best = Math.max(best, cur);
    }
    return best;
}
```

#### Example

```
Input: matrix = [[1,2],[-1,-2],[3,4]]
Cols=2, rows=3

left=0,right=0: rowSum=[1,-1,3], Kadane=3
left=0,right=1: rowSum=[3,-3,7], Kadane=7
left=1,right=1: rowSum=[2,-2,4], Kadane=4

maxSum = 7  (entire matrix columns 0-1, rows 2 = [[3,4]])? 
Actually Kadane([3,-3,7]): cur=3,-3,7→ restart at index 1→cur=-3,7→best=7 ✓
Output: 7
```

---

### Problem 11 — Maximum Sum of Submatrix No Larger than K
**LeetCode #363 | Difficulty: Hard | Company: Google | Pattern: 2D Kadane + TreeSet binary search**

#### Core insight

Same as Problem 10 (2D Kadane column compression), but instead of unrestricted Kadane, find the maximum subarray sum ≤ k. Use a **TreeSet of prefix sums** and binary search for `prefixSum - k` (smallest value in set that is ≥ `currentPrefix - k`).

#### Java code

```java
public int maxSumSubmatrix(int[][] matrix, int k) {
    int rows = matrix.length, cols = matrix[0].length;
    int result = Integer.MIN_VALUE;

    for (int left = 0; left < cols; left++) {
        int[] rowSum = new int[rows];

        for (int right = left; right < cols; right++) {
            for (int r = 0; r < rows; r++)
                rowSum[r] += matrix[r][right];

            // Find max subarray sum ≤ k using prefix sums + TreeSet
            result = Math.max(result, maxSumNoLargerThanK(rowSum, k));
        }
    }
    return result;
}

private int maxSumNoLargerThanK(int[] arr, int k) {
    TreeSet<Integer> prefixSet = new TreeSet<>();
    prefixSet.add(0);
    int prefix = 0, best = Integer.MIN_VALUE;

    for (int n : arr) {
        prefix += n;
        // We want: prefix - prevPrefix ≤ k → prevPrefix ≥ prefix - k
        Integer prevPrefix = prefixSet.ceiling(prefix - k);  // smallest value ≥ prefix-k
        if (prevPrefix != null)
            best = Math.max(best, prefix - prevPrefix);
        prefixSet.add(prefix);
    }
    return best;
}
```

#### Example

```
Input: matrix = [[1,0,1],[0,-2,3]], k = 2

left=0,right=2: rowSum=[2,1]
  maxSumNoLargerThanK([2,1], 2):
  prefix=2: ceiling(2-2=0) in {0} → 0 → sum=2-0=2 ≤ k ✓ → best=2
  prefix=3: ceiling(3-2=1) in {0,2} → 2 → sum=3-2=1 ≤ k ✓ → best=2
  Result for this pair: 2

Output: 2 ✓
```

---

### Problem 12 — Maximum Alternating Subarray Sum
**LeetCode #2036 | Difficulty: Medium | Company: Microsoft | Pattern: Alternating Kadane**

#### Core insight

Elements at even positions (0-indexed from subarray start) are added, odd positions are subtracted. At each index maintain two states:
- `maxEnd` = max alternating sum of subarray ENDING at index i with nums[i] **added** (positive)
- `minEnd` = max alternating sum of subarray ENDING at index i with nums[i] **subtracted** (negative)

```
Transition:
  new_maxEnd = max(nums[i],   minEnd + nums[i])   // start fresh OR extend (add nums[i])
  new_minEnd = max(-nums[i], maxEnd - nums[i])    // start fresh OR extend (subtract nums[i])
```

#### Java code

```java
public long maximumAlternatingSubarraySum(int[] nums) {
    long maxEnd = nums[0];   // subarray ending here with nums[0] added (+)
    long minEnd = -nums[0];  // subarray ending here with nums[0] subtracted (-)
    long result = nums[0];

    for (int i = 1; i < nums.length; i++) {
        long newMaxEnd = Math.max(nums[i], minEnd + nums[i]);   // add nums[i]
        long newMinEnd = Math.max(-nums[i], maxEnd - nums[i]);  // subtract nums[i]
        maxEnd = newMaxEnd;
        minEnd = newMinEnd;
        result = Math.max(result, maxEnd);
    }
    return result;
}
```

#### Example

```
Input: nums = [3,-1,1,2]

i=0: maxEnd=3, minEnd=-3, result=3
i=1(-1): newMaxEnd=max(-1,-3-1)=max(-1,-4)=-1
         newMinEnd=max(1,3-(-1))=max(1,4)=4
         maxEnd=-1, minEnd=4, result=3
i=2(1):  newMaxEnd=max(1,4+1)=5
         newMinEnd=max(-1,-1-1)=max(-1,-2)=-1
         maxEnd=5, minEnd=-1, result=5
i=3(2):  newMaxEnd=max(2,-1+2)=max(2,1)=2
         newMinEnd=max(-2,5-2)=max(-2,3)=3
         maxEnd=2, minEnd=3, result=5

Output: 5  (subarray [3,-1,1,2]: 3-(-1)+1 = no... [3,-1,1]: 3-1+1... 
Actually alternating: nums[0]-nums[1]+nums[2] = 3-(-1)+1=5) ✓
```

---

## Quick Pattern Reference

| Problem | Pattern | Key Formula |
|---------|---------|-------------|
| Max Subarray Sum | Classic Kadane | `cur = max(n, cur+n)` |
| Min Subarray Sum | Min Kadane | `cur = min(n, cur+n)` |
| Max Product Subarray | Product Kadane | swap max/min on negative |
| Max Sum Circular | Circular Kadane | `max(maxK, total - minK)` |
| Buy & Sell Stock | Kadane on diff | `profit = price - minPrice` |
| Max Sum One Deletion | Forward + Backward | `fwd[i-1] + bwd[i+1]` |
| Longest Positive Sum | Prefix + HashMap | first occurrence of prefix |
| Max Absolute Sum | Dual Kadane | `max(maxK, abs(minK))` |
| House Robber | Non-adjacent DP | `max(prev1, prev2 + curr)` |
| Max Sum Rectangle 2D | 2D Kadane | fix cols, compress rows, Kadane |
| Max Sum ≤ K | 2D Kadane + TreeSet | `ceiling(prefix - k)` in set |
| Alternating Sum | State Kadane | toggle add/subtract each step |
