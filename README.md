# 📚 DSA Interview Notes — Java

> Pattern-wise DSA notes in Java | Interview-focused | Clean code templates | Time complexity analysis

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
├── 03_Fast_And_Slow_Pointers/
│   └── 🔜 coming soon
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
└── README.md
```

---

## 🧩 Patterns Covered

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
| `03_Fast_And_Slow_Pointers` | Fast & Slow Pointers | Cycle detection, Middle of linked list, Happy number |
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
1. How to identify this pattern  (keywords + brute force test + 5 signals)
2. What is this pattern?
3. Core rules  (3 things to always remember)
4. 2-question framework  (how to identify the variant)
5. Variants table  (Key → Value → Query for each sub-pattern)
6. Universal Java template  (with commented labels)
7. 8–10 solved problems
   ├── Approach table  (loop / condition / result)
   ├── Clean Java code
   └── Input → Output example
8. Quick reference cheatsheet
9. Common mistakes
10. Complexity summary
```

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

---

## ⚙️ Setup

```bash
# Clone the repo
git clone https://github.com/rahul22mrk/DSA-Interview-Notes-Java.git

# Navigate to any pattern
cd DSA-Interview-Notes-Java/07_Stack_Pattern
cd DSA-Interview-Notes-Java/08_HashMap_Pattern
cd DSA-Interview-Notes-Java/09_In-Place_Reversal_LinkedList
```

> **Java Version:** 11+

---

## 🤝 Contributing

Found a bug or want to add a pattern? Feel free to open a PR or raise an issue.

---

*Last updated: March 2026 · Maintained by [@rahul22mrk](https://github.com/rahul22mrk)*
