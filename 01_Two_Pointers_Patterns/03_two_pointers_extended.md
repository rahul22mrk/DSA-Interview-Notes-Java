# Two Pointers — Extended Problems & Approach Guide

> **Notes & Templates:** [01_two_pointers_notes.md](./01_two_pointers_notes.md)
> **Core Problems (solved):** [02_two_pointers_problems.md](./02_two_pointers_problems.md)

Each group below has: the **core idea in 2-3 lines**, a **pseudocode skeleton**, and the list of problems that share that exact skeleton. Once you understand one problem in a group, all others follow the same structure.

---

## Category 1 — Running from Both Ends

---

### 1a — Sum Problems

**Core idea:** Sort first. `L` starts at 0, `R` at n-1. If sum < target → `L++`. If sum > target → `R--`. If equal → process.

```
sort(arr)
L = 0,  R = n-1
while L < R:
    sum = arr[L] + arr[R]
    if sum == target → record / return
    if sum < target  → L++
    if sum > target  → R--
```

**Skip duplicates (for 3Sum/4Sum):**
```
after recording a valid answer:
    while arr[L] == arr[L+1]: L++
    while arr[R] == arr[R-1]: R--
    L++, R--

for outer loop in 3Sum:
    if i > 0 and nums[i] == nums[i-1]: skip
```

**Count instead of collect (Triplets with Smaller Sum):**
```
if sum < target:
    count += R - L    // all pairs (L, L+1..R) with current i are valid
    L++
```

| Problem | LC # | Difficulty | Company |
|---------|------|------------|---------|
| Two Sum II | 167 | Easy | Amazon |
| 3Sum | 15 | Medium | Google, Amazon |
| 4Sum | 18 | Medium | Google |
| 3Sum Closest | 16 | Medium | Amazon, Adobe |
| Triplets with Smaller Sum | — | Medium | Flipkart |
| Sum of Square Numbers | 633 | Medium | — |
| Boats to Save People | 881 | Medium | Amazon |
| Minimize Maximum Pair Sum | 1877 | Medium | Google |
| 3Sum With Multiplicity | 923 | Medium | — |

**Boats to Save People twist:**
```
sort(people)
L = 0, R = n-1
while L <= R:
    if people[L] + people[R] <= limit → both board, L++, R--
    else → only heaviest boards, R--
    boats++
```

**Number of Subsequences (LC 1498) twist:**
```
sort(nums)
fix L, binary search R = last index where nums[L]+nums[R] <= target
count += 2^(R-L)   // all subsets between L and R with L fixed
L++
```

---

### 1b — Trapping Water

**Core idea:** Water above a cell = `min(maxLeft, maxRight) - height[cell]`. Two pointers compute this on the fly without extra arrays. Always advance the **shorter side** — its water is fully determined by its own max.

```
L = 0, R = n-1, maxL = 0, maxR = 0, water = 0
while L < R:
    if height[L] <= height[R]:
        if height[L] >= maxL: maxL = height[L]
        else: water += maxL - height[L]
        L++
    else:
        if height[R] >= maxR: maxR = height[R]
        else: water += maxR - height[R]
        R--
```

**Container with Most Water twist:** no water accumulation — just maximize area:
```
L = 0, R = n-1, best = 0
while L < R:
    best = max(best, min(h[L], h[R]) * (R-L))
    if h[L] <= h[R]: L++    // move shorter side — only way to potentially get more water
    else: R--
```

| Problem | LC # | Difficulty | Company |
|---------|------|------------|---------|
| Trapping Rain Water | 42 | Hard | Amazon, Google, Bloomberg |
| Container With Most Water | 11 | Medium | Amazon, Google |

---

### 1c — Next Permutation

**Core idea:** Find the rightmost "dip" (where `nums[i] < nums[i+1]`). Swap it with the smallest element to its right that's larger. Reverse the suffix.

```
step 1: scan right to left → find i where nums[i] < nums[i+1]
step 2: scan right to left → find j where nums[j] > nums[i]
step 3: swap(i, j)
step 4: reverse arr[i+1 .. end]

if no dip found (fully descending) → reverse entire array
```

| Problem | LC # | Difficulty | Company |
|---------|------|------------|---------|
| Next Permutation | 31 | Medium | Google, Microsoft |
| Next Greater Element III | 556 | Medium | — |
| Min Adjacent Swaps to kth Smallest | 1850 | Hard | — |

---

### 1d — Reverse / Palindrome / Swap

**Core idea:** `L` starts at 0, `R` at n-1. Swap or compare, then `L++, R--`. Skip irrelevant characters using inner while loops.

```
L = 0, R = n-1
while L < R:
    skip invalid chars at L (inner while)
    skip invalid chars at R (inner while)
    swap(arr[L], arr[R])   // or compare for palindrome
    L++, R--
```

**Valid Palindrome II (one skip allowed):**
```
isPalin(s, L+1, R) || isPalin(s, L, R-1)
// try skipping left char OR right char, check if rest is palindrome
```

**Squares of Sorted Array — fill from end:**
```
L = 0, R = n-1, idx = n-1
while L <= R:
    if abs(arr[L]) >= abs(arr[R]):
        result[idx--] = arr[L]*arr[L], L++
    else:
        result[idx--] = arr[R]*arr[R], R--
// fill largest squares first from the back
```

**Sort Array by Parity:**
```
// same as partition: evens go left, odds go right
L = 0, R = n-1
while L < R:
    while L<R and arr[L] is even: L++
    while L<R and arr[R] is odd:  R--
    swap(L, R), L++, R--
```

| Problem | LC # | Difficulty | Company |
|---------|------|------------|---------|
| Valid Palindrome | 125 | Easy | Facebook |
| Valid Palindrome II | 680 | Easy | Facebook |
| Reverse String | 344 | Easy | — |
| Reverse Vowels of a String | 345 | Easy | Google |
| Reverse Only Letters | 917 | Easy | — |
| Reverse Words in a String | 151 | Medium | Amazon, Microsoft |
| Reverse Words in a String III | 557 | Easy | — |
| Reverse Prefix of Word | 2000 | Easy | — |
| Squares of a Sorted Array | 977 | Easy | Google, Amazon |
| Sort Array by Parity | 905 | Easy | — |
| Sort Array by Parity II | 922 | Easy | — |
| Flipping an Image | 832 | Easy | — |

---

### 1e — Greedy Both-ends / Others

**DI String Match:**
```
// 'I' → assign smallest available, 'D' → assign largest available
lo = 0, hi = n
for each char c in pattern:
    if c == 'I': result[i] = lo++
    else:        result[i] = hi--
result[last] = lo  // (lo == hi at this point)
```

**Min Length After Deleting Similar Ends:**
```
L = 0, R = n-1
while L < R and s[L] == s[R]:
    ch = s[L]
    while L <= R and s[L] == ch: L++
    while L <= R and s[R] == ch: R--
return max(0, R - L + 1)
```

**Bag of Tokens:**
```
sort(tokens)
L = 0, R = n-1, score = 0, best = 0
while L <= R:
    if power >= tokens[L]: power -= tokens[L++], score++, best = max(best, score)
    else if score > 0:     power += tokens[R--], score--
    else: break
```

| Problem | LC # | Difficulty | Company |
|---------|------|------------|---------|
| Bag of Tokens | 948 | Medium | — |
| DI String Match | 942 | Easy | Google |
| Min Length After Deleting Similar Ends | 1750 | Medium | — |
| Sentence Similarity III | 1813 | Medium | — |
| Find K Closest Elements | 658 | Medium | Google, Amazon |
| Shortest Distance to a Character | 821 | Easy | — |

**Find K Closest Elements:**
```
// Binary search for window start, then expand
lo = 0, hi = n - k
while lo < hi:
    mid = lo + (hi-lo)/2
    if x - arr[mid] > arr[mid+k] - x: lo = mid+1
    else: hi = mid
return arr[lo .. lo+k-1]
```

---

## Category 2 — Same Direction (Slow/Fast)

**Core idea:** `slow` = write position. `fast` reads every element. Only advance `slow` when `fast` finds a "keepable" element.

```
slow = 0 (or 1 if first element always kept)
for fast = 0 to n-1:
    if arr[fast] is worth keeping:
        arr[slow++] = arr[fast]
return slow
```

**Remove Duplicates I** — keep: `arr[fast] != arr[fast-1]`
**Remove Duplicates II** — keep: `arr[fast] != arr[slow-2]` (allows at most 2)
**Remove Element** — keep: `arr[fast] != val`
**Move Zeros** — keep: `arr[fast] != 0`, then fill rest with 0

**Longest Mountain:**
```
for each index i (potential peak):
    expand left while increasing: l--
    expand right while decreasing: r++
    length = r - l - 1
    update best
```

| Problem | LC # | Difficulty | Company |
|---------|------|------------|---------|
| Remove Duplicates I | 26 | Easy | Amazon, Microsoft |
| Remove Duplicates II | 80 | Medium | — |
| Remove Element | 27 | Easy | — |
| Move Zeros | 283 | Easy | Facebook |
| Longest Mountain in Array | 845 | Medium | Google |
| Max Consecutive Ones | 485 | Easy | — |

---

## Category 3 — Two Arrays (One Pointer Each)

---

### 3a — Merge / Compare Sorted Arrays

**Core idea:** `i` on arr1, `j` on arr2. Advance whichever is "smaller" (or both on equal).

```
i = 0, j = 0
while i < m and j < n:
    if arr1[i] < arr2[j]:  process arr1[i], i++
    elif arr1[i] > arr2[j]: process arr2[j], j++
    else:                   process both, i++, j++
// handle remaining
```

**Merge Sorted Array (from end to avoid overwrite):**
```
i = m-1, j = n-1, k = m+n-1
while i >= 0 and j >= 0:
    if nums1[i] >= nums2[j]: nums1[k--] = nums1[i--]
    else:                     nums1[k--] = nums2[j--]
while j >= 0: nums1[k--] = nums2[j--]
```

| Problem | LC # | Difficulty | Company |
|---------|------|------------|---------|
| Merge Sorted Array | 88 | Easy | Amazon, Google |
| Intersection of Two Arrays | 349 | Easy | — |
| Intersection of Two Arrays II | 350 | Easy | Microsoft |
| Heaters | 475 | Medium | — |
| Find Distance Value Between Two Arrays | 1385 | Easy | — |

---

### 3b — Subsequence / String Matching

**Core idea:** `i` on pattern/shorter string, `j` on text/longer string. Advance both on match, only `j` otherwise. All of `i` matched = success.

```
i = 0 (pattern pointer)
j = 0 (text pointer)
while i < len(s) and j < len(t):
    if s[i] == t[j]: i++
    j++
return i == len(s)
```

**Backspace String Compare — reverse traversal:**
```
i = len(s)-1, j = len(t)-1
while i >= 0 or j >= 0:
    i = nextValid(s, i)   // skip characters that are backspaced
    j = nextValid(t, j)
    if s[i] != t[j]: return false
    i--, j--
return true

nextValid(str, idx):
    skip = 0
    while idx >= 0:
        if str[idx] == '#': skip++, idx--
        elif skip > 0: skip--, idx--
        else: break
    return idx
```

**Long Pressed Name:**
```
i = 0 (name), j = 0 (typed)
while i < len(name) and j < len(typed):
    if name[i] == typed[j]: i++, j++
    elif j > 0 and typed[j] == typed[j-1]: j++   // long press
    else: return false
return i == len(name)
```

| Problem | LC # | Difficulty | Company |
|---------|------|------------|---------|
| Is Subsequence | 392 | Easy | Google |
| Implement strStr | 28 | Easy | Amazon |
| Long Pressed Name | 925 | Easy | Google |
| Camelcase Matching | 1023 | Medium | — |
| Backspace String Compare | 844 | Medium | Google |
| Compare Version Numbers | 165 | Medium | — |
| Expressive Words | 809 | Medium | — |
| Longest Word in Dictionary Through Deleting | 524 | Medium | — |

---

### 3c — Median / Partition (Hard)

**Median of Two Sorted Arrays — partition approach:**
```
// Binary search on how many elements to take from nums1 for the left half
ensure nums1 is shorter
lo = 0, hi = len(nums1)
half = (m + n + 1) / 2

while lo <= hi:
    i = (lo+hi)/2       // take i elements from nums1
    j = half - i        // take j elements from nums2

    maxL1 = nums1[i-1] (or -INF if i=0)
    minR1 = nums1[i]   (or +INF if i=m)
    maxL2 = nums2[j-1] (or -INF if j=0)
    minR2 = nums2[j]   (or +INF if j=n)

    if maxL1 <= minR2 and maxL2 <= minR1:
        // correct partition
        if (m+n) is odd: return max(maxL1, maxL2)
        return (max(maxL1,maxL2) + min(minR1,minR2)) / 2.0
    elif maxL1 > minR2: hi = i-1   // too many from nums1
    else: lo = i+1
```

| Problem | LC # | Difficulty | Company |
|---------|------|------------|---------|
| Median of Two Sorted Arrays | 4 | Hard | Google, Amazon |
| Partition Array into Two to Minimize Sum Diff | 2035 | Hard | Google |
| Ways to Split Array into Three | 1712 | Medium | — |

---

### 3d — Others (Two Arrays)

**Shortest Unsorted Continuous Subarray:**
```
// One pass from left: track max, when nums[i] < max → high = i
// One pass from right: track min, when nums[i] > min → low = i
maxSeen = nums[0]
for i = 1 to n-1:
    maxSeen = max(maxSeen, nums[i])
    if nums[i] < maxSeen: high = i

minSeen = nums[n-1]
for i = n-2 to 0:
    minSeen = min(minSeen, nums[i])
    if nums[i] > minSeen: low = i

return high - low + 1   (or 0 if already sorted)
```

**Most Profit Assigning Work:**
```
sort jobs by difficulty, sort workers
i = 0, best = 0
for each worker ability (sorted):
    while i < jobs.length and jobs[i].diff <= ability:
        best = max(best, jobs[i].profit)
        i++
    total += best
```

| Problem | LC # | Difficulty | Company |
|---------|------|------------|---------|
| Shortest Unsorted Continuous Subarray | 581 | Medium | Amazon, Adobe |
| Most Profit Assigning Work | 826 | Medium | — |
| Swap Adjacent in LR String | 777 | Medium | Google |

**Swap Adjacent in LR String:**
```
// L can only move LEFT, R can only move RIGHT
// two pointers: skip spaces, check that types match and positions are valid
i on s (skip '_'), j on result (skip '_')
if s[i] != result[j]: return false
if s[i] == 'L' and i < j: return false  // L moved right — invalid
if s[i] == 'R' and i > j: return false  // R moved left — invalid
```

---

## Category 4 — Split & Merge (LinkedList)

**Core idea:** Use slow/fast to find the middle. Split into two lists. Process each half (reverse, sort). Merge the two processed halves with two pointers.

**Split step (find middle):**
```
slow = head, fast = head
while fast.next != null and fast.next.next != null:
    slow = slow.next
    fast = fast.next.next
// slow is at middle
second = slow.next
slow.next = null   // cut
```

**Merge two sorted lists step:**
```
dummy = new node
curr = dummy
while l1 != null and l2 != null:
    if l1.val <= l2.val: curr.next = l1, l1 = l1.next
    else:                 curr.next = l2, l2 = l2.next
    curr = curr.next
curr.next = l1 or l2 (whichever remains)
```

**Partition List (LC 86):**
```
// split into: nodes < x (small list) and nodes >= x (large list)
smallHead, smallTail = dummy nodes
largeHead, largeTail = dummy nodes
while node != null:
    if node.val < x: append to small list
    else:            append to large list
connect: smallTail.next = largeHead.next
return smallHead.next
```

| Problem | LC # | Difficulty | Company |
|---------|------|------------|---------|
| Partition List | 86 | Medium | Amazon |
| Sort List | 148 | Medium | Amazon |
| Reorder List | 143 | Medium | Amazon |

---

## Quick Recognition Guide

```
Sorted array + find pair/triplet with sum  → 1a: sort + both-ends
Fill result from largest to smallest        → 1d: fill from END (squares, merge)
Palindrome / string reverse                 → 1d: both-ends swap/compare
Next larger arrangement                     → 1c: find dip, swap, reverse suffix
Accumulate water / maximize area            → 1b: both-ends advance shorter side
Remove / keep elements in-place             → Cat 2: slow writes, fast reads
Match pattern as subsequence                → 3b: advance both on match, only text otherwise
Merge two sorted arrays                     → 3a: compare heads, advance smaller
LinkedList: split + reconnect               → Cat 4: find mid, cut, process, merge

Key decision tree:
  Are both pointers on the SAME array, moving inward?  → Category 1
  Are both pointers on the SAME array, moving forward? → Category 2
  Are pointers on TWO DIFFERENT arrays?                → Category 3
  Do you split a list into two, then reconnect?        → Category 4
```

---

## Interview Solve Order

```
Day 1-3 (Foundation — must do):
  LC 167 (2Sum) → LC 15 (3Sum) → LC 26 (Remove Dups) → LC 75 (Sort Colors) → LC 977 (Squares)

Day 4-6 (Core coverage):
  LC 11 (Container) → LC 42 (Trapping Water) → LC 88 (Merge Arrays) → LC 392 (Subsequence) → LC 125 (Palindrome)

Day 7-9 (Medium round):
  LC 18 (4Sum) → LC 844 (Backspace) → LC 581 (Min Window Sort) → LC 31 (Next Permutation) → LC 86 (Partition List)

Day 10-12 (Hard):
  LC 4 (Median) → LC 148 (Sort List) → LC 1498 (Subsequences Sum) → LC 2035 (Partition Min Diff)
```
