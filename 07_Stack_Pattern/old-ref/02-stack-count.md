# 🗂 Pattern 2 — Stack + Count

> **Language:** Java &nbsp;|&nbsp; **Difficulty:** Easy → Medium &nbsp;|&nbsp; **Problems:** 8

---

## 📌 What is Stack + Count?

Store **`[char, count]` pairs** in the stack instead of just the character. When the count hits a threshold → pop. The key insight is that **cascading removal is handled automatically** — because after a pop, the two sides join and the new top might also now need to be popped.

---

## 💡 Core Insight — Remember These 3 Rules

| # | Rule | Why |
|---|------|-----|
| 1 | **Store pair, not just char** | You need to track how many consecutive same chars are grouped together. |
| 2 | **count == threshold → pop** | Entire group is removed at once. Cascade happens automatically on next iteration. |
| 3 | **Rebuild string at the end** | Reverse stack order first, then repeat each char by its stored count. |

---

## 🔀 See the Problem → Ask Only 2 Questions

| Question | Option A | Option B | Decision |
|----------|----------|----------|----------|
| **Q1:** What triggers removal? | Fixed k (k adjacent) | Dynamic (all adjacent) | `count == k` &nbsp;vs&nbsp; `count == 2` |
| **Q2:** What's stored in stack? | `[char, count]` pair | `(repeatNum, stringSoFar)` | Duplicate removal &nbsp;vs&nbsp; Decode |

---

## 📊 Variants — What Changes Per Problem

| Type | Stack Stores | Pop Condition | Problem |
|------|-------------|---------------|---------|
| K duplicate removal | `[char, count]` | `count == k` | LC 1209 |
| All adjacent removal | `char` only | same char as top | LC 1047 |
| Decode nested string | `(int, StringBuilder)` | on `]` bracket | LC 394 |
| Remove on symbol | `char` only | on `*` or `#` | LC 2390, 844 |

---

## 💻 Universal Java Template

```java
// ── BASE TEMPLATE — K duplicate removal ──────────────────────────────────
Deque<int[]> stack = new ArrayDeque<>();   // stores [char, count]

for (char ch : s.toCharArray()) {
    if (!stack.isEmpty() && stack.peek()[0] == ch) {
        stack.peek()[1]++;                  // increment count of top pair
        if (stack.peek()[1] == k)           // ← change threshold here
            stack.pop();                    // threshold hit → remove entire group
    } else {
        stack.push(new int[]{ch, 1});       // new char, count starts at 1
    }
}

// ── REBUILD STRING ────────────────────────────────────────────────────────
StringBuilder sb = new StringBuilder();
List<int[]> list = new ArrayList<>(stack);
Collections.reverse(list);                 // stack is LIFO — must reverse
for (int[] pair : list)
    for (int i = 0; i < pair[1]; i++)
        sb.append((char) pair[0]);
return sb.toString();
```

### ⚡ Only Change These — Everything Else Stays the Same

| Change Point | K removal | All adjacent | Decode string |
|-------------|-----------|--------------|---------------|
| Stack type | `Deque<int[]>` | `Deque<Character>` | `Deque<Integer>` + `Deque<StringBuilder>` |
| Pop condition | `count == k` | `same as top` | on `]` |
| Rebuild | reverse + repeat by count | reverse chars | built during traversal |

---

## 🧩 8 Problems

---

### 1. Remove All Adjacent Duplicates I &nbsp;`Easy` &nbsp;·&nbsp; LC #1047

> 💡 k = 2 fixed. No need to store count — just check if top equals current char.

```java
Deque<Character> stack = new ArrayDeque<>();
for (char ch : s.toCharArray()) {
    if (!stack.isEmpty() && stack.peek() == ch)
        stack.pop();
    else
        stack.push(ch);
}
StringBuilder sb = new StringBuilder();
while (!stack.isEmpty()) sb.append(stack.pop());
return sb.reverse().toString();
```

```
Input  : "abbaca"
Output : "ca"
```

---

### 2. Remove All Adjacent Duplicates II &nbsp;`Medium` &nbsp;·&nbsp; LC #1209

> 💡 k is variable — store `[char, count]`. When count reaches k → pop the group.

```java
Deque<int[]> stack = new ArrayDeque<>();
for (char ch : s.toCharArray()) {
    if (!stack.isEmpty() && stack.peek()[0] == ch) {
        stack.peek()[1]++;
        if (stack.peek()[1] == k) stack.pop();
    } else {
        stack.push(new int[]{ch, 1});
    }
}
StringBuilder sb = new StringBuilder();
List<int[]> list = new ArrayList<>(stack);
Collections.reverse(list);
for (int[] pair : list)
    for (int i = 0; i < pair[1]; i++)
        sb.append((char) pair[0]);
return sb.toString();
```

**Dry Run** — `"deeedbbcccbdaa"`, k = 3

| Char | Action | Stack |
|------|--------|-------|
| d | push new | `[(d,1)]` |
| e | push new | `[(e,1),(d,1)]` |
| e | count++ | `[(e,2),(d,1)]` |
| **e** | **count=3 → POP ✂️** | **`[(d,1)]`** |
| d | count++ | `[(d,2)]` |
| b, b | push, count++ | `[(b,2),(d,2)]` |
| c, c | push, count++ | `[(c,2),(b,2),(d,2)]` |
| **c** | **count=3 → POP ✂️** | **`[(b,2),(d,2)]`** |
| **b** | **count=3 → POP ✂️** | **`[(d,2)]`** |
| **d** | **count=3 → POP ✂️** | **`[]`** |
| a, a | push, count++ | `[(a,2)]` |

```
Output : "aa" ✅
```

---

### 3. Decode String &nbsp;`Medium` &nbsp;·&nbsp; LC #394

> 💡 `3[abc]` → `abcabcabc`. On `[` save state to stack. On `]` pop and repeat.

```java
Deque<Integer> counts = new ArrayDeque<>();
Deque<StringBuilder> strings = new ArrayDeque<>();
StringBuilder curr = new StringBuilder();
int k = 0;
for (char ch : s.toCharArray()) {
    if (Character.isDigit(ch)) {
        k = k * 10 + (ch - '0');
    } else if (ch == '[') {
        counts.push(k);
        strings.push(curr);
        curr = new StringBuilder();
        k = 0;
    } else if (ch == ']') {
        int times = counts.pop();
        StringBuilder prev = strings.pop();
        for (int i = 0; i < times; i++) prev.append(curr);
        curr = prev;
    } else {
        curr.append(ch);
    }
}
return curr.toString();
```

```
Input  : "3[a2[c]]"
Output : "accaccacc"
```

---

### 4. Removing Stars From a String &nbsp;`Medium` &nbsp;·&nbsp; LC #2390

> 💡 `*` = delete the character to its left → pop on `*`.

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

### 5. Backspace String Compare &nbsp;`Easy` &nbsp;·&nbsp; LC #844

> 💡 `#` = backspace → pop. Process both strings, then compare.

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

### 6. Score of Parentheses &nbsp;`Medium` &nbsp;·&nbsp; LC #856

> 💡 `()` = 1, `(X)` = 2×X. Stack stores the running score at each nesting level.

```java
Deque<Integer> stack = new ArrayDeque<>();
stack.push(0);
for (char ch : s.toCharArray()) {
    if (ch == '(') {
        stack.push(0);
    } else {
        int top = stack.pop();
        int val = top == 0 ? 1 : 2 * top;
        stack.push(stack.pop() + val);
    }
}
return stack.pop();
```

```
Input  : "(()(()))"
Output : 6
```

---

### 7. Valid Parentheses &nbsp;`Easy` &nbsp;·&nbsp; LC #20

> 💡 Push open brackets. On close bracket — must match top. Empty stack at end = valid.

```java
Deque<Character> stack = new ArrayDeque<>();
for (char ch : s.toCharArray()) {
    if (ch == '(' || ch == '{' || ch == '[')
        stack.push(ch);
    else {
        if (stack.isEmpty()) return false;
        char top = stack.pop();
        if (ch == ')' && top != '(') return false;
        if (ch == '}' && top != '{') return false;
        if (ch == ']' && top != '[') return false;
    }
}
return stack.isEmpty();
```

```
Input  : "()[]{}"  →  true
Input  : "(]"      →  false
```

---

### 8. Minimum Remove to Make Valid &nbsp;`Medium` &nbsp;·&nbsp; LC #1249

> 💡 Stack stores indices of unmatched brackets. Remove those positions from the string.

```java
Set<Integer> toRemove = new HashSet<>();
Deque<Integer> stack = new ArrayDeque<>();
for (int i = 0; i < s.length(); i++) {
    char ch = s.charAt(i);
    if      (ch == '(') stack.push(i);
    else if (ch == ')') {
        if (stack.isEmpty()) toRemove.add(i);
        else                 stack.pop();
    }
}
while (!stack.isEmpty()) toRemove.add(stack.pop());
StringBuilder sb = new StringBuilder();
for (int i = 0; i < s.length(); i++)
    if (!toRemove.contains(i)) sb.append(s.charAt(i));
return sb.toString();
```

```
Input  : "lee(t(c)o)de)"
Output : "lee(t(c)o)de"
```

---

## ⚡ Quick Reference Cheatsheet

### 🎯 3 Questions — For Any Problem

| | Question | Answer |
|--|----------|--------|
| **Q1** | What triggers removal? | Count hits k / Matching bracket / Special char (`*`, `#`) |
| **Q2** | What to store in stack? | `[char, count]` / index / char / `(count, string)` |
| **Q3** | Cascading needed? | Yes → automatic after pop. No extra loop needed. |

---

### 📋 Problem → Pattern Map

| Problem | LC # | Stack Stores | Pop Condition | Difficulty |
|---------|------|-------------|---------------|------------|
| Remove Adjacent I | 1047 | `char` | same as top | Easy |
| Remove Adjacent II | 1209 | `[char, count]` | `count == k` | Medium |
| Decode String | 394 | `(int, StringBuilder)` | on `]` | Medium |
| Removing Stars | 2390 | `char` | on `*` | Medium |
| Backspace Compare | 844 | `char` | on `#` | Easy |
| Score of Parentheses | 856 | `int` score | on `)` | Medium |
| Valid Parentheses | 20 | `char` bracket | mismatch | Easy |
| Min Remove to Valid | 1249 | `int` index | unmatched | Medium |

---

### ⚠️ Common Mistakes — Avoid These

| ❌ Wrong | ✅ Correct |
|---------|-----------|
| Storing just char in Stack+Count | Store `[char, count]` pair — you need both |
| Forgetting to reverse before rebuild | Stack is LIFO — `Collections.reverse()` before iterating |
| Writing extra loop for cascading | Cascading is automatic — new top is checked on next iteration |
| Using `Stack<Character>` | Use `Deque<Character> = new ArrayDeque<>()` |

---

### 📊 Complexity

| | Time | Space |
|-|------|-------|
| All Stack + Count problems | **O(n)** | **O(n)** |

> Single pass through string. Each character pushed and popped at most once.
