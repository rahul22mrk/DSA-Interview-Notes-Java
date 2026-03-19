# Binary Search — Solved Problems (31 Problems)

> **Pattern family:** Divide and Conquer / Search
> **Notes & Templates:** [01_binary_search_notes.md](./01_binary_search_notes.md)
> **Language:** Java

---

## Table of Contents

### Basic Binary Search
- [P1 — Binary Search (Basic)](#problem-1--binary-search-basic)
- [P2 — Upper Bound / Ceiling](#problem-2--upper-bound--ceiling)
- [P3 — First and Last Position](#problem-3--first-and-last-position-of-element)
- [P4 — Count Number of Occurrences](#problem-4--count-number-of-occurrences)
- [P5 — Search in Infinite Sorted Array](#problem-5--search-in-infinite-sorted-array)

### Bitonic Array Search
- [P6 — Peak Index in Mountain Array](#problem-6--peak-index-in-mountain-array)
- [P7b — Search in Bitonic Array](#problem-7b--search-in-bitonic-array)
- [P7 — Find Peak Element](#problem-7--find-peak-in-mountain-range-find-peak-element)

### Range Search (Rotated / Special)
- [P8 — Find Minimum in Rotated Sorted Array](#problem-8--find-minimum-in-rotated-sorted-array)
- [P9 — Find Number of Rotations](#problem-9--find-number-of-rotations)
- [P10 — Search in Rotated Sorted Array](#problem-10--search-in-rotated-sorted-array)
- [P24 — Find Min in Rotated II (Duplicates)](#problem-24--find-minimum-in-rotated-sorted-array-ii-with-duplicates)
- [P25 — Search in Rotated II (Duplicates)](#problem-25--search-in-rotated-sorted-array-ii-with-duplicates)
- [P26 — Single Element in Sorted Array](#problem-26--single-element-in-a-sorted-array)

### Allocate Problems (Binary Search on Answer)
- [P11 — Koko Eating Bananas](#problem-11--koko-eating-bananas)
- [P12 — Min Days to Make Bouquets](#problem-12--minimum-days-to-make-m-bouquets)
- [P13 — Aggressive Cows](#problem-13--aggressive-cows)
- [P14 — H-Index II](#problem-14--h-index-ii)
- [P15 — Maximum Candies to K Children](#problem-15--maximum-candies-to-k-children)
- [P16 — Capacity to Ship Packages in D Days](#problem-16--capacity-to-ship-packages-in-d-days)
- [P17 — Book Allocation Problem](#problem-17--book-allocation-problem)
- [P18 — Split Array Largest Sum](#problem-18--split-array-largest-sum)
- [P29 — Minimum Speed to Arrive on Time](#problem-29--minimum-speed-to-arrive-on-time)
- [P30 — Minimize Max Gas Station Distance](#problem-30--minimize-maximum-distance-to-gas-station)

### Counting Occurrences / Kth Element
- [P19 — Search a 2D Matrix](#problem-19--search-a-2d-matrix)
- [P20 — Search a 2D Matrix II (Hard)](#problem-20--search-a-2d-matrix-ii-hard)
- [P21 — Kth Smallest in Sorted Matrix](#problem-21--kth-smallest-element-in-a-sorted-matrix)
- [P22 — Kth Smallest in Multiplication Table](#problem-22--kth-smallest-in-multiplication-table)
- [P23 — Median of Two Sorted Arrays](#problem-23--median-of-two-sorted-arrays)
- [P31 — Kth Missing Positive Number](#problem-31--kth-missing-positive-number)

### FAANG Extras
- [P27 — Time Based Key-Value Store](#problem-27--time-based-key-value-store)
- [P28 — Find K Closest Elements](#problem-28--find-k-closest-elements)

---

## 7. Solved problems

---

### Problem 1 — Binary Search (Basic)
**LeetCode #704 | Difficulty: Easy | Variant: Classic exact match**

#### Approach table

| Step | Condition | Update | Result |
|------|-----------|--------|--------|
| `arr[mid] == target` | found | — | return `mid` |
| `arr[mid] < target` | target in right | `lo = mid + 1` | continue |
| `arr[mid] > target` | target in left | `hi = mid - 1` | continue |
| `lo > hi` | not found | — | return `-1` |

#### Java code

```java
public int search(int[] nums, int target) {
    int lo = 0, hi = nums.length - 1;

    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;

        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) lo = mid + 1;
        else hi = mid - 1;
    }
    return -1;
}
```

#### Example

```
Input: nums = [-1,0,3,5,9,12], target = 9

lo=0, hi=5, mid=2 → nums[2]=3 < 9 → lo=3
lo=3, hi=5, mid=4 → nums[4]=9 == 9 → return 4 ✓
```

---

### Problem 2 — Upper Bound / Ceiling
**LeetCode #35 (Search Insert Position) | Difficulty: Easy | Variant: Left boundary**

> Find the first index where `arr[index] >= target`. This is the insertion position (ceiling).

#### Approach table

| Step | Condition | Update |
|------|-----------|--------|
| `arr[mid] >= target` | mid is a candidate | `hi = mid` |
| `arr[mid] < target` | need to go right | `lo = mid + 1` |
| `lo == hi` | converged | return `lo` |

#### Java code

```java
// Returns: first index where nums[index] >= target (insertion position)
public int searchInsert(int[] nums, int target) {
    int lo = 0, hi = nums.length;   // hi = n: target may go after all elements

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (nums[mid] >= target) hi = mid;
        else lo = mid + 1;
    }
    return lo==nums.length?-1:lo;   // lo == hi == insertion point
}
```

#### Example

```
Input: nums = [1,3,5,6], target = 5 → Output: 2  (nums[2]=5 >= 5)
Input: nums = [1,3,5,6], target = 2 → Output: 1  (nums[1]=3 >= 2, first such index)
Input: nums = [1,3,5,6], target = 7 → Output: 4  (goes after all elements)
```

---

### Problem 3 — First and Last Position of Element
**LeetCode #34 | Difficulty: Medium | Variant: Left + Right boundary**

#### Approach table

| Step | Find first | Find last |
|------|-----------|-----------|
| `nums[mid] == target` | `hi = mid` (keep looking left) | `lo = mid` (keep looking right) |
| `nums[mid] < target` | `lo = mid + 1` | `lo = mid + 1` |
| `nums[mid] > target` | `hi = mid - 1` | `hi = mid - 1` |

#### Java code

```java
public int[] searchRange(int[] nums, int target) {
    return new int[]{findFirst(nums, target), findLast(nums, target)};
}

private int findFirst(int[] nums, int target) {
    int lo = 0, hi = nums.length - 1, result = -1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if (nums[mid] == target) { result = mid; hi = mid - 1; }  // keep left
        else if (nums[mid] < target) lo = mid + 1;
        else hi = mid - 1;
    }
    return result;
}

private int findLast(int[] nums, int target) {
    int lo = 0, hi = nums.length - 1, result = -1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if (nums[mid] == target) { result = mid; lo = mid + 1; }  // keep right
        else if (nums[mid] < target) lo = mid + 1;
        else hi = mid - 1;
    }
    return result;
}
```

#### Example

```
Input: nums = [5,7,7,8,8,10], target = 8

findFirst: lo=0,hi=5→mid=2(7<8,lo=3)→mid=4(8==8,result=4,hi=3)→mid=3(8==8,result=3,hi=2) → 3
findLast:  lo=0,hi=5→mid=2(7<8,lo=3)→mid=4(8==8,result=4,lo=5)→mid=5(10>8,hi=4) → 4

Output: [3, 4] ✓
```

---

### Problem 4 — Count Number of Occurrences
**Difficulty: Easy | Variant: Right boundary − Left boundary + 1**

#### Java code

```java
public int countOccurrences(int[] nums, int target) {
    int first = findFirst(nums, target);
    if (first == -1) return 0;
    int last = findLast(nums, target);
    return last - first + 1;
}

// findFirst and findLast same as Problem 3
```

#### Example

```
Input: nums = [1,1,2,2,2,3,3], target = 2
first = 2, last = 4
count = 4 - 2 + 1 = 3 ✓
```

---

### Problem 5 — Search in Infinite Sorted Array
**Difficulty: Medium | Variant: Exponential search + Binary search**

> Array is infinite — you don't know `hi`. Double the window until target is in range, then binary search.

#### Java code

```java
public int searchInInfiniteArray(ArrayReader reader, int target) {
    // Step 1: find the range [lo, hi] containing target
    int lo = 0, hi = 1;
    while (reader.get(hi) < target) {
        lo = hi;
        hi *= 2;   // double the window
    }

    // Step 2: standard binary search in [lo, hi]
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        int val = reader.get(mid);

        if (val == target) return mid;
        else if (val < target) lo = mid + 1;
        else hi = mid - 1;
    }
    return -1;
}
```

#### Example

```
target = 10, array = [1,3,5,7,10,15,20,...]

Window: [0,1]→get(1)=3<10 → [1,2]→get(2)=5<10 → [2,4]→get(4)=10 ≥ 10 → stop
Binary search [2,4]: mid=3,get(3)=7<10,lo=4; mid=4,get(4)=10==10 → return 4 ✓
```

---

### Problem 6 — Peak Index in Mountain Array
**LeetCode #852 | Difficulty: Easy | Variant: Peak finding**

#### Approach table

| Condition | Meaning | Update |
|-----------|---------|--------|
| `arr[mid] < arr[mid+1]` | still going up → peak is right | `lo = mid + 1` |
| `arr[mid] > arr[mid+1]` | going down → peak is at mid or left | `hi = mid` |

#### Java code

```java
public int peakIndexInMountainArray(int[] arr) {
    int lo = 0, hi = arr.length - 1;

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (arr[mid] < arr[mid + 1]) lo = mid + 1;  // ascending → go right
        else hi = mid;                                // descending → peak ≤ mid
    }
    return lo;   // lo == hi == peak index
}
```

#### Example

```
Input: arr = [0,1,0]
lo=0,hi=2,mid=1: arr[1]=1 > arr[2]=0 → hi=1
lo=0,hi=1,mid=0: arr[0]=0 < arr[1]=1 → lo=1
lo==hi==1 → return 1 ✓
```

---

### Problem 7b — Search in Bitonic Array
**Difficulty: Medium | Variant: Bitonic Array Search (find peak → search both halves)**

> Given a bitonic array (increases then decreases), find if a target exists.

#### Java code

```java
public int searchBitonicArray(int[] arr, int target) {
    // Step 1: find the peak index
    int peak = findPeak(arr);

    // Step 2: binary search in ascending half [0..peak]
    int result = binarySearchAsc(arr, 0, peak, target);
    if (result != -1) return result;

    // Step 3: binary search in descending half [peak+1..n-1]
    return binarySearchDesc(arr, peak + 1, arr.length - 1, target);
}

private int findPeak(int[] arr) {
    int lo = 0, hi = arr.length - 1;
    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        if (arr[mid] < arr[mid + 1]) lo = mid + 1;
        else hi = mid;
    }
    return lo;
}

private int binarySearchAsc(int[] arr, int lo, int hi, int target) {
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) lo = mid + 1;
        else hi = mid - 1;
    }
    return -1;
}

private int binarySearchDesc(int[] arr, int lo, int hi, int target) {
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if (arr[mid] == target) return mid;
        else if (arr[mid] > target) lo = mid + 1;   // reversed comparison
        else hi = mid - 1;
    }
    return -1;
}
```

#### Example

```
Input: arr = [1,3,8,12,4,2], target = 4

findPeak: [1,3,8,12,4,2] → peak index = 3 (value 12)

binarySearchAsc([0..3], target=4):
  lo=0,hi=3,mid=1: 3<4 → lo=2
  lo=2,hi=3,mid=2: 8>4 → hi=1
  lo>hi → return -1

binarySearchDesc([4..5], target=4):
  lo=4,hi=5,mid=4: arr[4]=4==4 → return 4 ✓

Output: index 4 ✓
```

---

### Problem 7 — Find Peak in Mountain Range (Find Peak Element)
**LeetCode #162 | Difficulty: Medium | Variant: Peak in unsorted array with local peaks**

> Array may have multiple peaks. Find any one peak (where `arr[mid] > arr[mid-1]` and `arr[mid] > arr[mid+1]`).

#### Java code

```java
public int findPeakElement(int[] nums) {
    int lo = 0, hi = nums.length - 1;

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (nums[mid] < nums[mid + 1]) lo = mid + 1;  // slope goes up → peak right
        else hi = mid;                                  // slope goes down → peak ≤ mid
    }
    return lo;
}
```

#### Example

```
Input: nums = [1,2,1,3,5,6,4]
lo=0,hi=6,mid=3: nums[3]=3 < nums[4]=5 → lo=4
lo=4,hi=6,mid=5: nums[5]=6 > nums[6]=4 → hi=5
lo=4,hi=5,mid=4: nums[4]=5 < nums[5]=6 → lo=5
lo==hi==5 → return 5 ✓ (nums[5]=6 is a peak)
```

---

### Problem 8 — Find Minimum in Rotated Sorted Array
**LeetCode #153 | Difficulty: Medium | Variant: Rotated array minimum**

#### Approach table

| Condition | Meaning | Update |
|-----------|---------|--------|
| `nums[mid] > nums[hi]` | min is in right half | `lo = mid + 1` |
| `nums[mid] <= nums[hi]` | mid could be min, or min is left | `hi = mid` |

#### Java code

```java
public int findMin(int[] nums) {
    int lo = 0, hi = nums.length - 1;

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (nums[mid] > nums[hi]) lo = mid + 1;  // min in right half
        else hi = mid;                             // mid is candidate for min
    }
    return nums[lo];
}
```

#### Example

```
Input: nums = [3,4,5,1,2]
lo=0,hi=4,mid=2: nums[2]=5 > nums[4]=2 → lo=3
lo=3,hi=4,mid=3: nums[3]=1 <= nums[4]=2 → hi=3
lo==hi==3 → return nums[3]=1 ✓
```

---

### Problem 9 — Find Number of Rotations
**Difficulty: Easy | Variant: Index of minimum = number of rotations**

> The index of the minimum element in a rotated sorted array equals the number of rotations.

#### Java code

```java
public int countRotations(int[] nums) {
    int lo = 0, hi = nums.length - 1;

    // If not rotated
    if (nums[lo] <= nums[hi]) return 0;

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        if (nums[mid] > nums[hi]) lo = mid + 1;
        else hi = mid;
    }
    return lo;   // index of minimum = number of rotations
}
```

#### Example

```
Input: nums = [4,5,6,7,0,1,2]
Minimum is at index 4 → rotated 4 times ✓
```

---

### Problem 10 — Search in Rotated Sorted Array
**LeetCode #33 | Difficulty: Medium | Variant: Rotated array search**

#### Approach table

| Condition | Meaning | Update |
|-----------|---------|--------|
| `arr[lo] <= arr[mid]` | left half is sorted | check if target in `[arr[lo], arr[mid])` |
| else | right half is sorted | check if target in `(arr[mid], arr[hi]]` |

#### Java code

```java
public int search(int[] nums, int target) {
    int lo = 0, hi = nums.length - 1;

    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;

        if (nums[mid] == target) return mid;

        if (nums[lo] <= nums[mid]) {                              // left half sorted
            if (target >= nums[lo] && target < nums[mid]) hi = mid - 1;
            else lo = mid + 1;
        } else {                                                  // right half sorted
            if (target > nums[mid] && target <= nums[hi]) lo = mid + 1;
            else hi = mid - 1;
        }
    }
    return -1;
}
```

#### Example

```
Input: nums = [4,5,6,7,0,1,2], target = 0

lo=0,hi=6,mid=3: nums[3]=7≠0
  nums[0]=4 <= nums[3]=7 → left sorted
  target=0 not in [4,7) → lo=4
lo=4,hi=6,mid=5: nums[5]=1≠0
  nums[4]=0 <= nums[5]=1 → left sorted
  target=0 in [0,1) → hi=4
lo=4,hi=4,mid=4: nums[4]=0==0 → return 4 ✓
```

---

### Problem 11 — Koko Eating Bananas
**LeetCode #875 | Difficulty: Medium | Variant: Binary search on answer**

> Find minimum speed k (bananas/hour) such that Koko can eat all piles in `h` hours.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| lo | `1` (min possible speed) | at least 1 banana/hour |
| hi | `max(piles)` (max needed speed) | finish biggest pile in 1 hour |
| feasible(mid) | `hours needed ≤ h`? | sum of ceil(pile/mid) for all piles |
| if feasible | `hi = mid` | try slower |
| if not | `lo = mid + 1` | need faster |

#### Java code

```java
public int minEatingSpeed(int[] piles, int h) {
    int lo = 1, hi = 0;
    for (int p : piles) hi = Math.max(hi, p);   // hi = max pile

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (canFinish(piles, mid, h)) hi = mid;  // mid works → try smaller
        else lo = mid + 1;                        // too slow → increase speed
    }
    return lo;
}

private boolean canFinish(int[] piles, int speed, int h) {
    int hours = 0;
    for (int p : piles)
        hours += (p + speed - 1) / speed;   // ceil(p / speed)
    return hours <= h;
}
```

#### Example

```
piles = [3,6,7,11], h = 8
lo=1, hi=11

mid=6: hours = 1+1+2+2=6 ≤ 8 → hi=6
mid=3: hours = 1+2+3+4=10 > 8 → lo=4
mid=5: hours = 1+2+2+3=8 ≤ 8 → hi=5
mid=4: hours = 1+2+2+3=8 ≤ 8 → hi=4
lo==hi==4 → return 4 ✓
```

---

### Problem 12 — Minimum Days to Make M Bouquets
**LeetCode #1482 | Difficulty: Medium | Variant: Binary search on answer**

> Find minimum days to make `m` bouquets of `k` consecutive flowers.

#### Java code

```java
public int minDays(int[] bloomDay, int m, int k) {
    if ((long) m * k > bloomDay.length) return -1;   // impossible

    int lo = 1, hi = 0;
    for (int d : bloomDay) hi = Math.max(hi, d);

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (canMake(bloomDay, m, k, mid)) hi = mid;
        else lo = mid + 1;
    }
    return lo;
}

private boolean canMake(int[] bloomDay, int m, int k, int day) {
    int bouquets = 0, consecutive = 0;
    for (int d : bloomDay) {
        if (d <= day) {
            consecutive++;
            if (consecutive == k) { bouquets++; consecutive = 0; }
        } else {
            consecutive = 0;
        }
    }
    return bouquets >= m;
}
```

#### Example

```
bloomDay = [1,10,3,10,2], m = 3, k = 1
lo=1, hi=10

mid=5: day5 → flowers bloomed: [1,_,3,_,2] → 3 bouquets of 1 ≥ 3 → hi=5
mid=3: day3 → flowers bloomed: [1,_,3,_,2] → 3 bouquets ≥ 3 → hi=3
mid=2: day2 → flowers bloomed: [1,_,_,_,2] → 2 bouquets < 3 → lo=3
lo==hi==3 → return 3 ✓
```

---

### Problem 13 — Aggressive Cows
**Difficulty: Medium | Variant: Binary search on answer (maximize minimum distance)**

> Place `c` cows in stalls such that the minimum distance between any two cows is maximized.

#### Java code

```java
public int aggressiveCows(int[] stalls, int c) {
    Arrays.sort(stalls);
    int lo = 1, hi = stalls[stalls.length - 1] - stalls[0];

    while (lo < hi) {
        int mid = lo + (hi - lo + 1) / 2;   // upper mid to avoid infinite loop

        if (canPlace(stalls, c, mid)) lo = mid;   // works → try larger distance
        else hi = mid - 1;                         // too large → reduce
    }
    return lo;
}

private boolean canPlace(int[] stalls, int c, int minDist) {
    int count = 1, last = stalls[0];
    for (int i = 1; i < stalls.length; i++) {
        if (stalls[i] - last >= minDist) {
            count++;
            last = stalls[i];
            if (count >= c) return true;
        }
    }
    return false;
}
```

#### Example

```
stalls = [1,2,4,8,9], c = 3
sorted = [1,2,4,8,9], lo=1, hi=8

mid=4: canPlace(3,4)? [1,_,_,_,9] dist≥4: place at 1,_,_,8: 2 cows... 1,5→no,8: 1,8,? need 3rd, 8+4=12>9 → false → hi=3
mid=2: canPlace(3,2)? 1,_,4,_,_: 1→4(dist3<2? no,3≥2 yes)→8(dist4≥2 yes) = 3 cows → true → lo=2
mid=3: canPlace(3,3)? 1→4(3≥3 yes)→8(4≥3 yes) = 3 cows → true → lo=3
lo==hi==3 → return 3 ✓
```

---

### Problem 14 — H-Index II
**LeetCode #275 | Difficulty: Medium | Variant: Binary search on sorted citations**

> Find h such that researcher has at least h papers with ≥ h citations each.

#### Java code

```java
public int hIndex(int[] citations) {
    int n = citations.length;
    int lo = 0, hi = n;

    while (lo < hi) {
        int mid = lo + (hi - lo + 1) / 2;   // upper mid

        // citations[n-mid] is the mid-th largest citation
        if (citations[n - mid] >= mid) lo = mid;  // h=mid is achievable
        else hi = mid - 1;
    }
    return lo;
}
```

#### Example

```
citations = [0,1,3,5,6]  (sorted ascending), n=5

lo=0,hi=5,mid=3: citations[5-3]=citations[2]=3 >= 3 → lo=3
lo=3,hi=5,mid=4: citations[5-4]=citations[1]=1 < 4 → hi=3
lo==hi==3 → return 3 ✓ (3 papers with ≥3 citations each)
```

---

### Problem 15 — Maximum Candies to K Children
**LeetCode #2226 | Difficulty: Medium | Variant: Binary search on answer**

> Find maximum candies each child can get from piles, distributing equally.

#### Java code

```java
public int maximumCandies(int[] candies, long k) {
    int lo = 1, hi = 0;
    for (int c : candies) hi = Math.max(hi, c);

    while (lo < hi) {
        int mid = lo + (hi - lo + 1) / 2;   // upper mid (maximize)

        if (canDistribute(candies, k, mid)) lo = mid;  // works → try more
        else hi = mid - 1;                              // too many → reduce
    }
    return lo;
}

private boolean canDistribute(int[] candies, long k, int mid) {
    long children = 0;
    for (int c : candies) children += c / mid;
    return children >= k;
}
```

#### Example

```
candies = [5,8,6], k = 3

lo=1,hi=8,mid=4: 5/4+8/4+6/4=1+2+1=4 >= 3 → lo=4
lo=4,hi=8,mid=6: 5/6+8/6+6/6=0+1+1=2 < 3 → hi=5
lo=4,hi=5,mid=5: 5/5+8/5+6/5=1+1+1=3 >= 3 → lo=5
lo==hi==5 → return 5 ✓
```

---

### Problem 16 — Capacity to Ship Packages in D Days
**LeetCode #1011 | Difficulty: Medium | Variant: Binary search on answer**

#### Java code

```java
public int shipWithinDays(int[] weights, int days) {
    int lo = 0, hi = 0;
    for (int w : weights) {
        lo = Math.max(lo, w);    // min capacity = heaviest single package
        hi += w;                  // max capacity = ship all in one day
    }

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (canShip(weights, days, mid)) hi = mid;  // works → try less
        else lo = mid + 1;
    }
    return lo;
}

private boolean canShip(int[] weights, int days, int cap) {
    int daysNeeded = 1, current = 0;
    for (int w : weights) {
        if (current + w > cap) { daysNeeded++; current = 0; }
        current += w;
    }
    return daysNeeded <= days;
}
```

#### Example

```
weights = [1,2,3,4,5,6,7,8,9,10], days = 5
lo=10 (max weight), hi=55 (total)

mid=32: canShip? days=2 ≤ 5 → hi=32
mid=21: canShip? days=3 ≤ 5 → hi=21
mid=15: canShip? days=5 ≤ 5 → hi=15
mid=12: canShip? days=5 ≤ 5... actually 6 > 5 → lo=13
...
lo==hi==15 → return 15 ✓
```

---

### Problem 17 — Book Allocation Problem
**Difficulty: Hard | Variant: Binary search on answer (minimize maximum)**

> Allocate books to `m` students such that the maximum pages assigned to any student is minimized.

#### Java code

```java
public int allocateBooks(int[] pages, int m) {
    if (pages.length < m) return -1;

    int lo = 0, hi = 0;
    for (int p : pages) {
        lo = Math.max(lo, p);   // at least max single book
        hi += p;                 // at most all books to one student
    }

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (canAllocate(pages, m, mid)) hi = mid;  // works → try less
        else lo = mid + 1;
    }
    return lo;
}

private boolean canAllocate(int[] pages, int m, int maxPages) {
    int students = 1, current = 0;
    for (int p : pages) {
        if (current + p > maxPages) { students++; current = 0; }
        current += p;
    }
    return students <= m;
}
```

#### Example

```
pages = [12,34,67,90], m = 2
lo=90, hi=203

mid=146: canAllocate(2,146)? [12,34,67]=113≤146, [90]: 2 students ≤ 2 → hi=146
mid=118: canAllocate(2,118)? [12,34,67]=113≤118, [90]: 2 ≤ 2 → hi=118
mid=104: [12,34,67]=113>104 → student2=[67,90]=157>104 → 3>2 → lo=105
...
lo==hi==113 → return 113 ✓
```

---

### Problem 18 — Split Array Largest Sum
**LeetCode #410 | Difficulty: Hard | Variant: Binary search on answer — same as Book Allocation**

> Split array into `k` subarrays to minimize the largest subarray sum. Identical logic to Book Allocation.

#### Java code

```java
public int splitArray(int[] nums, int k) {
    int lo = 0, hi = 0;
    for (int n : nums) {
        lo = Math.max(lo, n);
        hi += n;
    }

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (canSplit(nums, k, mid)) hi = mid;
        else lo = mid + 1;
    }
    return lo;
}

private boolean canSplit(int[] nums, int k, int maxSum) {
    int parts = 1, current = 0;
    for (int n : nums) {
        if (current + n > maxSum) { parts++; current = 0; }
        current += n;
    }
    return parts <= k;
}
```

#### Example

```
nums = [7,2,5,10,8], k = 2
lo=10, hi=32

mid=21: [7,2,5]=14, [10,8]=18 → 2 parts ≤ 2 → hi=21
mid=15: [7,2,5]=14, [10,8]=18>15 → parts=3>2 → lo=16
mid=18: [7,2,5,10]→14+10=24>18, [7,2,5]=14,[10,8]=18 → 2 parts → hi=18
...
lo==hi==18 → return 18 ✓
```

---

### Problem 19 — Search a 2D Matrix
**LeetCode #74 | Difficulty: Medium | Variant: 2D binary search (treat as 1D)**

> Matrix rows and columns are sorted. Each row starts after the last row ends.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Map `mid` to 2D | `row = mid / cols`, `col = mid % cols` | treat as 1D array |
| Standard binary search | on range `[0, m*n-1]` | |

#### Java code

```java
public boolean searchMatrix(int[][] matrix, int target) {
    int m = matrix.length, n = matrix[0].length;
    int lo = 0, hi = m * n - 1;

    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        int val = matrix[mid / n][mid % n];   // map 1D index to 2D

        if (val == target) return true;
        else if (val < target) lo = mid + 1;
        else hi = mid - 1;
    }
    return false;
}
```

#### Example

```
matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
m=3, n=4, lo=0, hi=11

mid=5: matrix[5/4][5%4]=matrix[1][1]=11 > 3 → hi=4
mid=2: matrix[0][2]=5 > 3 → hi=1
mid=0: matrix[0][0]=1 < 3 → lo=1
mid=1: matrix[0][1]=3 == 3 → return true ✓
```

---

### Problem 20 — Search a 2D Matrix II (Hard)
**LeetCode #240 | Difficulty: Hard | Variant: Staircase search (not binary search)**

> Each row and column is sorted independently. Cannot treat as 1D.
> Use the "start from top-right corner" technique.

#### Approach table

| Condition | Update |
|-----------|--------|
| `matrix[r][c] == target` | return `true` |
| `matrix[r][c] < target` | `r++` (eliminate this row) |
| `matrix[r][c] > target` | `c--` (eliminate this column) |

#### Java code

```java
public boolean searchMatrix(int[][] matrix, int target) {
    int r = 0, c = matrix[0].length - 1;   // start top-right

    while (r < matrix.length && c >= 0) {
        if (matrix[r][c] == target) return true;
        else if (matrix[r][c] < target) r++;   // too small → go down
        else c--;                               // too large → go left
    }
    return false;
}
```

#### Example

```
matrix = [[1,4,7],[2,5,8],[3,6,9]], target = 5

Start: r=0, c=2, val=7 > 5 → c=1
r=0, c=1, val=4 < 5 → r=1
r=1, c=1, val=5 == 5 → return true ✓

Time: O(m+n)  Space: O(1)
```

---

### Problem 21 — Kth Smallest Element in a Sorted Matrix
**LeetCode #378 | Difficulty: Medium | Variant: Binary search on value range**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| lo | `matrix[0][0]` (min) | |
| hi | `matrix[n-1][n-1]` (max) | |
| count(mid) | elements ≤ mid | row-by-row binary search |
| condition | `count ≥ k` | first value where count reaches k |

#### Java code

```java
public int kthSmallest(int[][] matrix, int k) {
    int n = matrix.length;
    int lo = matrix[0][0], hi = matrix[n-1][n-1];

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        int count = countLE(matrix, mid, n);

        if (count >= k) hi = mid;    // mid could be answer
        else lo = mid + 1;
    }
    return lo;
}

private int countLE(int[][] matrix, int mid, int n) {
    int count = 0, row = n - 1, col = 0;
    while (row >= 0 && col < n) {
        if (matrix[row][col] <= mid) { count += row + 1; col++; }
        else row--;
    }
    return count;
}
```

#### Example

```
matrix = [[1,5,9],[10,11,13],[12,13,15]], k = 8
lo=1, hi=15

mid=8: countLE=4 < 8 → lo=9
mid=12: countLE=8 >= 8 → hi=12
mid=10: countLE=6 < 8 → lo=11
mid=11: countLE=7 < 8 → lo=12
lo==hi==12 → return 12 ✓
```

---

### Problem 22 — Kth Smallest in Multiplication Table
**LeetCode #668 | Difficulty: Hard | Variant: Binary search on value + counting**

> In m×n multiplication table, find kth smallest element.

#### Java code

```java
public int findKthNumber(int m, int n, int k) {
    int lo = 1, hi = m * n;

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        int count = countLE(mid, m, n);

        if (count >= k) hi = mid;
        else lo = mid + 1;
    }
    return lo;
}

private int countLE(int mid, int m, int n) {
    int count = 0;
    for (int i = 1; i <= m; i++)
        count += Math.min(mid / i, n);   // how many multiples of i are ≤ mid
    return count;
}
```

#### Example

```
m=3, n=3, k=5 (table: 1,2,3,2,4,6,3,6,9 sorted: 1,2,2,3,3,4,6,6,9)
lo=1, hi=9

mid=5: countLE? row1: min(5,3)=3, row2: min(2,3)=2, row3: min(1,3)=1 → 6 ≥ 5 → hi=5
mid=3: countLE? row1:3, row2:1, row3:1 → 5 ≥ 5 → hi=3
mid=2: countLE? row1:2, row2:1, row3:0 → 3 < 5 → lo=3
lo==hi==3 → return 3 ✓
```

---

### Problem 23 — Median of Two Sorted Arrays
**LeetCode #4 | Difficulty: Hard | Variant: Binary search on partition**

#### Core idea

Binary search on how many elements to take from `nums1` in the left half. The partition is correct when `max(left side) ≤ min(right side)`.

#### Java code

```java
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    // Ensure nums1 is the shorter array
    if (nums1.length > nums2.length) return findMedianSortedArrays(nums2, nums1);

    int m = nums1.length, n = nums2.length;
    int lo = 0, hi = m;
    int half = (m + n + 1) / 2;

    while (lo <= hi) {
        int i = lo + (hi - lo) / 2;   // partition nums1 at i
        int j = half - i;              // partition nums2 at j

        int maxLeft1  = (i == 0) ? Integer.MIN_VALUE : nums1[i - 1];
        int minRight1 = (i == m) ? Integer.MAX_VALUE : nums1[i];
        int maxLeft2  = (j == 0) ? Integer.MIN_VALUE : nums2[j - 1];
        int minRight2 = (j == n) ? Integer.MAX_VALUE : nums2[j];

        if (maxLeft1 <= minRight2 && maxLeft2 <= minRight1) {
            // Correct partition
            if ((m + n) % 2 == 1) return Math.max(maxLeft1, maxLeft2);
            return (Math.max(maxLeft1, maxLeft2) + Math.min(minRight1, minRight2)) / 2.0;
        } else if (maxLeft1 > minRight2) {
            hi = i - 1;   // too many from nums1
        } else {
            lo = i + 1;   // too few from nums1
        }
    }
    return 0.0;
}
```

#### Example

```
nums1 = [1,3], nums2 = [2]
m=2, n=1, half=2

i=1, j=1: maxLeft1=1, minRight1=3, maxLeft2=2, minRight2=MAX
  1 ≤ MAX and 2 ≤ 3 → correct partition
  (m+n)%2=1 → return max(1,2)=2.0 ✓

nums1 = [1,2], nums2 = [3,4]
m=2, n=2, half=2, i=1, j=1:
  maxLeft1=1, minRight1=2, maxLeft2=3, minRight2=4
  1 ≤ 4 ✓, but 3 > 2 ✗ → lo=2
i=2, j=0:
  maxLeft1=2, minRight1=MAX, maxLeft2=MIN, minRight2=3
  2 ≤ 3 ✓, MIN ≤ MAX ✓ → correct
  (2+2)%2=0 → return (max(2,MIN)+min(MAX,3))/2 = (2+3)/2=2.5 ✓
```

---

### Problem 24 — Find Minimum in Rotated Sorted Array II (with Duplicates)
**LeetCode #154 | Difficulty: Hard | FAANG Frequency: Google, Microsoft | Variant: Rotated array with duplicates**

> Same as #153 but array can have duplicates. Duplicates break the standard comparison — need an extra shrink step.

#### Approach table

| Condition | Action | Why |
|-----------|--------|-----|
| `nums[mid] > nums[hi]` | `lo = mid + 1` | min in right half |
| `nums[mid] < nums[hi]` | `hi = mid` | mid could be min |
| `nums[mid] == nums[hi]` | `hi--` | can't determine which half — shrink hi safely |

#### Java code

```java
public int findMin(int[] nums) {
    int lo = 0, hi = nums.length - 1;

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (nums[mid] > nums[hi])       lo = mid + 1;  // min in right half
        else if (nums[mid] < nums[hi])  hi = mid;       // mid is candidate
        else                            hi--;            // duplicate — shrink safely
    }
    return nums[lo];
}
```

#### Example

```
Input: nums = [2,2,2,0,1]

lo=0,hi=4,mid=2: nums[2]=2 == nums[4]=2 → hi=3
lo=0,hi=3,mid=1: nums[1]=2 == nums[3]=1? No, 2>1 → lo=2
lo=2,hi=3,mid=2: nums[2]=2 > nums[3]=1 → lo=3
lo==hi==3 → return nums[3]=0 ✓

Worst case: all duplicates → O(n). Average: O(log n).
```

---

### Problem 25 — Search in Rotated Sorted Array II (with Duplicates)
**LeetCode #81 | Difficulty: Medium | FAANG Frequency: Amazon, Microsoft | Variant: Rotated search with duplicates**

> Same as #33 but may contain duplicates. Duplicates create an ambiguous case — shrink from both ends.

#### Java code

```java
public boolean search(int[] nums, int target) {
    int lo = 0, hi = nums.length - 1;

    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;

        if (nums[mid] == target) return true;

        // Ambiguous case — can't determine sorted half
        if (nums[lo] == nums[mid] && nums[mid] == nums[hi]) {
            lo++; hi--;                              // shrink both ends
        } else if (nums[lo] <= nums[mid]) {          // left half sorted
            if (target >= nums[lo] && target < nums[mid]) hi = mid - 1;
            else lo = mid + 1;
        } else {                                     // right half sorted
            if (target > nums[mid] && target <= nums[hi]) lo = mid + 1;
            else hi = mid - 1;
        }
    }
    return false;
}
```

#### Example

```
Input: nums = [2,5,6,0,0,1,2], target = 0

lo=0,hi=6,mid=3: nums[3]=0 == 0 → return true ✓

Input: nums = [2,5,6,0,0,1,2], target = 3

lo=0,hi=6,mid=3: nums[3]=0 ≠ 3
  nums[0]=2 <= nums[3]=0? No → right half sorted [0,0,1,2]
  target=3 not in (0,2] → hi=2
...eventually → return false ✓
```

---

### Problem 26 — Single Element in a Sorted Array
**LeetCode #540 | Difficulty: Medium | FAANG Frequency: Google, Apple, Facebook | Variant: Parity-based binary search**

> Every element appears exactly twice except one. Find it in O(log n) time, O(1) space.

#### Core insight

In pairs: element at index `2k` has partner at `2k+1`.
If `nums[mid] == nums[mid^1]` → the single element is to the RIGHT.
If `nums[mid] != nums[mid^1]` → the single element is at mid or LEFT.

`mid^1` flips the last bit: if mid is even → mid^1 = mid+1; if mid is odd → mid^1 = mid-1.

#### Java code

```java
public int singleNonDuplicate(int[] nums) {
    int lo = 0, hi = nums.length - 1;

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (mid % 2 == 1) mid--;   // ensure mid is even

        if (nums[mid] == nums[mid + 1]) lo = mid + 2;  // pair intact → single is right
        else hi = mid;                                   // pair broken → single ≤ mid
    }
    return nums[lo];
}
```

#### Example

```
Input: nums = [1,1,2,3,3,4,4,8,8]

lo=0,hi=8,mid=4→even=4: nums[4]=3==nums[5]=4? No → hi=4
lo=0,hi=4,mid=2→even=2: nums[2]=2==nums[3]=3? No → hi=2
lo=0,hi=2,mid=1→even=0: nums[0]=1==nums[1]=1? Yes → lo=2
lo==hi==2 → return nums[2]=2 ✓
```

---

### Problem 27 — Time Based Key-Value Store
**LeetCode #981 | Difficulty: Medium | FAANG Frequency: Google, Uber, Amazon | Variant: Binary search on timestamp**

> Design a key-value store where each key can have multiple values with timestamps. `get(key, timestamp)` returns the value with the largest timestamp ≤ given timestamp.

#### Java code

```java
class TimeMap {
    private Map<String, List<int[]>> map;   // key → list of [timestamp, value]

    public TimeMap() {
        map = new HashMap<>();
    }

    public void set(String key, String value, int timestamp) {
        map.computeIfAbsent(key, k -> new ArrayList<>())
           .add(new int[]{timestamp, value.hashCode()});
        // Store as [timestamp, valueIndex] — simplified; real: store string
    }

    public String get(String key, int timestamp) {
        if (!map.containsKey(key)) return "";
        List<String[]> list = store.get(key);

        int lo = 0, hi = list.size() - 1, result = -1;
        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (Integer.parseInt(list.get(mid)[0]) <= timestamp) {
                result = mid;           // valid candidate — try to find later one
                lo = mid + 1;
            } else {
                hi = mid - 1;
            }
        }
        return result == -1 ? "" : list.get(result)[1];
    }
}

// Clean implementation:
class TimeMap {
    Map<String, List<String[]>> store = new HashMap<>();

    public void set(String key, String value, int timestamp) {
        store.computeIfAbsent(key, k -> new ArrayList<>())
             .add(new String[]{String.valueOf(timestamp), value});
    }

    public String get(String key, int timestamp) {
        if (!store.containsKey(key)) return "";
        List<String[]> list = store.get(key);

        int lo = 0, hi = list.size() - 1, result = -1;
        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (Integer.parseInt(list.get(mid)[0]) <= timestamp) {
                result = mid;
                lo = mid + 1;
            } else {
                hi = mid - 1;
            }
        }
        return result == -1 ? "" : list.get(result)[1];
    }
}
```

#### Example

```
set("foo", "bar", 1)  → store: {foo: [[1,"bar"]]}
set("foo", "bar2", 4) → store: {foo: [[1,"bar"],[4,"bar2"]]}

get("foo", 4)  → largest timestamp ≤ 4 → index 1 → "bar2" ✓
get("foo", 3)  → largest timestamp ≤ 3 → index 0 → "bar"  ✓
get("foo", 0)  → no timestamp ≤ 0 → "" ✓
```

---

### Problem 28 — Find K Closest Elements
**LeetCode #658 | Difficulty: Medium | FAANG Frequency: Google, Facebook, Amazon | Variant: Binary search on window start**

> Given sorted array, find `k` closest elements to `x`. Return them sorted.

#### Core insight

Binary search for the LEFT boundary of the k-element window. Compare which side to exclude: `x - arr[mid]` vs `arr[mid+k] - x`.

#### Java code

```java
public List<Integer> findClosestElements(int[] arr, int k, int x) {
    int lo = 0, hi = arr.length - k;   // hi = last valid window start

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        // Compare distance of left edge (arr[mid]) vs right edge (arr[mid+k]) from x
        if (x - arr[mid] > arr[mid + k] - x) lo = mid + 1;  // right side closer
        else hi = mid;                                         // left side closer or equal
    }

    List<Integer> result = new ArrayList<>();
    for (int i = lo; i < lo + k; i++) result.add(arr[i]);
    return result;
}
```

#### Example

```
Input: arr = [1,2,3,4,5], k = 4, x = 3

lo=0, hi=1
mid=0: x-arr[0] = 3-1=2,  arr[0+4]-x = 5-3=2 → equal → hi=0
lo==hi==0 → window [0..3] → [1,2,3,4] ✓

Input: arr = [1,2,3,4,5], k=4, x=-1
mid=0: x-arr[0]=-1-1=-2<0 → |dist|=2, arr[4]-x=5-(-1)=6 → left closer → hi=0
→ [1,2,3,4] ✓
```

---

### Problem 29 — Minimum Speed to Arrive on Time
**LeetCode #1870 | Difficulty: Medium | FAANG Frequency: Google, Amazon | Variant: Binary search on answer**

> Find minimum integer speed such that all trains are caught within `hour` time (last train time can be decimal, others must be integers).

#### Java code

```java
public int minSpeedOnTime(int[] dist, double hour) {
    if (hour <= dist.length - 1) return -1;   // impossible — all except last must be integers

    int lo = 1, hi = (int) 1e7;   // speed range: 1 to 10^7

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (canArrive(dist, mid, hour)) hi = mid;
        else lo = mid + 1;
    }
    return lo;
}

private boolean canArrive(int[] dist, int speed, double hour) {
    double time = 0;
    for (int i = 0; i < dist.length - 1; i++)
        time += Math.ceil((double) dist[i] / speed);   // must wait for next integer hour
    time += (double) dist[dist.length - 1] / speed;    // last leg — exact decimal OK
    return time <= hour;
}
```

#### Example

```
dist = [1,3,2], hour = 6

lo=1,hi=10^7
mid=5000000: canArrive? ceil(1/5M)+ceil(3/5M)+2/5M ≈ 0 ≤ 6 → hi=5M
...
mid=1: ceil(1/1)+ceil(3/1)+2/1=1+3+2=6 ≤ 6 → hi=1
lo==hi==1 → return 1 ✓
```

---

### Problem 30 — Minimize Maximum Distance to Gas Station
**LeetCode #774 | Difficulty: Hard | FAANG Frequency: Google | Variant: Binary search on answer (decimal)**

> Add `k` gas stations to minimize the maximum distance between any two consecutive stations.

#### Java code

```java
public double minmaxGasDist(int[] stations, int k) {
    double lo = 0, hi = stations[stations.length - 1] - stations[0];

    while (hi - lo > 1e-6) {   // precision threshold
        double mid = (lo + hi) / 2.0;

        if (canAchieve(stations, k, mid)) hi = mid;
        else lo = mid;
    }
    return lo;
}

private boolean canAchieve(int[] stations, int k, double maxDist) {
    int count = 0;
    for (int i = 1; i < stations.length; i++) {
        double gap = stations[i] - stations[i - 1];
        count += (int) (gap / maxDist);   // how many stations needed in this gap
    }
    return count <= k;
}
```

#### Example

```
stations = [1,2,3,4,5,6,7,8,9,10], k = 9

Answer = 0.5 — add station between every pair
Binary search converges to 0.5 within 1e-6 precision ✓
```

---

### Problem 31 — Kth Missing Positive Number
**LeetCode #1539 | Difficulty: Easy | FAANG Frequency: Google, Facebook | Variant: Binary search on missing count**

> Given sorted positive array with no duplicates, find the kth missing positive number.

#### Core insight

At index `i`, the count of missing numbers = `arr[i] - (i+1)`. Binary search for the first index where missing count ≥ k.

#### Java code

```java
public int findKthPositive(int[] arr, int k) {
    int lo = 0, hi = arr.length;

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        // Missing numbers before arr[mid] = arr[mid] - (mid + 1)
        if (arr[mid] - (mid + 1) >= k) hi = mid;
        else lo = mid + 1;
    }
    // lo = first index where missing count >= k
    // answer = lo + k  (lo elements in array + k missing numbers)
    return lo + k;
}
```

#### Example

```
Input: arr = [2,3,4,7,11], k = 5

Missing sequence: 1,5,6,8,9,10,...

lo=0,hi=5
mid=2: arr[2]-3=4-3=1 < 5 → lo=3
mid=4: arr[4]-5=11-5=6 >= 5 → hi=4
mid=3: arr[3]-4=7-4=3 < 5 → lo=4
lo==hi==4 → return 4+5=9 ✓  (missing: 1,5,6,8,9 → 5th is 9)
```

---

