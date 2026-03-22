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
│   ├── 01_cyclic_sort_notes.md
│   └── 02_cyclic_sort_problems.md
│
├── 12_Heap_Pattern/
│   ├── 01_heap_notes.md
│   └── 02_heap_problems.md
│
├── 13_Recursion_And_Backtracking/
│   ├── 01_recursion_backtracking_notes.md
│   └── 02_recursion_backtracking_problems.md
│
├── 14_Trees_Pattern/
│   ├── 01_tree_notes.md
│   ├── 02_tree_problems.md
│   └── tree_traversal.md
│
├── 15_Graph_Pattern/
│   ├── 01_graph_notes.md
│   ├── 02_graph_problems.md
│   ├── 03_graph_beginners_problems.md
│   └── 04_graph_algorithms_quick_revision.md
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

### ✅ Cyclic Sort
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_cyclic_sort_notes.md](./11_Cyclic_Sort_Pattern/01_cyclic_sort_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_cyclic_sort_problems.md](./11_Cyclic_Sort_Pattern/02_cyclic_sort_problems.md) | Core Cyclic Sort | Cyclic Sort | Easy |
| [02_cyclic_sort_problems.md](./11_Cyclic_Sort_Pattern/02_cyclic_sort_problems.md) | Find Missing | Missing Number, All Missing Numbers, Smallest Missing Positive, First K Missing | Easy → Hard |
| [02_cyclic_sort_problems.md](./11_Cyclic_Sort_Pattern/02_cyclic_sort_problems.md) | Find Duplicate | Find Duplicate Number, All Duplicate Numbers | Easy → Medium |
| [02_cyclic_sort_problems.md](./11_Cyclic_Sort_Pattern/02_cyclic_sort_problems.md) | Combined Missing + Duplicate | Corrupt Pair, Set Mismatch | Easy |
| [02_cyclic_sort_problems.md](./11_Cyclic_Sort_Pattern/02_cyclic_sort_problems.md) | FAANG / Hard | Missing Number (XOR/Math), Disappeared Numbers, First Missing Positive | Easy → Hard |

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

### ✅ Heap / Priority Queue
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_heap_notes.md](./12_Heap_Pattern/01_heap_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_heap_problems.md](./12_Heap_Pattern/02_heap_problems.md) | Kth Element | Kth Largest Array, Kth Smallest Matrix, Kth Largest Stream, Kth Weakest Row | Easy → Medium |
| [02_heap_problems.md](./12_Heap_Pattern/02_heap_problems.md) | Top K | Top K Frequent Elements/Words, Sort by Freq, K Closest Points/Elements | Easy → Medium |
| [02_heap_problems.md](./12_Heap_Pattern/02_heap_problems.md) | Merge K Lists / Arrays | Merge K Lists, Merge K Arrays, K Pairs Smallest Sums, Smallest Range K Lists | Medium → Hard |
| [02_heap_problems.md](./12_Heap_Pattern/02_heap_problems.md) | Two Heaps (Median) | Find Median from Stream, Sliding Window Median | Hard |
| [02_heap_problems.md](./12_Heap_Pattern/02_heap_problems.md) | Greedy + Heap | Task Scheduler, Reorganize String, Last Stone Weight, IPO, Course Schedule III, Min Refuel Stops | Medium → Hard |
| [02_heap_problems.md](./12_Heap_Pattern/02_heap_problems.md) | Design Problems | Design Twitter, Food Rating System, Distant Barcodes | Medium |

---

### ✅ Recursion & Backtracking
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_recursion_backtracking_notes.md](./13_Recursion_And_Backtracking/01_recursion_backtracking_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_recursion_backtracking_problems.md](./13_Recursion_And_Backtracking/02_recursion_backtracking_problems.md) | Basic Recursive Functions | Fibonacci, Palindrome Check, Array Sorted, Sum Digits, Remove Char, Count Good Numbers | Easy → Medium |
| [02_recursion_backtracking_problems.md](./13_Recursion_And_Backtracking/02_recursion_backtracking_problems.md) | Divide & Conquer | Pow(x,n), Binary Search, Merge Sort, Max Subarray, Count Smaller, Reverse Pairs, Count Range Sum | Easy → Hard |
| [02_recursion_backtracking_problems.md](./13_Recursion_And_Backtracking/02_recursion_backtracking_problems.md) | Backtracking (Classic) | Subsets I/II, Permutations I/II, Combinations, Combination Sum I/II, Generate Parens, Phone Letters, Palindrome Partition | Medium |
| [02_recursion_backtracking_problems.md](./13_Recursion_And_Backtracking/02_recursion_backtracking_problems.md) | Backtracking (Hard / Grid) | N-Queens, Word Search, Sudoku Solver, Unique Paths III, Path with Max Gold | Medium → Hard |
| [02_recursion_backtracking_problems.md](./13_Recursion_And_Backtracking/02_recursion_backtracking_problems.md) | Recursive Search | Jump Game | Medium |

---

### ✅ Trees
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_tree_notes.md](./14_Trees_Pattern/01_tree_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_tree_problems.md](./14_Trees_Pattern/02_tree_problems.md) | Traversal | Inorder, Preorder, Postorder, Level Order, Zigzag, Level Order II | Easy → Medium |
| [02_tree_problems.md](./14_Trees_Pattern/02_tree_problems.md) | Mirror & Symmetry | Invert Tree, Symmetric Tree, Same Tree, Subtree, Flip Equivalent | Easy → Medium |
| [02_tree_problems.md](./14_Trees_Pattern/02_tree_problems.md) | Traversal & Search (BST) | Search BST, LCA BST, LCA Binary Tree, LCA Deepest Leaves, Find Mode, Two Sum IV, Kth Smallest | Easy → Medium |
| [02_tree_problems.md](./14_Trees_Pattern/02_tree_problems.md) | Validation & Properties | Min/Max Depth, Balanced, Diameter, Tilt, Completeness, Validate BST, Recover BST | Easy → Hard |
| [02_tree_problems.md](./14_Trees_Pattern/02_tree_problems.md) | Path Sum & Root to Leaf | Path Sum I/II/III, Sum Root to Leaf, Max Path Sum | Easy → Hard |
| [02_tree_problems.md](./14_Trees_Pattern/02_tree_problems.md) | Construction | Construct from Traversals (3 variants), Sorted Array/List to BST, Max BT, Construct BST from Preorder, Serialize/Deserialize | Medium → Hard |
| [02_tree_problems.md](./14_Trees_Pattern/02_tree_problems.md) | Extended BFS | Even Odd Tree, Reverse Odd Levels, Deepest Leaves Sum, Add One Row, Max Width, Distance K | Medium |
| [02_tree_problems.md](./14_Trees_Pattern/02_tree_problems.md) | Extended Root to Leaf | Binary Tree Paths, Smallest String Leaf, Insufficient Nodes, Pseudo-Palindromic Paths | Easy → Medium |
| [02_tree_problems.md](./14_Trees_Pattern/02_tree_problems.md) | Extended Ancestor & BST | Max Diff Node Ancestor, Kth Ancestor, Range Sum BST, Min Abs Diff BST, Insert BST | Easy → Hard |
| [tree_traversal.md](./14_Trees_Pattern/tree_traversal.md) | Traversal Quick Reference | DFS Iterative/Recursive, BFS, Side Views (Left/Right/Top/Bottom), Boundary | Reference |
| [tree_traversal.md](./14_Trees_Pattern/tree_traversal.md) | Traversal Quick Revision | DFS Iterative/Recursive, BFS, Side Views (Left/Right/Top/Bottom), Boundary Traversal | Reference |

---

### ✅ Graph
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_graph_notes.md](./15_Graph_Pattern/01_graph_notes.md) | Identification + All Algorithm Templates + Cheatsheet | — | Reference |
| [02_graph_problems.md](./15_Graph_Pattern/02_graph_problems.md) | BFS / DFS / Grid | Number of Islands, Friend Circles, Max Area, Surrounded Regions, Shortest Path Binary Matrix, Word Ladder, Path Min Effort, Swim in Water, Find Safe States, All Paths, Longest Increasing Path | Easy → Hard |
| [02_graph_problems.md](./15_Graph_Pattern/02_graph_problems.md) | Shortest Path (Dijkstra / BF / Floyd) | Network Delay Time, Cheapest Flights K Stops, Path Max Probability, Min Cost Reach Destination, Find City | Medium → Hard |
| [02_graph_problems.md](./15_Graph_Pattern/02_graph_problems.md) | Topological Sort | Course Schedule I/II/IV, Alien Dictionary, Sequence Reconstruction, Strange Printer II | Medium → Hard |
| [02_graph_problems.md](./15_Graph_Pattern/02_graph_problems.md) | Union Find | Redundant Connection I/II, Accounts Merge, Network Connected, Equality Equations, Min Cost Connect Points | Medium → Hard |
| [02_graph_problems.md](./15_Graph_Pattern/02_graph_problems.md) | Bipartite / Graph Coloring | Is Graph Bipartite, Possible Bipartition, Flower Planting, M-Coloring | Easy → Medium |
| [02_graph_problems.md](./15_Graph_Pattern/02_graph_problems.md) | MST (Kruskal / Prim) | Min Cost Connect Points, Connecting Cities, Min Cost Water, Connect Sticks | Medium → Hard |
| [03_graph_beginners_problems.md](./15_Graph_Pattern/03_graph_beginners_problems.md) | Beginners Guide — 30 Solved Problems | All patterns with approach table + code + dry run | Easy → Medium |
| [04_graph_algorithms_quick_revision.md](./15_Graph_Pattern/04_graph_algorithms_quick_revision.md) | Quick Revision — Dijkstra, BF, Floyd, Prim, Kruskal, DSU | Full Java implementations for interview revision | Medium → Hard |

---

### 🔜 Coming Soon

| Folder | Pattern | Key Topics |
|--------|---------|------------|
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

## ⚡ Graph — Quick Clue Detector

| If you see this in the question | Algorithm |
|---------------------------------|-----------|
| `"connected components / islands / provinces"` | DFS or BFS (visited array) / Union Find |
| `"flood fill / spreading / rotting oranges"` | Multi-source BFS (seed all sources first) |
| `"shortest path, no weights"` | BFS (level = distance) |
| `"shortest path, positive weights"` | Dijkstra (min-heap + stale check) |
| `"shortest path, negative weights / K stops"` | Bellman-Ford (relax V-1 times) |
| `"shortest path between ALL pairs"` | Floyd-Warshall (3 nested loops) |
| `"task ordering / course prerequisites"` | Topological Sort — Kahn's BFS |
| `"cycle in directed graph"` | DFS 3-color (0=unseen, 1=in-path, 2=done) |
| `"cycle in undirected graph / merge groups"` | Union Find |
| `"minimum cost to connect all nodes"` | Kruskal (sort edges + UF) / Prim |
| `"2-colorable / bipartite / possible bipartition"` | BFS 2-coloring (conflict = false) |
| `"DFS from boundary / enclosed region"` | DFS from border cells first, mark safe |
| `"find eventual safe states"` | DFS 3-color (safe = no cycle reachable) |
| `"all paths from source to target"` | DFS backtracking |
| `"O(1) space" + connectivity` | Union Find instead of visited array |

---

## ⚡ Recursion & Backtracking — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"all subsets / power set"` | Backtracking — add at every level, pass `i+1` |
| `"all permutations"` | Backtracking — `used[]` array, add at leaf |
| `"all combinations summing to target"` | Backtracking — subtract target, pass `i` for reuse |
| `"generate all valid parentheses"` | Backtracking — open/close count constraints |
| `"all palindrome partitions"` | Backtracking — try every split + isPalindrome |
| `"N-Queens / Sudoku / Word Search"` | Constraint Backtracking — place + isValid + undo |
| `"duplicates in input, unique results"` | Sort first + `if (i>start && nums[i]==nums[i-1]) skip` |
| `"can reuse same element"` | Pass `i` instead of `i+1` in backtrack call |
| `"Pow(x,n) / fast exponentiation"` | Divide & Conquer — split exponent in half |
| `"count inversions / reverse pairs"` | Modified Merge Sort — count during merge |
| `"sort or find range"` | Divide & Conquer — split + solve + merge |
| `"f(n) = f(n-1) + something simple"` | Basic Recursion — direct recurrence |

---

## ⚡ Trees — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"inorder / preorder / postorder traversal"` | DFS — recursive or iterative with stack |
| `"level order / BFS / row by row"` | BFS — queue + snapshot `size = q.size()` |
| `"zigzag / spiral level order"` | BFS + direction flag per level |
| `"invert / mirror binary tree"` | Swap left/right recursively |
| `"symmetric / same tree / subtree"` | Dual DFS — compare pair of nodes |
| `"lowest common ancestor"` | Post-order DFS — both sides non-null → LCA |
| `"LCA of BST"` | BST property — both smaller → left, both larger → right |
| `"validate BST"` | Top-down bounds — pass (min, max) as Long |
| `"Kth smallest in BST"` | Inorder traversal = sorted order |
| `"recover BST"` | Find two out-of-order nodes in inorder |
| `"path sum root to leaf"` | Top-down DFS — pass remaining sum |
| `"path sum any node to any node"` | Prefix sum + HashMap + backtrack |
| `"maximum path sum"` | Bottom-up + global max — ignore negatives |
| `"diameter of binary tree"` | Bottom-up + global — L+R at each node |
| `"balanced binary tree"` | Bottom-up — return -1 on imbalance |
| `"construct tree from traversals"` | Divide & conquer — HashMap for inorder index |
| `"serialize / deserialize tree"` | Preorder DFS + null markers |
| `"convert sorted array/list to BST"` | Binary mid as root, recurse halves |

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

## ⚡ Cyclic Sort — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"array of n integers in range [1, n]"` | Cyclic Sort — place at index `nums[i]-1` |
| `"find the missing number"` | Cyclic sort → first `nums[i] != i+1` → `i+1` |
| `"find all missing numbers"` | Cyclic sort → collect all mismatches |
| `"find the duplicate number"` | Cyclic sort → `nums[i]==nums[home]` → return it |
| `"find all duplicates"` | Cyclic sort → collect `nums[i]` at mismatches |
| `"corrupt pair / missing and duplicate"` | Cyclic sort → `[nums[i], i+1]` at mismatch |
| `"smallest missing positive"` | Cyclic sort with range guard `[1,n]` |
| `"first k missing positives"` | Sort + scan + extend beyond n |
| `"O(n) time O(1) space" + range-constrained array` | Cyclic sort — use indices as HashMap |
| `"in-place" + range [1,n]` | Each number's home is `nums[i]-1` |

---

## ⚡ Heap / Priority Queue — Quick Clue Detector

| If you see this in the question | Pattern |
|---------------------------------|---------|
| `"Kth largest / smallest"` | Min-heap (Kth largest) or Max-heap (Kth smallest) of size k |
| `"top K frequent / closest / heaviest"` | Freq/dist map + min-heap size k |
| `"merge K sorted lists / arrays"` | Min-heap as pointer — (val, listIdx, elemIdx) |
| `"find median from data stream"` | Two heaps — maxHeap(lower) + minHeap(upper) |
| `"sliding window median"` | Two heaps + lazy deletion |
| `"task scheduler / reorganize string"` | Max-heap by frequency, greedy alternation |
| `"maximize profit with capital constraint"` | Sort by capital + max-heap for profit (IPO) |
| `"course schedule with deadline"` | Sort by deadline + max-heap, replace longest |
| `"minimum refueling stops"` | Greedy + max-heap — retroactive best station |
| `"K pairs with smallest sums"` | Min-heap expand (i, j+1) after each pop |
| `"smallest range covering K lists"` | Min-heap + track current max |
| `"design Twitter / leaderboard / feed"` | Per-entity heap or top-k with max-heap |
| `"O(n log k)" + top/bottom selection` | Heap of size k beats full sort |

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
| 196 | Cyclic Sort | — | Cyclic Sort — Core | Easy | ✅ |
| 197 | Find the Missing Number | 268 | Cyclic Sort — Missing | Easy | ✅ |
| 198 | Find All Missing Numbers | 448 | Cyclic Sort — All Missing | Easy | ✅ |
| 199 | Find the Duplicate Number | 287 | Cyclic Sort — Duplicate | Medium | ✅ |
| 200 | Find All Duplicate Numbers | 442 | Cyclic Sort — All Duplicates | Medium | ✅ |
| 201 | Find the Corrupt Pair | — | Cyclic Sort — Combined | Easy | ✅ |
| 202 | Smallest Missing Positive Number | 41 | Cyclic Sort — Missing Positive | Hard | ✅ |
| 203 | First K Missing Positive Numbers | — | Cyclic Sort — K Missing | Hard | ✅ |
| 204 | Set Mismatch | 645 | Cyclic Sort — Combined | Easy | ✅ |
| 205 | Find All Numbers Disappeared | 448 | Cyclic Sort — All Missing | Easy | ✅ |
| 206 | First Missing Positive | 41 | Cyclic Sort — Missing Positive | Hard | ✅ |
| 207 | Missing Number (XOR/Math) | 268 | Cyclic Sort — Missing (Multi-approach) | Easy | ✅ |
| 208 | Kth Largest Element in an Array | 215 | Heap — Kth Element | Medium | ✅ |
| 209 | Kth Smallest Element in Sorted Matrix | 378 | Heap — Kth Element | Medium | ✅ |
| 210 | Kth Largest Element in a Stream | 703 | Heap — Kth Element Design | Easy | ✅ |
| 211 | Kth Weakest Row in a Matrix | 1337 | Heap — Kth Element | Easy | ✅ |
| 212 | Top K Frequent Elements | 347 | Heap — Top K | Medium | ✅ |
| 213 | Top K Frequent Words | 692 | Heap — Top K | Medium | ✅ |
| 214 | Sort Characters By Frequency | 451 | Heap — Top K | Medium | ✅ |
| 215 | K Closest Points to Origin | 973 | Heap — Top K | Medium | ✅ |
| 216 | Find K Closest Elements | 658 | Heap — Top K | Medium | ✅ |
| 217 | Merge K Sorted Lists | 23 | Heap — Merge K | Hard | ✅ |
| 218 | Merge K Sorted Arrays | — | Heap — Merge K | Medium | ✅ |
| 219 | K Pairs with Smallest Sums | 373 | Heap — Merge K | Medium | ✅ |
| 220 | Smallest Range Covering K Lists | 632 | Heap — Merge K | Hard | ✅ |
| 221 | Find Median from Data Stream | 295 | Heap — Two Heaps | Hard | ✅ |
| 222 | Sliding Window Median | 480 | Heap — Two Heaps | Hard | ✅ |
| 223 | Task Scheduler | 621 | Heap — Greedy | Medium | ✅ |
| 224 | Reorganize String | 767 | Heap — Greedy | Medium | ✅ |
| 225 | Last Stone Weight | 1046 | Heap — Greedy | Easy | ✅ |
| 226 | IPO | 502 | Heap — Greedy | Hard | ✅ |
| 227 | Course Schedule III | 630 | Heap — Greedy | Hard | ✅ |
| 228 | Minimum Number of Refueling Stops | 871 | Heap — Greedy | Hard | ✅ |
| 229 | Design Twitter | 355 | Heap — Design | Medium | ✅ |
| 230 | Design Food Rating System | 2353 | Heap — Design | Medium | ✅ |
| 231 | Distant Barcodes | 1054 | Heap — Greedy | Medium | ✅ |
| 232 | Sort Array by Frequency | 1636 | Heap — Top K | Easy | ✅ |
| 233 | Binary Tree Inorder Traversal | 94 | Tree — Traversal | Easy | ✅ |
| 234 | Binary Tree Preorder Traversal | 144 | Tree — Traversal | Easy | ✅ |
| 235 | Binary Tree Postorder Traversal | 145 | Tree — Traversal | Easy | ✅ |
| 236 | Binary Tree Level Order Traversal | 102 | Tree — BFS | Medium | ✅ |
| 237 | Binary Tree Zigzag Level Order | 103 | Tree — BFS | Medium | ✅ |
| 238 | Binary Tree Level Order Traversal II | 107 | Tree — BFS | Easy | ✅ |
| 239 | Invert Binary Tree | 226 | Tree — Mirror | Easy | ✅ |
| 240 | Symmetric Tree | 101 | Tree — Symmetry | Easy | ✅ |
| 241 | Same Tree | 100 | Tree — Comparison | Easy | ✅ |
| 242 | Subtree of Another Tree | 572 | Tree — Comparison | Medium | ✅ |
| 243 | Flip Equivalent Binary Trees | 951 | Tree — Mirror | Medium | ✅ |
| 244 | Search in a Binary Search Tree | 700 | Tree — BST Search | Easy | ✅ |
| 245 | Lowest Common Ancestor of BST | 235 | Tree — BST LCA | Medium | ✅ |
| 246 | Lowest Common Ancestor of Binary Tree | 236 | Tree — LCA | Medium | ✅ |
| 247 | LCA of Deepest Leaves | 1123 | Tree — LCA | Medium | ✅ |
| 248 | Find Mode in BST | 501 | Tree — BST Traversal | Easy | ✅ |
| 249 | Two Sum IV — BST | 653 | Tree — BST Search | Easy | ✅ |
| 250 | Kth Smallest Element in BST | 230 | Tree — BST Inorder | Medium | ✅ |
| 251 | Minimum Depth of Binary Tree | 111 | Tree — Depth | Easy | ✅ |
| 252 | Maximum Depth of Binary Tree | 104 | Tree — Depth | Easy | ✅ |
| 253 | Balanced Binary Tree | 110 | Tree — Validation | Easy | ✅ |
| 254 | Diameter of Binary Tree | 543 | Tree — Properties | Easy | ✅ |
| 255 | Binary Tree Tilt | 563 | Tree — Properties | Easy | ✅ |
| 256 | Check Completeness of Binary Tree | 958 | Tree — Validation | Medium | ✅ |
| 257 | Validate Binary Search Tree | 98 | Tree — BST Validation | Medium | ✅ |
| 258 | Recover Binary Search Tree | 99 | Tree — BST Recovery | Hard | ✅ |
| 259 | Path Sum | 112 | Tree — Path Sum | Easy | ✅ |
| 260 | Path Sum II | 113 | Tree — Path Sum | Medium | ✅ |
| 261 | Path Sum III | 437 | Tree — Path Sum | Medium | ✅ |
| 262 | Sum Root to Leaf Numbers | 129 | Tree — Path Sum | Medium | ✅ |
| 263 | Binary Tree Maximum Path Sum | 124 | Tree — Path Sum | Hard | ✅ |
| 264 | Construct BT from Preorder and Inorder | 105 | Tree — Construction | Medium | ✅ |
| 265 | Construct BT from Inorder and Postorder | 106 | Tree — Construction | Medium | ✅ |
| 266 | Construct BT from Preorder and Postorder | 889 | Tree — Construction | Medium | ✅ |
| 267 | Convert Sorted Array to BST | 108 | Tree — Construction | Easy | ✅ |
| 268 | Convert Sorted List to BST | 109 | Tree — Construction | Medium | ✅ |
| 269 | Serialize and Deserialize Binary Tree | 297 | Tree — Serialization | Hard | ✅ |
| 270 | Even Odd Tree | 1609 | Tree — BFS | Medium | ✅ |
| 271 | Reverse Odd Levels of Binary Tree | 2415 | Tree — BFS | Medium | ✅ |
| 272 | Deepest Leaves Sum | 1302 | Tree — BFS | Medium | ✅ |
| 273 | Add One Row to Tree | 623 | Tree — BFS | Medium | ✅ |
| 274 | Maximum Width of Binary Tree | 662 | Tree — BFS | Medium | ✅ |
| 275 | All Nodes Distance K in Binary Tree | 863 | Tree — BFS + Graph | Medium | ✅ |
| 276 | Maximum Binary Tree | 654 | Tree — Construction | Medium | ✅ |
| 277 | Construct BST from Preorder Traversal | 1008 | Tree — Construction | Medium | ✅ |
| 278 | Binary Tree Paths | 257 | Tree — Root to Leaf | Easy | ✅ |
| 279 | Smallest String Starting from Leaf | 988 | Tree — Root to Leaf | Medium | ✅ |
| 280 | Insufficient Nodes in Root to Leaf | 1080 | Tree — Root to Leaf | Medium | ✅ |
| 281 | Pseudo-Palindromic Paths in Binary Tree | 1457 | Tree — Root to Leaf | Medium | ✅ |
| 282 | Maximum Difference Between Node and Ancestor | 1026 | Tree — Ancestor | Medium | ✅ |
| 283 | Kth Ancestor of a Tree Node | 1483 | Tree — Ancestor | Hard | ✅ |
| 284 | Range Sum of BST | 938 | Tree — BST | Easy | ✅ |
| 285 | Minimum Absolute Difference in BST | 530 | Tree — BST Inorder | Easy | ✅ |
| 286 | Insert into a BST | 701 | Tree — BST Insert | Medium | ✅ |
| 287 | Fibonacci Number | 509 | Recursion — Basic | Easy | ✅ |
| 288 | Check if String is Palindrome | — | Recursion — Basic | Easy | ✅ |
| 289 | Check if Array is Sorted | — | Recursion — Basic | Easy | ✅ |
| 290 | Sum of Digits of a Number | — | Recursion — Basic | Easy | ✅ |
| 291 | Remove Occurrences of a Character | — | Recursion — Basic | Easy | ✅ |
| 292 | Count Good Numbers | 1922 | Recursion — Basic | Medium | ✅ |
| 293 | Pow(x, n) | 50 | Recursion — D&C | Medium | ✅ |
| 294 | Binary Search (Recursive) | 704 | Recursion — D&C | Easy | ✅ |
| 295 | Merge Sort | — | Recursion — D&C | Medium | ✅ |
| 296 | Maximum Subarray (D&C) | 53 | Recursion — D&C | Medium | ✅ |
| 297 | Count Smaller Numbers After Self | 315 | Recursion — D&C | Hard | ✅ |
| 298 | Reverse Pairs | 493 | Recursion — D&C | Hard | ✅ |
| 299 | Count of Range Sum | 327 | Recursion — D&C | Hard | ✅ |
| 300 | Subsets | 78 | Backtracking — Subsets | Medium | ✅ |
| 301 | Subsets II | 90 | Backtracking — Subsets | Medium | ✅ |
| 302 | Permutations | 46 | Backtracking — Permutations | Medium | ✅ |
| 303 | Permutations II | 47 | Backtracking — Permutations | Medium | ✅ |
| 304 | Combinations | 77 | Backtracking — Combinations | Medium | ✅ |
| 305 | Combination Sum | 39 | Backtracking — Combinations | Medium | ✅ |
| 306 | Combination Sum II | 40 | Backtracking — Combinations | Medium | ✅ |
| 307 | Generate Parentheses | 22 | Backtracking — String | Medium | ✅ |
| 308 | Letter Combinations of a Phone Number | 17 | Backtracking — String | Medium | ✅ |
| 309 | Palindrome Partitioning | 131 | Backtracking — String | Medium | ✅ |
| 310 | Split String | — | Backtracking — String | Medium | ✅ |
| 311 | N-Queens | 51 | Backtracking — Hard | Hard | ✅ |
| 312 | Word Search | 79 | Backtracking — Grid | Medium | ✅ |
| 313 | Sudoku Solver | 37 | Backtracking — Hard | Hard | ✅ |
| 314 | Unique Paths III | 980 | Backtracking — Grid | Hard | ✅ |
| 315 | Path with Maximum Gold | 1219 | Backtracking — Grid | Medium | ✅ |
| 316 | Jump Game | 55 | Recursive Search | Medium | ✅ |
| 317 | Number of Islands | 200 | Graph — DFS/BFS | Medium | ✅ |
| 318 | Friend Circles (Number of Provinces) | 547 | Graph — DFS/UF | Medium | ✅ |
| 319 | Max Area of Island | 695 | Graph — DFS | Medium | ✅ |
| 320 | Surrounded Regions | 130 | Graph — DFS Boundary | Medium | ✅ |
| 321 | Shortest Path in Binary Matrix | 1091 | Graph — BFS | Medium | ✅ |
| 322 | Word Ladder | 127 | Graph — BFS | Hard | ✅ |
| 323 | Path with Minimum Effort | 1631 | Graph — Dijkstra | Medium | ✅ |
| 324 | Swim in Rising Water | 778 | Graph — Dijkstra | Hard | ✅ |
| 325 | Find Eventual Safe States | 802 | Graph — DFS Cycle | Medium | ✅ |
| 326 | All Paths Source to Target | 797 | Graph — DFS | Medium | ✅ |
| 327 | Longest Increasing Path in Matrix | 329 | Graph — DFS + Memo | Hard | ✅ |
| 328 | Network Delay Time | 743 | Graph — Dijkstra | Medium | ✅ |
| 329 | Cheapest Flights Within K Stops | 787 | Graph — Bellman-Ford | Medium | ✅ |
| 330 | Path with Maximum Probability | 1514 | Graph — Dijkstra | Medium | ✅ |
| 331 | Find the City (Smallest Neighbours) | 1334 | Graph — Floyd-Warshall | Medium | ✅ |
| 332 | Course Schedule | 207 | Graph — Topological Sort | Medium | ✅ |
| 333 | Course Schedule II | 210 | Graph — Topological Sort | Medium | ✅ |
| 334 | Course Schedule IV | 1462 | Graph — Topological Sort | Medium | ✅ |
| 335 | Alien Dictionary | 269 | Graph — Topological Sort | Hard | ✅ |
| 336 | Sequence Reconstruction | 444 | Graph — Topological Sort | Medium | ✅ |
| 337 | Redundant Connection | 684 | Graph — Union Find | Medium | ✅ |
| 338 | Redundant Connection II | 685 | Graph — Union Find | Hard | ✅ |
| 339 | Accounts Merge | 721 | Graph — Union Find | Medium | ✅ |
| 340 | Number of Operations — Network | 1319 | Graph — Union Find | Medium | ✅ |
| 341 | Satisfiability of Equality Equations | 990 | Graph — Union Find | Medium | ✅ |
| 342 | Min Cost to Connect All Points | 1584 | Graph — Kruskal / Prim | Medium | ✅ |
| 343 | Connecting Cities with Min Cost | 1135 | Graph — Kruskal | Medium | ✅ |
| 344 | Is Graph Bipartite? | 785 | Graph — BFS Coloring | Medium | ✅ |
| 345 | Possible Bipartition | 886 | Graph — BFS Coloring | Medium | ✅ |
| 346 | Flower Planting With No Adjacent | 1042 | Graph — Greedy Coloring | Easy | ✅ |
| 347 | M-Coloring Problem | — | Graph — Backtracking | Medium | ✅ |
| 348 | Min Cost to Provide Water | 1168 | Graph — Kruskal | Hard | ✅ |
| 349 | Minimum Obstacle Removal | 2290 | Graph — 0-1 BFS | Hard | ✅ |
| 350 | Minimum Moves to Move Box | 1263 | Graph — BFS (states) | Hard | ✅ |
| 351 | Minimum Cost Reach Destination in Time | 1928 | Graph — Dijkstra | Hard | ✅ |
| 352 | Connect Sticks (Min Cost) | 1167 | Graph — Greedy Heap | Medium | ✅ |
| 353 | Longest Path in DAG | — | Graph — Topo Sort + DP | Medium | ✅ |
| 354 | Number of Enclaves | 1020 | Graph — DFS Boundary | Medium | ✅ |
| 355 | Time to Inform All Employees | 1376 | Graph — DFS | Medium | ✅ |
| 356 | 01 Matrix | 542 | Graph — Multi-source BFS | Medium | ✅ |
| 357 | Rotting Oranges | 994 | Graph — Multi-source BFS | Medium | ✅ |
| 358 | As Far from Land as Possible | 1162 | Graph — Multi-source BFS | Medium | ✅ |
| 359 | Most Stones Removed | 947 | Graph — Union Find | Medium | ✅ |
| 360 | Strange Printer II | 1591 | Graph — Topological Sort | Hard | ✅ |
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
cd DSA-Interview-Notes-Java/11_Cyclic_Sort_Pattern
cd DSA-Interview-Notes-Java/12_Heap_Pattern
cd DSA-Interview-Notes-Java/13_Recursion_And_Backtracking
cd DSA-Interview-Notes-Java/14_Trees_Pattern
cd DSA-Interview-Notes-Java/15_Graph_Pattern

# Coming soon
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
