# Stack Pattern — Complete Notes

> **Pattern family:** Stack / Monotonic Stack / Design / Expression Evaluation
> **Difficulty range:** Easy → Hard
> **Language:** Java

---

## Table of Contents

1. [How to identify this pattern](#1-how-to-identify-this-pattern) ← **start here**
2. [What is this pattern?](#2-what-is-this-pattern)
3. [Core rules](#3-core-rules)
4. [2-Question framework](#4-2-question-framework)
5. [Variants table](#5-variants-table)
6. [Universal Java template](#6-universal-java-template)
7. [Quick reference cheatsheet](#7-quick-reference-cheatsheet)
8. [Common mistakes](#8-common-mistakes)
9. [Complexity summary](#9-complexity-summary)

---

## 1. How to identify this pattern

### Keyword scanner

| If you see this... | It means |
|--------------------|----------|
| "next greater / smaller element" | Monotonic Stack |
| "previous greater / smaller element" | Monotonic Stack (R→L) |
| "largest rectangle in histogram" | Monotonic Stack (width calculation) |
| "trapping rain water" | Monotonic Stack (valley detection) |
| "sum of subarray minimums / maximums" | Monotonic Stack (contribution technique) |
| "stock span / consecutive days" | Monotonic Stack (distance to prev greater) |
| "valid / balanced parentheses" | Stack — bracket matching |
| "decode 3[abc] / nested encoding" | Stack — save state on `[`, restore on `]` |
| "k adjacent equal duplicates" | Stack + Count `[char, count]` pair |
| "remove duplicates / backspace / stars" | Stack — pop on trigger character |
| "evaluate expression / RPN / calculator" | Stack — operand push, operator pop-2 |
| "collision / asteroid" | Stack — conditional pop |
| "simplify path / canonical path" | Stack — push dirs, pop on `..` |
| "min stack / max frequency stack" | Design Stack — augmented state |
| "implement queue using stacks" | Two Stacks — inbox/outbox |
| "browser history / undo/redo" | Two Stacks — back/forward |

### Brute force test

```
Brute force: for "next greater element" check every element to the right → O(n²).
→ Interviewer says "O(n)" → cannot scan right for every element.
→ Key insight: if you maintain a DECREASING stack (monotonic),
  the moment a larger element arrives, it IS the answer for everything it's larger than.
→ Total: O(n) — each element pushed and popped at most once.
```

### The 5 confirming signals

**Signal 1 — "Nearest / next / previous" + "greater / smaller"**
> Classic monotonic stack. The answer for each element depends on
> the nearest element satisfying a condition — stack gives O(1) lookup.

**Signal 2 — "Remove" + "adjacent" or "trigger character"**
> Stack naturally undoes the most recent action.
> Backspace, stars, k-duplicates — all are "pop on condition" problems.

**Signal 3 — "Nested structure" (brackets, encoded strings)**
> When you need to save current state, go deeper, then restore — push on `[`, pop on `]`.
> Valid parentheses, decode string, score of parentheses all follow this.

**Signal 4 — "Evaluate expression" or "calculator"**
> Operands pushed, operators trigger pop-2-calculate-push-1.
> RPN is the pure form; Basic Calculator adds operator precedence handling.

**Signal 5 — "Design" + "O(1) getMin/getMax" or "history"**
> Two stacks solve undo/redo and queue-from-stack problems.
> Augmented stack (storing extra state alongside value) handles min/max in O(1).

### Decision flowchart

```
Problem involves a stack-like structure?
        │
        ▼
What is the core operation?
        │
        ├── NEAREST GREATER/SMALLER element
        │       └── Monotonic Stack
        │           ├── Next → loop L→R, pop when condition met
        │           └── Prev → loop R→L, check top before push
        │
        ├── REMOVE characters based on condition
        │       ├── Single char trigger (#, *)  → Stack Simulation
        │       └── k adjacent same chars       → Stack + [char, count]
        │
        ├── NESTED / BRACKET structure
        │       ├── Valid/matching            → push open, pop+match close
        │       ├── Decode/encode string      → push (count, built-string)
        │       └── Score / depth calculation → push 0 on (, compute on )
        │
        ├── EVALUATE expression
        │       ├── RPN (postfix)      → push operands, operator triggers calc
        │       └── Infix (+operator precedence) → two-stack or shunting yard
        │
        ├── DESIGN problem
        │       ├── Min/Max Stack              → augmented stack (val, minSoFar)
        │       ├── Queue from Stacks          → inbox + outbox stacks
        │       ├── Browser History            → back-stack + forward-stack
        │       └── Max Frequency Stack        → freq map + group map
        │
        └── AREA / WIDTH calculation (histogram, rain water)
                └── Monotonic Stack
                    ├── Pop = valley/boundary found
                    └── Width = i - stack.peek() - 1
```

---

## 2. What is this pattern?

**Core data structure:** Stack = LIFO (Last In First Out). The top always holds the most recently seen / most relevant element.

### Sub-patterns and their core ideas:

**Monotonic Stack:**
Maintain a stack where elements are always in sorted order (increasing or decreasing). When the order is violated, **pop — and popping means the answer for that element has been found.**

```
Push INDEX, not value. From index you can get value, distance, AND width.
Pop = answer found for the popped element.
Elements left in stack = have no answer → default -1 or 0.
```

**Stack + Count (Pair Stack):**
Store `[char, count]` pairs. When count reaches threshold → pop the entire group.
Cascading is **automatic** — after a pop, the new top is checked on the very next iteration.

**Stack Simulation:**
Stack as a simulation machine. Each token/character triggers an action: push, pop, or compute. The top always holds the "most recent active state."

**Design Stacks:**
Augment the stack with extra information (min so far, frequency, etc.) or use two stacks to simulate other data structures.

```
Min Stack:   push (val, minSoFar) pair → O(1) getMin
Queue:       inbox stack + outbox stack → amortized O(1) dequeue
Browser:     back-stack + forward-stack → O(1) navigate
```

---

## 3. Core rules

**Rule 1 — Always push INDEX, not VALUE (for monotonic stack)**
```java
// WRONG — cannot calculate distance or width from value alone
st.push(arr[i]);

// CORRECT — index gives you value, distance, AND width
st.push(i);
// arr[st.peek()] = value
// i - st.peek()  = distance
// i - st.peek() - 1 = width between elements
```

**Rule 2 — Pop condition determines the variant**
```java
// WRONG — mixing up > and < gives you the opposite answer
while (!st.isEmpty() && arr[st.peek()] > arr[i])   // this is NEXT SMALLER, not next greater

// CORRECT mental model:
// Next Greater  → pop when top < current  (current IS the answer for popped)
// Next Smaller  → pop when top > current
// Prev Greater  → loop R→L, check top before push
// Prev Smaller  → loop R→L, check top before push
```

**Rule 3 — Always check `!isEmpty()` before `peek()` or `pop()`**
```java
// WRONG — NPE when stack is empty
while (arr[st.peek()] < arr[i]) { ... }

// CORRECT — always guard with isEmpty check
while (!st.isEmpty() && arr[st.peek()] < arr[i]) { ... }
```

**Rule 4 — Use `Deque<T>` not `Stack<T>`**
```java
// WRONG — Stack<T> is synchronized (slow), legacy class
Stack<Integer> st = new Stack<>();

// CORRECT — ArrayDeque is faster, Java-recommended
Deque<Integer> st = new ArrayDeque<>();
```

**Rule 5 — For expression evaluation, pop `b` before `a`**
```java
// WRONG — order matters for subtraction and division!
int a = stack.pop();
int b = stack.pop();
stack.push(a - b);   // WRONG: b was pushed first, a is more recent

// CORRECT
int b = stack.pop();   // more recent (right operand)
int a = stack.pop();   // older (left operand)
stack.push(a - b);     // a - b ✓
```

---

## 4. 2-Question framework

### Question 1 — What triggers a pop?

| Answer | Variant |
|--------|---------|
| A larger element arrives | Monotonic Decreasing Stack (Next Greater) |
| A smaller element arrives | Monotonic Increasing Stack (Next Smaller) |
| A special character (`#`, `*`) | Stack Simulation (backspace, star removal) |
| Count reaches threshold k | Stack + Count (k-duplicate removal) |
| A closing bracket `)` / `]` | Nested structure (parentheses, decode) |
| An operator token | Expression Evaluation (RPN, Calculator) |
| A collision condition | Conditional Simulation (Asteroid) |

### Question 2 — What do you store in the stack?

| Store | When | Example |
|-------|------|---------|
| **Index** | Need distance or width | Monotonic stack, histogram, rain water |
| **[char, count]** | Need count of consecutive | k-duplicate removal |
| **char** | Simple removal | Backspace, valid parentheses |
| **int value** | Computing running result | RPN, asteroid |
| **(count, StringBuilder)** | Nested string building | Decode String |
| **(val, minSoFar)** | O(1) min query | Min Stack |
| **[price, span]** | Online/streaming design | Online Stock Span |

> **Decision shortcut:**
> - "next/prev + greater/smaller" → monotonic stack, push index
> - "remove on trigger char" → push char, pop on trigger
> - "k adjacent same" → push `[char, count]`, pop when count==k
> - "bracket matching" → push open, match on close
> - "evaluate expression" → push numbers, operator pops 2
> - "O(1) getMin" → push (value, min) pair

---

## 5. Variants table

> **Common core:** `Deque<> st = new ArrayDeque<>()`
> **What differs:** loop direction, pop condition, what you push, what you record

| Variant | Loop | Pop when | Push | Record |
|---------|------|----------|------|--------|
| Next Greater | L→R | `arr[top] < arr[i]` | index | `result[pop] = arr[i]` |
| Next Smaller | L→R | `arr[top] > arr[i]` | index | `result[pop] = arr[i]` |
| Prev Greater | R→L | `arr[top] <= arr[i]` | index | `result[i] = arr[top]` before push |
| Prev Smaller | R→L | `arr[top] >= arr[i]` | index | `result[i] = arr[top]` before push |
| Histogram | L→R + sentinel | `arr[top] > h` | index | `h × (i - newTop - 1)` |
| Rain Water | L→R | `height[top] < height[i]` | index | `(min(L,R) - bottom) × width` |
| Circular NGE | L→R `2n` | `nums[top] < nums[i%n]` | index (1st pass only) | `result[pop] = nums[i%n]` |
| Stock Span | L→R | `arr[top] <= arr[i]` | index | `i - top` before push |
| k-Duplicate | L→R | `count == k` | `[char, count]` | pop entire group |
| Backspace | L→R | `ch == '#'` | char | remaining chars |
| Valid Parens | L→R | mismatch on `)` | open bracket | stack empty at end |
| Decode String | L→R | on `]` | `(count, sb)` | repeat and restore |
| RPN | L→R | on operator | int value | `a op b`, push result |
| Min Stack | push | never (keep both) | `(val, min)` | `peek()[1]` = min |
| Queue/2-Stack | push | transfer on empty outbox | int value | front = outbox.peek() |

---

## 6. Universal Java template

```java
// ─── TEMPLATE A: Monotonic Stack — Next Greater ───────────────────────────────
int[] result = new int[n];
Arrays.fill(result, -1);                        // default: no answer
Deque<Integer> st = new ArrayDeque<>();

for (int i = 0; i < n; i++) {                   // ← Prev type: i = n-1 to 0
    while (!st.isEmpty() && arr[st.peek()] < arr[i]) {  // ← Smaller: use >
        result[st.pop()] = arr[i];              // ← Prev type: result[i] = arr[st.peek()]
    }
    st.push(i);                                 // always push index
}
// Elements still in st have no next greater → result stays -1


// ─── TEMPLATE B: Histogram / Width Calculation ───────────────────────────────
Deque<Integer> st = new ArrayDeque<>();
st.push(-1);                                    // sentinel for width calculation
int maxArea = 0;

for (int i = 0; i <= n; i++) {
    int h = (i == n) ? 0 : arr[i];             // trailing sentinel forces all pops
    while (st.peek() != -1 && arr[st.peek()] > h) {
        int height = arr[st.pop()];
        int width  = i - st.peek() - 1;        // width between current and new top
        maxArea = Math.max(maxArea, height * width);
    }
    st.push(i);
}


// ─── TEMPLATE C: Stack + Count (k-Duplicate Removal) ─────────────────────────
Deque<int[]> st = new ArrayDeque<>();           // [charCode, count]

for (char ch : s.toCharArray()) {
    if (!st.isEmpty() && st.peek()[0] == ch) {
        st.peek()[1]++;
        if (st.peek()[1] == k) st.pop();        // ← change threshold here
    } else {
        st.push(new int[]{ch, 1});
    }
}
// Rebuild: reverse list, repeat each char by count


// ─── TEMPLATE D: Bracket Matching (Valid Parentheses) ────────────────────────
Deque<Character> st = new ArrayDeque<>();

for (char ch : s.toCharArray()) {
    if (ch == '(' || ch == '{' || ch == '[') {
        st.push(ch);
    } else {
        if (st.isEmpty()) return false;
        char top = st.pop();
        if (ch == ')' && top != '(') return false;
        if (ch == '}' && top != '{') return false;
        if (ch == ']' && top != '[') return false;
    }
}
return st.isEmpty();


// ─── TEMPLATE E: Decode String (Save/Restore State) ──────────────────────────
Deque<Integer> counts = new ArrayDeque<>();
Deque<StringBuilder> strings = new ArrayDeque<>();
StringBuilder curr = new StringBuilder();
int k = 0;

for (char ch : s.toCharArray()) {
    if (Character.isDigit(ch))  { k = k * 10 + (ch - '0'); }
    else if (ch == '[')         { counts.push(k); strings.push(curr); curr = new StringBuilder(); k = 0; }
    else if (ch == ']')         { int t = counts.pop(); StringBuilder prev = strings.pop(); for (int i = 0; i < t; i++) prev.append(curr); curr = prev; }
    else                        { curr.append(ch); }
}
return curr.toString();


// ─── TEMPLATE F: Expression Evaluation (RPN) ─────────────────────────────────
Deque<Integer> st = new ArrayDeque<>();

for (String token : tokens) {
    if ("+-*/".contains(token)) {
        int b = st.pop();                       // ← b first (right operand)
        int a = st.pop();                       // ← a second (left operand)
        switch (token) {
            case "+" -> st.push(a + b);
            case "-" -> st.push(a - b);
            case "*" -> st.push(a * b);
            case "/" -> st.push(a / b);
        }
    } else {
        st.push(Integer.parseInt(token));
    }
}
return st.pop();


// ─── TEMPLATE G: Min Stack (Augmented) ───────────────────────────────────────
Deque<int[]> st = new ArrayDeque<>();           // [value, minSoFar]

public void push(int val) {
    int min = st.isEmpty() ? val : Math.min(val, st.peek()[1]);
    st.push(new int[]{val, min});
}
public void pop()    { st.pop(); }
public int top()     { return st.peek()[0]; }
public int getMin()  { return st.peek()[1]; }  // O(1) always


// ─── TEMPLATE H: Queue Using Two Stacks ──────────────────────────────────────
Deque<Integer> inbox  = new ArrayDeque<>();    // push here
Deque<Integer> outbox = new ArrayDeque<>();    // pop/peek from here

public void push(int x) { inbox.push(x); }

public int pop() {
    transfer();
    return outbox.pop();
}
public int peek() {
    transfer();
    return outbox.peek();
}
private void transfer() {
    if (outbox.isEmpty())
        while (!inbox.isEmpty()) outbox.push(inbox.pop());
}


// ─── TEMPLATE I: Browser History (Two Stacks) ────────────────────────────────
Deque<String> back    = new ArrayDeque<>();    // visited pages
Deque<String> forward = new ArrayDeque<>();    // pages after current
String curr;

public void visit(String url)  { back.push(curr); curr = url; forward.clear(); }
public String back(int steps)  { while (steps-- > 0 && !back.isEmpty()) { forward.push(curr); curr = back.pop(); } return curr; }
public String forward(int steps) { while (steps-- > 0 && !forward.isEmpty()) { back.push(curr); curr = forward.pop(); } return curr; }
```

---

## 7. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                              → VARIANT                  → KEY CODE
────────────────────────────────────────────────────────────────────────────────────────────
"next greater element"                         → Monotonic ↓ stack       → pop when top < curr; result[pop] = curr
"next smaller element"                         → Monotonic ↑ stack       → pop when top > curr; result[pop] = curr
"previous greater / stock span"                → Monotonic, R→L or L→R   → result[i] = top before push
"largest rectangle in histogram"               → Monotonic + sentinel     → area = h × (i - newTop - 1)
"trapping rain water"                          → Monotonic valley         → water = (min(L,R) - bottom) × width
"sum of subarray minimums"                     → Monotonic contribution   → arr[idx] × left × right
"circular array next greater"                  → Monotonic 2n loop        → i % n; push only first n
"valid / balanced parentheses"                 → Bracket match            → push open, pop+match close
"remove k adjacent same"                       → Stack + [char, count]    → count == k → pop
"backspace / star / # removal"                 → Stack simulation         → pop on trigger char
"decode 3[abc]"                                → Save/restore state       → push (k, curr) on [; restore on ]
"evaluate RPN / postfix"                       → Expression stack         → b=pop, a=pop; push(a op b)
"basic calculator II"                          → Operator precedence      → handle +- with sign, */ inline
"min stack / O(1) getMin"                      → Augmented stack          → push (val, min); getMin = peek()[1]
"implement queue using stacks"                 → Two stacks               → inbox push; transfer on empty outbox
"browser history / undo redo"                  → Two stacks               → back-stack + forward-stack
"asteroid collision"                           → Conditional simulation   → pop while top>0 and curr<0
```

**Burn these into memory:**
```java
// Monotonic Stack — 4 variants in 2 lines each:
// Next Greater:  L→R, pop when top < curr,  result[pop] = curr
// Next Smaller:  L→R, pop when top > curr,  result[pop] = curr
// Prev Greater:  R→L, pop when top <= curr, result[i] = top (before push)
// Prev Smaller:  R→L, pop when top >= curr, result[i] = top (before push)

// Width formula (histogram/rain water):
int width = i - st.peek() - 1;   // between current and new stack top

// Expression eval — ORDER MATTERS:
int b = st.pop();   // right operand first
int a = st.pop();   // left operand second
st.push(a - b);     // a - b, NOT b - a
```

---

## 8. Common mistakes

### Mistake 1 — Pushing value instead of index

```java
// BUG — cannot calculate distance or width
st.push(arr[i]);   // only value stored

// FIX — push index, derive value when needed
st.push(i);
int val = arr[st.peek()];        // get value
int dist = i - st.pop();         // get distance
int width = i - st.peek() - 1;  // get width after pop
```

### Mistake 2 — Wrong pop condition for variant

```java
// BUG — this finds Next SMALLER, not Next Greater
while (!st.isEmpty() && arr[st.peek()] > arr[i])
    result[st.pop()] = arr[i];

// FIX — Next Greater: pop when top is LESS than current
while (!st.isEmpty() && arr[st.peek()] < arr[i])
    result[st.pop()] = arr[i];
```

### Mistake 3 — Missing isEmpty() check before peek()

```java
// BUG — NPE when stack is empty
while (arr[st.peek()] < arr[i]) { ... }

// FIX
while (!st.isEmpty() && arr[st.peek()] < arr[i]) { ... }
```

### Mistake 4 — Wrong operand order in expression evaluation

```java
// BUG — for subtraction and division, order matters
int a = st.pop();   // actually the RIGHT operand (most recently pushed)
int b = st.pop();   // actually the LEFT operand
st.push(a - b);     // WRONG: should be b - a

// FIX — pop b (right) first, then a (left)
int b = st.pop();   // right operand
int a = st.pop();   // left operand
st.push(a - b);     // correct: a - b ✓
```

### Mistake 5 — Forgetting the sentinel in histogram

```java
// BUG — bars taller than all others are never processed
for (int i = 0; i < n; i++) { ... }   // loop ends, stack still has indices

// FIX — add trailing sentinel 0 to force all pops
for (int i = 0; i <= n; i++) {
    int h = (i == n) ? 0 : arr[i];   // sentinel forces all remaining pops
    ...
}
```

### Mistake 6 — Using Stack<T> (legacy class)

```java
// WRONG — Stack is synchronized, slow, legacy
Stack<Integer> st = new Stack<>();

// CORRECT — ArrayDeque is the Java-recommended modern stack
Deque<Integer> st = new ArrayDeque<>();
// push → st.push(x)   peek → st.peek()   pop → st.pop()
```

### Mistake 7 — Forgetting to reverse when rebuilding from stack

```java
// BUG — stack is LIFO, reading directly gives reversed result
StringBuilder sb = new StringBuilder();
while (!st.isEmpty()) sb.append((char) st.pop()[0]);
// sb is in reverse order!

// FIX — either reverse at end, or iterate list after Collections.reverse()
List<int[]> list = new ArrayList<>(st);
Collections.reverse(list);                    // reverse first
for (int[] pair : list) { ... append pair ... }
```

### Mistake 8 — Forgetting to clear forward stack on browser visit

```java
// BUG — old forward history persists after visiting a new page
public void visit(String url) {
    back.push(curr);
    curr = url;
    // forgot: forward.clear()  → stale forward history!
}

// FIX
public void visit(String url) {
    back.push(curr); curr = url; forward.clear();   // always clear forward on new visit
}
```

---

## 9. Complexity summary

| Problem / Variant | Time | Space | Notes |
|-------------------|------|-------|-------|
| All Monotonic Stack problems | O(n) | O(n) | each element pushed/popped at most once |
| Largest Rectangle in Histogram | O(n) | O(n) | sentinel forces all pops |
| Trapping Rain Water | O(n) | O(n) | single pass with stack |
| Sum of Subarray Minimums | O(n) | O(n) | contribution per element |
| k-Duplicate Removal | O(n) | O(n) | single pass, each char processed once |
| Valid Parentheses | O(n) | O(n) | single pass |
| Decode String | O(n) | O(n) | n = output length (can be larger than input) |
| Evaluate RPN | O(n) | O(n) | n = number of tokens |
| Basic Calculator II | O(n) | O(n) | single pass with sign tracking |
| Min Stack | O(1) per op | O(n) | augmented stack stores min alongside |
| Queue via Two Stacks | O(1) amortized | O(n) | transfer is amortized O(1) per element |
| Browser History | O(steps) per op | O(n) | bounded by history length |
| Max Frequency Stack | O(log n) or O(1) | O(n) | depending on implementation |

**General rules:**
- **All stack problems are O(n) time** — each element enters and leaves the stack at most once.
- **Space is O(n)** — worst case all elements are in the stack at once.
- Exception: Decode String — output can be exponentially larger, but stack depth is O(n).
- Min Stack, Queue via Two Stacks — amortized O(1) per operation.

---

*Stack is the backbone of 5+ distinct problem families.*
*Master the monotonic stack first — it covers histogram, rain water, NGE, stock span, and subarray minimums all with ONE template.*
