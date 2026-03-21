# 📚 DSA Interview Notes — Java

> Pattern-wise DSA notes in Java | Interview-focused | Clean code templates | Time complexity analysis

---

## 🔗 DSA Resources I Follow

> Curated list of the best LeetCode discuss posts and cheatsheets — bookmark these.

| Resource | What it covers |
|----------|----------------|
| [DSA Patterns you need to know](https://leetcode.com/discuss/study-guide/651719/) | Master pattern list — start here |
| [Solved all Two Pointers problems in 100 days](https://leetcode.com/discuss/study-guide/1688903/) | Complete two pointers guide |
| [Dynamic Programming Patterns](https://leetcode.com/discuss/study-guide/458695/) | DP patterns Part I |
| [Dynamic Programming Patterns II](https://leetcode.com/discuss/study-guide/1437879/) | DP patterns Part II |
| [Maximum Sliding Window Cheatsheet Template](https://leetcode.com/discuss/study-guide/657507/) | Sliding window all variants |
| [10-line template for most Substring problems](https://leetcode.com/discuss/study-guide/14225/) | Substring / window template |
| [Powerful Ultimate Binary Search Template](https://leetcode.com/discuss/study-guide/786126/) | Binary search — one template solves all |
| [Graph For Beginners — Problems, Pattern, Solutions](https://leetcode.com/discuss/study-guide/655708/) | BFS, DFS, Union Find |
| [All Types of Bit Manipulation Patterns](https://leetcode.com/discuss/study-guide/3901862/) | Bits tricks and patterns |
| [Backtracking — Subsets, Permutations, Combination Sum](https://leetcode.com/discuss/study-guide/46981/) | General backtracking template in Java |
| [Tree Traversal — Iterative, Recursive, DFS, BFS](https://leetcode.com/discuss/study-guide/937307/) | In, Pre, Post, LevelOrder, Views |
| [Monotonic Stack — Comprehensive Guide](https://leetcode.com/discuss/study-guide/2347639/) | All monotonic stack patterns |
| [Collections of Important String Question Patterns](https://leetcode.com/discuss/study-guide/1333049/) | String pattern cheatsheet |
| [Must Do Questions for MAANG Companies](https://leetcode.com/discuss/study-guide/1998290/) | Interview-focused problem list |

---

## 📁 Repository Structure

```
DSA-Interview-Notes-Java/
│
├── 01_Two_Pointers_Patterns/
│   ├── 01_two_pointers_notes.md
│   ├── 02_two_pointers_problems.md
│   └── 03_two_pointers_extended.md
│
├── 02_Sliding_Window_Patterns/
│   ├── 01_sliding_window_pattern_notes.md
│   └── 02_sliding_window_pattern_problems.md
│
├── 03_Slow_And_Fast_Pointers_Pattern/
│   ├── 01_slow_fast_pointers_notes.md
│   └── 02_slow_fast_pointers_problems.md
│
├── 04_Kadane_Pattern/
│   ├── 01_kadane_pattern_notes.md
│   └── 02_kadane_pattern_problems.md
│
├── 05_Prefix_Sum_Pattern/
│   ├── 01_prefix_sum_notes.md
│   └── 02_prefix_sum_problems.md
│
├── 06_Merge_Interval_Pattern/
│   ├── 01_merge_interval_notes.md
│   └── 02_merge_interval_problems.md
│
├── 07_Stack_Pattern/
│   ├── 01_stack_notes.md
│   └── 02_stack_problems.md
│
├── 08_HashMap_Pattern/
│   ├── 01_hashmap_notes.md
│   └── 02_hashmap_problems.md
│
├── 09_In-Place_Reversal_LinkedList/
│   ├── 01_inplace_reversal_notes.md
│   └── 02_inplace_reversal_problems.md
│
├── 10_Binary_Search_Pattern/
│   ├── 01_binary_search_pattern_notes.md
│   └── 02_binary_search_pattern_problems.md
│
├── 11_Cyclic_Sort_Pattern/
│   └── 🔜 coming soon
│
├── 12_Heap_Pattern/
│   └── 🔜 coming soon
│
├── 13_Recursion_And_Backtracking/
│   └── 🔜 coming soon
│
├── 14_Trees_Pattern/
│   └── 🔜 coming soon
│
├── 15_Graph_Pattern/
│   └── 🔜 coming soon
│
├── 16_Dynamic_Programming_Pattern/
│   └── 🔜 coming soon
│
├── 17_Trie_Pattern/
│   └── 🔜 coming soon
│
├── 18_Bit_Manipulation_Pattern/
│   └── 🔜 coming soon
│
└── README.md
```

---

## 🧩 Patterns Covered

### ✅ Two Pointers
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_two_pointers_notes.md](./01_Two_Pointers_Patterns/01_two_pointers_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_two_pointers_problems.md](./01_Two_Pointers_Patterns/02_two_pointers_problems.md) | Both-ends — Sum (2Sum, 3Sum, 4Sum) | Pair with Target, 3Sum, 3Sum Closest, Triplets Smaller Sum, 4Sum | Easy → Medium |
| [02_two_pointers_problems.md](./01_Two_Pointers_Patterns/02_two_pointers_problems.md) | Both-ends — Reverse / Palindrome | Valid Palindrome, Reverse Vowels, Squares of Sorted Array | Easy |
| [02_two_pointers_problems.md](./01_Two_Pointers_Patterns/02_two_pointers_problems.md) | Same Direction — In-place Modify | Remove Duplicates, Rearrange 0s & 1s, Backspace Compare | Easy → Medium |
| [02_two_pointers_problems.md](./01_Two_Pointers_Patterns/02_two_pointers_problems.md) | Dutch National Flag (3-pointer) | Sort Colors | Medium |
| [02_two_pointers_problems.md](./01_Two_Pointers_Patterns/02_two_pointers_problems.md) | Two Arrays | Merge Sorted Array, Is Subsequence | Easy |
| [02_two_pointers_problems.md](./01_Two_Pointers_Patterns/02_two_pointers_problems.md) | Trapping Water / FAANG | Trapping Rain Water, Container with Most Water, Min Window Sort | Medium → Hard |
| [03_two_pointers_extended.md](./01_Two_Pointers_Patterns/03_two_pointers_extended.md) | Extended Classification + Pseudocode | 60+ problems grouped by sub-pattern with approach skeleton | Easy → Hard |

---

### ✅ Prefix Sum
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_prefix_sum_notes.md](./05_Prefix_Sum_Pattern/01_prefix_sum_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_prefix_sum_problems.md](./05_Prefix_Sum_Pattern/02_prefix_sum_problems.md) | Basic Prefix Array | Range Sum Query, Find Pivot Index | Easy |
| [02_prefix_sum_problems.md](./05_Prefix_Sum_Pattern/02_prefix_sum_problems.md) | HashMap — Count / Existence | Subarray Sum Equals K, Contiguous Array, Longest Subarray Sum K | Medium |
| [02_prefix_sum_problems.md](./05_Prefix_Sum_Pattern/02_prefix_sum_problems.md) | Modulo HashMap | Subarray Sums Divisible by K, Continuous Subarray Sum | Medium |
| [02_prefix_sum_problems.md](./05_Prefix_Sum_Pattern/02_prefix_sum_problems.md) | 2D Prefix Sum | Range Sum Query 2D, Max Sum Rectangle ≤ K | Medium → Hard |
| [02_prefix_sum_problems.md](./05_Prefix_Sum_Pattern/02_prefix_sum_problems.md) | Hard (Deque / Merge Sort) | Shortest Subarray Sum ≥ K, Count of Range Sum | Hard |
| [02_prefix_sum_problems.md](./05_Prefix_Sum_Pattern/02_prefix_sum_problems.md) | Bonus / FAANG | Maximum Product Subarray | Medium |

---

### ✅ Sliding Window
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_sliding_window_pattern_notes.md](./02_Sliding_Window_Patterns/01_sliding_window_pattern_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_sliding_window_pattern_problems.md](./02_Sliding_Window_Patterns/02_sliding_window_pattern_problems.md) | Fixed Window | Max Sum K, Max Average, Permutation in String, Find All Anagrams | Easy → Medium |
| [02_sliding_window_pattern_problems.md](./02_Sliding_Window_Patterns/02_sliding_window_pattern_problems.md) | Variable Window — Maximize | No-Repeat, K Distinct, Fruits/Baskets, Longest Replacement, Max Ones III, Delete One, Budget Substring | Medium → Hard |
| [02_sliding_window_pattern_problems.md](./02_Sliding_Window_Patterns/02_sliding_window_pattern_problems.md) | Variable Window — Minimize | Min Size Subarray Sum, Min Window Substring, Product Less Than K | Medium → Hard |
| [02_sliding_window_pattern_problems.md](./02_Sliding_Window_Patterns/02_sliding_window_pattern_problems.md) | At-Most to Exact (Count) | K Different Integers, Binary Subarrays Sum, Nice Subarrays | Medium → Hard |
| [02_sliding_window_pattern_problems.md](./02_Sliding_Window_Patterns/02_sliding_window_pattern_problems.md) | FAANG Hard | Words Concatenation, Max Freq Element, Exam Confusion, Min Ops Continuous | Medium → Hard |

---

### ✅ Merge Intervals
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_merge_interval_notes.md](./06_Merge_Interval_Pattern/01_merge_interval_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_merge_interval_problems.md](./06_Merge_Interval_Pattern/02_merge_interval_problems.md) | Core Merge / Insert | Merge Intervals, Insert Interval | Medium |
| [02_merge_interval_problems.md](./06_Merge_Interval_Pattern/02_merge_interval_problems.md) | Intersection / Overlap Detection | Interval List Intersections, Overlapping Intervals Check | Medium |
| [02_merge_interval_problems.md](./06_Merge_Interval_Pattern/02_merge_interval_problems.md) | Resource Scheduling (Heap) | Min Meeting Rooms, Max CPU Load, Task Scheduler | Medium → Hard |
| [02_merge_interval_problems.md](./06_Merge_Interval_Pattern/02_merge_interval_problems.md) | Greedy (Sort by End) | Non-overlapping Intervals, Min Arrows, Meeting Scheduler | Medium |
| [02_merge_interval_problems.md](./06_Merge_Interval_Pattern/02_merge_interval_problems.md) | Hard / FAANG | Employee Free Time, Remove Covered Intervals, Data Stream Intervals | Hard |

---

### ✅ Kadane's Algorithm
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_kadane_pattern_notes.md](./04_Kadane_Pattern/01_kadane_pattern_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_kadane_pattern_problems.md](./04_Kadane_Pattern/02_kadane_pattern_problems.md) | Classic Kadane (Sum) | Max Subarray Sum, Min Subarray Sum, Circular Max Sum | Easy → Medium |
| [02_kadane_pattern_problems.md](./04_Kadane_Pattern/02_kadane_pattern_problems.md) | Product Kadane | Max Product Subarray, Max Absolute Sum | Medium |
| [02_kadane_pattern_problems.md](./04_Kadane_Pattern/02_kadane_pattern_problems.md) | Kadane + Stock / DP | Buy & Sell Stock, House Robber, Longest Positive Sum | Easy → Medium |
| [02_kadane_pattern_problems.md](./04_Kadane_Pattern/02_kadane_pattern_problems.md) | Kadane with State | Max Sum with One Deletion, Alternating Subarray Sum | Medium |
| [02_kadane_pattern_problems.md](./04_Kadane_Pattern/02_kadane_pattern_problems.md) | 2D Kadane | Max Sum Rectangle in Matrix, Max Sum Submatrix ≤ K | Hard |

---

### ✅ Binary Search
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_binary_search_pattern_notes.md](./10_Binary_Search_Pattern/01_binary_search_pattern_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_binary_search_pattern_problems.md](./10_Binary_Search_Pattern/02_binary_search_pattern_problems.md) | Basic Binary Search | Binary Search, Upper Bound, First/Last Position, Count Occurrences, Infinite Array | Easy → Medium |
| [02_binary_search_pattern_problems.md](./10_Binary_Search_Pattern/02_binary_search_pattern_problems.md) | Bitonic Array Search | Peak Index, Search in Bitonic Array, Find Peak Element | Easy → Medium |
| [02_binary_search_pattern_problems.md](./10_Binary_Search_Pattern/02_binary_search_pattern_problems.md) | Range Search | Min in Rotated, Count Rotations, Search Rotated, Rotated with Duplicates, Single Element | Medium → Hard |
| [02_binary_search_pattern_problems.md](./10_Binary_Search_Pattern/02_binary_search_pattern_problems.md) | Allocate Problems (BS on Answer) | Koko, Ship Packages, Book Allocation, Split Array, Aggressive Cows, Bouquets, Candies, H-Index | Medium → Hard |
| [02_binary_search_pattern_problems.md](./10_Binary_Search_Pattern/02_binary_search_pattern_problems.md) | Counting / Kth Element | 2D Matrix I & II, Kth Smallest Matrix, Multiplication Table, Median Two Arrays, Kth Missing | Medium → Hard |
| [02_binary_search_pattern_problems.md](./10_Binary_Search_Pattern/02_binary_search_pattern_problems.md) | FAANG Extras | Time Based KV Store, K Closest Elements, Min Speed, Max Gas Station Distance | Medium → Hard |

---

### ✅ Slow & Fast Pointers (Floyd's Algorithm)
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_slow_fast_pointers_notes.md](./03_Slow_And_Fast_Pointers_Pattern/01_slow_fast_pointers_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_slow_fast_pointers_problems.md](./03_Slow_And_Fast_Pointers_Pattern/02_slow_fast_pointers_problems.md) | Classic Floyd's — Cycle Detection | LinkedList Cycle, Start of LinkedList Cycle, Circular Array Loop | Easy → Hard |
| [02_slow_fast_pointers_problems.md](./03_Slow_And_Fast_Pointers_Pattern/02_slow_fast_pointers_problems.md) | Find Middle + Process | Middle of LinkedList, Palindrome LinkedList, Reorder List | Easy → Medium |
| [02_slow_fast_pointers_problems.md](./03_Slow_And_Fast_Pointers_Pattern/02_slow_fast_pointers_problems.md) | Gap Technique | Remove Nth Node From End, Odd Even Linked List | Medium |
| [02_slow_fast_pointers_problems.md](./03_Slow_And_Fast_Pointers_Pattern/02_slow_fast_pointers_problems.md) | Implicit Cycle | Happy Number, Find the Duplicate Number | Medium |
| [02_slow_fast_pointers_problems.md](./03_Slow_And_Fast_Pointers_Pattern/02_slow_fast_pointers_problems.md) | Slow Write / Fast Read | String Compression, Remove Duplicates I & II, Duplicate Zeros | Easy → Medium |
| [02_slow_fast_pointers_problems.md](./03_Slow_And_Fast_Pointers_Pattern/02_slow_fast_pointers_problems.md) | Rotate / Split + Reconnect | Rotate List, Rotate Array | Medium |
| [02_slow_fast_pointers_problems.md](./03_Slow_And_Fast_Pointers_Pattern/02_slow_fast_pointers_problems.md) | Two-pointer String / Array | Partition Labels, Counting Binary Substrings, Last Substring | Easy → Hard |
| [02_slow_fast_pointers_problems.md](./03_Slow_And_Fast_Pointers_Pattern/02_slow_fast_pointers_problems.md) | Bonus / FAANG | Intersection of Two Lists, Sort List, Bounded Max Subarrays, K-diff Pairs | Easy → Medium |

---

### ✅ Stack
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_stack_notes.md](./07_Stack_Pattern/01_stack_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_stack_problems.md](./07_Stack_Pattern/02_stack_problems.md) | Monotonic Stack | NGE I/II, Daily Temps, Stock Span, Largest Rectangle, Trapping Rain Water, Sum Subarray Mins, Remove Nodes LL | Easy → Hard |
| [02_stack_problems.md](./07_Stack_Pattern/02_stack_problems.md) | Bracket / Parentheses | Valid Parentheses, Min Remove Valid, Longest Valid Parens, Score of Parentheses | Easy → Hard |
| [02_stack_problems.md](./07_Stack_Pattern/02_stack_problems.md) | Stack + Count / Removal | Remove Adjacent I & II, Backspace, Remove Stars, Remove Duplicate Letters, Remove K Digits | Easy → Hard |
| [02_stack_problems.md](./07_Stack_Pattern/02_stack_problems.md) | Expression Evaluation | Evaluate RPN, Basic Calculator II, Basic Calculator, Decode String | Medium → Hard |
| [02_stack_problems.md](./07_Stack_Pattern/02_stack_problems.md) | Stack Simulation | Simplify Path, Asteroid Collision, Baseball Game, Reverse String | Easy → Medium |
| [02_stack_problems.md](./07_Stack_Pattern/02_stack_problems.md) | Design Problems | Min Stack, Queue via Stacks, Stack via Queues, Browser History, Max Freq Stack | Easy → Hard |

---

### ✅ HashMap
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_hashmap_notes.md](./08_HashMap_Pattern/01_hashmap_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_hashmap_problems.md](./08_HashMap_Pattern/02_hashmap_problems.md) | Frequency Count | Valid Anagram, First Non-Repeating, Max Balloons, Longest Palindrome, Ransom Note, Top K Frequent | Easy → Medium |
| [02_hashmap_problems.md](./08_HashMap_Pattern/02_hashmap_problems.md) | Complement Lookup | Two Sum | Easy |
| [02_hashmap_problems.md](./08_HashMap_Pattern/02_hashmap_problems.md) | Prefix Sum | Subarray Sum = K | Medium |
| [02_hashmap_problems.md](./08_HashMap_Pattern/02_hashmap_problems.md) | Grouping / Bucketing | Group Anagrams | Medium |
| [02_hashmap_problems.md](./08_HashMap_Pattern/02_hashmap_problems.md) | Index Tracking + Sliding Window | Longest Substring Without Repeating | Medium |
| [02_hashmap_problems.md](./08_HashMap_Pattern/02_hashmap_problems.md) | Two-Map Bidirectional | Isomorphic Strings, Word Pattern | Easy |
| [02_hashmap_problems.md](./08_HashMap_Pattern/02_hashmap_problems.md) | HashSet Membership | Jewels & Stones, Contains Duplicate II, Longest Consecutive Sequence | Easy → Medium |
| [02_hashmap_problems.md](./08_HashMap_Pattern/02_hashmap_problems.md) | Design (LRU Cache) | LRU Cache | Medium |

---

### ✅ In-Place Reversal of a LinkedList
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_inplace_reversal_notes.md](./09_In-Place_Reversal_LinkedList/01_inplace_reversal_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_inplace_reversal_problems.md](./09_In-Place_Reversal_LinkedList/02_inplace_reversal_problems.md) | Full Reversal | Reverse a LinkedList | Easy |
| [02_inplace_reversal_problems.md](./09_In-Place_Reversal_LinkedList/02_inplace_reversal_problems.md) | Partial / Sub-list Reversal | Reverse a Sub-list [p,q] | Medium |
| [02_inplace_reversal_problems.md](./09_In-Place_Reversal_LinkedList/02_inplace_reversal_problems.md) | K-Group Reversal | Reverse in Pairs, Reverse K-Group, Reverse Alternate K | Medium → Hard |
| [02_inplace_reversal_problems.md](./09_In-Place_Reversal_LinkedList/02_inplace_reversal_problems.md) | Conditional Reversal | Reverse Nodes in Even Length Groups | Hard |
| [02_inplace_reversal_problems.md](./09_In-Place_Reversal_LinkedList/02_inplace_reversal_problems.md) | Rotation / Reconnect | Rotate a LinkedList | Medium |
| [02_inplace_reversal_problems.md](./09_In-Place_Reversal_LinkedList/02_inplace_reversal_problems.md) | Reversal as a Tool | Palindrome LL, Reorder List, Sort List | Easy → Medium |
| [02_inplace_reversal_problems.md](./09_In-Place_Reversal_LinkedList/02_inplace_reversal_problems.md) | FAANG / Hard | Remove Nth, Add Two Numbers, Copy Random Pointer, Merge Two Sorted | Easy → Medium |

---

### 🔜 Coming Soon

| Folder | Pattern | Key Topics |
|--------|---------|------------|
| `11_Cyclic_Sort_Pattern` | Cyclic Sort | Missing number, Duplicate number, Find all missing, Corrupt pair |
| `12_Heap_Pattern` | Heap / Priority Queue | Top K elements, Kth largest, Merge K sorted lists, Median from stream |
| `13_Recursion_And_Backtracking` | Recursion & Backtracking | Subsets, Permutations, Combination sum, N-Queens, Sudoku solver, Word search |
| `14_Trees_Pattern` | Trees | BFS/DFS traversal, BST operations, LCA, Tree diameter, Serialize/Deserialize |
| `15_Graph_Pattern` | Graphs | BFS, DFS, Topological sort, Union Find, Dijkstra, Bellman-Ford, Bipartite |
| `16_Dynamic_Programming_Pattern` | Dynamic Programming | 0/1 Knapsack, LCS, LIS, Coin change, DP on trees, DP on graphs |
| `17_Trie_Pattern` | Trie | Insert/Search/Delete, Word search II, Auto-complete, Replace words |
| `18_Bit_Manipulation_Pattern` | Bit Manipulation | XOR tricks, Count bits, Power of two, Subsets via bits, Single number |

---

## 🔍 How to Use These Notes

1. **Pick a pattern** from the table above
2. **Read the concept section** — core idea + 3 key rules
3. **Study the universal template** — adapt this in your interview
4. **Go through each problem** — read the approach table before the code
5. **Revise using the cheatsheet** — quick reference before your interview

---

## 📝 Note Format — Every File Follows This Structure

```
Notes file  (01_*_notes.md):
├── How to identify this pattern  (keywords + brute force test + 5 signals)
├── What is this pattern?
├── Core rules  (3 things to always remember)
├── 2-question framework  (how to identify the variant)
├── Variants table + Pattern categories
├── Universal Java template  (with commented labels)
├── Quick reference cheatsheet
├── Common mistakes
└── Complexity summary

Problems file  (02_*_problems.md):
├── TOC organized by category
└── Each problem:
    ├── Approach table  (loop / condition / result)
    ├── Clean Java code
    └── Input → Output example
```

---

## ⚡ Two Pointers — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"sorted array" + "find pair with target sum"` | Both-ends (L=0, R=n-1) |
| `"3Sum / 4Sum / triplet / quadruple"` | Both-ends inside outer loop + skip dups |
| `"in-place remove / partition / overwrite"` | Slow/fast same direction |
| `"palindrome check / reverse string"` | Both-ends compare/swap |
| `"squares of sorted array"` | Both-ends, fill result from end |
| `"sort 0s, 1s, 2s / Dutch national flag"` | 3-pointer (low, mid, high) |
| `"merge two sorted arrays"` | Two arrays, one pointer each |
| `"is X a subsequence of Y"` | Two arrays, advance both on match |
| `"backspace string compare"` | Reverse traversal with skip count |
| `"trapping rain water / container with most water"` | Both-ends, advance shorter side |
| `"next permutation"` | Find dip → swap → reverse suffix |
| `"O(1) space" + sorted input` | Two pointers instead of HashSet |

---

## ⚡ Sliding Window — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"max / min sum of subarray of size k"` | Fixed Window |
| `"permutation / anagram of pattern in s"` | Fixed Window (size = pattern length) |
| `"longest substring with at most k distinct"` | Variable Window — Maximize |
| `"longest with at most k replacements"` | Variable Window — Maximize |
| `"longest without repeating characters"` | Variable Window — Maximize |
| `"max consecutive ones with k flips"` | Variable Window — Maximize |
| `"smallest subarray with sum ≥ target"` | Variable Window — Minimize |
| `"minimum window containing all chars"` | Variable Window — Minimize |
| `"count subarrays with exactly k distinct"` | At-Most Trick |
| `"subarray product less than k"` | Variable Window — Count |
| `"contiguous subarray / substring" + optimize` | Sliding Window candidate |

---

## ⚡ Kadane's Algorithm — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"maximum subarray sum"` | Classic Kadane |
| `"minimum subarray sum"` | Min Kadane |
| `"maximum product subarray"` | Product Kadane (track max + min) |
| `"maximum sum circular subarray"` | Circular Kadane (total − min subarray) |
| `"best time to buy and sell stock"` | Kadane on price differences |
| `"max sum with one deletion"` | Forward + Backward Kadane arrays |
| `"house robber / non-adjacent elements"` | Non-adjacent DP (Kadane style) |
| `"maximum sum rectangle in 2D matrix"` | 2D Kadane (column compression) |
| `"max sum submatrix no larger than k"` | 2D Kadane + TreeSet binary search |
| `"maximum alternating subarray sum"` | Alternating state Kadane |
| `"maximum absolute sum of any subarray"` | max(maxKadane, abs(minKadane)) |

---

## ⚡ Binary Search — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"find target in sorted array"` | Classic Binary Search |
| `"first / last occurrence"` | Left / Right Boundary Search |
| `"search in rotated sorted array"` | Rotated Array Search |
| `"rotated array with duplicates"` | Rotated + Shrink on Equal |
| `"peak element / mountain array"` | Peak Finding (Bitonic) |
| `"search in bitonic / mountain array"` | Bitonic Array Search |
| `"single non-duplicate in sorted array"` | Parity-based Binary Search |
| `"minimize the maximum / maximize the minimum"` | Binary Search on Answer |
| `"minimum speed / days / capacity"` | Binary Search on Answer |
| `"allocate / split / distribute among k groups"` | Binary Search on Answer |
| `"kth smallest in sorted matrix"` | Count ≤ mid |
| `"median of two sorted arrays"` | Partition Binary Search |
| `"kth missing positive"` | Missing count formula |
| `"k closest elements"` | Window binary search |
| `"timestamp get latest ≤ t"` | Right boundary search |

---

## ⚡ Slow & Fast Pointers — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"detect a cycle in linked list"` | Cycle Detection |
| `"find start / entry point of cycle"` | Cycle Start (Floyd Phase 2) |
| `"middle of linked list"` | Find Middle |
| `"palindrome linked list"` | Find Middle + Reverse |
| `"reorder / rearrange linked list"` | Find Middle + Reverse + Merge |
| `"happy number"` | Implicit Cycle (number sequence) |
| `"find duplicate number"` | Implicit Cycle (array as linked list) |
| `"cycle in circular array"` | Implicit Cycle (index jumps) |
| `"kth node from end"` | Gap technique (fast starts k ahead) |
| `"odd/even index grouping"` | Pointer Rearrangement (odd/even hop) |
| `"does linked list intersect"` | Redirect technique |
| `"O(1) space" + linked list` | Cannot use HashSet → Fast & Slow |

---

## ⚡ Prefix Sum — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"subarray sum equals k"` | HashMap count — `map.put(0,1)` |
| `"count subarrays with sum / divisible by k"` | Modulo HashMap |
| `"equal 0s and 1s / equal X and Y"` | Remap 0→-1, sum=0 |
| `"pivot / equilibrium index"` | `2*leftSum + nums[i] == total` |
| `"range sum query"` (multiple queries) | Prefix array, O(1) query |
| `"2D rectangle sum query"` | 2D prefix — inclusion-exclusion |
| `"shortest subarray sum ≥ k"` (with negatives) | Prefix + monotonic deque |
| `"count range sums in [lo, hi]"` | Prefix + merge sort |
| `"max rectangle sum ≤ k"` | 2D prefix + TreeSet |
| `"running total"` + "O(1) space per query" | Prefix array |

---

## ⚡ Merge Intervals — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"merge overlapping intervals"` | Sort by start + linear scan |
| `"insert interval into sorted list"` | 3-phase: before / overlap / after |
| `"intersection of two interval lists"` | Two-pointer, advance smaller end |
| `"any two intervals overlap?"` | Sort + adjacent end >= next start |
| `"minimum meeting rooms / conference rooms"` | Min-heap of end times |
| `"maximum CPU load / max overlap at any point"` | Min-heap of end times |
| `"employee free time / common free slots"` | Merge all + find gaps |
| `"remove minimum intervals → non-overlapping"` | Sort by end, greedy keep earliest |
| `"minimum arrows / points to cover all"` | Sort by end, greedy shoot at end |
| `"O(1) space" + interval problems` | Two-pointer on sorted start/end arrays |

---

## ⚡ Stack — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"next / previous greater / smaller"` | Monotonic Stack |
| `"largest rectangle / histogram"` | Monotonic Stack + sentinel |
| `"trapping rain water"` | Monotonic Stack valley |
| `"sum of subarray minimums / maximums"` | Monotonic Stack contribution |
| `"stock span / consecutive days"` | Monotonic Stack distance |
| `"valid / balanced parentheses"` | Bracket match — push open, match close |
| `"remove k adjacent same"` | Stack + [char, count] pair |
| `"decode 3[abc] / nested encoding"` | Save/restore — push (k, sb) on `[` |
| `"backspace # / remove stars *"` | Stack simulation — pop on trigger |
| `"evaluate RPN / postfix expression"` | Expression stack — b=pop, a=pop |
| `"basic calculator / infix expression"` | Expression + sign tracking |
| `"collision / asteroid"` | Conditional stack — pop on condition |
| `"O(1) getMin"` | Augmented stack — push (val, min) |
| `"implement queue using stacks"` | Two stacks — inbox/outbox |
| `"browser history / undo redo"` | Two stacks — back/forward |
| `"most frequent / max frequency"` | Freq map + group map |

---

## ⚡ HashMap — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"two numbers that sum to target"` | Complement Lookup |
| `"find pair with difference k"` | Complement Lookup |
| `"count occurrences / frequency"` | Frequency Count |
| `"most frequent / top k"` | Frequency Count |
| `"first non-repeating / unique character"` | Frequency Count |
| `"anagram / permutation of"` | Frequency Count |
| `"can X be constructed from Y"` | Frequency Count (two-map) |
| `"palindrome from given characters"` | Frequency Count |
| `"group by / classify / anagram groups"` | Grouping / Bucketing |
| `"subarray sum equals k"` | Prefix Sum |
| `"longest subarray with sum k"` | Prefix Sum |
| `"longest substring without repeating"` | Index Tracking + Sliding Window |
| `"duplicate / already seen"` | HashSet |
| `"isomorphic / pattern match"` | Two-map Bidirectional |
| `"jewels in stones / membership check"` | HashSet Lookup |
| `"nearby duplicate within k indices"` | Index Tracking Map |
| `"longest consecutive sequence O(n)"` | HashSet + sequence start check |
| `"LRU cache / evict least recently used"` | LinkedHashMap or HashMap + DLL |

---

## ⚡ In-Place Reversal of a LinkedList — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"reverse a linked list"` | Full Reversal — 4-line flip |
| `"reverse between positions p and q"` | Partial Reversal — skip + segment reverse + reconnect |
| `"reverse in pairs / swap adjacent nodes"` | K-Group (k=2) — dummy + pair swap |
| `"reverse every k nodes / k-group"` | K-Group — check k exist, reverse, reconnect |
| `"reverse alternate k"` | K-Group + Skip — reverse k, skip k, repeat |
| `"reverse even-length groups"` | Conditional — check actual size, reverse if even |
| `"rotate a linked list by k"` | Rotation — find tail+len, `k%len`, reconnect |
| `"in-place" + linked list` | 3-pointer: prev, curr, next |
| `"do not use extra space"` | Cannot use array/stack → pointer flip |
| `"reorder list L0→Ln→L1→Ln-1"` | Reversal Tool — find mid, reverse half, merge |
| `"sort linked list O(n log n)"` | Reversal Tool — merge sort with find-mid |
| `"remove nth from end"` | Gap Technique — fast n+1 ahead |
| `"deep copy with random pointer"` | HashMap or interleave trick |
| `"merge two sorted lists"` | Dummy head + compare + append rest |

---

## 📊 Problems Index

| # | Problem | LC # | Pattern | Difficulty | Status |
|---|---------|------|---------|------------|--------|
| 1 | Pair with Target Sum (2Sum II) | 167 | Two Pointers — Both-ends Sum | Easy | ✅ |
| 2 | Triplet Sum to Zero (3Sum) | 15 | Two Pointers — Both-ends Sum | Medium | ✅ |
| 3 | 3Sum Closest | 16 | Two Pointers — Both-ends Sum | Medium | ✅ |
| 4 | Triplets with Smaller Sum | — | Two Pointers — Both-ends Sum | Medium | ✅ |
| 5 | Quadruple Sum to Target (4Sum) | 18 | Two Pointers — Both-ends Sum | Medium | ✅ |
| 6 | Valid Palindrome | 125 | Two Pointers — Both-ends Palindrome | Easy | ✅ |
| 7 | Reverse Vowels of a String | 345 | Two Pointers — Both-ends Swap | Easy | ✅ |
| 8 | Squares of a Sorted Array | 977 | Two Pointers — Both-ends Fill | Easy | ✅ |
| 9 | Remove Duplicates from Sorted Array | 26 | Two Pointers — Slow/Fast | Easy | ✅ |
| 10 | Rearrange 0s and 1s | — | Two Pointers — Slow/Fast | Easy | ✅ |
| 11 | Comparing Strings with Backspaces | 844 | Two Pointers — Reverse Traversal | Medium | ✅ |
| 12 | Sort Colors (Dutch National Flag) | 75 | Two Pointers — 3-pointer | Medium | ✅ |
| 13 | Merge Sorted Array | 88 | Two Pointers — Two Arrays | Easy | ✅ |
| 14 | Is Subsequence | 392 | Two Pointers — Two Arrays | Easy | ✅ |
| 15 | Subarrays with Product Less than K | 713 | Two Pointers — Window/Count | Medium | ✅ |
| 16 | Minimum Window Sort | 581 | Two Pointers — Both-ends Scan | Medium | ✅ |
| 17 | Remove Palindromic Subsequences | 1332 | Two Pointers — Palindrome Check | Easy | ✅ |
| 18 | Reverse Words in a String | 151 | Two Pointers — Both-ends Swap | Medium | ✅ |
| 19 | Trapping Rain Water | 42 | Two Pointers — Both-ends Water | Hard | ✅ |
| 20 | Container with Most Water | 11 | Two Pointers — Both-ends Area | Medium | ✅ |
| 21 | Next Greater Element I | 496 | Stack — Monotonic | Easy | ✅ |
| 22 | Daily Temperatures | 739 | Stack — Monotonic | Medium | ✅ |
| 23 | Next Greater Element II (Circular) | 503 | Stack — Monotonic | Medium | ✅ |
| 24 | Stock Span Problem | 901 | Stack — Monotonic | Medium | ✅ |
| 25 | Online Stock Span | 901 | Stack — Monotonic Design | Medium | ✅ |
| 26 | Largest Rectangle in Histogram | 84 | Stack — Monotonic | Hard | ✅ |
| 27 | Trapping Rain Water | 42 | Stack — Monotonic | Hard | ✅ |
| 28 | Sum of Subarray Minimums | 907 | Stack — Monotonic | Medium | ✅ |
| 29 | Remove Nodes From Linked List | 2487 | Stack — Monotonic | Medium | ✅ |
| 30 | Valid Parentheses | 20 | Stack — Bracket Match | Easy | ✅ |
| 31 | Minimum Remove to Make Valid | 1249 | Stack — Bracket Match | Medium | ✅ |
| 32 | Longest Valid Parentheses | 32 | Stack — Bracket Match | Hard | ✅ |
| 33 | Score of Parentheses | 856 | Stack — Bracket Score | Medium | ✅ |
| 34 | Remove All Adjacent Duplicates I | 1047 | Stack — Removal | Easy | ✅ |
| 35 | Remove All Adjacent Duplicates II | 1209 | Stack + Count | Medium | ✅ |
| 36 | Backspace String Compare | 844 | Stack — Simulation | Easy | ✅ |
| 37 | Removing Stars From a String | 2390 | Stack — Simulation | Medium | ✅ |
| 38 | Remove Duplicate Letters | 316 | Stack — Monotonic + Greedy | Hard | ✅ |
| 39 | Remove K Digits | 402 | Stack — Monotonic + Greedy | Medium | ✅ |
| 40 | Evaluate Reverse Polish Notation | 150 | Stack — Expression | Medium | ✅ |
| 41 | Basic Calculator II | 227 | Stack — Expression | Medium | ✅ |
| 42 | Basic Calculator | 224 | Stack — Expression | Hard | ✅ |
| 43 | Decode String | 394 | Stack — Save/Restore | Medium | ✅ |
| 44 | Simplify Path | 71 | Stack — Simulation | Medium | ✅ |
| 45 | Asteroid Collision | 735 | Stack — Conditional | Medium | ✅ |
| 46 | Baseball Game | 682 | Stack — Simulation | Easy | ✅ |
| 47 | Reverse String Using Stack | — | Stack — Basic | Easy | ✅ |
| 48 | Min Stack | 155 | Stack — Design | Medium | ✅ |
| 49 | Implement Queue Using Stacks | 232 | Stack — Design | Easy | ✅ |
| 50 | Implement Stack Using Queues | 225 | Stack — Design | Easy | ✅ |
| 51 | Design Browser History | 1472 | Stack — Design | Medium | ✅ |
| 52 | Maximum Frequency Stack | 895 | Stack — Design | Hard | ✅ |
| 53 | Two Sum | 1 | HashMap — Complement Lookup | Easy | ✅ |
| 54 | Valid Anagram | 242 | HashMap — Frequency Count | Easy | ✅ |
| 55 | First Non-Repeating Character | 387 | HashMap — Frequency Count | Easy | ✅ |
| 56 | Maximum Number of Balloons | 1189 | HashMap — Frequency Count | Easy | ✅ |
| 57 | Longest Palindrome | 409 | HashMap — Frequency Count | Easy | ✅ |
| 58 | Ransom Note | 383 | HashMap — Frequency Count | Easy | ✅ |
| 59 | Subarray Sum Equals K | 560 | HashMap — Prefix Sum | Medium | ✅ |
| 60 | Longest Substring Without Repeating | 3 | HashMap — Index Tracking | Medium | ✅ |
| 61 | Group Anagrams | 49 | HashMap — Grouping | Medium | ✅ |
| 62 | Top K Frequent Elements | 347 | HashMap — Frequency Count | Medium | ✅ |
| 63 | Jewels and Stones | 771 | HashMap — HashSet Lookup | Easy | ✅ |
| 64 | Isomorphic Strings | 205 | HashMap — Two-Map Bidirectional | Easy | ✅ |
| 65 | Word Pattern | 290 | HashMap — Two-Map Bidirectional | Easy | ✅ |
| 66 | Contains Duplicate II | 219 | HashMap — Index Tracking | Easy | ✅ |
| 67 | Longest Consecutive Sequence | 128 | HashMap — HashSet + Sequence | Medium | ✅ |
| 68 | LRU Cache | 146 | HashMap — Design (LinkedHashMap) | Medium | ✅ |
| 69 | Reverse a LinkedList | 206 | In-Place Reversal — Full | Easy | ✅ |
| 70 | Reverse a Sub-list | 92 | In-Place Reversal — Partial | Medium | ✅ |
| 71 | Reverse List in Pairs | 24 | In-Place Reversal — K-Group k=2 | Medium | ✅ |
| 72 | Reverse Every K-element Sub-list | 25 | In-Place Reversal — K-Group | Hard | ✅ |
| 73 | Reverse Nodes in Even Length Groups | 2074 | In-Place Reversal — Conditional | Hard | ✅ |
| 74 | Rotate a LinkedList | 61 | In-Place Reversal — Rotation | Medium | ✅ |
| 75 | Reverse Alternate K Elements | — | In-Place Reversal — Alternate K | Medium | ✅ |
| 76 | Palindrome LinkedList | 234 | In-Place Reversal — Tool | Easy | ✅ |
| 77 | Reorder List | 143 | In-Place Reversal — Tool | Medium | ✅ |
| 78 | Sort List | 148 | In-Place Reversal — Merge Sort | Medium | ✅ |
| 79 | Remove Nth Node From End | 19 | In-Place Reversal — Gap Technique | Medium | ✅ |
| 80 | Add Two Numbers | 2 | In-Place Reversal — Simulation | Medium | ✅ |
| 81 | Copy List with Random Pointer | 138 | In-Place Reversal — Clone | Medium | ✅ |
| 82 | Merge Two Sorted Lists | 21 | In-Place Reversal — Merge | Easy | ✅ |
| 83 | LinkedList Cycle | 141 | Slow & Fast — Cycle Detection | Easy | ✅ |
| 84 | Start of LinkedList Cycle | 142 | Slow & Fast — Cycle Start | Medium | ✅ |
| 85 | Happy Number | 202 | Slow & Fast — Implicit Cycle | Medium | ✅ |
| 86 | Find the Duplicate Number | 287 | Slow & Fast — Implicit Cycle | Medium | ✅ |
| 87 | Middle of the LinkedList | 876 | Slow & Fast — Find Middle | Easy | ✅ |
| 88 | Palindrome LinkedList | 234 | Slow & Fast — Middle + Reverse | Medium | ✅ |
| 89 | Reorder List | 143 | Slow & Fast — Middle + Reverse + Merge | Medium | ✅ |
| 90 | Cycle in a Circular Array | 457 | Slow & Fast — Implicit Cycle (Array) | Hard | ✅ |
| 91 | Remove Nth Node From End | 19 | Slow & Fast — Gap Technique | Medium | ✅ |
| 92 | Intersection of Two Lists | 160 | Slow & Fast — Redirect Technique | Easy | ✅ |
| 93 | Odd Even Linked List | 328 | Slow & Fast — Pointer Rearrangement | Medium | ✅ |
| 94 | String Compression | 443 | Slow & Fast — Slow Write / Fast Read | Medium | ✅ |
| 95 | Remove Duplicates from Sorted Array | 26 | Slow & Fast — Slow Write / Fast Read | Easy | ✅ |
| 96 | Remove Duplicates from Sorted Array II | 80 | Slow & Fast — Slow Write / Fast Read | Medium | ✅ |
| 97 | Duplicate Zeros | 1089 | Slow & Fast — Slow Write / Fast Read | Easy | ✅ |
| 98 | Rotate List | 61 | Slow & Fast — Rotate / Reconnect | Medium | ✅ |
| 99 | Rotate Array | 189 | Slow & Fast — Rotate / Reconnect | Medium | ✅ |
| 100 | Partition Labels | 763 | Slow & Fast — Two-pointer String | Medium | ✅ |
| 101 | Counting Binary Substrings | 696 | Slow & Fast — Two-pointer String | Easy | ✅ |
| 102 | Last Substring in Lexicographical Order | 1163 | Slow & Fast — Two-pointer String | Hard | ✅ |
| 103 | Sort List | 148 | Slow & Fast — Middle + Merge Sort | Medium | ✅ |
| 104 | Number of Subarrays with Bounded Maximum | 795 | Slow & Fast — Two-pointer Count | Medium | ✅ |
| 105 | K-diff Pairs in an Array | 532 | Slow & Fast — Two-pointer Sorted | Medium | ✅ |
| 106 | Binary Search | 704 | Binary Search — Basic | Easy | ✅ |
| 107 | Search Insert Position | 35 | Binary Search — Upper Bound | Easy | ✅ |
| 108 | First and Last Position | 34 | Binary Search — Boundary Search | Medium | ✅ |
| 109 | Count Occurrences in Sorted Array | — | Binary Search — Counting | Easy | ✅ |
| 110 | Search in Infinite Sorted Array | — | Binary Search — Exponential + BS | Medium | ✅ |
| 111 | Peak Index in Mountain Array | 852 | Binary Search — Bitonic | Easy | ✅ |
| 112 | Search in Bitonic Array | — | Binary Search — Bitonic | Medium | ✅ |
| 113 | Find Peak Element | 162 | Binary Search — Bitonic | Medium | ✅ |
| 114 | Find Minimum in Rotated Sorted Array | 153 | Binary Search — Range Search | Medium | ✅ |
| 115 | Find Number of Rotations | — | Binary Search — Range Search | Easy | ✅ |
| 116 | Search in Rotated Sorted Array | 33 | Binary Search — Range Search | Medium | ✅ |
| 117 | Find Min in Rotated II (Duplicates) | 154 | Binary Search — Range Search | Hard | ✅ |
| 118 | Search in Rotated II (Duplicates) | 81 | Binary Search — Range Search | Medium | ✅ |
| 119 | Single Element in Sorted Array | 540 | Binary Search — Parity | Medium | ✅ |
| 120 | Koko Eating Bananas | 875 | Binary Search — Allocate | Medium | ✅ |
| 121 | Min Days to Make M Bouquets | 1482 | Binary Search — Allocate | Medium | ✅ |
| 122 | Aggressive Cows | — | Binary Search — Allocate | Medium | ✅ |
| 123 | H-Index II | 275 | Binary Search — Allocate | Medium | ✅ |
| 124 | Maximum Candies to K Children | 2226 | Binary Search — Allocate | Medium | ✅ |
| 125 | Capacity to Ship in D Days | 1011 | Binary Search — Allocate | Medium | ✅ |
| 126 | Book Allocation Problem | — | Binary Search — Allocate | Hard | ✅ |
| 127 | Split Array Largest Sum | 410 | Binary Search — Allocate | Hard | ✅ |
| 128 | Minimum Speed to Arrive on Time | 1870 | Binary Search — Allocate | Medium | ✅ |
| 129 | Minimize Max Gas Station Distance | 774 | Binary Search — Allocate | Hard | ✅ |
| 130 | Search a 2D Matrix | 74 | Binary Search — 2D | Medium | ✅ |
| 131 | Search a 2D Matrix II | 240 | Binary Search — 2D (Staircase) | Medium | ✅ |
| 132 | Kth Smallest in Sorted Matrix | 378 | Binary Search — Kth Element | Medium | ✅ |
| 133 | Kth Smallest in Multiplication Table | 668 | Binary Search — Kth Element | Hard | ✅ |
| 134 | Median of Two Sorted Arrays | 4 | Binary Search — Partition | Hard | ✅ |
| 135 | Kth Missing Positive Number | 1539 | Binary Search — Missing Count | Easy | ✅ |
| 136 | Time Based Key-Value Store | 981 | Binary Search — FAANG | Medium | ✅ |
| 137 | Find K Closest Elements | 658 | Binary Search — FAANG | Medium | ✅ |
| 138 | Maximum Sum Subarray of Size K | — | Sliding Window — Fixed | Easy | ✅ |
| 139 | Maximum Average Subarray I | 643 | Sliding Window — Fixed | Easy | ✅ |
| 140 | Permutation in a String | 567 | Sliding Window — Fixed | Medium | ✅ |
| 141 | Find All Anagrams in a String | 438 | Sliding Window — Fixed | Medium | ✅ |
| 142 | Longest Substring Without Repeating | 3 | Sliding Window — Variable Maximize | Medium | ✅ |
| 143 | Longest Substring K Distinct | 340 | Sliding Window — Variable Maximize | Medium | ✅ |
| 144 | Fruits into Baskets | 904 | Sliding Window — Variable Maximize | Medium | ✅ |
| 145 | Longest Repeating Char Replacement | 424 | Sliding Window — Variable Maximize | Hard | ✅ |
| 146 | Max Consecutive Ones III | 1004 | Sliding Window — Variable Maximize | Medium | ✅ |
| 147 | Longest Subarray of 1s (Delete One) | 1493 | Sliding Window — Variable Maximize | Medium | ✅ |
| 148 | Get Equal Substrings Within Budget | 1208 | Sliding Window — Variable Maximize | Medium | ✅ |
| 149 | Minimum Size Subarray Sum | 209 | Sliding Window — Variable Minimize | Medium | ✅ |
| 150 | Minimum Window Substring | 76 | Sliding Window — Variable Minimize | Hard | ✅ |
| 151 | Subarray Product Less Than K | 713 | Sliding Window — Variable Count | Medium | ✅ |
| 152 | Subarrays with K Different Integers | 992 | Sliding Window — At-Most Trick | Hard | ✅ |
| 153 | Binary Subarrays with Sum | 930 | Sliding Window — At-Most Trick | Medium | ✅ |
| 154 | Count Number of Nice Subarrays | 1248 | Sliding Window — At-Most Trick | Medium | ✅ |
| 155 | Substring with Concatenation of Words | 30 | Sliding Window — FAANG Hard | Hard | ✅ |
| 156 | Frequency of Most Frequent Element | 1838 | Sliding Window — FAANG Hard | Medium | ✅ |
| 157 | Maximize the Confusion of an Exam | 2024 | Sliding Window — FAANG Hard | Medium | ✅ |
| 158 | Min Ops to Make Array Continuous | 2009 | Sliding Window — FAANG Hard | Hard | ✅ |
| 159 | Maximum Subarray Sum | 53 | Kadane — Classic | Easy | ✅ |
| 160 | Minimum Subarray Sum | — | Kadane — Classic | Easy | ✅ |
| 161 | Maximum Product Subarray | 152 | Kadane — Product | Medium | ✅ |
| 162 | Maximum Sum Circular Subarray | 918 | Kadane — Circular | Medium | ✅ |
| 163 | Best Time to Buy and Sell Stock | 121 | Kadane — Stock | Easy | ✅ |
| 164 | Max Subarray Sum with One Deletion | 1186 | Kadane — With State | Medium | ✅ |
| 165 | Longest Subarray with Positive Sum | — | Kadane — Prefix Sum | Medium | ✅ |
| 166 | Maximum Absolute Sum of Any Subarray | 1749 | Kadane — Dual | Medium | ✅ |
| 167 | House Robber | 198 | Kadane — Non-Adjacent DP | Medium | ✅ |
| 168 | Max Sum Rectangle in 2D Matrix | 363 | Kadane — 2D | Hard | ✅ |
| 169 | Max Sum Submatrix No Larger Than K | 363 | Kadane — 2D + Binary Search | Hard | ✅ |
| 170 | Maximum Alternating Subarray Sum | 2036 | Kadane — Alternating | Medium | ✅ |
| 171 | Range Sum Query - Immutable | 303 | Prefix Sum — Basic Prefix Array | Easy | ✅ |
| 172 | Find Pivot Index | 724 | Prefix Sum — Basic Prefix Array | Easy | ✅ |
| 173 | Subarray Sum Equals K | 560 | Prefix Sum — HashMap Count | Medium | ✅ |
| 174 | Contiguous Array | 525 | Prefix Sum — HashMap Remap | Medium | ✅ |
| 175 | Longest Subarray with Sum K | 325 | Prefix Sum — HashMap First-seen | Medium | ✅ |
| 176 | Subarray Sums Divisible by K | 974 | Prefix Sum — Modulo HashMap | Medium | ✅ |
| 177 | Continuous Subarray Sum | 523 | Prefix Sum — Modulo HashMap | Medium | ✅ |
| 178 | Range Sum Query 2D - Immutable | 304 | Prefix Sum — 2D Prefix Array | Medium | ✅ |
| 179 | Max Sum of Rectangle No Larger Than K | 363 | Prefix Sum — 2D Prefix + TreeSet | Hard | ✅ |
| 180 | Shortest Subarray with Sum at Least K | 862 | Prefix Sum — Prefix + Deque | Hard | ✅ |
| 181 | Count of Range Sum | 327 | Prefix Sum — Prefix + Merge Sort | Hard | ✅ |
| 182 | Maximum Product Subarray | 152 | Prefix Sum — Prefix Product | Medium | ✅ |
| 183 | Merge Intervals | 56 | Merge Interval — Sort + Scan | Medium | ✅ |
| 184 | Insert Interval | 57 | Merge Interval — 3-Phase Insert | Medium | ✅ |
| 185 | Interval List Intersections | 986 | Merge Interval — Two-pointer | Medium | ✅ |
| 186 | Overlapping Intervals Check | — | Merge Interval — Sort + Adjacent | Easy | ✅ |
| 187 | Minimum Meeting Rooms | 253 | Merge Interval — Min-Heap | Hard | ✅ |
| 188 | Maximum CPU Load | — | Merge Interval — Min-Heap | Hard | ✅ |
| 189 | Task Scheduler | 621 | Merge Interval — Max-Heap + Greedy | Medium | ✅ |
| 190 | Non-overlapping Intervals | 435 | Merge Interval — Greedy Sort End | Medium | ✅ |
| 191 | Min Arrows to Burst Balloons | 452 | Merge Interval — Greedy Sort End | Medium | ✅ |
| 192 | Meeting Scheduler | 1229 | Merge Interval — Two-pointer | Medium | ✅ |
| 193 | Employee Free Time | 759 | Merge Interval — Merge + Gap Scan | Hard | ✅ |
| 194 | Remove Covered Intervals | 1288 | Merge Interval — Sort + maxEnd | Medium | ✅ |
| 195 | Data Stream as Disjoint Intervals | 352 | Merge Interval — TreeMap Merge | Hard | ✅ |
---

## ⚙️ Setup

```bash
# Clone the repo
git clone https://github.com/rahul22mrk/DSA-Interview-Notes-Java.git

# Navigate to any pattern
cd DSA-Interview-Notes-Java/01_Two_Pointers_Patterns
cd DSA-Interview-Notes-Java/02_Sliding_Window_Patterns
cd DSA-Interview-Notes-Java/03_Slow_And_Fast_Pointers_Pattern
cd DSA-Interview-Notes-Java/07_Stack_Pattern
cd DSA-Interview-Notes-Java/08_HashMap_Pattern
cd DSA-Interview-Notes-Java/09_In-Place_Reversal_LinkedList
cd DSA-Interview-Notes-Java/10_Binary_Search_Pattern
cd DSA-Interview-Notes-Java/04_Kadane_Pattern

# Coming soon
cd DSA-Interview-Notes-Java/11_Cyclic_Sort_Pattern
cd DSA-Interview-Notes-Java/12_Heap_Pattern
cd DSA-Interview-Notes-Java/13_Recursion_And_Backtracking
cd DSA-Interview-Notes-Java/14_Trees_Pattern
cd DSA-Interview-Notes-Java/15_Graph_Pattern
cd DSA-Interview-Notes-Java/16_Dynamic_Programming_Pattern
cd DSA-Interview-Notes-Java/17_Trie_Pattern
cd DSA-Interview-Notes-Java/18_Bit_Manipulation_Pattern
```

> **Java Version:** 11+

---

## 🤝 Contributing

Found a bug or want to add a pattern? Feel free to open a PR or raise an issue.

---

*Last updated: March 2026 · Maintained by [@rahul22mrk](https://github.com/rahul22mrk)*
