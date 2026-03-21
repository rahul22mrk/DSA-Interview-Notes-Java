# 🗂 Pattern 1 — Monotonic Stack

> **Language:** Java &nbsp;|&nbsp; **Difficulty:** Easy → Hard &nbsp;|&nbsp; **Problems:** 10

---

## 📌 What is Monotonic Stack?

A stack where elements are **always maintained in a sorted order** (either always increasing or always decreasing). Whenever the order breaks, we pop — and **popping means the answer for that element has been found.**

---

## 💡 Core Insight — Remember These 3 Rules

| # | Rule | Why |
|---|------|-----|
| 1 | **Push INDEX, not VALUE** | From index you can get value `arr[i]`, but from value you cannot get the index back. Index lets you calculate distance and width too. |
| 2 | **Pop = Answer Found** | When an element is popped, the current element `arr[i]` IS the answer for that popped element. |
| 3 | **Elements left in stack after loop** | They have no answer. Assign default `-1` or `0` based on the problem. |

---

## 🔀 See the Problem → Ask Only 2 Questions

| Question | Option A | Option B | Decision |
|----------|----------|----------|----------|
| **Q1:** Where is the answer? | Right side | Left side | Loop **L→R** &nbsp;vs&nbsp; **R→L** |
| **Q2:** What do you need? | Greater element | Smaller element | Condition `top < curr` &nbsp;vs&nbsp; `top > curr` |

---

## 📊 4 Variants — Only These 2 Things Change

| Type | Loop Direction | Pop Condition `(while)` | Store Result When |
|------|---------------|-------------------------|-------------------|
| Next Greater | L → R &nbsp;`(i = 0 to n-1)` | `arr[st.peek()] < arr[i]` | On pop: &nbsp;`result[st.pop()] = arr[i]` |
| Next Smaller | L → R &nbsp;`(i = 0 to n-1)` | `arr[st.peek()] > arr[i]` | On pop: &nbsp;`result[st.pop()] = arr[i]` |
| Prev Greater | R → L &nbsp;`(i = n-1 to 0)` | `arr[st.peek()] <= arr[i]` | Before push: &nbsp;`result[i] = arr[st.peek()]` |
| Prev Smaller | R → L &nbsp;`(i = n-1 to 0)` | `arr[st.peek()] >= arr[i]` | Before push: &nbsp;`result[i] = arr[st.peek()]` |

> **Special Variants**
> - 🔄 **Circular Array** → `2*n` loop + `i%n`
> - 📈 **Design Problem** (Stock Span) → store `[price, span]` in stack instead of index
> - ↔️ **Both Sides** (Sum Subarray Minimums) → use sentinel `0` at end

---

## 💻 Universal Java Template

```java
// ── BASE TEMPLATE — This part always stays the same ──────────────────────
Deque<Integer> st = new ArrayDeque<>();   // Stack<Integer> also works
int[] result = new int[n];
Arrays.fill(result, -1);                  // default answer = -1 (no result found)

// LOOP →
for (int i = 0; i < n; i++) {            // ← For Prev type: change to i = n-1 to 0

    // POP →
    while (!st.isEmpty() && arr[st.peek()] < arr[i]) {   // ← For Smaller: use >

        // ANSWER →
        int idx = st.pop();
        result[idx] = arr[i];             // need the value
        // result[idx] = i - idx;         // need the distance
        // int width = i - st.peek() - 1; // need the width
    }

    // PEEK → (only for Prev type)
    // result[i] = st.isEmpty() ? -1 : arr[st.peek()];

    // PUSH →
    st.push(i);                           // always push INDEX, never value
}
```

### ⚡ Only Change These — Everything Else Stays the Same

| Change Point | Next type | Prev type |
|-------------|-----------|-----------|
| Loop Direction | `i = 0 to n-1` &nbsp;(L→R) | `i = n-1 to 0` &nbsp;(R→L) |
| Pop Condition | `arr[st.peek()] < arr[i]` | `arr[st.peek()] <= arr[i]` |
| Result Line | `result[st.pop()] = arr[i]` &nbsp;(on pop) | `result[i] = arr[st.peek()]` &nbsp;(before push) |
| Push | `st.push(i)` — same | `st.push(i)` — same |

---

## 🧩 10 Problems — All Solved With One Template

---

### 1. Next Greater Element &nbsp; `Easy`

> 💡 First larger element to the right → traverse L to R, pop when a larger element arrives

| Loop | Condition | Result |
|------|-----------|--------|
| L → R &nbsp;`(i = 0 to n-1)` | `arr[st.peek()] < arr[i]` | `result[st.pop()] = arr[i]` &nbsp;— on pop |

```java
Deque<Integer> st = new ArrayDeque<>();
int[] result = new int[n];
Arrays.fill(result, -1);
for (int i = 0; i < n; i++) {
    while (!st.isEmpty() && arr[st.peek()] < arr[i])
        result[st.pop()] = arr[i];
    st.push(i);
}
```

```
Input  : [3, 1, 4, 2, 5]
Output : [4, 4, 5, 5, -1]
```

---

### 2. Daily Temperatures &nbsp; `Medium` &nbsp; · &nbsp; LC #739

> 💡 Same as Next Greater — but need INDEX DIFFERENCE (distance), not the value itself

| Loop | Condition | Result |
|------|-----------|--------|
| L → R &nbsp;`(i = 0 to n-1)` | `arr[st.peek()] < arr[i]` | `result[st.pop()] = i - idx` &nbsp;— distance |

```java
Deque<Integer> st = new ArrayDeque<>();
int[] result = new int[n];   // default 0
for (int i = 0; i < n; i++) {
    while (!st.isEmpty() && arr[st.peek()] < arr[i]) {
        int idx = st.pop();
        result[idx] = i - idx;   // distance, not value
    }
    st.push(i);
}
```

```
Input  : [73, 74, 75, 71, 69, 72, 76, 73]
Output : [1, 1, 4, 2, 1, 1, 0, 0]
```

---

### 3. Previous Greater Element &nbsp; `Easy`

> 💡 Larger element to the left → traverse R to L, stack top before push is the answer

| Loop | Condition | Result |
|------|-----------|--------|
| R → L &nbsp;`(i = n-1 to 0)` | `arr[st.peek()] <= arr[i]` | `result[i] = arr[st.peek()]` &nbsp;— before push |

```java
Deque<Integer> st = new ArrayDeque<>();
int[] result = new int[n];
Arrays.fill(result, -1);
for (int i = n - 1; i >= 0; i--) {
    while (!st.isEmpty() && arr[st.peek()] <= arr[i])
        st.pop();
    result[i] = st.isEmpty() ? -1 : arr[st.peek()];
    st.push(i);
}
```

```
Input  : [3, 1, 4, 2, 5]
Output : [-1, 3, -1, 4, -1]
```

---

### 4. Next Smaller Element &nbsp; `Easy`

> 💡 Opposite of Next Greater — just flip `<` to `>`

| Loop | Condition | Result |
|------|-----------|--------|
| L → R &nbsp;`(i = 0 to n-1)` | `arr[st.peek()] > arr[i]` | `result[st.pop()] = arr[i]` &nbsp;— on pop |

```java
Deque<Integer> st = new ArrayDeque<>();
int[] result = new int[n];
Arrays.fill(result, -1);
for (int i = 0; i < n; i++) {
    while (!st.isEmpty() && arr[st.peek()] > arr[i])
        result[st.pop()] = arr[i];
    st.push(i);
}
```

```
Input  : [3, 1, 4, 2, 5]
Output : [1, -1, 2, -1, -1]
```

---

### 5. Stock Span Problem &nbsp; `Medium` &nbsp; · &nbsp; LC #901

> 💡 How many consecutive days was price `<=` today? Need index of Previous Greater → span = `i - prev_index`

| Loop | Condition | Result |
|------|-----------|--------|
| L → R &nbsp;`(i = 0 to n-1)` | `arr[st.peek()] <= arr[i]` | `result[i] = i - st.peek()` &nbsp;— before push |

```java
Deque<Integer> st = new ArrayDeque<>();
int[] result = new int[n];
for (int i = 0; i < n; i++) {
    while (!st.isEmpty() && arr[st.peek()] <= arr[i])
        st.pop();
    result[i] = st.isEmpty() ? i + 1 : i - st.peek();
    st.push(i);
}
```

```
Input  : [100, 80, 60, 70, 60, 75, 85]
Output : [1, 1, 1, 2, 1, 4, 6]
```

---

### 6. Largest Rectangle in Histogram &nbsp; `Hard` &nbsp; · &nbsp; LC #84

> 💡 When a shorter bar appears → pop and calculate area. Width = `current_i - new_top - 1`. Sentinel `0` at the end forces all bars to be processed.

| Loop | Condition | Result |
|------|-----------|--------|
| L → R &nbsp;`(i = 0 to n, sentinel 0)` | `arr[st.peek()] > h` | `area = height × (i - st.peek() - 1)` |

```java
Deque<Integer> st = new ArrayDeque<>();
st.push(-1);   // sentinel
int maxArea = 0;
for (int i = 0; i <= n; i++) {
    int h = (i == n) ? 0 : arr[i];
    while (st.peek() != -1 && arr[st.peek()] > h) {
        int height = arr[st.pop()];
        int width  = i - st.peek() - 1;
        maxArea = Math.max(maxArea, height * width);
    }
    st.push(i);
}
```

```
Input  : [2, 1, 5, 6, 2, 3]
Output : maxArea = 10
```

---

### 7. Next Greater Element II — Circular &nbsp; `Medium` &nbsp; · &nbsp; LC #503

> 💡 Traverse twice (`2*n`). Use `i%n` for actual index. Do NOT push in the second pass.

| Loop | Condition | Result |
|------|-----------|--------|
| L → R &nbsp;`(i = 0 to 2*n-1)` | `nums[st.peek()] < nums[i % n]` | `result[st.pop()] = nums[i % n]` &nbsp;— on pop |

```java
Deque<Integer> st = new ArrayDeque<>();
int[] result = new int[n];
Arrays.fill(result, -1);
for (int i = 0; i < 2 * n; i++) {
    while (!st.isEmpty() && nums[st.peek()] < nums[i % n])
        result[st.pop()] = nums[i % n];
    if (i < n) st.push(i);   // push only in 1st pass
}
```

```
Input  : [1, 2, 1]
Output : [2, -1, 2]
```

---

### 8. Online Stock Span &nbsp; `Medium` &nbsp; · &nbsp; LC #901

> 💡 No index available — prices arrive one at a time. Store `[price, span]` in stack. Accumulate span on pop.

| Loop | Condition | Result |
|------|-----------|--------|
| One price at a time | `st.peek()[0] <= price` | `span += st.pop()[1]` &nbsp;— add popped span |

```java
Deque<int[]> st = new ArrayDeque<>();   // [price, span]

public int next(int price) {
    int span = 1;
    while (!st.isEmpty() && st.peek()[0] <= price)
        span += st.pop()[1];   // accumulate span
    st.push(new int[]{price, span});
    return span;
}
```

```
Input  : [100, 80, 60, 70, 60, 75, 85]
Output : [1, 1, 1, 2, 1, 4, 6]
```

---

### 9. Trapping Rain Water &nbsp; `Hard` &nbsp; · &nbsp; LC #42

> 💡 Popped element = valley (bottom). New stack top = left wall. Current `i` = right wall. Water = `(min(left, right) - bottom) × width`

| Loop | Condition | Result |
|------|-----------|--------|
| L → R &nbsp;`(i = 0 to n-1)` | `height[st.peek()] < height[i]` | `water += (min(left, right) - bottom) × width` |

```java
Deque<Integer> st = new ArrayDeque<>();
int water = 0;
for (int i = 0; i < n; i++) {
    while (!st.isEmpty() && height[st.peek()] < height[i]) {
        int bottom = height[st.pop()];
        if (st.isEmpty()) break;
        int left  = height[st.peek()];
        int right = height[i];
        int width = i - st.peek() - 1;
        water += (Math.min(left, right) - bottom) * width;
    }
    st.push(i);
}
return water;
```

```
Input  : [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]
Output : 6
```

---

### 10. Sum of Subarray Minimums &nbsp; `Medium` &nbsp; · &nbsp; LC #907

> 💡 For each element — how many subarrays is it the minimum of? `left = idx - prev_smaller`, `right = next_smaller - idx`. Contribution = `arr[idx] × left × right`. Use MOD = 1e9+7.

| Loop | Condition | Result |
|------|-----------|--------|
| L → R &nbsp;`(i = 0 to n, sentinel)` | `arr[st.peek()] > curr` &nbsp;(both sides needed) | `arr[idx] × left × right` |

```java
int MOD = (int) 1e9 + 7;
Deque<Integer> st = new ArrayDeque<>();
long result = 0;
for (int i = 0; i <= n; i++) {
    int curr = (i == n) ? 0 : arr[i];   // sentinel forces all pops
    while (!st.isEmpty() && arr[st.peek()] > curr) {
        int idx   = st.pop();
        int left  = idx - (st.isEmpty() ? -1 : st.peek());
        int right = i - idx;
        result = (result + (long) arr[idx] * left * right) % MOD;
    }
    st.push(i);
}
return (int) result;
```

```
Input  : [3, 1, 2, 4]
Output : 17
```

---

## ⚡ Quick Reference Cheatsheet

### 🎯 3 Questions — For Any Problem

| | Question | Answer |
|--|----------|--------|
| **Q1** | What are we looking for? | Nearest Greater / Nearest Smaller / Distance to next / Width of range |
| **Q2** | Where is the answer — right or left? | Right → L to R loop &nbsp;·&nbsp; Left → R to L loop |
| **Q3** | Greater or Smaller? | Greater → `pop when top < current` &nbsp;·&nbsp; Smaller → `pop when top > current` |

---

### 📋 Problem → Pattern Map

| Problem | LC # | Loop | Pop Condition | Result Store | Push |
|---------|------|------|---------------|--------------|------|
| Next Greater Element | 496 | L→R | `top < curr` | on pop | INDEX |
| Daily Temperatures | 739 | L→R | `top < curr` | on pop (dist) | INDEX |
| Previous Greater Element | — | R→L | `top <= curr` | before push | INDEX |
| Next Smaller Element | — | L→R | `top > curr` | on pop | INDEX |
| Stock Span | 901 | L→R | `top <= curr` | before push | INDEX |
| Largest Rectangle | 84 | L→R | `top > curr` | on pop (area) | INDEX |
| Trapping Rain Water | 42 | L→R | `top < curr` | on pop (area) | INDEX |
| Remove K Digits | 402 | L→R | `top > curr` | pop it | VALUE |
| Next Greater II (Circular) | 503 | L→R `2*n` | `top < curr (i%n)` | on pop | INDEX |
| Online Stock Span | 901 | L→R | `top[0] <= price` | accumulate span | `[p,span]` |
| Sum of Subarray Minimums | 907 | L→R | `top > curr` | `val × left × right` | INDEX |

---

### ⚠️ Common Mistakes — Avoid These

| ❌ Wrong | ✅ Correct |
|---------|-----------|
| Using `Stack<Integer>` | Use `Deque<Integer> st = new ArrayDeque<>()` — faster, Java recommended |
| Pushing value `st.push(arr[i])` | Push index `st.push(i)` — distance/width cannot be calculated otherwise |
| Ignoring stack after loop ends | Remaining elements have no answer — default `-1` is already set |
| Calling `peek()` without `isEmpty()` | Always check `!st.isEmpty()` first — NPE will occur otherwise |

---

### 📊 Complexity

| | Time | Space |
|-|------|-------|
| All monotonic stack problems | **O(n)** | **O(n)** |

> Each element is pushed **once** and popped **at most once** → O(n) guaranteed.
