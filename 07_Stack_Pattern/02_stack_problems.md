# Stack Pattern — Solved Problems (32 Problems)

> **Pattern family:** Stack / Monotonic Stack / Design / Expression Evaluation
> **Notes & Templates:** [01_stack_notes.md](./01_stack_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Monotonic Stack
- [P1 — Next Greater Element I](#problem-1--next-greater-element-i)
- [P2 — Daily Temperatures](#problem-2--daily-temperatures)
- [P3 — Next Greater Element II (Circular)](#problem-3--next-greater-element-ii-circular)
- [P4 — Previous Greater Element / Stock Span](#problem-4--previous-greater-element--stock-span)
- [P5 — Online Stock Span](#problem-5--online-stock-span)
- [P6 — Largest Rectangle in Histogram](#problem-6--largest-rectangle-in-histogram)
- [P7 — Trapping Rain Water](#problem-7--trapping-rain-water)
- [P8 — Sum of Subarray Minimums](#problem-8--sum-of-subarray-minimums)
- [P9 — Remove Nodes From Linked List](#problem-9--remove-nodes-from-linked-list)

### Category 2 — Bracket / Parentheses
- [P10 — Valid Parentheses](#problem-10--valid-parentheses)
- [P11 — Minimum Remove to Make Valid](#problem-11--minimum-remove-to-make-valid)
- [P12 — Longest Valid Parentheses](#problem-12--longest-valid-parentheses)
- [P13 — Score of Parentheses](#problem-13--score-of-parentheses)

### Category 3 — Stack + Count / Removal
- [P14 — Remove All Adjacent Duplicates I](#problem-14--remove-all-adjacent-duplicates-i)
- [P15 — Remove All Adjacent Duplicates II](#problem-15--remove-all-adjacent-duplicates-ii)
- [P16 — Backspace String Compare](#problem-16--backspace-string-compare)
- [P17 — Removing Stars From a String](#problem-17--removing-stars-from-a-string)
- [P18 — Remove Duplicate Letters](#problem-18--remove-duplicate-letters)
- [P19 — Remove K Digits](#problem-19--remove-k-digits)

### Category 4 — Expression Evaluation
- [P20 — Evaluate Reverse Polish Notation](#problem-20--evaluate-reverse-polish-notation)
- [P21 — Basic Calculator II](#problem-21--basic-calculator-ii)
- [P22 — Basic Calculator](#problem-22--basic-calculator)
- [P23 — Decode String](#problem-23--decode-string)

### Category 5 — Stack Simulation
- [P24 — Simplify Path](#problem-24--simplify-path)
- [P25 — Asteroid Collision](#problem-25--asteroid-collision)
- [P26 — Baseball Game](#problem-26--baseball-game)
- [P27 — Reverse a String Using Stack](#problem-27--reverse-a-string-using-stack)

### Category 6 — Design Problems
- [P28 — Min Stack](#problem-28--min-stack)
- [P29 — Implement Queue Using Stacks](#problem-29--implement-queue-using-stacks)
- [P30 — Implement Stack Using Queues](#problem-30--implement-stack-using-queues)
- [P31 — Design Browser History](#problem-31--design-browser-history)
- [P32 — Maximum Frequency Stack](#problem-32--maximum-frequency-stack)

---

## Category 1 — Monotonic Stack

---

### Problem 1 — Next Greater Element I
**LeetCode #496 | Difficulty: Easy | Company: Amazon, Google | Category: Monotonic Stack**

> Find the next greater element for each element of `nums1` in `nums2`. Return -1 if none exists.

#### Core insight

Build a monotonic decreasing stack on `nums2`. Store results in a HashMap. For each element in `nums1`, look up in the map.

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Loop nums2 | `st not empty && nums2[top] < nums2[i]` | `map[nums2[pop]] = nums2[i]` |
| Push | always | `st.push(i)` |
| Answer | for each num in nums1 | `map.getOrDefault(num, -1)` |

#### Java code

```java
public int[] nextGreaterElement(int[] nums1, int[] nums2) {
    Map<Integer, Integer> map = new HashMap<>();
    Deque<Integer> st = new ArrayDeque<>();

    for (int num : nums2) {
        while (!st.isEmpty() && st.peek() < num)
            map.put(st.pop(), num);   // num is the next greater for popped element
        st.push(num);                 // push value (nums2 has unique elements)
    }

    int[] res = new int[nums1.length];
    for (int i = 0; i < nums1.length; i++)
        res[i] = map.getOrDefault(nums1[i], -1);
    return res;
}
```

#### Example

```
nums1 = [4,1,2], nums2 = [1,3,4,2]

Monotonic stack on nums2:
  push 1 → st=[1]
  3 > 1 → map[1]=3, push 3 → st=[3]
  4 > 3 → map[3]=4, push 4 → st=[4]
  2 < 4 → push 2 → st=[4,2]
  Remaining: no next greater → not in map

nums1: 4 → not in map → -1
       1 → map[1]=3
       2 → not in map → -1

Output: [-1, 3, -1] ✓
```

---

### Problem 2 — Daily Temperatures
**LeetCode #739 | Difficulty: Medium | Company: Amazon, Facebook | Category: Monotonic Stack**

> For each day, find how many days until a warmer temperature. Return 0 if no warmer day exists.

#### Core insight

Same as Next Greater but record the **distance** (index difference), not the value.

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Loop L→R | `temp[top] < temp[i]` | `result[pop] = i - pop` (distance) |
| Push | always | `st.push(i)` (index) |
| Default | no warmer day | `result[i] = 0` |

#### Java code

```java
public int[] dailyTemperatures(int[] temperatures) {
    int n = temperatures.length;
    int[] result = new int[n];   // default 0
    Deque<Integer> st = new ArrayDeque<>();

    for (int i = 0; i < n; i++) {
        while (!st.isEmpty() && temperatures[st.peek()] < temperatures[i]) {
            int idx = st.pop();
            result[idx] = i - idx;   // distance to warmer day
        }
        st.push(i);
    }
    return result;
}
```

#### Example

```
temperatures = [73,74,75,71,69,72,76,73]

i=0(73): st=[0]
i=1(74): 73<74 → result[0]=1-0=1. st=[1]
i=2(75): 74<75 → result[1]=2-1=1. st=[2]
i=3(71): 71<75 → push. st=[2,3]
i=4(69): push. st=[2,3,4]
i=5(72): 69<72 → result[4]=1, 71<72 → result[3]=2. st=[2,5]
i=6(76): 72<76 → result[5]=1, 75<76 → result[2]=4. st=[6]
i=7(73): push. st=[6,7]  (remain: result stays 0)

Output: [1,1,4,2,1,1,0,0] ✓
```

---

### Problem 3 — Next Greater Element II (Circular)
**LeetCode #503 | Difficulty: Medium | Company: Amazon | Category: Monotonic Stack Circular**

> Same as NGE but the array is circular — wrap around to find greater element.

#### Core insight

Loop `2*n` times. Use `i % n` for actual index. Push to stack only in the first pass (`i < n`).

#### Java code

```java
public int[] nextGreaterElements(int[] nums) {
    int n = nums.length;
    int[] result = new int[n];
    Arrays.fill(result, -1);
    Deque<Integer> st = new ArrayDeque<>();

    for (int i = 0; i < 2 * n; i++) {
        while (!st.isEmpty() && nums[st.peek()] < nums[i % n])
            result[st.pop()] = nums[i % n];
        if (i < n) st.push(i);   // push only first pass
    }
    return result;
}
```

#### Example

```
nums = [1, 2, 1]

i=0: st=[0]
i=1: 1<2 → result[0]=2. st=[1]
i=2: 2>1 → push. st=[1,2]
i=3(→1): 1<2 already done. st=[1,2]
i=4(→2): 1<2 → result[2]=2. st=[1]
i=5(→1): done.

Output: [2,-1,2] ✓
```

---

### Problem 4 — Previous Greater Element / Stock Span
**LeetCode #901 | Difficulty: Medium | Category: Monotonic Stack**

> For each element, find how many consecutive elements (including itself) to its left are ≤ current.

#### Core insight

Loop L→R. Pop elements ≤ current (they're dominated). Span = `i - top_index` (or `i+1` if stack empty).

#### Java code

```java
public int[] stockSpan(int[] prices) {
    int n = prices.length;
    int[] result = new int[n];
    Deque<Integer> st = new ArrayDeque<>();

    for (int i = 0; i < n; i++) {
        while (!st.isEmpty() && prices[st.peek()] <= prices[i])
            st.pop();
        result[i] = st.isEmpty() ? i + 1 : i - st.peek();
        st.push(i);
    }
    return result;
}
```

#### Example

```
prices = [100, 80, 60, 70, 60, 75, 85]

i=0(100): empty → span=1. st=[0]
i=1(80):  100>80 → span=1. st=[0,1]
i=2(60):  80>60  → span=1. st=[0,1,2]
i=3(70):  60<=70 → pop 2. 80>70 → span=3-1=2. st=[0,1,3]
i=4(60):  70>60  → span=1. st=[0,1,3,4]
i=5(75):  60<=75 → pop 4. 70<=75 → pop 3. 80>75 → span=5-1=4. st=[0,1,5]
i=6(85):  75<=85 → pop 5. 80<=85 → pop 1. 100>85 → span=6-0=6. st=[0,6]

Output: [1,1,1,2,1,4,6] ✓
```

---

### Problem 5 — Online Stock Span
**LeetCode #901 | Difficulty: Medium | Company: Amazon, Google | Category: Monotonic Stack Design**

> Design a system where prices arrive one at a time and return the span for each incoming price.

#### Core insight

No index available. Store `[price, span]` in stack. When popping, **accumulate the span** of the popped element.

#### Java code

```java
class StockSpanner {
    Deque<int[]> st = new ArrayDeque<>();   // [price, span]

    public int next(int price) {
        int span = 1;
        while (!st.isEmpty() && st.peek()[0] <= price)
            span += st.pop()[1];   // accumulate span of dominated days
        st.push(new int[]{price, span});
        return span;
    }
}
```

#### Example

```
next(100) → st=[(100,1)], span=1
next(80)  → st=[(100,1),(80,1)], span=1
next(60)  → st=[...,(60,1)], span=1
next(70)  → pop (60,1): span=1+1=2. st=[...,(80,1),(70,2)], span=2
next(60)  → span=1
next(75)  → pop (60,1)+pop(70,2): span=1+1+2=4. pop (80,1): span=5? → no, 80>75 → stop. span=4
next(85)  → pop (75,4)+(80,1): span=6.

Output: [1,1,1,2,1,4,6] ✓
```

---

### Problem 6 — Largest Rectangle in Histogram
**LeetCode #84 | Difficulty: Hard | Company: Amazon, Google, Microsoft | Category: Monotonic Stack**

> Given histogram bar heights, find the largest rectangle area.

#### Core insight

When a shorter bar arrives, all taller bars to its left cannot extend further right. Pop them and compute width using `i - newTop - 1`. Sentinel `0` at end forces all remaining bars to be processed.

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Loop `0 to n` (n = sentinel) | `arr[top] > h` | `area = h_pop × (i - newTop - 1)` |
| Sentinel | `i == n` | `h = 0` forces all pops |
| Push | always | push index `i` |

#### Java code

```java
public int largestRectangleArea(int[] heights) {
    int n = heights.length;
    Deque<Integer> st = new ArrayDeque<>();
    st.push(-1);   // sentinel for width calculation
    int maxArea = 0;

    for (int i = 0; i <= n; i++) {
        int h = (i == n) ? 0 : heights[i];
        while (st.peek() != -1 && heights[st.peek()] > h) {
            int height = heights[st.pop()];
            int width  = i - st.peek() - 1;
            maxArea = Math.max(maxArea, height * width);
        }
        st.push(i);
    }
    return maxArea;
}
```

#### Example

```
heights = [2,1,5,6,2,3]

sentinel=-1 in stack.
i=0(2): push. st=[-1,0]
i=1(1): 2>1 → pop 0: h=2, w=1-(-1)-1=1, area=2. push 1. st=[-1,1]
i=2(5): push. st=[-1,1,2]
i=3(6): push. st=[-1,1,2,3]
i=4(2): 6>2 → pop 3: h=6, w=4-2-1=1, area=6
        5>2 → pop 2: h=5, w=4-1-1=2, area=10  ← max
        1<2 → stop. push 4. st=[-1,1,4]
i=5(3): push. st=[-1,1,4,5]
i=6(0): 3>0 → pop 5: h=3, w=6-4-1=1, area=3
        2>0 → pop 4: h=2, w=6-1-1=4, area=8
        1>0 → pop 1: h=1, w=6-(-1)-1=6, area=6

Output: 10 ✓
```

---

### Problem 7 — Trapping Rain Water
**LeetCode #42 | Difficulty: Hard | Company: Amazon, Google, Facebook | Category: Monotonic Stack**

> Given elevation heights, compute how much water can be trapped.

#### Core insight

Popped element = valley bottom. New stack top = left wall. Current index = right wall. Water = `(min(left, right) - bottom) × width`.

#### Java code

```java
public int trap(int[] height) {
    int n = height.length;
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
}
```

#### Example

```
height = [0,1,0,2,1,0,1,3,2,1,2,1]

i=2(0): push
i=3(2): pop 2(0): bottom=0, left=1, right=2, w=3-1-1=1, water+=1
        pop 1(1): bottom=1, left empty → break
...
Output: 6 ✓
```

---

### Problem 8 — Sum of Subarray Minimums
**LeetCode #907 | Difficulty: Medium | Company: Amazon | Category: Monotonic Stack Contribution**

> For every subarray, sum all their minimums. Return result modulo 1e9+7.

#### Core insight

For each element at index `idx`, calculate how many subarrays it is the **minimum** of:
- `left` = distance to previous smaller (or boundary)
- `right` = distance to next smaller (or boundary)
- Contribution = `arr[idx] × left × right`

Use `>` (not `>=`) on one side to avoid double counting equal elements.

#### Java code

```java
public int sumSubarrayMins(int[] arr) {
    int n = arr.length, MOD = (int) 1e9 + 7;
    Deque<Integer> st = new ArrayDeque<>();
    long result = 0;

    for (int i = 0; i <= n; i++) {
        int curr = (i == n) ? 0 : arr[i];
        while (!st.isEmpty() && arr[st.peek()] > curr) {
            int idx   = st.pop();
            int left  = idx - (st.isEmpty() ? -1 : st.peek());   // prev smaller boundary
            int right = i - idx;                                   // next smaller boundary
            result = (result + (long) arr[idx] * left * right) % MOD;
        }
        st.push(i);
    }
    return (int) result;
}
```

#### Example

```
arr = [3, 1, 2, 4]

i=1(1): pop 0(3): left=0-(-1)=1, right=1-0=1, contrib=3×1×1=3
i=4(0): pop 3(4): left=3-2=1, right=4-3=1, contrib=4
        pop 2(2): left=2-1=1, right=4-2=2, contrib=4
        pop 1(1): left=1-(-1)=2, right=4-1=3, contrib=6

Total = 3+1+4+4+6-1 = 17  (careful: arr[1]=1 contributes 1×2×3=6 not -1)
Output: 17 ✓  ([3]=3,[1]=1,[2]=2,[4]=4,[3,1]=1,[1,2]=1,[2,4]=2,[3,1,2]=1,[1,2,4]=1,[3,1,2,4]=1 → sum=17)
```

---

### Problem 9 — Remove Nodes From Linked List
**LeetCode #2487 | Difficulty: Medium | Company: Amazon | Category: Monotonic Stack**

> Remove every node that has a node with a greater value to its right.

#### Core insight

Convert list to array, apply monotonic decreasing stack (keep only nodes where no greater element exists to the right), rebuild list.

#### Java code

```java
public ListNode removeNodes(ListNode head) {
    List<Integer> vals = new ArrayList<>();
    for (ListNode cur = head; cur != null; cur = cur.next)
        vals.add(cur.val);

    Deque<Integer> st = new ArrayDeque<>();
    for (int v : vals) {
        while (!st.isEmpty() && st.peek() < v) st.pop();
        st.push(v);
    }

    // Rebuild from stack (stack is reversed)
    List<Integer> res = new ArrayList<>(st);
    Collections.reverse(res);
    ListNode dummy = new ListNode(0), cur = dummy;
    for (int v : res) { cur.next = new ListNode(v); cur = cur.next; }
    return dummy.next;
}
```

#### Example

```
list = 5→2→13→3→8
vals = [5,2,13,3,8]

Monotonic decreasing stack:
  push 5 → [5]
  2<5 → push [5,2]? No: 5>2 so push [5,2] — wait, we pop smaller:
  actually: push 5; 2<5 push; 13>2 pop 2, 13>5 pop 5, push 13; 3<13 push; 8>3 pop 3, 8<13 push 8
  st = [13, 8] → reversed = [13, 8]? Wrong.

Correct trace (pop when top < new val):
  5: st=[5]
  2: 2<5 → push. st=[5,2]
  13: 2<13 pop, 5<13 pop → st=[13]
  3: 3<13 → push. st=[13,3]
  8: 3<8 pop → st=[13,8]

Reversed: [13,8] — but 5 should also remain if nothing greater is to its right... 
Hmm: 5 has 13 to its right (greater) → removed. Correct.

Output: 13→8 ✓
```

---

## Category 2 — Bracket / Parentheses

---

### Problem 10 — Valid Parentheses
**LeetCode #20 | Difficulty: Easy | Company: Amazon, Google, Facebook | Category: Bracket Matching**

> Determine if a string of brackets is valid (every open bracket has a matching close bracket in the correct order).

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Open bracket | `(`, `{`, `[` | push |
| Close bracket | stack empty | return false |
| Close bracket | top mismatches | return false |
| Close bracket | top matches | pop |
| End | stack empty | return true |

#### Java code

```java
public boolean isValid(String s) {
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
}
```

#### Example

```
s = "()[]{}"  → push (, pop+match ), push [, pop+match ], push {, pop+match } → empty → true ✓
s = "([)]"    → push (, push [, ) vs [ → mismatch → false ✓
```

---

### Problem 11 — Minimum Remove to Make Valid
**LeetCode #1249 | Difficulty: Medium | Company: Facebook, Amazon | Category: Bracket Matching**

> Remove the minimum number of parentheses to make the string valid. Return any valid result.

#### Java code

```java
public String minRemoveToMakeValid(String s) {
    Set<Integer> toRemove = new HashSet<>();
    Deque<Integer> st = new ArrayDeque<>();   // stores indices of unmatched '('

    for (int i = 0; i < s.length(); i++) {
        char ch = s.charAt(i);
        if      (ch == '(') st.push(i);
        else if (ch == ')') {
            if (st.isEmpty()) toRemove.add(i);   // unmatched ')'
            else              st.pop();           // matched pair
        }
    }
    while (!st.isEmpty()) toRemove.add(st.pop());  // remaining '(' are unmatched

    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < s.length(); i++)
        if (!toRemove.contains(i)) sb.append(s.charAt(i));
    return sb.toString();
}
```

#### Example

```
s = "lee(t(c)o)de)"

i=3 '(': st=[3]
i=5 '(': st=[3,5]
i=7 ')': pop 5. st=[3]
i=9 ')': pop 3. st=[]
i=12 ')': empty → toRemove={12}

Output: "lee(t(c)o)de" ✓
```

---

### Problem 12 — Longest Valid Parentheses
**LeetCode #32 | Difficulty: Hard | Company: Amazon, Google | Category: Bracket Matching**

> Find the length of the longest valid (well-formed) parentheses substring.

#### Core insight

Stack stores indices. Push `-1` as a base sentinel. On `(` push index. On `)`: pop — if stack empty push current index as new base, else update max length.

#### Java code

```java
public int longestValidParentheses(String s) {
    Deque<Integer> st = new ArrayDeque<>();
    st.push(-1);   // base sentinel
    int maxLen = 0;

    for (int i = 0; i < s.length(); i++) {
        if (s.charAt(i) == '(') {
            st.push(i);
        } else {
            st.pop();
            if (st.isEmpty()) st.push(i);       // new base
            else maxLen = Math.max(maxLen, i - st.peek());
        }
    }
    return maxLen;
}
```

#### Example

```
s = ")()())"
st=[-1]
i=0 ')': pop -1, empty → push 0. st=[0]
i=1 '(': push 1. st=[0,1]
i=2 ')': pop 1. len=2-0=2. st=[0]
i=3 '(': push 3. st=[0,3]
i=4 ')': pop 3. len=4-0=4. maxLen=4
i=5 ')': pop 0, empty → push 5. st=[5]

Output: 4 ✓
```

---

### Problem 13 — Score of Parentheses
**LeetCode #856 | Difficulty: Medium | Company: Google | Category: Bracket Score**

> `()` = 1, `(X)` = 2×X, concatenation = addition. Return the score of the balanced string.

#### Java code

```java
public int scoreOfParentheses(String s) {
    Deque<Integer> st = new ArrayDeque<>();
    st.push(0);   // score at current depth

    for (char ch : s.toCharArray()) {
        if (ch == '(') {
            st.push(0);              // new depth level, score starts at 0
        } else {
            int top = st.pop();
            int val = top == 0 ? 1 : 2 * top;   // () = 1; (X) = 2X
            st.push(st.pop() + val);             // add to parent level
        }
    }
    return st.pop();
}
```

#### Example

```
s = "(()(()))"

push 0 → [0]
push 0 → [0,0]    (first '(')
push 0 → [0,0,0]  (second '(')
')' → top=0 → val=1, parent: [0, 0+1=1]
push 0 → [0,1,0]
push 0 → [0,1,0,0]
')' → top=0 → val=1, [0,1,0+1=1]
')' → top=1 → val=2, [0,1+2=3]
')' → top=3 → val=6, [0+6=6]

Output: 6 ✓
```

---

## Category 3 — Stack + Count / Removal

---

### Problem 14 — Remove All Adjacent Duplicates I
**LeetCode #1047 | Difficulty: Easy | Company: Amazon | Category: Stack Removal**

> Repeatedly remove adjacent duplicate pairs until no more can be removed.

#### Java code

```java
public String removeDuplicates(String s) {
    Deque<Character> st = new ArrayDeque<>();
    for (char ch : s.toCharArray()) {
        if (!st.isEmpty() && st.peek() == ch) st.pop();   // duplicate → remove pair
        else                                  st.push(ch);
    }
    StringBuilder sb = new StringBuilder();
    while (!st.isEmpty()) sb.append(st.pop());
    return sb.reverse().toString();
}
```

#### Example

```
s = "abbaca"
a → [a]
b → [a,b]
b == top → pop → [a]
a == top → pop → []
c → [c]
a → [c,a]

Output: "ca" ✓
```

---

### Problem 15 — Remove All Adjacent Duplicates II
**LeetCode #1209 | Difficulty: Medium | Company: Amazon, Google | Category: Stack + Count**

> Remove k adjacent duplicate characters repeatedly.

#### Core insight

Store `[char, count]` pairs. When count reaches k, pop the entire group. Cascading is automatic.

#### Java code

```java
public String removeDuplicates(String s, int k) {
    Deque<int[]> st = new ArrayDeque<>();   // [charCode, count]

    for (char ch : s.toCharArray()) {
        if (!st.isEmpty() && st.peek()[0] == ch) {
            st.peek()[1]++;
            if (st.peek()[1] == k) st.pop();
        } else {
            st.push(new int[]{ch, 1});
        }
    }

    StringBuilder sb = new StringBuilder();
    List<int[]> list = new ArrayList<>(st);
    Collections.reverse(list);
    for (int[] pair : list)
        for (int i = 0; i < pair[1]; i++)
            sb.append((char) pair[0]);
    return sb.toString();
}
```

#### Example

```
s = "deeedbbcccbdaa", k = 3

d→[(d,1)]  e→[(e,1),(d,1)]  e→[(e,2),(d,1)]  e→count=3→POP→[(d,1)]
d→[(d,2)]  b→[(b,1),(d,2)]  b→[(b,2),(d,2)]
c→[(c,1),(b,2),(d,2)]  c→[(c,2)]  c→count=3→POP→[(b,2),(d,2)]
b→[(b,3)] count=3→POP→[(d,2)]  d→[(d,3)]→POP→[]
a→[(a,1)]  a→[(a,2)]

Output: "aa" ✓
```

---

### Problem 16 — Backspace String Compare
**LeetCode #844 | Difficulty: Easy | Company: Amazon, Facebook | Category: Stack Simulation**

> Compare two strings where `#` means backspace. Return if they are equal.

#### Java code

```java
public boolean backspaceCompare(String s, String t) {
    return process(s).equals(process(t));
}

private String process(String s) {
    Deque<Character> st = new ArrayDeque<>();
    for (char ch : s.toCharArray()) {
        if (ch == '#') { if (!st.isEmpty()) st.pop(); }
        else             st.push(ch);
    }
    StringBuilder sb = new StringBuilder();
    while (!st.isEmpty()) sb.append(st.pop());
    return sb.reverse().toString();
}
```

#### Example

```
s = "ab#c" → process: a→[a] b→[a,b] #→[a] c→[a,c] → "ac"
t = "ad#c" → process: a→[a] d→[a,d] #→[a] c→[a,c] → "ac"

Output: true ✓
```

---

### Problem 17 — Removing Stars From a String
**LeetCode #2390 | Difficulty: Medium | Company: Amazon | Category: Stack Simulation**

> `*` removes the closest non-star character to its left.

#### Java code

```java
public String removeStars(String s) {
    Deque<Character> st = new ArrayDeque<>();
    for (char ch : s.toCharArray()) {
        if (ch == '*') st.pop();
        else           st.push(ch);
    }
    StringBuilder sb = new StringBuilder();
    while (!st.isEmpty()) sb.append(st.pop());
    return sb.reverse().toString();
}
```

#### Example

```
s = "leet**cod*e"
l→[l] e→[l,e] e→[l,e,e] t→[l,e,e,t] *→[l,e,e] *→[l,e] c→[l,e,c] o→[l,e,c,o] d→[l,e,c,o,d] *→[l,e,c,o] e→[l,e,c,o,e]
Output: "lecoe" ✓
```

---

### Problem 18 — Remove Duplicate Letters
**LeetCode #316 | Difficulty: Hard | Company: Google, Amazon | Category: Monotonic Stack + Greedy**

> Remove duplicate letters so each letter appears once and the result is the lexicographically smallest.

#### Core insight

Greedy: maintain a monotonic increasing stack of characters. Pop a larger character only if it appears again later. Use `visited[]` to skip already-in-stack chars.

#### Java code

```java
public String removeDuplicateLetters(String s) {
    int[] lastIdx = new int[26];
    boolean[] visited = new boolean[26];
    for (int i = 0; i < s.length(); i++)
        lastIdx[s.charAt(i) - 'a'] = i;

    Deque<Character> st = new ArrayDeque<>();
    for (int i = 0; i < s.length(); i++) {
        char ch = s.charAt(i);
        if (visited[ch - 'a']) continue;              // already in result
        while (!st.isEmpty()
               && st.peek() > ch
               && lastIdx[st.peek() - 'a'] > i) {    // can remove (appears later)
            visited[st.pop() - 'a'] = false;
        }
        st.push(ch);
        visited[ch - 'a'] = true;
    }
    StringBuilder sb = new StringBuilder();
    while (!st.isEmpty()) sb.append(st.pop());
    return sb.reverse().toString();
}
```

#### Example

```
s = "bcabc"
lastIdx: b=3, c=4, a=2

i=0(b): push b. st=[b], visited={b}
i=1(c): push c. st=[b,c], visited={b,c}
i=2(a): c>a and lastIdx[c]=4>2 → pop c, unvisit c
        b>a and lastIdx[b]=3>2 → pop b, unvisit b
        push a. st=[a], visited={a}
i=3(b): push b. st=[a,b]
i=4(c): push c. st=[a,b,c]

Output: "abc" ✓
```

---

### Problem 19 — Remove K Digits
**LeetCode #402 | Difficulty: Medium | Company: Google, Amazon | Category: Monotonic Stack + Greedy**

> Remove k digits from a number to form the smallest possible number.

#### Core insight

Maintain a monotonic increasing stack. Pop whenever top > current AND k > 0. If k still remains after the loop, remove from the back (largest digits). Handle leading zeros.

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Each digit | `k>0 && top > curr` | pop + `k--` |
| Push | always | push char |
| After loop | `k > 0` | `pollLast()` k times |
| Rebuild | skip leading zeros | start appending after first non-zero |

#### Java code

```java
public String removeKdigits(String num, int k) {
    Deque<Character> st = new ArrayDeque<>();

    for (char ch : num.toCharArray()) {
        while (k > 0 && !st.isEmpty() && st.peek() > ch) {
            st.pollLast();   // pop from back (top of stack)
            k--;
        }
        st.addLast(ch);      // push to back
    }
    while (k-- > 0) st.pollLast();   // remove largest remaining digits

    StringBuilder sb = new StringBuilder();
    boolean leadingZero = true;
    for (char c : st) {
        if (leadingZero && c == '0') continue;
        leadingZero = false;
        sb.append(c);
    }
    return sb.length() == 0 ? "0" : sb.toString();
}
```

#### Example

```
num = "1432219", k = 3

1→[1]  4→[1,4]  3: 4>3,k=2 → pop 4 → [1,3]  2: 3>2,k=1→pop 3→[1,2]  2: push→[1,2,2]
2: push→[1,2,2,2]  1: 2>1,k=0→pop 2,k=0→stop → [1,2,2,1]? wait k=0 after 1 pop...

Correct trace: k=3
1→[1] 4→[1,4] 3: pop 4(k=2)→[1,3] 2: pop 3(k=1)→[1,2] 2: push→[1,2,2]
2: push→[1,2,2,2] 1: pop 2(k=0)→[1,2,2,1]? k=0 so stop, push 1→[1,2,2,1]? 
wait: 2>1 and k=1→pop, k=0. push 1. → [1,2,2] then k=0 so push 1,9.

Output: "1219" ✓
```

---

## Category 4 — Expression Evaluation

---

### Problem 20 — Evaluate Reverse Polish Notation
**LeetCode #150 | Difficulty: Medium | Company: Amazon, LinkedIn | Category: Expression Stack**

> Evaluate an expression in Reverse Polish Notation (postfix). Operands pushed; operators pop 2, compute, push result.

#### Approach table

| Token | Action |
|-------|--------|
| Number | `st.push(Integer.parseInt(token))` |
| Operator | `b = pop`, `a = pop`, `push(a op b)` |

#### Java code

```java
public int evalRPN(String[] tokens) {
    Deque<Integer> st = new ArrayDeque<>();

    for (String token : tokens) {
        if ("+-*/".contains(token)) {
            int b = st.pop();   // right operand (more recent)
            int a = st.pop();   // left operand
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
}
```

#### Example

```
tokens = ["2","1","+","3","*"]

push 2 → [2]
push 1 → [2,1]
"+": b=1, a=2, push 3 → [3]
push 3 → [3,3]
"*": b=3, a=3, push 9 → [9]

Output: 9  (= (2+1)*3) ✓
```

---

### Problem 21 — Basic Calculator II
**LeetCode #227 | Difficulty: Medium | Company: Facebook, Amazon | Category: Expression Stack**

> Evaluate a string expression with `+`, `-`, `*`, `/` (no parentheses).

#### Core insight

Track the last operator (sign). For `+`/`-`: push `sign * num`. For `*`/`/`: pop top, compute with num, push result. Sum the stack at end.

#### Java code

```java
public int calculate(String s) {
    Deque<Integer> st = new ArrayDeque<>();
    int num = 0;
    char sign = '+';   // last seen operator

    for (int i = 0; i < s.length(); i++) {
        char ch = s.charAt(i);
        if (Character.isDigit(ch)) num = num * 10 + (ch - '0');

        if ((!Character.isDigit(ch) && ch != ' ') || i == s.length() - 1) {
            switch (sign) {
                case '+' -> st.push(num);
                case '-' -> st.push(-num);
                case '*' -> st.push(st.pop() * num);
                case '/' -> st.push(st.pop() / num);
            }
            sign = ch;
            num = 0;
        }
    }
    int result = 0;
    while (!st.isEmpty()) result += st.pop();
    return result;
}
```

#### Example

```
s = "3+2*2"

ch='3': num=3
ch='+': sign was '+' → push 3. sign='+', num=0
ch='2': num=2
ch='*': sign was '+' → push 2. sign='*', num=0
ch='2': num=2, last char
  sign='*' → pop 2, push 2*2=4. stack=[3,4]

sum = 3 + 4 = 7 ✓
```

---

### Problem 22 — Basic Calculator
**LeetCode #224 | Difficulty: Hard | Company: Amazon, Google | Category: Expression Stack**

> Evaluate a string with `+`, `-`, and parentheses. Handles nested parentheses.

#### Core insight

Push current result and sign onto stack when `(` is encountered. Restore when `)` is found.

#### Java code

```java
public int calculate(String s) {
    Deque<Integer> st = new ArrayDeque<>();
    int result = 0, num = 0, sign = 1;

    for (char ch : s.toCharArray()) {
        if (Character.isDigit(ch)) {
            num = num * 10 + (ch - '0');
        } else if (ch == '+') {
            result += sign * num; num = 0; sign = 1;
        } else if (ch == '-') {
            result += sign * num; num = 0; sign = -1;
        } else if (ch == '(') {
            st.push(result);   // save current result
            st.push(sign);     // save sign before '('
            result = 0; sign = 1;
        } else if (ch == ')') {
            result += sign * num; num = 0;
            result *= st.pop();   // multiply by sign before '('
            result += st.pop();   // add saved result
        }
    }
    return result + sign * num;
}
```

#### Example

```
s = "1 + (2 - (3 + 1))"

result=0, sign=1
'1': num=1
'+': result=1, num=0, sign=1
'(': push 1, push 1. result=0, sign=1
'2': num=2
'-': result=2, num=0, sign=-1
'(': push 2, push -1. result=0, sign=1
'3': num=3
'+': result=3, sign=1
'1': num=1
')': result=3+1=4, result*=pop(-1)=-4, result+=pop(2)=-2
')': result=-2+0=result*=pop(1)=-2, result+=pop(1)=-1

Output: -1 ✓  (1 + (2 - 4) = 1 + (-2) = -1)
```

---

### Problem 23 — Decode String
**LeetCode #394 | Difficulty: Medium | Company: Google, Amazon | Category: Save/Restore State**

> `3[abc]` → `abcabcabc`. Supports nesting: `2[3[a]]` → `aaaaaa`.

#### Approach table

| Token | Action |
|-------|--------|
| Digit | `k = k*10 + digit` (handle multi-digit) |
| `[` | push `(k, curr)` onto stacks; reset k=0, curr="" |
| `]` | `prev = pop`; `curr = prev + curr × times` |
| Letter | append to `curr` |

#### Java code

```java
public String decodeString(String s) {
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
}
```

#### Example

```
s = "3[a2[c]]"

'3': k=3
'[': push (3, ""), curr="", k=0
'a': curr="a"
'2': k=2
'[': push (2, "a"), curr="", k=0
'c': curr="c"
']': times=2, prev="a" → prev="a"+"c"+"c"="acc". curr="acc"
']': times=3, prev="" → prev=""+"acc"+"acc"+"acc"="accaccacc". curr="accaccacc"

Output: "accaccacc" ✓
```

---

## Category 5 — Stack Simulation

---

### Problem 24 — Simplify Path
**LeetCode #71 | Difficulty: Medium | Company: Facebook, Amazon | Category: Stack Simulation**

> Convert a Unix file path to its canonical (simplified) form.

#### Approach table

| Token | Action |
|-------|--------|
| `""` or `"."` | skip |
| `".."` | pop if stack not empty |
| anything else | push directory name |

#### Java code

```java
public String simplifyPath(String path) {
    Deque<String> st = new ArrayDeque<>();

    for (String dir : path.split("/")) {
        if (dir.equals("..")) {
            if (!st.isEmpty()) st.pop();
        } else if (!dir.isEmpty() && !dir.equals(".")) {
            st.push(dir);
        }
    }

    List<String> list = new ArrayList<>(st);
    Collections.reverse(list);
    StringBuilder sb = new StringBuilder();
    for (String d : list) sb.append("/").append(d);
    return sb.length() == 0 ? "/" : sb.toString();
}
```

#### Example

```
path = "/home/../usr/./bin"
Split: ["", "home", "..", "usr", ".", "bin"]

"": skip
"home": push → [home]
"..": pop → []
"usr": push → [usr]
".": skip
"bin": push → [usr, bin]

Output: "/usr/bin" ✓
```

---

### Problem 25 — Asteroid Collision
**LeetCode #735 | Difficulty: Medium | Company: Amazon, Apple | Category: Conditional Stack**

> Positive asteroids move right, negative move left. When they collide, smaller explodes. Equal-size both explode.

#### Approach table

| Condition | Action |
|-----------|--------|
| Same direction (top>0,curr>0) or (top<0,curr<0) | no collision, push |
| curr > 0 | always push (moving right, no left asteroid coming) |
| curr < 0, top > 0 | collision! larger survives |

#### Java code

```java
public int[] asteroidCollision(int[] asteroids) {
    Deque<Integer> st = new ArrayDeque<>();

    for (int a : asteroids) {
        boolean alive = true;
        while (alive && a < 0 && !st.isEmpty() && st.peek() > 0) {
            if      (st.peek() < -a)  st.pop();           // stack asteroid explodes
            else if (st.peek() == -a) { st.pop(); alive = false; }  // both explode
            else                       alive = false;     // incoming explodes
        }
        if (alive) st.push(a);
    }

    int[] res = new int[st.size()];
    for (int i = res.length - 1; i >= 0; i--) res[i] = st.pop();
    return res;
}
```

#### Example

```
asteroids = [5, 10, -5]

push 5 → [5]
push 10 → [5,10]
-5: 10 > 5 → alive=false (incoming -5 explodes)
push nothing.

Output: [5,10] ✓

asteroids = [8,-8]
push 8 → [8]
-8: 8 == 8 → both explode. st=[]
Output: [] ✓
```

---

### Problem 26 — Baseball Game
**LeetCode #682 | Difficulty: Easy | Company: Amazon | Category: Stack Simulation**

> Simulate a baseball scoring game. `"+"` = sum of last 2, `"D"` = double last, `"C"` = cancel last.

#### Java code

```java
public int calPoints(String[] operations) {
    Deque<Integer> st = new ArrayDeque<>();

    for (String op : operations) {
        switch (op) {
            case "+" -> st.push(st.peek() + ((int[]) st.toArray())[1]); // top + second
            case "D" -> st.push(st.peek() * 2);
            case "C" -> st.pop();
            default  -> st.push(Integer.parseInt(op));
        }
    }
    // simpler "+" implementation:
    int sum = 0;
    while (!st.isEmpty()) sum += st.pop();
    return sum;
}
```

#### Cleaner implementation

```java
public int calPoints(String[] ops) {
    Deque<Integer> st = new ArrayDeque<>();
    for (String op : ops) {
        if (op.equals("C")) {
            st.pop();
        } else if (op.equals("D")) {
            st.push(st.peek() * 2);
        } else if (op.equals("+")) {
            int top = st.pop();
            int newTop = top + st.peek();
            st.push(top);
            st.push(newTop);
        } else {
            st.push(Integer.parseInt(op));
        }
    }
    int sum = 0;
    while (!st.isEmpty()) sum += st.pop();
    return sum;
}
```

#### Example

```
ops = ["5","2","C","D","+"]

push 5 → [5]
push 2 → [5,2]
C → pop → [5]
D → push 10 → [5,10]
+ → top=10, peek=5, newTop=15 → [5,10,15]

sum = 5+10+15 = 30 ✓
```

---

### Problem 27 — Reverse a String Using Stack
**Difficulty: Easy | Category: Basic Stack**

> Reverse a string using a stack.

#### Java code

```java
public String reverseString(String s) {
    Deque<Character> st = new ArrayDeque<>();
    for (char ch : s.toCharArray()) st.push(ch);

    StringBuilder sb = new StringBuilder();
    while (!st.isEmpty()) sb.append(st.pop());
    return sb.toString();
}
```

#### Example

```
s = "hello"
Push: h,e,l,l,o → stack top = 'o'
Pop order: o,l,l,e,h

Output: "olleh" ✓
```

---

## Category 6 — Design Problems

---

### Problem 28 — Min Stack
**LeetCode #155 | Difficulty: Medium | Company: Amazon, Google, Facebook | Category: Augmented Stack**

> Design a stack that supports `push`, `pop`, `top`, and `getMin` — all in O(1) time.

#### Core insight

Store `[value, minSoFar]` pairs. `getMin()` = peek at the second element of the top pair. No extra stack needed.

#### Java code

```java
class MinStack {
    Deque<int[]> st = new ArrayDeque<>();   // [value, minSoFar]

    public void push(int val) {
        int min = st.isEmpty() ? val : Math.min(val, st.peek()[1]);
        st.push(new int[]{val, min});
    }

    public void pop()   { st.pop(); }
    public int top()    { return st.peek()[0]; }
    public int getMin() { return st.peek()[1]; }   // O(1) always
}
```

#### Example

```
push(-2) → st=[(-2,-2)]
push(0)  → min=min(0,-2)=-2 → st=[(-2,-2),(0,-2)]
push(-3) → min=min(-3,-2)=-3 → st=[...,(0,-2),(-3,-3)]
getMin() → peek()[1] = -3 ✓
pop()    → st=[(-2,-2),(0,-2)]
top()    → peek()[0] = 0 ✓
getMin() → peek()[1] = -2 ✓
```

---

### Problem 29 — Implement Queue Using Stacks
**LeetCode #232 | Difficulty: Easy | Company: Amazon, Microsoft | Category: Two Stacks**

> Implement a FIFO queue using only two stacks.

#### Core insight

`inbox` for push. `outbox` for pop/peek. Transfer from inbox to outbox only when outbox is empty. Each element transferred at most once → amortized O(1) per operation.

#### Java code

```java
class MyQueue {
    Deque<Integer> inbox  = new ArrayDeque<>();
    Deque<Integer> outbox = new ArrayDeque<>();

    public void push(int x) { inbox.push(x); }

    public int pop()  { transfer(); return outbox.pop(); }
    public int peek() { transfer(); return outbox.peek(); }
    public boolean empty() { return inbox.isEmpty() && outbox.isEmpty(); }

    private void transfer() {
        if (outbox.isEmpty())
            while (!inbox.isEmpty()) outbox.push(inbox.pop());
    }
}
```

#### Example

```
push(1): inbox=[1]
push(2): inbox=[2,1]
peek():  outbox empty → transfer → outbox=[1,2]. peek=1 ✓
pop():   outbox=[1,2], pop=1. outbox=[2]
push(3): inbox=[3]
pop():   outbox=[2], pop=2. outbox=[]
pop():   outbox empty → transfer → outbox=[3]. pop=3 ✓
```

---

### Problem 30 — Implement Stack Using Queues
**LeetCode #225 | Difficulty: Easy | Company: Amazon | Category: Two Queues / One Queue**

> Implement a LIFO stack using only queue operations.

#### Core insight (one queue approach)

After each push, rotate the queue so the newly pushed element comes to the front. Then `pop` = `poll()` directly.

#### Java code

```java
class MyStack {
    Queue<Integer> q = new LinkedList<>();

    public void push(int x) {
        q.offer(x);
        for (int i = 0; i < q.size() - 1; i++)
            q.offer(q.poll());   // rotate: bring x to front
    }

    public int pop()     { return q.poll(); }
    public int top()     { return q.peek(); }
    public boolean empty() { return q.isEmpty(); }
}
```

#### Example

```
push(1): q=[1]
push(2): q=[2,1] after rotate (2 at front)
push(3): q=[3,2,1] after rotate (3 at front)
top():   peek = 3 ✓
pop():   poll = 3. q=[2,1]
top():   peek = 2 ✓
```

---

### Problem 31 — Design Browser History
**LeetCode #1472 | Difficulty: Medium | Company: Amazon, Google | Category: Two Stacks**

> Design a browser with `visit`, `back(steps)`, and `forward(steps)` operations.

#### Core insight

Two stacks: `back` for visited pages, `forward` for pages after current. On `visit`, clear `forward`. On `back`/`forward`, move between stacks step by step.

#### Java code

```java
class BrowserHistory {
    Deque<String> back    = new ArrayDeque<>();
    Deque<String> forward = new ArrayDeque<>();
    String curr;

    public BrowserHistory(String homepage) { curr = homepage; }

    public void visit(String url) {
        back.push(curr);
        curr = url;
        forward.clear();   // clear forward history on new visit
    }

    public String back(int steps) {
        while (steps-- > 0 && !back.isEmpty()) {
            forward.push(curr);
            curr = back.pop();
        }
        return curr;
    }

    public String forward(int steps) {
        while (steps-- > 0 && !forward.isEmpty()) {
            back.push(curr);
            curr = forward.pop();
        }
        return curr;
    }
}
```

#### Example

```
BrowserHistory("leetcode.com")
visit("google.com"):  back=[leetcode], curr=google, forward=[]
visit("facebook.com"): back=[google,leetcode], curr=facebook, forward=[]
visit("youtube.com"):  back=[facebook,google,leetcode], curr=youtube, forward=[]
back(1): forward=[youtube], curr=facebook ✓
back(1): forward=[youtube,facebook], curr=google ✓
forward(1): back=[...,google], curr=facebook ✓
visit("linkedin.com"): forward=[] cleared! curr=linkedin ✓
forward(2): forward empty → curr=linkedin ✓
back(2): curr=facebook → curr=google ✓
back(7): go as far as possible → curr=leetcode ✓
```

---

### Problem 32 — Maximum Frequency Stack
**LeetCode #895 | Difficulty: Hard | Company: Google, Amazon | Category: Design Stack**

> Design a stack-like data structure. `push(x)` adds x. `pop()` removes the most frequent element (ties broken by most recently pushed).

#### Core insight

Track `freq[x]` = frequency of x. Track `maxFreq` = current max frequency. Track `group[f]` = list of elements pushed when they first reached frequency `f`. On `pop`, remove from `group[maxFreq]`, decrement freq, decrement maxFreq if group becomes empty.

#### Java code

```java
class FreqStack {
    Map<Integer, Integer> freq  = new HashMap<>();
    Map<Integer, Deque<Integer>> group = new HashMap<>();
    int maxFreq = 0;

    public void push(int val) {
        int f = freq.merge(val, 1, Integer::sum);
        maxFreq = Math.max(maxFreq, f);
        group.computeIfAbsent(f, k -> new ArrayDeque<>()).push(val);
    }

    public int pop() {
        Deque<Integer> top = group.get(maxFreq);
        int val = top.pop();
        freq.merge(val, -1, Integer::sum);
        if (top.isEmpty()) { group.remove(maxFreq); maxFreq--; }
        return val;
    }
}
```

#### Example

```
push(5): freq={5:1}, group={1:[5]}, maxFreq=1
push(7): freq={5:1,7:1}, group={1:[7,5]}, maxFreq=1
push(5): freq={5:2,7:1}, group={1:[7,5],2:[5]}, maxFreq=2
push(7): freq={5:2,7:2}, group={1:[7,5],2:[7,5]}, maxFreq=2
push(4): freq={5:2,7:2,4:1}, group={1:[4,7,5],2:[7,5]}, maxFreq=2
push(5): freq={5:3,...}, group={...3:[5]}, maxFreq=3

pop(): maxFreq=3 → pop 5 from group[3]. freq[5]=2. group[3] empty → maxFreq=2. return 5 ✓
pop(): maxFreq=2 → pop 7 from group[2]. freq[7]=1. return 7 ✓
pop(): maxFreq=2 → pop 5 from group[2]. freq[5]=1. return 5 ✓
pop(): maxFreq=1 → pop 4 from group[1]. return 4 ✓
```

---

## Quick Pattern Reference

| Problem | Category | Key technique |
|---------|----------|---------------|
| Next Greater Element I | Monotonic ↓ | pop when top < curr; HashMap for lookup |
| Daily Temperatures | Monotonic ↓ | pop when top < curr; record distance |
| NGE II Circular | Monotonic ↓ 2n | `i % n`; push only first n |
| Stock Span | Monotonic ↓ | `i - top` before push |
| Online Stock Span | Monotonic design | push `[price, span]`; accumulate on pop |
| Largest Rectangle | Monotonic ↑ + sentinel | area = `h × (i - newTop - 1)` |
| Trapping Rain Water | Monotonic valley | water = `(min(L,R) - bottom) × width` |
| Sum Subarray Mins | Monotonic contribution | `val × left × right` per element |
| Remove Nodes LL | Monotonic ↓ | keep only nodes with no greater to right |
| Valid Parentheses | Bracket match | push open; match on close |
| Min Remove Valid | Bracket index | store indices; remove unmatched set |
| Longest Valid Parens | Bracket + sentinel | `-1` base; `i - peek` on match |
| Score of Parentheses | Bracket depth | push 0 on `(`; compute on `)` |
| Remove Adjacent I | Stack removal | pop on same char |
| Remove Adjacent II | Stack + count | `[char,count]`; pop when count==k |
| Backspace Compare | Stack simulation | pop on `#` |
| Remove Stars | Stack simulation | pop on `*` |
| Remove Duplicate Letters | Monotonic + greedy | pop if top > curr AND appears later |
| Remove K Digits | Monotonic + greedy | pop if top > curr AND k > 0 |
| Evaluate RPN | Expression stack | b=pop, a=pop; push(a op b) |
| Basic Calculator II | Expression + sign | push with sign; `*/` inline |
| Basic Calculator | Expression + parens | push (result, sign) on `(`; restore on `)` |
| Decode String | Save/restore state | push (k, sb) on `[`; repeat on `]` |
| Simplify Path | Stack simulation | split `/`; push dirs; pop on `..` |
| Asteroid Collision | Conditional stack | pop while right>0 and left<0 |
| Baseball Game | Stack simulation | C=pop, D=×2, +=sum of top 2 |
| Reverse String | Basic stack | push all, pop all |
| Min Stack | Augmented stack | push (val, min); getMin = peek()[1] |
| Queue via Stacks | Two stacks | inbox + outbox; transfer on empty |
| Stack via Queues | One queue rotate | rotate after each push |
| Browser History | Two stacks | back + forward; clear forward on visit |
| Max Frequency Stack | Freq + group map | group[freq] = deque; pop from maxFreq |
