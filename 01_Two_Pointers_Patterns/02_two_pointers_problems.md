# Two Pointers — Core Problems (20 Problems)

> **Pattern family:** Array / String / LinkedList Optimization
> **Notes & Templates:** [01_two_pointers_notes.md](./01_two_pointers_notes.md)
> **Extended problems:** [03_two_pointers_extended.md](./03_two_pointers_extended.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Both Ends: Sum Problems
- [P1 — Pair with Target Sum (2Sum II)](#problem-1--pair-with-target-sum)
- [P2 — Triplet Sum to Zero (3Sum)](#problem-2--triplet-sum-to-zero)
- [P3 — Triplet Sum Close to Target (3Sum Closest)](#problem-3--triplet-sum-close-to-target)
- [P4 — Triplets with Smaller Sum](#problem-4--triplets-with-smaller-sum)
- [P5 — Quadruple Sum to Target (4Sum)](#problem-5--quadruple-sum-to-target)

### Category 2 — Both Ends: Reverse / Palindrome / Swap
- [P6 — Valid Palindrome](#problem-6--valid-palindrome)
- [P7 — Reverse Vowels of a String](#problem-7--reverse-vowels-of-a-string)
- [P8 — Squares of a Sorted Array](#problem-8--squares-of-a-sorted-array)

### Category 3 — Same Direction: In-place Modification
- [P9 — Remove Duplicates from Sorted Array](#problem-9--remove-duplicates-from-sorted-array)
- [P10 — Rearrange 0s and 1s](#problem-10--rearrange-0s-and-1s)
- [P11 — Comparing Strings with Backspaces](#problem-11--comparing-strings-with-backspaces)

### Category 4 — Dutch National Flag
- [P12 — Sort Colors (Dutch National Flag)](#problem-12--sort-colors-dutch-national-flag)

### Category 5 — Two Arrays
- [P13 — Merge Sorted Array](#problem-13--merge-sorted-array)
- [P14 — Is Subsequence](#problem-14--is-subsequence)

### Category 6 — Window / Counting Hybrid
- [P15 — Subarrays with Product Less than K](#problem-15--subarrays-with-product-less-than-k)

### Category 7 — Tricky / FAANG
- [P16 — Minimum Window Sort](#problem-16--minimum-window-sort)
- [P17 — Dutch Flag — Remove Palindromic Subsequences](#problem-17--remove-palindromic-subsequences)
- [P18 — Reverse Words in a String](#problem-18--reverse-words-in-a-string)
- [P19 — Trapping Rain Water](#problem-19--trapping-rain-water)
- [P20 — Container with Most Water](#problem-20--container-with-most-water)

---

## Category 1 — Both Ends: Sum Problems

---

### Problem 1 — Pair with Target Sum
**LeetCode #167 | Difficulty: Easy | Company: Amazon | Pattern: Both-ends**

#### Approach table

| Condition | Action |
|-----------|--------|
| `arr[L] + arr[R] == target` | return `[L+1, R+1]` (1-indexed) |
| `arr[L] + arr[R] < target` | `L++` (need bigger) |
| `arr[L] + arr[R] > target` | `R--` (need smaller) |

#### Java code

```java
public int[] twoSum(int[] numbers, int target) {
    int left = 0, right = numbers.length - 1;

    while (left < right) {
        int sum = numbers[left] + numbers[right];
        if (sum == target)      return new int[]{left + 1, right + 1};
        else if (sum < target)  left++;
        else                    right--;
    }
    return new int[]{-1, -1};
}
```

#### Example

```
Input: numbers = [2,7,11,15], target = 9
left=0(2), right=3(15): sum=17 > 9 → right--
left=0(2), right=2(11): sum=13 > 9 → right--
left=0(2), right=1(7):  sum=9 == 9 → return [1,2] ✓
```

---

### Problem 2 — Triplet Sum to Zero (3Sum)
**LeetCode #15 | Difficulty: Medium | Company: Google, Amazon | Pattern: Both-ends in loop**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Sort array | enables two pointers |
| 2 | Outer loop `i` | fix first element |
| 3 | Skip `nums[i] == nums[i-1]` | avoid outer duplicates |
| 4 | Two pointers `L=i+1, R=n-1` | find pair summing to `-nums[i]` |
| 5 | On match: skip inner duplicates | avoid duplicate triplets |

#### Java code

```java
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
                while (left < right && nums[left] == nums[left+1]) left++;
                while (left < right && nums[right] == nums[right-1]) right--;
                left++; right--;
            } else if (sum < 0) left++;
            else right--;
        }
    }
    return result;
}
```

#### Example

```
Input: nums = [-1,0,1,2,-1,-4]
Sorted: [-4,-1,-1,0,1,2]

i=0(-4): L=1,R=5 → sum=-4+-1+2=-3<0→L++; -4+0+2=-2<0→L++; -4+1+2=-1<0→L++; L>=R stop
i=1(-1): L=2,R=5 → sum=-1+-1+2=0 → add[-1,-1,2], skip dups, L=3,R=4
         L=3,R=4 → -1+0+1=0 → add[-1,0,1], L=4,R=3 stop
i=2(-1): same as i=1, skip (dup)
Output: [[-1,-1,2],[-1,0,1]] ✓
```

---

### Problem 3 — Triplet Sum Close to Target (3Sum Closest)
**LeetCode #16 | Difficulty: Medium | Company: Amazon, Adobe | Pattern: Both-ends in loop**

#### Java code

```java
public int threeSumClosest(int[] nums, int target) {
    Arrays.sort(nums);
    int closest = nums[0] + nums[1] + nums[2];

    for (int i = 0; i < nums.length - 2; i++) {
        int left = i + 1, right = nums.length - 1;

        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];

            if (Math.abs(sum - target) < Math.abs(closest - target))
                closest = sum;

            if (sum < target)       left++;
            else if (sum > target)  right--;
            else                    return sum;    // exact match
        }
    }
    return closest;
}
```

#### Example

```
Input: nums = [-1,2,1,-4], target = 1
Sorted: [-4,-1,1,2]

i=0(-4): L=1,R=3: -4+-1+2=-3→closest=-3; -4+1+2=-1→closest=-1
i=1(-1): L=2,R=3: -1+1+2=2→closest=2 (|2-1|=1 < |-1-1|=2)
Output: 2 ✓
```

---

### Problem 4 — Triplets with Smaller Sum
**GFG | Difficulty: Medium | Pattern: Both-ends in loop — count instead of collect**

> Count triplets with sum < target. When `sum < target`, ALL pairs from `left` to `right-1` with current `right` also work → add `right - left` to count.

#### Java code

```java
public int tripletWithSmallerSum(int[] nums, int target) {
    Arrays.sort(nums);
    int count = 0;

    for (int i = 0; i < nums.length - 2; i++) {
        int left = i + 1, right = nums.length - 1;

        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];

            if (sum < target) {
                count += right - left;   // all pairs [left, left+1..right] with i are valid
                left++;
            } else {
                right--;
            }
        }
    }
    return count;
}
```

#### Example

```
Input: nums = [-1,4,2,1,3], target = 5
Sorted: [-1,1,2,3,4]

i=0(-1): L=1,R=4: -1+1+4=4<5 → count+=3(R-L), L=2
         L=2,R=4: -1+2+4=5 not <5 → R=3
         L=2,R=3: -1+2+3=4<5 → count+=1, L=3; L>=R stop
i=1(1):  L=2,R=4: 1+2+4=7 ≥5→R=3; 1+2+3=6 ≥5→R=2; L>=R stop
Output: count=4 ✓
```

---

### Problem 5 — Quadruple Sum to Target (4Sum)
**LeetCode #18 | Difficulty: Medium | Company: Google | Pattern: Both-ends in double loop**

#### Java code

```java
public List<List<Integer>> fourSum(int[] nums, int target) {
    Arrays.sort(nums);
    List<List<Integer>> result = new ArrayList<>();
    int n = nums.length;

    for (int i = 0; i < n - 3; i++) {
        if (i > 0 && nums[i] == nums[i-1]) continue;

        for (int j = i + 1; j < n - 2; j++) {
            if (j > i + 1 && nums[j] == nums[j-1]) continue;

            int left = j + 1, right = n - 1;
            while (left < right) {
                long sum = (long)nums[i] + nums[j] + nums[left] + nums[right];

                if (sum == target) {
                    result.add(Arrays.asList(nums[i],nums[j],nums[left],nums[right]));
                    while (left < right && nums[left] == nums[left+1]) left++;
                    while (left < right && nums[right] == nums[right-1]) right--;
                    left++; right--;
                } else if (sum < target) left++;
                else right--;
            }
        }
    }
    return result;
}
```

#### Example

```
Input: nums = [1,0,-1,0,-2,2], target = 0
Sorted: [-2,-1,0,0,1,2]
Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]] ✓
```

---

## Category 2 — Both Ends: Reverse / Palindrome / Swap

---

### Problem 6 — Valid Palindrome
**LeetCode #125 | Difficulty: Easy | Company: Facebook | Pattern: Both-ends compare**

#### Java code

```java
public boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;

    while (left < right) {
        // Skip non-alphanumeric
        while (left < right && !Character.isLetterOrDigit(s.charAt(left)))  left++;
        while (left < right && !Character.isLetterOrDigit(s.charAt(right))) right--;

        if (Character.toLowerCase(s.charAt(left)) !=
            Character.toLowerCase(s.charAt(right))) return false;

        left++; right--;
    }
    return true;
}
```

#### Example

```
Input: s = "A man, a plan, a canal: Panama"
After cleaning: "amanaplanacanalpanama"
Both ends meet at center → all chars match → true ✓
```

---

### Problem 7 — Reverse Vowels of a String
**LeetCode #345 | Difficulty: Easy | Company: Google | Pattern: Both-ends conditional swap**

#### Java code

```java
public String reverseVowels(String s) {
    char[] arr = s.toCharArray();
    Set<Character> vowels = Set.of('a','e','i','o','u','A','E','I','O','U');
    int left = 0, right = arr.length - 1;

    while (left < right) {
        while (left < right && !vowels.contains(arr[left]))  left++;
        while (left < right && !vowels.contains(arr[right])) right--;

        if (left < right) {
            char temp = arr[left]; arr[left] = arr[right]; arr[right] = temp;
            left++; right--;
        }
    }
    return new String(arr);
}
```

#### Example

```
Input: s = "hello"
Vowels: e(1), o(4) → swap → "holle" ✓
```

---

### Problem 8 — Squares of a Sorted Array
**LeetCode #977 | Difficulty: Easy | Company: Google, Amazon | Pattern: Both-ends fill from end**

> Sorted array has negatives on left, positives on right. Largest squares are at both ends. Fill result array from the back.

#### Java code

```java
public int[] sortedSquares(int[] nums) {
    int n = nums.length;
    int[] result = new int[n];
    int left = 0, right = n - 1, idx = n - 1;

    while (left <= right) {
        int lSq = nums[left] * nums[left];
        int rSq = nums[right] * nums[right];

        if (lSq >= rSq) {
            result[idx--] = lSq;
            left++;
        } else {
            result[idx--] = rSq;
            right--;
        }
    }
    return result;
}
```

#### Example

```
Input: nums = [-4,-1,0,3,10]
left=0(-4,sq=16), right=4(10,sq=100): 16<100 → result[4]=100, right=3
left=0(-4,sq=16), right=3(3,sq=9):   16>9  → result[3]=16, left=1
left=1(-1,sq=1),  right=3(3,sq=9):   1<9   → result[2]=9, right=2
left=1(-1,sq=1),  right=2(0,sq=0):   1>0   → result[1]=1, left=2
left=2=right:     sq=0               → result[0]=0
Output: [0,1,9,16,100] ✓
```

---

## Category 3 — Same Direction: In-place Modification

---

### Problem 9 — Remove Duplicates from Sorted Array
**LeetCode #26 | Difficulty: Easy | Company: Amazon, Microsoft | Pattern: Slow/fast**

#### Java code

```java
public int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;
    int slow = 1;   // slow = next write position (index 0 always kept)

    for (int fast = 1; fast < nums.length; fast++) {
        if (nums[fast] != nums[fast - 1]) {   // new unique element
            nums[slow++] = nums[fast];
        }
    }
    return slow;   // new length
}
```

#### Example

```
Input: nums = [0,0,1,1,1,2,2,3,3,4]
fast=1(0): same as prev → skip
fast=2(1): new → nums[1]=1, slow=2
fast=3(1): same → skip
fast=4(1): same → skip
fast=5(2): new → nums[2]=2, slow=3
...
Output: slow=5, nums=[0,1,2,3,4,...] ✓
```

---

### Problem 10 — Rearrange 0s and 1s
**GFG | Difficulty: Easy | Pattern: Slow/fast partition**

> Move all 0s to front, all 1s to back. In-place O(1) space.

#### Java code

```java
public void rearrange(int[] arr) {
    int slow = 0;   // next position to place a 0

    for (int fast = 0; fast < arr.length; fast++) {
        if (arr[fast] == 0) {
            int temp = arr[slow]; arr[slow] = arr[fast]; arr[fast] = temp;
            slow++;
        }
    }
}
```

#### Example

```
Input: arr = [1,0,1,1,0,1,0]
fast=1(0): swap arr[0]↔arr[1] → [0,1,1,1,0,1,0], slow=1
fast=4(0): swap arr[1]↔arr[4] → [0,0,1,1,1,1,0], slow=2
fast=6(0): swap arr[2]↔arr[6] → [0,0,0,1,1,1,1], slow=3
Output: [0,0,0,1,1,1,1] ✓
```

---

### Problem 11 — Comparing Strings Containing Backspaces
**LeetCode #844 | Difficulty: Medium | Company: Google | Pattern: Reverse traversal two pointers**

> Process both strings from the end, simulating backspace (`#`) by skipping characters.

#### Java code

```java
public boolean backspaceCompare(String s, String t) {
    int i = s.length() - 1, j = t.length() - 1;

    while (i >= 0 || j >= 0) {
        i = nextValidChar(s, i);
        j = nextValidChar(t, j);

        if (i < 0 && j < 0) return true;
        if (i < 0 || j < 0) return false;
        if (s.charAt(i) != t.charAt(j)) return false;

        i--; j--;
    }
    return true;
}

private int nextValidChar(String str, int idx) {
    int backspace = 0;
    while (idx >= 0) {
        if (str.charAt(idx) == '#') { backspace++; idx--; }
        else if (backspace > 0)     { backspace--; idx--; }
        else break;
    }
    return idx;
}
```

#### Example

```
Input: s = "ab#c", t = "ad#c"
s processed: ab#c → ac
t processed: ad#c → ac
Both are "ac" → return true ✓
```

---

## Category 4 — Dutch National Flag

---

### Problem 12 — Sort Colors (Dutch National Flag)
**LeetCode #75 | Difficulty: Medium | Company: Microsoft, Amazon | Pattern: 3-pointer partition**

#### Approach table

| `nums[mid]` | Action | Why |
|-------------|--------|-----|
| 0 | `swap(low,mid)`, `low++`, `mid++` | 0 goes to front |
| 1 | `mid++` | 1 is in correct region |
| 2 | `swap(mid,high)`, `high--` | 2 goes to back — don't mid++ |

#### Java code

```java
public void sortColors(int[] nums) {
    int low = 0, mid = 0, high = nums.length - 1;

    while (mid <= high) {
        if (nums[mid] == 0) {
            swap(nums, low++, mid++);
        } else if (nums[mid] == 1) {
            mid++;
        } else {
            swap(nums, mid, high--);   // don't mid++ — recheck swapped value
        }
    }
}

private void swap(int[] nums, int i, int j) {
    int t = nums[i]; nums[i] = nums[j]; nums[j] = t;
}
```

#### Example

```
Input: nums = [2,0,2,1,1,0]
low=0,mid=0,high=5

mid=0(2): swap(0,5)→[0,0,2,1,1,2], high=4
mid=0(0): swap(0,0)→same, low=1,mid=1
mid=1(0): swap(1,0)→[0,0,2,1,1,2]... wait idx shifted
  After sort: [0,0,1,1,2,2]
Output: [0,0,1,1,2,2] ✓
```

---

## Category 5 — Two Arrays

---

### Problem 13 — Merge Sorted Array
**LeetCode #88 | Difficulty: Easy | Company: Amazon, Google | Pattern: Two arrays from end**

> Merge from the END to avoid overwriting unprocessed elements in `nums1`.

#### Java code

```java
public void merge(int[] nums1, int m, int[] nums2, int n) {
    int i = m - 1, j = n - 1, k = m + n - 1;

    while (i >= 0 && j >= 0) {
        if (nums1[i] >= nums2[j]) nums1[k--] = nums1[i--];
        else                       nums1[k--] = nums2[j--];
    }
    // Copy remaining nums2 (nums1's remaining are already in place)
    while (j >= 0) nums1[k--] = nums2[j--];
}
```

#### Example

```
Input: nums1=[1,2,3,0,0,0] m=3, nums2=[2,5,6] n=3
i=2(3), j=2(6), k=5: 3<6 → nums1[5]=6, j=1
i=2(3), j=1(5), k=4: 3<5 → nums1[4]=5, j=0
i=2(3), j=0(2), k=3: 3>2 → nums1[3]=3, i=1
i=1(2), j=0(2), k=2: 2>=2 → nums1[2]=2, i=0
i=0(1), j=0(2), k=1: 1<2 → nums1[1]=2, j=-1
j<0, i=0(1) remaining → nums1[0]=1
Output: [1,2,2,3,5,6] ✓
```

---

### Problem 14 — Is Subsequence
**LeetCode #392 | Difficulty: Easy | Company: Google | Pattern: Two arrays**

#### Java code

```java
public boolean isSubsequence(String s, String t) {
    int i = 0, j = 0;

    while (i < s.length() && j < t.length()) {
        if (s.charAt(i) == t.charAt(j)) i++;   // match: advance s pointer
        j++;                                     // always advance t
    }
    return i == s.length();   // all of s matched
}
```

#### Example

```
Input: s = "ace", t = "abcde"
j=0(a): match → i=1; j=1(b): no match; j=2(c): match → i=2; j=3(d): no; j=4(e): match → i=3
i==3==s.length() → return true ✓
```

---

## Category 6 — Window / Counting Hybrid

---

### Problem 15 — Subarrays with Product Less than K
**LeetCode #713 | Difficulty: Medium | Company: Amazon | Pattern: Sliding window two pointers**

> For each `right`, shrink `left` until product < k. All subarrays ending at `right` starting from `left` to `right` are valid → add `right - left + 1` to count.

#### Java code

```java
public int numSubarrayProductLessThanK(int[] nums, int k) {
    if (k <= 1) return 0;
    int left = 0, product = 1, count = 0;

    for (int right = 0; right < nums.length; right++) {
        product *= nums[right];

        while (product >= k) product /= nums[left++];

        count += right - left + 1;   // subarrays ending at right: [left..right],[left+1..right],...,[right]
    }
    return count;
}
```

#### Example

```
Input: nums = [10,5,2,6], k = 100
right=0(10): prod=10<100, count+=1=1
right=1(5):  prod=50<100, count+=2=3
right=2(2):  prod=100≥100→div10,left=1,prod=10<100, count+=2=5
right=3(6):  prod=60<100, count+=3=8
Output: 8 ✓
```

---

## Category 7 — Tricky / FAANG

---

### Problem 16 — Minimum Window Sort
**LeetCode #581 | Difficulty: Medium | Company: Amazon, Adobe | Pattern: Both-ends scan inward**

> Find the shortest subarray that, if sorted, makes the whole array sorted.

#### Java code

```java
public int findUnsortedSubarray(int[] nums) {
    int n = nums.length;
    int low = -1, high = -2;   // initialise to make length = 0 when already sorted
    int maxSeen = nums[0], minSeen = nums[n-1];

    for (int i = 1; i < n; i++) {
        maxSeen = Math.max(maxSeen, nums[i]);
        if (nums[i] < maxSeen) high = i;       // extends the unsorted right boundary
    }
    for (int i = n-2; i >= 0; i--) {
        minSeen = Math.min(minSeen, nums[i]);
        if (nums[i] > minSeen) low = i;        // extends the unsorted left boundary
    }
    return high - low + 1;
}
```

#### Example

```
Input: nums = [2,6,4,8,10,9,15]
Left scan  → maxSeen grows. nums[2]=4 < maxSeen=6 → high=2; nums[5]=9 < maxSeen=10 → high=5
Right scan → minSeen shrinks. nums[3]=8 > minSeen=4 → low=3; nums[1]=6 > minSeen=4 → low=1

Output: high - low + 1 = 5 - 1 + 1 = 5  (subarray [6,4,8,10,9]) ✓
```

---

### Problem 17 — Remove Palindromic Subsequences
**LeetCode #1332 | Difficulty: Easy | Company: Amazon | Pattern: Both-ends palindrome check**

> String of only 'a' and 'b'. Remove subsequences (palindromes) to empty the string.
> Answer is always 1 (whole string is palindrome) or 2 (not palindrome — remove all 'a's then all 'b's).

#### Java code

```java
public int removePalindromeSub(String s) {
    int left = 0, right = s.length() - 1;

    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) return 2;  // not palindrome → 2 steps
        left++; right--;
    }
    return 1;   // already palindrome → 1 step
}
```

#### Example

```
Input: s = "ababa" → palindrome → return 1 ✓
Input: s = "abb"   → not palindrome → return 2 ✓
```

---

### Problem 18 — Reverse Words in a String
**LeetCode #151 | Difficulty: Medium | Company: Amazon, Microsoft | Pattern: Both-ends + word reversal**

#### Java code

```java
public String reverseWords(String s) {
    // Split, trim, reverse the list
    String[] words = s.trim().split("\\s+");
    int left = 0, right = words.length - 1;

    while (left < right) {
        String temp = words[left]; words[left] = words[right]; words[right] = temp;
        left++; right--;
    }
    return String.join(" ", words);
}
```

#### Example

```
Input: s = "  the sky is blue  "
Split+trim: ["the","sky","is","blue"]
Reverse:    ["blue","is","sky","the"]
Output: "blue is sky the" ✓
```

---

### Problem 19 — Trapping Rain Water
**LeetCode #42 | Difficulty: Hard | Company: Amazon, Google, Bloomberg | Pattern: Both-ends with max trackers**

#### Core insight

Water at index `i` = `min(maxLeft[i], maxRight[i]) - height[i]`. Two pointers track `maxLeft` and `maxRight` on the fly. Advance the shorter side — its contribution is determined by its own max.

#### Java code

```java
public int trap(int[] height) {
    int left = 0, right = height.length - 1;
    int maxLeft = 0, maxRight = 0, water = 0;

    while (left < right) {
        if (height[left] <= height[right]) {
            if (height[left] >= maxLeft) maxLeft = height[left];
            else water += maxLeft - height[left];
            left++;
        } else {
            if (height[right] >= maxRight) maxRight = height[right];
            else water += maxRight - height[right];
            right--;
        }
    }
    return water;
}
```

#### Example

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6 ✓

Key: advance shorter side — its max determines water above it.
left side: maxLeft grows as we go right
right side: maxRight grows as we go left
```

---

### Problem 20 — Container with Most Water
**LeetCode #11 | Difficulty: Medium | Company: Amazon, Google | Pattern: Both-ends area maximization**

#### Core insight

Area = `min(height[L], height[R]) * (R - L)`. To find more water, we must increase the shorter side (increasing the taller side can't help since min is bottlenecked).

#### Java code

```java
public int maxArea(int[] height) {
    int left = 0, right = height.length - 1, maxWater = 0;

    while (left < right) {
        int water = Math.min(height[left], height[right]) * (right - left);
        maxWater = Math.max(maxWater, water);

        if (height[left] <= height[right]) left++;   // move shorter side inward
        else right--;
    }
    return maxWater;
}
```

#### Example

```
Input: height = [1,8,6,2,5,4,8,3,7]
left=0(1), right=8(7): area=min(1,7)*8=8, maxWater=8, left++ (shorter)
left=1(8), right=8(7): area=min(8,7)*7=49, maxWater=49, right-- (shorter)
left=1(8), right=7(3): area=min(8,3)*6=18, right--
...
Output: 49 ✓
```

---

## Quick Pattern Reference

| Problem | Category | Key move |
|---------|----------|----------|
| Pair with Target Sum | Both-ends sum | L++ or R-- by sum vs target |
| 3Sum | Both-ends in loop | sort + outer + L/R + skip dups |
| 3Sum Closest | Both-ends in loop | track min abs diff |
| Triplets Smaller Sum | Both-ends count | count += R-L when sum < target |
| 4Sum | Both-ends double loop | sort + 2 outer loops + L/R |
| Valid Palindrome | Both-ends compare | skip non-alphanumeric, compare chars |
| Reverse Vowels | Both-ends swap | skip non-vowels, swap |
| Squares Sorted Array | Both-ends fill end | compare abs values, fill from back |
| Remove Duplicates | Slow/fast | write only on new value |
| Rearrange 0s/1s | Slow/fast swap | swap 0s to front |
| Backspace Compare | Reverse traversal | skip on #, compare valid chars |
| Sort Colors | 3-pointer | 0→swap+low+mid++, 1→mid++, 2→swap+high-- |
| Merge Sorted Array | Two arrays end | compare from end, write to back |
| Is Subsequence | Two arrays | advance both on match, only t otherwise |
| Product < K | Sliding window | count += R-L+1 per position |
| Min Window Sort | Both-ends scan | find unsorted range via max/min sweep |
| Remove Palindromic Sub | Both-ends | palindrome check → 1 or 2 |
| Reverse Words | Split + reverse | split by spaces, reverse array |
| Trapping Rain Water | Both-ends max | advance shorter, accumulate above max |
| Container with Most Water | Both-ends area | move shorter side inward |
