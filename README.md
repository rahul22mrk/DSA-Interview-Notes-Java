<div align="center">

# 📚 DSA Interview Notes — Java

**Pattern-wise DSA prep · Interview-focused · Clean Java templates · MAANG-ready**

<br>

![Problems](https://img.shields.io/badge/Problems-398-4f9cf9?style=for-the-badge)
![Patterns](https://img.shields.io/badge/Patterns-16-7c5cfc?style=for-the-badge)
![Language](https://img.shields.io/badge/Language-Java-f97316?style=for-the-badge&logo=java)
![Level](https://img.shields.io/badge/Level-MAANG_Ready-22c55e?style=for-the-badge)

<br>

| 🟢 Easy | 🟡 Medium | 🔴 Hard | Total |
|---------|-----------|---------|-------|
| 90 | 236 | 72 | **398** |

</div>

---

## 📑 Table of Contents

| | Section |
|--|---------|
| [🧩](#-patterns-covered) | Patterns Covered (16 patterns) |
| [📊](#-problems-index) | Problems Index (398 problems) |
| [⚡](#-quick-clue-detector) | Quick Clue Detector |
| [📁](#-repository-structure) | Repository Structure |
| [📖](#-how-to-use) | How to Use |
| [🔗](#-resources) | Resources |

---

## 🧩 Patterns Covered

> Each pattern → **notes file** (theory + templates) + **problems file** (solved problems with approach tables + examples).


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

---


### ✅ Dynamic Programming
| File | Sub-Pattern | Problems | Difficulty |
|------|------------|----------|------------|
| [01_dp_notes.md](./16_Dynamic_Programming_Pattern/01_dp_notes.md) | Identification + Templates + Cheatsheet | — | Reference |
| [02_dp_problems.md](./16_Dynamic_Programming_Pattern/02_dp_problems.md) | Fibonacci / Decision Making | House Robber, Maximum Subarray, Decode Ways | Easy → Medium |
| [02_dp_problems.md](./16_Dynamic_Programming_Pattern/02_dp_problems.md) | Min/Max Path to Target | Coin Change, Min Path Sum, Min Falling Path Sum, Unique Paths | Medium |
| [02_dp_problems.md](./16_Dynamic_Programming_Pattern/02_dp_problems.md) | 0/1 Knapsack | 0/1 Knapsack, Partition Equal Subset Sum, Target Sum, Ones and Zeroes, Last Stone Weight II | Medium |
| [02_dp_problems.md](./16_Dynamic_Programming_Pattern/02_dp_problems.md) | Unbounded Knapsack | Coin Change II, Count Numbers with Unique Digits | Medium |
| [02_dp_problems.md](./16_Dynamic_Programming_Pattern/02_dp_problems.md) | LIS / Subsequences | LIS, Count Palindromic Subsequences | Medium → Hard |
| [02_dp_problems.md](./16_Dynamic_Programming_Pattern/02_dp_problems.md) | DP on Strings | LCS, Edit Distance, LPS, Distinct Subsequences | Medium → Hard |
| [02_dp_problems.md](./16_Dynamic_Programming_Pattern/02_dp_problems.md) | Interval DP | Burst Balloons, Min Cost Cut Stick, MCM, Strange Printer, Merge Stones, Remove Boxes | Hard |
| [02_dp_problems.md](./16_Dynamic_Programming_Pattern/02_dp_problems.md) | Probability / Expectation DP | Knight Probability, Dice Roll Simulation, Soup Servings, New 21 Game | Medium |
| [03_dp_patterns_level1.md](./16_Dynamic_Programming_Pattern/03_dp_patterns_level1.md) | Level 1 Extended (48 problems) | Stocks, Grid DP, All Knapsack variants, All LCS/LIS variants | Easy → Hard |
| [04_dp_patterns_level2.md](./16_Dynamic_Programming_Pattern/04_dp_patterns_level2.md) | Level 2 Advanced (30 problems) | Interval DP, Tree DP, Digit DP, Bitmask DP, Probability DP | Hard |

---

---

### 🔜 Coming Soon

| Folder | Pattern | Key Topics |
|--------|---------|------------|
| `17_Trie_Pattern` | Trie | Insert/Search/Delete, Word search II, Auto-complete, Replace words |
| `18_Bit_Manipulation_Pattern` | Bit Manipulation | XOR tricks, Count bits, Power of two, Subsets via bits, Single number |


---


## 📊 Problems Index

> Full sortable list → **[PROBLEMS_INDEX.md](./PROBLEMS_INDEX.md)**

<details>
<summary><b>📈 Problems by Pattern — click to expand</b></summary>

| Pattern | Total | 🟢 Easy | 🟡 Medium | 🔴 Hard |
|---------|-------|---------|-----------|---------|
| 🌲 Tree | 54 | 20 | 29 | 5 |
| 🕸️ Graph | 44 | 2 | 32 | 10 |
| 🧮 Dynamic Programming | 38 | 3 | 26 | 9 |
| 🔍 Binary Search | 32 | 8 | 18 | 6 |
| 📚 Stack | 32 | 7 | 18 | 7 |
| ⛰️ Heap / Priority Queue | 25 | 5 | 14 | 6 |
| 💃 Slow & Fast Pointers | 23 | 6 | 17 | 0 |
| 🪟 Sliding Window | 21 | 2 | 17 | 2 |
| 👆 Two Pointers | 20 | 8 | 10 | 2 |
| 🗺️ HashMap | 16 | 8 | 7 | 1 |
| ↩️ Backtracking | 16 | 0 | 11 | 5 |
| 🔄 In-Place Reversal | 14 | 3 | 10 | 1 |
| ↩️ Recursion | 13 | 5 | 6 | 2 |
| 🔀 Merge Intervals | 13 | 1 | 9 | 3 |
| ∑ Prefix Sum | 12 | 2 | 7 | 3 |
| 📈 Kadane | 12 | 2 | 7 | 3 |
| 🔁 Cyclic Sort | 12 | 6 | 3 | 3 |
| **Total** | **398** | **90** | **236** | **72** |

</details>

<details>
<summary><b>🔢 First 50 Problems — click to expand</b></summary>

| # | Problem | LC# | Pattern | Diff |
|---|---------|-----|---------|------|
| 1 | Pair with Target Sum (2Sum II) | 167 | Two Pointers | 🟢 |
| 2 | Remove Duplicates from Sorted Array | 26 | Two Pointers | 🟢 |
| 3 | Squaring a Sorted Array | 977 | Two Pointers | 🟢 |
| 4 | Triplet Sum to Zero (3Sum) | 15 | Two Pointers | 🟡 |
| 5 | Triplet Sum Close to Target | 16 | Two Pointers | 🟡 |
| 6 | Dutch National Flag (Sort Colors) | 75 | Two Pointers | 🟡 |
| 7 | Backspace String Compare | 844 | Two Pointers | 🟢 |
| 8 | Trapping Rain Water | 42 | Two Pointers | 🔴 |
| 9 | Container With Most Water | 11 | Two Pointers | 🟡 |
| 10 | 4Sum | 18 | Two Pointers | 🟡 |
| 11 | Max Sum Subarray of Size K | — | Sliding Window | 🟢 |
| 12 | Smallest Subarray with Sum ≥ S | 209 | Sliding Window | 🟡 |
| 13 | Longest Substring with K Distinct | 340 | Sliding Window | 🟡 |
| 14 | Minimum Window Substring | 76 | Sliding Window | 🔴 |
| 15 | Find All Anagrams in a String | 438 | Sliding Window | 🟡 |
| 16 | Sliding Window Maximum | 239 | Sliding Window | 🔴 |
| 17 | Linked List Cycle | 141 | Slow & Fast | 🟢 |
| 18 | Cycle Start | 142 | Slow & Fast | 🟡 |
| 19 | Happy Number | 202 | Slow & Fast | 🟢 |
| 20 | Middle of Linked List | 876 | Slow & Fast | 🟢 |
| 21 | Find Duplicate Number (Floyd) | 287 | Slow & Fast | 🟡 |
| 22 | Max Sum Subarray (Kadane) | 53 | Kadane | 🟢 |
| 23 | Best Time to Buy Stock I | 121 | Kadane | 🟢 |
| 24 | Best Time II (unlimited) | 122 | Kadane | 🟡 |
| 25 | Best Time III (2 transactions) | 123 | Kadane | 🔴 |
| 26 | Best Time IV (k transactions) | 188 | Kadane | 🔴 |
| 27 | Range Sum Query - Immutable | 303 | Prefix Sum | 🟢 |
| 28 | Subarray Sum Equals K | 560 | Prefix Sum | 🟡 |
| 29 | Subarray Sums Divisible by K | 974 | Prefix Sum | 🟡 |
| 30 | Merge Intervals | 56 | Merge Interval | 🟡 |
| 31 | Insert Interval | 57 | Merge Interval | 🟡 |
| 32 | Minimum Meeting Rooms | 253 | Merge Interval | 🔴 |
| 33 | Employee Free Time | 759 | Merge Interval | 🔴 |
| 34 | Next Greater Element I | 496 | Stack | 🟢 |
| 35 | Daily Temperatures | 739 | Stack | 🟡 |
| 36 | Largest Rectangle in Histogram | 84 | Stack | 🔴 |
| 37 | Valid Parentheses | 20 | Stack | 🟢 |
| 38 | Min Stack | 155 | Stack | 🟡 |
| 39 | Two Sum | 1 | HashMap | 🟢 |
| 40 | Group Anagrams | 49 | HashMap | 🟡 |
| 41 | LRU Cache | 146 | HashMap | 🟡 |
| 42 | Reverse a LinkedList | 206 | In-Place Reversal | 🟢 |
| 43 | Reverse K-Group | 25 | In-Place Reversal | 🔴 |
| 44 | Binary Search | 704 | Binary Search | 🟢 |
| 45 | Search in Rotated Array | 33 | Binary Search | 🟡 |
| 46 | Median of Two Sorted Arrays | 4 | Binary Search | 🔴 |
| 47 | Cyclic Sort | — | Cyclic Sort | 🟢 |
| 48 | Find the Missing Number | 268 | Cyclic Sort | 🟢 |
| 49 | Find the Duplicate Number | 287 | Cyclic Sort | 🟡 |
| 50 | First Missing Positive | 41 | Cyclic Sort | 🔴 |

> 📄 Full 398 problems → **[PROBLEMS_INDEX.md](./PROBLEMS_INDEX.md)**

</details>

---

## ⚡ Quick Clue Detector

> Read the problem → spot these keywords → know the pattern instantly.

<details>
<summary><b>👆 Two Pointers</b></summary>

| If you see this... | Pattern |
|--------------------|---------|
| `"find pair/triplet with sum"` | Both-ends — start from both sides |
| `"remove duplicates in-place"` | Same-direction — fast pointer skips |
| `"partition around pivot"` | Dutch flag — three-pointer |
| `"sorted array, maximize/minimize"` | Both-ends sweep |
| `"in-place O(1) space"` | Pointer manipulation, no extra array |

</details>

<details>
<summary><b>🪟 Sliding Window</b></summary>

| If you see this... | Pattern |
|--------------------|---------|
| `"longest/shortest subarray with condition"` | Variable window — shrink when violated |
| `"subarray of fixed size k"` | Fixed window — slide by 1 |
| `"at most k distinct characters"` | Frequency map + shrink when > k |
| `"minimum window containing all"` | Variable — expand then shrink |
| `"all anagrams / permutations in string"` | Fixed window + frequency compare |

</details>

<details>
<summary><b>🗺️ HashMap</b></summary>

| If you see this... | Pattern |
|--------------------|---------|
| `"two numbers that sum to target"` | Complement lookup — `containsKey(target-x)` |
| `"count occurrences / frequency"` | Frequency map — `getOrDefault(x,0)+1` |
| `"group / classify / anagram"` | Bucketing — `computeIfAbsent(key, ...)` |
| `"subarray with sum k"` | Prefix sum map — `put(0,1); get(prefix-k)` |
| `"isomorphic / pattern match"` | Two-map bidirectional |
| `"LRU cache / evict least recently used"` | LinkedHashMap or HashMap + DLL |

</details>

<details>
<summary><b>🔍 Binary Search</b></summary>

| If you see this... | Pattern |
|--------------------|---------|
| `"sorted array, find target"` | Classic `lo+(hi-lo)/2` |
| `"rotated sorted array"` | Find pivot, search correct half |
| `"find minimum in rotated"` | Check which half is sorted |
| `"minimize max / maximize min"` | Binary search on answer + feasibility check |
| `"first/last position of element"` | `lo=mid+1` or `hi=mid` variant |

</details>

<details>
<summary><b>🧮 Dynamic Programming</b></summary>

| If you see this... | Pattern |
|--------------------|---------|
| `"max/min way to reach target"` | Min/Max path — `dp[i]=best(dp[i-way]+cost)` |
| `"count ways / how many ways"` | Counting DP — `dp[i]+=dp[i-way]`, `dp[0]=1` |
| `"each item used at most once"` | 0/1 Knapsack — **REVERSE** capacity loop |
| `"items reusable / unlimited supply"` | Unbounded Knapsack — **FORWARD** loop |
| `"two strings — match / edit / common"` | 2D `dp[i][j]` on strings |
| `"longest increasing subsequence"` | LIS — `dp[i]=max(dp[j]+1)` or O(n log n) |
| `"split interval [i..j] at point k"` | Interval DP — loop by LENGTH then k |
| `"buy/sell stock with cooldown/fee"` | State machine — hold/notHold states |

</details>

<details>
<summary><b>🌲 Trees</b></summary>

| If you see this... | Pattern |
|--------------------|---------|
| `"inorder/preorder/postorder"` | DFS — recursive or iterative with stack |
| `"level order / BFS"` | BFS — queue + snapshot `size=q.size()` |
| `"lowest common ancestor"` | Post-order — both sides non-null → LCA |
| `"path sum root to leaf"` | Top-down DFS — pass remaining sum |
| `"maximum path sum any node"` | Bottom-up + global max — ignore negatives |
| `"validate BST"` | Top-down bounds — pass `(min,max)` as Long |
| `"construct tree from traversals"` | Divide & conquer — HashMap for inorder index |

</details>

<details>
<summary><b>🕸️ Graph</b></summary>

| If you see this... | Pattern |
|--------------------|---------|
| `"islands / connected components"` | BFS or DFS flood fill |
| `"shortest path unweighted"` | BFS — level = distance |
| `"shortest path weighted"` | Dijkstra (non-negative) or Bellman-Ford |
| `"cycle detection directed graph"` | DFS with WHITE/GRAY/BLACK coloring |
| `"topological sort / course schedule"` | Kahn's BFS (in-degree) or DFS post-order |
| `"union find / connected groups"` | DSU with path compression + union by rank |
| `"minimum spanning tree"` | Kruskal (sort edges) or Prim (min-heap) |

</details>

<details>
<summary><b>⛰️ Heap / Priority Queue</b></summary>

| If you see this... | Pattern |
|--------------------|---------|
| `"Kth largest / smallest"` | Min-heap size k — `peek()` = kth largest |
| `"top K frequent / closest"` | Freq/dist map + min-heap size k |
| `"merge K sorted lists/arrays"` | Min-heap as pointer — `(val, listIdx, elemIdx)` |
| `"find median from stream"` | Two heaps — maxHeap(lower) + minHeap(upper) |
| `"task scheduler / reorganize string"` | Max-heap by frequency, greedy alternation |

</details>

<details>
<summary><b>📚 Stack · ↩️ Backtracking · 🔄 In-Place Reversal · 🔁 Cyclic Sort · 🐢 Slow & Fast · ∑ Prefix Sum</b></summary>

**📚 Stack (Monotonic)**

| If you see this... | Pattern |
|--------------------|---------|
| `"next greater / smaller element"` | Monotonic stack — push; pop when condition met |
| `"valid parentheses / brackets"` | Push open; pop on close; check match |
| `"largest rectangle / trapped water"` | Monotonic stack — area calc on pop |
| `"remove k digits / smallest number"` | Monotonic stack with removal limit |

**↩️ Backtracking**

| If you see this... | Pattern |
|--------------------|---------|
| `"all subsets / power set"` | Add at every level; pass `i+1` |
| `"all permutations"` | `used[]` array; add at leaf (size==n) |
| `"combinations summing to target"` | Pass `i` for reuse; prune `remain<0` |
| `"duplicates in input, unique results"` | Sort + `if(i>start && nums[i]==nums[i-1]) skip` |
| `"N-Queens / Sudoku / Word Search"` | Place + isValid + recurse + undo |

**🔄 In-Place Reversal**

| If you see this... | Pattern |
|--------------------|---------|
| `"reverse a linked list"` | 4-line flip: save next → flip → advance prev → advance curr |
| `"reverse every k nodes"` | K-group — check k exist, reverse, reconnect |
| `"rotate a linked list by k"` | Find tail+len, `k%=len`, reconnect |

**🔁 Cyclic Sort**

| If you see this... | Pattern |
|--------------------|---------|
| `"array of n integers in range [1, n]"` | Place each number at index `nums[i]-1` |
| `"find the missing / duplicate number"` | Cyclic sort → scan for `nums[i]!=i+1` |
| `"smallest missing positive"` | Cyclic sort with range guard `[1,n]` |

**🐢 Slow & Fast Pointers**

| If you see this... | Pattern |
|--------------------|---------|
| `"detect cycle in linked list"` | Floyd's — slow+1, fast+2 |
| `"find middle of linked list"` | Slow stops at middle when fast reaches end |
| `"find start of cycle"` | Reset slow to head after meeting; both move by 1 |

**∑ Prefix Sum**

| If you see this... | Pattern |
|--------------------|---------|
| `"subarray sum equals k"` | Prefix map — `put(0,1)` then `get(prefix-k)` |
| `"range sum query"` | Build prefix array, answer in O(1) |
| `"contiguous array equal 0s and 1s"` | Remap 0→-1, find longest subarray sum=0 |

</details>

---

## 📁 Repository Structure

```
DSA-Interview-Notes-Java/
├── 01_Two_Pointers_Patterns/        ├── 01_two_pointers_notes.md
│                                    ├── 02_two_pointers_problems.md
│                                    └── 03_two_pointers_extended.md
├── 02_Sliding_Window_Patterns/      ├── notes + problems
├── 03_Slow_And_Fast_Pointers_Pattern/
├── 04_Kadane_Pattern/
├── 05_Prefix_Sum_Pattern/
├── 06_Merge_Interval_Pattern/
├── 07_Stack_Pattern/
├── 08_HashMap_Pattern/
├── 09_In-Place_Reversal_LinkedList/
├── 10_Binary_Search_Pattern/
├── 11_Cyclic_Sort_Pattern/
├── 12_Heap_Pattern/
├── 13_Recursion_And_Backtracking/
├── 14_Trees_Pattern/                ├── notes + problems + tree_traversal.md
├── 15_Graph_Pattern/                ├── notes + problems + beginners + algorithms
├── 16_Dynamic_Programming_Pattern/  ├── notes + problems + level1 + level2
├── 17_Trie_Pattern/                 🔜 coming soon
├── 18_Bit_Manipulation_Pattern/     🔜 coming soon
├── PROBLEMS_INDEX.md                ← All 398 problems grouped by pattern
└── README.md
```

---

## 📖 How to Use

1. **Read notes first** — `01_*_notes.md` sections 1–4 (Identify, What is it, Core rules, Framework)
2. **Attempt blind** — Try each problem 15–20 min before looking at solution
3. **Study approach table** — Understand each step, not just the code
4. **Re-implement from memory** — Write code from scratch, then check
5. **Pre-interview revision** — Section 7 (cheatsheet) in every notes file

**Pattern Priority:**

| Priority | Patterns |
|----------|----------|
| 🔥 Master first | Two Pointers · Sliding Window · HashMap · Binary Search · Tree DFS/BFS · DP |
| ⚡ Important | Heap · Graph · Backtracking · Merge Intervals · Monotonic Stack |
| ✅ Good to have | Cyclic Sort · Prefix Sum · Slow/Fast Pointers |

---

## 📝 Note Format

```
01_*_notes.md               02_*_problems.md
├── 1. How to identify      └── Each problem:
├── 2. What is it               ├── Approach table
├── 3. Core rules               ├── Java code
├── 4. 2-Question framework     └── Traced example
├── 5. Variants table
├── 6. Java template
├── 7. Cheatsheet  ← pre-interview revision
├── 8. Common mistakes
└── 9. Complexity
```

---

## 🔗 Resources

| Resource | What it covers |
|----------|----------------|
| [DSA Patterns you need to know](https://leetcode.com/discuss/study-guide/651719/) | Master pattern list |
| [Dynamic Programming Patterns](https://leetcode.com/discuss/study-guide/458695/) | DP Part I |
| [Dynamic Programming Patterns II](https://leetcode.com/discuss/study-guide/1437879/) | DP Part II |
| [Ultimate Binary Search Template](https://leetcode.com/discuss/study-guide/786126/) | One template solves all |
| [Graph For Beginners](https://leetcode.com/discuss/study-guide/655708/) | BFS, DFS, Union Find |
| [Backtracking General Approach](https://leetcode.com/discuss/study-guide/46981/) | Subsets, Perms, Combinations |
| [Tree Traversal Complete Guide](https://leetcode.com/discuss/study-guide/937307/) | DFS, BFS, Views |
| [Monotonic Stack Guide](https://leetcode.com/discuss/study-guide/2347639/) | All stack patterns |
| [Must Do Questions for MAANG](https://leetcode.com/discuss/study-guide/1998290/) | Interview-focused list |

---

## ⚙️ Setup

```bash
git clone https://github.com/rahul22mrk/DSA-Interview-Notes-Java.git
```

> Java 11+

---

<div align="center">

**⭐ Star this repo if it helps your interview prep!**

</div>
