# Slow & Fast Pointers — Solved Problems (22 Problems)

> **Pattern family:** LinkedList / Cycle Detection / Sequence Traversal
> **Notes & Templates:** [01_slow_fast_pointers_notes.md](./01_slow_fast_pointers_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Classic Floyd's (Cycle Detection)
- [P1 — LinkedList Cycle](#problem-1--linkedlist-cycle)
- [P2 — Start of LinkedList Cycle](#problem-2--start-of-linkedlist-cycle)
- [P3 — Circular Array Loop](#problem-3--circular-array-loop)

### Category 2 — Find Middle + Process
- [P4 — Middle of LinkedList](#problem-4--middle-of-linkedlist)
- [P5 — Palindrome LinkedList](#problem-5--palindrome-linkedlist)
- [P6 — Reorder List](#problem-6--reorder-list)

### Category 3 — Gap Technique
- [P7 — Remove Nth Node From End](#problem-7--remove-nth-node-from-end)
- [P7b — Odd Even Linked List](#problem-7b--odd-even-linked-list)

### Category 4 — Implicit Cycle
- [P8 — Happy Number](#problem-8--happy-number)
- [P9 — Find the Duplicate Number](#problem-9--find-the-duplicate-number)

### Category 5 — Slow Write / Fast Read
- [P10 — String Compression](#problem-10--string-compression)
- [P11 — Remove Duplicates from Sorted Array](#problem-11--remove-duplicates-from-sorted-array)
- [P12 — Remove Duplicates from Sorted Array II](#problem-12--remove-duplicates-from-sorted-array-ii)
- [P13 — Duplicate Zeros](#problem-13--duplicate-zeros)

### Category 6 — Rotate / Split + Reconnect
- [P14 — Rotate List](#problem-14--rotate-list)
- [P15 — Rotate Array](#problem-15--rotate-array)

### Category 7 — Two-pointer String / Array
- [P16 — Partition Labels](#problem-16--partition-labels)
- [P17 — Counting Binary Substrings](#problem-17--counting-binary-substrings)
- [P18 — Last Substring in Lexicographical Order](#problem-18--last-substring-in-lexicographical-order)

### Bonus / FAANG
- [P19 — Intersection of Two Linked Lists](#problem-19--intersection-of-two-linked-lists)
- [P20 — Sort List](#problem-20--sort-list)
- [P21 — Number of Subarrays with Bounded Maximum](#problem-21--number-of-subarrays-with-bounded-maximum)
- [P22 — K-diff Pairs in an Array](#problem-22--k-diff-pairs-in-an-array)

---

## Category 1 — Classic Floyd's (Cycle Detection)

---

### Problem 1 — LinkedList Cycle
**LeetCode #141 | Difficulty: Easy | Company: Amazon, Microsoft | Category: Classic Floyd's**

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Loop | `fast != null && fast.next != null` | move slow 1 step, fast 2 steps |
| Inside loop | `slow == fast` | cycle exists → `return true` |
| Loop exits | `fast == null` | no cycle → `return false` |

#### Java code

```java
public boolean hasCycle(ListNode head) {
    ListNode slow = head, fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow == fast) {
            return true;
        }
    }
    return false;
}
```

#### Example

```
Input: 1 → 2 → 3 → 4 → 2 (cycle back to node 2)

iter1: slow=2, fast=3
iter2: slow=3, fast=2  (fast jumped 3→4→2)
iter3: slow=4, fast=4  → slow==fast → return true ✓

Input: 1 → 2 → 3 → null
iter2: slow=3, fast=null → loop exits → return false ✓
```

---

### Problem 2 — Start of LinkedList Cycle
**LeetCode #142 | Difficulty: Medium | Company: Amazon, Google | Category: Floyd Phase 2**

#### Approach table

| Phase | Step | Action |
|-------|------|--------|
| Phase 1 | detect meeting point | slow 1 step, fast 2 steps until `slow==fast` |
| Phase 2 | find cycle start | reset `slow=head`, move both 1 step until `slow==fast` |

#### My Solution

```java
public ListNode detectCycle(ListNode head) {
    ListNode slow = head, fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow == fast) {
            slow = head;                 // Phase 2: reset slow to head

            while (slow != fast) {
                slow = slow.next;
                fast = fast.next;        // both move 1 step
            }
            return fast;                 // cycle start
        }
    }
    return null;   // no cycle
}
```

#### Reference Solution

```java
public ListNode detectCycle(ListNode head) {
    ListNode slow = head, fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next; fast = fast.next.next;
        if (slow == fast) {
            slow = head;                    // Phase 2: reset slow to head
            while (slow != fast) {
                slow = slow.next;
                fast = fast.next;           // both move 1 step
            }
            return slow;                    // cycle start
        }
    }
    return null;   // no cycle
}
```

#### Example

```
Input: 3 → 1 → 2 → 4 → 2 (cycle at index 1)

Phase 1: slow=1,fast=2 → slow=2,fast=2 → meet at node(2)
Phase 2: slow=head=3, fast=node(2)
  step: slow=1, fast=4
  step: slow=2, fast=2 → return node(2) ✓
```

---

### Problem 3 — Circular Array Loop
**LeetCode #457 | Difficulty: Hard | Company: Google | Category: Implicit Cycle**

> Array contains positive and negative integers. `nums[i]` means jump `nums[i]` steps forward or backward. Find if there's a cycle of length > 1 where all elements have the same direction.

#### Java code

```java
public boolean circularArrayLoop(int[] nums) {
    int n = nums.length;

    for (int i = 0; i < n; i++) {
        if (nums[i] == 0) continue;

        int slow = i, fast = i;
        // All elements in cycle must have same direction as nums[i]
        while (true) {
            slow = getNext(nums, slow);
            fast = getNext(nums, getNext(nums, fast));

            if (slow == fast) break;
            // Direction changed — no valid cycle starting from i
            if (nums[slow] * nums[i] < 0) break;
            if (nums[fast] * nums[i] < 0) break;
        }

        if (slow == fast) {
            // Verify cycle length > 1
            if (getNext(nums, slow) == slow) continue;   // self-loop — invalid
            return true;
        }
    }
    return false;
}

private int getNext(int[] nums, int i) {
    int n = nums.length;
    return ((i + nums[i]) % n + n) % n;   // always positive index
}
```

#### Example

```
Input: nums = [2,-1,1,2,2]
Start i=0: slow=2, fast=4 → slow=0, fast=0 → meet!
getNext(0)=2 ≠ 0 → cycle length > 1 → return true ✓
```

---

## Category 2 — Find Middle + Process

---

### Problem 4 — Middle of LinkedList
**LeetCode #876 | Difficulty: Easy | Company: Amazon | Category: Find Middle**

#### Java code

```java
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode slow = head, fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;
    }
}
```

#### Example

```
Odd:  1→2→3→4→5  → slow=3 (exact middle) ✓
Even: 1→2→3→4    → slow=3 (right-middle) ✓
```

---

### Problem 5 — Palindrome LinkedList
**LeetCode #234 | Difficulty: Easy | Company: Amazon, Facebook | Category: Middle + Reverse**

#### Approach table

| Step | Action |
|------|--------|
| 1 | Find middle with slow/fast |
| 2 | Reverse second half from `slow` |
| 3 | Compare `p1` from head, `p2` from reversed head |

#### My Solution

```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) {
            return true;
        }
        ListNode fast = head;
        ListNode slow = head;

        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }

        ListNode secondGroupHead = reverse(slow);
        ListNode p1 = head;
        ListNode p2 = secondGroupHead;

        while (p2 != null) {
            if (p1.val != p2.val) {
                return false;
            }
            p1 = p1.next;
            p2 = p2.next;
        }
        return true;
    }

    private ListNode reverse(ListNode head) {
        ListNode curr = head;
        ListNode prev = null;

        while (curr != null) {
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
}
```

#### Reference Solution

```java
public boolean isPalindrome(ListNode head) {
    ListNode slow = head, fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next; fast = fast.next.next;
    }

    ListNode second = reverse(slow);   // includes middle in second half — OK for compare only
    ListNode p1 = head, p2 = second;

    while (p2 != null) {
        if (p1.val != p2.val) return false;
        p1 = p1.next; p2 = p2.next;
    }
    return true;
}

private ListNode reverse(ListNode head) {
    ListNode prev = null, curr = head;
    while (curr != null) {
        ListNode next = curr.next; curr.next = prev; prev = curr; curr = next;
    }
    return prev;
}
```

#### Example

```
Input: 1 → 2 → 2 → 1
slow=node(2nd 2), reverse from here: 1→2
p1=1,p2=1 ✓  p1=2,p2=2 ✓  p2=null → true ✓
```

---

### Problem 6 — Reorder List
**LeetCode #143 | Difficulty: Medium | Company: Amazon | Category: Middle + Reverse + Merge**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Find middle | slow/fast |
| 2 | `second = reverse(slow.next)` | reverse second half |
| 3 | `slow.next = null` | cut at middle |
| 4 | Merge alternately | `first` and `second` |

#### My Solution

```java
class Solution {
    public void reorderList(ListNode head) {
        if (head == null || head.next == null) {
            return;
        }
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }

        ListNode second = reverse(slow.next);   // reverse AFTER middle
        slow.next = null;                        // cut first half cleanly
        ListNode first = head;

        while (second != null) {
            ListNode temp1 = first.next;
            ListNode temp2 = second.next;

            first.next  = second;
            second.next = temp1;

            first  = temp1;
            second = temp2;
        }
    }

    private ListNode reverse(ListNode head) {
        ListNode curr = head;
        ListNode prev = null;

        while (curr != null) {
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
}
```

#### Reference Solution

```java
public void reorderList(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next; fast = fast.next.next;
    }

    ListNode second = reverse(slow.next);
    slow.next = null;                       // cut first half cleanly
    ListNode first = head;

    while (second != null) {
        ListNode t1 = first.next, t2 = second.next;
        first.next = second; second.next = t1;
        first = t1; second = t2;
    }
}
```

#### Example

```
Input: 1→2→3→4→5
Middle: slow=3, second=reverse(4→5)=5→4
Cut: first=1→2→3
Merge: 1→5→2→4→3 ✓
```

---

## Category 3 — Gap Technique

---

### Problem 7 — Remove Nth Node From End
**LeetCode #19 | Difficulty: Medium | Company: Amazon, Microsoft | Category: Gap Technique**

#### Core insight

Use a dummy node so we can handle removing the head. Advance `fast` by `n+1` steps (not n) so `slow` lands **one before** the node to delete.

#### Java code

```java
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(0); dummy.next = head;
    ListNode slow = dummy, fast = dummy;

    for (int i = 0; i <= n; i++) fast = fast.next;   // advance n+1 steps

    while (fast != null) { slow = slow.next; fast = fast.next; }

    slow.next = slow.next.next;   // skip the nth-from-end node
    return dummy.next;
}
```

#### Example

```
Input: 1→2→3→4→5, n=2
dummy→1→2→3→4→5

fast advances n+1=3 steps: fast=node(3)
Both move until fast=null:
  slow=1,fast=4 → slow=2,fast=5 → slow=3,fast=null
slow.next = slow.next.next → remove node(4)
Output: 1→2→3→5 ✓
```

---

### Problem 7b — Odd Even Linked List
**LeetCode #328 | Difficulty: Medium | Company: Amazon, Microsoft | Category: Pointer Rearrangement**

> Group all nodes at odd indices together followed by nodes at even indices. In-place, O(1) space.

#### Approach table

| Pointer | Starts at | Moves to |
|---------|-----------|----------|
| `odd` | head (index 1) | `even.next` |
| `even` | head.next (index 2) | `odd.next` |
| `evenHead` | head.next | fixed — join point at end |

#### Java code

```java
public ListNode oddEvenList(ListNode head) {
    if (head == null) return null;

    ListNode odd = head;
    ListNode even = head.next;
    ListNode evenHead = even;          // save even list's start

    while (even != null && even.next != null) {
        odd.next = even.next;          // odd skips over even
        odd = odd.next;
        even.next = odd.next;          // even skips over (new) odd
        even = even.next;
    }

    odd.next = evenHead;               // attach even list at end of odd list
    return head;
}
```

#### Example

```
Input: 1 → 2 → 3 → 4 → 5

odd=1, even=2, evenHead=2

iter1: odd.next=3, odd=3 | even.next=4, even=4
iter2: odd.next=5, odd=5 | even.next=null → loop exits

odd.next = evenHead(2)
Output: 1 → 3 → 5 → 2 → 4 ✓

Time: O(n), Space: O(1)
```

---

## Category 4 — Implicit Cycle

---

### Problem 8 — Happy Number
**LeetCode #202 | Difficulty: Medium | Company: Amazon, Google | Category: Implicit Cycle**

#### Core insight

Numbers eventually form a cycle. If the cycle reaches 1 → happy. If not → unhappy. Detect cycle with Floyd's: `getNext = sum of digit squares`.

#### My Solution

```java
class Solution {
    public boolean isHappy(int n) {
        int slow = n, fast = n;

        while (fast != 1) {
            slow = funSum(slow);           // 1 step
            fast = funSum(fast);
            fast = funSum(fast);           // 2 steps

            if (slow == fast && fast != 1) {
                return false;              // met in non-1 cycle → not happy
            }
        }
        return true;   // fast reached 1
    }

    private int funSum(int n) {
        int sum = 0;
        while (n != 0) {
            int d = n % 10;
            n /= 10;
            sum = sum + d * d;
        }
        return sum;
    }
}
```

> **Note:** `while(fast != 1)` approach short-circuits as soon as fast hits 1. The `fast != 1` guard inside correctly prevents false negatives when slow and fast both land on 1 simultaneously.

#### Reference Solution

```java
public boolean isHappy(int n) {
    int slow = n, fast = n;
    do {
        slow = getNext(slow);
        fast = getNext(getNext(fast));
    } while (slow != fast);
    return slow == 1;   // cycle at 1 → happy; cycle elsewhere → not happy
}

private int getNext(int n) {
    int sum = 0;
    while (n > 0) { int d = n % 10; sum += d * d; n /= 10; }
    return sum;
}
```

#### Example

```
Input: n = 19
getNext: 19→82→68→100→1→1 (cycle at 1) → return true ✓
Input: n = 2
getNext: 2→4→16→37→58→89→145→42→20→4 (cycle at 4, not 1) → return false ✓
```

---

### Problem 9 — Find the Duplicate Number
**LeetCode #287 | Difficulty: Medium | Company: Amazon, Microsoft | Category: Implicit Cycle**

#### Core insight

Array `nums[0..n]` contains values in `[1,n]`. Treat it as a linked list: index `i` → `nums[i]`. Duplicate means two indices map to same "next" → cycle exists. Find cycle start = duplicate.

#### Java code

```java
class Solution {
    public int findDuplicate(int[] nums) {
        int slow = 0, fast = 0;

        while (true) {
            slow = nums[slow];           // 1 step
            fast = nums[nums[fast]];     // 2 steps

            if (slow == fast) {
                slow = 0;                // Phase 2: reset slow to entry index

                while (slow != fast) {
                    slow = nums[slow];
                    fast = nums[fast];   // both 1 step
                }
                return slow;            // duplicate number
            }
        }
    }
}
```

> **Note:** Starts both pointers at index `0` — clean entry point since `nums[0]` is always in `[1,n]`, guaranteed to enter the cycle.

#### Example

```
Input: nums = [1,3,4,2,2]
Indices:        0 1 2 3 4
nums[i]:        1 3 4 2 2

Implicit list: 0→1→3→2→4→2→4→... (cycle at 2)
Phase 1: slow=1,fast=3 → slow=3,fast=2 → slow=2,fast=2 → meet
Phase 2: slow=0,fast=2
  slow=1,fast=4 → slow=3,fast=2 → slow=2,fast=2 → return 2 ✓
```

---

## Category 5 — Slow Write / Fast Read

---

### Problem 10 — String Compression
**LeetCode #443 | Difficulty: Medium | Company: Amazon, Google | Category: Slow/Fast**

#### Java code

```java
public int compress(char[] chars) {
    int slow = 0, fast = 0, n = chars.length;

    while (fast < n) {
        char ch = chars[fast]; int count = 0;

        // Count consecutive same chars
        while (fast < n && chars[fast] == ch) { fast++; count++; }

        chars[slow++] = ch;                              // write the char
        if (count > 1) {                                 // write count if > 1
            for (char c : String.valueOf(count).toCharArray())
                chars[slow++] = c;
        }
    }
    return slow;   // new length
}
```

#### Example

```
Input: ['a','a','b','b','c','c','c']
fast groups: aa→count=2, bb→count=2, ccc→count=3
slow writes: a,2,b,2,c,3
Output: length=6, chars=['a','2','b','2','c','3'] ✓
```

---

### Problem 11 — Remove Duplicates from Sorted Array
**LeetCode #26 | Difficulty: Easy | Company: Amazon, Microsoft | Category: Slow/Fast**

#### Java code

```java
public int removeDuplicates(int[] nums) {
    int slow = 1;
    for (int fast = 1; fast < nums.length; fast++) {
        if (nums[fast] != nums[fast-1]) {   // new unique value
            nums[slow++] = nums[fast];
        }
    }
    return slow;
}
```

#### Example

```
Input: [0,0,1,1,1,2,2,3,3,4]
fast=2(1): new → nums[1]=1, slow=2
fast=5(2): new → nums[2]=2, slow=3
fast=7(3): new → nums[3]=3, slow=4
fast=9(4): new → nums[4]=4, slow=5
Output: 5, nums=[0,1,2,3,4,...] ✓
```

---

### Problem 12 — Remove Duplicates from Sorted Array II
**LeetCode #80 | Difficulty: Medium | Category: Slow/Fast (allow at most 2)**

#### Core insight

Allow at most 2 of each element. Write position `slow` advances when `nums[fast] != nums[slow-2]` (different from what was written 2 positions ago).

#### Java code

```java
public int removeDuplicates(int[] nums) {
    int slow = 2;
    for (int fast = 2; fast < nums.length; fast++) {
        if (nums[fast] != nums[slow-2]) {   // not a 3rd duplicate
            nums[slow++] = nums[fast];
        }
    }
    return slow;
}
```

#### Example

```
Input: [1,1,1,2,2,3]
slow=2(init, first 2 elements always kept)
fast=2(1): nums[2]=1 == nums[0]=1 → skip
fast=3(2): nums[3]=2 != nums[1]=1 → write, slow=3
fast=4(2): nums[4]=2 != nums[2]=1 → write, slow=4
fast=5(3): nums[5]=3 != nums[3]=2 → write, slow=5
Output: 5, nums=[1,1,2,2,3,...] ✓
```

---

### Problem 13 — Duplicate Zeros
**LeetCode #1089 | Difficulty: Easy | Category: Slow/Fast (in-place)**

#### Core insight

Count how many zeros — that tells how many shifts needed. Work from back to front to avoid overwriting.

#### Java code

```java
public void duplicateZeros(int[] arr) {
    int zeros = 0, n = arr.length;
    for (int x : arr) if (x == 0) zeros++;

    int i = n - 1, j = n + zeros - 1;   // two pointers from end

    while (i >= 0) {
        if (j < n) arr[j] = arr[i];     // write only if within bounds
        j--;
        if (arr[i] == 0) {
            if (j < n) arr[j] = 0;      // duplicate the zero
            j--;
        }
        i--;
    }
}
```

#### Example

```
Input:  [1,0,2,3,0,4,5,0]
zeros=3, j starts at 10 (out of bounds mostly)
Working backwards: copies with duplication
Output: [1,0,0,2,3,0,0,4] ✓
```

---

## Category 6 — Rotate / Split + Reconnect

---

### Problem 14 — Rotate List
**LeetCode #61 | Difficulty: Medium | Company: Amazon | Category: Find tail + reconnect**

#### Approach table

| Step | Action |
|------|--------|
| 1 | Find length and tail node |
| 2 | `k = k % length` (avoid full rotations) |
| 3 | Find new tail at position `length - k` |
| 4 | `newHead = newTail.next`, `newTail.next = null`, `tail.next = head` |

#### Java code

```java
public ListNode rotateRight(ListNode head, int k) {
    if (head == null || head.next == null || k == 0) return head;

    // Step 1: find length and tail
    ListNode tail = head; int length = 1;
    while (tail.next != null) { tail = tail.next; length++; }

    // Step 2: effective rotation
    k = k % length;
    if (k == 0) return head;

    // Step 3: find new tail
    ListNode newTail = head;
    for (int i = 0; i < length - k - 1; i++) newTail = newTail.next;

    // Step 4: reconnect
    ListNode newHead = newTail.next;
    newTail.next = null;
    tail.next = head;
    return newHead;
}
```

#### Example

```
Input: 1→2→3→4→5, k=2
length=5, k=2%5=2
newTail at position 5-2-1=2: node(3)
newHead=node(4), tail(5).next=head(1)
Output: 4→5→1→2→3 ✓
```

---

### Problem 15 — Rotate Array
**LeetCode #189 | Difficulty: Medium | Company: Amazon, Microsoft | Category: Reverse trick**

#### Core insight

Rotating right by k = reverse all → reverse first k → reverse rest k.

#### Java code

```java
public void rotate(int[] nums, int k) {
    k %= nums.length;
    reverse(nums, 0, nums.length - 1);   // reverse all
    reverse(nums, 0, k - 1);             // reverse first k
    reverse(nums, k, nums.length - 1);   // reverse rest
}

private void reverse(int[] nums, int lo, int hi) {
    while (lo < hi) {
        int t = nums[lo]; nums[lo] = nums[hi]; nums[hi] = t;
        lo++; hi--;
    }
}
```

#### Example

```
Input: [1,2,3,4,5,6,7], k=3
After reverse all:  [7,6,5,4,3,2,1]
After reverse k=3:  [5,6,7,4,3,2,1]
After reverse rest: [5,6,7,1,2,3,4] ✓
```

---

## Category 7 — Two-pointer String / Array

---

### Problem 16 — Partition Labels
**LeetCode #763 | Difficulty: Medium | Company: Amazon, Google | Category: Last-occurrence boundary**

#### Core insight

Each character must appear in only one partition. For each position, the partition must extend at least to the last occurrence of the current character. When current position reaches the max boundary → partition ends.

#### Java code

```java
public List<Integer> partitionLabels(String s) {
    int[] last = new int[26];
    for (int i = 0; i < s.length(); i++) last[s.charAt(i)-'a'] = i;

    List<Integer> result = new ArrayList<>();
    int start = 0, maxReach = 0;

    for (int i = 0; i < s.length(); i++) {
        maxReach = Math.max(maxReach, last[s.charAt(i)-'a']);
        if (i == maxReach) {           // reached end of current partition
            result.add(i - start + 1);
            start = i + 1;
        }
    }
    return result;
}
```

#### Example

```
Input: s = "ababcbacadefegdehijhklij"
last: a=8, b=5, c=7, d=14, e=15, f=11, g=13, h=19, i=22, j=23, k=20, l=21

i=0(a): maxReach=8
...
i=8: i==maxReach=8 → partition 1, size=9 ("ababcbaca")
i=9(d): maxReach=14 → ... i=14: → partition 2, size=7
i=15(e): → ... → partition 3, size=8
Output: [9,7,8] ✓
```

---

### Problem 17 — Counting Binary Substrings
**LeetCode #696 | Difficulty: Easy | Company: Google | Category: Slow/Fast group counting**

> Count substrings with equal 0s and 1s, grouped consecutively.

#### Core insight

Track previous group count and current group count. When group changes, valid substrings = min(prev, curr).

#### Java code

```java
public int countBinarySubstrings(String s) {
    int prev = 0, curr = 1, count = 0;

    for (int i = 1; i < s.length(); i++) {
        if (s.charAt(i) == s.charAt(i-1)) {
            curr++;
        } else {
            prev = curr; curr = 1;
        }
        if (prev >= curr) count++;   // valid substrings where groups overlap
    }
    return count;
}
```

#### Example

```
Input: s = "00110011"
Groups: 2 zeros, 2 ones, 2 zeros, 2 ones
prev=0,curr=1: 00→curr=2; 0→1 transition: prev=2,curr=1→count+=1
curr=2: 11→curr=2; 1→0: prev=2,curr=1→count+=1; curr=2
prev=2: count+=1,count+=1 → total=6 ✓
```

---

### Problem 18 — Last Substring in Lexicographical Order
**LeetCode #1163 | Difficulty: Hard | Company: Google | Category: Two pointer comparison**

> Find the last substring in lexicographical order (without generating all substrings).

#### Core insight

The answer is always a suffix. Two pointers `i` and `j` compare suffixes. Advance the loser, skip when they agree.

#### Java code

```java
public String lastSubstring(String s) {
    int i = 0, j = 1, k = 0, n = s.length();

    while (j + k < n) {
        if (s.charAt(i+k) == s.charAt(j+k)) {
            k++;
        } else if (s.charAt(i+k) < s.charAt(j+k)) {
            i = i + k + 1;   // suffix starting at i is smaller — advance i
            if (i >= j) i = j + 1;
            k = 0;
        } else {
            j = j + k + 1;   // suffix starting at j is smaller — advance j
            k = 0;
        }
    }
    return s.substring(i);
}
```

#### Example

```
Input: s = "abab"
Compare suffixes: "abab"(0) vs "bab"(1) → 'a'<'b' → i=1
Compare "bab"(1) vs "ab"(2) → 'b'>'a' → j=3
j+k=3 ≥ n=4? 3<4 → compare "b"(1) with "b"(3) → k=1 → j+k=4 ≥ n → stop
return s.substring(1) = "bab" ✓
```

---

## Bonus / FAANG

---

### Problem 19 — Intersection of Two Linked Lists
**LeetCode #160 | Difficulty: Easy | Company: Amazon | Category: Redirect technique**

> Two pointers `p1` on A, `p2` on B. On reaching null, redirect to other list's head. They meet at intersection (or both null).

#### Java code

```java
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    ListNode p1 = headA, p2 = headB;
    while (p1 != p2) {
        p1 = (p1 == null) ? headB : p1.next;
        p2 = (p2 == null) ? headA : p2.next;
    }
    return p1;   // intersection node or null
}
```

#### Why it works

```
List A: a + c nodes  (a before intersection, c common)
List B: b + c nodes
p1 travels: a + c + b = a+b+c steps to meet
p2 travels: b + c + a = a+b+c steps to meet
Same total distance → meet at intersection ✓
```

---

### Problem 20 — Sort List
**LeetCode #148 | Difficulty: Medium | Company: Amazon | Category: Find Middle + Merge Sort**

#### Java code

```java
public ListNode sortList(ListNode head) {
    if (head == null || head.next == null) return head;

    // Step 1: find middle and split
    ListNode slow = head, fast = head.next;   // fast=head.next → left-middle
    while (fast != null && fast.next != null) {
        slow = slow.next; fast = fast.next.next;
    }
    ListNode second = slow.next;
    slow.next = null;

    // Step 2: recursively sort both halves
    ListNode left  = sortList(head);
    ListNode right = sortList(second);

    // Step 3: merge two sorted lists
    return merge(left, right);
}

private ListNode merge(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0), curr = dummy;
    while (l1 != null && l2 != null) {
        if (l1.val <= l2.val) { curr.next = l1; l1 = l1.next; }
        else                  { curr.next = l2; l2 = l2.next; }
        curr = curr.next;
    }
    curr.next = (l1 != null) ? l1 : l2;
    return dummy.next;
}
```

#### Example

```
Input: 4→2→1→3
Split: [4→2] and [1→3]
Sort each: [2→4] and [1→3]
Merge: 1→2→3→4 ✓
Time: O(n log n), Space: O(log n) recursion stack
```

---

### Problem 21 — Number of Subarrays with Bounded Maximum
**LeetCode #795 | Difficulty: Medium | Company: Google | Category: Two-pointer count**

> Count subarrays where max element is in [left, right]. Use "at most" trick: `count(max≤right) - count(max≤left-1)`.

#### Java code

```java
public int numSubarrayBoundedMax(int[] nums, int left, int right) {
    return countAtMost(nums, right) - countAtMost(nums, left - 1);
}

private int countAtMost(int[] nums, int bound) {
    int count = 0, curr = 0;
    for (int n : nums) {
        curr = (n <= bound) ? curr + 1 : 0;   // reset on element > bound
        count += curr;
    }
    return count;
}
```

#### Example

```
Input: nums = [2,1,4,3], left=2, right=3
countAtMost(3): [2,1,4,3] → curr=1,2,0,1 → count=4
countAtMost(1): [2,1,4,3] → curr=0,1,0,0 → count=1
Output: 4-1=3  ([2],[1],[2,1]) ✓
... actually [2],[1],[2,1],[3] = 4, but [2,1] max=2∈[2,3]✓, [3]✓, [2]✓, [1]✗ (1<2)
```

---

### Problem 22 — K-diff Pairs in an Array
**LeetCode #532 | Difficulty: Medium | Company: Amazon | Category: Two-pointer on sorted**

> Count unique k-diff pairs (a, b) where `b - a = k`.

#### Java code

```java
public int findPairs(int[] nums, int k) {
    if (k < 0) return 0;
    Arrays.sort(nums);
    int left = 0, right = 1, count = 0;

    while (right < nums.length) {
        int diff = nums[right] - nums[left];
        if (left == right || diff < k) {
            right++;
        } else if (diff > k) {
            left++;
        } else {
            count++;
            left++;
            // skip duplicates on left
            while (left < nums.length && nums[left] == nums[left-1]) left++;
        }
    }
    return count;
}
```

#### Example

```
Input: nums = [3,1,4,1,5], k=2
Sorted: [1,1,3,4,5]
left=0(1),right=1(1): same index check, right++
left=0(1),right=2(3): diff=2==k → count=1, left++, skip dup→left=2
left=2(3),right=3(4): diff=1<2, right++
left=2(3),right=4(5): diff=2==k → count=2, left++
left=3,right=4: diff=1<2, right++
Output: 2 (pairs: [1,3],[3,5]) ✓
```

---

## Quick Pattern Reference

| Problem | Category | Key technique |
|---------|----------|---------------|
| LinkedList Cycle | Classic Floyd's | slow==fast inside loop |
| Start of Cycle | Floyd Phase 2 | reset slow=head, both 1 step |
| Circular Array Loop | Implicit cycle | getNext with direction check |
| Middle of LinkedList | Find middle | fast=null → slow=middle |
| Palindrome LinkedList | Middle + reverse | reverse from slow, compare |
| Reorder List | Middle+reverse+merge | reverse slow.next, cut, merge |
| Remove Nth From End | Gap technique | dummy + fast k+1 ahead |
| Happy Number | Implicit cycle | getNext = sum digit squares |
| Find Duplicate | Implicit cycle | getNext = nums[i] |
| String Compression | Slow write/fast read | write char+count |
| Remove Duplicates I | Slow write | write on new value |
| Remove Duplicates II | Slow write | write when != slow-2 |
| Duplicate Zeros | Reverse from end | count zeros, work backwards |
| Rotate List | Find tail+reconnect | tail.next=head, cut new tail |
| Rotate Array | Reverse trick | reverse all → reverse k → reverse rest |
| Partition Labels | Last-occurrence | boundary = max last occurrence |
| Count Binary Substrings | Group tracking | min(prev_group, curr_group) |
| Last Substring | Two-pointer suffix | advance loser, skip on equal |
| Intersection | Redirect | switch to other list on null |
| Sort List | Middle + merge sort | split at left-middle, sort, merge |
| Bounded Max Subarrays | AtMost trick | atMost(R) - atMost(L-1) |
| K-diff Pairs | Sorted two-pointer | sort + advance by diff vs k |
