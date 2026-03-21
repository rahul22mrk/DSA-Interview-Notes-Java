# Recursion & Backtracking Pattern — Complete Notes

> **Pattern family:** Recursion / Divide & Conquer / Backtracking
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
| "all subsets / power set" | Backtracking — include/exclude each element |
| "all permutations" | Backtracking — swap or used[] array |
| "all combinations that sum to target" | Backtracking — pick with/without repetition |
| "generate all valid parentheses" | Backtracking — open/close count constraint |
| "all partitions / palindrome partition" | Backtracking — try every split point |
| "N-Queens / Sudoku / Word Search" | Backtracking — place and validate, undo on fail |
| "divide and conquer / sort" | Recursion — split in half, solve, merge |
| "Pow(x, n) / fast exponentiation" | Divide & Conquer — split exponent |
| "count inversions / reverse pairs" | Divide & Conquer — modify merge sort |
| "fibonacci / factorial / sum of digits" | Basic Recursion — direct subproblem |
| "jump game / can reach end" | Recursive Search — try each jump |

### Brute force test

```
Brute force for subsets: generate all 2^n combinations explicitly → exponential.
→ Backtracking IS the optimal approach for generating all valid solutions.
→ The "pruning" in backtracking avoids generating invalid branches.

Key question: can we PRUNE early?
  YES → Backtracking is efficient (e.g., Combination Sum: stop when sum > target)
  NO  → Still backtracking, but with full O(2^n) or O(n!) exploration
```

### The 5 confirming signals

**Signal 1 — "Find ALL" solutions (not just one)**
> When asked for all subsets, all permutations, all paths — backtracking generates every valid answer systematically.

**Signal 2 — Choices at each step with constraints**
> At each position you make a choice (include/exclude, which character, where to place a queen). Backtracking explores all choices and undoes bad ones.

**Signal 3 — The solution is built incrementally**
> You build the answer step by step. If the current partial solution can't lead to a valid complete solution → backtrack (undo last step, try next option).

**Signal 4 — "Divide the problem in half" + merge results**
> Split array/range in two → solve each half recursively → merge. Classic Divide & Conquer (Merge Sort, Count Inversions, Binary Search).

**Signal 5 — Simple function defined in terms of itself**
> `f(n) = f(n-1) + f(n-2)` (Fibonacci), `f(n) = n * f(n-1)` (Factorial) — direct recursive definition.

### Decision flowchart

```
Problem involves recursion?
        │
        ▼
What type?
        │
        ├── GENERATE ALL solutions (subsets, perms, combinations)
        │       └── Backtracking
        │           ├── No duplicates in input → standard template
        │           ├── Duplicates in input → sort + skip duplicate
        │           └── Can reuse elements → pass same index (not i+1)
        │
        ├── SEARCH with constraints (N-Queens, Sudoku, Word Search)
        │       └── Backtracking + isValid check
        │           ├── Place → recurse → undo (backtrack)
        │           └── Prune early if constraint violated
        │
        ├── DIVIDE in half + merge (Sort, Count Inversions)
        │       └── Divide & Conquer
        │           ├── Split at midpoint
        │           ├── Solve each half recursively
        │           └── Merge results (often where counting happens)
        │
        ├── DIRECT subproblem (f(n) = f(n-1) + something)
        │       └── Basic Recursion
        │           ├── Identify base case(s)
        │           └── Express f(n) using f(n-1), f(n-2), etc.
        │
        └── SEARCH / EXPLORE all paths (Jump Game, Unique Paths)
                └── Recursive Search (+ memoization if overlapping subproblems)
```

---

## 2. What is this pattern?

### Basic Recursion

A function calls itself with a **smaller subproblem** until it reaches a base case.

```
f(n) = operation + f(n-1)   ← recurrence relation
f(0) = base_value            ← base case (stops recursion)
```

### Divide & Conquer

Split the problem in half, solve each half, **merge the results**.

```
solve(arr, L, R):
    if L == R: return base
    mid = (L + R) / 2
    left  = solve(arr, L, mid)
    right = solve(arr, mid+1, R)
    return merge(left, right)
```

### Backtracking — The Core Idea

```
backtrack(currentState):
    if currentState is a COMPLETE solution:
        add to results
        return

    for each CHOICE available:
        if choice is VALID:
            MAKE the choice    (modify state)
            backtrack(nextState)
            UNDO the choice    (restore state) ← this is the backtrack step
```

**The "undo" step is what makes it backtracking** — you restore the state so the next choice starts fresh.

```
Visual for Subsets of [1, 2, 3]:

                    []
              /          \
           [1]             []
          /    \          /   \
       [1,2]  [1]      [2]    []
       /  \   / \      / \    / \
   [1,2,3][1,2][1,3][1][2,3][2][3][]
```

---

## 3. Core rules

**Rule 1 — Always define the base case first**
```java
// WRONG — infinite recursion, no stopping condition
int fibonacci(int n) {
    return fibonacci(n-1) + fibonacci(n-2);   // never stops!
}

// CORRECT — base cases first
int fibonacci(int n) {
    if (n <= 1) return n;   // base cases: fib(0)=0, fib(1)=1
    return fibonacci(n-1) + fibonacci(n-2);
}
```

**Rule 2 — Always copy the list when adding to results (backtracking)**
```java
// WRONG — adds a reference; when you backtrack, the list changes!
result.add(tempList);

// CORRECT — add a snapshot copy
result.add(new ArrayList<>(tempList));
```

**Rule 3 — For duplicates: sort first, then skip same adjacent elements**
```java
// WRONG — generates duplicate subsets/combinations without this check
for (int i = start; i < nums.length; i++) {
    tempList.add(nums[i]);
    ...
}

// CORRECT — skip duplicates at the same recursion level
Arrays.sort(nums);   // sort first!
for (int i = start; i < nums.length; i++) {
    if (i > start && nums[i] == nums[i-1]) continue;   // skip duplicate
    tempList.add(nums[i]);
    ...
}
```

**Rule 4 — Reusable vs non-reusable elements: `i` vs `i+1`**
```java
// Can REUSE same element (Combination Sum): pass i (not i+1)
backtrack(list, tempList, nums, remain - nums[i], i);    // i again!

// Cannot reuse (Subsets, Combination Sum II): pass i+1
backtrack(list, tempList, nums, remain - nums[i], i+1);  // next index
```

**Rule 5 — For Divide & Conquer: merge step is where the work happens**
```java
// The merge step in merge sort is O(n)
// In count inversions, counting happens DURING the merge
// In count of range sum, counting happens during the merge
// → Don't skip the merge step analysis in complexity
```

---

## 4. 2-Question framework

### Question 1 — What is the output?

| Output | Variant |
|--------|---------|
| All subsets of an array | Backtracking — include/exclude |
| All permutations | Backtracking — used[] array or swap |
| All combinations summing to target | Backtracking — subtract target |
| All valid string arrangements | Backtracking — string constraints |
| One valid placement (N-Queens, Sudoku) | Backtracking + isValid |
| Sorted array / count of inversions | Divide & Conquer (Merge Sort) |
| Single value (fib, pow, sum of digits) | Basic Recursion |

### Question 2 — Are there duplicates, and can elements be reused?

| Situation | Approach |
|-----------|----------|
| No duplicates, no reuse | Standard backtracking, pass `i+1` |
| **Duplicates** in input, no reuse | Sort + skip: `if (i > start && nums[i] == nums[i-1]) continue` |
| No duplicates, **can reuse** | Pass `i` (same index) instead of `i+1` |
| **Duplicates** in permutations | Sort + `used[]` array + `if (used[i] || nums[i]==nums[i-1] && !used[i-1]) continue` |

> **Decision shortcut:**
> - "all subsets" → include/exclude, add at EVERY level
> - "all permutations" → use `used[]`, add only at LEAF (full length)
> - "combinations summing to target" → subtract, prune when `remain < 0`
> - "duplicates in input" → sort + skip adjacent same at same level
> - "can reuse same element" → pass `i`, not `i+1`
> - "grid/board constraint" → place + isValid + recurse + undo

---

## 5. Variants table

> **Common core:** choose → recurse → unchoose (backtrack)
> **What differs:** what triggers "add to result", what constitutes a valid choice

| Variant | Add result when | Skip condition | Pass next index |
|---------|----------------|----------------|-----------------|
| Subsets | Every call | — | `i+1` |
| Subsets II (dups) | Every call | `i > start && nums[i] == nums[i-1]` | `i+1` |
| Combinations | `tempList.size() == k` | — | `i+1` |
| Combination Sum | `remain == 0` | `remain < 0` | `i` (reuse!) |
| Combination Sum II | `remain == 0` | `remain < 0` or dup | `i+1` |
| Permutations | `tempList.size() == n` | `used[i]` | `0` (all indices) |
| Permutations II | `tempList.size() == n` | `used[i]` or dup+!used[i-1] | `0` (all indices) |
| Generate Parentheses | `open==close==n` | `open > n` or `close > open` | — |
| Palindrome Partition | `start == s.length()` | not palindrome | `i+1` |
| N-Queens | `row == n` | `!isValid(board, row, col)` | next row |
| Word Search | found all chars | out of bounds or visited | all 4 directions |
| Sudoku | board filled | `!isValid(board, r, c, num)` | next cell |

---

## 6. Universal Java template

```java
// ─── TEMPLATE A: Subsets (no duplicates) ─────────────────────────────────────
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(result, new ArrayList<>(), nums, 0);
    return result;
}
private void backtrack(List<List<Integer>> result, List<Integer> temp, int[] nums, int start) {
    result.add(new ArrayList<>(temp));   // add at EVERY level (snapshot!)
    for (int i = start; i < nums.length; i++) {
        temp.add(nums[i]);
        backtrack(result, temp, nums, i + 1);
        temp.remove(temp.size() - 1);   // UNDO
    }
}


// ─── TEMPLATE B: Subsets II (with duplicates) ────────────────────────────────
private void backtrackWithDups(List<List<Integer>> result, List<Integer> temp, int[] nums, int start) {
    result.add(new ArrayList<>(temp));
    for (int i = start; i < nums.length; i++) {
        if (i > start && nums[i] == nums[i-1]) continue;   // skip duplicate at same level
        temp.add(nums[i]);
        backtrackWithDups(result, temp, nums, i + 1);
        temp.remove(temp.size() - 1);
    }
}


// ─── TEMPLATE C: Permutations ────────────────────────────────────────────────
private void permuteHelper(List<List<Integer>> result, List<Integer> temp, int[] nums, boolean[] used) {
    if (temp.size() == nums.length) {
        result.add(new ArrayList<>(temp));   // add only at LEAF
        return;
    }
    for (int i = 0; i < nums.length; i++) {
        if (used[i]) continue;
        used[i] = true;
        temp.add(nums[i]);
        permuteHelper(result, temp, nums, used);
        used[i] = false;
        temp.remove(temp.size() - 1);
    }
}


// ─── TEMPLATE D: Permutations II (with duplicates) ───────────────────────────
// Sort first! Skip: used[i] OR (same as prev AND prev not used at this level)
private void permuteUniqueHelper(List<List<Integer>> result, List<Integer> temp, int[] nums, boolean[] used) {
    if (temp.size() == nums.length) { result.add(new ArrayList<>(temp)); return; }
    for (int i = 0; i < nums.length; i++) {
        if (used[i] || (i > 0 && nums[i] == nums[i-1] && !used[i-1])) continue;
        used[i] = true;
        temp.add(nums[i]);
        permuteUniqueHelper(result, temp, nums, used);
        used[i] = false;
        temp.remove(temp.size() - 1);
    }
}


// ─── TEMPLATE E: Combination Sum (can reuse elements) ────────────────────────
private void combinationHelper(List<List<Integer>> result, List<Integer> temp, int[] nums, int remain, int start) {
    if (remain < 0) return;
    if (remain == 0) { result.add(new ArrayList<>(temp)); return; }
    for (int i = start; i < nums.length; i++) {
        temp.add(nums[i]);
        combinationHelper(result, temp, nums, remain - nums[i], i);   // i NOT i+1 (reuse!)
        temp.remove(temp.size() - 1);
    }
}


// ─── TEMPLATE F: Combination Sum II (no reuse, duplicates in input) ──────────
private void combinationHelperII(List<List<Integer>> result, List<Integer> temp, int[] nums, int remain, int start) {
    if (remain < 0) return;
    if (remain == 0) { result.add(new ArrayList<>(temp)); return; }
    for (int i = start; i < nums.length; i++) {
        if (i > start && nums[i] == nums[i-1]) continue;   // skip dup at same level
        temp.add(nums[i]);
        combinationHelperII(result, temp, nums, remain - nums[i], i + 1);
        temp.remove(temp.size() - 1);
    }
}


// ─── TEMPLATE G: Generate Parentheses ────────────────────────────────────────
private void generateHelper(List<String> result, StringBuilder sb, int open, int close, int n) {
    if (sb.length() == 2 * n) { result.add(sb.toString()); return; }
    if (open < n)  { sb.append('('); generateHelper(result, sb, open+1, close,   n); sb.deleteCharAt(sb.length()-1); }
    if (close < open) { sb.append(')'); generateHelper(result, sb, open, close+1, n); sb.deleteCharAt(sb.length()-1); }
}


// ─── TEMPLATE H: Palindrome Partitioning ─────────────────────────────────────
private void partitionHelper(List<List<String>> result, List<String> temp, String s, int start) {
    if (start == s.length()) { result.add(new ArrayList<>(temp)); return; }
    for (int i = start; i < s.length(); i++) {
        if (isPalindrome(s, start, i)) {
            temp.add(s.substring(start, i + 1));
            partitionHelper(result, temp, s, i + 1);
            temp.remove(temp.size() - 1);
        }
    }
}
private boolean isPalindrome(String s, int lo, int hi) {
    while (lo < hi) if (s.charAt(lo++) != s.charAt(hi--)) return false;
    return true;
}


// ─── TEMPLATE I: Grid Backtracking (Word Search) ─────────────────────────────
int[] dr = {0,0,1,-1};
int[] dc = {1,-1,0,0};

private boolean searchHelper(char[][] board, String word, int idx, int r, int c) {
    if (idx == word.length()) return true;
    if (r < 0 || r >= board.length || c < 0 || c >= board[0].length) return false;
    if (board[r][c] != word.charAt(idx)) return false;

    char tmp = board[r][c];
    board[r][c] = '#';                               // mark visited
    for (int d = 0; d < 4; d++) {
        if (searchHelper(board, word, idx+1, r+dr[d], c+dc[d])) return true;
    }
    board[r][c] = tmp;                               // unmark (backtrack)
    return false;
}


// ─── TEMPLATE J: N-Queens ────────────────────────────────────────────────────
private void queensHelper(List<List<String>> result, char[][] board, int row) {
    if (row == board.length) { result.add(construct(board)); return; }
    for (int col = 0; col < board.length; col++) {
        if (isValidQueen(board, row, col)) {
            board[row][col] = 'Q';
            queensHelper(result, board, row + 1);
            board[row][col] = '.';   // backtrack
        }
    }
}
private boolean isValidQueen(char[][] board, int row, int col) {
    int n = board.length;
    for (int i = 0; i < row; i++) if (board[i][col] == 'Q') return false;       // column
    for (int i=row-1, j=col-1; i>=0 && j>=0; i--, j--) if (board[i][j]=='Q') return false; // diag \
    for (int i=row-1, j=col+1; i>=0 && j<n;  i--, j++) if (board[i][j]=='Q') return false; // diag /
    return true;
}


// ─── TEMPLATE K: Divide & Conquer (Merge Sort + Count Inversions) ────────────
long mergeSort(int[] nums, int left, int right) {
    if (left >= right) return 0;
    int mid = left + (right - left) / 2;
    long count = mergeSort(nums, left, mid) + mergeSort(nums, mid+1, right);
    // count inversions during merge
    int[] temp = new int[right - left + 1];
    int i = left, j = mid+1, k = 0;
    while (i <= mid && j <= right) {
        if (nums[i] <= nums[j]) { temp[k++] = nums[i++]; }
        else { count += (mid - i + 1); temp[k++] = nums[j++]; }  // all remaining left > nums[j]
    }
    while (i <= mid)   temp[k++] = nums[i++];
    while (j <= right) temp[k++] = nums[j++];
    System.arraycopy(temp, 0, nums, left, temp.length);
    return count;
}
```

---

## 7. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                          → VARIANT                 → KEY CODE
────────────────────────────────────────────────────────────────────────────────────
"all subsets / power set"                  → Subsets                 → add at every level; pass i+1
"subsets with duplicates"                  → Subsets II              → sort + if(i>start && nums[i]==nums[i-1]) skip
"all combinations summing to k"            → Combination Sum         → pass i (reuse); prune remain<0
"combinations, no reuse, dups in input"    → Combination Sum II      → pass i+1; sort + skip dup
"all permutations"                         → Permutations            → used[]; add at leaf (size==n)
"permutations with duplicates"             → Permutations II         → sort + used[] + skip prev unused dup
"valid parentheses strings"                → Generate Parentheses    → open<n → add '('; close<open → add ')'
"all palindrome partitions"                → Palindrome Partition     → try every split; isPalindrome check
"N-Queens / Sudoku"                        → Constraint Backtracking → place + isValid + recurse + undo
"word search in grid"                      → Grid Backtracking       → mark '#' visited; unmark on return
"sort / count inversions"                  → Merge Sort D&C          → split + sort + merge + count
"Pow(x,n) fast"                            → D&C Exponentiation      → split n in half; n%2 handles odd
```

**Burn these into memory:**
```java
// The 3-line backtrack core (always the same):
make_choice();
backtrack(next_state);
undo_choice();           // ← THIS is what makes it backtracking

// Add result — ALWAYS copy:
result.add(new ArrayList<>(temp));   // NOT result.add(temp)!

// Skip duplicates at same recursion level (sort first!):
if (i > start && nums[i] == nums[i-1]) continue;

// Reuse vs no-reuse:
backtrack(..., i);     // reuse same element (Combination Sum)
backtrack(..., i+1);   // move to next    (everything else)

// Permutation duplicate skip:
if (used[i] || (i > 0 && nums[i] == nums[i-1] && !used[i-1])) continue;
```

---

## 8. Common mistakes

### Mistake 1 — Adding reference instead of copy

```java
// BUG — temp is modified later; result contains wrong/empty lists
result.add(temp);

// FIX — always snapshot
result.add(new ArrayList<>(temp));
```

### Mistake 2 — Wrong duplicate skip condition (Subsets II / Combination II)

```java
// BUG — skips too aggressively (removes valid combinations)
if (nums[i] == nums[i-1]) continue;   // wrong: also skips at different recursion levels

// FIX — only skip at SAME recursion level (i > start)
if (i > start && nums[i] == nums[i-1]) continue;
```

### Mistake 3 — Forgetting to undo (no backtrack)

```java
// BUG — changes persist; next branch sees polluted state
temp.add(nums[i]);
backtrack(result, temp, nums, i+1);
// forgot: temp.remove(temp.size() - 1);

// FIX — always undo after recursive call
temp.add(nums[i]);
backtrack(result, temp, nums, i+1);
temp.remove(temp.size() - 1);   // undo
```

### Mistake 4 — Using i+1 when reuse is allowed (Combination Sum)

```java
// BUG — can't reuse elements; misses valid combos like [2,2,3]
backtrack(list, temp, nums, remain - nums[i], i + 1);

// FIX — pass i to allow reuse
backtrack(list, temp, nums, remain - nums[i], i);   // same index!
```

### Mistake 5 — Not sorting before duplicate skipping

```java
// BUG — nums[i] == nums[i-1] check is meaningless if not sorted
// e.g. [1,2,1] — the two 1s are not adjacent, skip won't work
backtrack(list, temp, nums, start);

// FIX — always sort before backtracking with duplicate arrays
Arrays.sort(nums);
backtrack(list, temp, nums, 0);
```

### Mistake 6 — Missing base case in recursion (infinite loop)

```java
// BUG — no termination
int factorial(int n) {
    return n * factorial(n - 1);   // never stops!
}

// FIX
int factorial(int n) {
    if (n <= 1) return 1;   // base case
    return n * factorial(n - 1);
}
```

### Mistake 7 — Not unmarking visited cells in grid backtracking

```java
// BUG — board stays '#'; other paths can't use this cell
board[r][c] = '#';
dfs(board, word, idx+1, ...);
// forgot to restore!

// FIX
char tmp = board[r][c];
board[r][c] = '#';
dfs(board, word, idx+1, ...);
board[r][c] = tmp;   // restore
```

---

## 9. Complexity summary

| Problem | Time | Space | Notes |
|---------|------|-------|-------|
| Fibonacci (naive) | O(2^n) | O(n) | exponential — use memoization |
| Fibonacci (memoized) | O(n) | O(n) | each subproblem solved once |
| Pow(x, n) | O(log n) | O(log n) | halve exponent each time |
| Binary Search | O(log n) | O(log n) | recursive call stack |
| Merge Sort | O(n log n) | O(n) | n levels × O(n) merge |
| Count Inversions | O(n log n) | O(n) | modified merge sort |
| Subsets | O(2^n × n) | O(n) | 2^n subsets × O(n) copy |
| Permutations | O(n! × n) | O(n) | n! perms × O(n) copy |
| Combination Sum | O(2^t) | O(t/m) | t=target, m=min element |
| Generate Parentheses | O(4^n / √n) | O(n) | Catalan number |
| Palindrome Partition | O(2^n × n) | O(n²) | all splits × palindrome check |
| N-Queens | O(n!) | O(n²) | n! placements, n²  board |
| Word Search | O(m×n × 4^L) | O(L) | L=word length, 4 directions |
| Sudoku Solver | O(9^81) worst | O(81) | but heavy pruning in practice |

**General rules:**
- Backtracking is **exponential** in worst case — pruning is crucial.
- **Memoization** converts overlapping recursive subproblems from exponential to polynomial.
- All backtracking uses **O(depth)** call stack space (plus result storage).
- Divide & Conquer is usually **O(n log n)** — log n levels, O(n) work per level.
- When asked for complexity, state both the recursion tree size AND the work per node.

---

*Backtracking is one of the most common FAANG interview patterns.*
*Master the 3-line template: make choice → recurse → undo.*
*The only differences between problems are: when to add to result, what to skip, and whether to pass i or i+1.*
