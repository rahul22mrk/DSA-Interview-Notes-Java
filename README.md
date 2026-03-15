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
1. What is this pattern?
2. Core rules  (3 things to always remember)
3. 2-question framework  (how to identify the variant)
4. Variants table
5. Universal Java template  (with commented labels)
6. 8–10 solved problems
   ├── Approach table  (loop / condition / result)
   ├── Clean Java code
   └── Input → Output example
7. Quick reference cheatsheet
8. Common mistakes
9. Complexity summary
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

---

## ⚙️ Setup

```bash
# Clone the repo
git clone https://github.com/rahul22mrk/DSA-Interview-Notes-Java.git

# Navigate to any pattern
cd DSA-Interview-Notes-Java/07_Stack_Pattern
```

> **Java Version:** 11+

---

## 🤝 Contributing

Found a bug or want to add a pattern? Feel free to open a PR or raise an issue.

---

*Last updated: March 2026 · Maintained by [@rahul22mrk](https://github.com/rahul22mrk)*
