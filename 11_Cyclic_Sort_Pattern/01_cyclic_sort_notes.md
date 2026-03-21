# Cyclic Sort Pattern — Complete Notes

> **Pattern family:** Array / Sorting / Index Mapping
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
| "array of n integers in range [1, n]" | cyclic sort — every number belongs at index `num-1` |
| "find the missing number" | sort in-place then scan for `nums[i] != i+1` |
| "find all missing numbers" | sort in-place then collect all `i` where `nums[i] != i+1` |
| "find the duplicate number" | sort in-place then find `nums[i] != i+1` (num already placed) |
| "find all duplicates" | sort in-place then collect all `nums[i] != i+1` |
| "corrupt pair (missing + duplicate)" | sort then find both the wrong index and the value there |
| "smallest missing positive" | cyclic sort with range [1, n] then scan |
| "first k missing positives" | sort then collect missing positives in order |
| "in-place" + "O(1) space" + range-constrained array | cyclic sort |
| "numbers in range [0, n] or [1, n]" | index can represent the number — cyclic sort |

### Brute force test

```
Brute force: sort the array → scan for anomalies → O(n log n) time, O(1) space
→ Or use a HashSet to track seen numbers → O(n) time but O(n) space

Interviewer says "O(n) time AND O(1) space" → neither works above.
→ Cyclic Sort: use the array ITSELF as a HashMap — place each number at its
  "correct index" (num-1 for range [1,n]) → O(n) time, O(1) space.
```

### The 5 confirming signals

**Signal 1 — Numbers are in a range [1, n] or [0, n]**
> This is the key constraint. If each number has a "home index" (`num-1` for [1,n]),
> you can place every number in its correct position in one pass.

**Signal 2 — "Find missing / duplicate / corrupt" in such an array**
> After sorting correctly, any deviation reveals the anomaly.
> `nums[i] != i+1` → either `i+1` is missing OR `nums[i]` is a duplicate.

**Signal 3 — O(1) space constraint with O(n) time**
> No HashSet allowed. No extra array. The only O(1) approach is to use
> the array indices themselves as a tracking structure.

**Signal 4 — "Find all" missing or "find all" duplicates**
> Cyclic sort places every number correctly in one pass.
> A second pass collects all anomalies — still O(n) total.

**Signal 5 — "Smallest missing positive" (even if range is not explicit)**
> Treat array as [1, n] range. Ignore numbers outside [1, n].
> After sorting, first index where `nums[i] != i+1` gives the answer.

### Decision flowchart

```
Array has numbers in a constrained range [1,n] or [0,n]?
        │
        ▼
YES — use Cyclic Sort (place each num at index num-1)
        │
        ├── Find ONE missing number
        │       └── scan for first i where nums[i] != i+1 → missing = i+1
        │
        ├── Find ALL missing numbers
        │       └── collect all i where nums[i] != i+1
        │
        ├── Find ONE duplicate
        │       └── during sort: nums[i] == nums[nums[i]-1] → duplicate found
        │       └── OR after sort: find i where nums[i] != i+1 → nums[i] is duplicate
        │
        ├── Find ALL duplicates
        │       └── after sort: collect nums[i] for all i where nums[i] != i+1
        │
        ├── Corrupt pair (one missing, one duplicate)
        │       └── after sort: find i where nums[i] != i+1
        │           → nums[i] = duplicate, i+1 = missing
        │
        ├── Smallest missing positive (range may not be explicit)
        │       └── treat [1,n] as valid range, ignore others, scan after sort
        │
        └── First k missing positives
                └── sort then scan, collect missing positives in order
```

---

## 2. What is this pattern?

**Core idea:** When an array contains numbers in range `[1, n]`, each number `x` has an exact "home index" at position `x-1`. Cyclic Sort places every number at its home index in a single pass — O(n) time, O(1) space.

```
Array: [3, 1, 4, 2]
Home:   3→idx2, 1→idx0, 4→idx3, 2→idx1

After cyclic sort: [1, 2, 3, 4]  ← every nums[i] = i+1
```

**The swap mechanism:**

```java
// While nums[i] is not at its home index — swap it to its home
while (nums[i] != i + 1) {
    int home = nums[i] - 1;             // home index for nums[i]
    if (nums[i] == nums[home]) break;   // duplicate — stop (avoid infinite loop)
    swap(nums, i, home);                // move nums[i] to its home
}
```

**Why it's O(n):**
Each swap moves at least one element to its final position. An element already at its home is never swapped again. So despite the nested while loop, total swaps ≤ n → O(n) overall.

**Why it works for missing/duplicate detection:**
After sorting, if `nums[i] != i+1`, one of two things happened:
- `i+1` is missing from the array (something else is at index `i`)
- `nums[i]` is a duplicate (it already placed itself at another index)

---

## 3. Core rules

**Rule 1 — Always check for duplicates before swapping (avoid infinite loop)**
```java
// WRONG — infinite loop if nums[i] == nums[home] (duplicate)
while (nums[i] != i + 1) {
    int home = nums[i] - 1;
    swap(nums, i, home);   // if nums[i] == nums[home], swap forever!
}

// CORRECT — break on duplicate
while (nums[i] != i + 1) {
    int home = nums[i] - 1;
    if (nums[i] == nums[home]) break;   // already placed a copy there — stop
    swap(nums, i, home);
}
```

**Rule 2 — For range [0, n], home index = nums[i] itself (not nums[i]-1)**
```java
// Range [1, n] → home index = nums[i] - 1
swap(nums, i, nums[i] - 1);

// Range [0, n] or [0, n-1] → home index = nums[i]
swap(nums, i, nums[i]);
```

**Rule 3 — Ignore numbers outside [1, n] for "smallest missing positive"**
```java
// WRONG — tries to place numbers like 0, -1, or 1000 → ArrayIndexOutOfBounds
while (nums[i] != i + 1) {
    swap(nums, i, nums[i] - 1);

// CORRECT — skip numbers outside valid range
while (nums[i] >= 1 && nums[i] <= n && nums[i] != nums[nums[i] - 1]) {
    swap(nums, i, nums[i] - 1);
}
```

**Rule 4 — After the sort pass, i does NOT auto-increment when a swap happens**
```java
// WRONG — increments i even after swap (misses numbers)
for (int i = 0; i < n; i++) {
    swap(nums, i, nums[i] - 1);   // i++ happens even though new nums[i] needs checking!

// CORRECT — only increment i when nums[i] is already correct or unplaceable
int i = 0;
while (i < n) {
    int home = nums[i] - 1;
    if (nums[i] >= 1 && nums[i] <= n && nums[i] != nums[home]) {
        swap(nums, i, home);      // re-check same i after swap
    } else {
        i++;                      // move on only when stable
    }
}
```

---

## 4. 2-Question framework

### Question 1 — What does the answer look like?

| Answer | Variant |
|--------|---------|
| Single missing number | Cyclic sort → first `i` where `nums[i] != i+1` |
| All missing numbers | Cyclic sort → collect all `i` where `nums[i] != i+1` |
| Single duplicate | Cyclic sort → number that couldn't be placed at home |
| All duplicates | Cyclic sort → collect all `nums[i]` where `nums[i] != i+1` |
| Corrupt pair (missing + duplicate) | Cyclic sort → same scan, two values at once |
| Smallest missing positive | Cyclic sort with range guard → first `i` where `nums[i] != i+1` |
| First k missing positives | Cyclic sort → scan + extend beyond n |

### Question 2 — What is the valid range?

| Range | Home index formula | Handle out-of-range? |
|-------|-------------------|----------------------|
| `[1, n]` (standard) | `nums[i] - 1` | No |
| `[0, n]` | `nums[i]` | No |
| Arbitrary (e.g., missing positive, any array) | `nums[i] - 1` | Yes — skip if `< 1` or `> n` |
| `[1, n+1]` (one extra) | `nums[i] - 1` | Check bounds |

> **Decision shortcut:**
> - "range [1,n], find missing/duplicate" → cyclic sort, `home = nums[i]-1`
> - "find smallest missing positive" → same but guard out-of-range
> - "find all missing" → collect in second pass
> - "corrupt pair" → same as finding missing+duplicate simultaneously
> - "first k missing" → sort + scan + go beyond n

---

## 5. Variants table

> **Common core:** place `nums[i]` at index `nums[i]-1` if not already there
> **What differs:** what you do when `nums[i] != i+1` after the sort

| Variant | Sort Pass | Detection Pass | Return |
|---------|-----------|----------------|--------|
| Missing Number | standard cyclic sort | first `nums[i] != i+1` | `i+1` |
| All Missing Numbers | standard cyclic sort | all `i` where `nums[i] != i+1` | list of `i+1` |
| Find Duplicate | break on duplicate during sort | first `nums[i] != i+1` | `nums[i]` |
| All Duplicates | break on duplicate during sort | all `i` where `nums[i] != i+1` | list of `nums[i]` |
| Corrupt Pair | standard cyclic sort | find i where `nums[i] != i+1` | `[nums[i], i+1]` |
| Smallest Missing Positive | cyclic sort with range guard | first `nums[i] != i+1` | `i+1` |
| First K Missing | cyclic sort with range guard | collect k misses; extend past n | list |

---

## 6. Universal Java template

```java
// ─── TEMPLATE A: Cyclic Sort (standard range [1, n]) ─────────────────────────
private void cyclicSort(int[] nums) {
    int i = 0;
    while (i < nums.length) {
        int home = nums[i] - 1;                     // home index for nums[i]
        if (nums[i] != nums[home]) {                // not at home AND no duplicate at home
            swap(nums, i, home);                    // send nums[i] to its home
        } else {
            i++;                                    // already correct or duplicate — move on
        }
    }
}

private void swap(int[] nums, int i, int j) {
    int tmp = nums[i]; nums[i] = nums[j]; nums[j] = tmp;
}


// ─── TEMPLATE B: Find Single Missing (after sort) ─────────────────────────────
// After cyclicSort, first index where nums[i] != i+1 is the answer
int findMissing(int[] nums) {
    cyclicSort(nums);
    for (int i = 0; i < nums.length; i++)
        if (nums[i] != i + 1) return i + 1;        // i+1 is missing
    return nums.length + 1;                         // all present → n+1 is missing
}


// ─── TEMPLATE C: Find All Missing (after sort) ───────────────────────────────
List<Integer> findAllMissing(int[] nums) {
    cyclicSort(nums);
    List<Integer> missing = new ArrayList<>();
    for (int i = 0; i < nums.length; i++)
        if (nums[i] != i + 1) missing.add(i + 1);
    return missing;
}


// ─── TEMPLATE D: Find Single Duplicate (during sort) ─────────────────────────
int findDuplicate(int[] nums) {
    int i = 0;
    while (i < nums.length) {
        int home = nums[i] - 1;
        if (nums[i] != i + 1) {
            if (nums[i] == nums[home]) return nums[i];  // duplicate found
            swap(nums, i, home);
        } else {
            i++;
        }
    }
    return -1;
}


// ─── TEMPLATE E: Find All Duplicates (after sort) ────────────────────────────
List<Integer> findAllDuplicates(int[] nums) {
    cyclicSort(nums);
    List<Integer> duplicates = new ArrayList<>();
    for (int i = 0; i < nums.length; i++)
        if (nums[i] != i + 1) duplicates.add(nums[i]);
    return duplicates;
}


// ─── TEMPLATE F: Smallest Missing Positive (range guard) ─────────────────────
int firstMissingPositive(int[] nums) {
    int n = nums.length, i = 0;
    while (i < n) {
        int home = nums[i] - 1;
        if (nums[i] > 0 && nums[i] <= n && nums[i] != nums[home]) {
            swap(nums, i, home);                    // in-range and not duplicate
        } else {
            i++;                                    // out of range or already placed
        }
    }
    for (int j = 0; j < n; j++)
        if (nums[j] != j + 1) return j + 1;
    return n + 1;                                   // all 1..n present → n+1
}


// ─── TEMPLATE G: First K Missing Positives ────────────────────────────────────
List<Integer> firstKMissingPositive(int[] nums, int k) {
    int n = nums.length, i = 0;
    // Step 1: cyclic sort with range guard
    while (i < n) {
        int home = nums[i] - 1;
        if (nums[i] > 0 && nums[i] <= n && nums[i] != nums[home]) {
            swap(nums, i, home);
        } else {
            i++;
        }
    }
    // Step 2: collect missing in [1, n]
    List<Integer> missing = new ArrayList<>();
    Set<Integer> extraNums = new HashSet<>();
    for (int j = 0; j < n && missing.size() < k; j++) {
        if (nums[j] != j + 1) {
            missing.add(j + 1);
            extraNums.add(nums[j]);
        }
    }
    // Step 3: extend beyond n if needed
    int next = n + 1;
    while (missing.size() < k) {
        if (!extraNums.contains(next)) missing.add(next);
        next++;
    }
    return missing;
}
```

---

## 7. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                          → VARIANT                  → KEY CODE
────────────────────────────────────────────────────────────────────────────────────────
"array [1,n], find missing number"         → Cyclic sort + scan       → first nums[i] != i+1 → i+1 missing
"array [1,n], find all missing"            → Cyclic sort + collect    → all i where nums[i] != i+1
"array [1,n], find the duplicate"          → Cyclic sort + break      → nums[i]==nums[home] → return nums[i]
"array [1,n], find all duplicates"         → Cyclic sort + collect    → nums[i] where nums[i] != i+1
"array [1,n], corrupt pair"                → Cyclic sort + scan       → [nums[i], i+1] at first mismatch
"smallest missing positive"                → Cyclic sort + range guard → first nums[j] != j+1 → j+1
"first k missing positives"                → Sort + scan + extend     → collect in [1,n] then beyond
```

**Burn these into memory:**
```java
// HOME INDEX formula:
int home = nums[i] - 1;   // for range [1, n]
int home = nums[i];        // for range [0, n]

// SWAP CONDITION — always check BEFORE swapping:
nums[i] != nums[home]     // no duplicate at home position

// DETECTION — after sort:
if (nums[i] != i + 1) → i+1 is MISSING, nums[i] is the DUPLICATE

// RANGE GUARD for arbitrary arrays:
nums[i] >= 1 && nums[i] <= n && nums[i] != nums[nums[i]-1]
```

---

## 8. Common mistakes

### Mistake 1 — Swapping without checking for duplicates (infinite loop)

```java
// BUG — [1, 1] → nums[0]=1, home=0 → nums[0]==nums[0] → swap with itself forever
while (nums[i] != i + 1) {
    swap(nums, i, nums[i] - 1);   // no duplicate check → infinite loop

// FIX — check if home position already has the same value
while (nums[i] != i + 1) {
    int home = nums[i] - 1;
    if (nums[i] == nums[home]) break;   // stop — can't place this number
    swap(nums, i, home);
}
```

### Mistake 2 — Using `for` loop instead of `while` (skips re-check)

```java
// BUG — after swap, new nums[i] is never checked at the same index
for (int i = 0; i < n; i++) {
    while (nums[i] != i + 1 && nums[i] != nums[nums[i]-1])
        swap(nums, i, nums[i] - 1);
// This works only because of the inner while — but the outer for is misleading

// CORRECT and clearest pattern:
int i = 0;
while (i < n) {
    int home = nums[i] - 1;
    if (nums[i] != nums[home]) swap(nums, i, home);   // re-check same i
    else i++;                                          // only advance when stable
}
```

### Mistake 3 — ArrayIndexOutOfBounds for "smallest missing positive"

```java
// BUG — nums[i] could be 0, negative, or > n → home index out of bounds
while (nums[i] != i + 1) {
    int home = nums[i] - 1;   // if nums[i] = 0 → home = -1 → crash!
    swap(nums, i, home);

// FIX — range guard before computing home
if (nums[i] >= 1 && nums[i] <= n && nums[i] != nums[nums[i] - 1]) {
    swap(nums, i, nums[i] - 1);
} else {
    i++;
}
```

### Mistake 4 — Returning wrong value for "all missing" (off by one)

```java
// BUG — returns nums[i] instead of the missing number (i+1)
if (nums[i] != i + 1) missing.add(nums[i]);   // WRONG — nums[i] is the duplicate!

// FIX — the missing number is the expected value i+1, not what's there
if (nums[i] != i + 1) missing.add(i + 1);     // CORRECT
```

### Mistake 5 — Not handling n+1 as missing for "find missing number"

```java
// BUG — if all numbers 1..n are present (e.g., no missing in [1,n]),
// the loop finds no mismatch and returns nothing
for (int i = 0; i < n; i++)
    if (nums[i] != i + 1) return i + 1;
// Forgot the fallback!

// FIX — if loop completes without finding mismatch, n+1 is missing
return nums.length + 1;   // or return n+1
```

### Mistake 6 — Confusing duplicate and missing in corrupt pair

```java
// BUG — returning [i+1, nums[i]] instead of [nums[i], i+1]
if (nums[i] != i + 1) return new int[]{i + 1, nums[i]};
// [0] should be duplicate (what's there), [1] should be missing (what should be there)

// FIX
if (nums[i] != i + 1) return new int[]{nums[i], i + 1};
// nums[i] = duplicate value, i+1 = missing value
```

---

## 9. Complexity summary

| Problem | Time | Space | Notes |
|---------|------|-------|-------|
| Cyclic Sort | O(n) | O(1) | each element moves to final position at most once |
| Find Missing Number | O(n) | O(1) | sort pass + single scan |
| Find All Missing Numbers | O(n) | O(1) | sort pass + single scan (result list not counted) |
| Find Duplicate Number | O(n) | O(1) | sort pass with early exit on duplicate |
| Find All Duplicates | O(n) | O(1) | sort pass + single scan |
| Find Corrupt Pair | O(n) | O(1) | sort pass + single scan |
| Smallest Missing Positive | O(n) | O(1) | sort with range guard + scan |
| First K Missing Positives | O(n + k) | O(k) | sort + scan + extend (result list) |

**General rules:**
- Cyclic sort is always **O(n) time** — despite the inner while loop, each element is swapped at most once to its final position.
- Space is always **O(1)** — only index variables, no extra data structures.
- The sort pass and detection pass are separate O(n) passes → still O(n) total.
- For "First K Missing Positives", the extension step can add up to k iterations beyond n → O(n + k).

---

*Cyclic Sort is the most underrated pattern in DSA interviews.*
*It converts O(n) space HashSet solutions into O(1) space — interviewers love this.*
*Master the swap condition check — it's the only tricky part.*
