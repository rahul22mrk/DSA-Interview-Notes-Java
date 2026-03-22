# Dynamic Programming — Complete Notes & Templates

> **Pattern family:** Optimization / Counting / Decision Making
> **Difficulty range:** Easy → Hard
> **Language:** Java
> **Problems file:** [02_dp_problems.md](./02_dp_problems.md)
> **Pattern Guide Level 1:** [03_dp_patterns_level1.md](./03_dp_patterns_level1.md)
> **Pattern Guide Level 2:** [04_dp_patterns_level2.md](./04_dp_patterns_level2.md)

---

## Table of Contents

1. [How to identify DP](#1-how-to-identify-dp) ← **start here**
2. [What is DP? — Core concepts](#2-what-is-dp--core-concepts)
3. [Optimal Substructure & Overlapping Subproblems](#3-optimal-substructure--overlapping-subproblems)
4. [Top-Down vs Bottom-Up](#4-top-down-vs-bottom-up)
5. [Core rules](#5-core-rules)
6. [2-Question framework](#6-2-question-framework)
7. [All 14 DP patterns](#7-all-14-dp-patterns)
8. [Universal Java templates](#8-universal-java-templates)
9. [Quick reference cheatsheet](#9-quick-reference-cheatsheet)
10. [Common mistakes](#10-common-mistakes)
11. [Complexity summary](#11-complexity-summary)

---

## 1. How to identify DP

### Keyword scanner

| If you see this... | DP Pattern |
|--------------------|-----------|
| `"minimum / maximum cost / path to reach target"` | Min/Max Path to Target |
| `"number of distinct ways to reach"` | Distinct Ways (Counting) |
| `"can we partition / achieve sum"` (boolean) | 0/1 Knapsack |
| `"select items, each used once, max value"` | 0/1 Knapsack (Bounded) |
| `"items reusable / infinite supply"` | Unbounded Knapsack |
| `"two strings — edit / match / delete / common"` | DP on Strings (LCS family) |
| `"longest / shortest subsequence"` | LCS / LIS / Palindrome DP |
| `"grid — move right/down only"` | DP on Grids |
| `"burst / split / merge intervals optimally"` | Interval DP / MCM / Partition DP |
| `"buy and sell stocks with constraints"` | DP on Stocks |
| `"choose or skip current element"` | Decision Making / Fibonacci DP |
| `"probability / expected value over steps"` | Probability DP |
| `"count numbers with digit property in range"` | Digit DP |
| `"assign tasks, small n ≤ 20"` | DP + Bitmask |
| `"tree node selection — no adjacent"` | DP on Trees |

### Brute force test

```
Brute force = try all combinations → exponential O(2^n) or O(n!)
→ If same sub-problem appears MULTIPLE TIMES in recursion tree → DP (memoize it)
→ If optimal answer built from optimal sub-answers → DP (optimal substructure)

Two REQUIRED properties for DP:
  1. Overlapping Sub-problems
  2. Optimal Substructure
```

### Decision flowchart

```
Can problem be broken into sub-problems?
        │
        ├── Do sub-problems OVERLAP?
        │       ├── YES → Use DP
        │       └── NO  → Divide & Conquer (no cache benefit)
        │
        ├── What are you computing?
        │       ├── Min / Max value    → dp[i] = min/max(dp[prev]) + cost
        │       ├── Count ways         → dp[i] += dp[i - way]
        │       └── Boolean (can we?)  → dp[i] |= dp[i - val]
        │
        └── State dimension?
                ├── 1D dp[i]         → Fibonacci, Knapsack, LIS
                ├── 2D dp[i][j]      → Strings, Grid, Knapsack(item,cap)
                ├── Interval dp[i][j] → MCM, Burst Balloons
                └── dp[mask]          → Bitmask DP
```

---

## 2. What is DP? — Core concepts

DP solves problems by breaking them into **overlapping sub-problems**, solving each exactly once, and storing results to avoid recomputation.

```
Without DP — Fibonacci recursion tree (O(2^n)):

              f(5)
            /      \
         f(4)      f(3)
        /    \     /   \
      f(3)  f(2) f(2) f(1)   ← f(3), f(2) computed AGAIN!
      ...

With DP — memoize: f(3) and f(2) computed ONCE → O(n)
```

**Key insight:** DP is NOT about a specific algorithm — it is a technique to eliminate redundant computation by remembering answers to sub-problems.

---

## 3. Optimal Substructure & Overlapping Subproblems

### Optimal Substructure

The optimal solution to the problem **contains** optimal solutions to its sub-problems.

```
Example — Shortest Path A→C via B:
  If A→B→C is optimal, then A→B must be optimal sub-path.
  (If there was a shorter A→B', the overall path would use that.)

Example — Coin Change (amount=11, coins=[1,5,6]):
  Optimal for 11 = 1 + Optimal for 10
                 = 1 + (Optimal for 5 + Optimal for 5)
```

**Counter-example (no optimal substructure):** Longest path in graph with cycles — can't decompose.

### Overlapping Subproblems

Same sub-problem solved **multiple times** in naive recursion.

```java
// Fibonacci — f(3) called twice in computing f(5)
// Without memoization:
f(5) calls f(4) and f(3)
f(4) calls f(3) and f(2)   ← f(3) called again!

// With memoization:
int[] memo = new int[n+1];
Arrays.fill(memo, -1);
int fib(int n) {
    if (n <= 1) return n;
    if (memo[n] != -1) return memo[n];   // already computed!
    return memo[n] = fib(n-1) + fib(n-2);
}
```

---

## 4. Top-Down vs Bottom-Up

### Top-Down (Memoization)

Write the **recursive solution** first, then add a **cache**.

```java
// Step 1: write recursion
int solve(int n) {
    if (n == 0) return 0;          // base case
    return solve(n-1) + solve(n-2); // recurrence
}

// Step 2: add memo array
int[] memo = new int[n+1];
Arrays.fill(memo, -1);

int solve(int n) {
    if (n <= 1) return n;
    if (memo[n] != -1) return memo[n];   // cache hit
    return memo[n] = solve(n-1) + solve(n-2);
}
```

**Pros:** Easy to write, only computes needed states, natural recursion structure.
**Cons:** Recursion stack overhead, can cause StackOverflow for large n.

### Bottom-Up (Tabulation)

Build the answer iteratively from **base cases upward**.

```java
int[] dp = new int[n+1];
dp[0] = 0; dp[1] = 1;
for (int i = 2; i <= n; i++)
    dp[i] = dp[i-1] + dp[i-2];
return dp[n];
```

**Pros:** No recursion stack, easier space optimization, faster in practice.
**Cons:** Must compute all states even if not needed.

### When to use which?

| Situation | Prefer |
|-----------|--------|
| Not all states needed (sparse) | Top-Down |
| Space optimization critical | Bottom-Up |
| Recursion depth very large | Bottom-Up |
| Problem natural in recursion | Top-Down |
| Interview / competitive | Bottom-Up (cleaner) |

---

## 5. Core rules

**Rule 1 — Define the state BEFORE writing any code**
```java
// Always answer: "dp[i] = ???" first
// dp[i]    = minimum coins to make amount i
// dp[i][j] = length of LCS of s1[0..i-1] and s2[0..j-1]
// dp[i][w] = max value using items 0..i with capacity w
// dp[i][j] = max coins from bursting balloons in open range (i..j)
```

**Rule 2 — Recurrence is the heart — get it right**
```java
// Min/Max path:    dp[i] = min(dp[i-1], dp[i-2]) + cost[i]
// Count ways:      dp[i] += dp[i - way[j]]  for each valid way
// 0/1 Knapsack:   dp[w] = max(dp[w], dp[w-wt] + val) — iterate w REVERSE
// Unbounded:       dp[w] = max(dp[w], dp[w-wt] + val) — iterate w FORWARD
// LCS match:       dp[i][j] = dp[i-1][j-1] + 1
// LCS no match:    dp[i][j] = max(dp[i-1][j], dp[i][j-1])
// Interval:        dp[i][j] = opt_k(dp[i][k] + dp[k+1][j] + cost(i,k,j))
```

**Rule 3 — Base cases — think carefully**
```java
// dp[0] = 0   → "0 cost to do nothing" — Min/Max problems
// dp[0] = 1   → "1 way to do nothing" — Counting problems
// dp[i][i] = single element value   — Interval DP
// dp[0][j] = j, dp[i][0] = i       — Edit Distance (all inserts/deletes)
```

**Rule 4 — 0/1 vs Unbounded: the loop direction**
```java
// 0/1 Knapsack — each item AT MOST ONCE → traverse capacity REVERSE
for (int i = 0; i < n; i++)
    for (int w = W; w >= weight[i]; w--)   // ← REVERSE
        dp[w] = Math.max(dp[w], dp[w - weight[i]] + value[i]);

// Unbounded Knapsack — reuse allowed → traverse capacity FORWARD
for (int i = 0; i < n; i++)
    for (int w = weight[i]; w <= W; w++)   // ← FORWARD
        dp[w] = Math.max(dp[w], dp[w - weight[i]] + value[i]);
```

**Rule 5 — Space optimization when dp[i] only needs dp[i-1]**
```java
// 2D → 1D rolling array
int prev2 = base0, prev1 = base1;
for (int i = 2; i <= n; i++) {
    int curr = recurrence(prev1, prev2);
    prev2 = prev1;
    prev1 = curr;
}
return prev1;
```

**Rule 6 — Interval DP loop order: by LENGTH, not by i**
```java
// WRONG — dp[i][j] might not have sub-intervals computed yet
for (int i = 0; i < n; i++) for (int j = i; j < n; j++) ...

// CORRECT — process smaller intervals first
for (int len = 2; len <= n; len++)
    for (int i = 0; i <= n - len; i++) {
        int j = i + len - 1;
        for (int k = i; k < j; k++) ...
    }
```

---

## 6. 2-Question framework

### Question 1 — What does dp[...] represent?

| State | Meaning | Used in |
|-------|---------|---------|
| `dp[i]` | Best answer for first i elements | Fibonacci, Knapsack, Decode Ways |
| `dp[i][j]` | Best for interval s[i..j] | Interval DP, Palindrome |
| `dp[i][j]` | Best matching s1[0..i] with s2[0..j] | LCS, Edit Distance |
| `dp[i][w]` | Best with i items, capacity w | Classic Knapsack |
| `dp[day][hold]` | Max profit on day, holding/not | Stock DP |
| `dp[mask]` | Best for subset in bitmask | Bitmask DP |
| `dp[node][0/1]` | Best at node, excluded/included | Tree DP |
| `dp[pos][tight]` | Count numbers at position, constrained | Digit DP |

### Question 2 — What is the recurrence?

| Pattern | Recurrence |
|---------|-----------|
| Fibonacci | `dp[i] = dp[i-1] + dp[i-2]` |
| Min/Max path | `dp[i] = min/max(dp[i-k]) + cost[i]` |
| Count ways | `dp[i] += dp[i - way[j]]` |
| 0/1 Knapsack | `dp[w] = max(dp[w], dp[w-wt]+val)` — reverse w |
| Unbounded | `dp[w] = max(dp[w], dp[w-wt]+val)` — forward w |
| LCS | match: `dp[i-1][j-1]+1` else `max(dp[i-1][j], dp[i][j-1])` |
| LIS | `dp[i] = max(dp[j]+1)` for all j<i where arr[j]<arr[i] |
| Interval | `dp[i][j] = opt over k(dp[i][k]+dp[k+1][j]+cost)` |
| Stock | `hold=max(hold, notHold-price); notHold=max(notHold, hold+price)` |
| Tree | `include[u]=val+Σexclude[v]; exclude[u]=Σmax(include[v],exclude[v])` |

---

## 7. All 14 DP patterns

---

### Pattern 1 — Fibonacci / Decision Making

**What:** At each step, choose to use or skip the current element. `f(n) = f(n-1) + f(n-2)` style.

**Recurrence:** `dp[i] = max(dp[i-1], dp[i-2] + nums[i])`

**Java template:**
```java
int prev2 = 0, prev1 = nums[0];
for (int i = 1; i < n; i++) {
    int curr = Math.max(prev1, prev2 + nums[i]);
    prev2 = prev1;
    prev1 = curr;
}
return prev1;
```

**Problems:** Climbing Stairs, House Robber, Min Cost Climbing Stairs, Maximum Subarray

---

### Pattern 2 — Minimum (Maximum) Path to Reach a Target

**What:** Given a target, find min/max cost path to reach it. Try all ways to arrive at each state.

**Recurrence:** `dp[i] = min(dp[i - way[j]]) + cost`

**Java template:**
```java
int[] dp = new int[target + 1];
Arrays.fill(dp, Integer.MAX_VALUE);
dp[0] = 0;
for (int i = 1; i <= target; i++)
    for (int way : ways)
        if (way <= i && dp[i - way] != Integer.MAX_VALUE)
            dp[i] = Math.min(dp[i], dp[i - way] + cost);
return dp[target] == Integer.MAX_VALUE ? -1 : dp[target];
```

**Problems:** Coin Change, Min Cost Climbing Stairs, Min Path Sum, Min Falling Path Sum, Triangle, Perfect Squares

---

### Pattern 3 — Distinct Ways (Counting)

**What:** Count how many distinct ways to reach a target. Sum all valid prior states.

**Recurrence:** `dp[i] += dp[i - way[j]]`

**Java template:**
```java
int[] dp = new int[target + 1];
dp[0] = 1;   // 1 way to do nothing
for (int i = 1; i <= target; i++)
    for (int way : ways)
        if (way <= i)
            dp[i] += dp[i - way];
return dp[target];
```

**Problems:** Climbing Stairs, Unique Paths, Decode Ways, Coin Change II, Number of Dice Rolls with Target Sum

---

### Pattern 4 — 0/1 Knapsack (Bounded / Take or Not Take)

**What:** Each item used AT MOST ONCE. Decide: take or skip each item.

**Recurrence:** `dp[w] = max(dp[w], dp[w - wt[i]] + val[i])` — iterate w **REVERSE**

**Java template:**
```java
int[] dp = new int[W + 1];
for (int i = 0; i < n; i++)
    for (int w = W; w >= weight[i]; w--)      // ← REVERSE = 0/1 (no reuse)
        dp[w] = Math.max(dp[w], dp[w - weight[i]] + value[i]);
return dp[W];
```

**Boolean variant (subset sum):**
```java
boolean[] dp = new boolean[target + 1];
dp[0] = true;
for (int num : nums)
    for (int w = target; w >= num; w--)
        dp[w] = dp[w] || dp[w - num];
```

**Similar problems:** Subset Sum, Partition Equal Subset Sum, Target Sum, Last Stone Weight II, Ones and Zeroes

---

### Pattern 5 — 0/1 Knapsack (Unbounded / Infinite Supply)

**What:** Each item can be used ANY number of times.

**Recurrence:** `dp[w] = max(dp[w], dp[w - wt[i]] + val[i])` — iterate w **FORWARD**

**Java template:**
```java
int[] dp = new int[W + 1];
for (int i = 0; i < n; i++)
    for (int w = weight[i]; w <= W; w++)      // ← FORWARD = reuse allowed
        dp[w] = Math.max(dp[w], dp[w - weight[i]] + value[i]);
return dp[W];
```

**Problems:** Coin Change, Coin Change II, Perfect Squares, Rod Cutting, Combination Sum IV

---

### Pattern 6 — Longest Increasing Subsequence (LIS)

**What:** Find longest strictly increasing subsequence. `dp[i]` = LIS length ending at index i.

**Recurrence:** `dp[i] = max(dp[j] + 1)` for all j < i where arr[j] < arr[i]

**Java template (O(n²)):**
```java
int[] dp = new int[n];
Arrays.fill(dp, 1);
for (int i = 1; i < n; i++)
    for (int j = 0; j < i; j++)
        if (arr[j] < arr[i])
            dp[i] = Math.max(dp[i], dp[j] + 1);
return Arrays.stream(dp).max().getAsInt();
```

**O(n log n) — Binary search on tails array:**
```java
int[] tails = new int[n]; int size = 0;
for (int num : arr) {
    int lo = 0, hi = size;
    while (lo < hi) { int mid=(lo+hi)/2; if(tails[mid]<num) lo=mid+1; else hi=mid; }
    tails[lo] = num;
    if (lo == size) size++;
}
return size;
```

**Problems:** LIS, Number of LIS, Russian Doll Envelopes, Longest Chain

---

### Pattern 7 — DP on Strings (LCS family)

**What:** Two strings s1, s2. dp[i][j] = answer for s1[0..i-1] and s2[0..j-1].

**Recurrence:**
```
if s1[i-1] == s2[j-1]:  dp[i][j] = dp[i-1][j-1] + 1  (or some formula)
else:                     dp[i][j] = combine(dp[i-1][j], dp[i][j-1])
```

**Java template:**
```java
int[][] dp = new int[n + 1][m + 1];
for (int i = 1; i <= n; i++)
    for (int j = 1; j <= m; j++)
        if (s1.charAt(i-1) == s2.charAt(j-1))
            dp[i][j] = dp[i-1][j-1] + 1;        // LCS: match
        else
            dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);  // LCS: skip
return dp[n][m];
```

**One-string variant (palindrome):**
```java
for (int len = 2; len <= n; len++)
    for (int i = 0; i <= n - len; i++) {
        int j = i + len - 1;
        if (s.charAt(i) == s.charAt(j)) dp[i][j] = dp[i+1][j-1] + 2;
        else dp[i][j] = Math.max(dp[i+1][j], dp[i][j-1]);
    }
```

**Problems:** LCS, Edit Distance, Longest Palindromic Subsequence, Distinct Subsequences, Shortest Common Supersequence, Wildcard Matching

---

### Pattern 8 — DP on Grids

**What:** Grid traversal, typically only right/down moves. dp[i][j] = answer at cell (i,j).

**Recurrence:** `dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])`

**Java template:**
```java
int[][] dp = new int[m][n];
dp[0][0] = grid[0][0];
for (int i = 1; i < m; i++) dp[i][0] = dp[i-1][0] + grid[i][0];
for (int j = 1; j < n; j++) dp[0][j] = dp[0][j-1] + grid[0][j];
for (int i = 1; i < m; i++)
    for (int j = 1; j < n; j++)
        dp[i][j] = grid[i][j] + Math.min(dp[i-1][j], dp[i][j-1]);
return dp[m-1][n-1];
```

**Problems:** Unique Paths, Unique Paths II, Min Path Sum, Min Falling Path Sum, Triangle, Dungeon Game, Maximal Square, Cherry Pickup

---

### Pattern 9 — Interval DP / Partition DP (MCM / Merging)

**What:** Optimal way to split an interval [i..j]. Try every split point k.

**Recurrence:** `dp[i][j] = optimal over k of (dp[i][k] + dp[k+1][j] + cost(i,k,j))`

**Java template:**
```java
int[][] dp = new int[n][n];
// base: dp[i][i] = single element value
for (int len = 2; len <= n; len++)
    for (int i = 0; i <= n - len; i++) {
        int j = i + len - 1;
        dp[i][j] = Integer.MAX_VALUE;
        for (int k = i; k < j; k++)
            dp[i][j] = Math.min(dp[i][j],
                dp[i][k] + dp[k+1][j] + cost(i, k, j));
    }
return dp[0][n-1];
```

**Problems:** Matrix Chain Multiplication, Burst Balloons, Remove Boxes, Merge Stones, Min Cost to Cut Stick, Strange Printer, Palindrome Partitioning II, Partition Array for Max Sum

---

### Pattern 10 — DP on Stocks

**What:** State machine — at each day, you are either holding or not holding a stock. Track states across days.

**Recurrence:**
```java
hold    = max(hold,    notHold - price);  // keep holding OR buy today
notHold = max(notHold, hold    + price);  // keep not holding OR sell today
```

**Java template:**
```java
int hold = Integer.MIN_VALUE, notHold = 0;
for (int price : prices) {
    int prevHold = hold, prevNotHold = notHold;
    hold    = Math.max(prevHold,    prevNotHold - price);
    notHold = Math.max(prevNotHold, prevHold    + price);
}
return notHold;
```

**Problems:** Best Time to Buy/Sell Stock I, II, III, IV, With Cooldown, With Transaction Fee

---

### Pattern 11 — DP on Trees

**What:** Post-order DFS. Compute dp[node] from children's dp values.

**Two states — include or exclude current node:**
```java
int[] include = new int[n];
int[] exclude = new int[n];

void dfs(int u, int parent) {
    include[u] = value[u];
    exclude[u] = 0;
    for (int v : adj[u]) {
        if (v == parent) continue;
        dfs(v, u);
        include[u] += exclude[v];                        // can't include adjacent
        exclude[u] += Math.max(include[v], exclude[v]);  // take best of child
    }
}
// answer = max(include[root], exclude[root])
```

**Problems:** House Robber III, Binary Tree Maximum Path Sum, Diameter of Binary Tree, Unique BST II, Max Independent Set in Tree

---

### Pattern 12 — Digit DP

**What:** Count integers in range [0..N] satisfying a digit-based property.

**State:** `dp[pos][count][tight]`
- `pos` = current digit position (left to right)
- `count` = current count of "interesting" digit
- `tight` = are we still bounded by N's digits? (0=free, 1=tight)

**Java template:**
```java
int[] digits = new int[maxLen];  // store digits of N
int[][][] memo = new int[maxLen][maxCount][2];

int solve(int pos, int cnt, int tight) {
    if (pos == digits.length) return cnt == target ? 1 : 0;
    if (memo[pos][cnt][tight] != -1) return memo[pos][cnt][tight];

    int limit = tight == 1 ? digits[pos] : 9;
    int res = 0;
    for (int d = 0; d <= limit; d++) {
        int newTight = (tight == 1 && d == limit) ? 1 : 0;
        int newCnt = cnt + (d == interestingDigit ? 1 : 0);
        res += solve(pos + 1, newCnt, newTight);
    }
    return memo[pos][cnt][tight] = res;
}
```

**Problems:** Count Numbers with Unique Digits, Digit One Count, Non-negative Integers without Consecutive Ones

---

### Pattern 13 — DP + Bitmask

**What:** State includes a bitmask representing a subset of elements. Used when n ≤ 20.

**Recurrence:** `dp[mask | (1 << next)][next] = min(dp[mask][curr] + cost[curr][next])`

**Java template:**
```java
int n = elements.length;
int[][] dp = new int[1 << n][n];
for (int[] row : dp) Arrays.fill(row, Integer.MAX_VALUE);

// Initialize starting states
for (int i = 0; i < n; i++) dp[1 << i][i] = 0;

for (int mask = 1; mask < (1 << n); mask++)
    for (int u = 0; u < n; u++) {
        if ((mask >> u & 1) == 0 || dp[mask][u] == Integer.MAX_VALUE) continue;
        for (int v = 0; v < n; v++) {
            if ((mask >> v & 1) == 1) continue;  // already visited
            int newMask = mask | (1 << v);
            dp[newMask][v] = Math.min(dp[newMask][v], dp[mask][u] + cost[u][v]);
        }
    }
```

**Problems:** Shortest Superstring, Number of Ways to Wear Hats, Maximum Students Taking Exam, TSP, Task Allotment

---

### Pattern 14 — Probability DP

**What:** `dp[state]` = probability or expected value at that state. Propagate probabilities forward or backward.

**Recurrence:** `dp[state] = Σ (probability_of_transition × dp[next_state])`

**Java template:**
```java
double[][] dp = new double[n][n];  // state = position (r, c)
dp[startR][startC] = 1.0;

for (int step = 0; step < k; step++) {
    double[][] next = new double[n][n];
    for (int r = 0; r < n; r++)
        for (int c = 0; c < n; c++) {
            if (dp[r][c] == 0) continue;
            for (int[] move : moves) {
                int nr = r + move[0], nc = c + move[1];
                if (nr >= 0 && nr < n && nc >= 0 && nc < n)
                    next[nr][nc] += dp[r][c] / moves.length;
            }
        }
    dp = next;
}
```

**Problems:** Knight Probability in Chessboard, Soup Servings, New 21 Game, Dice Roll Simulation, Two Boxes

---

## 8. Universal Java templates

```java
// ─── TEMPLATE A: Fibonacci / 1D Rolling ──────────────────────────────────────
int prev2 = base0, prev1 = base1;
for (int i = 2; i <= n; i++) {
    int curr = Math.max(prev1, prev2 + cost[i]);   // or + / min
    prev2 = prev1; prev1 = curr;
}
return prev1;

// ─── TEMPLATE B: Min/Max Path to Target ──────────────────────────────────────
int[] dp = new int[target + 1];
Arrays.fill(dp, Integer.MAX_VALUE); dp[0] = 0;
for (int i = 1; i <= target; i++)
    for (int way : ways)
        if (way <= i && dp[i-way] != Integer.MAX_VALUE)
            dp[i] = Math.min(dp[i], dp[i-way] + 1);
return dp[target] > target ? -1 : dp[target];

// ─── TEMPLATE C: Counting (Distinct Ways) ────────────────────────────────────
int[] dp = new int[target + 1];
dp[0] = 1;
for (int i = 1; i <= target; i++)
    for (int way : ways)
        if (way <= i) dp[i] += dp[i-way];
return dp[target];

// ─── TEMPLATE D: 0/1 Knapsack (1D, REVERSE) ──────────────────────────────────
int[] dp = new int[W + 1];
for (int i = 0; i < n; i++)
    for (int w = W; w >= weight[i]; w--)
        dp[w] = Math.max(dp[w], dp[w-weight[i]] + value[i]);
return dp[W];

// ─── TEMPLATE E: Unbounded Knapsack (1D, FORWARD) ────────────────────────────
int[] dp = new int[W + 1];
for (int i = 0; i < n; i++)
    for (int w = weight[i]; w <= W; w++)
        dp[w] = Math.max(dp[w], dp[w-weight[i]] + value[i]);
return dp[W];

// ─── TEMPLATE F: LIS O(n²) ───────────────────────────────────────────────────
int[] dp = new int[n]; Arrays.fill(dp, 1);
for (int i = 1; i < n; i++)
    for (int j = 0; j < i; j++)
        if (arr[j] < arr[i]) dp[i] = Math.max(dp[i], dp[j]+1);
return Arrays.stream(dp).max().getAsInt();

// ─── TEMPLATE G: LIS O(n log n) ──────────────────────────────────────────────
int[] tails = new int[n]; int size = 0;
for (int num : arr) {
    int lo = 0, hi = size;
    while (lo < hi) { int mid=(lo+hi)/2; if(tails[mid]<num) lo=mid+1; else hi=mid; }
    tails[lo] = num;
    if (lo == size) size++;
}
return size;

// ─── TEMPLATE H: DP on Two Strings ───────────────────────────────────────────
int[][] dp = new int[n+1][m+1];
for (int i = 1; i <= n; i++)
    for (int j = 1; j <= m; j++)
        dp[i][j] = s1.charAt(i-1)==s2.charAt(j-1)
            ? dp[i-1][j-1] + 1
            : Math.max(dp[i-1][j], dp[i][j-1]);
return dp[n][m];

// ─── TEMPLATE I: DP on Grids ─────────────────────────────────────────────────
int[][] dp = new int[m][n]; dp[0][0] = grid[0][0];
for (int i=1;i<m;i++) dp[i][0]=dp[i-1][0]+grid[i][0];
for (int j=1;j<n;j++) dp[0][j]=dp[0][j-1]+grid[0][j];
for (int i=1;i<m;i++) for (int j=1;j<n;j++)
    dp[i][j] = grid[i][j] + Math.min(dp[i-1][j], dp[i][j-1]);
return dp[m-1][n-1];

// ─── TEMPLATE J: Interval DP ─────────────────────────────────────────────────
int[][] dp = new int[n][n];
for (int len=2;len<=n;len++)
    for (int i=0;i<=n-len;i++) {
        int j=i+len-1; dp[i][j]=Integer.MAX_VALUE;
        for (int k=i;k<j;k++)
            dp[i][j]=Math.min(dp[i][j], dp[i][k]+dp[k+1][j]+cost(i,k,j));
    }
return dp[0][n-1];

// ─── TEMPLATE K: Stock DP ────────────────────────────────────────────────────
int hold=Integer.MIN_VALUE, notHold=0;
for (int price:prices) {
    int ph=hold, pn=notHold;
    hold=Math.max(ph, pn-price);
    notHold=Math.max(pn, ph+price);
}
return notHold;

// ─── TEMPLATE L: Tree DP ─────────────────────────────────────────────────────
int[] inc=new int[n], exc=new int[n];
void dfs(int u, int p) {
    inc[u]=val[u]; exc[u]=0;
    for (int v:adj[u]) { if(v==p) continue; dfs(v,u);
        inc[u]+=exc[v]; exc[u]+=Math.max(inc[v],exc[v]); }
}

// ─── TEMPLATE M: Memoization (Top-Down) ──────────────────────────────────────
int[] memo = new int[n+1]; Arrays.fill(memo,-1);
int solve(int i) {
    if (i<=0) return 0;
    if (memo[i]!=-1) return memo[i];
    return memo[i] = Math.min(solve(i-1)+cost1, solve(i-2)+cost2);
}
```

---

## 9. Quick reference cheatsheet

```
SIGNAL                                    → PATTERN            → CRITICAL CODE
──────────────────────────────────────────────────────────────────────────────────
"min/max cost to reach target"            → Min/Max Path       → dp[i]=min(dp[i-way])+cost
"count distinct ways"                     → Count Ways         → dp[i]+=dp[i-way]; dp[0]=1
"select items, each once"                 → 0/1 Knapsack       → reverse capacity
"select items, reuse allowed"             → Unbounded          → forward capacity
"partition into equal subsets"            → 0/1 Knapsack(bool) → dp[w]|=dp[w-num]
"two strings, longest common"             → LCS                → match:dp[i-1][j-1]+1
"two strings, min edit operations"        → Edit Distance       → replace/insert/delete
"longest increasing subsequence"          → LIS                → dp[i]=max(dp[j]+1)
"grid, top-left to bottom-right"          → Grid DP            → dp[i][j]=+min(up,left)
"split interval, try all split points"    → Interval DP        → len loop, k split loop
"buy sell stocks with restrictions"       → Stock DP           → hold/notHold machine
"tree nodes, no two adjacent"             → Tree DP            → include/exclude DFS
"count numbers with digit property"       → Digit DP           → pos/tight/cnt states
"assign tasks, n≤20"                     → Bitmask DP         → dp[mask|(1<<j)]
"probability / expected steps"            → Probability DP     → dp=Σ P·next
```

**3-step approach (do this before writing code):**
```
Step 1 — DEFINE:      dp[i] = ???     (exact meaning)
Step 2 — RECURRENCE:  dp[i] = f(...)  (the equation)
Step 3 — BASE CASE:   dp[0] = ?       (empty/zero state)
```

**0/1 vs Unbounded — the one thing to remember:**
```
0/1 (each item once)  → reverse:  for w = W..weight[i]
Unbounded (reuse)     → forward:  for w = weight[i]..W
```

---

## 10. Common mistakes

### Mistake 1 — dp[0] = 0 vs dp[0] = 1 (counting problems)

```java
// BUG — dp[0]=0 means 0 ways to do nothing → no ways propagate
int[] dp = new int[target+1]; dp[0] = 0; // WRONG for counting

// FIX — dp[0]=1 means 1 way to do nothing (the empty selection)
int[] dp = new int[target+1]; dp[0] = 1; // CORRECT for counting
```

### Mistake 2 — 0/1 Knapsack: forward loop allows reuse

```java
// BUG — item used multiple times
for (int w = weight[i]; w <= W; w++) dp[w] = max(...);

// FIX — reverse prevents reuse
for (int w = W; w >= weight[i]; w--) dp[w] = max(...);
```

### Mistake 3 — Integer overflow in min-initialized dp

```java
// BUG — MAX_VALUE + 1 wraps negative
dp[i] = Math.min(dp[i], dp[i-way] + 1); // if dp[i-way]=MAX_VALUE → overflow

// FIX — guard before adding
if (dp[i-way] != Integer.MAX_VALUE)
    dp[i] = Math.min(dp[i], dp[i-way] + 1);
```

### Mistake 4 — Interval DP wrong loop order

```java
// BUG — sub-intervals may not be ready
for (int i=0;i<n;i++) for (int j=i+1;j<n;j++) ...

// FIX — iterate by length (ensures sub-intervals computed first)
for (int len=2;len<=n;len++)
    for (int i=0;i<=n-len;i++) { int j=i+len-1; ... }
```

### Mistake 5 — Stock DP: using updated state in same iteration

```java
// BUG — uses new hold to compute notHold
hold    = Math.max(hold, notHold - price);
notHold = Math.max(notHold, hold + price);  // hold is already updated!

// FIX — save previous values
int ph=hold, pn=notHold;
hold    = Math.max(ph, pn - price);
notHold = Math.max(pn, ph + price);
```

### Mistake 6 — Forgetting modulo in large counting

```java
// BUG — integer overflow for large inputs
dp[i] += dp[i-way];

// FIX
dp[i] = (dp[i] + dp[i-way]) % MOD;
```

### Mistake 7 — Wrong base for Edit Distance

```java
// BUG — forgetting to initialize first row/column
int[][] dp = new int[n+1][m+1]; // all zeros — wrong!

// FIX — first row = insert all of s2; first col = delete all of s1
for (int i=0;i<=n;i++) dp[i][0]=i;
for (int j=0;j<=m;j++) dp[0][j]=j;
```

---

## 11. Complexity summary

| Pattern | Time | Space | Optimized Space |
|---------|------|-------|----------------|
| Fibonacci / 1D | O(n) | O(n) | O(1) — two variables |
| Min/Max Path | O(n × ways) | O(n) | O(n) |
| Distinct Ways | O(n × ways) | O(n) | O(n) |
| 0/1 Knapsack | O(n × W) | O(n × W) | O(W) — 1D rolling |
| Unbounded Knapsack | O(n × W) | O(W) | Already O(W) |
| LIS — O(n²) | O(n²) | O(n) | — |
| LIS — O(n log n) | O(n log n) | O(n) | — |
| DP on Strings | O(n × m) | O(n × m) | O(min(n,m)) — 1 row |
| DP on Grids | O(m × n) | O(m × n) | O(n) — single row |
| Interval DP | O(n³) | O(n²) | — |
| DP on Stocks | O(n) | O(1) | Already O(1) |
| DP on Trees | O(n) | O(n) | — |
| Digit DP | O(digits × states) | O(digits × states) | — |
| Bitmask DP | O(2^n × n) | O(2^n × n) | — only viable n ≤ 20 |
| Probability DP | O(steps × states) | O(states) | — |
