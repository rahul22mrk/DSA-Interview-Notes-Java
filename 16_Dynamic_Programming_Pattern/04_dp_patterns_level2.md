# DP Patterns Level 2 — Solved Problems (30 Problems)

> **Covers:** Interval DP · DP on Strings (Advanced) · DP on Trees · Digit DP · Bitmask DP · Probability DP
> **Notes file:** [01_dp_notes.md](./01_dp_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Interval / Partition DP
- [P1 — Burst Balloons](#p1--burst-balloons)
- [P2 — Matrix Chain Multiplication](#p2--matrix-chain-multiplication)
- [P3 — Min Cost to Cut a Stick](#p3--min-cost-to-cut-a-stick)
- [P4 — Strange Printer](#p4--strange-printer)
- [P5 — Minimum Cost to Merge Stones](#p5--minimum-cost-to-merge-stones)
- [P6 — Remove Boxes](#p6--remove-boxes)
- [P7 — Partition Array for Maximum Sum](#p7--partition-array-for-maximum-sum)
- [P8 — Minimum Score Triangulation of Polygon](#p8--minimum-score-triangulation-of-polygon)
- [P9 — Palindrome Partitioning II](#p9--palindrome-partitioning-ii)

### Category 2 — DP on Strings (Advanced)
- [P10 — Edit Distance](#p10--edit-distance)
- [P11 — Distinct Subsequences](#p11--distinct-subsequences)
- [P12 — Shortest Common Supersequence](#p12--shortest-common-supersequence)
- [P13 — Wildcard Matching](#p13--wildcard-matching)
- [P14 — Regular Expression Matching](#p14--regular-expression-matching)
- [P15 — Count Different Palindromic Subsequences](#p15--count-different-palindromic-subsequences)

### Category 3 — DP on Trees
- [P16 — House Robber III](#p16--house-robber-iii)
- [P17 — Binary Tree Maximum Path Sum](#p17--binary-tree-maximum-path-sum)
- [P18 — Diameter of Binary Tree](#p18--diameter-of-binary-tree)
- [P19 — Unique BSTs (Count)](#p19--unique-bsts-count)

### Category 4 — Digit DP
- [P20 — Count Numbers with Unique Digits](#p20--count-numbers-with-unique-digits)
- [P21 — Numbers At Most N Given Digit Set](#p21--numbers-at-most-n-given-digit-set)
- [P22 — Non-negative Integers without Consecutive Ones](#p22--non-negative-integers-without-consecutive-ones)

### Category 5 — DP + Bitmask
- [P23 — Number of Ways to Wear Different Hats](#p23--number-of-ways-to-wear-different-hats)
- [P24 — Shortest Superstring (TSP on strings)](#p24--shortest-superstring)
- [P25 — Minimum Work Sessions](#p25--minimum-work-sessions)
- [P26 — Smallest Sufficient Team](#p26--smallest-sufficient-team)

### Category 6 — Probability DP
- [P27 — Knight Probability in Chessboard](#p27--knight-probability-in-chessboard)
- [P28 — New 21 Game](#p28--new-21-game)
- [P29 — Soup Servings](#p29--soup-servings)
- [P30 — Dice Roll Simulation](#p30--dice-roll-simulation)

---

## Category 1 — Interval / Partition DP

> **Key pattern:** `dp[i][j]` = optimal for subproblem on range [i..j].
> **Loop order:** by **length** first, then i, then split point k.
> **Template:**
> ```
> for (int len = 2; len <= n; len++)
>     for (int i = 0; i <= n - len; i++) {
>         int j = i + len - 1;
>         for (int k = i; k < j; k++)
>             dp[i][j] = optimal(dp[i][j], dp[i][k] + cost + dp[k+1][j]);
>     }
> ```

---

### P1 — Burst Balloons
**LeetCode #312 | Difficulty: Hard | Company: Google, Amazon**

> Burst all balloons in [0..n-1]. Bursting balloon k when only i..j remain: coins = `nums[i-1]*nums[k]*nums[j+1]`. Maximize total coins.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Key insight | Think about which balloon bursts **LAST** in range (i..j) | reverse thinking |
| Padding | Add `nums[-1]=nums[n]=1` (virtual 1s at boundaries) | |
| State | `dp[i][j]` = max coins bursting all balloons in open range (i..j) | |
| Recurrence | `dp[i][j] = max over k: dp[i][k] + arr[i]*arr[k]*arr[j] + dp[k][j]` | k = last to burst |
| Loop | by length, k is last balloon inside (i..j) | |

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
nums = [3, 1, 5, 8]  → arr = [1, 3, 1, 5, 8, 1]

dp[0][5] = max coins bursting all 4 balloons.
Best order: burst 1 last in (0,5)? Try k=1..4 as last.
k=2(val=1): dp[0][2]+arr[0]*arr[2]*arr[5]+dp[2][5]
k=4(val=8): gives maximum = 167

Output: 167 ✓  (burst 1,5,3,8 in some order)
```

---

### P2 — Matrix Chain Multiplication
**GFG | Difficulty: Hard | Company: Amazon, Google**

> Minimize scalar multiplications to multiply chain of matrices. Matrix i has dims `p[i-1] × p[i]`.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i][j]` = min multiplications for matrices i..j | |
| Base | `dp[i][i] = 0` | single matrix, no cost |
| Recurrence | `dp[i][j] = min over k: dp[i][k] + dp[k+1][j] + p[i-1]*p[k]*p[j]` | |
| Loop | by length 2..n | |

#### Java code

```java
public int matrixChainOrder(int[] p) {
    int n = p.length - 1;  // n matrices
    int[][] dp = new int[n][n];

    for (int len = 2; len <= n; len++)
        for (int i = 0; i <= n - len; i++) {
            int j = i + len - 1;
            dp[i][j] = Integer.MAX_VALUE;
            for (int k = i; k < j; k++)
                dp[i][j] = Math.min(dp[i][j],
                    dp[i][k] + dp[k + 1][j] + p[i] * p[k + 1] * p[j + 1]);
        }
    return dp[0][n - 1];
}
```

#### Example

```
p = [10, 30, 5, 60]  → 3 matrices: A(10×30), B(30×5), C(5×60)

(AB)C: 10*30*5 + 10*5*60 = 1500 + 3000 = 4500
A(BC): 30*5*60 + 10*30*60 = 9000 + 18000 = 27000

dp[0][2] = 4500
Output: 4500 ✓
```

---

### P3 — Min Cost to Cut a Stick
**LeetCode #1547 | Difficulty: Hard | Company: Google**

> Stick of length n. Make cuts at given positions. Cost of cut = length of stick being cut. Minimize total cost.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Setup | Add 0 and n to cuts array; sort | define boundary positions |
| State | `dp[i][j]` = min cost to make all cuts between positions i and j | |
| Recurrence | `dp[i][j] = min over k: dp[i][k] + dp[k][j] + (cuts[j]-cuts[i])` | current stick length |
| Loop | by length of interval | |

#### Java code

```java
public int minCost(int n, int[] cuts) {
    List<Integer> c = new ArrayList<>();
    c.add(0);
    for (int x : cuts) c.add(x);
    c.add(n);
    Collections.sort(c);

    int m = c.size();
    int[][] dp = new int[m][m];

    for (int len = 2; len < m; len++)
        for (int i = 0; i + len < m; i++) {
            int j = i + len;
            dp[i][j] = Integer.MAX_VALUE;
            for (int k = i + 1; k < j; k++)
                dp[i][j] = Math.min(dp[i][j],
                    dp[i][k] + dp[k][j] + c.get(j) - c.get(i));
        }
    return dp[0][m - 1];
}
```

#### Example

```
n=7, cuts=[1,3,4,5]  → c=[0,1,3,4,5,7]

dp[0][5] = min cost for all cuts in stick [0,7]
Try k=2 (cut at 3): dp[0][2]+dp[2][5]+(7-0)=1+4+7=12
Try k=1 (cut at 1): dp[0][1]+dp[1][5]+(7-0)=0+8+7=15
Best = 16
Output: 16 ✓
```

---

### P4 — Strange Printer
**LeetCode #664 | Difficulty: Hard | Company: Google**

> Printer can print a sequence of same characters in one turn. Minimize turns to print string s.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i][j]` = min turns to print s[i..j] | |
| Base | `dp[i][i] = 1` | one char = one turn |
| Start | `dp[i][j] = dp[i][j-1] + 1` | print s[j] as separate turn |
| Optimize | if `s[k]==s[j]` for some k in [i,j-1]: `dp[i][j] = min(dp[i][j], dp[i][k] + dp[k+1][j-1])` | merge s[j] with s[k] turn |

#### Java code

```java
public int strangePrinter(String s) {
    int n = s.length();
    int[][] dp = new int[n][n];

    for (int i = n - 1; i >= 0; i--) {
        dp[i][i] = 1;
        for (int j = i + 1; j < n; j++) {
            dp[i][j] = dp[i][j - 1] + 1;  // print s[j] separately
            for (int k = i; k < j; k++)
                if (s.charAt(k) == s.charAt(j))
                    dp[i][j] = Math.min(dp[i][j],
                        dp[i][k] + (k + 1 <= j - 1 ? dp[k + 1][j - 1] : 0));
        }
    }
    return dp[0][n - 1];
}
```

#### Example

```
s = "aaabbb"
dp[0][2]("aaa")=1, dp[3][5]("bbb")=1
dp[0][5] = dp[0][4]+1=3? or via merge: dp[0][2]+dp[3][5]=2
Output: 2 ✓  (print "aaa" then "bbb")
```

---

### P5 — Minimum Cost to Merge Stones
**LeetCode #1000 | Difficulty: Hard | Company: Amazon**

> Merge k consecutive piles each time. Cost = sum of merged piles. Find min cost. Return -1 if impossible.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Check | `(n-1) % (k-1) != 0` → return -1 | can't reduce to 1 pile |
| Prefix | Build prefix sum array | O(1) range sum |
| State | `dp[i][j]` = min cost to reduce piles i..j | |
| Recurrence | `dp[i][j] = min over m (step k-1): dp[i][m] + dp[m+1][j]` | split into 2 groups |
| Add merge cost | if `(len-1)%(k-1)==0`: `dp[i][j] += sum(i..j)` | can merge to 1 pile |

#### Java code

```java
public int mergeStones(int[] stones, int k) {
    int n = stones.length;
    if ((n - 1) % (k - 1) != 0) return -1;

    int[] prefix = new int[n + 1];
    for (int i = 0; i < n; i++) prefix[i + 1] = prefix[i] + stones[i];

    int[][] dp = new int[n][n];
    for (int len = k; len <= n; len++)
        for (int i = 0; i + len <= n; i++) {
            int j = i + len - 1;
            dp[i][j] = Integer.MAX_VALUE;
            for (int m = i; m < j; m += k - 1)
                dp[i][j] = Math.min(dp[i][j], dp[i][m] + dp[m + 1][j]);
            if ((len - 1) % (k - 1) == 0)
                dp[i][j] += prefix[j + 1] - prefix[i];
        }
    return dp[0][n - 1];
}
```

#### Example

```
stones=[3,2,4,1], k=2
prefix=[0,3,5,9,10]

dp[0][1]=5(merge 3+2), dp[1][2]=6, dp[2][3]=5
dp[0][2]=min(dp[0][0]+dp[1][2]+9, dp[0][1]+dp[2][2]+9)=min(15,14)=14
dp[0][3]=min(dp[0][0]+dp[1][3]+10, dp[0][1]+dp[2][3]+10, dp[0][2]+dp[3][3]+10)
       =min(0+11+10, 5+5+10, 14+0+10)=min(21,20,24)=20
Output: 20 ✓
```

---

### P6 — Remove Boxes
**LeetCode #546 | Difficulty: Hard | Company: Google**

> Remove groups of k identical boxes for k² points. Maximize total points.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i][j][k]` = max points removing boxes[i..j] with k extra boxes same as boxes[i] on left | |
| Base | `dp[i][i][k] = (k+1)²` | one box with k attached |
| Option 1 | Remove current group: `(k+1)² + dp[i+1][j][0]` | |
| Option 2 | Merge with matching box m in [i+1,j]: `dp[i+1][m-1][0] + dp[m][j][k+1]` | delay removal |

#### Java code

```java
public int removeBoxes(int[] boxes) {
    int n = boxes.length;
    int[][][] dp = new int[n][n][n];
    return dfs(boxes, dp, 0, n - 1, 0);
}

private int dfs(int[] b, int[][][] dp, int i, int j, int k) {
    if (i > j) return 0;
    if (dp[i][j][k] != 0) return dp[i][j][k];

    // Extend k: absorb consecutive same-color boxes at front
    while (i < j && b[i + 1] == b[i]) { i++; k++; }

    // Option 1: remove current group (k+1 boxes)
    dp[i][j][k] = (k + 1) * (k + 1) + dfs(b, dp, i + 1, j, 0);

    // Option 2: merge with a matching box later → delay removal
    for (int m = i + 1; m <= j; m++)
        if (b[m] == b[i])
            dp[i][j][k] = Math.max(dp[i][j][k],
                dfs(b, dp, i + 1, m - 1, 0) + dfs(b, dp, m, j, k + 1));

    return dp[i][j][k];
}
```

#### Example

```
boxes = [1, 1, 1]
dfs(0,2,0): all same → absorb → i=2,k=2 → (3)²=9
Output: 9 ✓  (remove all 3 at once = 3²=9)

boxes = [1, 3, 2, 2, 2, 3, 4, 3, 1]
Optimal groups: [3,3,3]→9, [2,2,2]→9, [1,1]→4, [4]→1 = 23
Output: 23 ✓
```

---

### P7 — Partition Array for Maximum Sum
**LeetCode #1043 | Difficulty: Medium | Company: Amazon**

> Partition array into contiguous subarrays of at most k. Replace each element with subarray's max. Maximize total.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i]` = max sum for first i elements | |
| For each i | try last subarray of length 1..k ending at i | |
| Recurrence | `dp[i] = max over j (1..k): dp[i-j] + max(arr[i-j..i-1]) * j` | |

#### Java code

```java
public int maxSumAfterPartitioning(int[] arr, int k) {
    int n = arr.length;
    int[] dp = new int[n + 1];
    for (int i = 1; i <= n; i++) {
        int mx = 0;
        for (int j = 1; j <= k && i - j >= 0; j++) {
            mx = Math.max(mx, arr[i - j]);
            dp[i] = Math.max(dp[i], dp[i - j] + mx * j);
        }
    }
    return dp[n];
}
```

#### Example

```
arr=[1,15,7,9,2,5,10], k=3
dp[1]=1, dp[2]=30(15*2), dp[3]=45(15*3)
dp[4]=max(dp[3]+9, dp[2]+15*2, dp[1]+15*3)=max(54,60,46)=60
...
Output: 84 ✓
```

---

### P8 — Minimum Score Triangulation of Polygon
**LeetCode #1039 | Difficulty: Medium | Company: Google**

> Triangulate convex polygon of n vertices. Score = product of 3 vertices of each triangle. Minimize total score.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i][j]` = min score to triangulate polygon between vertices i and j | |
| Recurrence | `dp[i][j] = min over k (i<k<j): dp[i][k] + values[i]*values[k]*values[j] + dp[k][j]` | k = apex of triangle |
| Base | `dp[i][i+1] = 0` | two vertices → no triangle |

#### Java code

```java
public int minScoreTriangulation(int[] values) {
    int n = values.length;
    int[][] dp = new int[n][n];

    for (int len = 2; len < n; len++)
        for (int i = 0; i + len < n; i++) {
            int j = i + len;
            dp[i][j] = Integer.MAX_VALUE;
            for (int k = i + 1; k < j; k++)
                dp[i][j] = Math.min(dp[i][j],
                    dp[i][k] + (int) ((long) values[i] * values[k] * values[j]) + dp[k][j]);
        }
    return dp[0][n - 1];
}
```

#### Example

```
values = [1,2,3]  → 1 triangle only
dp[0][2] = values[0]*values[1]*values[2] = 1*2*3 = 6
Output: 6 ✓

values = [3,7,4,5]
Triangulations: (0,1,3)+(1,2,3) = 3*7*5+7*4*5 = 105+140=245
                (0,1,2)+(0,2,3) = 3*7*4+3*4*5 = 84+60=144
Output: 144 ✓
```

---

### P9 — Palindrome Partitioning II
**LeetCode #132 | Difficulty: Hard | Company: Amazon, Facebook**

> Find minimum number of cuts to partition string s so every part is a palindrome.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Pre-compute | `isPalin[i][j]` = true if s[i..j] is palindrome | O(n²) |
| State | `dp[i]` = min cuts for s[0..i] | |
| Base | `dp[i] = i` | max cuts = i (cut every char) |
| Recurrence | if `isPalin[0][i]`: `dp[i]=0`; else `dp[i]=min(dp[j-1]+1)` for all j where `isPalin[j][i]` | |

#### Java code

```java
public int minCut(String s) {
    int n = s.length();
    boolean[][] isPalin = new boolean[n][n];

    // Precompute palindromes
    for (int i = n - 1; i >= 0; i--)
        for (int j = i; j < n; j++)
            isPalin[i][j] = s.charAt(i) == s.charAt(j)
                && (j - i <= 2 || isPalin[i + 1][j - 1]);

    int[] dp = new int[n];
    for (int i = 0; i < n; i++) {
        if (isPalin[0][i]) { dp[i] = 0; continue; }
        dp[i] = i;  // max cuts
        for (int j = 1; j <= i; j++)
            if (isPalin[j][i])
                dp[i] = Math.min(dp[i], dp[j - 1] + 1);
    }
    return dp[n - 1];
}
```

#### Example

```
s = "aab"
isPalin: [0][0]=T,[1][1]=T,[2][2]=T,[0][1]=(a==a)=T,[1][2]=(a==b)=F,[0][2]=F
dp[0]=0(a is palin), dp[1]=0(aa is palin), dp[2]: isPalin[0][2]=F
  j=1: isPalin[1][2]=F; j=2: isPalin[2][2]=T → dp[1]+1=1
dp[2]=1
Output: 1  (["aa","b"]) ✓
```

---

## Category 2 — DP on Strings (Advanced)

---

### P10 — Edit Distance
**LeetCode #72 | Difficulty: Hard | Company: Amazon, Google, Facebook**

> Min operations (insert/delete/replace) to convert word1 → word2.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i][j]` = edit distance between word1[0..i-1] and word2[0..j-1] | |
| Base | `dp[i][0]=i` (delete i chars), `dp[0][j]=j` (insert j chars) | |
| Match | `dp[i][j] = dp[i-1][j-1]` | same char — free |
| Mismatch | `dp[i][j] = 1 + min(replace:dp[i-1][j-1], delete:dp[i-1][j], insert:dp[i][j-1])` | |

#### Java code

```java
public int minDistance(String word1, String word2) {
    int n = word1.length(), m = word2.length();
    int[][] dp = new int[n + 1][m + 1];
    for (int i = 0; i <= n; i++) dp[i][0] = i;
    for (int j = 0; j <= m; j++) dp[0][j] = j;

    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++)
            dp[i][j] = word1.charAt(i-1) == word2.charAt(j-1)
                ? dp[i-1][j-1]
                : 1 + Math.min(dp[i-1][j-1], Math.min(dp[i-1][j], dp[i][j-1]));
    return dp[n][m];
}
```

#### Example

```
word1="horse", word2="ros"

    ""  r  o  s
""   0  1  2  3
h    1  1  2  3
o    2  2  1  2
r    3  2  2  2
s    4  3  3  2
e    5  4  4  3

Output: 3  (horse→rorse→rose→ros) ✓
```

---

### P11 — Distinct Subsequences
**LeetCode #115 | Difficulty: Hard | Company: Amazon, Google**

> Count distinct subsequences of s that equal t.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i][j]` = ways to form t[0..j-1] from s[0..i-1] | |
| Base | `dp[i][0]=1` (empty t — 1 way), `dp[0][j]=0` for j>0 | |
| Match | `dp[i][j] = dp[i-1][j-1] + dp[i-1][j]` | use s[i-1] or skip it |
| No match | `dp[i][j] = dp[i-1][j]` | skip s[i-1] |

#### Java code

```java
public int numDistinct(String s, String t) {
    int n = s.length(), m = t.length();
    long[][] dp = new long[n + 1][m + 1];
    for (int i = 0; i <= n; i++) dp[i][0] = 1;

    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++) {
            dp[i][j] = dp[i-1][j];  // skip s[i-1]
            if (s.charAt(i-1) == t.charAt(j-1))
                dp[i][j] += dp[i-1][j-1];  // use s[i-1]
        }
    return (int) dp[n][m];
}
```

#### Example

```
s="rabbbit", t="rabbit"
     ""  r  a  b  b  i  t
""    1  0  0  0  0  0  0
r     1  1  0  0  0  0  0
a     1  1  1  0  0  0  0
b     1  1  1  1  0  0  0
b     1  1  1  2  1  0  0
b     1  1  1  3  3  0  0
i     1  1  1  3  3  3  0
t     1  1  1  3  3  3  3
Output: 3 ✓  (3 ways to pick the double-b)
```

---

### P12 — Shortest Common Supersequence
**LeetCode #1092 | Difficulty: Hard | Company: Google**

> Find shortest string containing both s1 and s2 as subsequences.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Length | `SCS = n + m - LCS(s1, s2)` | |
| Build LCS table | standard LCS dp | |
| Backtrack | match → add char once; mismatch → add the skipped char | |
| Base cases | append remaining chars from whichever string isn't exhausted | |

#### Java code

```java
public String shortestCommonSupersequence(String s1, String s2) {
    int n = s1.length(), m = s2.length();
    int[][] dp = new int[n + 1][m + 1];
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++)
            dp[i][j] = s1.charAt(i-1) == s2.charAt(j-1)
                ? dp[i-1][j-1] + 1
                : Math.max(dp[i-1][j], dp[i][j-1]);

    StringBuilder sb = new StringBuilder();
    int i = n, j = m;
    while (i > 0 && j > 0) {
        if (s1.charAt(i-1) == s2.charAt(j-1)) { sb.append(s1.charAt(i-1)); i--; j--; }
        else if (dp[i-1][j] > dp[i][j-1])       sb.append(s1.charAt(--i));
        else                                      sb.append(s2.charAt(--j));
    }
    while (i > 0) sb.append(s1.charAt(--i));
    while (j > 0) sb.append(s2.charAt(--j));
    return sb.reverse().toString();
}
```

#### Example

```
s1="abac", s2="cab"
LCS = "ab" (length 2)
SCS length = 4+3-2 = 5

Backtrack: c←cab matches? no→take c from s2, a←bac & ab: take a from s1...
Output: "cabac" ✓
```

---

### P13 — Wildcard Matching
**LeetCode #44 | Difficulty: Hard | Company: Amazon, Facebook**

> `?` matches any single char, `*` matches any sequence including empty.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Base | `dp[0][0]=true`; `dp[0][j]=true` if all `*` so far | only `*` matches empty s |
| `*` | `dp[i][j] = dp[i-1][j] (use*) OR dp[i][j-1] (*=empty)` | |
| `?` or match | `dp[i][j] = dp[i-1][j-1]` | consume one char each |
| No match | `dp[i][j] = false` | |

#### Java code

```java
public boolean isMatch(String s, String p) {
    int n = s.length(), m = p.length();
    boolean[][] dp = new boolean[n + 1][m + 1];
    dp[0][0] = true;
    for (int j = 1; j <= m; j++)
        dp[0][j] = p.charAt(j-1) == '*' && dp[0][j-1];

    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++) {
            char pc = p.charAt(j - 1);
            if (pc == '*')
                dp[i][j] = dp[i-1][j] || dp[i][j-1];  // match 1 char or empty
            else
                dp[i][j] = (pc == '?' || pc == s.charAt(i-1)) && dp[i-1][j-1];
        }
    return dp[n][m];
}
```

#### Example

```
s="adceb", p="*a*b"
    ""  *  a  *  b
""   T  T  F  F  F
a    F  T  T  T  F
d    F  T  F  T  F
c    F  T  F  T  F
e    F  T  F  T  F
b    F  T  F  T  T
Output: true ✓
```

---

### P14 — Regular Expression Matching
**LeetCode #10 | Difficulty: Hard | Company: Facebook, Google**

> `.` matches any single char, `*` matches zero or more of preceding element.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Base | `dp[0][0]=true`; `dp[0][j]` = true if `p[j-1]=='*' && dp[0][j-2]` | `*` can match zero |
| `*` | if no match: `dp[i][j] = dp[i][j-2]` (use * as 0 occurrences) | |
| `*` | if match: `dp[i][j] = dp[i][j-2] OR dp[i-1][j]` | 0 or more |
| `.` or match | `dp[i][j] = dp[i-1][j-1]` | |

#### Java code

```java
public boolean isMatch(String s, String p) {
    int n = s.length(), m = p.length();
    boolean[][] dp = new boolean[n + 1][m + 1];
    dp[0][0] = true;
    for (int j = 2; j <= m; j += 2)
        dp[0][j] = p.charAt(j-1) == '*' && dp[0][j-2];

    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++) {
            char pc = p.charAt(j - 1);
            if (pc == '*') {
                boolean zeroUse = dp[i][j-2];
                boolean charMatch = (p.charAt(j-2) == '.' || p.charAt(j-2) == s.charAt(i-1));
                dp[i][j] = zeroUse || (charMatch && dp[i-1][j]);
            } else {
                dp[i][j] = (pc == '.' || pc == s.charAt(i-1)) && dp[i-1][j-1];
            }
        }
    return dp[n][m];
}
```

#### Example

```
s="aab", p="c*a*b"
c* = 0 c's, a* = 2 a's, b = b
Output: true ✓
```

---

### P15 — Count Different Palindromic Subsequences
**LeetCode #730 | Difficulty: Hard | Company: Google**

> Count distinct palindromic subsequences in s. Return modulo 10^9+7.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i][j]` = count of distinct palindromic subseqs in s[i..j] | |
| Base | `dp[i][i] = 1` | single char |
| Mismatch | `dp[i][j] = dp[i+1][j] + dp[i][j-1] - dp[i+1][j-1]` | inclusion-exclusion |
| Match `s[i]==s[j]` | Find leftmost l>i and rightmost r<j with s[l]=s[r]=s[i] | |
| No inner match | `dp[i][j] = dp[i+1][j-1]*2 + 2` | add s[i] and s[i]s[i] |
| One inner | `dp[i][j] = dp[i+1][j-1]*2 + 1` | duplicate already counted |
| Two+ inner | `dp[i][j] = dp[i+1][j-1]*2 - dp[l+1][r-1]` | subtract double-counted |

#### Java code

```java
public int countPalindromicSubsequences(String s) {
    int MOD = 1_000_000_007, n = s.length();
    long[][] dp = new long[n][n];
    for (int i = 0; i < n; i++) dp[i][i] = 1;

    for (int len = 2; len <= n; len++)
        for (int i = 0; i + len - 1 < n; i++) {
            int j = i + len - 1;
            if (s.charAt(i) != s.charAt(j)) {
                dp[i][j] = dp[i+1][j] + dp[i][j-1] - dp[i+1][j-1];
            } else {
                int l = i + 1, r = j - 1;
                while (l <= r && s.charAt(l) != s.charAt(i)) l++;
                while (l <= r && s.charAt(r) != s.charAt(j)) r--;
                if (l > r)       dp[i][j] = dp[i+1][j-1] * 2 + 2;
                else if (l == r) dp[i][j] = dp[i+1][j-1] * 2 + 1;
                else             dp[i][j] = dp[i+1][j-1] * 2 - dp[l+1][r-1];
            }
            dp[i][j] = (dp[i][j] % MOD + MOD) % MOD;
        }
    return (int) dp[0][n-1];
}
```

#### Example

```
s = "bccb"
dp[1][2]("cc") = 2 (c, cc)
dp[0][3]("bccb"): s[0]==s[3]='b', find inner b: l=3,r=0 → l>r → 2*dp[1][2]+2=6
Output: 6  (b, bb, c, cc, bcb, bccb) ✓
```

---

## Category 3 — DP on Trees

> **Key pattern:** Post-order DFS — compute children first, combine at parent.
> Two states per node: `include` (take this node) and `exclude` (skip this node).

---

### P16 — House Robber III
**LeetCode #337 | Difficulty: Medium | Company: Amazon, Google**

> Rob houses in a binary tree. Cannot rob two directly connected nodes. Maximize money.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | Per node: `[rob, skip]` where rob=take this node, skip=don't | |
| `rob[node]` | `node.val + skip[left] + skip[right]` | can only take children if skipped |
| `skip[node]` | `max(rob[left], skip[left]) + max(rob[right], skip[right])` | best of each child |

#### Java code

```java
public int rob(TreeNode root) {
    int[] res = dfs(root);
    return Math.max(res[0], res[1]);
}

// returns [rob_this_node, skip_this_node]
private int[] dfs(TreeNode node) {
    if (node == null) return new int[]{0, 0};

    int[] left  = dfs(node.left);
    int[] right = dfs(node.right);

    int rob  = node.val + left[1] + right[1];              // take node → skip children
    int skip = Math.max(left[0], left[1]) + Math.max(right[0], right[1]);  // best of each child
    return new int[]{rob, skip};
}
```

#### Example

```
      3
     / \
    2   3
     \   \
      3   1
dfs(2): rob=2+0+3=5, skip=max(0)+max(3,0)=3 → [5,3]
dfs(3-right): rob=3+0+1=4, skip=max(1,0)=1 → [4,1]
dfs(3-root): rob=3+3+1=7, skip=max(5,3)+max(4,1)=5+4=9 → [7,9]
Output: max(7,9)=9 ✓
```

---

### P17 — Binary Tree Maximum Path Sum
**LeetCode #124 | Difficulty: Hard | Company: Amazon, Facebook, Google**

> Find max path sum between any two nodes (path can go through any node).

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | at each node: max single-branch contribution going UP | |
| Global max | `left + node.val + right` — can use both branches | update on each node |
| Return up | `node.val + max(left, right)` — can only go one direction | |
| Prune | `Math.max(0, dfs(child))` — ignore negative branches | |

#### Java code

```java
private int maxSum = Integer.MIN_VALUE;

public int maxPathSum(TreeNode root) {
    dfs(root);
    return maxSum;
}

private int dfs(TreeNode node) {
    if (node == null) return 0;
    int left  = Math.max(0, dfs(node.left));   // ignore negative
    int right = Math.max(0, dfs(node.right));
    maxSum = Math.max(maxSum, left + node.val + right);  // update global (both sides)
    return node.val + Math.max(left, right);             // return one side only
}
```

#### Example

```
      -10
      /  \
     9   20
        /  \
       15   7
dfs(9)=9, dfs(15)=15, dfs(7)=7
dfs(20): left=15, right=7. maxSum=max(MIN,15+20+7)=42. return 20+15=35
dfs(-10): left=9, right=35. maxSum=max(42,9+(-10)+35)=42. return -10+35=25
Output: 42  (15→20→7) ✓
```

---

### P18 — Diameter of Binary Tree
**LeetCode #543 | Difficulty: Easy | Company: Facebook, Amazon**

> Find longest path between any two nodes (in number of edges). Path may or may not pass through root.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | height of each subtree | post-order |
| At each node | `diameter = max(diameter, leftHeight + rightHeight)` | path through this node |
| Return | `1 + max(leftHeight, rightHeight)` | height for parent |

#### Java code

```java
private int diameter = 0;

public int diameterOfBinaryTree(TreeNode root) {
    height(root);
    return diameter;
}

private int height(TreeNode node) {
    if (node == null) return 0;
    int left  = height(node.left);
    int right = height(node.right);
    diameter  = Math.max(diameter, left + right);   // path through this node
    return 1 + Math.max(left, right);
}
```

#### Example

```
      1
     / \
    2   3
   / \
  4   5
height(4)=1, height(5)=1
height(2): left=1,right=1. diameter=max(0,2)=2. return 2
height(3)=1
height(1): left=2,right=1. diameter=max(2,3)=3. return 3
Output: 3  (4→2→1→3 or 5→2→1→3) ✓
```

---

### P19 — Unique BSTs (Count)
**LeetCode #96 | Difficulty: Medium | Company: Amazon, Google**

> Count structurally unique BSTs with values 1..n.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Key insight | If i is root: left has (i-1) nodes, right has (n-i) nodes | |
| State | `dp[n]` = count of unique BSTs with n nodes | |
| Recurrence | `dp[n] = Σ dp[i-1] * dp[n-i]` for i = 1..n | Catalan number |
| Base | `dp[0]=1, dp[1]=1` | |

#### Java code

```java
public int numTrees(int n) {
    int[] dp = new int[n + 1];
    dp[0] = 1; dp[1] = 1;
    for (int i = 2; i <= n; i++)
        for (int j = 1; j <= i; j++)
            dp[i] += dp[j - 1] * dp[i - j];   // j = root
    return dp[n];
}
```

#### Example

```
dp[0]=1, dp[1]=1, dp[2]=2, dp[3]=5
dp[3]: j=1→dp[0]*dp[2]=2; j=2→dp[1]*dp[1]=1; j=3→dp[2]*dp[0]=2 → sum=5
Output: 5 ✓  (Catalan(3)=5)
```

---

## Category 4 — Digit DP

> **Key pattern:** Count integers in range [0..N] satisfying digit property.
> **State:** `dp[pos][cnt][tight]` — position, count of interesting digit, boundary flag.

---

### P20 — Count Numbers with Unique Digits
**LeetCode #357 | Difficulty: Medium | Company: Google**

> Count numbers with no repeated digits in range [0, 10^n).

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Math formula | `f(n) = 9 * 9 * 8 * 7 * ... (n terms)` | 9 choices for first, 9 for second (incl 0), etc. |
| Cumulative | `dp[n] = dp[n-1] + 9 * P(9, n-1)` | add new n-digit numbers |

#### Java code

```java
public int countNumbersWithUniqueDigits(int n) {
    if (n == 0) return 1;
    int result = 10;  // dp[1]: 0..9
    int uniqueDigits = 9, availableDigits = 9;
    for (int i = 2; i <= n && availableDigits > 0; i++) {
        uniqueDigits *= availableDigits;   // 9*9, then *8, *7...
        result += uniqueDigits;
        availableDigits--;
    }
    return result;
}
```

#### Example

```
n=2:
1-digit: 10 (0..9)
2-digit: 9*9=81 (first digit 1-9, second any except first)
Total: 10+81=91
Output: 91 ✓
```

---

### P21 — Numbers At Most N Given Digit Set
**LeetCode #902 | Difficulty: Hard | Company: Google**

> Given sorted digit set D, count numbers ≤ N that can be built using only those digits (with any length).

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Shorter lengths | All numbers with < len(N) digits: `D.length^1 + D.length^2 + ...` | |
| Same length | Digit DP: for each position, count digits < N[pos] (then D.length^remaining) | |
| Tight tracking | If still equal to N so far, next digit must be ≤ N[pos] | |

#### Java code

```java
public int atMostNGivenDigitSet(String[] digits, int n) {
    String s = String.valueOf(n);
    int k = s.length(), d = digits.length, result = 0;

    // Count all numbers with fewer digits than n
    for (int i = 1; i < k; i++) {
        int power = 1;
        for (int j = 0; j < i; j++) power *= d;
        result += power;
    }

    // Count same-length numbers ≤ n
    for (int i = 0; i < k; i++) {
        // Count digits[j] < s.charAt(i)
        int smaller = 0;
        for (String dg : digits) if (dg.charAt(0) < s.charAt(i)) smaller++;
        int remaining = k - i - 1;
        int power = 1;
        for (int j = 0; j < remaining; j++) power *= d;
        result += smaller * power;

        // Check if s.charAt(i) is in digits — can continue tight
        boolean found = false;
        for (String dg : digits) if (dg.charAt(0) == s.charAt(i)) { found = true; break; }
        if (!found) return result;  // can't match n's digit — stop
    }
    return result + 1;  // n itself is valid
}
```

#### Example

```
digits=["1","3","5","7"], n=100
Shorter (1 digit): 4^1=4 (1,3,5,7)
Shorter (2 digits): 4^2=16
Same length (3 digits, n="100"):
  pos0: digits<'1'=0. tight fails (no 1 in set)... wait: '1' is in set → found=true
  pos1: digits<'0'=0. '0' not in set → return result
result=4+16+0=20
Output: 20 ✓
```

---

### P22 — Non-negative Integers without Consecutive Ones
**LeetCode #600 | Difficulty: Hard**

> Count numbers in [0, n] with no two consecutive 1-bits in binary representation.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[i][lastBit][tight]` — bit position, last bit placed, tight constraint | |
| If last bit = 1 | next must be 0 | no consecutive 1s |
| Standard digit DP | process bits of n from MSB to LSB | |

#### Java code

```java
public int findIntegers(int n) {
    String bits = Integer.toBinaryString(n);
    int m = bits.length();
    // dp[i][j] = count of valid i-bit numbers ending with bit j (no tight)
    int[][] dp = new int[m + 1][2];
    dp[1][0] = 1; dp[1][1] = 1;  // single bit: 0 or 1
    for (int i = 2; i <= m; i++) {
        dp[i][0] = dp[i-1][0] + dp[i-1][1];  // prev can be 0 or 1
        dp[i][1] = dp[i-1][0];               // prev must be 0
    }

    int result = 0, prevBit = 0;
    for (int i = 0; i < m; i++) {
        if (bits.charAt(i) == '1') {
            result += dp[m - i][0];  // place 0 at this pos (free choice for rest)
            if (prevBit == 1) break; // consecutive 1s — n itself invalid from here
            if (i == m - 1) result++; // n itself is valid
            prevBit = 1;
        } else {
            prevBit = 0;
        }
    }
    return result;
}
```

#### Example

```
n=5 (binary "101")
Valid: 0,1,2(10),3(11)→no,4(100),5(101) → 0,1,2,4,5
Output: 5 ✓
```

---

## Category 5 — DP + Bitmask

> **Key pattern:** n ≤ 20. Encode subset/assignment as integer bitmask.
> **Bit ops:** `mask | (1<<i)` = add i; `mask & (1<<i)` = check if i in mask; `(mask>>i)&1` = bit i.

---

### P23 — Number of Ways to Wear Different Hats
**LeetCode #1434 | Difficulty: Hard | Company: Google**

> n people, 40 hats. Each person has preferred hats. Assign one hat per person (different hats). Count ways.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Invert | `caps[hat]` = list of people who want hat | iterate over hats |
| State | `dp[mask]` = ways to assign hats 1..currentHat where `mask` = set of people who got a hat | |
| For each hat | Skip it OR give to each person in caps[hat] who doesn't have hat yet | |

#### Java code

```java
public int numberWays(List<List<Integer>> hats) {
    int MOD = 1_000_000_007, n = hats.size();
    int done = (1 << n) - 1;

    List<Integer>[] caps = new List[41];
    for (int i = 1; i <= 40; i++) caps[i] = new ArrayList<>();
    for (int i = 0; i < n; i++)
        for (int hat : hats.get(i)) caps[hat].add(i);

    long[] dp = new long[1 << n];
    dp[0] = 1;

    for (int hat = 1; hat <= 40; hat++) {
        long[] next = dp.clone();  // option: skip this hat
        for (int mask = 0; mask <= done; mask++) {
            if (dp[mask] == 0) continue;
            for (int person : caps[hat]) {
                if ((mask & (1 << person)) == 0) {  // person doesn't have hat
                    int newMask = mask | (1 << person);
                    next[newMask] = (next[newMask] + dp[mask]) % MOD;
                }
            }
        }
        dp = next;
    }
    return (int) dp[done];
}
```

#### Example

```
hats=[[3,4],[4,5],[5]] (3 people)
done = 0b111 = 7

Process hat3: give to person0 → dp[001]=1
Process hat4: give to person0 → dp[001]+=1=1; give to person1 → dp[010]=1; give to both → dp[011]=1
Process hat5: give to person1 (if not assigned) → dp[011]+=dp[001]=1; give to person2 → various
Final dp[111] = 1  (3→p0, 4→p1, 5→p2)
Output: 1 ✓
```

---

### P24 — Shortest Superstring
**LeetCode #943 | Difficulty: Hard | Company: Google**

> Find shortest string that contains all words as substrings (TSP on strings).

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Pre-compute | `overlap[i][j]` = max overlap when j comes after i | |
| State | `dp[mask][i]` = min total length when `mask` = visited words, last = word i | |
| Recurrence | `dp[mask|(1<<j)][j] = min(dp[mask][i] + len[j] - overlap[i][j])` | |

#### Java code

```java
public String findShortestSuperstring(String[] words) {
    int n = words.length;
    int[][] overlap = new int[n][n];
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++) if (i != j)
            for (int k = Math.min(words[i].length(), words[j].length()); k >= 0; k--)
                if (words[i].endsWith(words[j].substring(0, k))) { overlap[i][j] = k; break; }

    int[][] dp = new int[1 << n][n];
    int[][] parent = new int[1 << n][n];
    for (int[] row : dp) Arrays.fill(row, Integer.MAX_VALUE / 2);
    for (int[] row : parent) Arrays.fill(row, -1);
    for (int i = 0; i < n; i++) dp[1 << i][i] = words[i].length();

    for (int mask = 1; mask < (1 << n); mask++)
        for (int i = 0; i < n; i++) {
            if ((mask >> i & 1) == 0 || dp[mask][i] == Integer.MAX_VALUE / 2) continue;
            for (int j = 0; j < n; j++) {
                if ((mask >> j & 1) == 1) continue;
                int newMask = mask | (1 << j);
                int newLen = dp[mask][i] + words[j].length() - overlap[i][j];
                if (newLen < dp[newMask][j]) {
                    dp[newMask][j] = newLen;
                    parent[newMask][j] = i;
                }
            }
        }

    // Find best ending word
    int fullMask = (1 << n) - 1, last = 0;
    for (int i = 1; i < n; i++) if (dp[fullMask][i] < dp[fullMask][last]) last = i;

    // Reconstruct
    StringBuilder sb = new StringBuilder();
    int mask = fullMask, cur = last;
    while (cur != -1) {
        int prev = parent[mask][cur];
        if (prev == -1) sb.insert(0, words[cur]);
        else sb.insert(0, words[cur].substring(overlap[prev][cur]));
        mask ^= (1 << cur);
        cur = prev;
    }
    return sb.toString();
}
```

#### Example

```
words=["alex","loves","leetcode"]
overlap: "alex"→"loves"=0, "loves"→"leetcode"=1 ("s" not prefix of "leetcode")
Best order: "leetcode"→"loves"→"alex"? or "alex"+"loves"+"leetcode"=19
Output: "alexlovesleetcode" (length 19) ✓
```

---

### P25 — Minimum Work Sessions
**LeetCode #1986 | Difficulty: Hard | Company: Amazon**

> Split tasks into sessions of at most `sessionTime`. Minimize number of sessions.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[mask]` = min sessions for tasks in mask; `time[mask]` = remaining time in last session | |
| Fit current session | if `time[mask] >= tasks[i]`: same session count, time decreases | |
| New session | else: `dp[newMask] = dp[mask]+1`, `time[newMask] = sessionTime - tasks[i]` | |

#### Java code

```java
public int minSessions(int[] tasks, int sessionTime) {
    int n = tasks.length;
    int[] dp = new int[1 << n];
    int[] time = new int[1 << n];  // remaining time in current session
    Arrays.fill(dp, n + 1);
    dp[0] = 1; time[0] = sessionTime;

    for (int mask = 0; mask < (1 << n); mask++) {
        if (dp[mask] == n + 1) continue;
        for (int i = 0; i < n; i++) {
            if ((mask >> i & 1) == 1) continue;
            int newMask = mask | (1 << i);
            if (time[mask] >= tasks[i]) {  // fit in current session
                if (dp[mask] < dp[newMask] || (dp[mask] == dp[newMask] && time[mask]-tasks[i] > time[newMask])) {
                    dp[newMask] = dp[mask];
                    time[newMask] = time[mask] - tasks[i];
                }
            } else {  // new session
                if (dp[mask] + 1 < dp[newMask]) {
                    dp[newMask] = dp[mask] + 1;
                    time[newMask] = sessionTime - tasks[i];
                }
            }
        }
    }
    return dp[(1 << n) - 1];
}
```

#### Example

```
tasks=[1,2,3], sessionTime=3
mask=000: dp=1, time=3
mask=001(task0=1): dp=1, time=2
mask=010(task1=2): dp=1, time=1
mask=100(task2=3): dp=1, time=0
mask=011: task0+task1=3 fits → dp=1, time=0
mask=101: task0+task2=4>3 → new session → dp=2
mask=111: best=2 sessions (e.g. {1,2},{3} or {3},{1,2})
Output: 2 ✓
```

---

### P26 — Smallest Sufficient Team
**LeetCode #1125 | Difficulty: Hard | Company: Google**

> Find smallest team where every required skill is covered.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Encode | skills as bitmask | all skills = `(1<<m)-1` |
| State | `dp[skillMask]` = min team covering skillMask | |
| For each person | their skills = bitmask; update all reachable masks | |

#### Java code

```java
public int[] smallestSufficientTeam(String[] req_skills, List<List<String>> people) {
    int m = req_skills.length;
    Map<String, Integer> skillIdx = new HashMap<>();
    for (int i = 0; i < m; i++) skillIdx.put(req_skills[i], i);

    int done = (1 << m) - 1;
    int[] personSkill = new int[people.size()];
    for (int i = 0; i < people.size(); i++)
        for (String s : people.get(i))
            if (skillIdx.containsKey(s)) personSkill[i] |= (1 << skillIdx.get(s));

    long[] dp = new long[done + 1];
    Arrays.fill(dp, Long.MAX_VALUE);
    dp[0] = 0;

    for (int mask = 0; mask <= done; mask++) {
        if (dp[mask] == Long.MAX_VALUE) continue;
        for (int i = 0; i < people.size(); i++) {
            int newMask = mask | personSkill[i];
            // Encode team as bitmask of people in dp value
            if (Long.bitCount(dp[newMask]) > Long.bitCount(dp[mask]) + 1)
                dp[newMask] = dp[mask] | (1L << i);
        }
    }

    long teamMask = dp[done];
    List<Integer> team = new ArrayList<>();
    for (int i = 0; i < people.size(); i++)
        if ((teamMask >> i & 1) == 1) team.add(i);
    return team.stream().mapToInt(x -> x).toArray();
}
```

#### Example

```
req_skills=["java","nodejs","reactjs"]
people=[["java"],["nodejs"],["nodejs","reactjs"]]

skillMask: java=1,nodejs=2,reactjs=4. done=7
person0=001, person1=010, person2=110

dp[0]=0(no people). 
dp[001]=person0. dp[010]=person1. dp[110]=person2.
dp[011]=person0+person1. dp[111]=person2+person0 OR person0+person1+?...
Smallest team covering 111: person0(001)+person2(110)=2 people
Output: [0,2] ✓
```

---

## Category 6 — Probability DP

> **Key pattern:** `dp[state]` = probability of being in that state.
> Spread probabilities forward each step: `next[state2] += dp[state1] * prob(transition)`.

---

### P27 — Knight Probability in Chessboard
**LeetCode #688 | Difficulty: Medium | Company: Amazon, Google**

> Knight starts at (r,c) on n×n board. After k moves, what's the probability it's still on the board?

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[r][c]` = probability of being at (r,c) | |
| Each step | For each cell, spread `dp[r][c]/8` to each of 8 knight moves | |
| Out of bounds | contribution lost (probability leaves board) | |
| Answer | sum of all `dp[r][c]` after k steps | |

#### Java code

```java
public double knightProbability(int n, int k, int row, int col) {
    double[][] dp = new double[n][n];
    dp[row][col] = 1.0;
    int[][] moves = {{-2,-1},{-2,1},{-1,-2},{-1,2},{1,-2},{1,2},{2,-1},{2,1}};

    for (int step = 0; step < k; step++) {
        double[][] next = new double[n][n];
        for (int r = 0; r < n; r++)
            for (int c = 0; c < n; c++) {
                if (dp[r][c] == 0) continue;
                for (int[] m : moves) {
                    int nr = r + m[0], nc = c + m[1];
                    if (nr >= 0 && nr < n && nc >= 0 && nc < n)
                        next[nr][nc] += dp[r][c] / 8.0;
                }
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
Step1: knight moves from (0,0) → only (1,2) and (2,1) are on board.
  dp[(1,2)] = 1/8, dp[(2,1)] = 1/8

Step2: from (1,2): moves to (0,0),(3,...)→off,(2,0),(3,...)→off... on board: (0,0),(2,0),(3,3)→off
  prob propagates...

Output: 0.0625 ✓
```

---

### P28 — New 21 Game
**LeetCode #837 | Difficulty: Medium | Company: Google**

> Start with 0 points. Draw a card 1..maxPts each turn. Stop when score ≥ k. Prob of score ≤ n?

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Edge case | `k==0 OR n>=k+maxPts` → return 1.0 | all outcomes ≤ n |
| State | `dp[i]` = probability of reaching exactly score i | |
| Recurrence | `dp[i] = windowSum / maxPts` where `windowSum = Σdp[i-maxPts..i-1]` (only while still drawing) | |
| Sliding window | maintain running sum for O(n) | |

#### Java code

```java
public double new21Game(int n, int k, int maxPts) {
    if (k == 0 || n >= k + maxPts) return 1.0;
    double[] dp = new double[n + 1];
    dp[0] = 1.0;
    double windowSum = 1.0, result = 0.0;

    for (int i = 1; i <= n; i++) {
        dp[i] = windowSum / maxPts;
        if (i < k)  windowSum += dp[i];         // still drawing — add to window
        else        result    += dp[i];         // stopped — add to answer
        if (i >= maxPts) windowSum -= dp[i - maxPts];  // slide window
    }
    return result;
}
```

#### Example

```
n=10, k=1, maxPts=10
k=1: stop as soon as score≥1. Draw 1..10 each with prob 1/10.
All scores 1..10 ≤ 10=n → result=1.0
Output: 1.0 ✓

n=6, k=1, maxPts=10
Scores 1..10 each with prob 1/10. Scores ≤ 6: prob=6/10=0.6
Output: 0.6 ✓
```

---

### P29 — Soup Servings
**LeetCode #808 | Difficulty: Medium | Company: Amazon**

> Two soups A and B. 4 operations with equal probability. Prob A empty first + half prob both empty simultaneously.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Scale | divide N by 25 (reduces state space) | operations are multiples of 25 |
| Convergence | for N > 4800 (after scaling ≈192): answer → 1.0 | |
| State | `dp[a][b]` = probability of outcome given a units of A, b units of B | memoization |
| Operations | (100,0), (75,25), (50,50), (25,75) each with prob 0.25 | |

#### Java code

```java
private Map<String, Double> memo = new HashMap<>();

public double soupServings(int n) {
    if (n > 4800) return 1.0;  // converges to 1 for large n
    return prob((n + 24) / 25, (n + 24) / 25);  // round up, scale by 25
}

private double prob(int a, int b) {
    if (a <= 0 && b <= 0) return 0.5;  // both empty simultaneously
    if (a <= 0) return 1.0;            // A empty first
    if (b <= 0) return 0.0;            // B empty first
    String key = a + "," + b;
    if (memo.containsKey(key)) return memo.get(key);
    double res = 0.25 * (prob(a-4, b) + prob(a-3, b-1) + prob(a-2, b-2) + prob(a-1, b-3));
    memo.put(key, res);
    return res;
}
```

#### Example

```
n=50 → scaled: a=2, b=2
prob(2,2) = 0.25*(prob(-2,2)+prob(-1,1)+prob(0,0)+prob(1,-1))
          = 0.25*(1.0 + 1.0 + 0.5 + 0.0) = 0.625
Output: 0.625 ✓
```

---

### P30 — Dice Roll Simulation
**LeetCode #1223 | Difficulty: Medium | Company: Amazon**

> Roll a die n times. No face can appear more than `rollMax[face]` consecutive times. Count distinct sequences mod 10^9+7.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| State | `dp[face][consecutive]` = ways to end with `consecutive` rolls of `face` | |
| Each roll | Roll different face → `next[nf][1] += dp[face][cnt]` for all nf ≠ face | |
| Same face | if `cnt+1 ≤ rollMax[face]`: `next[face][cnt+1] += dp[face][cnt]` | |
| Answer | sum all `dp[face][cnt]` after n rolls | |

#### Java code

```java
public int dieSimulator(int n, int[] rollMax) {
    int MOD = 1_000_000_007;
    int[][] dp = new int[6][16];
    for (int i = 0; i < 6; i++) dp[i][1] = 1;  // first roll

    for (int roll = 2; roll <= n; roll++) {
        int[][] next = new int[6][16];
        for (int face = 0; face < 6; face++)
            for (int cnt = 1; cnt <= rollMax[face]; cnt++) {
                if (dp[face][cnt] == 0) continue;
                // Roll a different face
                for (int nf = 0; nf < 6; nf++)
                    if (nf != face)
                        next[nf][1] = (next[nf][1] + dp[face][cnt]) % MOD;
                // Extend same face
                if (cnt + 1 <= rollMax[face])
                    next[face][cnt+1] = (next[face][cnt+1] + dp[face][cnt]) % MOD;
            }
        dp = next;
    }

    int ans = 0;
    for (int[] f : dp) for (int v : f) ans = (ans + v) % MOD;
    return ans;
}
```

#### Example

```
n=2, rollMax=[1,1,2,2,2,3]
After roll1: dp[0][1]=1,dp[1][1]=1,dp[2][1]=1,dp[3][1]=1,dp[4][1]=1,dp[5][1]=1
After roll2: each face can follow any other face.
  next[0][1] = dp[1..5][1] = 5 (can't follow itself since rollMax[0]=1)
  next[2][2] = dp[2][1] = 1 (face 2 can repeat, rollMax[2]=2)
Total = 30 (each of 6 faces can be followed by 5 others) - some constrained
Output: 34 ✓
```

---

## Quick Pattern Reference

| Problem | Pattern | Key state | Time |
|---------|---------|-----------|------|
| Burst Balloons | Interval DP | dp[i][j]=max coins in open (i..j), k=last burst | O(n³) |
| Matrix Chain Mult | Interval DP | dp[i][j]=min cost for chain i..j | O(n³) |
| Min Cost Cut Stick | Interval DP | dp[i][j]=min cost, cost=stick length | O(n³) |
| Strange Printer | Interval DP | dp[i][j]=min turns, merge matching chars | O(n³) |
| Merge Stones | Interval DP | dp[i][j]=min cost, step by k-1 | O(n³) |
| Remove Boxes | Interval DP 3D | dp[i][j][k] with trailing k same boxes | O(n⁴) |
| Partition for Max Sum | Interval DP 1D | dp[i]=max sum first i, try k-length windows | O(nk) |
| Edit Distance | String DP | dp[i][j]=edit dist, match/insert/delete/replace | O(nm) |
| Distinct Subseqs | String DP | dp[i][j]=ways, use or skip s[i-1] | O(nm) |
| SCS | String DP | LCS table + backtrack | O(nm) |
| Wildcard | String DP | `*` = 0+ chars, `?` = 1 char | O(nm) |
| Regex | String DP | `*` = 0+ of prev, `.` = any | O(nm) |
| House Robber III | Tree DP | [rob,skip] per node, post-order | O(n) |
| Max Path Sum | Tree DP | global max, return one branch | O(n) |
| Unique BSTs | Tree DP | dp[n]=Catalan(n) | O(n²) |
| Count Unique Digits | Digit DP | 9*9*8*7... | O(n) |
| Wearing Hats | Bitmask DP | dp[mask]=ways, iterate hats | O(40×2^n×n) |
| Shortest Superstring | Bitmask DP | TSP: dp[mask][last]=min length | O(2^n×n²) |
| Knight Probability | Prob DP | spread dp[r][c] each step | O(k×n²) |
| New 21 Game | Prob DP | sliding window sum | O(n) |
| Soup Servings | Prob DP | memoized recursion, scale by 25 | O((N/25)²) |
| Dice Simulation | Prob DP | dp[face][consecutive] | O(n×6×maxRoll) |
