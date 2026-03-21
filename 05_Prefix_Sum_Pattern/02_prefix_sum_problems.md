# Prefix Sum Pattern — Solved Problems (12 Problems)

> **Pattern family:** Array / Subarray / Range Query
> **Notes & Templates:** [01_prefix_sum_notes.md](./01_prefix_sum_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Basic Prefix Array
- [P1 — Range Sum Query - Immutable](#problem-1--range-sum-query---immutable)
- [P2 — Find Pivot Index](#problem-2--find-pivot-index)

### Category 2 — HashMap (Count / Existence)
- [P3 — Subarray Sum Equals K](#problem-3--subarray-sum-equals-k)
- [P4 — Contiguous Array](#problem-4--contiguous-array)
- [P5 — Longest Subarray with Sum K](#problem-5--longest-subarray-with-sum-k)

### Category 3 — Modulo HashMap
- [P6 — Subarray Sums Divisible by K](#problem-6--subarray-sums-divisible-by-k)
- [P7 — Continuous Subarray Sum (Multiple of K)](#problem-7--continuous-subarray-sum-multiple-of-k)

### Category 4 — 2D Prefix Sum
- [P8 — Range Sum Query 2D - Immutable](#problem-8--range-sum-query-2d---immutable)
- [P9 — Max Sum of Rectangle No Larger Than K](#problem-9--max-sum-of-rectangle-no-larger-than-k)

### Category 5 — Hard (Deque / Merge Sort)
- [P10 — Shortest Subarray with Sum at Least K](#problem-10--shortest-subarray-with-sum-at-least-k)
- [P11 — Count of Range Sum](#problem-11--count-of-range-sum)

### Bonus / FAANG
- [P12 — Maximum Product Subarray](#problem-12--maximum-product-subarray)

---

## Category 1 — Basic Prefix Array

---

### Problem 1 — Range Sum Query - Immutable
**LeetCode #303 | Difficulty: Easy | Company: Amazon, Google | Category: Basic Prefix Array**

> Given an integer array, handle multiple queries each asking for the sum of elements between indices `left` and `right` inclusive.

#### Core insight

Precompute prefix array once in O(n). Every query answered in O(1) using `prefix[right+1] - prefix[left]`.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Build | `prefix[i+1] = prefix[i] + nums[i]` | size n+1, prefix[0]=0 |
| Query | `prefix[right+1] - prefix[left]` | O(1) per query |

#### Java code

```java
class NumArray {
    private int[] prefix;

    public NumArray(int[] nums) {
        prefix = new int[nums.length + 1];
        for (int i = 0; i < nums.length; i++)
            prefix[i + 1] = prefix[i] + nums[i];
    }

    public int sumRange(int left, int right) {
        return prefix[right + 1] - prefix[left];
    }
}
```

#### Example

```
nums = [−2, 0, 3, −5, 2, −1]
prefix = [0, −2, −2, 1, −4, −2, −3]

sumRange(0, 2) = prefix[3] − prefix[0] = 1 − 0 = 1   ✓  (−2+0+3)
sumRange(2, 5) = prefix[6] − prefix[2] = −3 − (−2) = −1  ✓  (3−5+2−1)
```

---

### Problem 2 — Find Pivot Index
**LeetCode #724 | Difficulty: Easy | Company: Amazon, Facebook | Category: Basic Prefix Array**

> Find the leftmost index where the sum of all elements to the left equals the sum of all elements to the right.

#### Core insight

`leftSum == total - leftSum - nums[i]`  →  `2 * leftSum + nums[i] == total`. No HashMap needed — single pass after computing total.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Compute `total` = sum of all elements | one pass |
| 2 | Walk left→right, track `leftSum` | starts at 0 |
| 3 | Check `2 * leftSum + nums[i] == total` | pivot condition |
| 4 | Add `nums[i]` to `leftSum` | update after check |

#### My Solution

```java
class Solution {
    public int pivotIndex(int[] nums) {
        int leftSum = 0;
        int rightSum = 0;
        int sum = 0;
        for (int num : nums) {
            sum += num;
        }
        for (int i = 0; i < nums.length; i++) {
            rightSum = sum - leftSum - nums[i];
            if (leftSum == rightSum) {
                return i;
            }
            leftSum += nums[i];
        }
        return -1;
    }
}
```

> **Note:** Explicitly computes `rightSum = total - leftSum - nums[i]` and compares directly — easier to read. Reference uses the equivalent `2*leftSum + nums[i] == total` to avoid the extra variable.

#### Reference Solution

```java
public int pivotIndex(int[] nums) {
    int total = 0;
    for (int n : nums) total += n;

    int leftSum = 0;
    for (int i = 0; i < nums.length; i++) {
        if (2 * leftSum + nums[i] == total) return i;
        leftSum += nums[i];
    }
    return -1;
}
```

#### Example

```
nums = [1, 7, 3, 6, 5, 6]
total = 28

i=0: 2*0 + 1 = 1 ≠ 28,  leftSum=1
i=1: 2*1 + 7 = 9 ≠ 28,  leftSum=8
i=2: 2*8 + 3 = 19 ≠ 28, leftSum=11
i=3: 2*11 + 6 = 28 == 28 → return 3 ✓
     (left sum = 1+7+3=11, right sum = 5+6=11)
```

---

## Category 2 — HashMap (Count / Existence)

---

### Problem 3 — Subarray Sum Equals K
**LeetCode #560 | Difficulty: Medium | Company: Amazon, Facebook, Google | Category: HashMap Count**

> Count the total number of subarrays whose sum equals `k`.

#### Core insight

`sum(i,j) = k`  →  `prefix[j] - prefix[i] = k`  →  `prefix[i] = prefix[j] - k`.
For every `j`, count how many previous prefix sums equal `currentSum - k`.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Init | `map = {0: 1}`, `sum = 0`, `count = 0` | seed map before loop |
| Each num | `sum += num` | running prefix sum |
| Lookup | `count += map.get(sum - k, 0)` | subarrays ending here with sum=k |
| Store | `map[sum]++` | after lookup, not before |

#### My Solution

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> hm = new HashMap<>();
        hm.put(0, 1);
        int sum = 0;
        int res = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            int need = sum - k;
            res += hm.getOrDefault(need, 0);
            hm.put(sum, hm.getOrDefault(sum, 0) + 1);
        }
        return res;
    }
}
```

> **Note:** Uses `need = sum - k` as an explicit variable — makes the lookup intent very clear. Reference uses `map.merge()` which is more concise for incrementing. Both are identical in logic.

#### Reference Solution

```java
public int subarraySum(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, 1);          // empty prefix — sum 0 seen once
    int sum = 0, count = 0;

    for (int num : nums) {
        sum += num;
        count += map.getOrDefault(sum - k, 0);
        map.merge(sum, 1, Integer::sum);
    }
    return count;
}
```

#### Example

```
nums = [1, 2, 3],  k = 3

map={0:1}, sum=0, count=0

num=1: sum=1, look for 1-3=-2 → 0,  map={0:1, 1:1}
num=2: sum=3, look for 3-3=0  → 1,  map={0:1, 1:1, 3:1},  count=1
num=3: sum=6, look for 6-3=3  → 1,  map={0:1,1:1,3:1,6:1}, count=2

Output: 2  (subarrays [1,2] and [3]) ✓
```

---

### Problem 4 — Contiguous Array
**LeetCode #525 | Difficulty: Medium | Company: Amazon, Facebook | Category: HashMap Remap**

> Find the maximum length subarray with equal number of 0s and 1s.

#### Core insight

Remap `0 → -1`. Now "equal 0s and 1s" = "subarray sum = 0". Store the **first** index where each prefix sum appears. When the same sum reappears at index `j`, subarray `(firstIndex, j]` has sum 0 → equal 0s and 1s.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Init | `map = {0: -1}`, `sum = 0`, `maxLen = 0` | seed with index -1 |
| Remap | `sum += nums[i] == 0 ? -1 : 1` | 0 becomes -1 |
| If seen | `maxLen = max(maxLen, i - map[sum])` | length of subarray |
| If new | `map[sum] = i` | store first occurrence only |

#### My Solution

```java
class Solution {
    public int findMaxLength(int[] nums) {
        HashMap<Integer, Integer> hm = new HashMap<>();
        int zero = 0;
        int one = 0;
        int diff = 0;
        int ans = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) {
                zero++;
            } else {
                one++;
            }
            diff = zero - one;
            if (diff == 0) {
                ans = Math.max(ans, i + 1);
                continue;
            }
            if (hm.containsKey(diff)) {
                ans = Math.max(ans, i - hm.get(diff));
            } else {
                hm.put(diff, i);
            }
        }
        return ans;
    }
}
```

> **Note:** Tracks `zero` and `one` counters separately and uses `diff = zero - one` as the key — very intuitive to read. Reference remaps `0→-1` directly in the running sum which achieves the same thing more concisely. Also, your `diff==0` early check handles the case where the entire prefix from 0 to `i` is balanced — reference handles this via the `map.put(0, -1)` seed (same effect, different approach).

#### Reference Solution

```java
public int findMaxLength(int[] nums) {
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, -1);         // prefix sum 0 seen at index -1 (before array)
    int sum = 0, maxLen = 0;

    for (int i = 0; i < nums.length; i++) {
        sum += (nums[i] == 0) ? -1 : 1;
        if (map.containsKey(sum)) {
            maxLen = Math.max(maxLen, i - map.get(sum));
        } else {
            map.put(sum, i);   // first occurrence only — maximises length
        }
    }
    return maxLen;
}
```

#### Example

```
nums = [0, 1, 0, 1, 1]
remapped: [−1, 1, −1, 1, 1]

i=0: sum=−1, new → map={0:−1, −1:0}
i=1: sum= 0, seen at −1 → len=1−(−1)=2, maxLen=2
i=2: sum=−1, seen at 0  → len=2−0=2,   maxLen=2
i=3: sum= 0, seen at −1 → len=3−(−1)=4, maxLen=4
i=4: sum= 1, new → map={..., 1:4}

Output: 4  (subarray [0,1,0,1]) ✓
```

---

### Problem 5 — Longest Subarray with Sum K
**LeetCode #325 | Difficulty: Medium | Company: Amazon | Category: HashMap First-seen**

> Find the length of the longest subarray with sum equal to `k`. (Array may contain negatives.)

#### Core insight

Same as Subarray Sum Equals K but store **first occurrence** of each prefix sum (for maximum length). When `sum - k` is found in map, update `maxLen`.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Init | `map = {0: -1}`, `sum = 0`, `maxLen = 0` | seed index -1 |
| Each num | `sum += num` | running prefix |
| If `sum-k` in map | `maxLen = max(maxLen, i - map[sum-k])` | update length |
| Store sum | only if not already in map | first occurrence = max length |

#### Java code

```java
public int maxSubArrayLen(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, -1);
    int sum = 0, maxLen = 0;

    for (int i = 0; i < nums.length; i++) {
        sum += nums[i];
        if (map.containsKey(sum - k)) {
            maxLen = Math.max(maxLen, i - map.get(sum - k));
        }
        if (!map.containsKey(sum)) {
            map.put(sum, i);   // store first occurrence only
        }
    }
    return maxLen;
}
```

#### Example

```
nums = [1, −1, 5, −2, 3],  k = 3
prefix sums: [0, 1, 0, 5, 3, 6]

i=0: sum=1,  look for 1-3=−2 → not found,  map={0:−1, 1:0}
i=1: sum=0,  look for 0-3=−3 → not found,  sum 0 already in map → skip
i=2: sum=5,  look for 5-3=2  → not found,  map={..., 5:2}
i=3: sum=3,  look for 3-3=0  → found at −1, len=3−(−1)=4, maxLen=4
i=4: sum=6,  look for 6-3=3  → found at 3,  len=4−3=1,    maxLen=4

Output: 4  (subarray [1,−1,5,−2]) ✓
```

---

## Category 3 — Modulo HashMap

---

### Problem 6 — Subarray Sums Divisible by K
**LeetCode #974 | Difficulty: Medium | Company: Amazon, Google | Category: Modulo HashMap**

> Return the number of subarrays whose sum is divisible by `k`.

#### Core insight

`sum(i,j) % k == 0`  →  `(prefix[j] - prefix[i]) % k == 0`  →  `prefix[j] % k == prefix[i] % k`. Count pairs with equal remainders. Normalise negative remainders with `((rem % k) + k) % k`.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Init | `map = {0: 1}`, `sum = 0`, `count = 0` | seed remainder 0 |
| Each num | `sum += num` | running prefix |
| Remainder | `rem = ((sum % k) + k) % k` | normalise negatives |
| Lookup | `count += map.get(rem, 0)` | pairs with same remainder |
| Store | `map[rem]++` | after lookup |

#### My Solution

```java
class Solution {
    public int subarraysDivByK(int[] nums, int k) {
        int ans = 0;
        HashMap<Integer, Integer> hm = new HashMap<>();
        hm.put(0, 1);
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            int rem = sum % k;
            if (rem < 0) {
                rem += k;
            }
            ans += hm.getOrDefault(rem, 0);
            hm.put(rem, hm.getOrDefault(rem, 0) + 1);
        }
        return ans;
    }
}
```

> **Note:** Uses `if (rem < 0) rem += k` to handle negatives — explicit and easy to understand. Reference uses the one-liner `((sum % k) + k) % k` which handles it in one shot. Both produce the same result.

#### Reference Solution

```java
public int subarraysDivByK(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, 1);
    int sum = 0, count = 0;

    for (int num : nums) {
        sum += num;
        int rem = ((sum % k) + k) % k;   // normalise negative remainder
        count += map.getOrDefault(rem, 0);
        map.merge(rem, 1, Integer::sum);
    }
    return count;
}
```

#### Example

```
nums = [4, 5, 0, −2, −3, 1],  k = 5
prefix sums: [0, 4, 9, 9, 7, 4, 5]
remainders:  [0, 4, 4, 4, 2, 4, 0]

rem=0: map={0:1} → count+=1=1,  map={0:2}
rem=4: new → map={0:2,4:1}
rem=4: found 1 → count=2,  map={0:2,4:2}
rem=4: found 2 → count=4,  map={0:2,4:3}
rem=2: new → map={...,2:1}
rem=4: found 3 → count=7,  map={0:2,4:4,2:1}
rem=0: found 2 → count=9  map={0:3,...}

Output: 7 ✓
```

---

### Problem 7 — Continuous Subarray Sum (Multiple of K)
**LeetCode #523 | Difficulty: Medium | Company: Amazon, Facebook | Category: Modulo HashMap**

> Return `true` if there exists a subarray of length **at least 2** whose sum is a multiple of `k`.

#### Core insight

Same modulo trick. Store **first index** where each remainder appears. If same remainder seen again at index `j` and `j - firstIndex >= 2` → valid subarray exists.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Init | `map = {0: -1}`, `sum = 0` | seed index -1 |
| Each num | `sum += num`, `rem = sum % k` | running prefix |
| If seen | `if j - map[rem] >= 2 → return true` | length ≥ 2 check |
| If new | `map[rem] = j` | store first occurrence |

#### Java code

```java
public boolean checkSubarraySum(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, -1);
    int sum = 0;

    for (int i = 0; i < nums.length; i++) {
        sum += nums[i];
        int rem = sum % k;
        if (map.containsKey(rem)) {
            if (i - map.get(rem) >= 2) return true;   // length at least 2
        } else {
            map.put(rem, i);   // first occurrence only
        }
    }
    return false;
}
```

#### Example

```
nums = [23, 2, 4, 6, 7],  k = 6

i=0: sum=23, rem=5, new → map={0:−1, 5:0}
i=1: sum=25, rem=1, new → map={..., 1:1}
i=2: sum=29, rem=5, seen at 0, i−0=2 ≥ 2 → return true ✓
     (subarray [2,4] has sum 6, divisible by 6)
```

---

## Category 4 — 2D Prefix Sum

---

### Problem 8 — Range Sum Query 2D - Immutable
**LeetCode #304 | Difficulty: Medium | Company: Amazon, Google | Category: 2D Prefix Array**

> Handle multiple queries on a 2D matrix, each returning the sum of elements inside a rectangle.

#### Core insight

Build a 2D prefix array using inclusion-exclusion. Each query answered in O(1).

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Build | `p[i][j] = mat[i-1][j-1] + p[i-1][j] + p[i][j-1] - p[i-1][j-1]` | (m+1)×(n+1) array |
| Query | `p[r2+1][c2+1] - p[r1][c2+1] - p[r2+1][c1] + p[r1][c1]` | inclusion-exclusion |

#### Java code

```java
class NumMatrix {
    private int[][] prefix;

    public NumMatrix(int[][] matrix) {
        int m = matrix.length, n = matrix[0].length;
        prefix = new int[m + 1][n + 1];

        for (int i = 1; i <= m; i++)
            for (int j = 1; j <= n; j++)
                prefix[i][j] = matrix[i-1][j-1]
                              + prefix[i-1][j]
                              + prefix[i][j-1]
                              - prefix[i-1][j-1];   // add back overlap
    }

    public int sumRegion(int r1, int c1, int r2, int c2) {
        return prefix[r2+1][c2+1]
             - prefix[r1][c2+1]
             - prefix[r2+1][c1]
             + prefix[r1][c1];
    }
}
```

#### Example

```
matrix = [[3,0,1,4],
          [5,6,3,2],
          [1,2,0,1]]

sumRegion(1,1,2,2):
  prefix[3][3] - prefix[1][3] - prefix[3][1] + prefix[1][1]
= (3+0+1+5+6+3+1+2+0) - (3+0+1) - (3+5+1) - (3)
= 21 - 4 - 9 + 3 = 11  ✓  (6+3+2+0)
```

---

### Problem 9 — Max Sum of Rectangle No Larger Than K
**LeetCode #363 | Difficulty: Hard | Company: Google, Amazon | Category: 2D Prefix + Sorted Set**

> Given a matrix and integer `k`, find the max sum of a rectangle in the matrix such that its sum is no larger than `k`.

#### Core insight

Fix top and bottom rows. Compress each column to a 1D array of column sums. Then find the max subarray sum ≤ k in the 1D array using prefix sums + a sorted TreeSet. Binary search for the smallest prefix sum ≥ `currentSum - k`.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Fix top row `r1` | iterate 0 to m-1 | outer loop |
| Fix bottom row `r2` | iterate r1 to m-1 | inner loop |
| Build colSum | `colSum[j] += matrix[r2][j]` | compress rows to 1D |
| 1D problem | find max subarray sum ≤ k | prefix + TreeSet |
| For each prefix | `set.ceiling(sum - k)` → smallest valid prev prefix | binary search |

#### Java code

```java
public int maxSumSubmatrix(int[][] matrix, int k) {
    int m = matrix.length, n = matrix[0].length, res = Integer.MIN_VALUE;

    for (int r1 = 0; r1 < m; r1++) {
        int[] colSum = new int[n];

        for (int r2 = r1; r2 < m; r2++) {
            for (int j = 0; j < n; j++) colSum[j] += matrix[r2][j];

            // Max subarray sum ≤ k using prefix + TreeSet
            TreeSet<Integer> set = new TreeSet<>();
            set.add(0);
            int sum = 0;

            for (int col : colSum) {
                sum += col;
                Integer target = set.ceiling(sum - k);   // smallest prefix ≥ sum-k
                if (target != null) res = Math.max(res, sum - target);
                set.add(sum);
            }
        }
    }
    return res;
}
```

#### Example

```
matrix = [[1,0,1],[0,−2,3]],  k = 2

Fix r1=0, r2=1: colSum = [1, −2, 4]
prefix sums: 0, 1, −1, 3
set={0}: sum=1, ceiling(1−2=−1)=0, res=1−0=1
set={0,1}: sum=−1, ceiling(−1−2=−3)=0, res=max(1,−1−0)=1
set={0,1,−1}: sum=3, ceiling(3−2=1)=1, res=max(1,3−1)=2

Output: 2 ✓
```

---

## Category 5 — Hard (Deque / Merge Sort)

---

### Problem 10 — Shortest Subarray with Sum at Least K
**LeetCode #862 | Difficulty: Hard | Company: Google, Amazon | Category: Prefix + Monotonic Deque**

> Return the length of the shortest non-empty subarray with sum at least `k`. Array may contain negatives.

#### Core insight

Sliding window fails with negatives. Build prefix array. Use a **monotonic increasing deque** of prefix indices. For each `i`, pop front while `prefix[i] - prefix[front] >= k` — these are valid subarrays, take the shortest. Maintain deque increasing by popping back when current prefix ≤ back.

#### Why deque works

```
If prefix[i] <= prefix[j] and i < j:
  prefix[j] can never be a better left endpoint than prefix[i]
  (same or larger sum, but closer to current index = shorter subarray)
  → discard j from the back
```

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Build | `prefix[i+1] = prefix[i] + nums[i]` | long[] to avoid overflow |
| Deque front | while `prefix[i] - prefix[front] >= k` → update res, pop front | shrink from left |
| Deque back | while `prefix[i] <= prefix[back]` → pop back | maintain increasing |
| Push | `deque.addLast(i)` | always push current index |

#### Java code

```java
public int shortestSubarray(int[] nums, int k) {
    int n = nums.length;
    long[] prefix = new long[n + 1];
    for (int i = 0; i < n; i++) prefix[i + 1] = prefix[i] + nums[i];

    int res = Integer.MAX_VALUE;
    Deque<Integer> deque = new ArrayDeque<>();

    for (int i = 0; i <= n; i++) {
        // Front: valid subarray found — take shortest
        while (!deque.isEmpty() && prefix[i] - prefix[deque.peekFirst()] >= k)
            res = Math.min(res, i - deque.pollFirst());

        // Back: maintain increasing prefix values
        while (!deque.isEmpty() && prefix[i] <= prefix[deque.peekLast()])
            deque.pollLast();

        deque.addLast(i);
    }
    return res == Integer.MAX_VALUE ? -1 : res;
}
```

#### Example

```
nums = [2, −1, 2],  k = 3
prefix = [0, 2, 1, 3]

i=0: deque=[0]
i=1: prefix[1]=2, back check: 2>0 ok → deque=[0,1]
i=2: prefix[2]=1, back check: 1<=prefix[1]=2 → pop 1, deque=[0,2]
i=3: prefix[3]=3, front: 3-prefix[0]=3>=3 → res=3-0=3, pop 0
     deque=[2], front: 3-prefix[2]=2 < 3 → stop

Output: 3  ([2,−1,2]) ✓
```

---

### Problem 11 — Count of Range Sum
**LeetCode #327 | Difficulty: Hard | Company: Google | Category: Prefix + Merge Sort**

> Count the number of range sums `sum(i,j)` that lie in `[lower, upper]`.

#### Core insight

Build prefix array. A range sum `prefix[j] - prefix[i]` is in `[lower, upper]` iff `prefix[i]` is in `[prefix[j] - upper, prefix[j] - lower]`. Count such pairs using **merge sort** on the prefix array — during merge, for each right element, find how many left elements fall in the valid range using two pointers.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Build | prefix array of size n+1 | prefix[0]=0 |
| Merge sort | sort prefix array, count valid pairs during merge | divide and conquer |
| Two pointers | for each right half element, advance lo/hi in left half | `[prefix[j]-upper, prefix[j]-lower]` |

#### Java code

```java
public int countRangeSum(int[] nums, int lower, int upper) {
    int n = nums.length;
    long[] prefix = new long[n + 1];
    for (int i = 0; i < n; i++) prefix[i + 1] = prefix[i] + nums[i];
    return mergeCount(prefix, 0, prefix.length, lower, upper);
}

private int mergeCount(long[] prefix, int left, int right, int lower, int upper) {
    if (right - left <= 1) return 0;
    int mid = (left + right) / 2;
    int count = mergeCount(prefix, left, mid, lower, upper)
              + mergeCount(prefix, mid, right, lower, upper);

    int lo = mid, hi = mid;
    for (int i = left; i < mid; i++) {
        // Advance hi: prefix[hi] - prefix[i] <= upper
        while (hi < right && prefix[hi] - prefix[i] <= upper) hi++;
        // Advance lo: prefix[lo] - prefix[i] < lower
        while (lo < right && prefix[lo] - prefix[i] < lower) lo++;
        count += hi - lo;
    }

    // Standard merge
    long[] sorted = Arrays.copyOfRange(prefix, left, right);
    Arrays.sort(sorted);
    System.arraycopy(sorted, 0, prefix, left, sorted.length);
    return count;
}
```

#### Example

```
nums = [−2, 5, −1],  lower = −2,  upper = 2
prefix = [0, −2, 3, 2]

Valid range sums (i,j):
  (0,0): −2 ✓
  (2,3): 2−3=−1 ✓
  (0,3): 2−0=2 ✓
Output: 3 ✓
```

---

## Bonus / FAANG

---

### Problem 12 — Maximum Product Subarray
**LeetCode #152 | Difficulty: Medium | Company: Amazon, Google | Category: Prefix Product (min/max tracking)**

> Find the contiguous subarray with the largest product.

#### Core insight

Unlike sum, product can flip sign. Track both `maxProd` and `minProd` at each index (min can become max after multiplying by a negative). Reset both to `nums[i]` when current element breaks the streak (i.e., zero resets everything).

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Each num | update both max and min | `newMax = max(num, max*num, min*num)` |
| | | `newMin = min(num, max*num, min*num)` |
| Result | track global max | `res = max(res, maxProd)` |

#### Java code

```java
public int maxProduct(int[] nums) {
    int maxProd = nums[0], minProd = nums[0], res = nums[0];

    for (int i = 1; i < nums.length; i++) {
        int num = nums[i];
        int tempMax = Math.max(num, Math.max(maxProd * num, minProd * num));
        minProd     = Math.min(num, Math.min(maxProd * num, minProd * num));
        maxProd     = tempMax;
        res = Math.max(res, maxProd);
    }
    return res;
}
```

#### Example

```
nums = [2, 3, −2, 4]

i=1(3):  maxProd=max(3,6,3)=6,  minProd=min(3,6,3)=3,  res=6
i=2(−2): maxProd=max(−2,−12,−6)=−2, minProd=min(−2,−12,−6)=−12, res=6
i=3(4):  maxProd=max(4,−8,−48)=4,   minProd=min(4,−8,−48)=−48, res=6

Output: 6  (subarray [2,3]) ✓

nums = [−2, 3, −4]
i=1(3):  maxProd=3, minProd=−6
i=2(−4): maxProd=max(−4,−12,24)=24, res=24 ✓
```

---

## Quick Pattern Reference

| Problem | Category | Key technique |
|---------|----------|---------------|
| Range Sum Query | Basic prefix | `prefix[r+1] - prefix[l]` |
| Find Pivot Index | Basic prefix | `2*leftSum + nums[i] == total` |
| Subarray Sum = K | HashMap count | `map.put(0,1)`, count `sum-k` |
| Contiguous Array | HashMap remap | `0→-1`, store first index |
| Longest Subarray Sum K | HashMap first-seen | store first index, max length |
| Subarray Sums Div by K | Modulo HashMap | `((sum%k)+k)%k`, count pairs |
| Continuous Subarray Sum | Modulo first-seen | first index + length ≥ 2 check |
| Range Sum Query 2D | 2D prefix | inclusion-exclusion build + query |
| Max Rectangle ≤ K | 2D prefix + TreeSet | fix rows, 1D + `ceiling(sum-k)` |
| Shortest Subarray ≥ K | Prefix + Deque | monotone increasing deque |
| Count Range Sum | Prefix + Merge Sort | count valid pairs during merge |
| Maximum Product Subarray | Prefix product | track both max and min product |
