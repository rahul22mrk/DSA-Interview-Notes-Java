# Dynamic Programming — 1D Problems
### Pattern: Linear DP (Index-based)

> **Core Idea:** Every problem follows one pattern — `dp[i]` = best answer at index `i`.
> Think recursively first, then memoize, then tabulate, then optimize space.

---

## 🧭 PART 1 — How to Recognize & Approach Any DP Problem

---

### Step 1 — Is it DP?

Ask these questions when you read a problem:

| Question | If YES → likely DP |
|---|---|
| Are you asked for **count of ways**? | ✅ |
| Are you asked for **min / max** of something? | ✅ |
| Can a choice at step `i` affect future steps? | ✅ |
| Does brute force have **repeated subproblems**? | ✅ |

> 🚨 **Keyword signals in problem statement:**
> `"minimum cost"`, `"maximum sum"`, `"number of ways"`, `"can you reach"`, `"optimal"`, `"at most k steps"` → Almost always DP.

---

### Step 2 — Identify the DP Type

```
What changes as you move through the problem?
       ↓
   Index only?           →  1D DP   ← (all 5 problems here)
   Two indices?          →  2D DP   (grids, strings)
   Subset of elements?   →  Bitmask DP
   Intervals?            →  Interval DP
```

**For 1D DP, look for:**
- You move left to right through an array or a number
- At each position you make a **choice** (jump 1 or 2, pick or skip)
- The answer at position `i` depends only on **previous positions**

---

### Step 3 — Striver's 3-Step Recursion Framework

> This is the most important framework. Once you can write the recursion,
> memoization and tabulation follow mechanically.

```
┌────────────────────────────────────────────────────────────────────┐
│             STRIVER'S 3 STEPS TO WRITE ANY RECURSION               │
│                                                                    │
│  STEP 1 → Express the problem in terms of an INDEX                 │
│           What parameter uniquely identifies a subproblem?         │
│           Usually it's the current position/index.                 │
│                                                                    │
│  STEP 2 → Do ALL possible things at that index                     │
│           Try every valid choice available at this index.          │
│           (jump 1 step, jump 2 steps, pick element, skip it, etc.) │
│                                                                    │
│  STEP 3 → Based on the problem type, combine results:              │
│           • Count all ways   →  SUM up all choices                 │
│           • Min/Max value    →  MIN or MAX of all choices           │
│           • Check if possible → OR of all choices (any true?)      │
└────────────────────────────────────────────────────────────────────┘
```

**How these 3 steps map to each problem:**

| Problem | Step 1: Index | Step 2: Choices at index | Step 3: Combine |
|---|---|---|---|
| Climbing Stairs | current step `n` | jump 1 back, jump 2 back | SUM (count ways) |
| Frog Jump | current step `i` | jump 1 back, jump 2 back | MIN (minimize cost) |
| Frog Jump K | current step `i` | jump 1..k back | MIN (minimize cost) |
| Max Non-Adjacent | current index `i` | pick element, skip element | MAX (maximize sum) |
| House Robber | current index `i` | pick element, skip element | MAX, run twice |

---

### Step 4 — The 4-Step Coding Ladder

Once you have the recursion (Step 3 above), follow this ladder:

```
① Write plain recursion          (brute force, exponential time)
        ↓
   Add:  int[] dp = new int[n]; Arrays.fill(dp, -1);
         if (dp[ind] != -1) return dp[ind];
         return dp[ind] = ...
        ↓
② Memoization                    (top-down, O(N) time + space)
        ↓
   Convert: recursive calls → iterative loop
            base case → dp[0] = ...
            fill dp[1..n] in order
        ↓
③ Tabulation                     (bottom-up, O(N) time + space)
        ↓
   Replace: dp[i-1] → prev
            dp[i-2] → prev2
            update both at end of each iteration
        ↓
④ Space Optimization             (O(N) time, O(1) space)
```

> 💡 **Interview tip:** Explain Step ① verbally, then code Step ③ directly.
> It shows you understand both the intuition and the optimized solution.

---

### Step 5 — Pattern Recognition Cheatsheet

```
"Number of ways to reach..."         →  SUM  the subproblems
"Minimum cost / Maximum profit..."   →  MIN / MAX the subproblems
"Pick elements, no two adjacent..."  →  Pick/Skip at each index
"Circular array..."                  →  Break into 2 linear runs
"Jump up to K steps..."              →  Loop j from 1 to k inside dp
```

---

## 🔍 PART 2 — Per-Problem Breakdown

---

## Problem 1 — Climbing Stairs

### Applying Striver's 3 Steps

```
STEP 1: Express in terms of index
        → f(n) = number of ways to reach step n

STEP 2: All possible things at index n
        → came from step (n-1)  [took 1 step]
        → came from step (n-2)  [took 2 steps]

STEP 3: Problem asks "count of ways" → SUM
        → f(n) = f(n-1) + f(n-2)
```

**Recurrence:**
```
f(n) = f(n-1) + f(n-2)
Base: f(0) = 1, f(1) = 1
```

### ① Recursive
```java
public static int climbStairs(int n) {
    if (n == 0) return 1;
    if (n == 1) return 1;
    return climbStairs(n - 1) + climbStairs(n - 2);
}
```
⏱ O(2^N) | 💾 O(N) stack

---

### ② Memoization
```java
private int func(int n, int[] dp) {
    if (n <= 1) return 1;
    if (dp[n] != -1) return dp[n];          // cache hit
    return dp[n] = func(n-1, dp) + func(n-2, dp);
}

public int climbStairs(int n) {
    int[] dp = new int[n + 1];
    Arrays.fill(dp, -1);
    return func(n, dp);
}
```
⏱ O(N) | 💾 O(N) + O(N)

---

### ③ Tabulation
```java
public int climbStairs(int n) {
    int[] dp = new int[n + 1];
    dp[0] = 1; dp[1] = 1;
    for (int i = 2; i <= n; i++)
        dp[i] = dp[i-1] + dp[i-2];
    return dp[n];
}
```
⏱ O(N) | 💾 O(N)

---

### ④ Space Optimized ✅
```java
public int climbStairs(int n) {
    int prev2 = 1, prev = 1;
    for (int i = 2; i <= n; i++) {
        int cur = prev + prev2;
        prev2 = prev;
        prev = cur;
    }
    return prev;
}
```
⏱ O(N) | 💾 **O(1)**

> 💡 **Key Insight:** Only the last 2 values are needed at any point — this is Fibonacci in disguise.

---

## Problem 2 — Frog Jump

### Applying Striver's 3 Steps

```
STEP 1: Express in terms of index
        → f(i) = minimum energy to reach step i

STEP 2: All possible things at index i
        → came from step (i-1), cost = abs(h[i] - h[i-1])
        → came from step (i-2), cost = abs(h[i] - h[i-2])

STEP 3: Problem asks "minimum energy" → MIN
        → f(i) = min(f(i-1) + cost1, f(i-2) + cost2)
```

**Recurrence:**
```
dp[i] = min(
    dp[i-1] + abs(h[i] - h[i-1]),
    dp[i-2] + abs(h[i] - h[i-2])   // only if i > 1
)
Base: dp[0] = 0
```

### ① Recursive
```java
public int frogJump(int[] heights, int ind) {
    if (ind == 0) return 0;

    int jumpOne = frogJump(heights, ind-1) + Math.abs(heights[ind] - heights[ind-1]);
    int jumpTwo = Integer.MAX_VALUE;
    if (ind > 1)
        jumpTwo = frogJump(heights, ind-2) + Math.abs(heights[ind] - heights[ind-2]);

    return Math.min(jumpOne, jumpTwo);
}
```
⏱ O(2^N) | 💾 O(N)

---

### ② Memoization
```java
private int solve(int ind, int[] heights, int[] dp) {
    if (ind == 0) return 0;
    if (dp[ind] != -1) return dp[ind];

    int jumpOne = solve(ind-1, heights, dp) + Math.abs(heights[ind] - heights[ind-1]);
    int jumpTwo = Integer.MAX_VALUE;
    if (ind > 1)
        jumpTwo = solve(ind-2, heights, dp) + Math.abs(heights[ind] - heights[ind-2]);

    return dp[ind] = Math.min(jumpOne, jumpTwo);
}
```
⏱ O(N) | 💾 O(N) + O(N)

---

### ③ Tabulation
```java
public int frogJump(int[] heights) {
    int n = heights.length;
    int[] dp = new int[n];
    dp[0] = 0;
    for (int i = 1; i < n; i++) {
        int jumpOne = dp[i-1] + Math.abs(heights[i] - heights[i-1]);
        int jumpTwo = Integer.MAX_VALUE;
        if (i > 1)
            jumpTwo = dp[i-2] + Math.abs(heights[i] - heights[i-2]);
        dp[i] = Math.min(jumpOne, jumpTwo);
    }
    return dp[n-1];
}
```
⏱ O(N) | 💾 O(N)

---

### ④ Space Optimized ✅
```java
public int frogJump(int[] heights) {
    int n = heights.length;
    int prev = 0, prev2 = 0;
    for (int i = 1; i < n; i++) {
        int jumpOne = prev + Math.abs(heights[i] - heights[i-1]);
        int jumpTwo = Integer.MAX_VALUE;
        if (i > 1)
            jumpTwo = prev2 + Math.abs(heights[i] - heights[i-2]);
        int cur = Math.min(jumpOne, jumpTwo);
        prev2 = prev;
        prev = cur;
    }
    return prev;
}
```
⏱ O(N) | 💾 **O(1)**

> 💡 **Key Insight:** Same structure as Climbing Stairs. The only difference — instead of summing, you're taking the minimum, and each choice has an associated cost.

---

## Problem 3 — Frog Jump with K Distances

### Applying Striver's 3 Steps

```
STEP 1: Express in terms of index
        → f(i) = minimum energy to reach step i

STEP 2: All possible things at index i
        → came from ANY of: (i-1), (i-2), ..., (i-k)
        → this is just Problem 2 with a loop instead of 2 hardcoded choices

STEP 3: Problem asks "minimum energy" → MIN over all j choices
        → f(i) = min over j in [1..k] of f(i-j) + abs(h[i] - h[i-j])
```

**Recurrence:**
```
dp[i] = min over j in [1..k]:
    dp[i-j] + abs(h[i] - h[i-j])    // if i-j >= 0
Base: dp[0] = 0
```

### ① Recursive
```java
private int func(int ind, int[] heights, int k) {
    if (ind == 0) return 0;
    int mmStep = Integer.MAX_VALUE;
    for (int j = 1; j <= k; j++) {
        if (ind - j >= 0) {
            int jump = func(ind-j, heights, k) + Math.abs(heights[ind] - heights[ind-j]);
            mmStep = Math.min(jump, mmStep);
        }
    }
    return mmStep;
}
```
⏱ O(k^N) | 💾 O(N)

---

### ② Memoization
```java
private int func(int ind, int[] heights, int k, int[] dp) {
    if (ind == 0) return 0;
    if (dp[ind] != -1) return dp[ind];
    int mmStep = Integer.MAX_VALUE;
    for (int j = 1; j <= k; j++) {
        if (ind - j >= 0) {
            int jump = func(ind-j, heights, k, dp) + Math.abs(heights[ind] - heights[ind-j]);
            mmStep = Math.min(jump, mmStep);
        }
    }
    return dp[ind] = mmStep;
}
```
⏱ O(N × k) | 💾 O(N) + O(N)

---

### ③ Tabulation
```java
public int frogJump(int[] heights, int k) {
    int n = heights.length;
    int[] dp = new int[n];
    dp[0] = 0;
    for (int i = 1; i < n; i++) {
        int mmSteps = Integer.MAX_VALUE;
        for (int j = 1; j <= k; j++) {
            if (i - j >= 0) {
                int jump = dp[i-j] + Math.abs(heights[i] - heights[i-j]);
                mmSteps = Math.min(jump, mmSteps);
            }
        }
        dp[i] = mmSteps;
    }
    return dp[n-1];
}
```
⏱ O(N × k) | 💾 O(N)

---

### ④ Space Optimized ✅ (Rolling Array)
```java
public int frogJump(int[] heights, int k) {
    int n = heights.length;
    int[] dp = new int[k];   // only store last k values
    for (int i = 1; i < n; i++) {
        int mmSteps = Integer.MAX_VALUE;
        for (int j = 1; j <= k; j++) {
            if (i - j >= 0) {
                int jump = dp[(i-j) % k] + Math.abs(heights[i] - heights[i-j]);
                mmSteps = Math.min(mmSteps, jump);
            }
        }
        dp[i % k] = mmSteps;
    }
    return dp[(n-1) % k];
}
```
⏱ O(N × k) | 💾 **O(k)**

> 💡 **Key Insight:** When K=2, this is exactly Problem 2. The "at most K choices" pattern always means — replace hardcoded choices with a `for j = 1 to k` loop inside the DP.

---

## Problem 4 — Maximum Sum of Non-Adjacent Elements

### Applying Striver's 3 Steps

```
STEP 1: Express in terms of index
        → f(i) = maximum sum we can get from index 0 to i

STEP 2: All possible things at index i
        → PICK   arr[i]:  move to (i-2), cannot touch (i-1)
        → SKIP   arr[i]:  move to (i-1), this element ignored

STEP 3: Problem asks "maximum sum" → MAX
        → f(i) = max( arr[i] + f(i-2),  f(i-1) )
```

**Recurrence:**
```
dp[i] = max(
    arr[i] + dp[i-2],   // pick current element
    dp[i-1]              // skip current element
)
Base: dp[0] = arr[0]
```

### ① Recursive
```java
private int func(int ind, int[] arr) {
    if (ind == 0) return arr[0];
    if (ind < 0)  return 0;
    int pick    = arr[ind] + func(ind-2, arr);
    int nonPick = func(ind-1, arr);
    return Math.max(pick, nonPick);
}
```
⏱ O(2^N) | 💾 O(N)

---

### ② Memoization
```java
private int func(int ind, int[] arr, int[] dp) {
    if (ind == 0) return arr[0];
    if (ind < 0)  return 0;
    if (dp[ind] != -1) return dp[ind];
    int pick    = arr[ind] + func(ind-2, arr, dp);
    int nonPick = func(ind-1, arr, dp);
    return dp[ind] = Math.max(pick, nonPick);
}
```
⏱ O(N) | 💾 O(N) + O(N)

---

### ③ Tabulation
```java
public int nonAdjacent(int[] nums) {
    int n = nums.length;
    int[] dp = new int[n];
    dp[0] = nums[0];
    for (int i = 1; i < n; i++) {
        int pick    = nums[i] + (i > 1 ? dp[i-2] : 0);
        int nonPick = dp[i-1];
        dp[i] = Math.max(pick, nonPick);
    }
    return dp[n-1];
}
```
⏱ O(N) | 💾 O(N)

---

### ④ Space Optimized ✅
```java
public int nonAdjacent(int[] nums) {
    int n = nums.length;
    int prev = nums[0], prev2 = 0;
    for (int i = 1; i < n; i++) {
        int pick    = nums[i] + (i > 1 ? prev2 : 0);
        int nonPick = prev;
        int cur = Math.max(pick, nonPick);
        prev2 = prev;
        prev = cur;
    }
    return prev;
}
```
⏱ O(N) | 💾 **O(1)**

> 💡 **Key Insight:** At every index, a binary choice — take it (skip one behind) or leave it (carry previous best). House Robber is just this problem on a circular array.

---

## Problem 5 — House Robber (Circular)

### Applying Striver's 3 Steps

```
STEP 1: Express in terms of index
        → same as Problem 4, but first and last indices are adjacent

STEP 2: All possible things at index i
        → same: PICK or SKIP

STEP 3: Same: MAX — but circular constraint means
        you can never pick both index 0 and index n-1

KEY INSIGHT: Break circular into 2 separate linear runs:
        Run 1 → indices [0 .. n-2]  (exclude last house)
        Run 2 → indices [1 .. n-1]  (exclude first house)
        Answer = max(Run1, Run2)

Why? If you include house[0], you cannot include house[n-1].
     If you include house[n-1], you cannot include house[0].
     These are the only two cases — cover both, take the max.
```

### ① Recursive
```java
private int func(int ind, int[] arr) {
    if (ind == 0) return arr[0];
    if (ind < 0)  return 0;
    int pick    = arr[ind] + func(ind-2, arr);
    int nonPick = func(ind-1, arr);
    return Math.max(pick, nonPick);
}

public int houseRobber(int[] money) {
    int n = money.length;
    if (n == 1) return money[0];
    int[] arr1 = Arrays.copyOfRange(money, 0, n-1);  // exclude last
    int[] arr2 = Arrays.copyOfRange(money, 1, n);    // exclude first
    return Math.max(func(arr1.length-1, arr1), func(arr2.length-1, arr2));
}
```
⏱ O(2^N) | 💾 O(N)

---

### ② Memoization
```java
private int func(int ind, int[] arr, int[] dp) {
    if (ind == 0) return arr[0];
    if (ind < 0)  return 0;
    if (dp[ind] != -1) return dp[ind];
    int pick    = arr[ind] + func(ind-2, arr, dp);
    int nonPick = func(ind-1, arr, dp);
    return dp[ind] = Math.max(pick, nonPick);
}

public int houseRobber(int[] money) {
    int n = money.length;
    if (n == 1) return money[0];
    int[] arr1 = Arrays.copyOfRange(money, 0, n-1);
    int[] arr2 = Arrays.copyOfRange(money, 1, n);
    int[] dp1 = new int[n]; Arrays.fill(dp1, -1);
    int[] dp2 = new int[n]; Arrays.fill(dp2, -1);
    return Math.max(func(arr1.length-1, arr1, dp1), func(arr2.length-1, arr2, dp2));
}
```
⏱ O(N) | 💾 O(N)

---

### ③ Tabulation
```java
private int func(int[] nums) {
    int n = nums.length;
    int[] dp = new int[n];
    dp[0] = nums[0];
    for (int i = 1; i < n; i++) {
        int pick    = nums[i] + (i > 1 ? dp[i-2] : 0);
        int nonPick = dp[i-1];
        dp[i] = Math.max(pick, nonPick);
    }
    return dp[n-1];
}

public int houseRobber(int[] money) {
    int n = money.length;
    if (n == 1) return money[0];
    int[] arr1 = Arrays.copyOfRange(money, 0, n-1);
    int[] arr2 = Arrays.copyOfRange(money, 1, n);
    return Math.max(func(arr1), func(arr2));
}
```
⏱ O(N) | 💾 O(N)

---

### ④ Space Optimized ✅ (My Clean Solution — no extra array copies)
```java
class Solution {
    public int houseRobber(int[] nums) {
        int n = nums.length;
        if (n == 0) return 0;
        if (n == 1) return nums[0];
        // Run Problem 4 twice using start/end pointers — no array copy needed
        return Math.max(solve(nums, 0, n-2), solve(nums, 1, n-1));
    }

    private int solve(int[] nums, int start, int end) {
        int prev = nums[start], prev2 = 0;
        for (int i = start + 1; i <= end; i++) {
            int pick    = nums[i] + (i > start + 1 ? prev2 : 0);
            int notPick = prev;
            int curr = Math.max(pick, notPick);
            prev2 = prev;
            prev = curr;
        }
        return prev;
    }
}
```
⏱ O(N) | 💾 **O(1)**

> 💡 **Key Insight:** Using `start` and `end` pointers instead of copying the array saves O(N) extra space — no `Arrays.copyOfRange` needed.

---

## 🧠 PART 3 — Master Summary

### Pattern Table

| # | Problem | Index | Choices at index | Combine | Trick |
|---|---|---|---|---|---|
| 1 | Climbing Stairs | step `n` | come from n-1, n-2 | SUM | Fibonacci |
| 2 | Frog Jump | step `i` | come from i-1, i-2 + cost | MIN | Cost-Fibonacci |
| 3 | Frog Jump K | step `i` | come from i-1 .. i-k + cost | MIN | Loop j=1..k |
| 4 | Max Non-Adjacent | index `i` | pick or skip | MAX | Binary choice |
| 5 | House Robber | index `i` | pick or skip | MAX | Circular → 2 linear |

---

### Striver's 3-Step Quick Reference

```
┌─────────────────────────────────────────────────────────────────┐
│  STEP 1: Represent the problem in terms of INDEX                 │
│  STEP 2: Do ALL possible things at that index                    │
│  STEP 3: Based on problem type — SUM / MIN / MAX the choices     │
└─────────────────────────────────────────────────────────────────┘
```

---

### Golden Rules

1. **Always identify index first** — what parameter defines a subproblem?
2. **List every valid choice** at that index before writing any code
3. **Problem says "count"** → sum the choices | **"min/max"** → min/max the choices
4. **Base cases** — handle both `ind == 0` AND `ind < 0`
5. **Memoization** — just add `dp[]` array + `if (dp[ind] != -1) return dp[ind]` to recursion
6. **Tabulation** — reverse the recursion, fill dp left to right
7. **Space optimization** — replace `dp[i-1]`, `dp[i-2]` with two variables `prev`, `prev2`
8. **"At most K choices"** → loop `j = 1 to k` inside the DP
9. **Circular array** → always break into 2 separate linear sub-problems

---

*Happy Revision! 🚀*
