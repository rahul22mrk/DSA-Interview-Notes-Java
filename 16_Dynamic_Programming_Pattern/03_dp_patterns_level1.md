# DP Patterns Level 1 — Solved Problems (48 Problems)

> **Pattern:** Fibonacci · Min/Max Path · Distinct Ways · 0/1 Knapsack · Unbounded Knapsack · LCS · LIS · Grid DP · DP on Stocks
> **Notes:** [01_dp_notes.md](./01_dp_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Fibonacci / Decision Making
- [P1 — House Robber](#p1--house-robber)
- [P2 — Min Cost Climbing Stairs](#p2--min-cost-climbing-stairs)

### Category 2 — DP on Stocks
- [P3 — Best Time to Buy & Sell Stock I](#p3--best-time-to-buy--sell-stock-i)
- [P4 — Best Time to Buy & Sell Stock II](#p4--best-time-to-buy--sell-stock-ii)
- [P5 — Best Time with Transaction Fee](#p5--best-time-with-transaction-fee)
- [P6 — Best Time with Cooldown](#p6--best-time-with-cooldown)
- [P7 — Best Time III (at most 2 transactions)](#p7--best-time-iii-at-most-2-transactions)
- [P8 — Best Time IV (at most k transactions)](#p8--best-time-iv-at-most-k-transactions)

### Category 3 — Min/Max Path to Target
- [P9 — Coin Change](#p9--coin-change)
- [P10 — Minimum Path Sum](#p10--minimum-path-sum)
- [P11 — Minimum Falling Path Sum](#p11--minimum-falling-path-sum)
- [P12 — Triangle](#p12--triangle)
- [P13 — Perfect Squares](#p13--perfect-squares)
- [P14 — Dungeon Game](#p14--dungeon-game)
- [P15 — Ones and Zeroes](#p15--ones-and-zeroes)
- [P16 — Minimum Number of Refueling Stops](#p16--minimum-number-of-refueling-stops)

### Category 4 — Distinct Ways (Counting)
- [P17 — Climbing Stairs](#p17--climbing-stairs)
- [P18 — Unique Paths](#p18--unique-paths)
- [P19 — Unique Paths II](#p19--unique-paths-ii)
- [P20 — Decode Ways](#p20--decode-ways)
- [P21 — Coin Change II](#p21--coin-change-ii)
- [P22 — Number of Dice Rolls with Target Sum](#p22--number-of-dice-rolls-with-target-sum)
- [P23 — Target Sum](#p23--target-sum)
- [P24 — Combination Sum IV](#p24--combination-sum-iv)
- [P25 — Out of Boundary Paths](#p25--out-of-boundary-paths)
- [P26 — Domino and Tromino Tiling](#p26--domino-and-tromino-tiling)

### Category 5 — 0/1 Knapsack (Bounded)
- [P27 — 0/1 Knapsack](#p27--01-knapsack)
- [P28 — Subset Sum](#p28--subset-sum)
- [P29 — Partition Equal Subset Sum](#p29--partition-equal-subset-sum)
- [P30 — Last Stone Weight II](#p30--last-stone-weight-ii)

### Category 6 — Unbounded Knapsack (Infinite Supply)
- [P31 — Min Cost for Tickets](#p31--min-cost-for-tickets)

### Category 7 — LCS (DP on Strings)
- [P32 — Longest Common Subsequence](#p32--longest-common-subsequence)
- [P33 — Edit Distance](#p33--edit-distance)
- [P34 — Shortest Common Supersequence](#p34--shortest-common-supersequence)
- [P35 — Distinct Subsequences](#p35--distinct-subsequences)
- [P36 — Min ASCII Delete Sum](#p36--min-ascii-delete-sum)
- [P37 — Wildcard Matching](#p37--wildcard-matching)
- [P38 — Longest Palindromic Subsequence](#p38--longest-palindromic-subsequence)
- [P39 — Palindromic Substrings](#p39--palindromic-substrings)

### Category 8 — LIS (Subsequences)
- [P40 — Longest Increasing Subsequence](#p40--longest-increasing-subsequence)
- [P41 — Number of LIS](#p41--number-of-lis)
- [P42 — Largest Divisible Subset](#p42--largest-divisible-subset)
- [P43 — Max Length of Pair Chain](#p43--max-length-of-pair-chain)
- [P44 — Longest String Chain](#p44--longest-string-chain)
- [P45 — Russian Doll Envelopes](#p45--russian-doll-envelopes)

### Category 9 — DP on Grids
- [P46 — Maximal Square](#p46--maximal-square)
- [P47 — Cherry Pickup](#p47--cherry-pickup)
- [P48 — Minimum Cost Tickets (DP Array)](#p48--minimum-cost-tickets-dp-array)

---

## Category 1 — Fibonacci / Decision Making

---

### P1 — House Robber
**LeetCode #198 | Difficulty: Medium | Company: Amazon, Google**

> Rob houses in a row. No two adjacent houses. Maximize money robbed.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i]` = max money robbing 0..i | |
| Recurrence | `max(skip i: dp[i-1], take i: dp[i-2]+nums[i])` | can't rob adjacent |
| Base | `dp[0]=nums[0]`, `dp[1]=max(nums[0],nums[1])` | |
| Optimize | Two variables prev2, prev1 | O(1) space |

#### Java code

```java
public int rob(int[] nums) {
    int n = nums.length;
    if (n == 1) return nums[0];
    int prev2 = nums[0];
    int prev1 = Math.max(nums[0], nums[1]);
    for (int i = 2; i < n; i++) {
        int curr = Math.max(prev1, prev2 + nums[i]);
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```

#### Example

```
nums = [2,7,9,3,1]
prev2=2, prev1=7
i=2(9): curr=max(7,2+9)=11 → prev2=7, prev1=11
i=3(3): curr=max(11,7+3)=11 → prev2=11, prev1=11
i=4(1): curr=max(11,11+1)=12
Output: 12  (rob houses 0,2,4 → 2+9+1=12) ✓
```

---

### P2 — Min Cost Climbing Stairs
**LeetCode #746 | Difficulty: Easy | Company: Amazon**

> Pay cost[i] to step on stair i. Start from index 0 or 1. Min cost to reach top.

#### Approach table

| Step | Action |
|------|--------|
| Recurrence | `dp[i] = min(dp[i-1], dp[i-2]) + cost[i]` |
| Base | `dp[0]=cost[0]`, `dp[1]=cost[1]` |
| Answer | `min(dp[n-1], dp[n-2])` (can jump from last or second-last) |

#### Java code

```java
public int minCostClimbingStairs(int[] cost) {
    int n = cost.length;
    int prev2 = cost[0], prev1 = cost[1];
    for (int i = 2; i < n; i++) {
        int curr = Math.min(prev1, prev2) + cost[i];
        prev2 = prev1;
        prev1 = curr;
    }
    return Math.min(prev1, prev2);
}
```

#### Example

```
cost = [10,15,20]
prev2=10, prev1=15
i=2: curr=min(15,10)+20=30 → prev2=15, prev1=30
min(30,15) = 15  (step on index 1 costs 15, then jump 2 to top) ✓
```

---

## Category 2 — DP on Stocks

> **Key idea:** State machine — at each day you are either HOLDING a stock or NOT HOLDING.
> Save previous state before updating to avoid using same-day values.

---

### P3 — Best Time to Buy & Sell Stock I
**LeetCode #121 | Difficulty: Easy | Company: Amazon, Google**

> At most 1 transaction. Maximize profit.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | track `minPrice` so far | greedy, no actual dp array needed |
| Each day | `maxProfit = max(maxProfit, price - minPrice)` | sell today at best previous buy |
| Recurrence | `dp[i] = max(dp[i-1], price[i] - min(prices[0..i]))` | |

#### Java code

```java
public int maxProfit(int[] prices) {
    int minPrice = Integer.MAX_VALUE, maxProfit = 0;
    for (int price : prices) {
        minPrice = Math.min(minPrice, price);
        maxProfit = Math.max(maxProfit, price - minPrice);
    }
    return maxProfit;
}
```

#### Example

```
prices = [7,1,5,3,6,4]
minPrice tracks: 7,1,1,1,1,1
maxProfit tracks: 0,0,4,4,5,5
Output: 5 (buy at 1, sell at 6) ✓
```

---

### P4 — Best Time to Buy & Sell Stock II
**LeetCode #122 | Difficulty: Medium | Company: Amazon**

> Unlimited transactions. Maximize total profit.

#### Approach table

| State | Meaning | Transition |
|-------|---------|-----------|
| `hold` | currently holding stock | `max(hold, notHold - price)` — keep or buy |
| `notHold` | not holding stock | `max(notHold, hold + price)` — keep or sell |

> **Key:** Save previous states before updating (avoid using same-day values).

#### Java code

```java
public int maxProfit(int[] prices) {
    int hold = Integer.MIN_VALUE, notHold = 0;
    for (int price : prices) {
        int ph = hold, pn = notHold;
        hold    = Math.max(ph, pn - price);   // keep holding OR buy today
        notHold = Math.max(pn, ph + price);   // keep cash OR sell today
    }
    return notHold;
}
```

#### Example

```
prices = [7,1,5,3,6,4]
Day1(7): hold=max(MIN,-7)=-7, notHold=0
Day2(1): hold=max(-7,0-1)=-1, notHold=max(0,-7+1)=0
Day3(5): hold=max(-1,0-5)=-1, notHold=max(0,-1+5)=4
Day4(3): hold=max(-1,4-3)=1, notHold=max(4,-1+3)=4
Day5(6): hold=max(1,4-6)=1, notHold=max(4,1+6)=7
Output: 7 ✓
```

---

### P5 — Best Time with Transaction Fee
**LeetCode #714 | Difficulty: Medium | Company: Google**

> Unlimited transactions but pay fee on each sell.

#### Approach table

| State | Meaning | Transition |
|-------|---------|-----------|
| `hold` | holding stock | `max(hold, notHold - price)` |
| `notHold` | not holding | `max(notHold, hold + price - fee)` — fee on sell |

#### Java code

```java
public int maxProfit(int[] prices, int fee) {
    int hold = Integer.MIN_VALUE, notHold = 0;
    for (int price : prices) {
        int ph = hold, pn = notHold;
        hold    = Math.max(ph, pn - price);
        notHold = Math.max(pn, ph + price - fee);  // fee deducted on sell
    }
    return notHold;
}
```

#### Example

```
prices=[1,3,2,8,4,9], fee=2
Day1(1): hold=-1, notHold=0
Day2(3): hold=-1, notHold=max(0,-1+3-2)=0
Day3(2): hold=max(-1,0-2)=-1, notHold=0
Day4(8): hold=-1, notHold=max(0,-1+8-2)=5
Day5(4): hold=max(-1,5-4)=1, notHold=max(5,-1+4-2)=5
Day6(9): hold=1, notHold=max(5,1+9-2)=8
Output: 8 ✓
```

---

### P6 — Best Time with Cooldown
**LeetCode #309 | Difficulty: Medium | Company: Amazon**

> After selling, must rest 1 day (cooldown) before buying again.

#### Approach table

| State | Meaning | Transition |
|-------|---------|-----------|
| hold | holding stock | `max(hold, cooldown - price)` — buy only from cooldown |
| notHold | not holding, not cooldown | `max(notHold, cooldown)` |
| cooldown | just sold | `hold + price` |

#### Java code

```java
public int maxProfit(int[] prices) {
    int hold = Integer.MIN_VALUE, notHold = 0, cooldown = 0;
    for (int price : prices) {
        int ph = hold, pn = notHold, pc = cooldown;
        hold     = Math.max(ph, pc - price);    // buy only after cooldown
        notHold  = Math.max(pn, pc);            // rest or stay
        cooldown = ph + price;                  // sold today → enter cooldown
    }
    return Math.max(notHold, cooldown);
}
```

#### Example

```
prices = [1,2,3,0,2]
Day1(1): hold=-1, notHold=0, cooldown=0
Day2(2): hold=max(-1,0-2)=-1, notHold=0, cooldown=-1+2=1
Day3(3): hold=max(-1,1-3)=-1, notHold=max(0,1)=1, cooldown=-1+3=2
Day4(0): hold=max(-1,2-0)=2, notHold=max(1,2)=2, cooldown=-1+0=-1
Day5(2): hold=max(2,-1-2)=2, notHold=max(2,-1)=2, cooldown=2+2=4
max(2,4)=4 ✓
```

---

### P7 — Best Time III (at most 2 transactions)
**LeetCode #123 | Difficulty: Hard | Company: Amazon, Google**

> At most 2 complete transactions.

#### Approach table

| State | Meaning | Transition |
|-------|---------|-----------|
| `buy1` | max profit after 1st buy | `max(buy1, -price)` |
| `sell1` | max profit after 1st sell | `max(sell1, buy1 + price)` |
| `buy2` | max profit after 2nd buy | `max(buy2, sell1 - price)` |
| `sell2` | max profit after 2nd sell | `max(sell2, buy2 + price)` |

#### Java code

```java
public int maxProfit(int[] prices) {
    int buy1 = Integer.MIN_VALUE, sell1 = 0;
    int buy2 = Integer.MIN_VALUE, sell2 = 0;
    for (int price : prices) {
        buy1  = Math.max(buy1,  -price);           // first buy
        sell1 = Math.max(sell1, buy1 + price);     // first sell
        buy2  = Math.max(buy2,  sell1 - price);    // second buy (use profit from sell1)
        sell2 = Math.max(sell2, buy2 + price);     // second sell
    }
    return sell2;
}
```

#### Example

```
prices = [3,3,5,0,0,3,1,4]
Tracing buy1,sell1,buy2,sell2:
Final: buy1=-0, sell1=3, buy2=3, sell2=6
Output: 6 (buy at 0, sell at 3; buy at 1, sell at 4) ✓
```

---

### P8 — Best Time IV (at most k transactions)
**LeetCode #188 | Difficulty: Hard | Company: Amazon**

> At most k complete transactions.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| If `k >= n/2` | treat as unlimited | greedy sum of gains |
| Arrays | `buy[k]`, `sell[k]` | one entry per transaction |
| Each price | update buy[j] then sell[j] for all j | chain: sell[j-1] funds buy[j] |
| State | `buy[j] = max(buy[j], sell[j-1] - price)` | |
| State | `sell[j] = max(sell[j], buy[j] + price)` | |

#### Java code

```java
public int maxProfit(int k, int[] prices) {
    int n = prices.length;
    if (n == 0 || k == 0) return 0;
    if (k >= n / 2) {   // unlimited effectively
        int profit = 0;
        for (int i = 1; i < n; i++) profit += Math.max(0, prices[i] - prices[i-1]);
        return profit;
    }
    int[] buy  = new int[k]; Arrays.fill(buy,  Integer.MIN_VALUE);
    int[] sell = new int[k];
    for (int price : prices) {
        buy[0]  = Math.max(buy[0],  -price);
        sell[0] = Math.max(sell[0], buy[0] + price);
        for (int j = 1; j < k; j++) {
            buy[j]  = Math.max(buy[j],  sell[j-1] - price);
            sell[j] = Math.max(sell[j], buy[j]    + price);
        }
    }
    return sell[k - 1];
}
```

#### Example

```
prices=[2,4,1,5], k=2
buy=[MIN,MIN], sell=[0,0]
price=2: buy=[−2,MIN], sell=[0,0]
price=4: buy=[−2,MIN], sell=[2,0] → buy[1]=max(MIN,2-4)=−2, sell[1]=0
price=1: buy=[−1,−2], sell=[2,0] → buy[1]=max(−2,2-1)=1? wait: sell[0]=2, buy[1]=max(−2,2-1)=1
price=5: buy=[−1,1], sell=[4,6]
Output: sell[1]=6 ✓
```

---

## Category 3 — Min/Max Path to Target

> **Key idea:** `dp[i] = min(dp[i - way]) + cost` for each valid way to arrive at i.
> Init dp with MAX_VALUE (except dp[0]=0). Return -1 if unreachable.

---

### P9 — Coin Change
**LeetCode #322 | Difficulty: Medium | Company: Amazon, Google**

> Min coins to make amount. Coins reusable → Unbounded Knapsack.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i]` = min coins to make amount i | |
| Init | `dp[0]=0`, rest = `amount+1` (infinity) | |
| Recurrence | `dp[i] = min(dp[i], dp[i-coin]+1)` for each coin | forward loop — reuse |
| Answer | `dp[amount]` if ≤ amount, else -1 | |

#### Java code

```java
public int coinChange(int[] coins, int amount) {
    int[] dp = new int[amount + 1];
    Arrays.fill(dp, amount + 1);    // init with "impossible" value
    dp[0] = 0;
    for (int i = 1; i <= amount; i++)
        for (int coin : coins)
            if (coin <= i)
                dp[i] = Math.min(dp[i], dp[i - coin] + 1);
    return dp[amount] > amount ? -1 : dp[amount];
}
```

#### Example

```
coins=[1,5,11], amount=15
dp[5]=1, dp[10]=2, dp[11]=1
dp[15]=min(dp[14]+1, dp[10]+1, dp[4]+1)
dp[10]+1 = 3  →  5+5+5
Output: 3 ✓
```

---

### P10 — Minimum Path Sum
**LeetCode #64 | Difficulty: Medium | Company: Amazon, Google**

> Min sum from top-left to bottom-right. Move right or down only.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Base | First row/col = prefix sums | only one direction possible |
| Recurrence | `dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])` | from top or left |
| Answer | `dp[m-1][n-1]` | |

#### Java code

```java
public int minPathSum(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int[][] dp = new int[m][n];
    dp[0][0] = grid[0][0];
    for (int i = 1; i < m; i++) dp[i][0] = dp[i-1][0] + grid[i][0];
    for (int j = 1; j < n; j++) dp[0][j] = dp[0][j-1] + grid[0][j];
    for (int i = 1; i < m; i++)
        for (int j = 1; j < n; j++)
            dp[i][j] = grid[i][j] + Math.min(dp[i-1][j], dp[i][j-1]);
    return dp[m-1][n-1];
}
```

#### Example

```
grid=[[1,3,1],[1,5,1],[4,2,1]]
dp: [1,4,5]
    [2,7,6]
    [6,8,7]
Output: 7 (1→3→1→1→1) ✓
```

---

### P11 — Minimum Falling Path Sum
**LeetCode #931 | Difficulty: Medium | Company: Google**

> Fall from top row to bottom row. Each step can move to adjacent column (±1) or same.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Base | `dp[0] = matrix[0]` (top row as-is) | |
| Recurrence | `dp[i][j] = matrix[i][j] + min(dp[i-1][j-1], dp[i-1][j], dp[i-1][j+1])` | 3 choices |
| Answer | `min(dp[n-1])` | minimum of last row |

#### Java code

```java
public int minFallingPathSum(int[][] matrix) {
    int n = matrix.length;
    int[][] dp = new int[n][n];
    dp[0] = matrix[0].clone();
    for (int i = 1; i < n; i++)
        for (int j = 0; j < n; j++) {
            int best = dp[i-1][j];
            if (j > 0)   best = Math.min(best, dp[i-1][j-1]);
            if (j < n-1) best = Math.min(best, dp[i-1][j+1]);
            dp[i][j] = matrix[i][j] + best;
        }
    int min = Integer.MAX_VALUE;
    for (int x : dp[n-1]) min = Math.min(min, x);
    return min;
}
```

#### Example

```
matrix=[[2,1,3],[6,5,4],[7,8,9]]
dp[0]=[2,1,3]
dp[1]=[2+1,5+1,4+1]=[3,6,5]  (j=0:min(2,1)=1; j=1:min(2,1,3)=1; j=2:min(1,3)=1)
dp[2]=[7+3,8+3,9+5]=[10,11,14]
min=10 ✓
```

---

### P12 — Triangle
**LeetCode #120 | Difficulty: Medium | Company: Amazon**

> Min path sum from top to bottom of triangle. Move to adjacent index below.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Direction | Bottom-up (last row → first row) | avoids boundary issues |
| Base | `dp = last row` | |
| Recurrence | `dp[j] = triangle[i][j] + min(dp[j], dp[j+1])` | pick better of two below |
| Answer | `dp[0]` | |

#### Java code

```java
public int minimumTotal(List<List<Integer>> triangle) {
    int n = triangle.size();
    int[] dp = new int[n];
    // start from bottom row
    for (int i = 0; i < n; i++) dp[i] = triangle.get(n-1).get(i);
    // work upward
    for (int i = n-2; i >= 0; i--)
        for (int j = 0; j <= i; j++)
            dp[j] = triangle.get(i).get(j) + Math.min(dp[j], dp[j+1]);
    return dp[0];
}
```

#### Example

```
triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]
Bottom row dp = [4,1,8,3]
i=2: dp[0]=6+min(4,1)=7, dp[1]=5+min(1,8)=6, dp[2]=7+min(8,3)=10
i=1: dp[0]=3+min(7,6)=9, dp[1]=4+min(6,10)=10
i=0: dp[0]=2+min(9,10)=11
Output: 11 ✓
```

---

### P13 — Perfect Squares
**LeetCode #279 | Difficulty: Medium | Company: Google**

> Min number of perfect squares that sum to n.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i]` = min perfect squares to sum to i | |
| Init | `dp[0]=0`, rest = `n+1` (infinity) | |
| Recurrence | for each j where j²≤i: `dp[i] = min(dp[i], dp[i-j²]+1)` | |
| Answer | `dp[n]` | |

#### Java code

```java
public int numSquares(int n) {
    int[] dp = new int[n + 1];
    Arrays.fill(dp, n + 1);
    dp[0] = 0;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j * j <= i; j++)
            dp[i] = Math.min(dp[i], dp[i - j*j] + 1);
    return dp[n];
}
```

#### Example

```
n=12
squares: 1,4,9
dp[4]=1(4), dp[8]=2(4+4), dp[9]=1(9), dp[12]=min(dp[11]+1,dp[8]+1,dp[3]+1)
dp[8]+1=3 → 4+4+4
Output: 3 ✓
```

---

### P14 — Dungeon Game
**LeetCode #174 | Difficulty: Hard | Company: Amazon**

> Knight starts at top-left, rescue princess at bottom-right. Min initial health needed.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Direction | Backward: bottom-right → top-left | forward DP doesn't work here |
| Base | `dp[m-1][n-1] = max(1 - dungeon[m-1][n-1], 1)` | need at least 1 HP |
| Recurrence | `dp[i][j] = max(min(dp[i+1][j], dp[i][j+1]) - dungeon[i][j], 1)` | at least 1 HP |
| Answer | `dp[0][0]` | min health at start |

#### Java code

```java
public int calculateMinimumHP(int[][] dungeon) {
    int m = dungeon.length, n = dungeon[0].length;
    int[][] dp = new int[m][n];
    // base: bottom-right
    dp[m-1][n-1] = Math.max(1 - dungeon[m-1][n-1], 1);
    // last column (can only go down)
    for (int i = m-2; i >= 0; i--)
        dp[i][n-1] = Math.max(dp[i+1][n-1] - dungeon[i][n-1], 1);
    // last row (can only go right)
    for (int j = n-2; j >= 0; j--)
        dp[m-1][j] = Math.max(dp[m-1][j+1] - dungeon[m-1][j], 1);
    // fill backwards
    for (int i = m-2; i >= 0; i--)
        for (int j = n-2; j >= 0; j--) {
            int minNext = Math.min(dp[i+1][j], dp[i][j+1]);
            dp[i][j] = Math.max(minNext - dungeon[i][j], 1);
        }
    return dp[0][0];
}
```

#### Example

```
dungeon=[[-2,-3,3],[-5,-10,1],[10,30,-5]]
dp[2][2]=max(1-(-5),1)=6
dp[2][1]=max(6-30,1)=1
dp[2][0]=max(1-10,1)=1
dp[1][2]=max(6-1,1)=5
dp[0][2]=max(5-3,1)=2
dp[1][1]=max(min(1,5)-(-10),1)=11
dp[1][0]=max(min(11,1)-(-5),1)=6
dp[0][1]=max(min(11,2)-(-3),1)=5
dp[0][0]=max(min(6,5)-(-2),1)=7
Output: 7 ✓
```

---

### P15 — Ones and Zeroes
**LeetCode #474 | Difficulty: Medium | Company: Google**

> Max strings in subset with at most m zeros and n ones. 2D Knapsack.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i][j]` = max strings using i zeros and j ones | 2D knapsack |
| Loop | Reverse both i and j dimensions | 0/1 — each string used once |
| Recurrence | `dp[i][j] = max(dp[i][j], dp[i-zeros][j-ones] + 1)` | |

#### Java code

```java
public int findMaxForm(String[] strs, int m, int n) {
    int[][] dp = new int[m+1][n+1];
    for (String s : strs) {
        int zeros = 0, ones = 0;
        for (char c : s.toCharArray()) { if (c=='0') zeros++; else ones++; }
        for (int i = m; i >= zeros; i--)       // REVERSE both dims — 0/1
            for (int j = n; j >= ones; j--)
                dp[i][j] = Math.max(dp[i][j], dp[i-zeros][j-ones] + 1);
    }
    return dp[m][n];
}
```

#### Example

```
strs=["10","0001","111001","1","0"], m=5, n=3
"10"  (1z,1o): dp[1][1]=1, dp[2][2]=1...
"0001"(3z,1o): dp[3][1]=1, ...
...
dp[5][3]=4 ✓
```

---

### P16 — Minimum Number of Refueling Stops
**LeetCode #871 | Difficulty: Hard | Company: Google**

> Car starts at 0 with `startFuel`. `dp[t]` = max distance reachable with exactly t refueling stops.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[t]` = max distance reachable using exactly t stops | |
| Loop | Outer: stations. Inner: **REVERSE** t from i to 0 | 0/1 style |
| Recurrence | if `dp[t] >= station pos`: `dp[t+1] = max(dp[t+1], dp[t]+station fuel)` | |
| Answer | first t where `dp[t] >= target` | |

#### Java code

```java
public int minRefuelStops(int target, int startFuel, int[][] stations) {
    int n = stations.length;
    long[] dp = new long[n + 1];
    dp[0] = startFuel;
    for (int i = 0; i < n; i++)
        for (int t = i; t >= 0; t--)        // REVERSE — 0/1 style
            if (dp[t] >= stations[i][0])    // can reach station i with t stops
                dp[t+1] = Math.max(dp[t+1], dp[t] + stations[i][1]);
    for (int t = 0; t <= n; t++)
        if (dp[t] >= target) return t;
    return -1;
}
```

#### Example

```
target=100, startFuel=10, stations=[[10,60],[20,30],[30,30],[60,40]]
dp[0]=10
Station(10,60): dp[0]>=10 → dp[1]=max(0,10+60)=70
Station(20,30): dp[0]<20 skip; dp[1]=70>=20 → dp[2]=max(0,70+30)=100
dp[2]=100>=100 → return 2 ✓
```

---

## Category 4 — Distinct Ways (Counting)

> **Key idea:** `dp[i] += dp[i - way]` for each valid way. **dp[0] = 1** (1 way to do nothing).

---

### P17 — Climbing Stairs
**LeetCode #70 | Difficulty: Easy | Company: Amazon**

> Count distinct ways to climb n stairs (1 or 2 steps at a time).

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i]` = ways to reach step i | |
| Recurrence | `dp[i] = dp[i-1] + dp[i-2]` | come from 1 step below or 2 |
| Base | `dp[1]=1, dp[2]=2` | |

#### Java code

```java
public int climbStairs(int n) {
    if (n <= 2) return n;
    int prev2 = 1, prev1 = 2;
    for (int i = 3; i <= n; i++) {
        int curr = prev1 + prev2;
        prev2 = prev1; prev1 = curr;
    }
    return prev1;
}
```

#### Example

```
n=5: 1,2,3,5,8
Output: 8 ✓
```

---

### P18 — Unique Paths
**LeetCode #62 | Difficulty: Medium | Company: Amazon**

> Count paths from top-left to bottom-right (only right or down).

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Base | All first row/col = 1 | only one way to reach edge cells |
| Recurrence | `dp[i][j] = dp[i-1][j] + dp[i][j-1]` | from top or left |
| Answer | `dp[m-1][n-1]` | |

#### Java code

```java
public int uniquePaths(int m, int n) {
    int[][] dp = new int[m][n];
    for (int i = 0; i < m; i++) dp[i][0] = 1;
    for (int j = 0; j < n; j++) dp[0][j] = 1;
    for (int i = 1; i < m; i++)
        for (int j = 1; j < n; j++)
            dp[i][j] = dp[i-1][j] + dp[i][j-1];
    return dp[m-1][n-1];
}
```

#### Example

```
m=3,n=7 → dp[2][6]=28 ✓
```

---

### P19 — Unique Paths II
**LeetCode #63 | Difficulty: Medium | Company: Amazon**

> Same as Unique Paths but some cells are obstacles (1=obstacle).

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Base | First row/col: fill 1 until obstacle, then 0 | obstacle blocks all further |
| Recurrence | if obstacle: `dp[i][j]=0`; else `dp[i-1][j]+dp[i][j-1]` | |

#### Java code

```java
public int uniquePathsWithObstacles(int[][] obstacleGrid) {
    int m = obstacleGrid.length, n = obstacleGrid[0].length;
    if (obstacleGrid[0][0] == 1 || obstacleGrid[m-1][n-1] == 1) return 0;
    int[][] dp = new int[m][n];
    for (int i = 0; i < m && obstacleGrid[i][0] == 0; i++) dp[i][0] = 1;
    for (int j = 0; j < n && obstacleGrid[0][j] == 0; j++) dp[0][j] = 1;
    for (int i = 1; i < m; i++)
        for (int j = 1; j < n; j++)
            if (obstacleGrid[i][j] == 0)
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
    return dp[m-1][n-1];
}
```

#### Example

```
obstacleGrid=[[0,0,0],[0,1,0],[0,0,0]]
dp[0]=[1,1,1]
dp[1]: j=0→1, j=1 obstacle→0, j=2: dp[0][2]+dp[1][1]=1+0=1
dp[2]: j=0→1, j=1: dp[1][1]+dp[2][0]=0+1=1, j=2: dp[1][2]+dp[2][1]=1+1=2
Output: 2 ✓
```

---

### P20 — Decode Ways
**LeetCode #91 | Difficulty: Medium | Company: Facebook, Amazon**

> '1'=A .. '26'=Z. Count distinct decodings of digit string.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Base | `dp[0]=1` (empty), `dp[1]=0 if s[0]=='0' else 1` | |
| 1-digit | if `s[i-1]≠'0'`: `dp[i] += dp[i-1]` | single char decode |
| 2-digit | if `10 ≤ s[i-2..i-1] ≤ 26`: `dp[i] += dp[i-2]` | two-char decode |

#### Java code

```java
public int numDecodings(String s) {
    int n = s.length();
    int[] dp = new int[n + 1];
    dp[0] = 1;
    dp[1] = s.charAt(0) == '0' ? 0 : 1;
    for (int i = 2; i <= n; i++) {
        int one = s.charAt(i-1) - '0';
        int two = Integer.parseInt(s.substring(i-2, i));
        if (one != 0) dp[i] += dp[i-1];
        if (two >= 10 && two <= 26) dp[i] += dp[i-2];
    }
    return dp[n];
}
```

#### Example

```
s="226"
dp[0]=1, dp[1]=1
i=2: one=2≠0→dp[2]+=dp[1]=1; two=22∈[10,26]→dp[2]+=dp[0]=1 → dp[2]=2
i=3: one=6≠0→dp[3]+=dp[2]=2; two=26∈[10,26]→dp[3]+=dp[1]=1 → dp[3]=3
Output: 3  (2|2|6, 22|6, 2|26) ✓
```

---

### P21 — Coin Change II
**LeetCode #518 | Difficulty: Medium | Company: Amazon**

> Count ways to make amount. Coins reusable → Unbounded Knapsack (forward loop).

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[w]` = number of ways to make amount w | |
| Base | `dp[0]=1` | 1 way to make 0 (use nothing) |
| Loop | Outer: coins. Inner: FORWARD `w` from coin to amount | unbounded — reuse |
| Recurrence | `dp[w] += dp[w - coin]` | |

#### Java code

```java
public int change(int amount, int[] coins) {
    int[] dp = new int[amount + 1];
    dp[0] = 1;
    for (int coin : coins)
        for (int w = coin; w <= amount; w++)    // FORWARD — reuse allowed
            dp[w] += dp[w - coin];
    return dp[amount];
}
```

#### Example

```
amount=5, coins=[1,2,5]
coin=1: dp=[1,1,1,1,1,1]
coin=2: dp=[1,1,2,2,3,3]
coin=5: dp=[1,1,2,2,3,4]
Output: 4 ✓
```

---

### P22 — Number of Dice Rolls with Target Sum
**LeetCode #1155 | Difficulty: Medium**

> d dice each with f faces (1..f). Count ways to get exactly target.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i]` = ways to reach sum i with dice rolled so far | |
| Each die | Create `next[]` fresh each round | avoid reusing same die |
| Recurrence | `next[i] += dp[i - face]` for face in 1..f | |

#### Java code

```java
public int numRollsToTarget(int d, int f, int target) {
    int MOD = 1_000_000_007;
    int[] dp = new int[target + 1];
    dp[0] = 1;
    for (int rep = 0; rep < d; rep++) {
        int[] next = new int[target + 1];
        for (int i = 1; i <= target; i++)
            for (int face = 1; face <= f && face <= i; face++)
                next[i] = (next[i] + dp[i - face]) % MOD;
        dp = next;
    }
    return dp[target];
}
```

#### Example

```
d=2,f=6,target=7
After die1: dp=[0,1,1,1,1,1,1]  (can reach 1..6)
After die2: dp[7]=dp2[7]=sum(dp[1..6])=6
Output: 6 ✓
```

---

### P23 — Target Sum
**LeetCode #494 | Difficulty: Medium | Company: Facebook, Amazon**

> Assign + or − to each number. Count ways to get target.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Convert | `sum = (total + target) / 2` | count subsets summing to `sum` |
| Check | `(total+target)%2 != 0` → return 0 | impossible |
| State | `dp[w]` = count of subsets summing to w | |
| Loop | REVERSE — 0/1 knapsack | each number used once |

#### Java code

```java
public int findTargetSumWays(int[] nums, int target) {
    int total = 0;
    for (int n : nums) total += n;
    if (Math.abs(target) > total || (target + total) % 2 != 0) return 0;
    int sum = (target + total) / 2;
    int[] dp = new int[sum + 1];
    dp[0] = 1;
    for (int num : nums)
        for (int w = sum; w >= num; w--)   // REVERSE — 0/1
            dp[w] += dp[w - num];
    return dp[sum];
}
```

#### Example

```
nums=[1,1,1,1,1], target=3
total=5, sum=(3+5)/2=4
After 5 ones: dp[4]=5
Output: 5 ✓
```

---

### P24 — Combination Sum IV
**LeetCode #377 | Difficulty: Medium | Company: Google**

> Count ordered sequences (order matters!) that sum to target.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i]` = ordered ways to reach sum i | |
| Loop | Outer: **target** i (1..target). Inner: all nums | order matters → target outer |
| Recurrence | `dp[i] += dp[i - num]` for each valid num | |

#### Java code

```java
public int combinationSum4(int[] nums, int target) {
    int[] dp = new int[target + 1];
    dp[0] = 1;
    for (int i = 1; i <= target; i++)
        for (int num : nums)
            if (num <= i)
                dp[i] += dp[i - num];
    return dp[target];
}
```

#### Example

```
nums=[1,2,3], target=4
dp[1]=1(1), dp[2]=2(1+1,2), dp[3]=4(1+1+1,1+2,2+1,3)
dp[4]=dp[3]+dp[2]+dp[1]=4+2+1=7
Output: 7 ✓
```

---

### P25 — Out of Boundary Paths
**LeetCode #576 | Difficulty: Medium | Company: Google**

> m×n grid. Ball starts at (startRow,startCol). Count ways to exit boundary in ≤ maxMove steps.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[r][c]` = ways to be at (r,c) after current step | |
| Each step | Create `next[][]` fresh; count exits | |
| Transition | 4 neighbors: if in bounds add to `next`; if out add to `count` | |

#### Java code

```java
public int findPaths(int m, int n, int maxMove, int startRow, int startCol) {
    int MOD = 1_000_000_007;
    int[][] dp = new int[m][n];
    dp[startRow][startCol] = 1;
    int count = 0;
    int[] dr = {0,0,1,-1}, dc = {1,-1,0,0};
    for (int move = 0; move < maxMove; move++) {
        int[][] next = new int[m][n];
        for (int r = 0; r < m; r++)
            for (int c = 0; c < n; c++) {
                if (dp[r][c] == 0) continue;
                for (int d = 0; d < 4; d++) {
                    int nr = r+dr[d], nc = c+dc[d];
                    if (nr<0||nr>=m||nc<0||nc>=n) count = (count+dp[r][c])%MOD;
                    else next[nr][nc] = (next[nr][nc]+dp[r][c])%MOD;
                }
            }
        dp = next;
    }
    return count;
}
```

#### Example

```
m=2,n=2, maxMove=2, start=(0,0)
Move1: from (0,0) → exits: left(-1,0) and up(0,-1) → count+=2; next[(0,1)]=1, next[(1,0)]=1
Move2: from (0,1): exits up+right=2→count+=2; from (1,0): exits left+down=2→count+=2
Total count = 2+2+2 = 6 ✓
```

---

### P26 — Domino and Tromino Tiling
**LeetCode #790 | Difficulty: Medium**

> Count ways to tile 2×n board with dominoes and trominoes.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Recurrence | `dp[n] = 2*dp[n-1] + dp[n-3]` | derived from tiling patterns |
| Base | `dp[0]=1, dp[1]=1, dp[2]=2` | |
| Key insight | Each new column: add vertical domino OR combine with previous | |

#### Java code

```java
public int numTilings(int n) {
    int MOD = 1_000_000_007;
    if (n <= 2) return n;
    long[] dp = new long[n + 1];
    dp[0] = 1; dp[1] = 1; dp[2] = 2;
    for (int i = 3; i <= n; i++)
        dp[i] = (2 * dp[i-1] + dp[i-3]) % MOD;
    return (int) dp[n];
}
```

#### Example

```
n=3: dp[3]=2*dp[2]+dp[0]=2*2+1=5
Output: 5 ✓
```

---

## Category 5 — 0/1 Knapsack (Bounded)

> **Key:** Each item used AT MOST ONCE → iterate capacity **REVERSE**.

---

### P27 — 0/1 Knapsack
**GFG | Difficulty: Medium | Company: Amazon**

> Given items with weights and values, fill knapsack of capacity W. Each item used at most once.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[w]` = max value with capacity w | 1D space-optimized |
| Loop | Outer: items. Inner: **REVERSE** w from W to weight[i] | 0/1 — each item once |
| Recurrence | `dp[w] = max(dp[w], dp[w-weight[i]] + value[i])` | take or skip |

#### Java code

```java
public int knapsack(int[] weight, int[] value, int n, int W) {
    int[] dp = new int[W + 1];
    for (int i = 0; i < n; i++)
        for (int w = W; w >= weight[i]; w--)    // ← REVERSE = each item once
            dp[w] = Math.max(dp[w], dp[w - weight[i]] + value[i]);
    return dp[W];
}
```

#### Example

```
weight=[1,3,4,5], value=[1,4,5,7], W=7
After item0(w=1,v=1): dp[1..7]=1
After item1(w=3,v=4): dp[3]=5,dp[4]=5,dp[5]=5,dp[6]=5,dp[7]=5
After item2(w=4,v=5): dp[4]=6,dp[5]=6,dp[6]=9,dp[7]=9
After item3(w=5,v=7): dp[5]=8,dp[6]=9,dp[7]=9
Output: 9 (items 1+2: weight 3+4=7, value 4+5=9) ✓
```

---

### P28 — Subset Sum
**GFG | Difficulty: Medium**

> Can we find a subset with sum = target?

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[w]` = true if sum w is achievable | boolean 0/1 knapsack |
| Loop | Outer: nums. Inner: **REVERSE** w (W down to num) | each num used once |
| Recurrence | `dp[w] |= dp[w - num]` | |

#### Java code

```java
public boolean subsetSum(int[] nums, int target) {
    boolean[] dp = new boolean[target + 1];
    dp[0] = true;
    for (int num : nums)
        for (int w = target; w >= num; w--)    // ← REVERSE
            dp[w] = dp[w] || dp[w - num];
    return dp[target];
}
```

#### Example

```
nums=[3,34,4,12,5,2], target=9
dp[3]=true, dp[4]=true, dp[7]=true, dp[9]=true (3+4+2 or 4+5)
Output: true ✓
```

---

### P29 — Partition Equal Subset Sum
**LeetCode #416 | Difficulty: Medium | Company: Amazon, Facebook**

> Can we split array into 2 equal-sum subsets? Reduce to: subset sum = total/2.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Check | if `total % 2 != 0` → false (odd total can't split) | |
| Reduce to | Subset Sum with target = `total/2` | |
| State | `dp[w]` = true if achievable | boolean knapsack |
| Loop | REVERSE w | 0/1 |

#### Java code

```java
public boolean canPartition(int[] nums) {
    int total = 0;
    for (int n : nums) total += n;
    if (total % 2 != 0) return false;
    int target = total / 2;
    boolean[] dp = new boolean[target + 1];
    dp[0] = true;
    for (int num : nums)
        for (int w = target; w >= num; w--)
            dp[w] = dp[w] || dp[w - num];
    return dp[target];
}
```

#### Example

```
nums=[1,5,11,5], total=22, target=11
num=1: dp[1]=true
num=5: dp[6]=true, dp[5]=true
num=11: dp[11]=true
Output: true ({11} and {1,5,5}) ✓
```

---

### P30 — Last Stone Weight II
**LeetCode #1049 | Difficulty: Medium | Company: Google**

> Minimize last stone. Partition into 2 groups, minimize |S1-S2|. Find largest subset ≤ total/2.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Insight | min|S1-S2| = total - 2*maxS1 where S1 ≤ total/2 | |
| State | `dp[w]` = true if sum w achievable | boolean knapsack |
| Loop | REVERSE w | 0/1 |
| Answer | `total - 2 * (largest w ≤ total/2 where dp[w]=true)` | |

#### Java code

```java
public int lastStoneWeightII(int[] stones) {
    int total = 0;
    for (int s : stones) total += s;
    int target = total / 2;
    boolean[] dp = new boolean[target + 1];
    dp[0] = true;
    for (int stone : stones)
        for (int w = target; w >= stone; w--)
            dp[w] = dp[w] || dp[w - stone];
    for (int w = target; w >= 0; w--)
        if (dp[w]) return total - 2 * w;
    return 0;
}
```

#### Example

```
stones=[2,7,4,1,8,1], total=23, target=11
Achievable sums up to 11: all up to 11
w=11 achievable → return 23-22=1 ✓
```

---

## Category 6 — Unbounded Knapsack

---

### P31 — Min Cost for Tickets
**LeetCode #983 | Difficulty: Medium | Company: Google**

> 3 pass types: 1-day, 7-day, 30-day. Min cost to cover all travel days.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i]` = min cost to cover days up to day i | |
| Non-travel day | `dp[i] = dp[i-1]` | no cost |
| Travel day | `min(dp[i-1]+c[0], dp[max(0,i-7)]+c[1], dp[max(0,i-30)]+c[2])` | |

#### Java code

```java
public int mincostTickets(int[] days, int[] costs) {
    int last = days[days.length - 1];
    int[] dp = new int[last + 1];
    Set<Integer> travelDays = new HashSet<>();
    for (int d : days) travelDays.add(d);

    for (int i = 1; i <= last; i++) {
        if (!travelDays.contains(i)) { dp[i] = dp[i-1]; continue; }
        dp[i] = Math.min(dp[i-1]  + costs[0],              // 1-day pass
                Math.min(dp[Math.max(0,i-7)]  + costs[1],  // 7-day pass
                         dp[Math.max(0,i-30)] + costs[2]));// 30-day pass
    }
    return dp[last];
}
```

#### Example

```
days=[1,4,6,7,8,20], costs=[2,7,15]
dp[1]=min(0+2, 0+7, 0+15)=2
dp[4]=min(dp[3]+2, dp[0]+7, 0+15)=min(4,7,15)=4... trace to dp[20]=11
Output: 11 ✓
```

---

## Category 7 — LCS (DP on Strings)

> **Template:** dp[i][j] — match: `dp[i-1][j-1]+1`; no match: `max(dp[i-1][j], dp[i][j-1])`

---

### P32 — Longest Common Subsequence
**LeetCode #1143 | Difficulty: Medium | Company: Amazon, Google**

> Find length of longest common subsequence of two strings.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i][j]` = LCS of s1[0..i-1] and s2[0..j-1] | |
| Match | if `s1[i-1]==s2[j-1]`: `dp[i][j] = dp[i-1][j-1] + 1` | extend |
| Mismatch | else: `dp[i][j] = max(dp[i-1][j], dp[i][j-1])` | skip one |
| Base | `dp[i][0]=0, dp[0][j]=0` | |

#### Java code

```java
public int longestCommonSubsequence(String t1, String t2) {
    int n=t1.length(), m=t2.length();
    int[][] dp = new int[n+1][m+1];
    for (int i=1;i<=n;i++)
        for (int j=1;j<=m;j++)
            dp[i][j] = t1.charAt(i-1)==t2.charAt(j-1)
                ? dp[i-1][j-1]+1
                : Math.max(dp[i-1][j], dp[i][j-1]);
    return dp[n][m];
}
```

#### Example

```
t1="abcde", t2="ace"
      ""  a  c  e
  ""   0  0  0  0
   a   0  1  1  1
   b   0  1  1  1
   c   0  1  2  2
   d   0  1  2  2
   e   0  1  2  3
Output: 3 ("ace") ✓
```

---

### P33 — Edit Distance
**LeetCode #72 | Difficulty: Hard | Company: Google, Amazon**

> Min operations (insert/delete/replace) to convert word1 → word2.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Base | `dp[i][0]=i` (delete i chars), `dp[0][j]=j` (insert j chars) | |
| Match | `dp[i][j] = dp[i-1][j-1]` | free — chars equal |
| Mismatch | `dp[i][j] = 1 + min(replace:dp[i-1][j-1], delete:dp[i-1][j], insert:dp[i][j-1])` | |

#### Java code

```java
public int minDistance(String w1, String w2) {
    int n=w1.length(), m=w2.length();
    int[][] dp = new int[n+1][m+1];
    for (int i=0;i<=n;i++) dp[i][0]=i;
    for (int j=0;j<=m;j++) dp[0][j]=j;
    for (int i=1;i<=n;i++)
        for (int j=1;j<=m;j++)
            dp[i][j] = w1.charAt(i-1)==w2.charAt(j-1)
                ? dp[i-1][j-1]
                : 1 + Math.min(dp[i-1][j-1], Math.min(dp[i-1][j], dp[i][j-1]));
    return dp[n][m];
}
```

#### Example

```
w1="horse", w2="ros"
       ""  r  o  s
  ""    0  1  2  3
   h    1  1  2  3
   o    2  2  1  2
   r    3  2  2  2
   s    4  3  3  2
   e    5  4  4  3
Output: 3 ✓
```

---

### P34 — Shortest Common Supersequence
**LeetCode #1092 | Difficulty: Medium | Company: Google**

> Shortest string containing both s1 and s2 as subsequences. Length = n+m-LCS.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Length | `SCS length = n + m - LCS(s1,s2)` | |
| Build | Backtrack dp table: match → add once, mismatch → add the skipped char | |
| Base cases | Append remaining chars of whichever string isn't exhausted | |

#### Java code

```java
public String shortestCommonSupersequence(String s1, String s2) {
    int n=s1.length(), m=s2.length();
    int[][] dp = new int[n+1][m+1];
    for (int i=1;i<=n;i++) for (int j=1;j<=m;j++)
        dp[i][j] = s1.charAt(i-1)==s2.charAt(j-1)
            ? dp[i-1][j-1]+1 : Math.max(dp[i-1][j], dp[i][j-1]);
    // backtrack
    StringBuilder sb = new StringBuilder();
    int i=n, j=m;
    while (i>0 && j>0) {
        if (s1.charAt(i-1)==s2.charAt(j-1)) { sb.append(s1.charAt(i-1)); i--; j--; }
        else if (dp[i-1][j]>dp[i][j-1]) sb.append(s1.charAt(--i));
        else sb.append(s2.charAt(--j));
    }
    while (i>0) sb.append(s1.charAt(--i));
    while (j>0) sb.append(s2.charAt(--j));
    return sb.reverse().toString();
}
```

#### Example

```
s1="abac", s2="cab"
LCS="ab"(length 2), SCS length=4+3-2=5
Backtrack → "cabac"
Output: "cabac" ✓
```

---

### P35 — Distinct Subsequences
**LeetCode #115 | Difficulty: Hard | Company: Google**

> Count distinct ways to form t as a subsequence of s.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Base | `dp[i][0]=1` (empty t always matched) | |
| Match | `dp[i][j] = dp[i-1][j-1] + dp[i-1][j]` | use s[i-1] or skip it |
| No match | `dp[i][j] = dp[i-1][j]` | skip s[i-1] |

#### Java code

```java
public int numDistinct(String s, String t) {
    int n=s.length(), m=t.length();
    long[][] dp = new long[n+1][m+1];
    for (int i=0;i<=n;i++) dp[i][0]=1;   // 1 way to match empty t
    for (int i=1;i<=n;i++)
        for (int j=1;j<=m;j++) {
            dp[i][j] = dp[i-1][j];        // skip s[i-1]
            if (s.charAt(i-1)==t.charAt(j-1))
                dp[i][j] += dp[i-1][j-1]; // use s[i-1] to match t[j-1]
        }
    return (int)dp[n][m];
}
```

#### Example

```
s="rabbbit", t="rabbit"
Three 'b's in s, we need two 'b's → C(3,2)=3 ways
Output: 3 ✓
```

---

### P36 — Min ASCII Delete Sum
**LeetCode #712 | Difficulty: Medium | Company: Google**

> Minimum sum of ASCII values of deleted characters to make s1 == s2.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Base | `dp[i][0]=sum(s1[0..i-1])`, `dp[0][j]=sum(s2[0..j-1])` | delete all |
| Match | `dp[i][j] = dp[i-1][j-1]` | keep both — no cost |
| Mismatch | `dp[i][j] = min(dp[i-1][j]+s1[i-1], dp[i][j-1]+s2[j-1])` | delete one |

#### Java code

```java
public int minimumDeleteSum(String s1, String s2) {
    int n=s1.length(), m=s2.length();
    int[][] dp = new int[n+1][m+1];
    for (int i=1;i<=n;i++) dp[i][0]=dp[i-1][0]+s1.charAt(i-1);
    for (int j=1;j<=m;j++) dp[0][j]=dp[0][j-1]+s2.charAt(j-1);
    for (int i=1;i<=n;i++)
        for (int j=1;j<=m;j++)
            dp[i][j] = s1.charAt(i-1)==s2.charAt(j-1)
                ? dp[i-1][j-1]
                : Math.min(dp[i-1][j]+s1.charAt(i-1), dp[i][j-1]+s2.charAt(j-1));
    return dp[n][m];
}
```

#### Example

```
s1="sea", s2="eat"
Delete 's' (115) and 't' (116): "ea" == "ea"
Output: 231 ✓
```

---

### P37 — Wildcard Matching
**LeetCode #44 | Difficulty: Hard | Company: Google, Facebook**

> `?` matches any single char, `*` matches any sequence (including empty).

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Base | `dp[0][j] = true` if p[0..j-1] all '*' | only stars match empty |
| `*` in pattern | `dp[i][j] = dp[i-1][j] OR dp[i][j-1]` | use or skip one char |
| `?` or match | `dp[i][j] = dp[i-1][j-1]` | single match |

#### Java code

```java
public boolean isMatch(String s, String p) {
    int n=s.length(), m=p.length();
    boolean[][] dp = new boolean[n+1][m+1];
    dp[0][0] = true;
    for (int j=1;j<=m;j++) dp[0][j] = p.charAt(j-1)=='*' && dp[0][j-1];
    for (int i=1;i<=n;i++)
        for (int j=1;j<=m;j++) {
            char pc = p.charAt(j-1);
            if (pc=='*')
                dp[i][j] = dp[i-1][j] ||     // * matches one more char
                            dp[i][j-1];       // * matches empty
            else
                dp[i][j] = (pc=='?'||pc==s.charAt(i-1)) && dp[i-1][j-1];
        }
    return dp[n][m];
}
```

#### Example

```
s="adceb", p="*a*b"
dp[0][1]=true (*=empty), dp[0][3]=true (*=empty)
dp[1][2]=true (a==a), dp[1][3]=dp[0][3]=true
... dp[5][4]=true ✓
```

---

### P38 — Longest Palindromic Subsequence
**LeetCode #516 | Difficulty: Medium | Company: Amazon**

> LPS of a string. Equivalent to LCS(s, reverse(s)).

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Insight | LPS(s) = LCS(s, reversed(s)) | or use interval DP directly |
| Interval DP | `dp[i][j]` = LPS of s[i..j] | |
| Match | `dp[i][j] = dp[i+1][j-1] + 2` | both ends match |
| No match | `dp[i][j] = max(dp[i+1][j], dp[i][j-1])` | skip one end |

#### Java code

```java
public int longestPalindromeSubseq(String s) {
    int n = s.length();
    int[][] dp = new int[n][n];
    for (int i=0;i<n;i++) dp[i][i]=1;
    for (int len=2;len<=n;len++)
        for (int i=0;i<=n-len;i++) {
            int j=i+len-1;
            dp[i][j] = s.charAt(i)==s.charAt(j)
                ? dp[i+1][j-1]+2
                : Math.max(dp[i+1][j], dp[i][j-1]);
        }
    return dp[0][n-1];
}
```

#### Example

```
s="bbbab"
dp[0][4]:
  dp[0][1]=2(bb), dp[1][2]=2(bb), dp[2][3]=1(ba), dp[3][4]=1(ab)
  dp[0][2]=3(bbb), dp[1][3]=2(bb), dp[2][4]=2(ba→b)
  dp[0][3]=3(bbb), dp[1][4]=3(bbb)
  dp[0][4]: b==b → dp[1][3]+2=4
Output: 4 ✓
```

---

### P39 — Palindromic Substrings
**LeetCode #647 | Difficulty: Medium | Company: Amazon, Google**

> Count all palindromic substrings in s.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i][j]` = true if s[i..j] is palindrome | |
| Base | `dp[i][i]=true` (single char), `dp[i][i+1]=(s[i]==s[i+1])` | |
| Expand | `dp[i][j] = (s[i]==s[j]) && dp[i+1][j-1]` | |
| Count | increment for every `dp[i][j]=true` | |

#### Java code

```java
public int countSubstrings(String s) {
    int n = s.length(), count = 0;
    boolean[][] dp = new boolean[n][n];
    for (int len=1;len<=n;len++)
        for (int i=0;i<=n-len;i++) {
            int j = i+len-1;
            if (s.charAt(i)==s.charAt(j))
                dp[i][j] = (len<=2) || dp[i+1][j-1];
            if (dp[i][j]) count++;
        }
    return count;
}
```

#### Example

```
s="abc": a,b,c → 3 palindromes
s="aaa": a,a,a,aa,aa,aaa → 6 palindromes
Output for "abc": 3 ✓
```

---

## Category 8 — LIS (Subsequences)

---

### P40 — Longest Increasing Subsequence
**LeetCode #300 | Difficulty: Medium | Company: Amazon, Google**

> Find length of longest strictly increasing subsequence.

#### Approach table

| Approach | Time | Note |
|----------|------|------|
| DP | O(n²) | `dp[i]=max(dp[j]+1)` for j<i with nums[j]<nums[i] |
| Binary Search | O(n log n) | patience sorting — maintain `tails[]` array |

#### Java code

```java
// O(n²)
public int lengthOfLIS(int[] nums) {
    int n = nums.length;
    int[] dp = new int[n]; Arrays.fill(dp, 1);
    for (int i=1;i<n;i++)
        for (int j=0;j<i;j++)
            if (nums[j]<nums[i]) dp[i]=Math.max(dp[i],dp[j]+1);
    return Arrays.stream(dp).max().getAsInt();
}

// O(n log n) — patience sort
public int lengthOfLIS_Fast(int[] nums) {
    int[] tails = new int[nums.length]; int size=0;
    for (int num:nums) {
        int lo=0,hi=size;
        while(lo<hi){int mid=(lo+hi)/2; if(tails[mid]<num)lo=mid+1; else hi=mid;}
        tails[lo]=num; if(lo==size)size++;
    }
    return size;
}
```

#### Example

```
nums=[10,9,2,5,3,7,101,18]
dp:   1  1  1  2  2  3   4   4
Output: 4 ([2,5,7,101] or [2,3,7,18]) ✓
```

---

### P41 — Number of LIS
**LeetCode #673 | Difficulty: Medium | Company: Google**

> Count the number of distinct LIS.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `len[i]` = LIS ending at i; `cnt[i]` = number of such LIS | |
| If `len[j]+1 > len[i]` | `len[i]=len[j]+1; cnt[i]=cnt[j]` | found longer |
| If `len[j]+1 == len[i]` | `cnt[i]+=cnt[j]` | another way same length |
| Answer | sum `cnt[i]` where `len[i]==maxLen` | |

#### Java code

```java
public int findNumberOfLIS(int[] nums) {
    int n=nums.length, maxLen=0, res=0;
    int[] len=new int[n], cnt=new int[n];
    Arrays.fill(len,1); Arrays.fill(cnt,1);
    for (int i=1;i<n;i++)
        for (int j=0;j<i;j++)
            if (nums[j]<nums[i]) {
                if (len[j]+1>len[i]) { len[i]=len[j]+1; cnt[i]=cnt[j]; }
                else if (len[j]+1==len[i]) cnt[i]+=cnt[j];
            }
    for (int l:len) maxLen=Math.max(maxLen,l);
    for (int i=0;i<n;i++) if (len[i]==maxLen) res+=cnt[i];
    return res;
}
```

#### Example

```
nums=[1,3,5,4,7]
len=[1,2,3,3,4], cnt=[1,1,1,1,2]
maxLen=4, count at len=4: cnt[4]=2
Output: 2 ([1,3,5,7] and [1,3,4,7]) ✓
```

---

### P42 — Largest Divisible Subset
**LeetCode #368 | Difficulty: Medium | Company: Amazon**

> Largest subset where every pair (a,b): a%b==0 or b%a==0.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Sort | Sort nums ascending | divisibility chain works on sorted |
| State | `dp[i]` = max subset size ending at i | LIS-style |
| Recurrence | if `nums[i] % nums[j] == 0`: `dp[i] = max(dp[i], dp[j]+1)` | |
| Reconstruct | Use `prev[i]` array to backtrack the subset | |

#### Java code

```java
public List<Integer> largestDivisibleSubset(int[] nums) {
    Arrays.sort(nums); int n=nums.length;
    int[] dp=new int[n], prev=new int[n];
    Arrays.fill(dp,1); Arrays.fill(prev,-1);
    int maxLen=1, maxIdx=0;
    for (int i=1;i<n;i++)
        for (int j=0;j<i;j++)
            if (nums[i]%nums[j]==0 && dp[j]+1>dp[i]) {
                dp[i]=dp[j]+1; prev[i]=j;
            }
    for (int i=0;i<n;i++) if (dp[i]>maxLen) { maxLen=dp[i]; maxIdx=i; }
    List<Integer> res=new ArrayList<>();
    while (maxIdx!=-1) { res.add(nums[maxIdx]); maxIdx=prev[maxIdx]; }
    return res;
}
```

#### Example

```
nums=[1,2,4,8] → sorted same
dp=[1,2,3,4], all divisible
Output: [1,2,4,8] ✓
```

---

### P43 — Max Length of Pair Chain
**LeetCode #646 | Difficulty: Medium | Company: Amazon**

> Chain pairs where each pair's start > previous pair's end. Sort by end, LIS-style.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Sort | by pair end ascending | greedy + DP works |
| State | `dp[i]` = longest chain ending at pair i | |
| Recurrence | if `pairs[j][1] < pairs[i][0]`: `dp[i]=max(dp[i], dp[j]+1)` | |
| Answer | `max(dp)` | |

#### Java code

```java
public int findLongestChain(int[][] pairs) {
    Arrays.sort(pairs, (a,b)->a[1]-b[1]);  // sort by end
    int n=pairs.length;
    int[] dp=new int[n]; Arrays.fill(dp,1);
    for (int i=1;i<n;i++)
        for (int j=0;j<i;j++)
            if (pairs[j][1]<pairs[i][0])   // end of j < start of i
                dp[i]=Math.max(dp[i],dp[j]+1);
    return Arrays.stream(dp).max().getAsInt();
}
```

#### Example

```
pairs=[[1,2],[2,3],[3,4]]  sort by end: same
dp[0]=1, dp[1]: pairs[0][1]=2 not < pairs[1][0]=2 → dp[1]=1
dp[2]: pairs[0][1]=2<3→dp[2]=2; pairs[1][1]=3 not <3 → dp[2]=2
Output: 2 ([1,2]→[3,4]) ✓
```

---

### P44 — Longest String Chain
**LeetCode #1048 | Difficulty: Medium | Company: Amazon**

> Chain of words where each is predecessor (add one letter) of the next.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Sort | by word length ascending | shorter words first |
| State | `dp[word]` = longest chain ending at word | HashMap |
| Recurrence | for each word, try removing each char → check if predecessor in dp | |
| Answer | `max(dp.values())` | |

#### Java code

```java
public int longestStrChain(String[] words) {
    Arrays.sort(words, (a,b)->a.length()-b.length());
    Map<String,Integer> dp = new HashMap<>();
    int best = 1;
    for (String w : words) {
        dp.put(w, 1);
        for (int i=0;i<w.length();i++) {
            String prev = w.substring(0,i)+w.substring(i+1);  // remove char i
            if (dp.containsKey(prev))
                dp.put(w, Math.max(dp.get(w), dp.get(prev)+1));
        }
        best = Math.max(best, dp.get(w));
    }
    return best;
}
```

#### Example

```
words=["a","b","ba","bca","bda","bdca"]
Sorted by len: a,b,ba,bca,bda,bdca
dp: a=1,b=1,ba=2,bca=3,bda=3,bdca=4
Output: 4 ✓
```

---

### P45 — Russian Doll Envelopes
**LeetCode #354 | Difficulty: Hard | Company: Google**

> Max envelopes you can nest (each must be strictly smaller in both dims).

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Sort | width ASC, height **DESC** for same width | prevents using same width twice |
| Reduce to | LIS on heights only | after sort, just find LIS |
| LIS | O(n log n) binary search on `tails[]` | |

#### Java code

```java
public int maxEnvelopes(int[][] envelopes) {
    // Sort: width ASC, height DESC (prevent using same width)
    Arrays.sort(envelopes, (a,b)->a[0]!=b[0] ? a[0]-b[0] : b[1]-a[1]);
    int n=envelopes.length;
    int[] tails=new int[n]; int size=0;
    for (int[] e:envelopes) {
        int h=e[1], lo=0, hi=size;
        while(lo<hi){int mid=(lo+hi)/2; if(tails[mid]<h)lo=mid+1; else hi=mid;}
        tails[lo]=h; if(lo==size)size++;
    }
    return size;
}
```

#### Example

```
envelopes=[[5,4],[6,4],[6,7],[2,3]]
Sort: [2,3],[5,4],[6,7],[6,4] → heights for LIS=[3,4,7,4]
LIS of [3,4,7]: length 3
Output: 3 ✓
```

---

## Category 9 — Grid DP (Extra)

---

### P46 — Maximal Square
**LeetCode #221 | Difficulty: Medium | Company: Amazon, Google**

> Find side of largest square of all 1s in binary matrix.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i][j]` = side of largest square with bottom-right at (i,j) | |
| If cell = '1' | `dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1` | |
| If cell = '0' | `dp[i][j] = 0` | |
| Answer | `maxSide²` | |

#### Java code

```java
public int maximalSquare(char[][] matrix) {
    int m=matrix.length, n=matrix[0].length, maxSide=0;
    int[][] dp=new int[m+1][n+1];
    for (int i=1;i<=m;i++)
        for (int j=1;j<=n;j++)
            if (matrix[i-1][j-1]=='1') {
                dp[i][j]=Math.min(dp[i-1][j], Math.min(dp[i][j-1],dp[i-1][j-1]))+1;
                maxSide=Math.max(maxSide,dp[i][j]);
            }
    return maxSide*maxSide;
}
```

#### Example

```
matrix=[["1","0","1","0","0"],
        ["1","0","1","1","1"],
        ["1","1","1","1","1"],
        ["1","0","0","1","0"]]
dp[3][4]=3 (3×3 square at bottom-right area)
Output: 4 (2×2 = area 4)... let me trace:
dp[2][3]=2, dp[2][4]=2, dp[3][3]=min(2,2,2)+1=3? → maxSide=2, output=4 ✓
```

---

### P47 — Cherry Pickup
**LeetCode #741 | Difficulty: Hard | Company: Google**

> Max cherries picking going (0,0)→(n-1,n-1) and back. Model as two people moving forward simultaneously.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[r1][r2][c1]` = max cherries when person1 at (r1,c1) and person2 at same step | c2 = step-r2 |
| Step sync | Both move in sync: `step = r1+c1 = r2+c2` | |
| Cherries | `grid[r1][c1] + (r1≠r2 ? grid[r2][c2] : 0)` | don't double count same cell |
| Return | `max(0, dp[n-1][n-1][n-1])` | |

#### Java code

```java
public int cherryPickup(int[][] grid) {
    int n=grid.length;
    // dp[r1][c1][c2] = max cherries when person1 at (r1,c1) and person2 at (r1,r1+c1-c2)
    // Both move in sync: r1+c1=r2+c2=step
    int[][][] dp=new int[n][n][n];
    for (int[][] a:dp) for (int[] b:a) Arrays.fill(b,-1);
    dp[0][0][0]=grid[0][0];
    for (int step=1;step<2*n-1;step++)
        for (int r1=Math.min(step,n-1);r1>=Math.max(0,step-n+1);r1--)
            for (int r2=r1;r2>=Math.max(0,step-n+1);r2--) {
                int c1=step-r1, c2=step-r2;
                if (c1>=n||c2>=n) continue;
                if (grid[r1][c1]==-1||grid[r2][c2]==-1) continue;
                int best=-1;
                for (int dr1:new int[]{0,1}) for (int dr2:new int[]{0,1}) {
                    int pr1=r1-dr1, pc1=c1-(1-dr1), pr2=r2-dr2, pc2=c2-(1-dr2);
                    if (pr1<0||pc1<0||pr2<0||pc2<0) continue;
                    if (dp[pr1][pr2][pc1]==-1) continue;
                    best=Math.max(best, dp[pr1][pr2][pc1]);
                }
                if (best==-1) continue;
                best += grid[r1][c1]+(r1!=r2 ? grid[r2][c2] : 0);
                dp[r1][r2][c1]=Math.max(dp[r1][r2][c1], best);
            }
    return Math.max(0, dp[n-1][n-1][n-1]);
}
```

#### Example

```
grid=[[0,1,-1],[1,0,-1],[1,1,1]]
Two people move in sync forward.
Person1 path: (0,0)→(1,0)→(2,0) picks 0+1+1=2
Person2 path: (0,0)→(0,1)→(1,1) picks 0+1+0=1 (shared (0,0) counted once)
Best combined = 4  (pick right cells avoiding -1 walls)
Output: 4 ✓
```

---

### P48 — Minimum Cost Tickets (DP Array variant)
**LeetCode #983 | Difficulty: Medium | Company: Amazon**

> Same as P31 but using full day-indexed DP array without a Set.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i]` = min cost to travel all days up to day i | indexed by day number |
| Non-travel | `dp[i] = dp[i-1]` | no travel on this day |
| Travel | `dp[i] = min(dp[i-1]+costs[0], dp[max(0,i-7)]+costs[1], dp[max(0,i-30)]+costs[2])` | |

#### Java code

```java
public int mincostTickets(int[] days, int[] costs) {
    int last=days[days.length-1];
    boolean[] travel=new boolean[last+1];
    for (int d:days) travel[d]=true;
    int[] dp=new int[last+1];
    for (int i=1;i<=last;i++) {
        if (!travel[i]) { dp[i]=dp[i-1]; continue; }
        dp[i]=Math.min(dp[i-1]+costs[0],
               Math.min(dp[Math.max(0,i-7)]+costs[1],
                        dp[Math.max(0,i-30)]+costs[2]));
    }
    return dp[last];
}
```

#### Example

```
days=[1,4,6,7,8,20], costs=[2,7,15]
last=20, travel=[T,F,F,T,F,T,T,T,F,...,T]
dp[1]=2(1-day), dp[4]=4(1+1-day), dp[6]=6, dp[7]=7, dp[8]=9
dp[20]=min(dp[19]+2, dp[13]+7, dp[0]+15)=min(11,11,15)=11
Output: 11 ✓
```

---

## Quick Pattern Reference`

---

## Quick Pattern Reference

| Problem | Pattern | Key recurrence |
|---------|---------|----------------|
| House Robber | Fibonacci | `max(prev1, prev2+nums[i])` |
| Min Cost Climbing | Fibonacci | `min(prev1,prev2)+cost[i]` |
| Stock I | Greedy | track minPrice |
| Stock II/Fee/Cooldown | State machine | hold/notHold/cooldown |
| Stock III | Extended states | buy1→sell1→buy2→sell2 |
| Stock IV | k transactions | buy[k]/sell[k] arrays |
| Coin Change | Min/Max path | `min(dp[i-coin]+1)` |
| Min Path Sum | Grid DP | `grid+min(up,left)` |
| Triangle | Grid DP (bottom-up) | `tri+min(dp[j],dp[j+1])` |
| Perfect Squares | Min/Max path | `min(dp[i-j²]+1)` |
| Climbing Stairs | Count ways | `dp[i]=dp[i-1]+dp[i-2]` |
| Unique Paths | Count ways | `dp[i][j]=up+left` |
| Decode Ways | Count ways | 1-digit + 2-digit checks |
| Coin Change II | Count ways | forward loop (reuse) |
| 0/1 Knapsack | Knapsack | reverse capacity loop |
| Partition Equal | Knapsack bool | `dp[w]\|=dp[w-num]` |
| Target Sum | Knapsack count | subset count = (total+target)/2 |
| LCS | String DP | match:diag+1 else max(up,left) |
| Edit Distance | String DP | replace/insert/delete |
| Distinct Subsequences | String DP | use/skip s[i] for t[j] |
| Wildcard | String DP | ?→single, *→any |
| LPS | String DP | match:diag+2 else max |
| Palindromic Substrings | String DP | expand from equal ends |
| LIS | Sequence DP | `dp[i]=max(dp[j]+1)` j<i |
| Number of LIS | Sequence DP | track len+cnt arrays |
| Maximal Square | Grid DP | `min(left,up,diag)+1` |
