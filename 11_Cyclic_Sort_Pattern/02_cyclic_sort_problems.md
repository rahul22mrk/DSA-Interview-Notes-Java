# Cyclic Sort Pattern — Solved Problems (12 Problems)

> **Pattern family:** Array / Sorting / Index Mapping
> **Notes & Templates:** [01_cyclic_sort_notes.md](./01_cyclic_sort_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Core Cyclic Sort
- [P1 — Cyclic Sort](#problem-1--cyclic-sort)

### Category 2 — Find Missing
- [P2 — Find the Missing Number](#problem-2--find-the-missing-number)
- [P3 — Find All Missing Numbers](#problem-3--find-all-missing-numbers)
- [P7 — Find the Smallest Missing Positive Number](#problem-7--find-the-smallest-missing-positive-number)
- [P8 — Find the First K Missing Positive Numbers](#problem-8--find-the-first-k-missing-positive-numbers)

### Category 3 — Find Duplicate
- [P4 — Find the Duplicate Number](#problem-4--find-the-duplicate-number)
- [P5 — Find All Duplicate Numbers](#problem-5--find-all-duplicate-numbers)

### Category 4 — Combined (Missing + Duplicate)
- [P6 — Find the Corrupt Pair](#problem-6--find-the-corrupt-pair)

### Category 5 — FAANG / Hard
- [P9 — Missing Number (XOR / Math approach)](#problem-9--missing-number-xor--math-approach)
- [P10 — Set Mismatch](#problem-10--set-mismatch)
- [P11 — Find All Numbers Disappeared in an Array](#problem-11--find-all-numbers-disappeared-in-an-array)
- [P12 — First Missing Positive (LeetCode Hard)](#problem-12--first-missing-positive-leetcode-hard)

---

## Category 1 — Core Cyclic Sort

---

### Problem 1 — Cyclic Sort
**Difficulty: Easy | Category: Core Cyclic Sort**

> Given an array containing numbers in range `[1, n]`, sort it in-place in O(n) without using any built-in sort.

#### Core insight

Each number `x` belongs at index `x-1`. Swap each number to its home until the entire array is sorted. The key: only advance `i` when `nums[i]` is already at home (or is a duplicate).

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| While `i < n` | `nums[i] != nums[nums[i]-1]` | swap `nums[i]` to home |
| While `i < n` | `nums[i] == nums[nums[i]-1]` | `i++` (already placed or duplicate) |

#### Java code

```java
public void cyclicSort(int[] nums) {
    int i = 0;
    while (i < nums.length) {
        int home = nums[i] - 1;                  // home index for nums[i]
        if (nums[i] != nums[home]) {             // not at home, no duplicate
            swap(nums, i, home);                 // place nums[i] at its home
        } else {
            i++;                                 // already correct or duplicate
        }
    }
}

private void swap(int[] nums, int i, int j) {
    int tmp = nums[i]; nums[i] = nums[j]; nums[j] = tmp;
}
```

#### Example

```
Input: [3, 1, 5, 4, 2]

i=0: nums[0]=3, home=2. nums[2]=5≠3 → swap → [5,1,3,4,2]. re-check i=0
i=0: nums[0]=5, home=4. nums[4]=2≠5 → swap → [2,1,3,4,5]. re-check i=0
i=0: nums[0]=2, home=1. nums[1]=1≠2 → swap → [1,2,3,4,5]. re-check i=0
i=0: nums[0]=1, home=0. nums[0]==nums[0] → i++
i=1..4: all already at home → i++

Output: [1, 2, 3, 4, 5] ✓
```

---

## Category 2 — Find Missing

---

### Problem 2 — Find the Missing Number
**LeetCode #268 | Difficulty: Easy | Company: Amazon, Google | Category: Missing**

> Array of n distinct numbers taken from [0, n]. Find the missing number.

#### Core insight

Sort using cyclic sort (range [0, n] → home = nums[i] for values in [0, n-1]). After sort, first index where `nums[i] != i` has the missing number. If all match, `n` is missing.

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Sort | `nums[i] < n && nums[i] != i` | swap `nums[i]` to index `nums[i]` |
| Scan | `nums[i] != i` | return `i` |
| After loop | all match | return `n` |

#### Java code

```java
public int missingNumber(int[] nums) {
    int i = 0, n = nums.length;

    // Cyclic sort — range [0, n], home = nums[i]
    while (i < n) {
        if (nums[i] < n && nums[i] != i) {
            swap(nums, i, nums[i]);
        } else {
            i++;
        }
    }

    // Find missing
    for (int j = 0; j < n; j++)
        if (nums[j] != j) return j;

    return n;   // n itself is missing
}
```

#### Example

```
Input: [3, 0, 1]  (n=3, range [0,3])

i=0: nums[0]=3, 3<3? No → i++
i=1: nums[1]=0, 0<3 and 0≠1 → swap(1,0) → [0,3,1]
i=1: nums[1]=3, 3<3? No → i++
i=2: nums[2]=1, 1<3 and 1≠2 → swap(2,1) → [0,1,3]
i=2: nums[2]=3, 3<3? No → i++

Scan: nums[0]=0✓ nums[1]=1✓ nums[2]=3≠2 → return 2 ✓
```

---

### Problem 3 — Find All Missing Numbers
**LeetCode #448 | Difficulty: Easy | Company: Amazon, Facebook | Category: All Missing**

> Array of n integers in [1, n]. Some appear twice, some not at all. Find all missing numbers.

#### Java code

```java
public List<Integer> findDisappearedNumbers(int[] nums) {
    int i = 0;
    while (i < nums.length) {
        int home = nums[i] - 1;
        if (nums[i] != nums[home]) {   // not at home and no duplicate at home
            swap(nums, i, home);
        } else {
            i++;
        }
    }

    List<Integer> missing = new ArrayList<>();
    for (int j = 0; j < nums.length; j++)
        if (nums[j] != j + 1) missing.add(j + 1);   // j+1 is missing

    return missing;
}
```

#### Example

```
Input: [4, 3, 2, 7, 8, 2, 3, 1]  (n=8)

After cyclic sort: [1, 2, 3, 4, 3, 2, 7, 8]
                                ↑     ↑
Scan: idx4: nums[4]=3≠5 → 5 missing
      idx5: nums[5]=2≠6 → 6 missing

Output: [5, 6] ✓
```

---

### Problem 7 — Find the Smallest Missing Positive Number
**LeetCode #41 | Difficulty: Hard | Company: Amazon, Google, Facebook | Category: Missing Positive**

> Find the smallest missing positive integer in an unsorted array. Must be O(n) time, O(1) space.

#### Core insight

Cyclic sort with range guard — only place numbers in [1, n]. Ignore 0, negatives, and numbers > n. After sorting, first index where `nums[i] != i+1` gives the answer.

#### Java code

```java
public int firstMissingPositive(int[] nums) {
    int n = nums.length, i = 0;

    while (i < n) {
        int home = nums[i] - 1;
        if (nums[i] > 0 && nums[i] <= n && nums[i] != nums[home]) {
            swap(nums, i, home);          // valid range, not duplicate → place
        } else {
            i++;                          // out of range or duplicate → skip
        }
    }

    for (int j = 0; j < n; j++)
        if (nums[j] != j + 1) return j + 1;

    return n + 1;   // all 1..n present → answer is n+1
}
```

#### Example

```
Input: [3, 4, -1, 1]  (n=4)

i=0: nums[0]=3, home=2. 3∈[1,4] and nums[2]=-1≠3 → swap → [-1,4,3,1]
i=0: nums[0]=-1, -1<1 → i++
i=1: nums[1]=4, home=3. 4∈[1,4] and nums[3]=1≠4 → swap → [-1,1,3,4]
i=1: nums[1]=1, home=0. 1∈[1,4] and nums[0]=-1≠1 → swap → [1,-1,3,4]
i=1: nums[1]=-1, -1<1 → i++
i=2: nums[2]=3, home=2. nums[2]==nums[2] → i++
i=3: nums[3]=4, home=3. nums[3]==nums[3] → i++

Scan: nums[0]=1✓ nums[1]=-1≠2 → return 2 ✓
```

---

### Problem 8 — Find the First K Missing Positive Numbers
**Difficulty: Hard | Category: First K Missing**

> Find the first k missing positive integers from an array of positive numbers.

#### Java code

```java
public List<Integer> findFirstKMissingPositive(int[] nums, int k) {
    int n = nums.length, i = 0;

    // Cyclic sort with range guard
    while (i < n) {
        int home = nums[i] - 1;
        if (nums[i] > 0 && nums[i] <= n && nums[i] != nums[home]) {
            swap(nums, i, home);
        } else {
            i++;
        }
    }

    List<Integer> missing = new ArrayList<>();
    Set<Integer> extraNums = new HashSet<>();

    // Collect missing in [1, n]
    for (int j = 0; j < n && missing.size() < k; j++) {
        if (nums[j] != j + 1) {
            missing.add(j + 1);
            extraNums.add(nums[j]);   // track what's "extra" for beyond-n step
        }
    }

    // Extend beyond n if still need more
    int next = n + 1;
    while (missing.size() < k) {
        if (!extraNums.contains(next)) missing.add(next);
        next++;
    }

    return missing;
}
```

#### Example

```
nums = [3, -1, 4, 5, 5], k = 3

After sort: [-1, 3, 4, 5, 5] → actually [3,-1,4,5,5] has:
  nums[0]=3→home=2, nums[2]=4≠3 → swap → [4,-1,3,5,5]
  nums[0]=4→home=3, nums[3]=5≠4 → swap → [5,-1,3,4,5]
  nums[0]=5→home=4, nums[4]=5==5 → i++ (dup)
  i=1: nums[1]=-1 → i++
  i=2: nums[2]=3, home=2 → equal → i++
  i=3: nums[3]=4, home=3 → equal → i++
  i=4: nums[4]=5, home=4 → equal → i++

Sorted: [5,-1,3,4,5]
j=0: nums[0]=5≠1 → missing=[1], extra={5}
j=1: nums[1]=-1≠2 → missing=[1,2], extra={5,-1}
j=2: nums[2]=3✓
j=3: nums[3]=4✓
j=4: nums[4]=5≠5? 5==5 ✓ wait: j=4, j+1=5, nums[4]=5 → equal
No more in [1,n]. Extend: next=6, 6∉extra → missing=[1,2,6] ✓
```

---

## Category 3 — Find Duplicate

---

### Problem 4 — Find the Duplicate Number
**LeetCode #287 | Difficulty: Medium | Company: Amazon, Microsoft | Category: Duplicate**

> Array of n+1 integers in range [1, n]. Find the duplicate without modifying the array (or with modification for cyclic sort approach).

#### Core insight (Cyclic Sort approach)

Place each number at home. When you find `nums[i] == nums[home]`, you've found the duplicate — two numbers claim the same home.

#### Java code

```java
// Approach A: Cyclic Sort (modifies array) — O(n) time, O(1) space
public int findDuplicate(int[] nums) {
    int i = 0;
    while (i < nums.length) {
        if (nums[i] != i + 1) {
            int home = nums[i] - 1;
            if (nums[i] == nums[home]) return nums[i];   // duplicate!
            swap(nums, i, home);
        } else {
            i++;
        }
    }
    return -1;
}

// Approach B: Floyd's Cycle Detection (does NOT modify array) — O(n) time, O(1) space
public int findDuplicateFloyd(int[] nums) {
    int slow = nums[0], fast = nums[0];

    // Phase 1: find meeting point
    do {
        slow = nums[slow];
        fast = nums[nums[fast]];
    } while (slow != fast);

    // Phase 2: find cycle start = duplicate
    slow = nums[0];
    while (slow != fast) {
        slow = nums[slow];
        fast = nums[fast];
    }
    return slow;
}
```

#### Example

```
Input: [1, 3, 4, 2, 2]

i=0: nums[0]=1, home=0. nums[0]==nums[0] → i++ (already at home)
i=1: nums[1]=3, home=2. nums[3]≠3... wait: home=2, nums[2]=4≠3 → swap → [1,4,3,2,2]
i=1: nums[1]=4, home=3. nums[3]=2≠4 → swap → [1,2,3,4,2]? No: [1,2,3,4,2]
     Actually: [1,4,3,2,2]→swap(1,3)→[1,2,3,4,2]
i=1: nums[1]=2, home=1. nums[1]==nums[1] → i++
i=2,3: already correct → i++
i=4: nums[4]=2, home=1. nums[4]==nums[1]=2 → return 2 ✓
```

---

### Problem 5 — Find All Duplicate Numbers
**LeetCode #442 | Difficulty: Medium | Company: Amazon, Google | Category: All Duplicates**

> Array of n integers in [1, n]. Each element appears once or twice. Find all duplicates.

#### Java code

```java
public List<Integer> findAllDuplicates(int[] nums) {
    int i = 0;
    while (i < nums.length) {
        int home = nums[i] - 1;
        if (nums[i] != nums[home]) {   // not at home and no dup at home
            swap(nums, i, home);
        } else {
            i++;
        }
    }

    List<Integer> duplicates = new ArrayList<>();
    for (int j = 0; j < nums.length; j++)
        if (nums[j] != j + 1) duplicates.add(nums[j]);   // nums[j] is the duplicate

    return duplicates;
}
```

#### Example

```
Input: [4, 3, 2, 7, 8, 2, 3, 1]

After sort: [1, 2, 3, 4, 3, 2, 7, 8]
  idx4: nums[4]=3≠5 → 3 is duplicate
  idx5: nums[5]=2≠6 → 2 is duplicate

Output: [3, 2] ✓
```

---

## Category 4 — Combined (Missing + Duplicate)

---

### Problem 6 — Find the Corrupt Pair
**Difficulty: Easy | Category: Corrupt Pair**

> Array of n integers in [1, n]. One number is duplicated and one is missing. Find [duplicate, missing].

#### Core insight

After cyclic sort, find the first index `i` where `nums[i] != i+1`.
- `nums[i]` = the duplicate (it's sitting at the wrong index)
- `i+1` = the missing number (nothing placed itself here)

#### Java code

```java
public int[] findCorruptPair(int[] nums) {
    int i = 0;
    while (i < nums.length) {
        int home = nums[i] - 1;
        if (nums[i] != nums[home]) {
            swap(nums, i, home);
        } else {
            i++;
        }
    }

    for (int j = 0; j < nums.length; j++)
        if (nums[j] != j + 1)
            return new int[]{nums[j], j + 1};   // [duplicate, missing]

    return new int[]{-1, -1};
}
```

#### Example

```
Input: [3, 1, 2, 5, 2]

After sort: [1, 2, 2, 3, 5]
  idx2: nums[2]=2≠3 → duplicate=2, missing=3

Output: [2, 3] ✓
```

---

## Category 5 — FAANG / Hard

---

### Problem 9 — Missing Number (XOR / Math approach)
**LeetCode #268 | Difficulty: Easy | Company: Amazon, Google, Microsoft | Category: Missing (Multiple Approaches)**

> Same as P2 but interviewer may ask for XOR or math approach instead of cyclic sort.

#### Approach A: XOR

```java
public int missingNumber(int[] nums) {
    int xor = nums.length;   // start with n
    for (int i = 0; i < nums.length; i++)
        xor ^= i ^ nums[i];  // XOR every index and value
    return xor;
    // Each number 0..n appears twice (once as index, once as value) except the missing one
}
```

#### Approach B: Math (Gauss)

```java
public int missingNumber(int[] nums) {
    int n = nums.length;
    int expectedSum = n * (n + 1) / 2;   // sum of 0..n
    int actualSum = 0;
    for (int num : nums) actualSum += num;
    return expectedSum - actualSum;
}
```

#### Example

```
nums = [3, 0, 1]
XOR: start=3. i=0: 3^0^3=0. i=1: 0^1^0=1. i=2: 1^2^1=2 → return 2 ✓
Math: expected=6, actual=4 → 6-4=2 ✓
```

---

### Problem 10 — Set Mismatch
**LeetCode #645 | Difficulty: Easy | Company: Amazon | Category: Corrupt Pair**

> Set `{1..n}` becomes corrupted — one number is duplicated and one is missing. Find [duplicate, missing].

> Same as Find the Corrupt Pair (Problem 6) — LeetCode version.

#### Java code

```java
public int[] findErrorNums(int[] nums) {
    int i = 0, n = nums.length;
    while (i < n) {
        int home = nums[i] - 1;
        if (nums[i] != nums[home]) swap(nums, i, home);
        else i++;
    }
    for (int j = 0; j < n; j++)
        if (nums[j] != j + 1)
            return new int[]{nums[j], j + 1};   // [duplicate, missing]
    return new int[]{-1, -1};
}
```

#### Example

```
Input: [1, 2, 2, 4]
After sort: [1, 2, 2, 4]
idx2: nums[2]=2≠3 → return [2, 3] ✓
```

---

### Problem 11 — Find All Numbers Disappeared in an Array
**LeetCode #448 | Difficulty: Easy | Company: Amazon, Facebook | Category: All Missing**

> Same as Problem 3 — LeetCode version. Find all missing from [1, n].

#### Alternative: Negative Marking approach (no sort needed)

```java
public List<Integer> findDisappearedNumbers(int[] nums) {
    // Mark visited by negating at index nums[i]-1
    for (int i = 0; i < nums.length; i++) {
        int idx = Math.abs(nums[i]) - 1;
        if (nums[idx] > 0) nums[idx] = -nums[idx];
    }
    List<Integer> missing = new ArrayList<>();
    for (int i = 0; i < nums.length; i++)
        if (nums[i] > 0) missing.add(i + 1);   // positive → never visited
    return missing;
}
```

> **Note:** Cyclic sort approach (Problem 3) is equally valid. Negative marking is an alternative O(n)/O(1) trick.

#### Example

```
Input: [4, 3, 2, 7, 8, 2, 3, 1]

Negate at index abs(nums[i])-1:
  4→idx3: neg → [4,3,2,-7,8,2,3,1]
  3→idx2: neg → [4,3,-2,-7,8,2,3,1]
  2→idx1: neg → [4,-3,-2,-7,8,2,3,1]
  7→idx6: neg → [4,-3,-2,-7,8,2,-3,1]
  8→idx7: neg → [4,-3,-2,-7,8,2,-3,-1]
  2→idx1: already neg (skip)
  3→idx2: already neg (skip)
  1→idx0: neg → [-4,-3,-2,-7,8,2,-3,-1]

Positive at idx4(=5) and idx5(=6) → missing: [5,6] ✓
```

---

### Problem 12 — First Missing Positive (LeetCode Hard)
**LeetCode #41 | Difficulty: Hard | Company: Amazon, Google, Facebook | Category: Missing Positive**

> Same as Problem 7 — the canonical LeetCode Hard version. Must be O(n) time, O(1) space.

> The solution is exactly the cyclic sort with range guard from Problem 7.

#### Key interview talking points

```
Why is this Hard?
→ Most candidates try HashSet (O(n) space) or sorting (O(n log n)) first.
→ The trick: use the array itself as a HashSet by placing each number at its index.
→ Ignore numbers ≤ 0 and > n — they can never be the answer for an n-length array.

Why O(n) despite nested while?
→ Each swap moves one element to its final position permanently.
→ An element can be swapped at most n times total across all iterations.
→ Amortized O(1) per element → O(n) total.
```

#### Java code (same as P7, shown for completeness)

```java
public int firstMissingPositive(int[] nums) {
    int n = nums.length, i = 0;
    while (i < n) {
        int home = nums[i] - 1;
        if (nums[i] > 0 && nums[i] <= n && nums[i] != nums[home]) {
            swap(nums, i, home);
        } else {
            i++;
        }
    }
    for (int j = 0; j < n; j++)
        if (nums[j] != j + 1) return j + 1;
    return n + 1;
}
```

#### Example

```
Input: [7, 8, 9, 11, 12]  (all out of range [1,5])

No swaps happen (all nums[i] > n=5).
Scan: nums[0]=7≠1 → return 1 ✓

Input: [1, 2, 3]
After sort: [1,2,3]. All correct → return n+1=4 ✓
```

---

## Quick Pattern Reference

| Problem | Category | Swap condition | Detection |
|---------|----------|---------------|-----------|
| Cyclic Sort | Core | `nums[i] != nums[home]` | — (just sort) |
| Missing Number | Missing | `nums[i] < n && nums[i] != i` | first `nums[i] != i` |
| All Missing Numbers | All Missing | `nums[i] != nums[home]` | all `j` where `nums[j] != j+1` |
| Find Duplicate | Duplicate | stop when `nums[i]==nums[home]` | return `nums[i]` |
| All Duplicates | All Duplicates | `nums[i] != nums[home]` | all `j` where `nums[j] != j+1` → `nums[j]` |
| Corrupt Pair | Combined | `nums[i] != nums[home]` | `[nums[j], j+1]` at mismatch |
| Smallest Missing Positive | Missing+ | range guard `[1,n]` | first `nums[j] != j+1` |
| First K Missing | K Missing | range guard `[1,n]` | collect + extend beyond n |
| Set Mismatch (#645) | Combined | `nums[i] != nums[home]` | `[nums[j], j+1]` at mismatch |
| Disappeared Numbers (#448) | All Missing | negative marking OR cyclic | positive index after marking |
| First Missing Positive (#41) | Missing+ | range guard `[1,n]` | first `nums[j] != j+1` |
| Missing Number (#268) | Missing | XOR or Gauss or cyclic | depends on approach |
