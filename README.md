# 📚 DSA Interview Notes — Java

> Pattern-wise DSA notes in Java | Interview-focused | Clean code templates | Time complexity analysis

---

## 🗂 What's Inside

Each pattern folder contains:
- **Concept note** — what the pattern is, when to use it, core rules
- **Universal template** — reusable Java code you can adapt to any problem
- **8–10 solved problems** — each with approach, clean code, dry run, input/output
- **Cheatsheet** — quick reference table for interviews

---

## 📁 Repository Structure

```
DSA-Interview-Notes-Java/
│
├── Stack/
│   ├── 01-monotonic-stack.md
│   ├── 02-stack-count.md
│   └── 03-stack-simulation.md
│
├── Sliding-Window/          🔜 coming soon
├── Two-Pointers/            🔜 coming soon
├── Binary-Search/           🔜 coming soon
├── Trees/                   🔜 coming soon
├── Graphs/                  🔜 coming soon
├── Dynamic-Programming/     🔜 coming soon
│
└── README.md
```

---

## 🧩 Patterns Covered

### ✅ Stack
| File | Sub-Pattern | Problems Covered | Difficulty |
|------|------------|-----------------|------------|
| [01-monotonic-stack.md](./Stack/01-monotonic-stack.md) | Monotonic Stack | Next/Prev Greater/Smaller, Daily Temperatures, Largest Rectangle, Trapping Rain Water, Stock Span, Sum of Subarray Minimums | Easy → Hard |
| [02-stack-count.md](./Stack/02-stack-count.md) | Stack + Count | Remove Adjacent Duplicates I & II, Decode String, Removing Stars, Backspace Compare, Score of Parentheses, Valid Parentheses, Min Remove to Valid | Easy → Medium |
| [03-stack-simulation.md](./Stack/03-stack-simulation.md) | Stack Simulation | Backspace Compare, Asteroid Collision, Evaluate RPN, Simplify Path, Remove K Digits, Remove Duplicate Letters | Easy → Hard |

### 🔜 Coming Soon
| Pattern | Topics |
|---------|--------|
| Sliding Window | Fixed window, Variable window, At most K distinct |
| Two Pointers | Sorted arrays, Palindrome, Container with most water |
| Binary Search | Classic, On answer, Rotated array |
| Trees | DFS, BFS, LCA, Diameter, Serialization |
| Graphs | BFS/DFS, Topological sort, Union Find, Dijkstra |
| Dynamic Programming | 1D/2D DP, Knapsack, LCS, LIS |

---

## 🔍 How to Use These Notes

1. **Pick a pattern** from the table above
2. **Read the concept section** — understand the core idea and 3 key rules
3. **Study the universal template** — this is what you'll adapt in interviews
4. **Go through each problem** — focus on the approach table before reading code
5. **Revise using the cheatsheet** — quick reference before your interview

---

## ⚡ Stack Patterns — Quick Clue Detector

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

| # | Problem | LC | Pattern | Difficulty |
|---|---------|-----|---------|------------|
| 1 | Next Greater Element I | 496 | Monotonic | Easy |
| 2 | Daily Temperatures | 739 | Monotonic | Medium |
| 3 | Stock Span Problem | 901 | Monotonic | Medium |
| 4 | Next Greater Element II | 503 | Monotonic | Medium |
| 5 | Sum of Subarray Minimums | 907 | Monotonic | Medium |
| 6 | Largest Rectangle in Histogram | 84 | Monotonic | Hard |
| 7 | Trapping Rain Water | 42 | Monotonic | Hard |
| 8 | Remove All Adjacent Duplicates I | 1047 | Stack+Count | Easy |
| 9 | Valid Parentheses | 20 | Stack+Count | Easy |
| 10 | Backspace String Compare | 844 | Stack+Count | Easy |
| 11 | Remove All Adjacent Duplicates II | 1209 | Stack+Count | Medium |
| 12 | Decode String | 394 | Stack+Count | Medium |
| 13 | Removing Stars From a String | 2390 | Stack+Count | Medium |
| 14 | Score of Parentheses | 856 | Stack+Count | Medium |
| 15 | Min Remove to Make Valid | 1249 | Stack+Count | Medium |
| 16 | Removing Stars | 2390 | Simulation | Medium |
| 17 | Evaluate RPN | 150 | Simulation | Medium |
| 18 | Asteroid Collision | 735 | Simulation | Medium |
| 19 | Simplify Path | 71 | Simulation | Medium |
| 20 | Remove K Digits | 402 | Simulation | Medium |
| 21 | Longest Valid Parentheses | 32 | Stack+Count | Hard |
| 22 | Remove Duplicate Letters | 316 | Simulation | Hard |

---

## ⚙️ Setup

```bash
# Clone the repo
git clone https://github.com/rahul22mrk/DSA-Interview-Notes-Java.git

# Open any note
cd DSA-Interview-Notes-Java/Stack
```

> **Java Version:** 11+ &nbsp;|&nbsp; No external dependencies

---

## 📌 Note Format (Every File Follows This)

Every `.md` file is structured the same way so you always know where to look:

```
1. What is this pattern?
2. Core rules (3 key things to remember)
3. 2-question framework (how to identify the variant)
4. Variants table
5. Universal Java template
6. 8-10 solved problems
   └── Approach table (loop / condition / result)
   └── Clean Java code
   └── Input → Output example
7. Quick reference cheatsheet
8. Common mistakes
9. Complexity summary
```

---

## 🤝 Contributing

Found a bug or want to add a pattern? Feel free to open a PR or raise an issue.

---

*Last updated: March 2026 &nbsp;·&nbsp; Maintained by [@rahul22mrk](https://github.com/rahul22mrk)*
