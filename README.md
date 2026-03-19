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
├── 01_Two_Pointers/
│   └── 🔜 coming soon
│
├── 02_Sliding_Window_Patterns/
│   └── 🔜 coming soon
│
├── 03_Slow_And_Fast_Pointers_Pattern/
│   └── 01_slow_fast_pointers_notes.md
│
├── 04_Kadane_Pattern/
│   └── 🔜 coming soon
│
├── 05_Prefix_Sum_Pattern/
│   └── 🔜 coming soon
│
├── 06_Merge_Interval_Pattern/
│   └── 🔜 coming soon
│
├── 07_Stack_Pattern/
│   ├── 01-monotonic-stack.md
│   ├── 02-stack-count.md
│   └── 03-stack-simulation.md
│
├── 08_HashMap_Pattern/
│   └── 01-hashmap-pattern.md
│
├── 09_In-Place_Reversal_LinkedList/
│   └── 01-inplace-reversal-linkedlist.md
│
├── 10_Binary_Search_Pattern/
│   ├── 01_binary_search_pattern_notes.md
│   └── 02_binary_search_pattern_problems.md
│
└── README.md
```

---

## 🧩 Patterns Covered

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
| [01_slow_fast_pointers_notes.md](./03_Slow_And_Fast_Pointers_Pattern/01_slow_fast_pointers_notes.md) | Cycle Detection | LinkedList Cycle | Easy |
| [01_slow_fast_pointers_notes.md](./03_Slow_And_Fast_Pointers_Pattern/01_slow_fast_pointers_notes.md) | Cycle Start (Floyd Phase 2) | Start of LinkedList Cycle | Medium |
| [01_slow_fast_pointers_notes.md](./03_Slow_And_Fast_Pointers_Pattern/01_slow_fast_pointers_notes.md) | Implicit Cycle | Happy Number, Find Duplicate Number | Medium |
| [01_slow_fast_pointers_notes.md](./03_Slow_And_Fast_Pointers_Pattern/01_slow_fast_pointers_notes.md) | Find Middle | Middle of the LinkedList | Easy |
| [01_slow_fast_pointers_notes.md](./03_Slow_And_Fast_Pointers_Pattern/01_slow_fast_pointers_notes.md) | Middle + Reverse | Palindrome LinkedList | Medium |
| [01_slow_fast_pointers_notes.md](./03_Slow_And_Fast_Pointers_Pattern/01_slow_fast_pointers_notes.md) | Middle + Reverse + Merge | Reorder List | Medium |
| [01_slow_fast_pointers_notes.md](./03_Slow_And_Fast_Pointers_Pattern/01_slow_fast_pointers_notes.md) | Implicit Cycle (Array) | Cycle in a Circular Array | Hard |
| [01_slow_fast_pointers_notes.md](./03_Slow_And_Fast_Pointers_Pattern/01_slow_fast_pointers_notes.md) | Gap Technique | Remove Nth Node From End | Medium |
| [01_slow_fast_pointers_notes.md](./03_Slow_And_Fast_Pointers_Pattern/01_slow_fast_pointers_notes.md) | Redirect Technique | Intersection of Two Lists | Easy |

---

### ✅ Stack
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01-monotonic-stack.md](./07_Stack_Pattern/01-monotonic-stack.md) | Monotonic Stack | Next/Prev Greater, Daily Temps, Largest Rectangle, Trapping Rain Water, Stock Span, Subarray Minimums | Easy → Hard |
| [02-stack-count.md](./07_Stack_Pattern/02-stack-count.md) | Stack + Count | Remove Duplicates I & II, Decode String, Removing Stars, Backspace, Score of Parentheses, Valid Parentheses | Easy → Medium |
| [03-stack-simulation.md](./07_Stack_Pattern/03-stack-simulation.md) | Stack Simulation | Asteroid Collision, Evaluate RPN, Simplify Path, Remove K Digits, Remove Duplicate Letters | Easy → Hard |

---

### ✅ HashMap
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01-hashmap-pattern.md](./08_HashMap_Pattern/01-hashmap-pattern.md) | Frequency Count | Valid Anagram, First Non-Repeating Char, Max Balloons, Longest Palindrome, Ransom Note, Top K Frequent | Easy → Medium |
| [01-hashmap-pattern.md](./08_HashMap_Pattern/01-hashmap-pattern.md) | Complement Lookup | Two Sum | Easy |
| [01-hashmap-pattern.md](./08_HashMap_Pattern/01-hashmap-pattern.md) | Prefix Sum | Subarray Sum = K | Medium |
| [01-hashmap-pattern.md](./08_HashMap_Pattern/01-hashmap-pattern.md) | Grouping / Bucketing | Group Anagrams | Medium |
| [01-hashmap-pattern.md](./08_HashMap_Pattern/01-hashmap-pattern.md) | Index Tracking + Sliding Window | Longest Substring Without Repeating | Medium |

---

### ✅ In-Place Reversal of a LinkedList
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01-inplace-reversal-linkedlist.md](./09_In-Place_Reversal_LinkedList/01-inplace-reversal-linkedlist.md) | Full Reversal | Reverse a LinkedList | Easy |
| [01-inplace-reversal-linkedlist.md](./09_In-Place_Reversal_LinkedList/01-inplace-reversal-linkedlist.md) | Partial Reversal | Reverse a Sub-list [p,q] | Medium |
| [01-inplace-reversal-linkedlist.md](./09_In-Place_Reversal_LinkedList/01-inplace-reversal-linkedlist.md) | Pair Reversal (k=2) | Reverse List in Pairs | Medium |
| [01-inplace-reversal-linkedlist.md](./09_In-Place_Reversal_LinkedList/01-inplace-reversal-linkedlist.md) | K-Group Reversal | Reverse Every K-element Sub-list | Hard |
| [01-inplace-reversal-linkedlist.md](./09_In-Place_Reversal_LinkedList/01-inplace-reversal-linkedlist.md) | Conditional Reversal | Reverse Nodes in Even Length Groups | Hard |
| [01-inplace-reversal-linkedlist.md](./09_In-Place_Reversal_LinkedList/01-inplace-reversal-linkedlist.md) | Rotation | Rotate a LinkedList | Medium |

---

### 🔜 Coming Soon

| Folder | Pattern | Key Topics |
|--------|---------|------------|
| `01_Two_Pointers` | Two Pointers | Sorted arrays, Palindrome, Container with most water, 3Sum |
| `02_Sliding_Window_Patterns` | Sliding Window | Fixed window, Variable window, At most K distinct |
| `04_Kadane_Pattern` | Kadane's Algorithm | Max subarray, Max circular subarray |
| `05_Prefix_Sum_Pattern` | Prefix Sum | Subarray sum equals K, Range sum query |
| `06_Merge_Interval_Pattern` | Merge Intervals | Merge overlapping, Insert interval, Meeting rooms |

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
├── Variants table
├── Universal Java template  (with commented labels)
├── Quick reference cheatsheet
├── Common mistakes
└── Complexity summary

Problems file  (02_*_problems.md):
├── TOC by category
└── Each problem:
    ├── Approach table  (loop / condition / result)
    ├── Clean Java code
    └── Input → Output example
```

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
| `"does linked list intersect"` | Redirect technique |
| `"O(1) space" + linked list` | Cannot use HashSet → Fast & Slow |

---

## ⚡ Stack — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"next greater / smaller"` | Monotonic Stack |
| `"largest rectangle / histogram"` | Monotonic Stack |
| `"trapping rain water"` | Monotonic Stack |
| `"k adjacent equal / duplicates"` | Stack + Count |
| `"decode 3[abc]"` | Stack + Count |
| `"valid / balanced brackets"` | Stack + Count |
| `"collision / asteroid"` | Stack Simulation |
| `"evaluate expression / RPN"` | Stack Simulation |
| `"backspace / remove stars"` | Stack Simulation |

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
| `"isomorphic / pattern match"` | Two-map (bidirectional) |

---

## ⚡ In-Place Reversal of a LinkedList — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"reverse a linked list"` | Full Reversal |
| `"reverse between positions p and q"` | Partial Reversal (Sub-list) |
| `"reverse in pairs / swap adjacent nodes"` | Pair Reversal (k=2) |
| `"reverse every k nodes / k-group"` | K-Group Reversal |
| `"reverse even-length groups"` | Conditional Group Reversal |
| `"rotate a linked list by k"` | Rotation (no flip, reconnect) |
| `"in-place" + linked list` | 3-pointer technique |
| `"do not use extra space"` | Cannot use array/stack → pointer flip |

---

## 📊 Problems Index

| # | Problem | LC # | Pattern | Difficulty | Status |
|---|---------|------|---------|------------|--------|
| 1 | Next Greater Element I | 496 | Monotonic Stack | Easy | ✅ |
| 2 | Daily Temperatures | 739 | Monotonic Stack | Medium | ✅ |
| 3 | Stock Span Problem | 901 | Monotonic Stack | Medium | ✅ |
| 4 | Next Greater Element II | 503 | Monotonic Stack | Medium | ✅ |
| 5 | Sum of Subarray Minimums | 907 | Monotonic Stack | Medium | ✅ |
| 6 | Largest Rectangle in Histogram | 84 | Monotonic Stack | Hard | ✅ |
| 7 | Trapping Rain Water | 42 | Monotonic Stack | Hard | ✅ |
| 8 | Remove All Adjacent Duplicates I | 1047 | Stack + Count | Easy | ✅ |
| 9 | Valid Parentheses | 20 | Stack + Count | Easy | ✅ |
| 10 | Backspace String Compare | 844 | Stack + Count | Easy | ✅ |
| 11 | Remove All Adjacent Duplicates II | 1209 | Stack + Count | Medium | ✅ |
| 12 | Decode String | 394 | Stack + Count | Medium | ✅ |
| 13 | Removing Stars From a String | 2390 | Stack + Count | Medium | ✅ |
| 14 | Score of Parentheses | 856 | Stack + Count | Medium | ✅ |
| 15 | Min Remove to Make Valid | 1249 | Stack + Count | Medium | ✅ |
| 16 | Evaluate RPN | 150 | Stack Simulation | Medium | ✅ |
| 17 | Asteroid Collision | 735 | Stack Simulation | Medium | ✅ |
| 18 | Simplify Path | 71 | Stack Simulation | Medium | ✅ |
| 19 | Remove K Digits | 402 | Stack Simulation | Medium | ✅ |
| 20 | Longest Valid Parentheses | 32 | Stack + Count | Hard | ✅ |
| 21 | Remove Duplicate Letters | 316 | Stack Simulation | Hard | ✅ |
| 22 | Two Sum | 1 | HashMap — Complement Lookup | Easy | ✅ |
| 23 | Valid Anagram | 242 | HashMap — Frequency Count | Easy | ✅ |
| 24 | First Non-Repeating Character | 387 | HashMap — Frequency Count | Easy | ✅ |
| 25 | Maximum Number of Balloons | 1189 | HashMap — Frequency Count | Easy | ✅ |
| 26 | Longest Palindrome | 409 | HashMap — Frequency Count | Easy | ✅ |
| 27 | Ransom Note | 383 | HashMap — Frequency Count | Easy | ✅ |
| 28 | Subarray Sum Equals K | 560 | HashMap — Prefix Sum | Medium | ✅ |
| 29 | Longest Substring Without Repeating | 3 | HashMap — Index Tracking | Medium | ✅ |
| 30 | Group Anagrams | 49 | HashMap — Grouping | Medium | ✅ |
| 31 | Top K Frequent Elements | 347 | HashMap — Frequency Count | Medium | ✅ |
| 32 | Reverse a LinkedList | 206 | In-Place Reversal — Full | Easy | ✅ |
| 33 | Reverse a Sub-list | 92 | In-Place Reversal — Partial | Medium | ✅ |
| 34 | Reverse List in Pairs | 24 | In-Place Reversal — k=2 | Medium | ✅ |
| 35 | Reverse Every K-element Sub-list | 25 | In-Place Reversal — K-Group | Hard | ✅ |
| 36 | Reverse Nodes in Even Length Groups | 2074 | In-Place Reversal — Conditional | Hard | ✅ |
| 37 | Rotate a LinkedList | 61 | In-Place Reversal — Rotation | Medium | ✅ |
| 38 | Reverse Alternate K Elements | — | In-Place Reversal — Alternate K | Medium | ✅ |
| 39 | Palindrome LinkedList | 234 | In-Place Reversal — Tool usage | Easy | ✅ |
| 40 | LinkedList Cycle | 141 | Slow & Fast — Cycle Detection | Easy | ✅ |
| 41 | Start of LinkedList Cycle | 142 | Slow & Fast — Cycle Start | Medium | ✅ |
| 42 | Happy Number | 202 | Slow & Fast — Implicit Cycle | Medium | ✅ |
| 43 | Find the Duplicate Number | 287 | Slow & Fast — Implicit Cycle | Medium | ✅ |
| 44 | Middle of the LinkedList | 876 | Slow & Fast — Find Middle | Easy | ✅ |
| 45 | Palindrome LinkedList | 234 | Slow & Fast — Middle + Reverse | Medium | ✅ |
| 46 | Reorder List | 143 | Slow & Fast — Middle + Reverse + Merge | Medium | ✅ |
| 47 | Cycle in a Circular Array | 457 | Slow & Fast — Implicit Cycle (Array) | Hard | ✅ |
| 48 | Remove Nth Node From End | 19 | Slow & Fast — Gap Technique | Medium | ✅ |
| 49 | Intersection of Two Lists | 160 | Slow & Fast — Redirect Technique | Easy | ✅ |
| 50 | Binary Search | 704 | Binary Search — Basic | Easy | ✅ |
| 51 | Search Insert Position | 35 | Binary Search — Upper Bound | Easy | ✅ |
| 52 | First and Last Position | 34 | Binary Search — Boundary Search | Medium | ✅ |
| 53 | Count Occurrences in Sorted Array | — | Binary Search — Counting | Easy | ✅ |
| 54 | Search in Infinite Sorted Array | — | Binary Search — Exponential + BS | Medium | ✅ |
| 55 | Peak Index in Mountain Array | 852 | Binary Search — Bitonic | Easy | ✅ |
| 56 | Search in Bitonic Array | — | Binary Search — Bitonic | Medium | ✅ |
| 57 | Find Peak Element | 162 | Binary Search — Bitonic | Medium | ✅ |
| 58 | Find Minimum in Rotated Sorted Array | 153 | Binary Search — Range Search | Medium | ✅ |
| 59 | Find Number of Rotations | — | Binary Search — Range Search | Easy | ✅ |
| 60 | Search in Rotated Sorted Array | 33 | Binary Search — Range Search | Medium | ✅ |
| 61 | Find Min in Rotated II (Duplicates) | 154 | Binary Search — Range Search | Hard | ✅ |
| 62 | Search in Rotated II (Duplicates) | 81 | Binary Search — Range Search | Medium | ✅ |
| 63 | Single Element in Sorted Array | 540 | Binary Search — Parity | Medium | ✅ |
| 64 | Koko Eating Bananas | 875 | Binary Search — Allocate | Medium | ✅ |
| 65 | Min Days to Make M Bouquets | 1482 | Binary Search — Allocate | Medium | ✅ |
| 66 | Aggressive Cows | — | Binary Search — Allocate | Medium | ✅ |
| 67 | H-Index II | 275 | Binary Search — Allocate | Medium | ✅ |
| 68 | Maximum Candies to K Children | 2226 | Binary Search — Allocate | Medium | ✅ |
| 69 | Capacity to Ship in D Days | 1011 | Binary Search — Allocate | Medium | ✅ |
| 70 | Book Allocation Problem | — | Binary Search — Allocate | Hard | ✅ |
| 71 | Split Array Largest Sum | 410 | Binary Search — Allocate | Hard | ✅ |
| 72 | Minimum Speed to Arrive on Time | 1870 | Binary Search — Allocate | Medium | ✅ |
| 73 | Minimize Max Gas Station Distance | 774 | Binary Search — Allocate | Hard | ✅ |
| 74 | Search a 2D Matrix | 74 | Binary Search — 2D | Medium | ✅ |
| 75 | Search a 2D Matrix II | 240 | Binary Search — 2D (Staircase) | Medium | ✅ |
| 76 | Kth Smallest in Sorted Matrix | 378 | Binary Search — Kth Element | Medium | ✅ |
| 77 | Kth Smallest in Multiplication Table | 668 | Binary Search — Kth Element | Hard | ✅ |
| 78 | Median of Two Sorted Arrays | 4 | Binary Search — Partition | Hard | ✅ |
| 79 | Kth Missing Positive Number | 1539 | Binary Search — Missing Count | Easy | ✅ |
| 80 | Time Based Key-Value Store | 981 | Binary Search — FAANG | Medium | ✅ |
| 81 | Find K Closest Elements | 658 | Binary Search — FAANG | Medium | ✅ |

---

## ⚙️ Setup

```bash
# Clone the repo
git clone https://github.com/rahul22mrk/DSA-Interview-Notes-Java.git

# Navigate to any pattern
cd DSA-Interview-Notes-Java/03_Slow_And_Fast_Pointers_Pattern
cd DSA-Interview-Notes-Java/07_Stack_Pattern
cd DSA-Interview-Notes-Java/08_HashMap_Pattern
cd DSA-Interview-Notes-Java/09_In-Place_Reversal_LinkedList
cd DSA-Interview-Notes-Java/10_Binary_Search_Pattern
```

> **Java Version:** 11+

---

## 🤝 Contributing

Found a bug or want to add a pattern? Feel free to open a PR or raise an issue.

---

*Last updated: March 2026 · Maintained by [@rahul22mrk](https://github.com/rahul22mrk)*
