# Dynamic Programming — Solved Problems (38 Problems)

> **Notes & Templates:** [01_dp_notes.md](./01_dp_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Fibonacci / Decision Making (Easy warmup)
- [P1 — House Robber](#problem-1--house-robber)
- [P2 — Maximum Subarray](#problem-2--maximum-subarray)
- [P3 — Decode Ways](#problem-3--decode-ways)

### Category 2 — Min/Max Path to Target
- [P4 — Coin Change](#problem-4--coin-change)
- [P5 — Minimum Path Sum](#problem-5--minimum-path-sum)
- [P6 — Minimum Falling Path Sum](#problem-6--minimum-falling-path-sum)
- [P7 — Unique Paths](#problem-7--unique-paths)

### Category 3 — 0/1 Knapsack (Take / Not Take)
- [P8 — 0/1 Knapsack](#problem-8--01-knapsack)
- [P9 — Partition Equal Subset Sum](#problem-9--partition-equal-subset-sum)
- [P10 — Target Sum](#problem-10--target-sum)
- [P11 — Ones and Zeroes](#problem-11--ones-and-zeroes)
- [P12 — Last Stone Weight II](#problem-12--last-stone-weight-ii)

### Category 4 — Unbounded Knapsack (Infinite Supply)
- [P13 — Coin Change II](#problem-13--coin-change-ii)
- [P14 — Count Numbers with Unique Digits](#problem-14--count-numbers-with-unique-digits)

### Category 5 — LIS / Subsequences
- [P15 — Longest Increasing Subsequence](#problem-15--longest-increasing-subsequence)
- [P16 — Count Different Palindromic Subsequences](#problem-16--count-different-palindromic-subsequences)

### Category 6 — DP on Strings
- [P17 — Longest Common Subsequence](#problem-17--longest-common-subsequence)
- [P18 — Edit Distance](#problem-18--edit-distance)
- [P19 — Longest Palindromic Subsequence](#problem-19--longest-palindromic-subsequence)
- [P20 — Distinct Subsequences](#problem-20--distinct-subsequences)

### Category 7 — Interval DP (Merging)
- [P21 — Burst Balloons](#problem-21--burst-balloons)
- [P22 — Min Cost to Cut a Stick](#problem-22--min-cost-to-cut-a-stick)
- [P23 — Matrix Chain Multiplication](#problem-23--matrix-chain-multiplication)
- [P24 — Strange Printer](#problem-24--strange-printer)
- [P25 — Minimum Cost to Merge Stones](#problem-25--minimum-cost-to-merge-stones)
- [P26 — Remove Boxes](#problem-26--remove-boxes)

### Category 8 — Probability / Expectation DP
- [P27 — Knight Probability in Chessboard](#problem-27--knight-probability-in-chessboard)
- [P28 — Dice Roll Simulation](#problem-28--dice-roll-simulation)
- [P29 — Soup Servings](#problem-29--soup-servings)
- [P30 — New 21 Game](#problem-30--new-21-game)
- [P31 — Two Boxes (Probability of Black Balls)](#problem-31--two-boxes)

### Category 9 — Bonus / Extra (important for interviews)
- [P32 — Number of Ways (Climbing Stairs variant)](#problem-32--number-of-ways)
- [P33 — Num of Decodings (Decode Ways II)](#problem-33--num-of-decodings-ii)
- [P34 — Longest Palindromic Substring](#problem-34--longest-palindromic-substring)
- [P35 — Word Break](#problem-35--word-break)
- [P36 — Jump Game II](#problem-36--jump-game-ii)
- [P37 — House Robber II](#problem-37--house-robber-ii)
- [P38 — Maximal Square](#problem-38--maximal-square)

---

## Category 1 — Fibonacci / Decision Making

---

### Problem 1 — House Robber
**LeetCode #198 | Difficulty: Easy | Company: Amazon, Google**

> Rob houses, no two adjacent. Max money.

#### Approach table

| State | Meaning | Recurrence |
|-------|---------|-----------|
| `dp[i]` | max money robbing houses 0..i | `max(dp[i-1], dp[i-2] + nums[i])` |

#### Java code

```java
public int rob(int[] nums) {
    if (nums.length == 1) return nums[0];
    int prev2 = nums[0];
    int prev1 = Math.max(nums[0], nums[1]);

    for (int i = 2; i < nums.length; i++) {
        int curr = Math.max(prev1,           // skip house i
                            prev2 + nums[i]); // rob house i
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```

#### Example

```
nums = [2,7,9,3,1]
prev2=2, prev1=max(2,7)=7
i=2(9): curr=max(7, 2+9)=11, prev2=7, prev1=11
i=3(3): curr=max(11, 7+3)=11, prev2=11, prev1=11
i=4(1): curr=max(11, 11+1)=12
Output: 12 (rob 0,2,4 → 2+9+1) ✓
```

---

### Problem 2 — Maximum Subarray
**LeetCode #53 | Difficulty: Easy | Company: Amazon, Google**

> Kadane's algorithm — DP version.

#### Approach table

| State | Meaning | Recurrence |
|-------|---------|-----------|
| `dp[i]` | max subarray sum ENDING at i | `max(nums[i], dp[i-1] + nums[i])` |

#### Java code

```java
public int maxSubArray(int[] nums) {
    int cur = nums[0], best = nums[0];
    for (int i = 1; i < nums.length; i++) {
        cur = Math.max(nums[i], cur + nums[i]);  // extend or restart
        best = Math.max(best, cur);
    }
    return best;
}
```

#### Example

```
nums = [-2,1,-3,4,-1,2,1,-5,4]
cur:   -2  1  -2  4   3  5  6   1  5
best:  -2  1   1  4   4  5  6   6  6
Output: 6 ([4,-1,2,1]) ✓
```

---

### Problem 3 — Decode Ways
**LeetCode #91 | Difficulty: Medium | Company: Facebook, Amazon**

> Count ways to decode digit string ('A'=1..'Z'=26).

#### Java code

```java
public int numDecodings(String s) {
    int n = s.length();
    int[] dp = new int[n + 1];
    dp[0] = 1;                                   // empty string: 1 way
    dp[1] = s.charAt(0) == '0' ? 0 : 1;

    for (int i = 2; i <= n; i++) {
        int oneDigit = s.charAt(i-1) - '0';
        int twoDigit = Integer.parseInt(s.substring(i-2, i));

        if (oneDigit != 0)      dp[i] += dp[i-1];  // single digit valid
        if (twoDigit >= 10 && twoDigit <= 26) dp[i] += dp[i-2];  // two digits valid
    }
    return dp[n];
}
```

#### Example

```
s = "226"
dp[0]=1, dp[1]=1 (2 valid)
i=2: oneDigit=2✓→dp[2]+=dp[1]=1; twoDigit=22✓→dp[2]+=dp[0]=1 → dp[2]=2
i=3: oneDigit=6✓→dp[3]+=dp[2]=2; twoDigit=26✓→dp[3]+=dp[1]=1 → dp[3]=3
Output: 3 (2|2|6, 22|6, 2|26) ✓
```

---

## Category 2 — Min/Max Path to Target

---

### Problem 4 — Coin Change
**LeetCode #322 | Difficulty: Medium | Company: Amazon, Google**

> Min coins to make amount. Coins reusable → Unbounded Knapsack.

#### Java code

```java
public int coinChange(int[] coins, int amount) {
    int[] dp = new int[amount + 1];
    Arrays.fill(dp, amount + 1);     // init with "infinity"
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
dp[5]=1(5), dp[10]=2(5+5), dp[11]=1(11), dp[15]=min(dp[14]+1, dp[10]+1, dp[4]+1)
dp[14]=dp[3]+dp[11]=? let's trace: dp[15]=3 (5+5+5) ✓
Actually: dp[15] = min way = 3 coins (5,5,5) NOT 5 (1x5) — wait dp[11]=1, dp[15-11=4]=4 → 5
Hmm: dp[15] = min(dp[14]+1=5, dp[10]+1=3, dp[4]+1=5) = 3
Output: 3 ✓
```

---

### Problem 5 — Minimum Path Sum
**LeetCode #64 | Difficulty: Medium | Company: Amazon, Google**

> Min sum from top-left to bottom-right (move right or down only).

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
grid = [[1,3,1],[1,5,1],[4,2,1]]

dp:  1  4  5
     2  7  6
     6  8  7

Output: 7 (1→3→1→1→1) ✓
```

---

### Problem 6 — Minimum Falling Path Sum
**LeetCode #931 | Difficulty: Medium | Company: Google**

> Each row you can move to adjacent column (±1) or same. Min path from top to bottom.

#### Java code

```java
public int minFallingPathSum(int[][] matrix) {
    int n = matrix.length;
    int[][] dp = new int[n][n];
    dp[0] = matrix[0].clone();

    for (int i = 1; i < n; i++)
        for (int j = 0; j < n; j++) {
            int best = dp[i-1][j];
            if (j > 0) best = Math.min(best, dp[i-1][j-1]);
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
matrix = [[2,1,3],[6,5,4],[7,8,9]]
dp[0] = [2,1,3]
dp[1]: j=0→2+min(2,1)=3, j=1→5+min(2,1,3)=6, j=2→4+min(1,3)=5
dp[2]: j=0→7+min(3,6)=10, j=1→8+min(3,6,5)=11, j=2→9+min(6,5)=14
min(10,11,14) = 10 ✓
```

---

### Problem 7 — Unique Paths
**LeetCode #62 | Difficulty: Medium | Company: Amazon**

> Count paths from top-left to bottom-right moving only right or down.

#### Java code

```java
public int uniquePaths(int m, int n) {
    int[][] dp = new int[m][n];
    for (int i = 0; i < m; i++) dp[i][0] = 1;  // left column: only 1 way (all down)
    for (int j = 0; j < n; j++) dp[0][j] = 1;  // top row: only 1 way (all right)

    for (int i = 1; i < m; i++)
        for (int j = 1; j < n; j++)
            dp[i][j] = dp[i-1][j] + dp[i][j-1];  // from above + from left

    return dp[m-1][n-1];
}
```

#### Example

```
m=3, n=7
dp[2][6] = 28 ✓
```

---

## Category 3 — 0/1 Knapsack (Take / Not Take)

---

### Problem 8 — 0/1 Knapsack
**GFG | Difficulty: Medium | Company: Amazon**

> Max value in knapsack of capacity W. Each item used at most once.

#### Java code

```java
public int knapsack(int[] weight, int[] value, int n, int W) {
    int[] dp = new int[W + 1];

    for (int i = 0; i < n; i++)
        for (int w = W; w >= weight[i]; w--)   // REVERSE — 0/1 (no reuse)
            dp[w] = Math.max(dp[w], dp[w - weight[i]] + value[i]);

    return dp[W];
}
```

#### Example

```
weight=[1,3,4,5], value=[1,4,5,7], W=7

After item 0(w=1,v=1): dp[1..7]=[1,1,1,1,1,1,1]
After item 1(w=3,v=4): dp[3]=5,dp[4]=5,dp[5]=5,dp[6]=5,dp[7]=5
After item 2(w=4,v=5): dp[4]=max(5,1+5)=6,dp[5]=max(5,1+5)=6,dp[6]=max(5,4+5)=9,dp[7]=9
After item 3(w=5,v=7): dp[5]=max(6,1+7)=8,dp[6]=max(9,1+7)=9,dp[7]=max(9,4+7)=11... wait
Actually dp[7]=max(dp[7], dp[7-5]+7)=max(9, dp[2]+7)=max(9,1+7)=9
Correct answer: dp[7]=9 (items 1+2: 4+5=9) ✓
```

---

### Problem 9 — Partition Equal Subset Sum
**LeetCode #416 | Difficulty: Medium | Company: Amazon, Facebook**

> Can we split array into 2 subsets with equal sum? → Can we find subset with sum = total/2?

#### Java code

```java
public boolean canPartition(int[] nums) {
    int total = 0;
    for (int n : nums) total += n;
    if (total % 2 != 0) return false;

    int target = total / 2;
    boolean[] dp = new boolean[target + 1];
    dp[0] = true;                                  // empty subset sums to 0

    for (int num : nums)
        for (int w = target; w >= num; w--)        // REVERSE — 0/1
            dp[w] = dp[w] || dp[w - num];

    return dp[target];
}
```

#### Example

```
nums=[1,5,11,5], total=22, target=11
dp[0]=true
num=1: dp[1]=true
num=5: dp[6]=true, dp[5]=true
num=11: dp[11]=true ← found!
Output: true (subsets {11} and {1,5,5}) ✓
```

---

### Problem 10 — Target Sum
**LeetCode #494 | Difficulty: Medium | Company: Facebook, Amazon**

> Assign + or - to each number. Count ways to reach target.

#### Core insight

Let P = sum of positives, N = sum of negatives. P - N = target, P + N = total.
→ P = (target + total) / 2. Count subsets with sum P.

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
        for (int w = sum; w >= num; w--)    // REVERSE — 0/1
            dp[w] += dp[w - num];

    return dp[sum];
}
```

#### Example

```
nums=[1,1,1,1,1], target=3
total=5, sum=(3+5)/2=4
dp[0]=1
After each num=1: dp[w]+=dp[w-1]
After 5 ones: dp[4]=5
Output: 5 ✓
```

---

### Problem 11 — Ones and Zeroes
**LeetCode #474 | Difficulty: Medium | Company: Google**

> Max strings in subset with at most m zeros and n ones → 2D Knapsack.

#### Java code

```java
public int findMaxForm(String[] strs, int m, int n) {
    int[][] dp = new int[m + 1][n + 1];  // dp[zeros][ones] = max strings

    for (String s : strs) {
        int zeros = 0, ones = 0;
        for (char c : s.toCharArray()) { if (c == '0') zeros++; else ones++; }

        for (int i = m; i >= zeros; i--)       // REVERSE both — 0/1
            for (int j = n; j >= ones; j--)
                dp[i][j] = Math.max(dp[i][j], dp[i-zeros][j-ones] + 1);
    }
    return dp[m][n];
}
```

#### Example

```
strs=["10","0001","111001","1","0"], m=5, n=3
"10"(1z,1o): dp[1][1]=1, dp[2][2]=1...
Final dp[5][3]=4 ✓
```

---

### Problem 12 — Last Stone Weight II
**LeetCode #1049 | Difficulty: Medium | Company: Google**

> Split stones into 2 groups, minimize |sum1 - sum2|.
> Same as: find subset with sum closest to total/2.

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
        if (dp[w]) return total - 2 * w;   // |total - 2*subset|
    return 0;
}
```

#### Example

```
stones=[2,7,4,1,8,1], total=23, target=11
dp achievable: 0,1,2,3,4,5,6,7,8,9,10,11
w=11 is achievable → output = 23-22=1 ✓
```

---

## Category 4 — Unbounded Knapsack (Infinite Supply)

---

### Problem 13 — Coin Change II
**LeetCode #518 | Difficulty: Medium | Company: Amazon**

> Count number of ways to make amount using coins (reusable).

#### Java code

```java
public int change(int amount, int[] coins) {
    int[] dp = new int[amount + 1];
    dp[0] = 1;                                 // 1 way to make amount 0

    for (int coin : coins)
        for (int w = coin; w <= amount; w++)   // FORWARD — unbounded
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
Output: 4 (5, 2+2+1, 2+1+1+1, 1+1+1+1+1) ✓
```

---

### Problem 14 — Count Numbers with Unique Digits
**LeetCode #357 | Difficulty: Medium | Company: Google**

> Count numbers with no repeated digits in range [0, 10^n).

#### Core insight

1-digit: 10 choices. k-digit: 9 × 9 × 8 × ... × (9-k+2). DP on available digit slots.

#### Java code

```java
public int countNumbersWithUniqueDigits(int n) {
    if (n == 0) return 1;
    int result = 10;      // 0-9 for n=1
    int choices = 9;      // first non-zero digit: 9 choices (1-9)
    int available = 9;    // second digit: 9 choices (0-9 except first)

    for (int i = 2; i <= n && available > 0; i++) {
        choices *= available;
        result += choices;
        available--;
    }
    return result;
}
```

#### Example

```
n=2:
1-digit: 10 (0..9)
2-digit: 9×9=81 (first=1..9, second=0..9 except first)
Total = 10+81 = 91 ✓
```

---

## Category 5 — LIS / Subsequences

---

### Problem 15 — Longest Increasing Subsequence
**LeetCode #300 | Difficulty: Medium | Company: Amazon, Google**

#### Java code

```java
// O(n²) — DP approach
public int lengthOfLIS(int[] nums) {
    int n = nums.length;
    int[] dp = new int[n];
    Arrays.fill(dp, 1);    // each element alone = LIS of 1

    for (int i = 1; i < n; i++)
        for (int j = 0; j < i; j++)
            if (nums[j] < nums[i])
                dp[i] = Math.max(dp[i], dp[j] + 1);

    return Arrays.stream(dp).max().getAsInt();
}

// O(n log n) — Greedy + Binary Search
public int lengthOfLIS_Fast(int[] nums) {
    int[] tails = new int[nums.length];
    int size = 0;
    for (int num : nums) {
        int lo = 0, hi = size;
        while (lo < hi) {
            int mid = (lo + hi) / 2;
            if (tails[mid] < num) lo = mid + 1;
            else hi = mid;
        }
        tails[lo] = num;
        if (lo == size) size++;
    }
    return size;
}
```

#### Example

```
nums = [10,9,2,5,3,7,101,18]
dp:     1  1  1  2  2  3   4   4
Output: 4 ([2,3,7,101]) ✓
```

---

### Problem 16 — Count Different Palindromic Subsequences
**LeetCode #730 | Difficulty: Hard | Company: Google**

> Count distinct palindromic subsequences in s.

#### Java code

```java
public int countPalindromicSubsequences(String s) {
    int n = s.length(); long MOD = 1_000_000_007;
    long[][] dp = new long[n][n];
    for (int i = 0; i < n; i++) dp[i][i] = 1;

    for (int len = 2; len <= n; len++) {
        for (int i = 0; i <= n - len; i++) {
            int j = i + len - 1;
            if (s.charAt(i) == s.charAt(j)) {
                int lo = i + 1, hi = j - 1;
                while (lo <= hi && s.charAt(lo) != s.charAt(i)) lo++;
                while (lo <= hi && s.charAt(hi) != s.charAt(j)) hi--;
                if (lo > hi) dp[i][j] = dp[i+1][j-1] * 2 + 2;
                else if (lo == hi) dp[i][j] = dp[i+1][j-1] * 2 + 1;
                else dp[i][j] = dp[i+1][j-1] * 2 - dp[lo+1][hi-1];
            } else {
                dp[i][j] = dp[i+1][j] + dp[i][j-1] - dp[i+1][j-1];
            }
            dp[i][j] = (dp[i][j] + MOD) % MOD;
        }
    }
    return (int) dp[0][n-1];
}
```

---

## Category 6 — DP on Strings

---

### Problem 17 — Longest Common Subsequence
**LeetCode #1143 | Difficulty: Medium | Company: Amazon, Google**

#### Approach table

| Condition | Action |
|-----------|--------|
| `s1[i-1] == s2[j-1]` | `dp[i][j] = dp[i-1][j-1] + 1` |
| different | `dp[i][j] = max(dp[i-1][j], dp[i][j-1])` |

#### Java code

```java
public int longestCommonSubsequence(String text1, String text2) {
    int n = text1.length(), m = text2.length();
    int[][] dp = new int[n + 1][m + 1];

    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++)
            if (text1.charAt(i-1) == text2.charAt(j-1))
                dp[i][j] = dp[i-1][j-1] + 1;
            else
                dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);

    return dp[n][m];
}
```

#### Example

```
text1="abcde", text2="ace"
       ""  a  c  e
  ""    0  0  0  0
   a    0  1  1  1
   b    0  1  1  1
   c    0  1  2  2
   d    0  1  2  2
   e    0  1  2  3

Output: 3 ("ace") ✓
```

---

### Problem 18 — Edit Distance
**LeetCode #72 | Difficulty: Hard | Company: Google, Amazon**

> Min operations (insert/delete/replace) to convert word1 to word2.

#### Approach table

| Condition | Recurrence | Meaning |
|-----------|-----------|---------|
| chars match | `dp[i][j] = dp[i-1][j-1]` | no operation needed |
| chars differ | `dp[i][j] = 1 + min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1])` | replace / delete / insert |

#### Java code

```java
public int minDistance(String word1, String word2) {
    int n = word1.length(), m = word2.length();
    int[][] dp = new int[n + 1][m + 1];

    for (int i = 0; i <= n; i++) dp[i][0] = i;  // delete all of word1
    for (int j = 0; j <= m; j++) dp[0][j] = j;  // insert all of word2

    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++)
            if (word1.charAt(i-1) == word2.charAt(j-1))
                dp[i][j] = dp[i-1][j-1];
            else
                dp[i][j] = 1 + Math.min(dp[i-1][j-1],   // replace
                                Math.min(dp[i-1][j],      // delete
                                         dp[i][j-1]));    // insert
    return dp[n][m];
}
```

#### Example

```
word1="horse", word2="ros"
dp[3][2] = 3 (horse→rorse→rose→ros)
Output: 3 ✓
```

---

### Problem 19 — Longest Palindromic Subsequence
**LeetCode #516 | Difficulty: Medium | Company: Amazon**

> LPS(s) = LCS(s, reverse(s))

#### Java code

```java
public int longestPalindromeSubseq(String s) {
    int n = s.length();
    int[][] dp = new int[n][n];
    for (int i = 0; i < n; i++) dp[i][i] = 1;  // single char = palindrome of len 1

    for (int len = 2; len <= n; len++)
        for (int i = 0; i <= n - len; i++) {
            int j = i + len - 1;
            if (s.charAt(i) == s.charAt(j))
                dp[i][j] = dp[i+1][j-1] + 2;
            else
                dp[i][j] = Math.max(dp[i+1][j], dp[i][j-1]);
        }
    return dp[0][n-1];
}
```

#### Example

```
s = "bbbab"
dp[0][4]: LPS = "bbbb" = 4
Output: 4 ✓
```

---

### Problem 20 — Distinct Subsequences
**LeetCode #115 | Difficulty: Hard | Company: Google**

> Count distinct subsequences of s that equal t.

#### Java code

```java
public int numDistinct(String s, String t) {
    int n = s.length(), m = t.length();
    long[][] dp = new long[n + 1][m + 1];
    for (int i = 0; i <= n; i++) dp[i][0] = 1;  // empty t: 1 way

    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++) {
            dp[i][j] = dp[i-1][j];  // don't use s[i-1]
            if (s.charAt(i-1) == t.charAt(j-1))
                dp[i][j] += dp[i-1][j-1];  // use s[i-1] to match t[j-1]
        }
    return (int) dp[n][m];
}
```

#### Example

```
s="rabbbit", t="rabbit"
dp[7][6] = 3 (three 'b's can be chosen in C(3,2)=3 ways)
Output: 3 ✓
```

---

## Category 7 — Interval DP (Merging)

---

### Problem 21 — Burst Balloons
**LeetCode #312 | Difficulty: Hard | Company: Google, Amazon**

> dp[i][j] = max coins from bursting all balloons in (i..j) exclusive.
> Think LAST balloon to burst (not first) — nums[i]*nums[k]*nums[j].

#### Java code

```java
public int maxCoins(int[] nums) {
    int n = nums.length;
    int[] arr = new int[n + 2];
    arr[0] = arr[n + 1] = 1;
    for (int i = 0; i < n; i++) arr[i + 1] = nums[i];
    n += 2;

    int[][] dp = new int[n][n];

    for (int len = 2; len < n; len++)
        for (int i = 0; i < n - len; i++) {
            int j = i + len;
            for (int k = i + 1; k < j; k++)  // k = last balloon to burst in (i,j)
                dp[i][j] = Math.max(dp[i][j],
                    dp[i][k] + arr[i] * arr[k] * arr[j] + dp[k][j]);
        }
    return dp[0][n - 1];
}
```

#### Example

```
nums=[3,1,5,8] → arr=[1,3,1,5,8,1]
dp[0][5]: last burst at k=1(3): 1*3*1+dp[0][1]+dp[1][5]
                    k=2(1): 1*1*1+dp[0][2]+dp[2][5]... etc
Output: 167 ✓
```

---

### Problem 22 — Min Cost to Cut a Stick
**LeetCode #1547 | Difficulty: Hard | Company: Google**

> dp[i][j] = min cost to perform all cuts between position i and j.

#### Java code

```java
public int minCost(int n, int[] cuts) {
    Arrays.sort(cuts);
    int m = cuts.length;
    int[] c = new int[m + 2];
    c[0] = 0; c[m + 1] = n;
    for (int i = 0; i < m; i++) c[i + 1] = cuts[i];

    int[][] dp = new int[m + 2][m + 2];

    for (int len = 2; len <= m + 1; len++)
        for (int i = 0; i + len <= m + 1; i++) {
            int j = i + len;
            dp[i][j] = Integer.MAX_VALUE;
            for (int k = i + 1; k < j; k++)
                dp[i][j] = Math.min(dp[i][j],
                    dp[i][k] + dp[k][j] + c[j] - c[i]);
        }
    return dp[0][m + 1];
}
```

#### Example

```
n=7, cuts=[1,3,4,5]
c=[0,1,3,4,5,7]
dp[0][5] = min cost = 16 ✓
```

---

### Problem 23 — Matrix Chain Multiplication
**GFG | Difficulty: Hard | Company: Google**

> dp[i][j] = min multiplications to compute product of matrices i..j.

#### Java code

```java
public int matrixChainOrder(int[] dims) {
    int n = dims.length - 1;   // n matrices
    int[][] dp = new int[n][n];

    for (int len = 2; len <= n; len++)
        for (int i = 0; i <= n - len; i++) {
            int j = i + len - 1;
            dp[i][j] = Integer.MAX_VALUE;
            for (int k = i; k < j; k++)
                dp[i][j] = Math.min(dp[i][j],
                    dp[i][k] + dp[k+1][j] + dims[i] * dims[k+1] * dims[j+1]);
        }
    return dp[0][n - 1];
}
```

#### Example

```
dims=[10,30,5,60]  (matrices: 10×30, 30×5, 5×60)
dp[0][2] = min(
  split at k=0: 0 + dp[1][2] + 10*30*60 = 0+9000+18000=27000
  split at k=1: dp[0][1] + 0 + 10*5*60  = 1500+0+3000=4500
) = 4500 ✓
```

---

### Problem 24 — Strange Printer
**LeetCode #664 | Difficulty: Hard | Company: Google**

> dp[i][j] = min turns to print s[i..j].

#### Java code

```java
public int strangePrinter(String s) {
    int n = s.length();
    int[][] dp = new int[n][n];

    for (int i = n - 1; i >= 0; i--) {
        dp[i][i] = 1;
        for (int j = i + 1; j < n; j++) {
            dp[i][j] = dp[i][j-1] + 1;   // print s[j] separately
            for (int k = i; k < j; k++)
                if (s.charAt(k) == s.charAt(j))
                    dp[i][j] = Math.min(dp[i][j], dp[i][k] + (k+1 <= j-1 ? dp[k+1][j-1] : 0));
        }
    }
    return dp[0][n - 1];
}
```

---

### Problem 25 — Minimum Cost to Merge Stones
**LeetCode #1000 | Difficulty: Hard | Company: Google**

> Merge k consecutive piles each time. dp[i][j] = min cost to merge piles i..j into as few as possible.

#### Java code

```java
public int mergeStones(int[] stones, int k) {
    int n = stones.length;
    if ((n - 1) % (k - 1) != 0) return -1;

    int[] prefix = new int[n + 1];
    for (int i = 0; i < n; i++) prefix[i+1] = prefix[i] + stones[i];

    int[][] dp = new int[n][n];

    for (int len = k; len <= n; len++)
        for (int i = 0; i + len <= n; i++) {
            int j = i + len - 1;
            dp[i][j] = Integer.MAX_VALUE;
            for (int m = i; m < j; m += k - 1)
                dp[i][j] = Math.min(dp[i][j], dp[i][m] + dp[m+1][j]);
            if ((len - 1) % (k - 1) == 0)
                dp[i][j] += prefix[j+1] - prefix[i];
        }
    return dp[0][n-1];
}
```

---

### Problem 26 — Remove Boxes
**LeetCode #546 | Difficulty: Hard | Company: Google**

> dp[i][j][k] = max points removing boxes[i..j] with k boxes same color as boxes[i] attached to left.

#### Java code

```java
public int removeBoxes(int[] boxes) {
    int n = boxes.length;
    int[][][] dp = new int[n][n][n];
    return dfs(boxes, dp, 0, n-1, 0);
}
int dfs(int[] b, int[][][] dp, int i, int j, int k) {
    if (i > j) return 0;
    if (dp[i][j][k] != 0) return dp[i][j][k];

    // Extend k: if boxes to the right match boxes[i]
    while (i < j && b[i+1] == b[i]) { i++; k++; }

    // Remove current group of same-color boxes
    dp[i][j][k] = (k+1)*(k+1) + dfs(b, dp, i+1, j, 0);

    // Try attaching boxes[i] to a matching box further right
    for (int m = i+1; m <= j; m++)
        if (b[m] == b[i])
            dp[i][j][k] = Math.max(dp[i][j][k],
                dfs(b, dp, i+1, m-1, 0) + dfs(b, dp, m, j, k+1));

    return dp[i][j][k];
}
```

---

## Category 8 — Probability / Expectation DP

---

### Problem 27 — Knight Probability in Chessboard
**LeetCode #688 | Difficulty: Medium | Company: Google, Amazon**

> After k moves, probability knight still on n×n board.

#### Java code

```java
public double knightProbability(int n, int k, int row, int col) {
    double[][] dp = new double[n][n];
    dp[row][col] = 1.0;
    int[][] moves = {{-2,-1},{-2,1},{-1,-2},{-1,2},{1,-2},{1,2},{2,-1},{2,1}};

    for (int step = 0; step < k; step++) {
        double[][] next = new double[n][n];
        for (int r = 0; r < n; r++)
            for (int c = 0; c < n; c++)
                if (dp[r][c] > 0)
                    for (int[] m : moves) {
                        int nr = r + m[0], nc = c + m[1];
                        if (nr >= 0 && nr < n && nc >= 0 && nc < n)
                            next[nr][nc] += dp[r][c] / 8.0;
                    }
        dp = next;
    }
    double prob = 0;
    for (double[] row2 : dp) for (double v : row2) prob += v;
    return prob;
}
```

#### Example

```
n=3, k=2, row=0, col=0
Start: dp[0][0]=1.0
After 1 move: knight can go to (1,2) or (2,1) → each with prob 1/8
After 2 moves: from (1,2) and (2,1), check remaining on-board positions
Output: 0.0625 ✓
```

---

### Problem 28 — Dice Roll Simulation
**LeetCode #1223 | Difficulty: Medium | Company: Microsoft**

> Count sequences of length n where no face appears more than rollMax[i] times consecutively.

#### Java code

```java
public int dieSimulator(int n, int[] rollMax) {
    int MOD = 1_000_000_007;
    // dp[i][j] = ways to have j consecutive of face i at end of current sequence
    int[][] dp = new int[6][16];  // 6 faces, max consecutive = 15
    for (int i = 0; i < 6; i++) dp[i][1] = 1;  // first roll: each face once

    for (int roll = 2; roll <= n; roll++) {
        int[][] next = new int[6][16];
        for (int face = 0; face < 6; face++) {
            for (int cnt = 1; cnt <= rollMax[face]; cnt++) {
                if (dp[face][cnt] == 0) continue;
                // Roll a different face
                for (int nextFace = 0; nextFace < 6; nextFace++) {
                    if (nextFace != face)
                        next[nextFace][1] = (next[nextFace][1] + dp[face][cnt]) % MOD;
                }
                // Roll same face (extend streak)
                if (cnt + 1 <= rollMax[face])
                    next[face][cnt+1] = (next[face][cnt+1] + dp[face][cnt]) % MOD;
            }
        }
        dp = next;
    }
    int ans = 0;
    for (int[] face : dp) for (int v : face) ans = (ans + v) % MOD;
    return ans;
}
```

---

### Problem 29 — Soup Servings
**LeetCode #808 | Difficulty: Medium | Company: Google**

> 4 operations. Expected probability that A runs out first or both together. For large N → probability approaches 1.0.

#### Java code

```java
public double soupServings(int n) {
    if (n > 4800) return 1.0;   // probability converges to 1 for large n
    int m = (n + 24) / 25;      // scale down
    double[][] dp = new double[m + 1][m + 1];
    dp[0][0] = 1.0;

    for (int i = 0; i <= m; i++)
        for (int j = 0; j <= m; j++) {
            if (dp[i][j] == 0) continue;
            int[][] ops = {{4,0},{3,1},{2,2},{1,3}};
            for (int[] op : ops) {
                int na = Math.max(0, i - op[0]);
                int nb = Math.max(0, j - op[1]);
                dp[na][nb] += dp[i][j] / 4.0;
            }
        }
    // Wait — standard approach is memoization from original state
    // Simpler:
    return dp[0][0]; // placeholder
}

// Clean version with memoization
Map<String, Double> memo = new HashMap<>();
public double soupServings2(int n) {
    if (n > 4800) return 1.0;
    return prob(n, n);
}
private double prob(int a, int b) {
    if (a <= 0 && b <= 0) return 0.5;
    if (a <= 0) return 1.0;
    if (b <= 0) return 0.0;
    String key = a + "," + b;
    if (memo.containsKey(key)) return memo.get(key);
    double res = 0.25 * (prob(a-100,b) + prob(a-75,b-25) + prob(a-50,b-50) + prob(a-25,b-75));
    memo.put(key, res);
    return res;
}
```

---

### Problem 30 — New 21 Game
**LeetCode #837 | Difficulty: Medium | Company: Google**

> Start at 0, draw 1..maxPts each round, stop when score >= n. P(score <= maxN)?

#### Java code

```java
public double new21Game(int n, int k, int maxPts) {
    if (k == 0 || n >= k + maxPts) return 1.0;

    double[] dp = new double[n + 1];
    dp[0] = 1.0;
    double windowSum = 1.0;     // sum of dp in sliding window of size maxPts

    for (int i = 1; i <= n; i++) {
        dp[i] = windowSum / maxPts;
        if (i < k) windowSum += dp[i];           // still drawing: add to window
        if (i >= maxPts) windowSum -= dp[i - maxPts]; // remove oldest from window
    }

    double result = 0;
    for (int i = k; i <= n; i++) result += dp[i];
    return result;
}
```

#### Example

```
n=10, k=1, maxPts=10
dp[0]=1.0, windowSum=1.0
i=1: dp[1]=1/10=0.1, k=1 so don't add (i<k false), windowSum=1-0=1 (maxPts=10, i-10<0)
... dp[i] for 1<=i<=10 = 0.1 each
result = sum(dp[1..10]) = 1.0 ✓
```

---

### Problem 31 — Two Boxes
**LeetCode #1467 | Difficulty: Hard | Company: Amazon**

> Split 2*n balls (n red, n blue) equally into 2 boxes. P(each box has equal colors).

#### Java code

```java
public double getProbability(int[] balls) {
    int n = balls.length;
    int total = 0; for (int b : balls) total += b;
    int half = total / 2;

    // dp[i][j][d] = ways to put balls from colors 0..i-1
    //   with j balls in box1 and color-count difference d in box1 vs box2
    // Complex DP with multinomial coefficients
    // Simplified: use DFS with memoization

    long[] fact = new long[total + 1];
    fact[0] = 1;
    for (int i = 1; i <= total; i++) fact[i] = fact[i-1] * i;

    // Total ways to split (nCr approach)
    double[] result = new double[2];
    dfsBoxes(balls, 0, 0, 0, 0, 0, fact, result);
    return result[1] / result[0];
}

private void dfsBoxes(int[] balls, int idx, int box1, int box2, int types1, int types2,
                       long[] fact, double[] result) {
    int half = 0; for (int b : balls) half += b; half /= 2;
    if (box1 > half || box2 > half) return;

    if (idx == balls.length) {
        if (box1 == half && box2 == half) {
            result[0] += 1.0 / fact[box1] / fact[box2];
            if (types1 == types2) result[1] += 1.0 / fact[box1] / fact[box2];
        }
        return;
    }
    for (int i = 0; i <= balls[idx]; i++) {
        dfsBoxes(balls, idx+1, box1+i, box2+(balls[idx]-i),
                 types1+(i>0?1:0), types2+(balls[idx]-i>0?1:0), fact, result);
    }
}
```

---

## Category 9 — Bonus / Extra

---

### Problem 32 — Number of Ways (Climbing Stairs with variable steps)
**Variation | Difficulty: Easy | Pattern: Distinct Ways**

```java
// Generalization: can climb 1 to k steps at a time
public int climbStairs(int n, int k) {
    int[] dp = new int[n + 1];
    dp[0] = 1;
    for (int i = 1; i <= n; i++)
        for (int step = 1; step <= k && step <= i; step++)
            dp[i] += dp[i - step];
    return dp[n];
}
```

---

### Problem 33 — Num of Decodings II (Decode Ways II)
**LeetCode #639 | Difficulty: Hard**

```java
public int numDecodings(String s) {
    long MOD = 1_000_000_007;
    long[] dp = new long[s.length() + 1];
    dp[0] = 1;
    dp[1] = s.charAt(0) == '*' ? 9 : (s.charAt(0) == '0' ? 0 : 1);

    for (int i = 2; i <= s.length(); i++) {
        char c = s.charAt(i-1), p = s.charAt(i-2);
        // Single digit
        if (c == '*') dp[i] += 9 * dp[i-1];
        else if (c != '0') dp[i] += dp[i-1];
        // Two digits
        if (p == '*') {
            if (c == '*') dp[i] += 15 * dp[i-2];  // 11-19, 21-26
            else if (c <= '6') dp[i] += 2 * dp[i-2];
            else dp[i] += dp[i-2];
        } else if (p == '1') {
            if (c == '*') dp[i] += 9 * dp[i-2];
            else dp[i] += dp[i-2];
        } else if (p == '2') {
            if (c == '*') dp[i] += 6 * dp[i-2];
            else if (c <= '6') dp[i] += dp[i-2];
        }
        dp[i] %= MOD;
    }
    return (int) dp[s.length()];
}
```

---

### Problem 34 — Longest Palindromic Substring
**LeetCode #5 | Difficulty: Medium | Company: Amazon, Google**

```java
public String longestPalindrome(String s) {
    int n = s.length(), start = 0, maxLen = 1;
    boolean[][] dp = new boolean[n][n];
    for (int i = 0; i < n; i++) dp[i][i] = true;

    for (int len = 2; len <= n; len++)
        for (int i = 0; i <= n - len; i++) {
            int j = i + len - 1;
            if (s.charAt(i) == s.charAt(j)) {
                dp[i][j] = (len == 2) || dp[i+1][j-1];
                if (dp[i][j] && len > maxLen) { maxLen = len; start = i; }
            }
        }
    return s.substring(start, start + maxLen);
}
```

---

### Problem 35 — Word Break
**LeetCode #139 | Difficulty: Medium | Company: Amazon, Google**

```java
public boolean wordBreak(String s, List<String> wordDict) {
    Set<String> dict = new HashSet<>(wordDict);
    int n = s.length();
    boolean[] dp = new boolean[n + 1];
    dp[0] = true;

    for (int i = 1; i <= n; i++)
        for (int j = 0; j < i; j++)
            if (dp[j] && dict.contains(s.substring(j, i))) { dp[i] = true; break; }

    return dp[n];
}
```

---

### Problem 36 — Jump Game II
**LeetCode #45 | Difficulty: Medium | Company: Amazon, Google**

```java
public int jump(int[] nums) {
    int jumps = 0, curEnd = 0, farthest = 0;
    for (int i = 0; i < nums.length - 1; i++) {
        farthest = Math.max(farthest, i + nums[i]);
        if (i == curEnd) { jumps++; curEnd = farthest; }
    }
    return jumps;
}
```

---

### Problem 37 — House Robber II
**LeetCode #213 | Difficulty: Medium | Company: Amazon**

> Circle of houses — run House Robber twice: once excluding first, once excluding last.

```java
public int rob(int[] nums) {
    if (nums.length == 1) return nums[0];
    return Math.max(robRange(nums, 0, nums.length - 2),
                    robRange(nums, 1, nums.length - 1));
}
int robRange(int[] nums, int lo, int hi) {
    int prev2 = 0, prev1 = 0;
    for (int i = lo; i <= hi; i++) {
        int curr = Math.max(prev1, prev2 + nums[i]);
        prev2 = prev1; prev1 = curr;
    }
    return prev1;
}
```

---

### Problem 38 — Maximal Square
**LeetCode #221 | Difficulty: Medium | Company: Amazon, Google**

> dp[i][j] = side of largest square with bottom-right at (i,j).

```java
public int maximalSquare(char[][] matrix) {
    int m = matrix.length, n = matrix[0].length, maxSide = 0;
    int[][] dp = new int[m + 1][n + 1];

    for (int i = 1; i <= m; i++)
        for (int j = 1; j <= n; j++)
            if (matrix[i-1][j-1] == '1') {
                dp[i][j] = Math.min(dp[i-1][j], Math.min(dp[i][j-1], dp[i-1][j-1])) + 1;
                maxSide = Math.max(maxSide, dp[i][j]);
            }
    return maxSide * maxSide;
}
```

---

## Quick Pattern Reference

| Problem | Pattern | Key state / recurrence |
|---------|---------|----------------------|
| House Robber | Fibonacci DP | `max(prev1, prev2+nums[i])` |
| Max Subarray | Kadane DP | `max(nums[i], cur+nums[i])` |
| Decode Ways | 1D counting | `dp[i]+=dp[i-1]+dp[i-2]` |
| Coin Change | Min path | `dp[i]=min(dp[i-coin]+1)` |
| Min Path Sum | Grid DP | `dp[i][j]=grid+min(up,left)` |
| Min Falling Path | Grid DP | `dp[i][j]=matrix+min(3 above)` |
| Unique Paths | Grid count | `dp[i][j]=dp[i-1][j]+dp[i][j-1]` |
| 0/1 Knapsack | Knapsack | reverse capacity loop |
| Partition Equal Subset | 0/1 Knapsack | `dp[w] |= dp[w-num]` |
| Target Sum | 0/1 Knapsack | count subsets sum=(total+target)/2 |
| Ones and Zeroes | 2D Knapsack | reverse both dims |
| Last Stone Weight II | 0/1 Knapsack | find subset closest to total/2 |
| Coin Change II | Unbounded | forward capacity loop |
| Count Unique Digits | Counting DP | 9 × 9 × 8 × ... |
| LIS | Sequence DP | `dp[i]=max(dp[j]+1)` for j<i |
| Count Palindromic Subseq | Interval DP | depends on ends match/mismatch |
| LCS | String DP | match: diag+1, else max(up,left) |
| Edit Distance | String DP | replace/insert/delete |
| Longest Palindromic Subseq | String DP | match: diag+2, else max |
| Distinct Subsequences | String DP | use/skip s[i] for t[j] |
| Burst Balloons | Interval DP | think LAST balloon, dp[i][k]+arr[i]*arr[k]*arr[j]+dp[k][j] |
| Min Cut Stick | Interval DP | dp[i][j]=dp[i][k]+dp[k][j]+c[j]-c[i] |
| MCM | Interval DP | dp[i][j]=dp[i][k]+dp[k+1][j]+dims multiply |
| Strange Printer | Interval DP | merge same chars |
| Merge Stones | Interval DP | dp[i][j] over k steps of k-1 |
| Remove Boxes | 3D DP | dp[i][j][k] with k trailing same color |
| Knight Probability | Probability DP | dp[r][c] spread to 8 moves |
| Dice Simulation | State DP | face × consecutive count |
| Soup Servings | Probability DP | 4 operations, recurse with memo |
| New 21 Game | Sliding window DP | windowSum/maxPts |
| Two Boxes | Combinatorics DP | dfs over color splits |
