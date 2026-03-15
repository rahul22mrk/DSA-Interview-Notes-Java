# 🗂 Pattern 3 — Stack Simulation

> **Language:** Java &nbsp;|&nbsp; **Difficulty:** Easy → Hard &nbsp;|&nbsp; **Problems:** 8

---

## 📌 What is Stack Simulation?

Use the stack as a **simulation machine**. Apply operations one by one and store the current state in the stack. The most recent state is always at the top — perfect for undo operations, collisions, and expression evaluation.

---

## 💡 Core Insight — Remember These 3 Rules

| # | Rule | Why |
|---|------|-----|
| 1 | **Model the problem as a sequence of operations** | Each character or token triggers an action — push, pop, or calculate. |
| 2 | **Stack top = most recent active state** | Collision, backspace, and RPN all rely on "what happened just before". |
| 3 | **Conditional pop** | Don't always pop — check a condition first. e.g. asteroids only collide if moving toward each other. |

---

## 🔀 See the Problem → Ask Only 2 Questions

| Question | Option A | Option B | Decision |
|----------|----------|----------|----------|
| **Q1:** What triggers a pop? | A specific character (`*`, `#`, operator) | A condition (size comparison, sign) | Symbol-based &nbsp;vs&nbsp; Condition-based |
| **Q2:** What to push? | Raw character / value | Processed result (e.g. computed value) | Backspace/Stars &nbsp;vs&nbsp; RPN/Collision |

---

## 📊 Variants — What Changes Per Problem

| Type | Stack Stores | Pop Condition | Result |
|------|-------------|---------------|--------|
| Backspace / Star removal | `char` | on `#` or `*` | Remaining chars |
| Collision (Asteroids) | `int` asteroid | opposite signs + size check | Surviving asteroids |
| Expression eval (RPN) | `int` operand | on operator token | Final computed value |
| Path simplification | `String` dirs | on `..` | Canonical path |

---

## 💻 Template 1 — Symbol Triggered Pop (Backspace / Stars)

```java
// Pop on special symbol, push otherwise
Deque<Character> stack = new ArrayDeque<>();

for (char ch : s.toCharArray()) {
    if (ch == '#' || ch == '*') {    // ← change symbol here
        if (!stack.isEmpty()) stack.pop();
    } else {
        stack.push(ch);
    }
}

// Rebuild result
StringBuilder sb = new StringBuilder();
while (!stack.isEmpty()) sb.append(stack.pop());
return sb.reverse().toString();
```

## 💻 Template 2 — Expression Evaluation (RPN)

```java
// Push operands, on operator → pop 2, calculate, push result
Deque<Integer> stack = new ArrayDeque<>();

for (String token : tokens) {
    if ("+-*/".contains(token)) {
        int b = stack.pop();
        int a = stack.pop();
        switch (token) {
            case "+" -> stack.push(a + b);
            case "-" -> stack.push(a - b);
            case "*" -> stack.push(a * b);
            case "/" -> stack.push(a / b);
        }
    } else {
        stack.push(Integer.parseInt(token));
    }
}
return stack.pop();
```

## 💻 Template 3 — Conditional Pop (Collision)

```java
// Pop only when condition is met between top and current
Deque<Integer> stack = new ArrayDeque<>();

for (int val : arr) {
    boolean alive = true;
    while (alive && /* collision condition */) {
        if      (/* top loses */)  stack.pop();
        else if (/* tie */)       { stack.pop(); alive = false; }
        else                       alive = false;   // current loses
    }
    if (alive) stack.push(val);
}
```

---

## 🧩 8 Problems

---

### 1. Backspace String Compare &nbsp;`Easy` &nbsp;·&nbsp; LC #844

> 💡 `#` = backspace → pop. Process both strings independently, then compare.

```java
public boolean backspaceCompare(String s, String t) {
    return process(s).equals(process(t));
}
private String process(String s) {
    Deque<Character> stack = new ArrayDeque<>();
    for (char ch : s.toCharArray()) {
        if (ch == '#') { if (!stack.isEmpty()) stack.pop(); }
        else             stack.push(ch);
    }
    StringBuilder sb = new StringBuilder();
    while (!stack.isEmpty()) sb.append(stack.pop());
    return sb.reverse().toString();
}
```

```
Input  : s = "ab#c",  t = "ad#c"
Output : true   (both become "ac")
```

---

### 2. Removing Stars From a String &nbsp;`Medium` &nbsp;·&nbsp; LC #2390

> 💡 `*` = delete the closest non-star character to its left → pop on `*`.

```java
Deque<Character> stack = new ArrayDeque<>();
for (char ch : s.toCharArray()) {
    if (ch == '*') stack.pop();
    else           stack.push(ch);
}
StringBuilder sb = new StringBuilder();
while (!stack.isEmpty()) sb.append(stack.pop());
return sb.reverse().toString();
```

```
Input  : "leet**cod*e"
Output : "lecoe"
```

---

### 3. Evaluate Reverse Polish Notation &nbsp;`Medium` &nbsp;·&nbsp; LC #150

> 💡 Numbers → push. Operator → pop 2, calculate, push result back.

```java
Deque<Integer> stack = new ArrayDeque<>();
for (String t : tokens) {
    if ("+-*/".contains(t)) {
        int b = stack.pop(), a = stack.pop();
        switch (t) {
            case "+" -> stack.push(a + b);
            case "-" -> stack.push(a - b);
            case "*" -> stack.push(a * b);
            case "/" -> stack.push(a / b);
        }
    } else {
        stack.push(Integer.parseInt(t));
    }
}
return stack.pop();
```

```
Input  : ["2","1","+","3","*"]
Output : 9    →  (2+1)*3 = 9
```

---

### 4. Asteroid Collision &nbsp;`Medium` &nbsp;·&nbsp; LC #735

> 💡 Positive = right, Negative = left. Collision only when stack top `> 0` and current `< 0`. Larger survives.

```java
Deque<Integer> stack = new ArrayDeque<>();
for (int a : asteroids) {
    boolean alive = true;
    while (alive && a < 0 && !stack.isEmpty() && stack.peek() > 0) {
        if      (stack.peek() < -a)  stack.pop();
        else if (stack.peek() == -a) { stack.pop(); alive = false; }
        else                           alive = false;
    }
    if (alive) stack.push(a);
}
int[] res = new int[stack.size()];
for (int i = res.length - 1; i >= 0; i--) res[i] = stack.pop();
return res;
```

```
Input  : [5, 10, -5]     Output : [5, 10]
Input  : [8, -8]         Output : []
Input  : [10, 2, -5]     Output : [10]
```

---

### 5. Simplify Path &nbsp;`Medium` &nbsp;·&nbsp; LC #71

> 💡 Split by `/`. Skip empty and `.`. On `..` pop the stack. Everything else → push.

```java
Deque<String> stack = new ArrayDeque<>();
for (String dir : path.split("/")) {
    if (dir.equals("..")) {
        if (!stack.isEmpty()) stack.pop();
    } else if (!dir.isEmpty() && !dir.equals(".")) {
        stack.push(dir);
    }
}
StringBuilder sb = new StringBuilder();
List<String> list = new ArrayList<>(stack);
Collections.reverse(list);
for (String d : list) sb.append("/").append(d);
return sb.length() == 0 ? "/" : sb.toString();
```

```
Input  : "/home/../usr/./bin"
Output : "/usr/bin"
```

---

### 6. Daily Temperatures &nbsp;`Medium` &nbsp;·&nbsp; LC #739

> 💡 Monotonic stack variant — but fits here too. Stack holds indices waiting for their next warmer day.

```java
Deque<Integer> stack = new ArrayDeque<>();
int[] result = new int[temperatures.length];
for (int i = 0; i < temperatures.length; i++) {
    while (!stack.isEmpty() && temperatures[stack.peek()] < temperatures[i]) {
        int idx = stack.pop();
        result[idx] = i - idx;
    }
    stack.push(i);
}
return result;
```

```
Input  : [73,74,75,71,69,72,76,73]
Output : [1,1,4,2,1,1,0,0]
```

---

### 7. Remove K Digits &nbsp;`Medium` &nbsp;·&nbsp; LC #402

> 💡 Remove k digits to form the smallest possible number. Pop when top > current and k > 0.

```java
Deque<Character> stack = new ArrayDeque<>();
int k = k;
for (char ch : num.toCharArray()) {
    while (k > 0 && !stack.isEmpty() && stack.peek() > ch) {
        stack.pop();
        k--;
    }
    stack.push(ch);
}
while (k-- > 0) stack.pollLast();   // remove from back if k still > 0

StringBuilder sb = new StringBuilder();
boolean leadingZero = true;
for (char c : stack) {
    if (leadingZero && c == '0') continue;
    leadingZero = false;
    sb.append(c);
}
return sb.length() == 0 ? "0" : sb.toString();
```

```
Input  : num = "1432219",  k = 3
Output : "1219"
```

---

### 8. Remove Duplicate Letters &nbsp;`Hard` &nbsp;·&nbsp; LC #316

> 💡 Stack + greedy + last occurrence tracking + visited set → lexicographically smallest result without duplicates.

```java
int[] lastIdx = new int[26];
boolean[] visited = new boolean[26];
for (int i = 0; i < s.length(); i++)
    lastIdx[s.charAt(i) - 'a'] = i;

Deque<Character> stack = new ArrayDeque<>();
for (int i = 0; i < s.length(); i++) {
    char ch = s.charAt(i);
    if (visited[ch - 'a']) continue;
    while (!stack.isEmpty()
           && stack.peek() > ch
           && lastIdx[stack.peek() - 'a'] > i) {
        visited[stack.pop() - 'a'] = false;
    }
    stack.push(ch);
    visited[ch - 'a'] = true;
}
StringBuilder sb = new StringBuilder();
while (!stack.isEmpty()) sb.append(stack.pop());
return sb.reverse().toString();
```

```
Input  : "bcabc"
Output : "abc"
```

---

## ⚡ Quick Reference Cheatsheet

### 🎯 3 Questions — For Any Problem

| | Question | Answer |
|--|----------|--------|
| **Q1** | What triggers a pop? | Special char (`#`, `*`) / Operator / Condition (collision, size) |
| **Q2** | What to store in stack? | Raw chars / indices / integers / computed values |
| **Q3** | How to read the result? | Reverse stack / Read top / Build during traversal |

---

### 📋 Problem → Pattern Map

| Problem | LC # | Stack Stores | Pop Condition | Difficulty |
|---------|------|-------------|---------------|------------|
| Backspace String Compare | 844 | `char` | on `#` | Easy |
| Removing Stars | 2390 | `char` | on `*` | Medium |
| Evaluate RPN | 150 | `int` | on operator | Medium |
| Asteroid Collision | 735 | `int` | opposite sign + size | Medium |
| Simplify Path | 71 | `String` | on `..` | Medium |
| Daily Temperatures | 739 | `int` index | `top < curr` | Medium |
| Remove K Digits | 402 | `char` | `top > curr` + k > 0 | Medium |
| Remove Duplicate Letters | 316 | `char` | `top > curr` + last occurs later | Hard |

---

### ⚠️ Common Mistakes — Avoid These

| ❌ Wrong | ✅ Correct |
|---------|-----------|
| Popping without checking `isEmpty()` | Always `!st.isEmpty()` before `pop()` or `peek()` |
| Wrong order of pop in RPN | Pop `b` first, then `a` → order matters for `-` and `/` |
| Asteroid: colliding same-sign asteroids | Collision only when top `> 0` AND current `< 0` |
| Using `Stack<T>` class | Use `Deque<T> = new ArrayDeque<>()` — faster |

---

### 📊 Complexity

| | Time | Space |
|-|------|-------|
| All Stack Simulation problems | **O(n)** | **O(n)** |

> Each element enters and leaves the stack at most once.
