# HashMap Pattern — Complete Notes

> **Pattern family:** Frequency / Lookup / Grouping  
> **Difficulty range:** Easy → Hard  
> **Language:** Java

---

## Table of Contents

1. [How to identify a HashMap problem](#1-how-to-identify-a-hashmap-problem) ← **start here**
2. [What is this pattern?](#2-what-is-this-pattern)
3. [Core rules](#3-core-rules)
4. [2-Question framework](#4-2-question-framework)
5. [Variants table](#5-variants-table)
6. [Universal Java template](#6-universal-java-template)
7. [Solved problems](#7-solved-problems)
8. [Quick reference cheatsheet](#8-quick-reference-cheatsheet)
9. [Common mistakes](#9-common-mistakes)
10. [Complexity summary](#10-complexity-summary)

---

## 1. How to identify a HashMap problem

> **Read this first. Recognizing the pattern is more important than memorizing the solution.**

Use this 3-layer system: scan keywords → test the brute force → confirm the signal.

---

### Layer 1 — Keyword scanner (read the problem statement)

Certain words almost always mean HashMap. Scan for these first.

| If you see this word/phrase... | It likely means... | HashMap role |
|-------------------------------|-------------------|--------------|
| "two numbers that sum to target" | complement lookup | store `value → index` |
| "find a pair with difference k" | complement lookup | store `value`, check `value + k` |
| "count occurrences / frequency" | frequency map | store `value → count` |
| "most frequent / top k" | frequency map + sort | store `value → count` |
| "first non-repeating / unique" | frequency map | count → find first with count 1 |
| "duplicate / already seen" | seen set/map | `set.contains(x)` |
| "anagram / permutation of" | frequency map | compare char counts |
| "group by / classify" | bucketing | `canonical key → list` |
| "subarray with sum k" | prefix sum map | store `prefixSum → count` |
| "longest subarray / substring" | prefix sum or sliding window map | store `prefixSum → first index` |
| "can X be constructed from Y" | two-map compare | check supply ≥ demand |
| "isomorphic / pattern match" | two-map bidirectional | map both directions |

---

### Layer 2 — Brute force test

Write the brute force in your head. If it has a **nested loop**, HashMap probably removes one loop.

```
Brute force has nested loop?
        │
        ├── YES → Inner loop is "searching for something"?
        │              │
        │              ├── YES → HashMap can replace the inner search → O(n)
        │              └── NO  → Maybe sorting or two pointers instead
        │
        └── NO  → Maybe HashMap is not needed (already O(n) or O(log n))
```

**Example:**
```
Problem: "Find if any two numbers sum to target"

Brute force:
  for i in 0..n
    for j in i+1..n          ← inner loop = searching for complement
      if nums[i]+nums[j]==target → return true

Inner loop just searches → replace with HashMap lookup → O(n)
```

---

### Layer 3 — The 5 confirming signals

After keywords and brute force, confirm with these signals:

**Signal 1 — You need O(n) but brute force is O(n²)**  
> The problem says "optimize" or has n ≤ 10^5 (O(n²) would TLE). HashMap is the standard way to go from O(n²) → O(n).

**Signal 2 — You need to "remember" something from earlier in the array**  
> "Have I seen x before?", "What index was x at?", "How many times did x appear before position i?"  
> All of these = store in HashMap as you go.

**Signal 3 — Two things need to be matched or compared**  
> ransomNote ↔ magazine, pattern ↔ string, s ↔ t for isomorphic  
> Two separate entities being compared = two frequency maps.

**Signal 4 — The answer depends on a count or frequency**  
> "how many subarrays", "how many pairs", "most/least frequent"  
> Counting = HashMap values are counts.

**Signal 5 — Elements need to be grouped by a property**  
> "group anagrams", "group by first letter", "classify by remainder"  
> Grouping = HashMap values are lists, key is the canonical property.

---

### The full decision flowchart

```
Read the problem
      │
      ▼
See "pair / sum / complement"?   ──YES──▶  Complement lookup
      │                                     map: value → index
      NO
      │
      ▼
See "count / frequency / most"?  ──YES──▶  Frequency map
      │                                     map: value → count
      NO
      │
      ▼
See "duplicate / seen / exists"? ──YES──▶  HashSet (or map with bool)
      │                                     set: add and check
      NO
      │
      ▼
See "group / anagram / classify"?──YES──▶  Bucketing
      │                                     map: canonical key → list
      NO
      │
      ▼
See "subarray / substring" +      ──YES──▶  Prefix sum + HashMap
"sum = k / longest"?                        map: prefixSum → count/index
      │
      NO
      │
      ▼
See "sliding window" +            ──YES──▶  Window frequency map
"at most k distinct"?                        map: char → count in window
      │
      NO
      │
      ▼
Brute force has nested loop
where inner loop "searches"?     ──YES──▶  HashMap likely removes inner loop
      │
      NO
      │
      ▼
Probably not a HashMap problem
(try sorting / two pointers / binary search)
```

---

### Side-by-side: same topic, different pattern

Sometimes two problems look identical but need different approaches. HashMap is not always the answer.

| Problem | Looks like HashMap? | Actually needs | Why |
|---------|-------------------|----------------|-----|
| Two Sum (unsorted) | YES | HashMap | O(n), single pass |
| Two Sum (sorted array) | maybe | Two pointers | O(n) with no extra space |
| Contains Duplicate | YES | HashSet | no value to store, just existence |
| Longest Consecutive Sequence | YES | HashSet | set for O(1) lookup, no counts |
| Subarray Sum = K | YES | Prefix sum HashMap | need running total |
| Maximum Subarray (Kadane's) | NO | DP (Kadane) | no lookup needed |
| Anagram in string (sliding) | YES | Sliding window + freq map | fixed-size window |
| Valid Anagram (whole string) | YES | Single freq map | no window needed |

---

### Practice: identify the pattern before looking at the answer

```
1. "Given an array, return true if any value appears at least twice."
   Signal: ____________   Pattern: ____________

2. "Given strings s and t, return true if t is an anagram of s."
   Signal: ____________   Pattern: ____________

3. "Find the number of subarrays that sum to k."
   Signal: ____________   Pattern: ____________

4. "Given a list of words, group all anagrams together."
   Signal: ____________   Pattern: ____________

5. "Find the longest substring where no character repeats."
   Signal: ____________   Pattern: ____________
```

<details>
<summary>Answers</summary>

```
1. "appears at least twice"    → duplicate/seen  → HashSet
2. "anagram"                   → frequency map   → map char counts of s, compare with t
3. "subarrays that sum to k"   → prefix sum      → map prefixSum → count
4. "group all anagrams"        → bucketing       → map sorted(word) → list
5. "longest substring, no rep" → sliding window  → map char → last index
```

</details>

---

> **One-line rule to remember:**  
> *If the brute force searches inside a loop — HashMap kills that search. If you need to remember what you've seen — HashMap stores it.*

---

## 2. What is this pattern?

The **HashMap pattern** trades extra memory for speed. Instead of comparing every element against every other element (O(n²)), you store elements in a map as you process them and look up what you need in **O(1)** time.

**Core idea in one line:**  
> *"Store what you've seen. Ask the map instead of re-scanning the array."*

**Why it works:**  
A `HashMap` gives you O(1) average-time `put`, `get`, and `containsKey`. Any problem that naively needs a nested loop — searching for a complement, counting occurrences, grouping items — can be solved in a single pass with a HashMap.

```
Brute force:   for each x → scan entire array for answer  →  O(n²)
HashMap:       for each x → put(x); look up answer in map  →  O(n)
```

---

## 3. Core rules

**Rule 1 — Look up BEFORE you store (Two Sum rule)**  
```java
// WRONG — stores first, then finds: may match element with itself
map.put(nums[i], i);
if (map.containsKey(target - nums[i])) ...   // BUG

// CORRECT — check first, then store
if (map.containsKey(target - nums[i])) return ...;
map.put(nums[i], i);
```

**Rule 2 — Always initialize base cases for prefix-sum maps**  
```java
map.put(0, 1);   // prefix sum problems: "empty prefix" exists once
map.put(0, -1);  // longest subarray problems: index before start
```
Forgetting this causes wrong answers on inputs where the answer starts at index 0.

**Rule 3 — char[] cannot be a HashMap key directly**  
```java
char[] arr = s.toCharArray();
Arrays.sort(arr);

// WRONG — compares references, not content
map.put(arr, list);

// CORRECT — convert to String first
map.put(new String(arr), list);
map.put(Arrays.toString(arr), list);
```

---

## 4. 2-Question framework

Ask these two questions to identify which variant you need:

### Question 1 — What am I storing?

| Answer | Store | Example |
|--------|-------|---------|
| How many times does X appear? | `value → count` | Valid Anagram, Top K |
| Where did I first see X? | `value → index` | Two Sum, Longest Subarray |
| Which group does X belong to? | `canonical key → [items]` | Group Anagrams |
| Have I seen X before? | `value → boolean` (use `Set`) | Contains Duplicate |
| Running total up to here? | `prefixSum → count/index` | Subarray Sum = K |

### Question 2 — What am I asking?

| Answer | Operation | Example |
|--------|-----------|---------|
| Does the complement exist? | `containsKey(target - x)` | Two Sum |
| How many times have I seen X? | `getOrDefault(x, 0)` | Frequency problems |
| What's the earliest index of X? | `get(x)` → compute distance | Longest Subarray |
| What group does X map to? | `computeIfAbsent(key, ...)` | Group Anagrams |
| Can I build this from that? | compare two maps | Ransom Note |

> **Decision shortcut:**  
> - "find pair/sum" → complement lookup  
> - "count/frequency" → frequency map  
> - "duplicate/seen" → HashSet  
> - "group/classify" → bucketing  
> - "longest subarray" → prefix sum + map  

---

## 5. Variants table

> **One thing is common across all 5 patterns:** `HashMap<K, V> map = new HashMap<>()`  
> **What differs:** What is the Key → What is the Value → What do you query from the map  
> Decide these three things first — the code writes itself.

---

### Quick comparison

| Pattern | Key | Value | What you ask the map | Classic problems |
|---------|-----|-------|----------------------|-----------------|
| **Frequency count** | element | count | how many times did x appear? | Valid Anagram, Top K, Balloons |
| **Complement lookup** | value | index | does target-x exist? | Two Sum, 4Sum II |
| **Prefix sum** | prefixSum | count / first index | was prefix-k seen before? | Subarray Sum=K, Longest Subarray |
| **Grouping** | canonical form | `List<item>` | who belongs to this group? | Group Anagrams, Classify |
| **Index tracking** | element | last index seen | where was x last seen? shrink window | Longest Substr No Repeat |

---

### Pattern 1 — Frequency count

**When to use:** "count occurrences", "how many times", "anagram", "most frequent"

```
Key   = element itself   (char, int, string)
Value = how many times it has been seen
Query = map.get(x)  →  compare or check the count
```

```java
Map<Character, Integer> freq = new HashMap<>();

// Build the frequency map
for (char c : s.toCharArray())
    freq.put(c, freq.getOrDefault(c, 0) + 1);

// Query — read the count
freq.get('a');              // how many times 'a' appeared
freq.getOrDefault('z', 0);  // safe read — returns 0 if absent
```

**Problems:** Valid Anagram, Top K Frequent, Max Balloons, Ransom Note, First Non-Repeating, Longest Palindrome

---

### Pattern 2 — Complement lookup

**When to use:** "two numbers that sum to target", "find pair with difference k"

```
Key   = the number itself
Value = its index in the array
Query = map.containsKey(target - x)  →  look for the complement
```

```java
Map<Integer, Integer> seen = new HashMap<>();  // value → index

for (int i = 0; i < nums.length; i++) {
    int complement = target - nums[i];

    // CHECK first — STORE after  (prevents matching an element with itself)
    if (seen.containsKey(complement))
        return new int[]{seen.get(complement), i};

    seen.put(nums[i], i);
}
```

**Problems:** Two Sum, 4Sum II, Pair with given difference

---

### Pattern 3 — Prefix sum

**When to use:** "subarray sum equals k", "longest subarray with sum k", "count subarrays with condition"

```
Key   = running prefix sum
Value = count (for "how many subarrays") OR first index (for "longest subarray")
Query = map.get(prefix - k)  →  find a previous prefix that creates a subarray summing to k
```

```java
// Variant A — COUNT of subarrays with sum = k
Map<Integer, Integer> prefixCount = new HashMap<>();
prefixCount.put(0, 1);   // CRITICAL base case — empty prefix seen once

int prefix = 0, count = 0;
for (int n : nums) {
    prefix += n;
    count += prefixCount.getOrDefault(prefix - k, 0);  // query
    prefixCount.put(prefix, prefixCount.getOrDefault(prefix, 0) + 1);
}

// Variant B — LONGEST subarray with sum = k
Map<Integer, Integer> firstSeen = new HashMap<>();
firstSeen.put(0, -1);   // base case — index before array start

int prefix = 0, maxLen = 0;
for (int i = 0; i < nums.length; i++) {
    prefix += nums[i];
    if (firstSeen.containsKey(prefix - k))
        maxLen = Math.max(maxLen, i - firstSeen.get(prefix - k));
    firstSeen.putIfAbsent(prefix, i);   // store only the first occurrence
}
```

**Problems:** Subarray Sum = K, Longest Subarray Sum K, Contiguous Array (0s and 1s)

---

### Pattern 4 — Grouping / Bucketing

**When to use:** "group by", "classify", "anagram groups", "items with the same property together"

```
Key   = canonical form  (sorted string, remainder, first letter — whatever the shared property is)
Value = list of all items that share this key
Query = map.get(key)  →  retrieve the entire group
```

```java
Map<String, List<String>> groups = new HashMap<>();

for (String s : strs) {
    // Step 1: compute the canonical key — the shared property
    char[] arr = s.toCharArray();
    Arrays.sort(arr);
    String key = new String(arr);   // "eat", "tea", "ate" all become "aet"

    // Step 2: add to that group's bucket
    groups.computeIfAbsent(key, k -> new ArrayList<>()).add(s);
}

return new ArrayList<>(groups.values());
```

**Problems:** Group Anagrams, Group by remainder, Classify strings by pattern

---

### Pattern 5 — Index tracking (+ Sliding Window)

**When to use:** "longest substring without repeating characters", "first non-repeating", "shrink window on duplicate"

```
Key   = element itself
Value = last index where it was seen
Query = map.get(x)  →  where was x last seen?  →  update left pointer
```

```java
Map<Character, Integer> lastSeen = new HashMap<>();  // char → last index seen
int left = 0, maxLen = 0;

for (int right = 0; right < s.length(); right++) {
    char c = s.charAt(right);

    if (lastSeen.containsKey(c)) {
        // Duplicate found — shrink the window from the left
        // Math.max ensures left never moves backwards
        left = Math.max(left, lastSeen.get(c) + 1);
    }

    lastSeen.put(c, right);   // always update to the latest index
    maxLen = Math.max(maxLen, right - left + 1);
}
```

**Problems:** Longest Substring No Repeat, Longest Substring K Distinct, First Non-Repeating

---

### The one question to ask before writing any code

```
"What am I storing as the KEY
 and what am I storing as the VALUE?"

KEY   = the thing you are searching for or grouping by
VALUE = what you need to remember  (count / index / list)

Once these two are clear → the pattern is clear → the code follows.
```

---

## 6. Universal Java template

```java
// ─── SETUP ────────────────────────────────────────────────────────────────────
Map<KeyType, ValueType> map = new HashMap<>();

// Base case — only for prefix-sum variants
// map.put(0, 1);   // for count-based prefix sum
// map.put(0, -1);  // for index-based (longest subarray) prefix sum

// ─── SINGLE PASS ──────────────────────────────────────────────────────────────
for (ElementType x : data) {

    // Step 1: transform x into a key (identity / sort / prefix sum / mod …)
    KeyType key = transform(x);

    // Step 2: ask the map — O(1) lookup
    if (map.containsKey(key)) {
        answer = combine(map.get(key), x);   // found complement / group / duplicate
    }

    // Step 3: store AFTER asking (Two Sum rule — prevents self-match)
    map.put(key, store(x));                  // store value, index, count, list …
}

// ─── QUERY THE MAP ────────────────────────────────────────────────────────────
// Post-loop aggregation if needed (e.g. palindrome length, top-k)
for (Map.Entry<KeyType, ValueType> entry : map.entrySet()) {
    // process entry.getKey(), entry.getValue()
}
```

**Java utility methods you will use constantly:**

```java
map.getOrDefault(key, 0)                                    // safe get with default
map.put(key, map.getOrDefault(key, 0) + 1)                  // increment frequency
map.computeIfAbsent(key, k -> new ArrayList<>()).add(item)  // grouping
map.putIfAbsent(key, value)                                 // store only first occurrence
map.merge(key, 1, Integer::sum)                             // another way to increment
```

---

## 7. Solved problems

---

### Problem 1 — Two Sum
**LeetCode #1 | Difficulty: Easy | Variant: Complement Lookup**

#### Approach table

| Step | Loop over | Condition | Result |
|------|-----------|-----------|--------|
| 1 | `nums[i]` | `map.containsKey(target - nums[i])` | Return `[stored_index, i]` |
| 2 | — | else | `map.put(nums[i], i)` |

#### Java code

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> seen = new HashMap<>();  // value → index

    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];

        if (seen.containsKey(complement)) {
            return new int[]{seen.get(complement), i};
        }
        seen.put(nums[i], i);   // store AFTER checking — avoids self-match
    }
    return new int[]{};
}
```

#### Example

```
Input:  nums = [2, 7, 11, 15], target = 9
i=0: complement=7, map={} → not found, map={2:0}
i=1: complement=2, map={2:0} → FOUND → return [0, 1]
Output: [0, 1]
```

---

### Problem 2 — Valid Anagram
**LeetCode #242 | Difficulty: Easy | Variant: Frequency Count**

#### Approach table

| Step | Loop over | Condition | Result |
|------|-----------|-----------|--------|
| 1 | chars of `s` | always | `freq[c]++` |
| 2 | chars of `t` | `freq[c] == 0` | return `false` |
| 2 | chars of `t` | else | `freq[c]--`, remove if 0 |
| 3 | — | `map.isEmpty()` | return `true` |

#### Java code

```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) return false;

    Map<Character, Integer> freq = new HashMap<>();

    for (char c : s.toCharArray())
        freq.put(c, freq.getOrDefault(c, 0) + 1);

    for (char c : t.toCharArray()) {
        if (!freq.containsKey(c)) return false;
        freq.put(c, freq.get(c) - 1);
        if (freq.get(c) == 0) freq.remove(c);
    }
    return freq.isEmpty();
}
```

#### Example

```
Input:  s = "anagram", t = "nagaram"
After s: {a:3, n:1, g:1, r:1, m:1}
After t: map becomes empty → return true
Output: true
```

---

### Problem 3 — First Non-Repeating Character
**LeetCode #387 | Difficulty: Easy | Variant: Frequency Count + Index Tracking**

#### Approach table

| Step | Loop over | Condition | Result |
|------|-----------|-----------|--------|
| 1 | chars of `s` | always | `freq[c]++` |
| 2 | indices of `s` | `freq[s[i]] == 1` | return `i` |
| 3 | — | no such char | return `-1` |

> **Why loop twice?** HashMap has no guaranteed order. The second loop uses the **string's order** to find the first unique character.

#### Java code

```java
public int firstUniqChar(String s) {
    Map<Character, Integer> freq = new HashMap<>();

    for (char c : s.toCharArray())
        freq.put(c, freq.getOrDefault(c, 0) + 1);

    for (int i = 0; i < s.length(); i++) {
        if (freq.get(s.charAt(i)) == 1)
            return i;
    }
    return -1;
}
```

#### Example

```
Input:  s = "leetcode"
freq:   {l:1, e:2, t:1, c:1, o:1, d:1}
Loop:   l → freq=1 → return 0
Output: 0
```

---

### Problem 4 — Maximum Number of Balloons
**LeetCode #1189 | Difficulty: Easy | Variant: Frequency Count with Division**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Build `freq` map for `text` | count all chars |
| 2 | For each letter in `"balloon"` | divide freq by times needed |
| 3 | Return `min` across all letters | bottleneck letter limits count |

> **Key insight:** `l` and `o` each appear **twice** in "balloon", so divide their frequency by 2.

#### Java code

```java
public int maxNumberOfBalloons(String text) {
    Map<Character, Integer> freq = new HashMap<>();
    for (char c : text.toCharArray())
        freq.put(c, freq.getOrDefault(c, 0) + 1);

    int ans = Integer.MAX_VALUE;
    ans = Math.min(ans, freq.getOrDefault('b', 0) / 1);
    ans = Math.min(ans, freq.getOrDefault('a', 0) / 1);
    ans = Math.min(ans, freq.getOrDefault('l', 0) / 2);  // needs 2
    ans = Math.min(ans, freq.getOrDefault('o', 0) / 2);  // needs 2
    ans = Math.min(ans, freq.getOrDefault('n', 0) / 1);
    return ans;
}
```

#### Example

```
Input:  text = "nlaebolko"
freq:   {n:1, l:2, a:1, e:1, b:1, o:2, k:1}
b:1/1=1  a:1/1=1  l:2/2=1  o:2/2=1  n:1/1=1  →  min=1
Output: 1
```

---

### Problem 5 — Longest Palindrome
**LeetCode #409 | Difficulty: Easy | Variant: Frequency Count + Math**

#### Approach table

| Step | Loop over | Condition | Result |
|------|-----------|-----------|--------|
| 1 | chars of `s` | always | `freq[c]++` |
| 2 | freq values | `count % 2 == 0` | `length += count` |
| 2 | freq values | `count % 2 == 1` | `length += count - 1`, set `oddFound = true` |
| 3 | — | `oddFound` | `length += 1` (center character) |

> **Key insight:** All even-count characters fit in a palindrome. One odd-count character can sit in the center.

#### Java code

```java
public int longestPalindrome(String s) {
    Map<Character, Integer> freq = new HashMap<>();
    for (char c : s.toCharArray())
        freq.put(c, freq.getOrDefault(c, 0) + 1);

    int length = 0;
    boolean oddFound = false;

    for (int count : freq.values()) {
        length += (count / 2) * 2;   // take the even part of every count
        if (count % 2 == 1) oddFound = true;
    }
    return length + (oddFound ? 1 : 0);
}
```

#### Example

```
Input:  s = "abccccdd"
freq:   {a:1, b:1, c:4, d:2}
a:0 (odd)  b:0 (odd)  c:4  d:2  →  length=6, oddFound=true → +1
Output: 7   ("dccaccd")
```

---

### Problem 6 — Ransom Note
**LeetCode #383 | Difficulty: Easy | Variant: Two-Map Comparison**

#### Approach table

| Step | Loop over | Condition | Result |
|------|-----------|-----------|--------|
| 1 | chars of `magazine` | always | `magFreq[c]++` |
| 2 | chars of `ransomNote` | `magFreq[c] == 0` | return `false` |
| 2 | chars of `ransomNote` | else | `magFreq[c]--` |
| 3 | — | loop finishes | return `true` |

> **Key insight:** Decrement the magazine map as you consume letters. If ever 0, magazine is exhausted for that letter.

#### Java code

```java
public boolean canConstruct(String ransomNote, String magazine) {
    Map<Character, Integer> magFreq = new HashMap<>();
    for (char c : magazine.toCharArray())
        magFreq.put(c, magFreq.getOrDefault(c, 0) + 1);

    for (char c : ransomNote.toCharArray()) {
        int available = magFreq.getOrDefault(c, 0);
        if (available == 0) return false;   // not enough supply
        magFreq.put(c, available - 1);      // consume one
    }
    return true;
}
```

#### Example

```
Input:  ransomNote = "aa", magazine = "aab"
magFreq: {a:2, b:1}
note[0]='a': available=2 → put(a,1)
note[1]='a': available=1 → put(a,0)
Loop ends → return true   ✓

Input:  ransomNote = "aa", magazine = "ab"
note[1]='a': available=0 → return false   ✓
```

---

### Problem 7 — Subarray Sum Equals K
**LeetCode #560 | Difficulty: Medium | Variant: Prefix Sum**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Init `map.put(0, 1)` | base case: empty prefix |
| 2 | `prefix += nums[i]` | running sum |
| 3 | `count += map.getOrDefault(prefix - k, 0)` | how many prior prefixes give a subarray of sum k |
| 4 | `map.put(prefix, ...)` | store AFTER querying |

> **Why `map.put(0, 1)`?** If the subarray starts at index 0, `prefix - k == 0`. Without seeding the map, we miss these cases.

#### Java code

```java
public int subarraySum(int[] nums, int k) {
    Map<Integer, Integer> prefixCount = new HashMap<>();
    prefixCount.put(0, 1);   // CRITICAL base case

    int count = 0, prefix = 0;

    for (int n : nums) {
        prefix += n;
        count += prefixCount.getOrDefault(prefix - k, 0);
        prefixCount.put(prefix, prefixCount.getOrDefault(prefix, 0) + 1);
    }
    return count;
}
```

#### Example

```
Input:  nums = [1, 1, 1], k = 2
map={0:1}
i=0: prefix=1, look (1-2)=-1 → 0,  map={0:1,1:1}
i=1: prefix=2, look (2-2)=0  → 1,  map={0:1,1:1,2:1},  count=1
i=2: prefix=3, look (3-2)=1  → 1,  map={0:1,1:1,2:1,3:1},  count=2
Output: 2
```

---

### Problem 8 — Longest Substring Without Repeating Characters
**LeetCode #3 | Difficulty: Medium | Variant: Index Tracking + Sliding Window**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | `right` pointer moves forward | expand window |
| 2 | If `map.containsKey(c)` | shrink left: `left = max(left, map.get(c) + 1)` |
| 3 | `map.put(c, right)` | always update to latest index |
| 4 | `maxLen = max(maxLen, right - left + 1)` | track answer |

> **`Math.max(left, ...)`** prevents left from moving backwards when a duplicate was outside the current window.

#### Java code

```java
public int lengthOfLongestSubstring(String s) {
    Map<Character, Integer> lastSeen = new HashMap<>();  // char → last index
    int left = 0, maxLen = 0;

    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);

        if (lastSeen.containsKey(c)) {
            left = Math.max(left, lastSeen.get(c) + 1);  // shrink window
        }
        lastSeen.put(c, right);
        maxLen = Math.max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

#### Example

```
Input:  s = "abcabcbb"
r=0: a, map={a:0}, len=1
r=1: b, map={a:0,b:1}, len=2
r=2: c, map={a:0,b:1,c:2}, len=3
r=3: a, left=max(0,1)=1, map={a:3,...}, len=3
r=4: b, left=max(1,2)=2, map={b:4,...}, len=3
Output: 3   ("abc")
```

---

### Problem 9 — Group Anagrams
**LeetCode #49 | Difficulty: Medium | Variant: Grouping / Bucketing**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Sort each string's chars | creates canonical key |
| 2 | `map.computeIfAbsent(key, x -> new ArrayList<>()).add(s)` | group into bucket |
| 3 | Return `map.values()` | all groups |

> **Why sorted string as key?** All anagrams have the same sorted form — `"eat"`, `"tea"`, `"ate"` all sort to `"aet"`.

#### Java code

```java
public List<List<String>> groupAnagrams(String[] strs) {
    Map<String, List<String>> groups = new HashMap<>();

    for (String s : strs) {
        char[] arr = s.toCharArray();
        Arrays.sort(arr);
        String key = new String(arr);   // canonical form

        groups.computeIfAbsent(key, k -> new ArrayList<>()).add(s);
    }
    return new ArrayList<>(groups.values());
}
```

#### Example

```
Input:  ["eat","tea","tan","ate","nat","bat"]
"eat"→"aet"  "tea"→"aet"  "tan"→"ant"  "ate"→"aet"  "nat"→"ant"  "bat"→"abt"
Output: [["eat","tea","ate"], ["tan","nat"], ["bat"]]
```

---

### Problem 10 — Top K Frequent Elements
**LeetCode #347 | Difficulty: Medium | Variant: Frequency Count + Sort/Heap**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Build frequency map | `freq[num]++` |
| 2 | Sort entries by value descending | or use a min-heap of size k |
| 3 | Return first k keys | |

#### Java code

```java
// Approach A — sort (simple, O(n log n))
public int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> freq = new HashMap<>();
    for (int n : nums)
        freq.put(n, freq.getOrDefault(n, 0) + 1);

    return freq.entrySet().stream()
        .sorted((a, b) -> b.getValue() - a.getValue())
        .limit(k)
        .mapToInt(Map.Entry::getKey)
        .toArray();
}

// Approach B — min-heap (optimal, O(n log k))
public int[] topKFrequentHeap(int[] nums, int k) {
    Map<Integer, Integer> freq = new HashMap<>();
    for (int n : nums)
        freq.put(n, freq.getOrDefault(n, 0) + 1);

    PriorityQueue<Integer> heap = new PriorityQueue<>(
        (a, b) -> freq.get(a) - freq.get(b)   // min-heap by frequency
    );
    for (int num : freq.keySet()) {
        heap.offer(num);
        if (heap.size() > k) heap.poll();      // evict least frequent
    }

    int[] result = new int[k];
    for (int i = k - 1; i >= 0; i--)
        result[i] = heap.poll();
    return result;
}
```

#### Example

```
Input:  nums = [1,1,1,2,2,3], k = 2
freq:   {1:3, 2:2, 3:1}
top 2:  [1, 2]
Output: [1, 2]
```

---

## 8. Quick reference cheatsheet

```
SIGNAL IN PROBLEM               → PATTERN               → KEY OPERATION
──────────────────────────────────────────────────────────────────────────
"find two numbers that sum to"  → complement lookup     → map.containsKey(target - x)
"count occurrences / frequency" → frequency map         → map.getOrDefault(x, 0) + 1
"find duplicate / contains"     → HashSet               → set.contains(x)
"group / classify / anagram"    → bucketing             → map.computeIfAbsent(key, ...)
"longest subarray with sum k"   → prefix sum + map      → map.get(prefix - k)
"first non-repeating"           → freq map, loop twice  → freq.get(c) == 1
"can X be built from Y"         → two-map compare       → magFreq[c] >= noteFreq[c]
"palindrome length"             → freq map + math       → even counts + 1 center
"sliding window + constraint"   → window freq map       → window.size() > k → shrink
```

**Java API quick-pick:**

```java
map.put(k, map.getOrDefault(k, 0) + 1);                    // increment count
map.merge(k, 1, Integer::sum);                             // same, more concise
map.computeIfAbsent(key, x -> new ArrayList<>()).add(item); // grouping
map.putIfAbsent(key, value);                               // store first occurrence only
map.getOrDefault(key, defaultValue);                       // safe get
map.forEach((k, v) -> { ... });                            // iterate

// When you need sorted keys   → TreeMap
// When you need insert order  → LinkedHashMap (e.g. LRU cache)
```

---

## 9. Common mistakes

### Mistake 1 — Storing before checking (Two Sum self-match bug)

```java
// BUG: nums=[3,3], target=6 → wrongly returns [0,0]
map.put(nums[i], i);
if (map.containsKey(target - nums[i])) ...   // WRONG

// FIX: check first, store after
if (map.containsKey(target - nums[i])) return new int[]{map.get(...), i};
map.put(nums[i], i);                         // CORRECT
```

### Mistake 2 — Missing base case in prefix-sum problems

```java
Map<Integer, Integer> map = new HashMap<>();   // WRONG — misses subarrays from index 0

map.put(0, 1);   // CORRECT for count problems
map.put(0, -1);  // CORRECT for "longest subarray" (index before array start)
```

### Mistake 3 — Using char[] as a HashMap key

```java
map.put(arr, value);                  // WRONG — compares object references
map.put(new String(arr), value);      // CORRECT
map.put(Arrays.toString(arr), value); // CORRECT
```

### Mistake 4 — Left pointer going backwards in sliding window

```java
left = lastSeen.get(c) + 1;                    // WRONG — left can jump back
left = Math.max(left, lastSeen.get(c) + 1);    // CORRECT — only move forward
```

### Mistake 5 — Using HashMap when HashSet is enough

```java
Map<Integer, Boolean> seen = new HashMap<>();  // wasteful
Set<Integer> seen = new HashSet<>();           // correct for existence-only checks
```

### Mistake 6 — NullPointerException on Integer unboxing

```java
int val = map.get(key);                  // NPE if key absent — WRONG
int val = map.getOrDefault(key, 0);      // safe — CORRECT
```

---

## 10. Complexity summary

| Problem | Time | Space | Notes |
|---------|------|-------|-------|
| Two Sum | O(n) | O(n) | single pass |
| Valid Anagram | O(n) | O(1) | at most 26 chars |
| First Non-Repeating | O(n) | O(1) | two passes, alphabet bounded |
| Max Balloons | O(n) | O(1) | fixed 5-letter check |
| Longest Palindrome | O(n) | O(1) | at most 52 chars (a-z + A-Z) |
| Ransom Note | O(n + m) | O(1) | n = note length, m = magazine length |
| Subarray Sum = K | O(n) | O(n) | prefix sum map |
| Longest Substring No Repeat | O(n) | O(min(n,α)) | α = alphabet size |
| Group Anagrams | O(n · k log k) | O(n · k) | k = avg string length |
| Top K Frequent (heap) | O(n log k) | O(n) | better than O(n log n) sort |

**General rule:**
- HashMap gives **O(n) time** at the cost of **O(n) extra space**
- Space is often O(1) or O(alphabet size) when keys are characters
- When ordering matters — use `LinkedHashMap` (insertion order) or `TreeMap` (sorted)

---

*HashMap pattern covers roughly 25–30% of array and string problems in coding interviews.*  
*Master this pattern before moving to sliding window, two pointers, or binary search.*
