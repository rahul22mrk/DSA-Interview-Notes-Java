# Heap / Priority Queue Pattern — Solved Problems (26 Problems)

> **Pattern family:** Heap / Priority Queue / Greedy
> **Notes & Templates:** [01_heap_notes.md](./01_heap_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Kth Element
- [P1 — Kth Largest Element in an Array](#problem-1--kth-largest-element-in-an-array)
- [P2 — Kth Smallest Element in a Sorted Matrix](#problem-2--kth-smallest-element-in-a-sorted-matrix)
- [P3 — Kth Largest Element in a Stream](#problem-3--kth-largest-element-in-a-stream)
- [P4 — Kth Weakest Row in a Matrix](#problem-4--kth-weakest-row-in-a-matrix)

### Category 2 — Top K
- [P5 — Top K Frequent Elements](#problem-5--top-k-frequent-elements)
- [P6 — Top K Frequent Words](#problem-6--top-k-frequent-words)
- [P7 — Sort Characters By Frequency](#problem-7--sort-characters-by-frequency)
- [P8 — K Closest Points to Origin](#problem-8--k-closest-points-to-origin)
- [P9 — Find K Closest Elements](#problem-9--find-k-closest-elements)

### Category 3 — Merge K Lists / Arrays
- [P10 — Merge K Sorted Lists](#problem-10--merge-k-sorted-lists)
- [P11 — Merge K Sorted Arrays](#problem-11--merge-k-sorted-arrays)
- [P12 — K Pairs with Smallest Sums](#problem-12--k-pairs-with-smallest-sums)
- [P13 — Smallest Range Covering Elements from K Lists](#problem-13--smallest-range-covering-elements-from-k-lists)

### Category 4 — Two Heaps (Median)
- [P14 — Find Median from Data Stream](#problem-14--find-median-from-data-stream)
- [P15 — Sliding Window Median](#problem-15--sliding-window-median)

### Category 5 — Greedy + Heap
- [P16 — Task Scheduler](#problem-16--task-scheduler)
- [P17 — Reorganize String](#problem-17--reorganize-string)
- [P18 — Last Stone Weight](#problem-18--last-stone-weight)
- [P19 — IPO](#problem-19--ipo)
- [P20 — Course Schedule III](#problem-20--course-schedule-iii)
- [P21 — Minimum Number of Refueling Stops](#problem-21--minimum-number-of-refueling-stops)

### Category 6 — Design Problems
- [P22 — Design Twitter](#problem-22--design-twitter)
- [P23 — Design a Food Rating System](#problem-23--design-a-food-rating-system)
- [P24 — Distant Barcodes / Rearrange String](#problem-24--distant-barcodes--rearrange-string)

### Bonus / FAANG
- [P25 — Sort Array by Frequency](#problem-25--sort-array-by-frequency)
- [P26 — Smallest Range Covering Elements from K Lists (Hard)](#problem-26--smallest-range-covering-elements-from-k-lists-hard)

---

## Category 1 — Kth Element

---

### Problem 1 — Kth Largest Element in an Array
**LeetCode #215 | Difficulty: Medium | Company: Amazon, Facebook, Google | Category: Kth Element**

> Find the kth largest element in an unsorted array.

#### Core insight

Min-heap of size k. When heap exceeds k, evict the smallest. The top is always the kth largest seen so far.

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Each number | always | `offer(num)` |
| After offer | `size > k` | `poll()` — evict smallest |
| Return | — | `peek()` = kth largest |

#### Java code

```java
public int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();

    for (int num : nums) {
        minHeap.offer(num);
        if (minHeap.size() > k) minHeap.poll();   // remove smallest
    }
    return minHeap.peek();   // top of min-heap = kth largest
}
```

#### Example

```
nums = [3,2,1,5,6,4], k = 2

After processing: heap = [5, 6] (min-heap of size 2)
peek() = 5 = 2nd largest ✓
```

---

### Problem 2 — Kth Smallest Element in a Sorted Matrix
**LeetCode #378 | Difficulty: Medium | Company: Amazon, Google | Category: Kth Element**

> n×n matrix where each row and column is sorted. Find the kth smallest element.

#### Core insight

Min-heap stores (value, row, col). Start by pushing first column's elements. After each pop, push next element from same row.

#### Java code

```java
public int kthSmallest(int[][] matrix, int k) {
    int n = matrix.length;
    PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> a[0] - b[0]);

    for (int r = 0; r < Math.min(n, k); r++)
        minHeap.offer(new int[]{matrix[r][0], r, 0});

    int result = 0;
    for (int i = 0; i < k; i++) {
        int[] curr = minHeap.poll();
        result = curr[0];
        int row = curr[1], col = curr[2];
        if (col + 1 < n)
            minHeap.offer(new int[]{matrix[row][col+1], row, col+1});
    }
    return result;
}
```

#### Example

```
matrix = [[1,5,9],[10,11,13],[12,13,15]], k = 8

Heap starts with first col: [(1,0,0),(10,1,0),(12,2,0)]
Pop 7 times (k=8, last pop is answer):
1→push(5,0,1), 5→push(9,0,2), 9→done col0, 10→push(11,1,1), 11→push(13,1,2),
12→push(13,2,1), 13 → result = 13 ✓
```

---

### Problem 3 — Kth Largest Element in a Stream
**LeetCode #703 | Difficulty: Easy | Company: Amazon | Category: Kth Element Design**

> Design a class that finds the kth largest element in a stream of numbers.

#### Java code

```java
class KthLargest {
    private final int k;
    private final PriorityQueue<Integer> minHeap;

    public KthLargest(int k, int[] nums) {
        this.k = k;
        this.minHeap = new PriorityQueue<>();
        for (int num : nums) add(num);
    }

    public int add(int val) {
        minHeap.offer(val);
        if (minHeap.size() > k) minHeap.poll();
        return minHeap.peek();
    }
}
```

#### Example

```
KthLargest(3, [4,5,8,2])
Heap after init: [4,5,8] (size 3)

add(3):  heap=[3,4,5]? No: offer 3→[2,3,4,5,8]→poll→[3,4,5,8] wait k=3: after offers=[2,3,4,5,8], poll to size 3=[5,8,?]...
Actually: init with [4,5,8,2]:
  offer 4 → [4], offer 5 → [4,5], offer 8 → [4,5,8], offer 2 → [2,4,5,8] size>3 → poll(2) → [4,5,8]
add(3): offer → [3,4,5,8] size>3 → poll(3) → [4,5,8] → peek=4 ✓
add(5): offer → [4,5,5,8] size>3 → poll(4) → [5,5,8] → peek=5 ✓
```

---

### Problem 4 — Kth Weakest Row in a Matrix
**LeetCode #1337 | Difficulty: Easy | Company: Amazon | Category: Kth Element**

> Matrix of 0s and 1s (1s before 0s in each row). Find indices of k weakest rows (fewest soldiers).

#### Java code

```java
public int[] kWeakestRows(int[][] mat, int k) {
    // Max-heap: keep k weakest (fewest soldiers = smallest count)
    PriorityQueue<int[]> maxHeap = new PriorityQueue<>(
        (a, b) -> a[0] != b[0] ? b[0] - a[0] : b[1] - a[1]  // by soldiers desc, then index desc
    );

    for (int i = 0; i < mat.length; i++) {
        int soldiers = countSoldiers(mat[i]);
        maxHeap.offer(new int[]{soldiers, i});
        if (maxHeap.size() > k) maxHeap.poll();
    }

    int[] res = new int[k];
    for (int i = k - 1; i >= 0; i--) res[i] = maxHeap.poll()[1];
    return res;
}

private int countSoldiers(int[] row) {
    int lo = 0, hi = row.length;
    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        if (row[mid] == 1) lo = mid + 1;
        else hi = mid;
    }
    return lo;   // binary search for last 1
}
```

---

## Category 2 — Top K

---

### Problem 5 — Top K Frequent Elements
**LeetCode #347 | Difficulty: Medium | Company: Amazon, Facebook, Google | Category: Top K**

> Return the k most frequent elements.

#### Java code

```java
public int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> freq = new HashMap<>();
    for (int n : nums) freq.merge(n, 1, Integer::sum);

    // Min-heap by frequency — keeps top k most frequent
    PriorityQueue<Integer> minHeap = new PriorityQueue<>(
        (a, b) -> freq.get(a) - freq.get(b)
    );
    for (int num : freq.keySet()) {
        minHeap.offer(num);
        if (minHeap.size() > k) minHeap.poll();   // evict least frequent
    }

    int[] res = new int[k];
    for (int i = k - 1; i >= 0; i--) res[i] = minHeap.poll();
    return res;
}
```

#### Example

```
nums = [1,1,1,2,2,3], k = 2
freq = {1:3, 2:2, 3:1}

heap after processing: [2, 1] (top 2 most frequent)
Output: [1, 2] ✓
```

---

### Problem 6 — Top K Frequent Words
**LeetCode #692 | Difficulty: Medium | Company: Amazon, Bloomberg | Category: Top K**

> Return the k most frequent words. Ties broken alphabetically.

#### Java code

```java
public List<String> topKFrequent(String[] words, int k) {
    Map<String, Integer> freq = new HashMap<>();
    for (String w : words) freq.merge(w, 1, Integer::sum);

    // Min-heap: evict least frequent (or alphabetically last for ties)
    PriorityQueue<String> minHeap = new PriorityQueue<>(
        (a, b) -> freq.get(a).equals(freq.get(b))
            ? b.compareTo(a)               // higher alphabetical → evict first (for ties)
            : freq.get(a) - freq.get(b)    // lower frequency → evict first
    );

    for (String word : freq.keySet()) {
        minHeap.offer(word);
        if (minHeap.size() > k) minHeap.poll();
    }

    List<String> res = new LinkedList<>();
    while (!minHeap.isEmpty()) res.add(0, minHeap.poll());   // reverse order
    return res;
}
```

#### Example

```
words = ["i","love","leetcode","i","love","coding"], k = 2
freq = {i:2, love:2, leetcode:1, coding:1}

Top 2: "i"(2) and "love"(2) → alphabetically "i" < "love"
Output: ["i", "love"] ✓
```

---

### Problem 7 — Sort Characters By Frequency
**LeetCode #451 | Difficulty: Medium | Company: Amazon | Category: Top K**

> Sort characters by frequency of occurrence (most frequent first).

#### Java code

```java
public String frequencySort(String s) {
    Map<Character, Integer> freq = new HashMap<>();
    for (char c : s.toCharArray()) freq.merge(c, 1, Integer::sum);

    PriorityQueue<Character> maxHeap = new PriorityQueue<>(
        (a, b) -> freq.get(b) - freq.get(a)   // max-heap by frequency
    );
    maxHeap.addAll(freq.keySet());

    StringBuilder sb = new StringBuilder();
    while (!maxHeap.isEmpty()) {
        char c = maxHeap.poll();
        for (int i = 0; i < freq.get(c); i++) sb.append(c);
    }
    return sb.toString();
}
```

#### Example

```
s = "tree"
freq = {t:1, r:1, e:2}
maxHeap polls: e(2) → "ee", t(1) → "t", r(1) → "r"
Output: "eert" ✓
```

---

### Problem 8 — K Closest Points to Origin
**LeetCode #973 | Difficulty: Medium | Company: Amazon, Facebook | Category: Top K**

> Find the k closest points to the origin (0,0).

#### Java code

```java
public int[][] kClosest(int[][] points, int k) {
    // Max-heap by distance — evict farthest, keep k closest
    PriorityQueue<int[]> maxHeap = new PriorityQueue<>(
        (a, b) -> Integer.compare(
            b[0]*b[0] + b[1]*b[1],
            a[0]*a[0] + a[1]*a[1]
        )
    );

    for (int[] point : points) {
        maxHeap.offer(point);
        if (maxHeap.size() > k) maxHeap.poll();   // evict farthest
    }

    return maxHeap.toArray(new int[k][]);
}
```

#### Example

```
points = [[1,3],[-2,2]], k = 1
dist([1,3]) = 10, dist([-2,2]) = 8
maxHeap keeps closest → [[-2,2]] ✓
```

---

### Problem 9 — Find K Closest Elements
**LeetCode #658 | Difficulty: Medium | Company: Google, Amazon | Category: Top K**

> Given sorted array `arr`, find k closest elements to x. Return them sorted.

#### Core insight

Binary search to find the optimal left boundary, then return `arr[left..left+k-1]`.

#### Java code

```java
public List<Integer> findClosestElements(int[] arr, int k, int x) {
    int lo = 0, hi = arr.length - k;

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        // Compare distance of left boundary vs right boundary of window
        if (x - arr[mid] > arr[mid + k] - x) lo = mid + 1;
        else hi = mid;
    }

    List<Integer> res = new ArrayList<>();
    for (int i = lo; i < lo + k; i++) res.add(arr[i]);
    return res;
}
```

#### Example

```
arr = [1,2,3,4,5], k = 4, x = 3
Binary search: window of size 4
mid=0: x-arr[0]=2 vs arr[4]-x=2 → equal → hi=0 → lo=0
Return arr[0..3] = [1,2,3,4] ✓
```

---

## Category 3 — Merge K Lists / Arrays

---

### Problem 10 — Merge K Sorted Lists
**LeetCode #23 | Difficulty: Hard | Company: Amazon, Google, Facebook | Category: Merge K**

> Merge k sorted linked lists and return one sorted linked list.

#### Java code

```java
public ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> minHeap = new PriorityQueue<>((a, b) -> a.val - b.val);

    for (ListNode node : lists)
        if (node != null) minHeap.offer(node);   // null check!

    ListNode dummy = new ListNode(0), curr = dummy;
    while (!minHeap.isEmpty()) {
        ListNode node = minHeap.poll();
        curr.next = node;
        curr = curr.next;
        if (node.next != null) minHeap.offer(node.next);
    }
    return dummy.next;
}
```

#### Example

```
lists = [[1,4,5],[1,3,4],[2,6]]

Heap starts: {1(L1), 1(L2), 2(L3)}
Poll 1(L1) → push 4(L1). Result: 1
Poll 1(L2) → push 3(L2). Result: 1→1
...continues until all merged

Output: 1→1→2→3→4→4→5→6 ✓
Time: O(n log k), Space: O(k)
```

---

### Problem 11 — Merge K Sorted Arrays
**Difficulty: Medium | Company: Amazon, Google | Category: Merge K**

> Merge k sorted arrays into one sorted array.

#### Java code

```java
public int[] mergeKSortedArrays(int[][] arrays) {
    // (value, arrayIndex, elementIndex)
    PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> a[0] - b[0]);

    int totalSize = 0;
    for (int i = 0; i < arrays.length; i++) {
        if (arrays[i].length > 0) {
            minHeap.offer(new int[]{arrays[i][0], i, 0});
            totalSize += arrays[i].length;
        }
    }

    int[] result = new int[totalSize];
    int idx = 0;
    while (!minHeap.isEmpty()) {
        int[] curr = minHeap.poll();
        result[idx++] = curr[0];
        int arrIdx = curr[1], elemIdx = curr[2];
        if (elemIdx + 1 < arrays[arrIdx].length)
            minHeap.offer(new int[]{arrays[arrIdx][elemIdx+1], arrIdx, elemIdx+1});
    }
    return result;
}
```

---

### Problem 12 — K Pairs with Smallest Sums
**LeetCode #373 | Difficulty: Medium | Company: Amazon, Google | Category: Merge K**

> Find k pairs (u, v) with smallest sums where u ∈ nums1 and v ∈ nums2.

#### Core insight

Start with (nums1[0], nums2[j]) for all j. After popping (i, j), push (i+1, j) — each pair's next candidate.

#### Java code

```java
public List<List<Integer>> kSmallestPairs(int[] nums1, int[] nums2, int k) {
    List<List<Integer>> res = new ArrayList<>();
    if (nums1.length == 0 || nums2.length == 0) return res;

    // (sum, i, j) — i from nums1, j from nums2
    PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> a[0] - b[0]);

    // Push first pair for each index in nums1
    for (int i = 0; i < Math.min(nums1.length, k); i++)
        minHeap.offer(new int[]{nums1[i] + nums2[0], i, 0});

    while (!minHeap.isEmpty() && res.size() < k) {
        int[] curr = minHeap.poll();
        int i = curr[1], j = curr[2];
        res.add(Arrays.asList(nums1[i], nums2[j]));
        if (j + 1 < nums2.length)
            minHeap.offer(new int[]{nums1[i] + nums2[j+1], i, j+1});
    }
    return res;
}
```

#### Example

```
nums1=[1,7,11], nums2=[2,4,6], k=3
Init heap: [(3,0,0),(9,1,0),(13,2,0)]
Poll (3,0,0) → [1,2], push (5,0,1)
Poll (5,0,1) → [1,4], push (7,0,2)
Poll (7,0,2) → [1,6]
Output: [[1,2],[1,4],[1,6]] ✓
```

---

### Problem 13 — Smallest Range Covering Elements from K Lists
**LeetCode #632 | Difficulty: Hard | Company: Google | Category: Merge K**

> Find the smallest range that includes at least one element from each of k sorted lists.

#### Core insight

Min-heap of (val, listIdx, elemIdx). Track current max. Range = [minHeap.peek(), currentMax]. Advance the min element, update range.

#### Java code

```java
public int[] smallestRange(List<List<Integer>> nums) {
    PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> a[0] - b[0]);
    int currentMax = Integer.MIN_VALUE;

    for (int i = 0; i < nums.size(); i++) {
        int val = nums.get(i).get(0);
        minHeap.offer(new int[]{val, i, 0});
        currentMax = Math.max(currentMax, val);
    }

    int[] range = {minHeap.peek()[0], currentMax};

    while (!minHeap.isEmpty()) {
        int[] curr = minHeap.poll();
        int val = curr[0], listIdx = curr[1], elemIdx = curr[2];

        if (elemIdx + 1 == nums.get(listIdx).size()) break;  // one list exhausted

        int nextVal = nums.get(listIdx).get(elemIdx + 1);
        currentMax = Math.max(currentMax, nextVal);
        minHeap.offer(new int[]{nextVal, listIdx, elemIdx + 1});

        if (currentMax - minHeap.peek()[0] < range[1] - range[0])
            range = new int[]{minHeap.peek()[0], currentMax};
    }
    return range;
}
```

---

## Category 4 — Two Heaps (Median)

---

### Problem 14 — Find Median from Data Stream
**LeetCode #295 | Difficulty: Hard | Company: Amazon, Google, Facebook | Category: Two Heaps**

> Design a structure supporting `addNum(int num)` and `findMedian()`.

#### Core insight

Two heaps: `maxHeap` stores lower half, `minHeap` stores upper half. Invariant: `maxHeap.peek() ≤ minHeap.peek()` and sizes differ by at most 1.

#### Java code

```java
class MedianFinder {
    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder()); // lower half
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();                            // upper half

    public void addNum(int num) {
        maxHeap.offer(num);                                           // step 1: add to lower
        if (!minHeap.isEmpty() && maxHeap.peek() > minHeap.peek())
            minHeap.offer(maxHeap.poll());                            // step 2: fix order

        if (maxHeap.size() > minHeap.size() + 1)
            minHeap.offer(maxHeap.poll());                            // step 3: rebalance
        else if (minHeap.size() > maxHeap.size())
            maxHeap.offer(minHeap.poll());
    }

    public double findMedian() {
        if (maxHeap.size() == minHeap.size())
            return (maxHeap.peek() + (double) minHeap.peek()) / 2;
        return maxHeap.peek();
    }
}
```

#### Example

```
addNum(1): maxHeap=[1], minHeap=[]
addNum(2): maxHeap=[1], minHeap=[2]
findMedian(): equal sizes → (1+2)/2 = 1.5 ✓
addNum(3): maxHeap=[2,1], minHeap=[3]
findMedian(): maxHeap larger → 2 ✓
```

---

### Problem 15 — Sliding Window Median
**LeetCode #480 | Difficulty: Hard | Company: Google | Category: Two Heaps**

> Return the median of each window of size k as it slides through the array.

#### Java code

```java
public double[] medianSlidingWindow(int[] nums, int k) {
    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    double[] result = new double[nums.length - k + 1];

    for (int i = 0; i < nums.length; i++) {
        // Add incoming element
        maxHeap.offer(nums[i]);
        minHeap.offer(maxHeap.poll());
        if (maxHeap.size() < minHeap.size()) maxHeap.offer(minHeap.poll());

        // Remove outgoing element (when window is full)
        if (i >= k) {
            int remove = nums[i - k];
            if (remove <= maxHeap.peek()) maxHeap.remove(remove);
            else minHeap.remove(remove);
            if (maxHeap.size() < minHeap.size()) maxHeap.offer(minHeap.poll());
            else if (maxHeap.size() > minHeap.size() + 1) minHeap.offer(maxHeap.poll());
        }

        if (i >= k - 1)
            result[i - k + 1] = k % 2 == 0
                ? ((double) maxHeap.peek() + minHeap.peek()) / 2.0
                : maxHeap.peek();
    }
    return result;
}
```

---

## Category 5 — Greedy + Heap

---

### Problem 16 — Task Scheduler
**LeetCode #621 | Difficulty: Medium | Company: Facebook, Amazon | Category: Greedy + Heap**

> Tasks with cooldown n. Find minimum time intervals to execute all tasks.

#### Java code

```java
public int leastInterval(char[] tasks, int n) {
    int[] freq = new int[26];
    for (char t : tasks) freq[t - 'A']++;

    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    for (int f : freq) if (f > 0) maxHeap.offer(f);

    int time = 0;
    while (!maxHeap.isEmpty()) {
        List<Integer> temp = new ArrayList<>();
        int cycle = n + 1;   // one cooldown window

        while (cycle > 0 && !maxHeap.isEmpty()) {
            temp.add(maxHeap.poll() - 1);
            cycle--;
        }
        for (int t : temp) if (t > 0) maxHeap.offer(t);
        time += maxHeap.isEmpty() ? (n + 1 - cycle) : (n + 1);
    }
    return time;
}
```

#### Example

```
tasks = ['A','A','A','B','B','B'], n = 2
freq: A=3, B=3. maxHeap = [3,3]

Cycle 1: A(→2),B(→2). idle 1. time=3
Cycle 2: A(→1),B(→1). idle 1. time=6
Cycle 3: A(→0),B(→0). time=8
Output: 8 (A B _ A B _ A B) ✓
```

---

### Problem 17 — Reorganize String
**LeetCode #767 | Difficulty: Medium | Company: Google, Amazon | Category: Greedy + Heap**

> Rearrange string so no two adjacent characters are the same. Return "" if impossible.

#### Java code

```java
public String reorganizeString(String s) {
    int[] freq = new int[26];
    for (char c : s.toCharArray()) freq[c - 'a']++;

    PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a, b) -> b[1] - a[1]);
    for (int i = 0; i < 26; i++)
        if (freq[i] > 0) maxHeap.offer(new int[]{i, freq[i]});

    StringBuilder sb = new StringBuilder();
    while (maxHeap.size() >= 2) {
        int[] first  = maxHeap.poll();
        int[] second = maxHeap.poll();
        sb.append((char)('a' + first[0]));
        sb.append((char)('a' + second[0]));
        if (--first[1]  > 0) maxHeap.offer(first);
        if (--second[1] > 0) maxHeap.offer(second);
    }
    if (!maxHeap.isEmpty()) {
        int[] last = maxHeap.poll();
        if (last[1] > 1) return "";   // more than 1 remaining → impossible
        sb.append((char)('a' + last[0]));
    }
    return sb.toString();
}
```

#### Example

```
s = "aab"
freq: a=2, b=1. maxHeap = [(a,2),(b,1)]

Pop (a,2),(b,1) → "ab". Push (a,1). heap=[(a,1)]
Pop last: (a,1) → "aba"
Output: "aba" ✓
```

---

### Problem 18 — Last Stone Weight
**LeetCode #1046 | Difficulty: Easy | Company: Amazon | Category: Greedy + Heap**

> Repeatedly smash the two heaviest stones. Return weight of last stone (or 0).

#### Java code

```java
public int lastStoneWeight(int[] stones) {
    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    for (int s : stones) maxHeap.offer(s);

    while (maxHeap.size() > 1) {
        int y = maxHeap.poll();   // heaviest
        int x = maxHeap.poll();   // second heaviest
        if (y != x) maxHeap.offer(y - x);
    }
    return maxHeap.isEmpty() ? 0 : maxHeap.peek();
}
```

#### Example

```
stones = [2,7,4,1,8,1]
maxHeap = [8,7,4,2,1,1]
8 vs 7 → push 1. heap=[4,2,1,1,1]
4 vs 2 → push 2. heap=[2,1,1,1]
2 vs 1 → push 1. heap=[1,1,1]
1 vs 1 → tie, push nothing. heap=[1]
Output: 1 ✓
```

---

### Problem 19 — IPO
**LeetCode #502 | Difficulty: Hard | Company: Google | Category: Greedy + Two Heaps**

> Maximize capital by picking at most k projects. Each project has profit and required capital.

#### Core insight

Sort by capital. Use max-heap for profits of affordable projects. Greedily pick max profit each round.

#### Java code

```java
public int findMaximizedCapital(int k, int w, int[] profits, int[] capital) {
    int n = profits.length;
    int[][] projects = new int[n][2];
    for (int i = 0; i < n; i++) projects[i] = new int[]{capital[i], profits[i]};
    Arrays.sort(projects, (a, b) -> a[0] - b[0]);   // sort by capital needed

    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    int idx = 0;

    for (int i = 0; i < k; i++) {
        while (idx < n && projects[idx][0] <= w)
            maxHeap.offer(projects[idx++][1]);       // push all affordable profits
        if (maxHeap.isEmpty()) break;
        w += maxHeap.poll();                          // pick most profitable
    }
    return w;
}
```

#### Example

```
k=2, w=0, profits=[1,2,3], capital=[0,1,1]
Sorted by capital: [(0,1),(1,2),(1,3)]

Round 1: affordable=[1]. pick 1. w=1
Round 2: affordable=[2,3]. pick 3. w=4
Output: 4 ✓
```

---

### Problem 20 — Course Schedule III
**LeetCode #630 | Difficulty: Hard | Company: Google | Category: Greedy + Heap**

> Take as many courses as possible. Course i takes duration[i] days and must finish by lastDay[i].

#### Core insight

Sort by deadline. If adding a course exceeds its deadline, replace the longest previous course (if it's longer — saves time).

#### Java code

```java
public int scheduleCourse(int[][] courses) {
    Arrays.sort(courses, (a, b) -> a[1] - b[1]);   // sort by deadline
    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    int time = 0;

    for (int[] course : courses) {
        int duration = course[0], lastDay = course[1];
        if (time + duration <= lastDay) {
            maxHeap.offer(duration);
            time += duration;
        } else if (!maxHeap.isEmpty() && maxHeap.peek() > duration) {
            time -= maxHeap.poll();     // remove longest course taken so far
            maxHeap.offer(duration);
            time += duration;           // replace with shorter current course
        }
    }
    return maxHeap.size();
}
```

---

### Problem 21 — Minimum Number of Refueling Stops
**LeetCode #871 | Difficulty: Hard | Company: Google, Amazon | Category: Greedy + Heap**

> Car with initial fuel, target distance, stations with fuel. Minimum stops to reach target.

#### Core insight

Greedily use the largest fuel station only when you run out. Track all passed stations in a max-heap; pop the max when needed.

#### Java code

```java
public int minRefuelStops(int target, int startFuel, int[][] stations) {
    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    int fuel = startFuel, stops = 0, prev = 0;

    for (int[] station : stations) {
        int pos = station[0], amount = station[1];
        fuel -= (pos - prev);       // fuel used to reach this station
        prev = pos;

        while (fuel < 0 && !maxHeap.isEmpty()) {
            fuel += maxHeap.poll(); // retroactively refuel at best passed station
            stops++;
        }
        if (fuel < 0) return -1;   // can't reach this station

        maxHeap.offer(amount);      // add this station's fuel as option
    }

    fuel -= (target - prev);        // fuel to reach target from last station
    while (fuel < 0 && !maxHeap.isEmpty()) {
        fuel += maxHeap.poll();
        stops++;
    }
    return fuel >= 0 ? stops : -1;
}
```

---

## Category 6 — Design Problems

---

### Problem 22 — Design Twitter
**LeetCode #355 | Difficulty: Medium | Company: Amazon, Twitter | Category: Design**

> Design simplified Twitter: `postTweet`, `getNewsFeed` (top 10), `follow`, `unfollow`.

#### Java code

```java
class Twitter {
    private int timestamp = 0;
    private Map<Integer, List<int[]>> tweets = new HashMap<>();     // userId → [(time, tweetId)]
    private Map<Integer, Set<Integer>> follows = new HashMap<>();   // userId → followees

    public void postTweet(int userId, int tweetId) {
        tweets.computeIfAbsent(userId, k -> new ArrayList<>()).add(new int[]{timestamp++, tweetId});
    }

    public List<Integer> getNewsFeed(int userId) {
        // Max-heap by timestamp
        PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a, b) -> b[0] - a[0]);
        Set<Integer> followees = follows.getOrDefault(userId, new HashSet<>());
        followees.add(userId);   // include own tweets

        for (int fId : followees) {
            List<int[]> userTweets = tweets.getOrDefault(fId, new ArrayList<>());
            for (int[] tweet : userTweets) maxHeap.offer(tweet);
        }

        List<Integer> feed = new ArrayList<>();
        int count = 0;
        while (!maxHeap.isEmpty() && count++ < 10)
            feed.add(maxHeap.poll()[1]);
        return feed;
    }

    public void follow(int followerId, int followeeId) {
        follows.computeIfAbsent(followerId, k -> new HashSet<>()).add(followeeId);
    }

    public void unfollow(int followerId, int followeeId) {
        follows.getOrDefault(followerId, new HashSet<>()).remove(followeeId);
    }
}
```

---

### Problem 23 — Design a Food Rating System
**LeetCode #2353 | Difficulty: Medium | Company: Amazon | Category: Design**

> Design a system to rate foods by cuisine, supporting `changeRating` and `highestRated(cuisine)`.

#### Java code

```java
class FoodRatings {
    Map<String, Integer> foodRating = new HashMap<>();
    Map<String, String>  foodCuisine = new HashMap<>();
    // cuisine → max-heap of (rating, food) — sorted by rating desc, name asc
    Map<String, PriorityQueue<int[]>> cuisineHeap = new HashMap<>();
    Map<String, Integer> foodIdx = new HashMap<>();   // food → index for lookup

    public FoodRatings(String[] foods, String[] cuisines, int[] ratings) {
        for (int i = 0; i < foods.length; i++) {
            foodRating.put(foods[i], ratings[i]);
            foodCuisine.put(foods[i], cuisines[i]);
            cuisineHeap.computeIfAbsent(cuisines[i],
                k -> new PriorityQueue<>((a, b) -> a[0] != b[0] ? b[0]-a[0] : foods[a[1]].compareTo(foods[b[1]])))
                .offer(new int[]{ratings[i], i});
            foodIdx.put(foods[i], i);
        }
    }

    // Simpler approach: lazy deletion
    // Use TreeSet<int[]> per cuisine for O(log n) changeRating
}
```

#### Cleaner approach with TreeSet (recommended)

```java
class FoodRatings {
    Map<String, Integer> rating = new HashMap<>();
    Map<String, String>  cuisine = new HashMap<>();
    Map<String, TreeSet<String>> best = new HashMap<>();  // cuisine → foods sorted

    public FoodRatings(String[] foods, String[] cuisines, int[] ratings) {
        for (int i = 0; i < foods.length; i++) {
            rating.put(foods[i], ratings[i]);
            cuisine.put(foods[i], cuisines[i]);
            best.computeIfAbsent(cuisines[i],
                k -> new TreeSet<>((a, b) ->
                    rating.get(b) != rating.get(a) ? rating.get(b) - rating.get(a) : a.compareTo(b)))
                .add(foods[i]);
        }
    }

    public void changeRating(String food, int newRating) {
        String c = cuisine.get(food);
        best.get(c).remove(food);      // remove old entry
        rating.put(food, newRating);
        best.get(c).add(food);         // re-insert with new rating
    }

    public String highestRated(String c) {
        return best.get(c).first();
    }
}
```

---

### Problem 24 — Distant Barcodes / Rearrange String
**LeetCode #1054 | Difficulty: Medium | Company: Amazon | Category: Greedy + Heap**

> Rearrange barcodes so no two adjacent barcodes are the same.

> Same approach as Reorganize String (Problem 17) — max-heap by frequency, alternate two most frequent.

#### Java code

```java
public int[] rearrangeBarcodes(int[] barcodes) {
    Map<Integer, Integer> freq = new HashMap<>();
    for (int b : barcodes) freq.merge(b, 1, Integer::sum);

    PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a, b) -> b[1] - a[1]);
    for (Map.Entry<Integer,Integer> e : freq.entrySet())
        maxHeap.offer(new int[]{e.getKey(), e.getValue()});

    int[] res = new int[barcodes.length];
    int idx = 0;
    while (maxHeap.size() >= 2) {
        int[] a = maxHeap.poll(), b = maxHeap.poll();
        res[idx++] = a[0]; res[idx++] = b[0];
        if (--a[1] > 0) maxHeap.offer(a);
        if (--b[1] > 0) maxHeap.offer(b);
    }
    if (!maxHeap.isEmpty()) res[idx] = maxHeap.poll()[0];
    return res;
}
```

---

## Bonus / FAANG

---

### Problem 25 — Sort Array by Frequency
**LeetCode #1636 | Difficulty: Easy | Category: Top K**

> Sort by increasing frequency. For equal frequencies, sort by decreasing value.

#### Java code

```java
public int[] frequencySort(int[] nums) {
    Map<Integer, Integer> freq = new HashMap<>();
    for (int n : nums) freq.merge(n, 1, Integer::sum);

    Integer[] boxed = new Integer[nums.length];
    for (int i = 0; i < nums.length; i++) boxed[i] = nums[i];

    Arrays.sort(boxed, (a, b) ->
        freq.get(a).equals(freq.get(b)) ? b - a : freq.get(a) - freq.get(b)
    );

    for (int i = 0; i < nums.length; i++) nums[i] = boxed[i];
    return nums;
}
```

---

### Problem 26 — Smallest Range Covering Elements from K Lists (Hard)
**LeetCode #632 | Difficulty: Hard | Company: Google | Category: Merge K**

> Already covered in Problem 13 with full solution.

#### Key interview talking points

```
Why min-heap + track max works:
  At each step, the range is [heap_min, current_max].
  To shrink range, we must increase the minimum → advance the list
  that contributed the current minimum.
  When any list is exhausted, we can't include all K lists → stop.

Time: O(n log k) where n = total elements, k = number of lists
Space: O(k) for the heap
```

---

## Quick Pattern Reference

| Problem | Category | Heap type | Size | Key trick |
|---------|----------|-----------|------|-----------|
| Kth Largest Array | Kth | min-heap | k | peek = answer |
| Kth Smallest Matrix | Kth | min-heap | ≤k | row-pointer (val,r,c) |
| Kth Largest Stream | Kth Design | min-heap | k | peek on every add |
| Kth Weakest Row | Kth | max-heap | k | binary search soldiers |
| Top K Frequent | Top K | min-heap by freq | k | poll excess |
| Top K Words | Top K | min-heap | k | tie-break alphabetically |
| Sort by Frequency | Top K | sort | — | freq map + comparator |
| K Closest Points | Top K | max-heap by dist | k | keep closest k |
| Find K Closest | Top K | binary search | — | optimal window start |
| Merge K Lists | Merge K | min-heap | k | (val, listIdx) |
| Merge K Arrays | Merge K | min-heap | k | (val, arr, idx) |
| K Pairs Smallest | Merge K | min-heap | k | expand (i, j+1) |
| Smallest Range | Merge K | min-heap + max | k | advance min pointer |
| Find Median Stream | Two Heaps | max+min | n | balance sizes |
| Sliding Window Median | Two Heaps | max+min | k | lazy delete |
| Task Scheduler | Greedy | max-heap | 26 | cooldown cycle |
| Reorganize String | Greedy | max-heap | 26 | alternate top 2 |
| Last Stone Weight | Greedy | max-heap | n | smash top 2 |
| IPO | Greedy | max-heap | n | sort capital + pick max profit |
| Course Schedule III | Greedy | max-heap | n | sort deadline + replace longest |
| Min Refuel Stops | Greedy | max-heap | n | retroactive best station |
| Design Twitter | Design | max-heap | follows | top 10 by timestamp |
| Food Rating System | Design | TreeSet | per cuisine | sorted by rating+name |
| Distant Barcodes | Greedy | max-heap | 26 | same as reorganize |
| Sort Array by Freq | Top K | sort | — | freq asc, val desc on tie |
