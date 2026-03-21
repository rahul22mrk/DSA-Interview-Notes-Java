# Sliding Window — Notes & Templates

> **Pattern family:** Array / String Optimization
> **Difficulty range:** Easy → Hard
> **Language:** Java
> **Problems file:** [02_sliding_window_pattern_problems.md](./02_sliding_window_pattern_problems.md)

---

## Table of Contents

1. [How to identify this pattern](#1-how-to-identify-this-pattern) ← **start here**
2. [What is this pattern?](#2-what-is-this-pattern)
3. [Core rules](#3-core-rules)
4. [2-Question framework](#4-2-question-framework)
5. [Variants table](#5-variants-table)
   - [5b. Pattern categories — all types covered](#5b-pattern-categories--all-types-covered)
6. [Universal Java template](#6-universal-java-template)
7. [Quick reference cheatsheet](#7-quick-reference-cheatsheet)
8. [Common mistakes](#8-common-mistakes)
9. [Complexity summary](#9-complexity-summary)

---

## 1. How to identify this pattern

### Keyword scanner

| If you see this... | It means |
|--------------------|----------|
| "subarray / substring of size k" | fixed window |
| "maximum / minimum sum of subarray of size k" | fixed window |
| "longest substring with at most k distinct" | variable window (maximize) |
| "smallest subarray with sum ≥ target" | variable window (minimize) |
| "no-repeat / without repeating characters" | variable window with HashSet/Map |
| "permutation / anagram of pattern in string" | fixed window (pattern length) |
| "minimum window containing all characters" | variable window (minimize) |
| "replace at most k characters" | variable window with frequency map |
| "contiguous subarray / substring" | sliding window candidate |
| "subarray product less than k" | variable window |

### Brute force test

```
Brute force: check every subarray — O(n²) or O(n³)
→ If you need max/min/count of a contiguous subarray/substring property
  AND that property is monotone (adding element doesn't decrease window validity)
→ Sliding Window = O(n)

Key insight: instead of recomputing from scratch each time,
SLIDE the window — add one element on right, remove one on left.
```

### The 5 confirming signals

**Signal 1 — "Contiguous subarray or substring"**
> Non-contiguous = DP or greedy. Contiguous + optimize = Sliding Window.

**Signal 2 — Fixed size k given**
> Window never changes size → Fixed window. Slide one step at a time.

**Signal 3 — "Longest / maximum" with a constraint**
> Expand right always, shrink left when constraint violated → Variable window maximize.

**Signal 4 — "Shortest / minimum" with a constraint**
> Expand right until condition met, then shrink left as much as possible → Variable window minimize.

**Signal 5 — "At most k" convertible to exact count**
> `exactly(k) = atMost(k) - atMost(k-1)` → use variable window twice.

### Decision flowchart

```
Problem asks about contiguous subarray/substring?
        │
        ├── YES → Is window size fixed (given as k)?
        │              ├── YES → Fixed Window
        │              └── NO  → Is it maximize or minimize?
        │                             ├── MAXIMIZE → Variable Window (expand right, shrink on violation)
        │                             └── MINIMIZE → Variable Window (expand until met, shrink as much as possible)
        │                             └── COUNT EXACT k → At Most trick: atMost(k) - atMost(k-1)
        │
        └── NO → Not Sliding Window (try DP / Two Pointers / Binary Search)
```

---

## 2. What is this pattern?

A **window** is a contiguous portion of an array or string defined by two pointers — `left` and `right`. Instead of recomputing the entire window from scratch each step, you **slide** it:

```
Expand:  right++  (add new element to window)
Shrink:  left++   (remove oldest element from window)
```

This converts O(n²) brute force into O(n) by reusing computation.

```
arr = [2, 1, 5, 2, 3, 2], k = 3

Window [2,1,5] → sum=8
Slide  [1,5,2] → sum = 8 - 2 + 2 = 8  (don't recompute from scratch)
Slide  [5,2,3] → sum = 8 - 1 + 3 = 10
Slide  [2,3,2] → sum = 10 - 5 + 2 = 7
```

**Two fundamentally different window types:**

| Type | Window size | Right pointer | Left pointer | Goal |
|------|------------|--------------|-------------|------|
| **Fixed** | always = k | moves every step | moves every step (right - k) | aggregate over all windows of size k |
| **Variable** | changes | always moves right | moves when condition violated (maximize) OR when condition met (minimize) | find optimal window |

---

## 3. Core rules

**Rule 1 — Fixed window: add right, remove left simultaneously**
```java
// Window size always = k
for (int right = 0; right < n; right++) {
    // add arr[right] to window
    windowSum += arr[right];

    if (right >= k - 1) {
        // window is full — use result
        maxSum = Math.max(maxSum, windowSum);
        // remove leftmost element
        windowSum -= arr[right - k + 1];   // left = right - k + 1
    }
}
```

**Rule 2 — Variable window maximize: shrink until valid, never discard answer**
```java
int left = 0;
for (int right = 0; right < n; right++) {
    // expand — add arr[right]

    while (/* window invalid */) {
        // shrink — remove arr[left]
        left++;
    }
    // window is now valid — update answer
    maxLen = Math.max(maxLen, right - left + 1);
}
```

**Rule 3 — Variable window minimize: shrink as long as valid, update answer inside shrink**
```java
int left = 0;
for (int right = 0; right < n; right++) {
    // expand — add arr[right]

    while (/* window still valid — can shrink more */) {
        // update answer BEFORE shrinking
        minLen = Math.min(minLen, right - left + 1);
        // shrink — remove arr[left]
        left++;
    }
}
```

> **Key difference:**
> - Maximize → update answer **after** the while loop (window just became valid)
> - Minimize → update answer **inside** the while loop (window is currently valid)

---

## 4. 2-Question framework

### Question 1 — Is the window size fixed or variable?

| Answer | Type | Clue words |
|--------|------|-----------|
| Size k given explicitly | Fixed Window | "subarray of size k", "window of length k" |
| Size changes based on condition | Variable Window | "longest", "shortest", "at most k", "minimum window" |

### Question 2 — What are you optimizing? (variable window only)

| Goal | Approach | Update answer |
|------|----------|--------------|
| Maximize window (longest/max) | shrink when **invalid** | after while loop |
| Minimize window (shortest/min) | shrink when **valid** | inside while loop |
| Count windows with exact k | `atMost(k) - atMost(k-1)` | count = right - left + 1 per step |

> **Decision shortcut:**
> - "fixed size k" → fixed window
> - "longest / maximum" + constraint → variable maximize
> - "shortest / minimum" + condition → variable minimize
> - "count subarrays with exactly k" → at-most trick
> - "permutation / anagram of pattern" → fixed window = pattern.length()

---

## 5. Variants table

> **Common core:** `left` and `right` pointers, expand right, conditionally shrink left  
> **What differs:** when to shrink, what to track, when to update answer

| Variant | Track in window | Shrink condition | Answer update |
|---------|----------------|-----------------|---------------|
| Fixed window — max/min sum | running sum | always when `right >= k-1` | each full window |
| Fixed window — pattern match | char frequency map | always when `right >= k-1` | when map matches |
| Variable — maximize length | char/int frequency | when constraint violated | after shrink |
| Variable — minimize length | running sum | when condition still holds | inside shrink loop |
| Variable — at most k distinct | distinct count | when distinct > k | `right - left + 1` per step |
| Variable — at most k replacements | max freq in window | when `(window - maxFreq) > k` | after shrink |
| At-most to exact | — | `atMost(k) - atMost(k-1)` | accumulated count |

---

## 5b. Pattern categories — all types covered

### Category 1 — Fixed Window
> Window size = k throughout. Slide one step at a time.

**Pattern:**
```java
for (int right = 0; right < n; right++) {
    add(arr[right]);
    if (right >= k - 1) {
        updateAnswer();
        remove(arr[right - k + 1]);
    }
}
```

**Problems:** Max Sum Subarray Size K, Find All Anagrams, Permutation in String, Max Consecutive Ones (fixed)

---

### Category 2 — Variable Window: Maximize
> Expand right always. Shrink left only when window becomes **invalid**.  
> Answer = max window size seen while valid.

**Pattern:**
```java
int left = 0;
for (int right = 0; right < n; right++) {
    add(arr[right]);
    while (isInvalid()) {
        remove(arr[left++]);
    }
    maxLen = Math.max(maxLen, right - left + 1);  // update AFTER shrink
}
```

**Sub-types:**
- **2a. Maximize with distinct count limit** — use `HashMap<char, count>`, shrink when `map.size() > k`
- **2b. Maximize with replacement limit** — track `maxFreq`, shrink when `(window - maxFreq) > k`
- **2c. Maximize with no-repeat constraint** — use `HashSet` or `HashMap<char, lastIndex>`

**Problems:** Longest Substring K Distinct, Fruits into Baskets, No-repeat Substring, Longest After Replacement, Max Consecutive Ones III

---

### Category 3 — Variable Window: Minimize
> Expand right until condition **met**. Then shrink left as much as possible.  
> Answer = min window size seen while valid.

**Pattern:**
```java
int left = 0;
for (int right = 0; right < n; right++) {
    add(arr[right]);
    while (isValid()) {
        minLen = Math.min(minLen, right - left + 1);  // update INSIDE shrink
        remove(arr[left++]);
    }
}
```

**Problems:** Smallest Subarray with Given Sum, Minimum Window Substring, Min Size Subarray Sum

---

### Category 4 — At-Most to Exact (Count problems)
> "Exactly k" is hard directly. Convert using:  
> `count(exactly k) = count(at most k) - count(at most k-1)`

**Pattern:**
```java
return atMost(nums, k) - atMost(nums, k - 1);

private int atMost(int[] nums, int k) {
    int left = 0, count = 0;
    for (int right = 0; right < nums.length; right++) {
        // add nums[right]
        while (/* invalid: exceeded k */) left++;
        count += right - left + 1;  // all windows ending at right
    }
    return count;
}
```

**Problems:** Subarrays with K Different Integers, Binary Subarrays with Sum, Count Nice Subarrays

---

### Summary — all pattern types at a glance

| # | Type | Window size | Shrink when | Update answer |
|---|------|------------|-------------|---------------|
| 1 | Fixed window | always k | every step | each full window |
| 2a | Variable maximize (distinct) | grows/shrinks | distinct > k | after shrink |
| 2b | Variable maximize (replace) | grows/shrinks | replacements > k | after shrink |
| 2c | Variable maximize (no-repeat) | grows/shrinks | duplicate found | after shrink |
| 3 | Variable minimize | grows/shrinks | condition still holds | inside shrink |
| 4 | At-most to exact | variable | — | atMost(k) - atMost(k-1) |

---

## 6. Universal Java template

```java
// ─── TEMPLATE A: Fixed Window ─────────────────────────────────────────────────
public int fixedWindow(int[] arr, int k) {
    int windowSum = 0, maxSum = 0;

    for (int right = 0; right < arr.length; right++) {
        windowSum += arr[right];                        // expand

        if (right >= k - 1) {
            maxSum = Math.max(maxSum, windowSum);       // update answer
            windowSum -= arr[right - k + 1];            // shrink: remove leftmost
        }
    }
    return maxSum;
}

// ─── TEMPLATE B: Variable Window — Maximize ───────────────────────────────────
// "Longest substring / subarray satisfying condition"
public int variableMaximize(String s, int k) {
    Map<Character, Integer> freq = new HashMap<>();
    int left = 0, maxLen = 0;

    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        freq.put(c, freq.getOrDefault(c, 0) + 1);      // expand

        while (isInvalid(freq, k)) {                    // shrink until valid
            char lc = s.charAt(left);
            freq.put(lc, freq.get(lc) - 1);
            if (freq.get(lc) == 0) freq.remove(lc);
            left++;
        }
        maxLen = Math.max(maxLen, right - left + 1);    // update AFTER shrink
    }
    return maxLen;
}

// ─── TEMPLATE C: Variable Window — Minimize ───────────────────────────────────
// "Smallest subarray / substring satisfying condition"
public int variableMinimize(int[] arr, int target) {
    int windowSum = 0, left = 0;
    int minLen = Integer.MAX_VALUE;

    for (int right = 0; right < arr.length; right++) {
        windowSum += arr[right];                        // expand

        while (windowSum >= target) {                   // condition MET → shrink
            minLen = Math.min(minLen, right - left + 1); // update INSIDE shrink
            windowSum -= arr[left++];
        }
    }
    return minLen == Integer.MAX_VALUE ? 0 : minLen;
}

// ─── TEMPLATE D: At-Most to Exact (Count exact k) ────────────────────────────
public int countExact(int[] nums, int k) {
    return atMost(nums, k) - atMost(nums, k - 1);
}

private int atMost(int[] nums, int k) {
    Map<Integer, Integer> freq = new HashMap<>();
    int left = 0, count = 0;

    for (int right = 0; right < nums.length; right++) {
        freq.put(nums[right], freq.getOrDefault(nums[right], 0) + 1);

        while (freq.size() > k) {                      // shrink until valid
            int lv = nums[left++];
            freq.put(lv, freq.get(lv) - 1);
            if (freq.get(lv) == 0) freq.remove(lv);
        }
        count += right - left + 1;                     // all valid windows ending at right
    }
    return count;
}

// ─── TEMPLATE E: Fixed Window — Pattern Match (Anagram / Permutation) ─────────
public boolean patternMatch(String s, String p) {
    if (p.length() > s.length()) return false;
    int[] pFreq = new int[26], wFreq = new int[26];

    for (char c : p.toCharArray()) pFreq[c - 'a']++;

    for (int right = 0; right < s.length(); right++) {
        wFreq[s.charAt(right) - 'a']++;                // expand

        if (right >= p.length()) {                      // shrink: remove leftmost
            wFreq[s.charAt(right - p.length()) - 'a']--;
        }
        if (Arrays.equals(pFreq, wFreq)) return true;  // match check
    }
    return false;
}
```

---

## 7. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                              → TYPE                   → KEY OPERATION
──────────────────────────────────────────────────────────────────────────────────────────
"max/min sum of subarray of size k"            → Fixed window           → add right, remove arr[right-k+1]
"permutation / anagram of pattern in s"        → Fixed window           → int[26] freq compare
"longest substring with at most k distinct"    → Variable maximize      → map.size() > k → shrink
"longest with at most k replacements"          → Variable maximize      → (window-maxFreq) > k → shrink
"longest without repeating characters"         → Variable maximize      → duplicate in map → shrink
"smallest subarray with sum ≥ target"          → Variable minimize      → sum >= target → shrink inside
"minimum window containing all chars"          → Variable minimize      → formed==required → shrink inside
"count subarrays with exactly k distinct"      → At-most trick          → atMost(k) - atMost(k-1)
"subarray product less than k"                 → Variable minimize      → product >= k → shrink
"max consecutive ones with k flips"            → Variable maximize      → zeros > k → shrink
```

**Template picker — one question decides:**
```
Fixed size k given?          → Template A (Fixed Window)
Maximize + constraint?       → Template B (Variable Maximize)
Minimize + condition to meet?→ Template C (Variable Minimize)
Count exact k subarrays?     → Template D (At-Most Trick)
Anagram / permutation match? → Template E (Pattern Match)
```

**The one insight that unlocks all variable window problems:**
```
Maximize → shrink when INVALID  → answer AFTER while
Minimize → shrink when VALID    → answer INSIDE while
```

---

## 8. Common mistakes

### Mistake 1 — Updating answer at wrong place (maximize vs minimize)

```java
// BUG (maximize): updating inside shrink loop → counts invalid windows
while (invalid()) { left++; }
maxLen = Math.max(maxLen, right - left + 1);  // WRONG — should be after

// FIX (maximize): update AFTER shrink
while (invalid()) { remove(arr[left]); left++; }
maxLen = Math.max(maxLen, right - left + 1);  // CORRECT

// BUG (minimize): updating after shrink → misses valid windows
while (valid()) { left++; }
minLen = Math.min(minLen, right - left + 1);  // WRONG — already invalid

// FIX (minimize): update INSIDE shrink
while (valid()) {
    minLen = Math.min(minLen, right - left + 1);  // CORRECT
    remove(arr[left]); left++;
}
```

### Mistake 2 — Not handling "no valid window" for minimize

```java
// BUG — returns Integer.MAX_VALUE if no valid window exists
return minLen;

// FIX
return minLen == Integer.MAX_VALUE ? 0 : minLen;
```

### Mistake 3 — Using size() instead of value for distinct count

```java
// BUG — map.size() counts distinct keys, but you may want total count
while (map.size() > k) { ... }   // correct for "at most k distinct"

// But for replacement problems, track maxFreq separately:
maxFreq = Math.max(maxFreq, freq[c - 'a']);
while ((right - left + 1) - maxFreq > k) { ... }
// Note: maxFreq may be stale but safe — it only grows, never causes over-shrinking
```

### Mistake 4 — maxFreq not updated correctly in replacement problems

```java
// BUG — decreasing maxFreq when shrinking (not needed, causes wrong answers)
while ((right - left + 1) - maxFreq > k) {
    freq[s.charAt(left) - 'a']--;
    maxFreq--;   // WRONG — maxFreq is a historical max, don't decrease
    left++;
}

// FIX — only increase maxFreq when expanding, never decrease
maxFreq = Math.max(maxFreq, freq[s.charAt(right) - 'a']);
while ((right - left + 1) - maxFreq > k) {
    freq[s.charAt(left) - 'a']--;
    left++;   // maxFreq stays — safe because window can only shrink to valid size
}
```

### Mistake 5 — Off-by-one in fixed window removal

```java
// BUG — removing wrong element
windowSum -= arr[left];   // left not updated yet → wrong index

// FIX — remove element that just left the window
windowSum -= arr[right - k + 1];   // or: windowSum -= arr[left]; left++;
```

### Mistake 6 — Forgetting to shrink map entry before removing key

```java
// BUG — removing key without decrementing first
map.remove(arr[left]);   // count lost

// FIX — decrement first, then remove if zero
map.put(arr[left], map.get(arr[left]) - 1);
if (map.get(arr[left]) == 0) map.remove(arr[left]);
left++;
```

---

## 9. Complexity summary

| Variant | Time | Space | Notes |
|---------|------|-------|-------|
| Fixed window — sum | O(n) | O(1) | running sum only |
| Fixed window — pattern match (int[26]) | O(n) | O(1) | fixed 26-char array |
| Variable maximize — distinct count | O(n) | O(k) | HashMap of at most k distinct |
| Variable maximize — replacement | O(n) | O(1) | int[26] array |
| Variable maximize — no-repeat | O(n) | O(min(n,α)) | α = alphabet size |
| Variable minimize — sum | O(n) | O(1) | |
| Variable minimize — min window substring | O(n + m) | O(m) | m = pattern length |
| At-most to exact | O(n) | O(k) | two passes of variable window |

**General rules:**
- All sliding window → **O(n) time** — each element enters and leaves the window at most once
- Space is **O(1)** for integer arrays, **O(k)** or **O(alphabet)** for HashMap-based windows
- Never O(n²) — if your solution has nested loops over different ranges, it is not sliding window
