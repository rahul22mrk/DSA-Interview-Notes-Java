# HashMap Pattern — Solved Problems (16 Problems)

> **Pattern family:** Frequency / Lookup / Grouping
> **Notes & Templates:** [01_hashmap_notes.md](./01_hashmap_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Frequency Count
- [P1 — Two Sum](#problem-1--two-sum)
- [P2 — Valid Anagram](#problem-2--valid-anagram)
- [P3 — First Non-Repeating Character](#problem-3--first-non-repeating-character)
- [P4 — Maximum Number of Balloons](#problem-4--maximum-number-of-balloons)
- [P5 — Longest Palindrome](#problem-5--longest-palindrome)
- [P6 — Ransom Note](#problem-6--ransom-note)
- [P10 — Top K Frequent Elements](#problem-10--top-k-frequent-elements)

### Category 2 — Complement Lookup
- [P1 — Two Sum](#problem-1--two-sum) *(also here)*

### Category 3 — Prefix Sum
- [P7 — Subarray Sum Equals K](#problem-7--subarray-sum-equals-k)

### Category 4 — Index Tracking + Sliding Window
- [P8 — Longest Substring Without Repeating](#problem-8--longest-substring-without-repeating-characters)

### Category 5 — Grouping / Bucketing
- [P9 — Group Anagrams](#problem-9--group-anagrams)

### Category 6 — Two-Map Bidirectional
- [P12 — Isomorphic Strings](#problem-12--isomorphic-strings)
- [P13 — Word Pattern](#problem-13--word-pattern)

### Category 7 — HashSet Membership
- [P11 — Jewels and Stones](#problem-11--jewels-and-stones)
- [P14 — Contains Duplicate II](#problem-14--contains-duplicate-ii)
- [P15 — Longest Consecutive Sequence](#problem-15--longest-consecutive-sequence)

### Category 8 — Design
- [P16 — LRU Cache](#problem-16--lru-cache)

---

## Category 1 — Frequency Count

---

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


## Category 3 — Prefix Sum

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


## Category 4 — Index Tracking + Sliding Window

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


## Category 5 — Grouping / Bucketing

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


## Category 1 (continued) — Frequency Count

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


## Category 7 — HashSet Membership

---

### Problem 11 — Jewels and Stones
**LeetCode #771 | Difficulty: Easy | Variant: HashSet Lookup**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Add every char in `jewels` to a `HashSet` | O(j) build |
| 2 | Loop through `stones`, count if in set | O(s) lookup |

> **Key insight:** HashSet gives O(1) lookup per stone — single pass after building the jewel set.

#### Java code

```java
public int numJewelsInStones(String jewels, String stones) {
    Set<Character> jewelSet = new HashSet<>();
    for (char c : jewels.toCharArray()) jewelSet.add(c);

    int count = 0;
    for (char c : stones.toCharArray())
        if (jewelSet.contains(c)) count++;
    return count;
}
```

#### Example

```
jewels = "aA", stones = "aAAbbbb"
jewelSet = {'a','A'}
stones: a✓ A✓ A✓ b✗ b✗ b✗ b✗  →  count = 3
Output: 3 ✓
```

---


## Category 6 — Two-Map Bidirectional

---

### Problem 12 — Isomorphic Strings
**LeetCode #205 | Difficulty: Easy | Variant: Two-Map Bidirectional**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Map `s[i] → t[i]` AND `t[i] → s[i]` | bidirectional mapping |
| 2 | If `s[i]` already mapped to something ≠ `t[i]` | return false |
| 3 | If `t[i]` already mapped to something ≠ `s[i]` | return false |

> **Why two maps?** One map catches `s→t` conflicts. The reverse map catches when two different chars in `s` both map to the same char in `t`.

#### Java code

```java
public boolean isIsomorphic(String s, String t) {
    Map<Character, Character> sToT = new HashMap<>();
    Map<Character, Character> tToS = new HashMap<>();

    for (int i = 0; i < s.length(); i++) {
        char sc = s.charAt(i), tc = t.charAt(i);

        if (sToT.containsKey(sc) && sToT.get(sc) != tc) return false;
        if (tToS.containsKey(tc) && tToS.get(tc) != sc) return false;

        sToT.put(sc, tc);
        tToS.put(tc, sc);
    }
    return true;
}
```

#### Example

```
s = "egg", t = "add"
i=0: e→a, a→e ✓   i=1: g→d, d→g ✓   i=2: g→d matches ✓
Output: true ✓

s = "foo", t = "bar"
i=1: o→a, a→o ✓   i=2: o→r? but sToT[o]=a ≠ r → false ✓
```

---

### Problem 13 — Word Pattern
**LeetCode #290 | Difficulty: Easy | Variant: Two-Map Bidirectional**

> Check if string `s` follows the same pattern as `pattern` (each letter maps to exactly one word and vice versa).

#### Java code

```java
public boolean wordPattern(String pattern, String s) {
    String[] words = s.split(" ");
    if (pattern.length() != words.length) return false;

    Map<Character, String> charToWord = new HashMap<>();
    Map<String, Character> wordToChar = new HashMap<>();

    for (int i = 0; i < pattern.length(); i++) {
        char c = pattern.charAt(i);
        String w = words[i];

        if (charToWord.containsKey(c) && !charToWord.get(c).equals(w)) return false;
        if (wordToChar.containsKey(w) && wordToChar.get(w) != c)       return false;

        charToWord.put(c, w);
        wordToChar.put(w, c);
    }
    return true;
}
```

#### Example

```
pattern = "abba", s = "dog cat cat dog"
i=0: a→dog, dog→a ✓   i=1: b→cat, cat→b ✓
i=2: b→cat matches ✓   i=3: a→dog matches ✓
Output: true ✓

pattern = "abba", s = "dog cat cat fish"
i=3: a→dog but word="fish" ≠ dog → false ✓
```

---


## Category 7 (continued) — HashSet Membership

---

### Problem 14 — Contains Duplicate II
**LeetCode #219 | Difficulty: Easy | Variant: Index Tracking**

> Return true if any two equal elements exist with indices at most `k` apart.

#### Java code

```java
public boolean containsNearbyDuplicate(int[] nums, int k) {
    Map<Integer, Integer> lastIndex = new HashMap<>();

    for (int i = 0; i < nums.length; i++) {
        if (lastIndex.containsKey(nums[i]) && i - lastIndex.get(nums[i]) <= k)
            return true;
        lastIndex.put(nums[i], i);
    }
    return false;
}
```

#### Example

```
nums = [1,2,3,1], k = 3
i=3: 1 seen at 0, diff=3 ≤ 3 → true ✓
```

---

### Problem 15 — Longest Consecutive Sequence
**LeetCode #128 | Difficulty: Medium | Variant: HashSet + Sequence Building**

> Find the length of the longest consecutive elements sequence in O(n).

#### Core insight

Only start counting from elements where `num - 1` is NOT in the set (those are sequence starts). Count forward. Each sequence visited exactly once → O(n).

#### Java code

```java
public int longestConsecutive(int[] nums) {
    Set<Integer> numSet = new HashSet<>();
    for (int n : nums) numSet.add(n);

    int maxLen = 0;
    for (int n : numSet) {
        if (!numSet.contains(n - 1)) {   // n is a sequence start
            int len = 1;
            while (numSet.contains(n + len)) len++;
            maxLen = Math.max(maxLen, len);
        }
    }
    return maxLen;
}
```

#### Example

```
nums = [100,4,200,1,3,2]
n=1: 0 not in set → start. 2✓ 3✓ 4✓ 5? No → len=4. maxLen=4
n=100: 99 not in set → start. 101? No → len=1
Output: 4 ✓  ([1,2,3,4])
```

---


## Category 8 — Design

---

### Problem 16 — LRU Cache
**LeetCode #146 | Difficulty: Medium | Company: Amazon, Facebook, Google | Variant: LinkedHashMap / HashMap + DLL**

> Design a data structure with O(1) `get` and `put`. Evict the Least Recently Used item when at capacity.

#### Core insight

`LinkedHashMap` with access-order mode automatically moves accessed entries to the end (most recent). Remove eldest entry when over capacity.

#### Java code (LinkedHashMap — concise)

```java
class LRUCache extends LinkedHashMap<Integer, Integer> {
    private final int capacity;

    public LRUCache(int capacity) {
        super(capacity, 0.75f, true);   // true = access-order
        this.capacity = capacity;
    }

    public int get(int key)             { return super.getOrDefault(key, -1); }
    public void put(int key, int value) { super.put(key, value); }

    @Override
    protected boolean removeEldestEntry(Map.Entry<Integer, Integer> eldest) {
        return size() > capacity;
    }
}
```

#### Java code (HashMap + Doubly Linked List — interview standard)

```java
class LRUCache {
    private final int capacity;
    private final Map<Integer, Node> map = new HashMap<>();
    private final Node head = new Node(0, 0);   // dummy head (most recent)
    private final Node tail = new Node(0, 0);   // dummy tail (LRU end)

    public LRUCache(int capacity) {
        this.capacity = capacity;
        head.next = tail; tail.prev = head;
    }

    public int get(int key) {
        if (!map.containsKey(key)) return -1;
        Node node = map.get(key);
        remove(node); addToFront(node);
        return node.val;
    }

    public void put(int key, int value) {
        if (map.containsKey(key)) remove(map.get(key));
        Node node = new Node(key, value);
        addToFront(node);
        map.put(key, node);
        if (map.size() > capacity) {
            Node lru = tail.prev;
            remove(lru); map.remove(lru.key);
        }
    }

    private void remove(Node n)      { n.prev.next = n.next; n.next.prev = n.prev; }
    private void addToFront(Node n)  { n.next = head.next; n.prev = head; head.next.prev = n; head.next = n; }

    static class Node { int key, val; Node prev, next; Node(int k, int v) { key=k; val=v; } }
}
```

#### Example

```
LRUCache(2)
put(1,1) → {1:1}
put(2,2) → {1:1, 2:2}
get(1)   → order=[2,1]. return 1
put(3,3) → evict LRU=2. {1:1, 3:3}
get(2)   → -1 ✓
put(4,4) → evict LRU=1. {3:3, 4:4}
get(1)   → -1 ✓   get(3) → 3 ✓   get(4) → 4 ✓
```

---


---

## Quick Pattern Reference

| Problem | Category | Key technique |
|---------|----------|---------------|
| Two Sum | Complement Lookup | `containsKey(target - x)`; check before store |
| Valid Anagram | Frequency Count | build freq of s, decrement for t |
| First Non-Repeating | Frequency Count | two passes; find first with count 1 |
| Max Balloons | Frequency Count | divide l,o counts by 2; take min |
| Longest Palindrome | Frequency Count | sum even counts + 1 if any odd |
| Ransom Note | Two-Map Compare | decrement magazine map; 0 → false |
| Subarray Sum = K | Prefix Sum | `map.put(0,1)`; count `prefix-k` hits |
| Longest Substr No Repeat | Index Tracking | `left = max(left, lastSeen+1)` |
| Group Anagrams | Grouping | sorted string as key; `computeIfAbsent` |
| Top K Frequent | Freq + Heap | min-heap size k; O(n log k) |
| Jewels and Stones | HashSet | add jewels, count matching stones |
| Isomorphic Strings | Two-Map Bidirectional | sToT + tToS both must be consistent |
| Word Pattern | Two-Map Bidirectional | charToWord + wordToChar |
| Contains Duplicate II | Index Tracking | `i - lastIndex[val] <= k` |
| Longest Consecutive | HashSet | only count from `num-1` not in set |
| LRU Cache | Design | LinkedHashMap access-order or HashMap+DLL |
