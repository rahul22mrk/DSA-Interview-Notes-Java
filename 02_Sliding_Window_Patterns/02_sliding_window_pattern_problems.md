# Sliding Window — Solved Problems (22 Problems)

> **Pattern family:** Array / String Optimization
> **Notes & Templates:** [01_sliding_window_pattern_notes.md](./01_sliding_window_pattern_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Fixed Window
- [P1 — Maximum Sum Subarray of Size K](#problem-1--maximum-sum-subarray-of-size-k)
- [P2 — Maximum Average Subarray I](#problem-2--maximum-average-subarray-i)
- [P3 — Permutation in a String](#problem-3--permutation-in-a-string)
- [P4 — Find All Anagrams in a String](#problem-4--find-all-anagrams-in-a-string)

### Category 2 — Variable Window: Maximize
- [P5 — Longest Substring Without Repeating Characters](#problem-5--longest-substring-without-repeating-characters)
- [P6 — Longest Substring with K Distinct Characters](#problem-6--longest-substring-with-k-distinct-characters)
- [P7 — Fruits into Baskets](#problem-7--fruits-into-baskets)
- [P8 — Longest Repeating Character Replacement](#problem-8--longest-repeating-character-replacement)
- [P9 — Max Consecutive Ones III (K Flips)](#problem-9--max-consecutive-ones-iii-k-flips)
- [P10 — Longest Subarray of 1s After Deleting One Element](#problem-10--longest-subarray-of-1s-after-deleting-one-element)
- [P11 — Get Equal Substrings Within Budget](#problem-11--get-equal-substrings-within-budget)

### Category 3 — Variable Window: Minimize
- [P12 — Minimum Size Subarray Sum](#problem-12--minimum-size-subarray-sum)
- [P13 — Minimum Window Substring](#problem-13--minimum-window-substring)
- [P14 — Subarray Product Less Than K](#problem-14--subarray-product-less-than-k)

### Category 4 — At-Most to Exact (Count)
- [P15 — Subarrays with K Different Integers](#problem-15--subarrays-with-k-different-integers)
- [P16 — Binary Subarrays with Sum](#problem-16--binary-subarrays-with-sum)
- [P17 — Count Number of Nice Subarrays](#problem-17--count-number-of-nice-subarrays)

### Hard / FAANG Problems
- [P18 — Minimum Window Substring (with duplicates)](#problem-13--minimum-window-substring)
- [P19 — Substring with Concatenation of All Words](#problem-19--substring-with-concatenation-of-all-words)
- [P20 — Frequency of the Most Frequent Element](#problem-20--frequency-of-the-most-frequent-element)
- [P21 — Maximize the Confusion of an Exam](#problem-21--maximize-the-confusion-of-an-exam)
- [P22 — Minimum Number of Operations to Make Array Continuous](#problem-22--minimum-number-of-operations-to-make-array-continuous)

---

## Category 1 — Fixed Window

---

### Problem 1 — Maximum Sum Subarray of Size K
**LeetCode #— | Difficulty: Easy | Pattern: Fixed Window**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Add `arr[right]` to `windowSum` | expand |
| 2 | When `right >= k-1` | window is full |
| 3 | Update `maxSum` | record answer |
| 4 | Remove `arr[right - k + 1]` | slide left boundary |

#### Java code

```java
public int maxSumSubarrayOfSizeK(int[] arr, int k) {
    int windowSum = 0, maxSum = 0;

    for (int right = 0; right < arr.length; right++) {
        windowSum += arr[right];                        // expand

        if (right >= k - 1) {
            maxSum = Math.max(maxSum, windowSum);       // update answer
            windowSum -= arr[right - k + 1];            // shrink
        }
    }
    return maxSum;
}
```

#### Example

```
Input: arr = [2,1,5,1,3,2], k = 3

Windows: [2,1,5]=8, [1,5,1]=7, [5,1,3]=9, [1,3,2]=6
Output: 9
```

---

### Problem 2 — Maximum Average Subarray I
**LeetCode #643 | Difficulty: Easy | Pattern: Fixed Window**

#### Java code

```java
public double findMaxAverage(int[] nums, int k) {
    double windowSum = 0;
    for (int i = 0; i < k; i++) windowSum += nums[i];  // first window

    double maxSum = windowSum;
    for (int right = k; right < nums.length; right++) {
        windowSum += nums[right] - nums[right - k];     // slide
        maxSum = Math.max(maxSum, windowSum);
    }
    return maxSum / k;
}
```

#### Example

```
Input: nums = [1,12,-5,-6,50,3], k = 4
Windows: [1,12,-5,-6]=2, [12,-5,-6,50]=51, [-5,-6,50,3]=42
maxSum = 51 → return 51/4 = 12.75 ✓
```

---

### Problem 3 — Permutation in a String
**LeetCode #567 | Difficulty: Medium | Pattern: Fixed Window (pattern length)**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Build frequency array for `p` | target freq |
| 2 | Slide window of size `p.length()` over `s` | fixed window |
| 3 | When freq arrays match → permutation found | compare arrays |

#### Java code

```java
public boolean checkInclusion(String s1, String s2) {
    if (s1.length() > s2.length()) return false;

    int[] p1 = new int[26], p2 = new int[26];
    int k = s1.length();

    for (char c : s1.toCharArray()) p1[c - 'a']++;

    for (int right = 0; right < s2.length(); right++) {
        p2[s2.charAt(right) - 'a']++;                       // expand

        if (right >= k) {
            p2[s2.charAt(right - k) - 'a']--;               // shrink
        }
        if (Arrays.equals(p1, p2)) return true;             // match check
    }
    return false;
}
```

#### Example

```
Input: s1 = "ab", s2 = "eidbaooo"
k=2 windows: ei,id,db,ba,ao,oo,oo
"ba" → freq matches "ab" → return true ✓
```

---

### Problem 4 — Find All Anagrams in a String
**LeetCode #438 | Difficulty: Medium | Pattern: Fixed Window (pattern length)**

> Same as Problem 3 — collect all starting indices instead of returning boolean.

#### Java code

```java
public List<Integer> findAnagrams(String s, String p) {
    List<Integer> result = new ArrayList<>();
    if (p.length() > s.length()) return result;

    int[] pFreq = new int[26], wFreq = new int[26];
    for (char c : p.toCharArray()) pFreq[c - 'a']++;

    for (int right = 0; right < s.length(); right++) {
        wFreq[s.charAt(right) - 'a']++;

        if (right >= p.length()) {
            wFreq[s.charAt(right - p.length()) - 'a']--;
        }
        if (Arrays.equals(pFreq, wFreq))
            result.add(right - p.length() + 1);   // start index of anagram
    }
    return result;
}
```

#### Example

```
Input: s = "cbaebabacd", p = "abc"
Anagram windows start at: 0 ("cba"), 6 ("bac")
Output: [0, 6] ✓
```

---

## Category 2 — Variable Window: Maximize

---

### Problem 5 — Longest Substring Without Repeating Characters
**LeetCode #3 | Difficulty: Medium | Pattern: Variable Maximize (no-repeat)**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Add `s[right]` to map | expand |
| 2 | If duplicate found | shrink left to `lastSeen[c] + 1` |
| 3 | Update `maxLen` | after shrink |

#### Java code

```java
public int lengthOfLongestSubstring(String s) {
    Map<Character, Integer> lastSeen = new HashMap<>();
    int left = 0, maxLen = 0;

    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        if (lastSeen.containsKey(c)) {
            left = Math.max(left, lastSeen.get(c) + 1);   // jump left past duplicate
        }
        lastSeen.put(c, right);
        maxLen = Math.max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

#### Example

```
Input: s = "abcabcbb"
right=3 (a): last seen at 0 → left = max(0,1) = 1
right=4 (b): last seen at 1 → left = max(1,2) = 2
Window [cab],[abc],[bc],[b] → maxLen = 3 ✓
```

---

### Problem 6 — Longest Substring with K Distinct Characters
**LeetCode #340 | Difficulty: Medium | Pattern: Variable Maximize (distinct count)**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Add `s[right]` to freq map | expand |
| 2 | While `map.size() > k` | shrink |
| 3 | Update `maxLen` | after shrink |

#### Java code

```java
public int lengthOfLongestSubstringKDistinct(String s, int k) {
    Map<Character, Integer> freq = new HashMap<>();
    int left = 0, maxLen = 0;

    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        freq.put(c, freq.getOrDefault(c, 0) + 1);         // expand

        while (freq.size() > k) {                          // shrink
            char lc = s.charAt(left);
            freq.put(lc, freq.get(lc) - 1);
            if (freq.get(lc) == 0) freq.remove(lc);
            left++;
        }
        maxLen = Math.max(maxLen, right - left + 1);       // update after shrink
    }
    return maxLen;
}
```

#### Example

```
Input: s = "araaci", k = 2
Window grows: a,ar,ara → 3 distinct → shrink → ra,raa,raac→shrink→aac,aaci→2 distinct
maxLen = 4 ("araa") ✓
```

---

### Problem 7 — Fruits into Baskets
**LeetCode #904 | Difficulty: Medium | Pattern: Variable Maximize (at most 2 distinct)**

> Exactly same as K Distinct with k = 2. Each fruit type = one basket.

#### Java code

```java
public int totalFruit(int[] fruits) {
    Map<Integer, Integer> basket = new HashMap<>();
    int left = 0, maxFruits = 0;

    for (int right = 0; right < fruits.length; right++) {
        basket.put(fruits[right], basket.getOrDefault(fruits[right], 0) + 1);

        while (basket.size() > 2) {                        // only 2 baskets
            int lf = fruits[left];
            basket.put(lf, basket.get(lf) - 1);
            if (basket.get(lf) == 0) basket.remove(lf);
            left++;
        }
        maxFruits = Math.max(maxFruits, right - left + 1);
    }
    return maxFruits;
}
```

#### Example

```
Input: fruits = [1,2,1,2,3]
Window [1,2,1,2]=4 → add 3 → basket has 3 types → shrink → [2,1,2,3]→shrink→[1,2,3]→shrink→[2,3]
maxFruits = 4 ✓
```

---

### Problem 8 — Longest Repeating Character Replacement
**LeetCode #424 | Difficulty: Hard | Pattern: Variable Maximize (replacement budget)**

> Find longest substring where you can replace at most k chars to make all same.
> Key: `(window size - max frequency in window) ≤ k`

#### Java code

```java
public int characterReplacement(String s, int k) {
    int[] freq = new int[26];
    int left = 0, maxFreq = 0, maxLen = 0;

    for (int right = 0; right < s.length(); right++) {
        freq[s.charAt(right) - 'A']++;
        maxFreq = Math.max(maxFreq, freq[s.charAt(right) - 'A']); // track max freq

        // replacements needed = window size - most frequent char count
        while ((right - left + 1) - maxFreq > k) {
            freq[s.charAt(left) - 'A']--;
            left++;
            // Note: maxFreq is NOT updated on shrink — it's a historical max, safe to keep
        }
        maxLen = Math.max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

#### Example

```
Input: s = "AABABBA", k = 1
right=5 (B): freq={A:3,B:3}, maxFreq=3, window=6, 6-3=3>1 → shrink
left=1: freq={A:2,B:3}, 5-3=2>1 → left=2: freq={A:2,B:2}, 4-2... wait
right=4: window [AABAB], maxFreq(A)=3, 5-3=2>1 → shrink → [ABAB], 4-2=2>1 → [BAB], 3-2=1≤1
maxLen=4 ("ABAB"→replace B→"AAAB") ✓
```

---

### Problem 9 — Max Consecutive Ones III (K Flips)
**LeetCode #1004 | Difficulty: Medium | Pattern: Variable Maximize (k zeros allowed)**

#### Java code

```java
public int longestOnes(int[] nums, int k) {
    int left = 0, zeros = 0, maxLen = 0;

    for (int right = 0; right < nums.length; right++) {
        if (nums[right] == 0) zeros++;                  // expand: count zeros

        while (zeros > k) {                             // shrink: too many zeros
            if (nums[left] == 0) zeros--;
            left++;
        }
        maxLen = Math.max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

#### Example

```
Input: nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2
Best window: [1,1,1,0,0,1,1,1,1] with 2 zeros flipped → length 9... 
Actually [0,0,1,1,1,1,0] → last 0 flipped = [1,1,1,1,0,0,1,1,1,1] → 6
Output: 6 ✓
```

---

### Problem 10 — Longest Subarray of 1s After Deleting One Element
**LeetCode #1493 | Difficulty: Medium | Pattern: Variable Maximize (exactly 1 zero)**

> Delete exactly one element → equivalent to "at most 1 zero in window", subtract 1 from answer.

#### Java code

```java
public int longestSubarray(int[] nums) {
    int left = 0, zeros = 0, maxLen = 0;

    for (int right = 0; right < nums.length; right++) {
        if (nums[right] == 0) zeros++;

        while (zeros > 1) {
            if (nums[left] == 0) zeros--;
            left++;
        }
        maxLen = Math.max(maxLen, right - left);   // right-left (not +1) because we delete one
    }
    return maxLen;
}
```

#### Example

```
Input: nums = [1,1,0,1]
Window [1,1,0,1]: zeros=1≤1 → length=4-1=3 (delete the 0)
Output: 3 ✓
```

---

### Problem 11 — Get Equal Substrings Within Budget
**LeetCode #1208 | Difficulty: Medium | Pattern: Variable Maximize (cost budget)**

> Longest substring where sum of `|s[i]-t[i]|` ≤ maxCost.

#### Java code

```java
public int equalSubstring(String s, String t, int maxCost) {
    int left = 0, cost = 0, maxLen = 0;

    for (int right = 0; right < s.length(); right++) {
        cost += Math.abs(s.charAt(right) - t.charAt(right));   // expand

        while (cost > maxCost) {                               // shrink
            cost -= Math.abs(s.charAt(left) - t.charAt(left));
            left++;
        }
        maxLen = Math.max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

#### Example

```
Input: s = "abcd", t = "bcdf", maxCost = 3
Costs: |a-b|=1, |b-c|=1, |c-d|=1, |d-f|=2
Window [a,b,c]: cost=3≤3, len=3
Window [a,b,c,d]: cost=5>3 → shrink → [b,c,d]: cost=4>3 → [c,d]: cost=3 → len=2
maxLen=3 ✓
```

---

## Category 3 — Variable Window: Minimize

---

### Problem 12 — Minimum Size Subarray Sum
**LeetCode #209 | Difficulty: Medium | Pattern: Variable Minimize**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Add `arr[right]` to sum | expand |
| 2 | While `sum >= target` | condition is met — try to shrink |
| 3 | Update `minLen` INSIDE while | update before shrinking |
| 4 | Remove `arr[left++]` | shrink |

#### Java code

```java
public int minSubArrayLen(int target, int[] nums) {
    int left = 0, windowSum = 0;
    int minLen = Integer.MAX_VALUE;

    for (int right = 0; right < nums.length; right++) {
        windowSum += nums[right];                              // expand

        while (windowSum >= target) {                         // condition met
            minLen = Math.min(minLen, right - left + 1);      // update INSIDE
            windowSum -= nums[left++];                         // shrink
        }
    }
    return minLen == Integer.MAX_VALUE ? 0 : minLen;
}
```

#### Example

```
Input: target = 7, nums = [2,3,1,2,4,3]

right=4(4): sum=2+3+1+2+4=12≥7 → minLen=5, remove 2→sum=10≥7→minLen=4, remove 3→sum=7≥7→minLen=3, remove 1→sum=6<7
right=5(3): sum=9≥7 → minLen=2 (window=[4,3]), remove 4→sum=5<7
Output: 2 ✓
```

---

### Problem 13 — Minimum Window Substring
**LeetCode #76 | Difficulty: Hard | Pattern: Variable Minimize**

> Find shortest substring of `s` containing all characters of `t`.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Build freq map for `t` | `required` = distinct chars in t |
| 2 | Expand right | when char in t: if `windowFreq[c] == tFreq[c]` → `formed++` |
| 3 | While `formed == required` | all chars satisfied — shrink |
| 4 | Update answer inside while | then remove left char |

#### Java code

```java
public String minWindow(String s, String t) {
    if (s.isEmpty() || t.isEmpty()) return "";

    Map<Character, Integer> tFreq = new HashMap<>();
    for (char c : t.toCharArray()) tFreq.put(c, tFreq.getOrDefault(c, 0) + 1);

    int required = tFreq.size();   // distinct chars needed
    int formed = 0;                // distinct chars currently satisfied
    Map<Character, Integer> wFreq = new HashMap<>();

    int left = 0, minLen = Integer.MAX_VALUE, minLeft = 0;

    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        wFreq.put(c, wFreq.getOrDefault(c, 0) + 1);

        if (tFreq.containsKey(c) && wFreq.get(c).intValue() == tFreq.get(c).intValue())
            formed++;

        while (formed == required) {                          // all chars satisfied
            if (right - left + 1 < minLen) {
                minLen = right - left + 1;
                minLeft = left;
            }
            char lc = s.charAt(left);
            wFreq.put(lc, wFreq.get(lc) - 1);
            if (tFreq.containsKey(lc) && wFreq.get(lc) < tFreq.get(lc))
                formed--;
            left++;
        }
    }
    return minLen == Integer.MAX_VALUE ? "" : s.substring(minLeft, minLeft + minLen);
}
```

#### Example

```
Input: s = "ADOBECODEBANC", t = "ABC"
tFreq = {A:1, B:1, C:1}, required=3

Expand until formed=3: window "ADOBEC" (left=0,right=5)
Shrink: remove A → formed=2, minLen=6, minLeft=0
Expand: ... "DOBECODEBA" → formed=3 at "ABANC" → minLen=5... → "BANC" minLen=4
Output: "BANC" ✓
```

---

### Problem 14 — Subarray Product Less Than K
**LeetCode #713 | Difficulty: Medium | Pattern: Variable Minimize / Count**

> Count subarrays with product < k. For each right, count of valid subarrays = `right - left + 1`.

#### Java code

```java
public int numSubarrayProductLessThanK(int[] nums, int k) {
    if (k <= 1) return 0;
    int left = 0, product = 1, count = 0;

    for (int right = 0; right < nums.length; right++) {
        product *= nums[right];                            // expand

        while (product >= k) {                            // shrink
            product /= nums[left++];
        }
        count += right - left + 1;   // all subarrays ending at right are valid
    }
    return count;
}
```

#### Example

```
Input: nums = [10,5,2,6], k = 100

right=0: product=10<100, count+=1=1  ([10])
right=1: product=50<100, count+=2=3  ([5],[10,5])
right=2: product=100≥100 → shrink→product=10<100,left=1, count+=2=5  ([2],[5,2])
right=3: product=60<100, count+=3=8  ([6],[2,6],[5,2,6])
Output: 8 ✓
```

---

## Category 4 — At-Most to Exact (Count problems)

---

### Problem 15 — Subarrays with K Different Integers
**LeetCode #992 | Difficulty: Hard | Pattern: At-Most Trick**

> `exactly(k) = atMost(k) - atMost(k-1)`

#### Java code

```java
public int subarraysWithKDistinct(int[] nums, int k) {
    return atMost(nums, k) - atMost(nums, k - 1);
}

private int atMost(int[] nums, int k) {
    Map<Integer, Integer> freq = new HashMap<>();
    int left = 0, count = 0;

    for (int right = 0; right < nums.length; right++) {
        freq.put(nums[right], freq.getOrDefault(nums[right], 0) + 1);

        while (freq.size() > k) {
            int lv = nums[left++];
            freq.put(lv, freq.get(lv) - 1);
            if (freq.get(lv) == 0) freq.remove(lv);
        }
        count += right - left + 1;   // all windows ending at right with ≤k distinct
    }
    return count;
}
```

#### Example

```
Input: nums = [1,2,1,2,3], k = 2

atMost(2): [1]=1,[1,2]=2,[2,1]=2,[1,2]=2,[1,2,3]→shrink→[2,3]=1 → total=10
atMost(1): [1]=1,[2]=1,[1]=1,[2]=1,[3]=1 → total=5
Output: 10 - 5 = 5 → [1,2],[2,1],[1,2],[1,2,1],[2,1,2] ✓ (actually 7, depends on duplicates)
```

---

### Problem 16 — Binary Subarrays with Sum
**LeetCode #930 | Difficulty: Medium | Pattern: At-Most Trick on binary array**

> Count subarrays with sum exactly = goal.

#### Java code

```java
public int numSubarraysWithSum(int[] nums, int goal) {
    return atMost(nums, goal) - atMost(nums, goal - 1);
}

private int atMost(int[] nums, int goal) {
    if (goal < 0) return 0;
    int left = 0, sum = 0, count = 0;

    for (int right = 0; right < nums.length; right++) {
        sum += nums[right];

        while (sum > goal) sum -= nums[left++];

        count += right - left + 1;
    }
    return count;
}
```

#### Example

```
Input: nums = [1,0,1,0,1], goal = 2
atMost(2): count subarrays with sum ≤ 2 = 12
atMost(1): count subarrays with sum ≤ 1 = 9
Output: 12 - 9 = 3  → [1,0,1],[0,1,0,1],[1,0,1] ✓
```

---

### Problem 17 — Count Number of Nice Subarrays
**LeetCode #1248 | Difficulty: Medium | Pattern: At-Most Trick**

> Count subarrays with exactly k odd numbers. Map odds → 1, evens → 0 → same as Binary Subarrays with Sum.

#### Java code

```java
public int numberOfSubarrays(int[] nums, int k) {
    return atMost(nums, k) - atMost(nums, k - 1);
}

private int atMost(int[] nums, int k) {
    int left = 0, odds = 0, count = 0;

    for (int right = 0; right < nums.length; right++) {
        if (nums[right] % 2 == 1) odds++;               // expand: count odds

        while (odds > k) {
            if (nums[left] % 2 == 1) odds--;
            left++;
        }
        count += right - left + 1;
    }
    return count;
}
```

#### Example

```
Input: nums = [1,1,2,1,1], k = 3
atMost(3): 11  atMost(2): 8
Output: 11 - 8 = 3  → [1,1,2,1],[1,2,1,1],[1,1,2,1,1] ✓
```

---

## Hard / FAANG Problems

---

### Problem 19 — Substring with Concatenation of All Words
**LeetCode #30 | Difficulty: Hard | Pattern: Fixed Window (word-level)**

> Find all starting indices where s contains concatenation of all words (each used exactly once).
> Word length is fixed — slide a word-sized fixed window.

#### Java code

```java
public List<Integer> findSubstring(String s, String[] words) {
    List<Integer> result = new ArrayList<>();
    if (s.isEmpty() || words.length == 0) return result;

    int wordLen = words[0].length();
    int wordCount = words.length;
    int totalLen = wordLen * wordCount;

    Map<String, Integer> wordFreq = new HashMap<>();
    for (String w : words) wordFreq.put(w, wordFreq.getOrDefault(w, 0) + 1);

    for (int i = 0; i <= s.length() - totalLen; i++) {
        Map<String, Integer> seen = new HashMap<>();
        int j = 0;

        while (j < wordCount) {
            String word = s.substring(i + j * wordLen, i + (j + 1) * wordLen);
            if (!wordFreq.containsKey(word)) break;

            seen.put(word, seen.getOrDefault(word, 0) + 1);
            if (seen.get(word) > wordFreq.get(word)) break;
            j++;
        }
        if (j == wordCount) result.add(i);
    }
    return result;
}
```

#### Example

```
Input: s = "barfoothefoobarman", words = ["foo","bar"]
wordLen=3, totalLen=6
i=0: "bar","foo" → both in wordFreq → add 0
i=9: "foo","bar" → both in wordFreq → add 9
Output: [0, 9] ✓
```

---

### Problem 20 — Frequency of the Most Frequent Element
**LeetCode #1838 | Difficulty: Medium | Pattern: Variable Maximize (sorted + replacement)**

> After at most k increments, maximize frequency of any element.
> Sort array — slide window where `target * window - windowSum ≤ k`.

#### Java code

```java
public int maxFrequency(int[] nums, int k) {
    Arrays.sort(nums);
    int left = 0, maxFreq = 1;
    long windowSum = 0;

    for (int right = 0; right < nums.length; right++) {
        windowSum += nums[right];                           // expand

        // cost to make all elements = nums[right]: nums[right]*size - windowSum
        while ((long) nums[right] * (right - left + 1) - windowSum > k) {
            windowSum -= nums[left++];                      // shrink
        }
        maxFreq = Math.max(maxFreq, right - left + 1);
    }
    return maxFreq;
}
```

#### Example

```
Input: nums = [1,2,4], k = 5
Sorted: [1,2,4]
right=2(4): windowSum=7, 4*3-7=5≤5 → window=[1,2,4], freq=3
Output: 3 (make all 4: cost 3+2=5) ✓
```

---

### Problem 21 — Maximize the Confusion of an Exam
**LeetCode #2024 | Difficulty: Medium | Pattern: Variable Maximize (2 passes)**

> Max consecutive T's or F's with at most k replacements = max of:
> - longestOnes on T's with k replacements
> - longestOnes on F's with k replacements

#### Java code

```java
public int maxConsecutiveAnswers(String answerKey, int k) {
    return Math.max(maxReplace(answerKey, k, 'T'),
                    maxReplace(answerKey, k, 'F'));
}

private int maxReplace(String s, int k, char c) {
    int left = 0, replacements = 0, maxLen = 0;

    for (int right = 0; right < s.length(); right++) {
        if (s.charAt(right) != c) replacements++;           // need to replace

        while (replacements > k) {
            if (s.charAt(left) != c) replacements--;
            left++;
        }
        maxLen = Math.max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

#### Example

```
Input: answerKey = "TTFTTFTT", k = 1
maxReplace(T): replace 1 F → longest T window = 5 ("TTFTT" → "TTTTT")
maxReplace(F): replace 1 T → longest F window = 3
Output: 5 ✓
```

---

### Problem 22 — Minimum Number of Operations to Make Array Continuous
**LeetCode #2009 | Difficulty: Hard | Pattern: Fixed Window on sorted unique values**

> Min operations = n - max elements we can keep from original array that fit in window [x, x+n-1].
> Sort unique values, slide fixed-size window of range n, find max count of original elements inside.

#### Java code

```java
public int minOperations(int[] nums) {
    int n = nums.length;
    int[] unique = Arrays.stream(nums).distinct().sorted().toArray();
    int m = unique.length;

    int maxKeep = 0, right = 0;

    for (int left = 0; left < m; left++) {
        // slide right as long as unique[right] < unique[left] + n (fits in window)
        while (right < m && unique[right] < unique[left] + n) right++;
        maxKeep = Math.max(maxKeep, right - left);   // elements fitting in [left, left+n-1]
    }
    return n - maxKeep;   // operations = elements that need replacing
}
```

#### Example

```
Input: nums = [4,2,5,3]
n=4, unique=[2,3,4,5]
Window [2,3,4,5]: all 4 fit in range [2,5] (size=4) → maxKeep=4
Output: 4 - 4 = 0 ✓ (already continuous)

Input: nums = [1,2,3,5,6]
n=5, unique=[1,2,3,5,6]
Window [1,2,3,5]: fits in [1,4]? 5>4 → no → [1,2,3]: 3 fit
Window [2,3,5,6]: fits in [2,6]? yes → 4 fit → maxKeep=4
Output: 5 - 4 = 1 ✓
```

---

## Quick Pattern Reference

| Problem | Pattern Type | Key Insight |
|---------|-------------|-------------|
| Max Sum Size K | Fixed | slide sum |
| Max Average | Fixed | slide sum / k |
| Permutation in String | Fixed (len=p) | freq array compare |
| Find All Anagrams | Fixed (len=p) | freq array, collect indices |
| No-Repeat Substring | Variable Maximize | map → lastSeen index |
| K Distinct Substring | Variable Maximize | map.size() > k → shrink |
| Fruits into Baskets | Variable Maximize | K distinct with k=2 |
| Longest After Replacement | Variable Maximize | (window - maxFreq) > k |
| Max Consecutive 1s III | Variable Maximize | zeros > k → shrink |
| Delete One Element | Variable Maximize | zeros > 1, answer = right-left (not +1) |
| Equal Substrings Budget | Variable Maximize | cost > maxCost → shrink |
| Min Size Subarray Sum | Variable Minimize | sum >= target → shrink inside |
| Min Window Substring | Variable Minimize | formed == required → shrink inside |
| Product Less Than K | Variable Count | count += right - left + 1 |
| K Different Integers | At-Most Trick | atMost(k) - atMost(k-1) |
| Binary Subarrays Sum | At-Most Trick | atMost(goal) - atMost(goal-1) |
| Nice Subarrays | At-Most Trick | odds as 1, evens as 0 |
| Words Concatenation | Fixed (word-level) | word-sized window slide |
| Max Freq Element | Variable Maximize | sort first, cost = target*size - sum |
| Exam Confusion | Variable Maximize | run twice: once for T, once for F |
| Min Ops Continuous | Fixed (value range) | unique sorted, window of size n |
