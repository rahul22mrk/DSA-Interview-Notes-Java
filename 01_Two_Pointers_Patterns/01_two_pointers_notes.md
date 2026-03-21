# Two Pointers — Notes & Templates

> **Pattern family:** Array / String / LinkedList Optimization
> **Difficulty range:** Easy → Hard
> **Language:** Java
> **Problems file:** [02_two_pointers_problems.md](./02_two_pointers_problems.md)
> **Extended problems:** [03_two_pointers_extended.md](./03_two_pointers_extended.md)

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
| "sorted array" + "find pair with sum" | Both-ends (2-sum variant) |
| "remove duplicates in-place" | Slow/fast pointer (same direction) |
| "3Sum / 4Sum / kSum" | Sort + both-ends inside a loop |
| "sort colors / Dutch national flag" | 3-pointer partition |
| "squares of sorted array" | Both-ends (handle negatives) |
| "merge two sorted arrays" | Two arrays, two pointers |
| "palindrome check" | Both-ends comparison |
| "reverse a string / vowels" | Both-ends swap |
| "is subsequence" | Two arrays, one pointer per array |
| "minimum window sort" | Both-ends + scan inward |
| "boats / pair max sum ≤ limit" | Greedy both-ends |
| "trapping rain water" | Both-ends (height-based) |
| "container with most water" | Both-ends (area optimization) |
| "partition list" | Split + merge two pointers |
| "compare strings with backspace" | Reverse traversal two pointers |

### Brute force test

```
Brute force: check every pair → O(n²)
→ If array is SORTED (or can be sorted first), two pointers eliminates inner loop.
→ Left moves right (sum too small), right moves left (sum too big) → O(n).

Key insight: in a sorted array, the two-pointer invariant is monotone.
Moving left inward always increases the sum.
Moving right inward always decreases the sum.
This eliminates all impossible pairs in one pass.
```

### The 5 confirming signals

**Signal 1 — "Find pair / triplet with target sum in sorted array"**
> Sort first if not sorted. Two pointers from both ends. Classic O(n) after O(n log n) sort.

**Signal 2 — "In-place modification of an array (remove, partition)"**
> One slow pointer (write position) + one fast pointer (read position). O(1) space.

**Signal 3 — "Merge / compare two sorted arrays or strings"**
> One pointer per array, advance the smaller/matching one. O(m+n).

**Signal 4 — "Palindrome / reverse / symmetric check"**
> Both-ends meet in the middle. O(n) with O(1) space.

**Signal 5 — "O(1) space" + "sorted input"**
> Sorting eliminates hash set. Two pointers eliminates nested loop.

### Decision flowchart

```
Two pointers or not?
        │
        ├── Sorted array + find pair/triplet with target?
        │       └── YES → Both-ends (Type 1)
        │
        ├── In-place remove/partition/overwrite?
        │       └── YES → Slow/fast same direction (Type 2)
        │
        ├── Two sorted arrays to merge/compare/intersect?
        │       └── YES → Two arrays two pointers (Type 3)
        │
        ├── Palindrome / reverse / symmetric?
        │       └── YES → Both-ends swap/compare (Type 1)
        │
        ├── Dutch national flag / 3-way partition?
        │       └── YES → 3-pointer (Type 4)
        │
        └── Split list + reconnect?
                └── YES → Partition + merge (Type 5)
```

---

## 2. What is this pattern?

Two pointers is a technique where you use **two index variables** that move through a data structure — usually at different speeds, from different ends, or over two separate arrays — to reduce an O(n²) solution to O(n).

**The fundamental types:**

```
Type 1 — Both ends, move toward center:
[L ————————————————— R]
 →                   ←
 Move L right: sum increases
 Move R left:  sum decreases

Type 2 — Same direction, different speeds:
[slow ——— fast ————————]
  ↑          ↑
  write      read
  position   position

Type 3 — Two separate arrays:
[i —————————] arr1
[j —————————] arr2
Advance whichever pointer is "behind"

Type 4 — Three-pointer partition (Dutch flag):
[low ——— mid ————— high]
 0s    unknown    2s

Type 5 — Split then merge:
 split list → [front] + [back]
 merge with two pointers
```

---

## 3. Core rules

**Rule 1 — Sort first for sum problems (unless already sorted)**
```java
// For 2Sum, 3Sum, 4Sum — sorting enables two pointers
Arrays.sort(arr);
// Then: if sum < target → left++
//       if sum > target → right--
//       if sum == target → found
```

**Rule 2 — Skip duplicates to avoid duplicate answers in kSum**
```java
// After finding a valid triplet (or after moving a pointer):
while (left < right && nums[left] == nums[left - 1]) left++;    // skip left dups
while (left < right && nums[right] == nums[right + 1]) right--; // skip right dups
// For outer loop in 3Sum:
if (i > 0 && nums[i] == nums[i-1]) continue;  // skip outer dups
```

**Rule 3 — For in-place modification, write pointer only advances on valid elements**
```java
int write = 0;
for (int read = 0; read < n; read++) {
    if (isValid(arr[read])) {       // condition: not duplicate, not target, etc.
        arr[write++] = arr[read];   // write only valid elements
    }
}
return write;  // new length
```

---

## 4. 2-Question framework

### Question 1 — Where do the pointers start?

| Start position | Use case |
|---------------|----------|
| Both at opposite ends `[0, n-1]` | Sum problems, palindrome, reverse, water trapping |
| Both at beginning `[0, 0]` | Slow/fast for in-place modification |
| One per array `[0, 0]` on arr1, arr2 | Merge, intersect, compare two arrays |
| Three pointers `[0, 0, n-1]` | Dutch national flag, 3-way partition |

### Question 2 — What condition drives pointer movement?

| Condition | Move which pointer |
|-----------|------------------|
| `sum < target` | `left++` (increase sum) |
| `sum > target` | `right--` (decrease sum) |
| `arr[read]` is invalid / duplicate | skip `read++`, don't advance `write` |
| `arr1[i] < arr2[j]` | `i++` (catch up in arr1) |
| `arr1[i] > arr2[j]` | `j++` (catch up in arr2) |
| `mid` element is 0 | `swap(mid, low)`, `low++`, `mid++` |
| `mid` element is 2 | `swap(mid, high)`, `high--` (don't advance mid) |

> **Decision shortcut:**
> - "sorted + find pair" → both-ends, move based on sum vs target
> - "remove / keep certain elements" → slow/fast same direction
> - "merge two sorted" → one pointer per array
> - "sort 3 values in-place" → Dutch national flag (3 pointers)
> - "palindrome / reverse" → both ends, compare and swap

---

## 5. Variants table

| Variant | Pointers | Move condition | Goal |
|---------|----------|---------------|------|
| **Both-ends — 2Sum** | `L=0, R=n-1` | sum<target: L++, sum>target: R-- | find pair |
| **Both-ends — 3Sum** | outer loop + L/R | same + skip duplicates | find triplets |
| **Both-ends — reverse/palindrome** | `L=0, R=n-1` | swap/compare, both move inward | reverse / check |
| **Both-ends — trapping water** | `L=0, R=n-1` | advance shorter side | max water |
| **Slow/fast — remove dups** | `slow=0, fast=1` | fast advances always, slow only on new value | in-place remove |
| **Slow/fast — partition** | `slow=0, fast=0` | fast finds valid, slow writes | in-place filter |
| **Two arrays — merge** | `i=0, j=0` | advance smaller, write to result | sorted merge |
| **Two arrays — intersect** | `i=0, j=0` | advance smaller, record equal | common elements |
| **Two arrays — subsequence** | `i=0, j=0` | advance both on match, only j on mismatch | check subsequence |
| **Dutch national flag** | `low=0, mid=0, high=n-1` | partition by 3 values | sort 3-value array |
| **Both-ends — boats/pairs** | `L=0, R=n-1` | if fit together: both move, else only R-- | greedy pairing |

---

## 5b. Pattern categories — all types covered

### Category 1 — Both Ends (Inward)
> Left starts at 0, right starts at n-1. Move inward based on comparison.

**Sub-types:**

**1a — Sum problems (sort first):**
```java
Arrays.sort(arr);
int left = 0, right = arr.length - 1;
while (left < right) {
    int sum = arr[left] + arr[right];
    if (sum == target) { /* found */ left++; right--; }
    else if (sum < target) left++;
    else right--;
}
```

**1b — Reverse / Palindrome / Swap:**
```java
int left = 0, right = arr.length - 1;
while (left < right) {
    swap(arr, left, right);   // or compare
    left++; right--;
}
```

**1c — Trapping Water / Container:**
```java
int left = 0, right = n - 1, maxLeft = 0, maxRight = 0;
while (left < right) {
    if (height[left] <= height[right]) {
        water += Math.max(0, maxLeft - height[left]);
        maxLeft = Math.max(maxLeft, height[left++]);
    } else {
        water += Math.max(0, maxRight - height[right]);
        maxRight = Math.max(maxRight, height[right--]);
    }
}
```

**Problems:** 2Sum II, 3Sum, 3Sum Closest, 4Sum, Valid Palindrome, Reverse String, Reverse Vowels, Squares of Sorted Array, Sort Colors, Trapping Rain Water, Container with Most Water, Boats to Save People, Minimum Window Sort

---

### Category 2 — Same Direction (Slow/Fast)
> Both start at beginning. Fast reads, slow writes.

```java
int slow = 0;
for (int fast = 0; fast < n; fast++) {
    if (condition(arr[fast])) {   // keep this element
        arr[slow++] = arr[fast];
    }
}
return slow;   // new length
```

**Problems:** Remove Duplicates from Sorted Array, Remove Element, Move Zeros, Rearrange 0s and 1s, Compare Strings with Backspaces

---

### Category 3 — Two Arrays (Separate Pointers)
> One pointer per array. Advance based on which is "behind".

```java
int i = 0, j = 0;
while (i < arr1.length && j < arr2.length) {
    if (arr1[i] == arr2[j]) { /* match */ i++; j++; }
    else if (arr1[i] < arr2[j]) i++;
    else j++;
}
```

**Problems:** Merge Sorted Array, Intersection of Two Arrays, Is Subsequence, Implement strStr, Long Pressed Name, Merge Sorted Lists

---

### Category 4 — Three Pointers (Dutch National Flag)
> Partition array into 3 regions with 3 pointers.

```java
int low = 0, mid = 0, high = n - 1;
while (mid <= high) {
    if (arr[mid] == 0) { swap(arr, low++, mid++); }
    else if (arr[mid] == 1) { mid++; }
    else { swap(arr, mid, high--); }  // don't increment mid — recheck swapped element
}
```

**Problems:** Sort Colors, Dutch National Flag, Rearrange Array Elements

---

### Category 5 — Split & Merge (Divide & Conquer)
> Split a list/array into two halves, then merge with two pointers.

```java
// Step 1: find middle
ListNode slow = head, fast = head;
while (fast.next != null && fast.next.next != null) {
    slow = slow.next; fast = fast.next.next;
}
ListNode second = slow.next;
slow.next = null;

// Step 2: process each half (reverse, sort, etc.)

// Step 3: merge with two pointers
```

**Problems:** Sort List, Partition List, Reorder List (merge variant)

---

### Summary — all 5 categories

| # | Category | Pointers start | Move condition | Space |
|---|----------|---------------|---------------|-------|
| 1 | Both-ends | opposite ends | sum vs target / height | O(1) |
| 2 | Same direction | both at 0 | fast reads, slow writes valid | O(1) |
| 3 | Two arrays | one each at 0 | advance the smaller/matching | O(1) or O(n) |
| 4 | Three-pointer | 0, 0, n-1 | by element value | O(1) |
| 5 | Split + merge | after split | merge two halves | O(1) |

---

## 6. Universal Java template

```java
// ─── TEMPLATE 1A: Both-ends — 2Sum in sorted array ───────────────────────────
public int[] twoSumSorted(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while (left < right) {
        int sum = arr[left] + arr[right];
        if (sum == target) return new int[]{left, right};
        else if (sum < target) left++;
        else right--;
    }
    return new int[]{-1, -1};
}

// ─── TEMPLATE 1B: Both-ends — 3Sum (with duplicate skip) ─────────────────────
public List<List<Integer>> threeSum(int[] nums) {
    Arrays.sort(nums);
    List<List<Integer>> result = new ArrayList<>();

    for (int i = 0; i < nums.length - 2; i++) {
        if (i > 0 && nums[i] == nums[i-1]) continue;     // skip outer dups

        int left = i + 1, right = nums.length - 1;
        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];
            if (sum == 0) {
                result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                while (left < right && nums[left] == nums[left+1]) left++;   // skip left dups
                while (left < right && nums[right] == nums[right-1]) right--; // skip right dups
                left++; right--;
            } else if (sum < 0) left++;
            else right--;
        }
    }
    return result;
}

// ─── TEMPLATE 2: Same direction — remove / filter in-place ───────────────────
public int removeElement(int[] nums, int val) {
    int slow = 0;
    for (int fast = 0; fast < nums.length; fast++) {
        if (nums[fast] != val) {            // valid element
            nums[slow++] = nums[fast];      // write position advances only on valid
        }
    }
    return slow;   // new length
}

// ─── TEMPLATE 3: Two arrays — merge sorted ────────────────────────────────────
public void merge(int[] nums1, int m, int[] nums2, int n) {
    int i = m - 1, j = n - 1, k = m + n - 1;   // merge from the end
    while (i >= 0 && j >= 0) {
        if (nums1[i] > nums2[j]) nums1[k--] = nums1[i--];
        else nums1[k--] = nums2[j--];
    }
    while (j >= 0) nums1[k--] = nums2[j--];   // remaining from nums2
}

// ─── TEMPLATE 3B: Two arrays — is subsequence ────────────────────────────────
public boolean isSubsequence(String s, String t) {
    int i = 0, j = 0;
    while (i < s.length() && j < t.length()) {
        if (s.charAt(i) == t.charAt(j)) i++;    // match: advance both
        j++;                                      // always advance t
    }
    return i == s.length();   // all of s matched
}

// ─── TEMPLATE 4: Dutch National Flag — 3-pointer partition ────────────────────
public void sortColors(int[] nums) {
    int low = 0, mid = 0, high = nums.length - 1;
    while (mid <= high) {
        if (nums[mid] == 0) {
            swap(nums, low++, mid++);
        } else if (nums[mid] == 1) {
            mid++;
        } else {
            swap(nums, mid, high--);   // don't mid++ — recheck swapped element
        }
    }
}

// ─── TEMPLATE 5: Both-ends — Palindrome / Reverse ────────────────────────────
public boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        while (left < right && !Character.isLetterOrDigit(s.charAt(left))) left++;
        while (left < right && !Character.isLetterOrDigit(s.charAt(right))) right--;
        if (Character.toLowerCase(s.charAt(left)) !=
            Character.toLowerCase(s.charAt(right))) return false;
        left++; right--;
    }
    return true;
}

// ─── HELPER ───────────────────────────────────────────────────────────────────
private void swap(int[] arr, int i, int j) {
    int temp = arr[i]; arr[i] = arr[j]; arr[j] = temp;
}
```

---

## 7. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                          → CATEGORY          → KEY MOVE
───────────────────────────────────────────────────────────────────────────────
"pair with sum in sorted array"            → Both-ends         → L++/R-- based on sum vs target
"3Sum / 4Sum"                              → Both-ends in loop → sort + outer loop + L/R + skip dups
"palindrome / reverse string"             → Both-ends swap    → compare & swap, both move inward
"sort 0s 1s 2s / Dutch flag"              → 3-pointer         → low/mid/high partition
"squares of sorted array"                 → Both-ends         → compare abs values, fill from end
"remove duplicates in-place"              → Slow/fast         → slow writes, fast reads
"merge two sorted arrays"                 → Two arrays        → compare heads, take smaller
"is X subsequence of Y"                   → Two arrays        → advance both on match, only Y on mismatch
"backspace string compare"                → Reverse pointer   → iterate from end, skip on #
"minimum window sort"                     → Both-ends scan    → find unsorted boundaries, expand outward
"boats / pairs with weight limit"         → Greedy both-ends  → pair lightest + heaviest if fits
"trapping rain water"                     → Both-ends         → advance shorter side, accumulate water
```

**The one insight for both-ends sum problems:**
```
sorted + sum < target → left++   (need bigger value)
sorted + sum > target → right--  (need smaller value)
sorted + sum == target → found!
```

**Duplicate skip pattern for kSum:**
```java
// After processing position i (outer):
if (i > 0 && nums[i] == nums[i-1]) continue;

// After finding a valid pair/triplet (inner):
while (left < right && nums[left] == nums[left+1]) left++;
while (left < right && nums[right] == nums[right-1]) right--;
left++; right--;
```

---

## 8. Common mistakes

### Mistake 1 — Not sorting before two-pointer sum problems

```java
// BUG — two pointers only work on sorted arrays for sum problems
int left = 0, right = n - 1;
// For unsorted array: moving left doesn't guarantee sum increases

// FIX — always sort first
Arrays.sort(arr);
// Then apply two pointers
```

### Mistake 2 — Wrong duplicate skip position in 3Sum

```java
// BUG — skip BEFORE processing (misses valid triplets)
while (left < right && nums[left] == nums[left+1]) left++;
// missing: what if left+1 is part of a valid new triplet?

// FIX — skip AFTER processing the current triplet
result.add(Arrays.asList(nums[i], nums[left], nums[right]));
while (left < right && nums[left] == nums[left+1]) left++;    // skip AFTER adding
while (left < right && nums[right] == nums[right-1]) right--;
left++; right--;
```

### Mistake 3 — Dutch National Flag: advancing mid after swapping with high

```java
// BUG — swapped element from high not checked
if (nums[mid] == 2) { swap(arr, mid++, high--); }  // mid++ skips unchecked element

// FIX — don't advance mid when swapping with high
if (nums[mid] == 2) { swap(arr, mid, high--); }  // recheck nums[mid] in next iteration
```

### Mistake 4 — Off by one in Squares of Sorted Array (fill from end)

```java
// BUG — wrong direction: filling from start causes overwrite
int[] result = new int[n];
int left = 0, right = n - 1, idx = 0;
// idx=0 → small values get overwritten

// FIX — fill from the END since largest squares go at back
int idx = n - 1;
while (left <= right) {
    if (Math.abs(nums[left]) >= Math.abs(nums[right]))
        result[idx--] = nums[left] * nums[left++];
    else
        result[idx--] = nums[right] * nums[right--];
}
```

### Mistake 5 — Not handling `while(left < right)` in palindrome check

```java
// BUG — comparing after pointers cross
while (left <= right) {  // <= allows checking middle character against itself
    if (s[left] != s[right]) return false;
    left++; right--;
}

// FIX — use strict < (middle char of odd-length string doesn't need comparison)
while (left < right) {
    if (s.charAt(left) != s.charAt(right)) return false;
    left++; right--;
}
```

### Mistake 6 — Two-array merge: ignoring remaining elements

```java
// BUG — stops when one array is exhausted, ignores the other
while (i < m && j < n) { ... }  // what about remaining in arr2?

// FIX — handle remaining elements
while (j >= 0) nums1[k--] = nums2[j--];  // nums1's remaining are already in place
```

---

## 9. Complexity summary

| Problem | Time | Space | Notes |
|---------|------|-------|-------|
| 2Sum (sorted input) | O(n) | O(1) | no sort needed |
| 2Sum (unsorted) | O(n log n) | O(1) | sort first |
| 3Sum | O(n²) | O(1) | sort + outer loop + two pointers |
| 4Sum | O(n³) | O(1) | sort + two outer loops + two pointers |
| 3Sum Closest | O(n²) | O(1) | same as 3Sum |
| Triplets with smaller sum | O(n²) | O(1) | count += right - left on valid |
| Remove Duplicates | O(n) | O(1) | single pass slow/fast |
| Squares of Sorted Array | O(n) | O(n) | fill result from end |
| Sort Colors (Dutch Flag) | O(n) | O(1) | single pass, 3 pointers |
| Valid Palindrome | O(n) | O(1) | both ends meet |
| Merge Sorted Array | O(m+n) | O(1) | merge from end |
| Is Subsequence | O(n) | O(1) | two array pointers |
| Trapping Rain Water | O(n) | O(1) | both-ends with max trackers |
| Minimum Window Sort | O(n) | O(1) | find bounds + expand |
| Backspace String Compare | O(m+n) | O(1) | reverse traversal |
| Product Less than K | O(n) | O(1) | sliding window hybrid |

**General rules:**
- Both-ends problems → **O(n) or O(n²)** depending on how many outer loops
- In-place modification → always **O(1) space**
- kSum → **O(n^(k-1))** time — each extra sum dimension adds one loop
- Sorting adds **O(n log n)** as a one-time cost for unsorted inputs
