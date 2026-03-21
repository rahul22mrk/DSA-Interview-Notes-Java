# Recursion & Backtracking — Solved Problems (30 Problems)

> **Pattern family:** Recursion / Divide & Conquer / Backtracking
> **Notes & Templates:** [01_recursion_backtracking_notes.md](./01_recursion_backtracking_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Basic Recursive Functions
- [P1 — Fibonacci Number](#problem-1--fibonacci-number)
- [P2 — Check if String is Palindrome](#problem-2--check-if-string-is-palindrome)
- [P3 — Check if Array is Sorted](#problem-3--check-if-array-is-sorted)
- [P4 — Sum of Digits of a Number](#problem-4--sum-of-digits-of-a-number)
- [P5 — Remove Occurrences of a Character](#problem-5--remove-occurrences-of-a-character)
- [P6 — Count Good Numbers](#problem-6--count-good-numbers)

### Category 2 — Divide & Conquer
- [P7 — Pow(x, n)](#problem-7--powx-n)
- [P8 — Binary Search (Recursive)](#problem-8--binary-search-recursive)
- [P9 — Merge Sort](#problem-9--merge-sort)
- [P10 — Maximum Subarray (D&C)](#problem-10--maximum-subarray-dc)
- [P11 — Count Smaller Numbers After Self](#problem-11--count-smaller-numbers-after-self)
- [P12 — Reverse Pairs](#problem-12--reverse-pairs)
- [P13 — Count of Range Sum](#problem-13--count-of-range-sum)

### Category 3 — Backtracking (Classic)
- [P14 — Subsets](#problem-14--subsets)
- [P15 — Subsets II (with duplicates)](#problem-15--subsets-ii-with-duplicates)
- [P16 — Permutations](#problem-16--permutations)
- [P17 — Permutations II (with duplicates)](#problem-17--permutations-ii-with-duplicates)
- [P18 — Combinations](#problem-18--combinations)
- [P19 — Combination Sum](#problem-19--combination-sum)
- [P20 — Combination Sum II](#problem-20--combination-sum-ii)
- [P21 — Generate Parentheses](#problem-21--generate-parentheses)
- [P22 — Letter Combinations of a Phone Number](#problem-22--letter-combinations-of-a-phone-number)
- [P23 — Palindrome Partitioning](#problem-23--palindrome-partitioning)
- [P24 — Split String](#problem-24--split-string)

### Category 4 — Backtracking (Hard / Grid)
- [P25 — N-Queens](#problem-25--n-queens)
- [P26 — Word Search](#problem-26--word-search)
- [P27 — Sudoku Solver](#problem-27--sudoku-solver)
- [P28 — Unique Paths III](#problem-28--unique-paths-iii)
- [P29 — Path with Maximum Gold](#problem-29--path-with-maximum-gold)

### Category 5 — Recursive Search
- [P30 — Jump Game](#problem-30--jump-game)

---

## Category 1 — Basic Recursive Functions

---

### Problem 1 — Fibonacci Number
**LeetCode #509 | Difficulty: Easy | Category: Basic Recursion**

> Compute the nth Fibonacci number. `F(0) = 0, F(1) = 1, F(n) = F(n-1) + F(n-2)`.

#### Approach table

| Approach | Time | Space | Notes |
|----------|------|-------|-------|
| Naive Recursion | O(2^n) | O(n) | exponential — TLE for large n |
| Memoization | O(n) | O(n) | cache repeated subproblems |
| Iterative | O(n) | O(1) | optimal |

#### Java code

```java
// Naive — shows the recursion pattern
public int fib(int n) {
    if (n <= 1) return n;        // base cases
    return fib(n-1) + fib(n-2); // recurrence
}

// Memoized — O(n)
public int fibMemo(int n, int[] memo) {
    if (n <= 1) return n;
    if (memo[n] != 0) return memo[n];
    memo[n] = fibMemo(n-1, memo) + fibMemo(n-2, memo);
    return memo[n];
}

// Iterative — O(n) time, O(1) space (best)
public int fibIterative(int n) {
    if (n <= 1) return n;
    int a = 0, b = 1;
    for (int i = 2; i <= n; i++) {
        int c = a + b; a = b; b = c;
    }
    return b;
}
```

#### Example

```
fib(5):
  fib(4)       + fib(3)
  fib(3)+fib(2)  fib(2)+fib(1)
  ...
= 3 + 2 = 5 ✓
```

---

### Problem 2 — Check if String is Palindrome
**Difficulty: Easy | Category: Basic Recursion**

> Check if a string is a palindrome using recursion.

#### Java code

```java
public boolean isPalindrome(String s) {
    return check(s, 0, s.length() - 1);
}

private boolean check(String s, int left, int right) {
    if (left >= right) return true;                         // base case: crossed or met
    if (s.charAt(left) != s.charAt(right)) return false;   // mismatch
    return check(s, left + 1, right - 1);                  // recurse inward
}
```

#### Example

```
"racecar"
check(0,6): r==r ✓ → check(1,5)
check(1,5): a==a ✓ → check(2,4)
check(2,4): c==c ✓ → check(3,3)
check(3,3): left>=right → true ✓
```

---

### Problem 3 — Check if Array is Sorted
**Difficulty: Easy | Category: Basic Recursion**

> Check if an array is sorted in non-decreasing order using recursion.

#### Java code

```java
public boolean isSorted(int[] arr, int n) {
    if (n == 1) return true;                              // base case: single element
    if (arr[n-1] < arr[n-2]) return false;               // last pair violates order
    return isSorted(arr, n - 1);                         // check rest
}
// Call: isSorted(arr, arr.length)
```

#### Example

```
arr = [1, 2, 3, 4]
isSorted(4): arr[3]=4 >= arr[2]=3 ✓ → isSorted(3)
isSorted(3): arr[2]=3 >= arr[1]=2 ✓ → isSorted(2)
isSorted(2): arr[1]=2 >= arr[0]=1 ✓ → isSorted(1) → true ✓
```

---

### Problem 4 — Sum of Digits of a Number
**Difficulty: Easy | Category: Basic Recursion**

> Calculate the sum of digits of a number recursively.

#### Java code

```java
public int sumOfDigits(int n) {
    if (n == 0) return 0;                    // base case
    return (n % 10) + sumOfDigits(n / 10);  // last digit + sum of rest
}
```

#### Example

```
sumOfDigits(1234)
= 4 + sumOfDigits(123)
= 4 + 3 + sumOfDigits(12)
= 4 + 3 + 2 + sumOfDigits(1)
= 4 + 3 + 2 + 1 + sumOfDigits(0)
= 4 + 3 + 2 + 1 + 0 = 10 ✓
```

---

### Problem 5 — Remove Occurrences of a Character
**Difficulty: Easy | Category: Basic Recursion**

> Remove all occurrences of a given character from a string using recursion.

#### Java code

```java
public String removeChar(String s, char ch) {
    if (s.isEmpty()) return "";                                // base case
    String rest = removeChar(s.substring(1), ch);            // recurse on rest
    return s.charAt(0) == ch ? rest : s.charAt(0) + rest;    // skip or keep
}
```

#### Example

```
removeChar("programming", 'g')
= 'p' + removeChar("rogramming", 'g')
...at 'g': skip → removeChar("ramming", 'g')
...at 'g': skip → removeChar("", 'g') → ""
Result: "pramin" ✓
```

---

### Problem 6 — Count Good Numbers
**LeetCode #1922 | Difficulty: Medium | Company: Google | Category: Basic Recursion**

> A digit string of length n is "good" if even indices have even digits (0,2,4,6,8) and odd indices have prime digits (2,3,5,7). Count such strings mod 10^9+7.

#### Core insight

Even positions: 5 choices (0,2,4,6,8). Odd positions: 4 choices (2,3,5,7).
Count = 5^(ceil(n/2)) × 4^(floor(n/2)). Use fast power (Divide & Conquer).

#### Java code

```java
static final long MOD = 1_000_000_007;

public int countGoodNumbers(long n) {
    long evenCount = (n + 1) / 2;  // ceil(n/2) even positions
    long oddCount  = n / 2;         // floor(n/2) odd positions
    return (int)((fastPow(5, evenCount) * fastPow(4, oddCount)) % MOD);
}

private long fastPow(long base, long exp) {
    if (exp == 0) return 1;
    if (exp % 2 == 0) {
        long half = fastPow(base, exp / 2);
        return (half * half) % MOD;
    }
    return (base * fastPow(base, exp - 1)) % MOD;
}
```

---

## Category 2 — Divide & Conquer

---

### Problem 7 — Pow(x, n)
**LeetCode #50 | Difficulty: Medium | Company: Amazon, Google | Category: D&C**

> Implement `pow(x, n)` — x raised to the power n.

#### Core insight

Split: `pow(x, n) = pow(x, n/2) * pow(x, n/2)`. Handle odd n: multiply one more x. Handle negative n: `pow(1/x, -n)`. This is O(log n) not O(n).

#### Java code

```java
public double myPow(double x, int n) {
    long N = n;                      // avoid overflow when n = Integer.MIN_VALUE
    if (N < 0) { x = 1 / x; N = -N; }
    return fastPow(x, N);
}

private double fastPow(double x, long n) {
    if (n == 0) return 1.0;
    double half = fastPow(x, n / 2);
    if (n % 2 == 0) return half * half;
    else            return half * half * x;
}
```

#### Example

```
pow(2.0, 10):
  half = pow(2, 5)
    half = pow(2, 2)
      half = pow(2, 1) = 2 * pow(2,0) = 2
      return 2*2 = 4      (even)
    return 4*4*2 = 32     (odd)
  return 32*32 = 1024     (even) ✓
```

---

### Problem 8 — Binary Search (Recursive)
**LeetCode #704 | Difficulty: Easy | Category: D&C**

> Implement binary search recursively.

#### Java code

```java
public int search(int[] nums, int target) {
    return binarySearch(nums, target, 0, nums.length - 1);
}

private int binarySearch(int[] nums, int target, int left, int right) {
    if (left > right) return -1;                    // base case: not found
    int mid = left + (right - left) / 2;
    if (nums[mid] == target) return mid;
    if (nums[mid] < target)  return binarySearch(nums, target, mid + 1, right);
    else                     return binarySearch(nums, target, left, mid - 1);
}
```

---

### Problem 9 — Merge Sort
**Difficulty: Medium | Category: D&C**

> Sort an array using merge sort (Divide & Conquer).

#### Java code

```java
public void mergeSort(int[] nums, int left, int right) {
    if (left >= right) return;                              // base case
    int mid = left + (right - left) / 2;
    mergeSort(nums, left, mid);                             // sort left half
    mergeSort(nums, mid + 1, right);                        // sort right half
    merge(nums, left, mid, right);                          // merge
}

private void merge(int[] nums, int left, int mid, int right) {
    int[] temp = new int[right - left + 1];
    int i = left, j = mid + 1, k = 0;
    while (i <= mid && j <= right) {
        if (nums[i] <= nums[j]) temp[k++] = nums[i++];
        else                    temp[k++] = nums[j++];
    }
    while (i <= mid)   temp[k++] = nums[i++];
    while (j <= right) temp[k++] = nums[j++];
    System.arraycopy(temp, 0, nums, left, temp.length);
}
```

#### Example

```
[38, 27, 43, 3]
  Split: [38,27] | [43,3]
  Split: [38]|[27]  [43]|[3]
  Merge: [27,38]    [3,43]
  Merge: [3,27,38,43] ✓
Time: O(n log n), Space: O(n)
```

---

### Problem 10 — Maximum Subarray (D&C)
**LeetCode #53 | Difficulty: Medium | Company: Amazon | Category: D&C**

> Find the maximum subarray sum using Divide & Conquer.

#### Core insight

The max subarray is either entirely in left half, entirely in right half, or crosses the midpoint. Crossing case: max suffix of left + max prefix of right.

#### Java code

```java
public int maxSubArray(int[] nums) {
    return divideAndConquer(nums, 0, nums.length - 1);
}

private int divideAndConquer(int[] nums, int left, int right) {
    if (left == right) return nums[left];
    int mid = left + (right - left) / 2;
    int leftMax  = divideAndConquer(nums, left,    mid);
    int rightMax = divideAndConquer(nums, mid + 1, right);
    int crossMax = crossSum(nums, left, right, mid);
    return Math.max(Math.max(leftMax, rightMax), crossMax);
}

private int crossSum(int[] nums, int left, int right, int mid) {
    int leftSum = Integer.MIN_VALUE, rightSum = Integer.MIN_VALUE;
    int currSum = 0;
    for (int i = mid; i >= left; i--) {           // max suffix of left part
        currSum += nums[i];
        leftSum = Math.max(leftSum, currSum);
    }
    currSum = 0;
    for (int i = mid + 1; i <= right; i++) {      // max prefix of right part
        currSum += nums[i];
        rightSum = Math.max(rightSum, currSum);
    }
    return leftSum + rightSum;
}
```

---

### Problem 11 — Count Smaller Numbers After Self
**LeetCode #315 | Difficulty: Hard | Company: Google, Amazon | Category: D&C (Merge Sort)**

> Return a count array where `count[i]` = number of elements to the right of `nums[i]` that are smaller than `nums[i]`.

#### Core insight

Modified merge sort on (value, index) pairs. During merge, when right element is placed before left elements, all remaining left elements have found a smaller element to their right.

#### Java code

```java
public List<Integer> countSmaller(int[] nums) {
    int n = nums.length;
    int[] count = new int[n];
    int[][] indexed = new int[n][2];
    for (int i = 0; i < n; i++) indexed[i] = new int[]{nums[i], i};
    mergeSort(indexed, count, 0, n - 1);
    List<Integer> res = new ArrayList<>();
    for (int c : count) res.add(c);
    return res;
}

private void mergeSort(int[][] arr, int[] count, int left, int right) {
    if (left >= right) return;
    int mid = left + (right - left) / 2;
    mergeSort(arr, count, left, mid);
    mergeSort(arr, count, mid + 1, right);
    merge(arr, count, left, mid, right);
}

private void merge(int[][] arr, int[] count, int left, int mid, int right) {
    int[][] temp = new int[right - left + 1][2];
    int i = left, j = mid + 1, k = 0, rightCount = 0;
    while (i <= mid && j <= right) {
        if (arr[j][0] < arr[i][0]) {
            rightCount++;                          // arr[j] is smaller than arr[i..mid]
            temp[k++] = arr[j++];
        } else {
            count[arr[i][1]] += rightCount;        // rightCount elements jumped over arr[i]
            temp[k++] = arr[i++];
        }
    }
    while (i <= mid) { count[arr[i][1]] += rightCount; temp[k++] = arr[i++]; }
    while (j <= right) temp[k++] = arr[j++];
    System.arraycopy(temp, 0, arr, left, temp.length);
}
```

#### Example

```
nums = [5, 2, 6, 1]
Answer: [2, 1, 1, 0]
  5 → 2 smaller to right (2 and 1)
  2 → 1 smaller to right (1)
  6 → 1 smaller to right (1)
  1 → 0 smaller to right ✓
```

---

### Problem 12 — Reverse Pairs
**LeetCode #493 | Difficulty: Hard | Company: Amazon | Category: D&C (Merge Sort)**

> Count pairs (i, j) where i < j and `nums[i] > 2 * nums[j]`.

#### Java code

```java
public int reversePairs(int[] nums) {
    return mergeSort(nums, 0, nums.length - 1);
}

private int mergeSort(int[] nums, int left, int right) {
    if (left >= right) return 0;
    int mid = left + (right - left) / 2;
    int count = mergeSort(nums, left, mid) + mergeSort(nums, mid + 1, right);

    // Count reverse pairs BEFORE merging
    int j = mid + 1;
    for (int i = left; i <= mid; i++) {
        while (j <= right && nums[i] > 2L * nums[j]) j++;
        count += j - (mid + 1);
    }

    // Standard merge
    int[] temp = new int[right - left + 1];
    int i = left, k = 0; j = mid + 1;
    while (i <= mid && j <= right) {
        if (nums[i] <= nums[j]) temp[k++] = nums[i++];
        else                    temp[k++] = nums[j++];
    }
    while (i <= mid)   temp[k++] = nums[i++];
    while (j <= right) temp[k++] = nums[j++];
    System.arraycopy(temp, 0, nums, left, temp.length);
    return count;
}
```

---

### Problem 13 — Count of Range Sum
**LeetCode #327 | Difficulty: Hard | Company: Google | Category: D&C (Merge Sort)**

> Count number of range sums that lie in `[lower, upper]`.

#### Core insight

Convert to prefix sums. A range sum `sum[i..j] = prefix[j+1] - prefix[i]`. Use merge sort on prefix array — during merge, count pairs where `lower ≤ prefix[j] - prefix[i] ≤ upper`.

#### Java code

```java
public int countRangeSum(int[] nums, int lower, int upper) {
    int n = nums.length;
    long[] prefix = new long[n + 1];
    for (int i = 0; i < n; i++) prefix[i+1] = prefix[i] + nums[i];
    return mergeSort(prefix, 0, n, lower, upper);
}

private int mergeSort(long[] prefix, int left, int right, int lower, int upper) {
    if (left >= right) return 0;
    int mid = left + (right - left) / 2;
    int count = mergeSort(prefix, left, mid, lower, upper)
              + mergeSort(prefix, mid+1, right, lower, upper);

    // Count valid pairs
    int j = mid+1, k = mid+1;
    for (int i = left; i <= mid; i++) {
        while (k <= right && prefix[k] - prefix[i] <  lower) k++;
        while (j <= right && prefix[j] - prefix[i] <= upper) j++;
        count += j - k;
    }

    // Standard merge
    long[] temp = new long[right - left + 1];
    int i = left, p = mid+1, q = 0;
    while (i <= mid && p <= right) {
        if (prefix[i] <= prefix[p]) temp[q++] = prefix[i++];
        else                        temp[q++] = prefix[p++];
    }
    while (i <= mid)  temp[q++] = prefix[i++];
    while (p <= right) temp[q++] = prefix[p++];
    System.arraycopy(temp, 0, prefix, left, temp.length);
    return count;
}
```

---

## Category 3 — Backtracking (Classic)

> **The LeetCode general backtracking template (from the famous post):**
> Same structure for ALL problems below — only 3 things change:
> 1. **When to add result** (every call vs only at leaf)
> 2. **What to skip** (duplicates, used elements)
> 3. **What index to pass next** (`i` vs `i+1` for reuse)

---

### Problem 14 — Subsets
**LeetCode #78 | Difficulty: Medium | Company: Amazon, Facebook | Category: Backtracking**

> Return all possible subsets of an array with distinct integers.

#### Key: add result at EVERY recursive call (including empty set)

#### Java code

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(list, new ArrayList<>(), nums, 0);
    return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] nums, int start) {
    list.add(new ArrayList<>(tempList));           // add at EVERY level
    for (int i = start; i < nums.length; i++) {
        tempList.add(nums[i]);
        backtrack(list, tempList, nums, i + 1);
        tempList.remove(tempList.size() - 1);      // undo
    }
}
```

#### Example

```
nums = [1,2,3]
Recursion tree (each node added to result):
[]
[1] → [1,2] → [1,2,3]
              [1,3]
[2] → [2,3]
[3]
Output: [[], [1], [1,2], [1,2,3], [1,3], [2], [2,3], [3]] ✓ (2^3 = 8 subsets)
```

---

### Problem 15 — Subsets II (with duplicates)
**LeetCode #90 | Difficulty: Medium | Company: Amazon | Category: Backtracking**

> Same as Subsets but input may contain duplicates. Return only unique subsets.

#### Key: sort first + skip `if (i > start && nums[i] == nums[i-1])`

#### Java code

```java
public List<List<Integer>> subsetsWithDup(int[] nums) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);                             // MUST sort first
    backtrack(list, new ArrayList<>(), nums, 0);
    return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] nums, int start) {
    list.add(new ArrayList<>(tempList));
    for (int i = start; i < nums.length; i++) {
        if (i > start && nums[i] == nums[i-1]) continue;  // skip dup at same level
        tempList.add(nums[i]);
        backtrack(list, tempList, nums, i + 1);
        tempList.remove(tempList.size() - 1);
    }
}
```

#### Example

```
nums = [1,2,2]
After sort: [1,2,2]
At level 0: i=0(1), i=1(2), i=2 → skip (2==2, i>start)
Result: [[],[1],[1,2],[1,2,2],[2],[2,2]] ✓  (no duplicate [2] sets)
```

---

### Problem 16 — Permutations
**LeetCode #46 | Difficulty: Medium | Company: Amazon, Google | Category: Backtracking**

> Return all permutations of distinct integers.

#### Key: add only at LEAF (when size == n). Use `used[]` to track chosen elements.

#### Java code

```java
public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> list = new ArrayList<>();
    backtrack(list, new ArrayList<>(), nums, new boolean[nums.length]);
    return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] nums, boolean[] used) {
    if (tempList.size() == nums.length) {
        list.add(new ArrayList<>(tempList));       // add only at LEAF
        return;
    }
    for (int i = 0; i < nums.length; i++) {
        if (used[i]) continue;
        used[i] = true;
        tempList.add(nums[i]);
        backtrack(list, tempList, nums, used);
        used[i] = false;
        tempList.remove(tempList.size() - 1);
    }
}
```

#### Example

```
nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]] ✓ (3! = 6)
```

---

### Problem 17 — Permutations II (with duplicates)
**LeetCode #47 | Difficulty: Medium | Company: Amazon | Category: Backtracking**

> Return all unique permutations when input may contain duplicates.

#### Key: sort + `if (used[i] || (i>0 && nums[i]==nums[i-1] && !used[i-1])) continue`

#### Java code

```java
public List<List<Integer>> permuteUnique(int[] nums) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(list, new ArrayList<>(), nums, new boolean[nums.length]);
    return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] nums, boolean[] used) {
    if (tempList.size() == nums.length) { list.add(new ArrayList<>(tempList)); return; }
    for (int i = 0; i < nums.length; i++) {
        // Skip if used, OR if same as previous AND previous not used at this level
        if (used[i] || (i > 0 && nums[i] == nums[i-1] && !used[i-1])) continue;
        used[i] = true;
        tempList.add(nums[i]);
        backtrack(list, tempList, nums, used);
        used[i] = false;
        tempList.remove(tempList.size() - 1);
    }
}
```

#### Why `!used[i-1]`?

```
nums = [1,1,2]  (sorted)
When placing first 1 (i=0): used[0]=false initially — OK
When placing second 1 (i=1): nums[1]==nums[0] AND !used[0] → SKIP
This prevents [1b,1a,2] which is a duplicate of [1a,1b,2]
```

---

### Problem 18 — Combinations
**LeetCode #77 | Difficulty: Medium | Category: Backtracking**

> Find all combinations of k numbers chosen from range [1, n].

#### Java code

```java
public List<List<Integer>> combine(int n, int k) {
    List<List<Integer>> list = new ArrayList<>();
    backtrack(list, new ArrayList<>(), n, k, 1);
    return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int n, int k, int start) {
    if (tempList.size() == k) { list.add(new ArrayList<>(tempList)); return; }
    for (int i = start; i <= n; i++) {
        tempList.add(i);
        backtrack(list, tempList, n, k, i + 1);
        tempList.remove(tempList.size() - 1);
    }
}
```

---

### Problem 19 — Combination Sum
**LeetCode #39 | Difficulty: Medium | Company: Amazon, Google | Category: Backtracking**

> Find all combinations that sum to target. Same element can be reused.

#### Key: pass `i` (not `i+1`) to allow reuse. Prune when `remain < 0`.

#### Java code

```java
public List<List<Integer>> combinationSum(int[] nums, int target) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(list, new ArrayList<>(), nums, target, 0);
    return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] nums, int remain, int start) {
    if (remain < 0) return;
    if (remain == 0) { list.add(new ArrayList<>(tempList)); return; }
    for (int i = start; i < nums.length; i++) {
        tempList.add(nums[i]);
        backtrack(list, tempList, nums, remain - nums[i], i);  // i NOT i+1 (reuse!)
        tempList.remove(tempList.size() - 1);
    }
}
```

#### Example

```
candidates=[2,3,6,7], target=7
[2,2,3]: 2+2+3=7 ✓
[7]:     7=7 ✓
Output: [[2,2,3],[7]] ✓
```

---

### Problem 20 — Combination Sum II
**LeetCode #40 | Difficulty: Medium | Company: Amazon | Category: Backtracking**

> Same but each number used only once, input has duplicates.

#### Key: sort + `i>start && nums[i]==nums[i-1]` skip + pass `i+1`

#### Java code

```java
public List<List<Integer>> combinationSum2(int[] nums, int target) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(list, new ArrayList<>(), nums, target, 0);
    return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] nums, int remain, int start) {
    if (remain < 0) return;
    if (remain == 0) { list.add(new ArrayList<>(tempList)); return; }
    for (int i = start; i < nums.length; i++) {
        if (i > start && nums[i] == nums[i-1]) continue;  // skip dup at same level
        tempList.add(nums[i]);
        backtrack(list, tempList, nums, remain - nums[i], i + 1);  // i+1 (no reuse)
        tempList.remove(tempList.size() - 1);
    }
}
```

---

### Problem 21 — Generate Parentheses
**LeetCode #22 | Difficulty: Medium | Company: Amazon, Google, Facebook | Category: Backtracking**

> Generate all combinations of n pairs of valid parentheses.

#### Key: open < n → add `(`. close < open → add `)`. Prune otherwise.

#### Java code

```java
public List<String> generateParenthesis(int n) {
    List<String> list = new ArrayList<>();
    backtrack(list, new StringBuilder(), 0, 0, n);
    return list;
}

private void backtrack(List<String> list, StringBuilder sb, int open, int close, int n) {
    if (sb.length() == 2 * n) { list.add(sb.toString()); return; }
    if (open < n) {
        sb.append('(');
        backtrack(list, sb, open + 1, close, n);
        sb.deleteCharAt(sb.length() - 1);
    }
    if (close < open) {
        sb.append(')');
        backtrack(list, sb, open, close + 1, n);
        sb.deleteCharAt(sb.length() - 1);
    }
}
```

#### Example

```
n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"] ✓ (Catalan(3) = 5)
```

---

### Problem 22 — Letter Combinations of a Phone Number
**LeetCode #17 | Difficulty: Medium | Company: Amazon, Google | Category: Backtracking**

> Given a string of digits, return all possible letter combinations (phone keypad).

#### Java code

```java
String[] phone = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};

public List<String> letterCombinations(String digits) {
    List<String> list = new ArrayList<>();
    if (digits.isEmpty()) return list;
    backtrack(list, new StringBuilder(), digits, 0);
    return list;
}

private void backtrack(List<String> list, StringBuilder sb, String digits, int idx) {
    if (idx == digits.length()) { list.add(sb.toString()); return; }
    String letters = phone[digits.charAt(idx) - '0'];
    for (char c : letters.toCharArray()) {
        sb.append(c);
        backtrack(list, sb, digits, idx + 1);
        sb.deleteCharAt(sb.length() - 1);
    }
}
```

#### Example

```
digits = "23"
'2'→abc, '3'→def
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"] ✓ (3×3=9)
```

---

### Problem 23 — Palindrome Partitioning
**LeetCode #131 | Difficulty: Medium | Company: Amazon, Facebook | Category: Backtracking**

> Partition string s such that every substring is a palindrome. Return all partitions.

#### Key: add result only when `start == s.length()`. Try every split; check isPalindrome.

#### Java code

```java
public List<List<String>> partition(String s) {
    List<List<String>> list = new ArrayList<>();
    backtrack(list, new ArrayList<>(), s, 0);
    return list;
}

private void backtrack(List<List<String>> list, List<String> tempList, String s, int start) {
    if (start == s.length()) { list.add(new ArrayList<>(tempList)); return; }
    for (int i = start; i < s.length(); i++) {
        if (isPalindrome(s, start, i)) {
            tempList.add(s.substring(start, i + 1));
            backtrack(list, tempList, s, i + 1);
            tempList.remove(tempList.size() - 1);
        }
    }
}

private boolean isPalindrome(String s, int lo, int hi) {
    while (lo < hi) if (s.charAt(lo++) != s.charAt(hi--)) return false;
    return true;
}
```

#### Example

```
s = "aab"
Partitions: ["a","a","b"], ["aa","b"] ✓
```

---

### Problem 24 — Split String
**Difficulty: Medium | Category: Backtracking**

> Split a string into substrings such that each substring is a valid word from a dictionary (or each part converts to a specific pattern).

#### Java code

```java
// General split/partition template
public List<List<String>> splitString(String s, Set<String> dict) {
    List<List<String>> result = new ArrayList<>();
    backtrack(result, new ArrayList<>(), s, 0, dict);
    return result;
}

private void backtrack(List<List<String>> result, List<String> temp, String s, int start, Set<String> dict) {
    if (start == s.length()) { result.add(new ArrayList<>(temp)); return; }
    for (int i = start + 1; i <= s.length(); i++) {
        String sub = s.substring(start, i);
        if (dict.contains(sub)) {
            temp.add(sub);
            backtrack(result, temp, s, i, dict);
            temp.remove(temp.size() - 1);
        }
    }
}
```

---

## Category 4 — Backtracking (Hard / Grid)

---

### Problem 25 — N-Queens
**LeetCode #51 | Difficulty: Hard | Company: Amazon, Google | Category: Constraint Backtracking**

> Place n queens on an n×n chessboard so no two queens attack each other.

#### Key: try each column in each row. isValid checks column + both diagonals.

#### Java code

```java
public List<List<String>> solveNQueens(int n) {
    List<List<String>> result = new ArrayList<>();
    char[][] board = new char[n][n];
    for (char[] row : board) Arrays.fill(row, '.');
    backtrack(result, board, 0);
    return result;
}

private void backtrack(List<List<String>> result, char[][] board, int row) {
    if (row == board.length) { result.add(construct(board)); return; }
    for (int col = 0; col < board.length; col++) {
        if (isValid(board, row, col)) {
            board[row][col] = 'Q';
            backtrack(result, board, row + 1);
            board[row][col] = '.';            // undo
        }
    }
}

private boolean isValid(char[][] board, int row, int col) {
    int n = board.length;
    for (int i = 0; i < row; i++)                      if (board[i][col] == 'Q') return false;
    for (int i=row-1, j=col-1; i>=0 && j>=0; i--,j--) if (board[i][j] == 'Q') return false;
    for (int i=row-1, j=col+1; i>=0 && j<n;  i--,j++) if (board[i][j] == 'Q') return false;
    return true;
}

private List<String> construct(char[][] board) {
    List<String> res = new ArrayList<>();
    for (char[] row : board) res.add(new String(row));
    return res;
}
```

#### Example

```
n=4, one solution:
. Q . .
. . . Q
Q . . .
. . Q .
Output: 2 solutions ✓
```

---

### Problem 26 — Word Search
**LeetCode #79 | Difficulty: Medium | Company: Amazon, Facebook | Category: Grid Backtracking**

> Find if word exists in a 2D grid by adjacent (up/down/left/right) letters.

#### Key: mark visited with `'#'`, unmark on return (backtrack).

#### Java code

```java
int[] dr = {0, 0, 1, -1};
int[] dc = {1, -1, 0, 0};

public boolean exist(char[][] board, String word) {
    for (int r = 0; r < board.length; r++)
        for (int c = 0; c < board[0].length; c++)
            if (dfs(board, word, 0, r, c)) return true;
    return false;
}

private boolean dfs(char[][] board, String word, int idx, int r, int c) {
    if (idx == word.length()) return true;
    if (r < 0 || r >= board.length || c < 0 || c >= board[0].length) return false;
    if (board[r][c] != word.charAt(idx)) return false;

    char tmp = board[r][c];
    board[r][c] = '#';                               // mark visited
    for (int d = 0; d < 4; d++)
        if (dfs(board, word, idx + 1, r+dr[d], c+dc[d])) {
            board[r][c] = tmp;
            return true;
        }
    board[r][c] = tmp;                               // unmark (backtrack)
    return false;
}
```

---

### Problem 27 — Sudoku Solver
**LeetCode #37 | Difficulty: Hard | Company: Amazon, Google | Category: Constraint Backtracking**

> Solve a Sudoku puzzle by filling in empty cells.

#### Java code

```java
public void solveSudoku(char[][] board) {
    solve(board);
}

private boolean solve(char[][] board) {
    for (int r = 0; r < 9; r++) {
        for (int c = 0; c < 9; c++) {
            if (board[r][c] != '.') continue;
            for (char num = '1'; num <= '9'; num++) {
                if (isValid(board, r, c, num)) {
                    board[r][c] = num;
                    if (solve(board)) return true;  // found solution
                    board[r][c] = '.';              // backtrack
                }
            }
            return false;    // no valid number → backtrack to previous cell
        }
    }
    return true;             // all cells filled
}

private boolean isValid(char[][] board, int row, int col, char num) {
    for (int i = 0; i < 9; i++) {
        if (board[row][i] == num) return false;   // row
        if (board[i][col] == num) return false;   // column
        // 3×3 box
        int boxRow = 3*(row/3) + i/3, boxCol = 3*(col/3) + i%3;
        if (board[boxRow][boxCol] == num) return false;
    }
    return true;
}
```

---

### Problem 28 — Unique Paths III
**LeetCode #980 | Difficulty: Hard | Company: Google | Category: Grid Backtracking**

> Walk from start to end, visiting every non-obstacle cell exactly once.

#### Java code

```java
int result = 0;

public int uniquePathsIII(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int startR = 0, startC = 0, empty = 0;
    for (int r = 0; r < m; r++)
        for (int c = 0; c < n; c++) {
            if (grid[r][c] != -1) empty++;
            if (grid[r][c] == 1) { startR = r; startC = c; }
        }
    dfs(grid, startR, startC, empty);
    return result;
}

int[] dr = {0,0,1,-1}, dc = {1,-1,0,0};

private void dfs(int[][] grid, int r, int c, int remaining) {
    if (r < 0 || r >= grid.length || c < 0 || c >= grid[0].length || grid[r][c] == -1) return;
    if (grid[r][c] == 2) {
        if (remaining == 1) result++;   // reached end and visited all cells
        return;
    }
    int tmp = grid[r][c];
    grid[r][c] = -1;                   // mark visited
    for (int d = 0; d < 4; d++) dfs(grid, r+dr[d], c+dc[d], remaining - 1);
    grid[r][c] = tmp;                  // unmark (backtrack)
}
```

---

### Problem 29 — Path with Maximum Gold
**LeetCode #1219 | Difficulty: Medium | Company: Amazon | Category: Grid Backtracking**

> Find the path that collects maximum gold. Can start/end anywhere. Cannot visit cell with 0 gold or revisit.

#### Java code

```java
int maxGold = 0;
int[] dr = {0,0,1,-1}, dc = {1,-1,0,0};

public int getMaximumGold(int[][] grid) {
    for (int r = 0; r < grid.length; r++)
        for (int c = 0; c < grid[0].length; c++)
            if (grid[r][c] != 0) dfs(grid, r, c, 0);
    return maxGold;
}

private void dfs(int[][] grid, int r, int c, int collected) {
    if (r < 0 || r >= grid.length || c < 0 || c >= grid[0].length || grid[r][c] == 0) return;
    int gold = grid[r][c];
    collected += gold;
    maxGold = Math.max(maxGold, collected);
    grid[r][c] = 0;                    // mark visited
    for (int d = 0; d < 4; d++) dfs(grid, r+dr[d], c+dc[d], collected);
    grid[r][c] = gold;                 // unmark (backtrack)
}
```

---

## Category 5 — Recursive Search

---

### Problem 30 — Jump Game
**LeetCode #55 | Difficulty: Medium | Company: Amazon, Google | Category: Recursive Search**

> Given an array where each element is the max jump length from that position, determine if you can reach the last index.

#### Note: Greedy is optimal (O(n)), but recursive/memoized approach shown here for pattern completeness.

#### Java code

```java
// Greedy — O(n), O(1) — best approach
public boolean canJump(int[] nums) {
    int maxReach = 0;
    for (int i = 0; i < nums.length; i++) {
        if (i > maxReach) return false;
        maxReach = Math.max(maxReach, i + nums[i]);
    }
    return true;
}

// Recursive + Memoization — O(n²), O(n)
// 0=unknown, 1=reachable, -1=not reachable
public boolean canJumpMemo(int[] nums) {
    int[] memo = new int[nums.length];
    return canReach(nums, 0, memo);
}

private boolean canReach(int[] nums, int pos, int[] memo) {
    if (pos >= nums.length - 1) return true;
    if (memo[pos] != 0) return memo[pos] == 1;
    for (int jump = nums[pos]; jump >= 1; jump--) {
        if (canReach(nums, pos + jump, memo)) {
            memo[pos] = 1;
            return true;
        }
    }
    memo[pos] = -1;
    return false;
}
```

---

## Quick Pattern Reference

| Problem | When to add | Skip condition | Pass next |
|---------|------------|----------------|-----------|
| Subsets | Every call | — | `i+1` |
| Subsets II | Every call | `i>start && nums[i]==nums[i-1]` | `i+1` |
| Permutations | `size==n` (leaf) | `used[i]` | `0` (all) |
| Permutations II | `size==n` (leaf) | `used[i]` or dup+!used[i-1] | `0` (all) |
| Combinations | `size==k` | — | `i+1` |
| Combination Sum | `remain==0` | `remain<0` | `i` (reuse) |
| Combination Sum II | `remain==0` | `remain<0` or dup | `i+1` |
| Generate Parens | `len==2n` | `open>n` or `close>open` | — |
| Phone Combinations | `idx==digits.len` | — | `idx+1` |
| Palindrome Partition | `start==s.len` | not palindrome | `i+1` |
| N-Queens | `row==n` | `!isValid` | `row+1` |
| Word Search | `idx==word.len` | OOB or visited or mismatch | 4 dirs |
| Sudoku | board full | `!isValid` | next cell |
| Unique Paths III | end + remaining==1 | OOB or obstacle | 4 dirs |
| Path with Max Gold | — (maximize) | OOB or 0 | 4 dirs |
