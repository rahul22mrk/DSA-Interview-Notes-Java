# Merge Interval Pattern — Complete Notes

> **Pattern family:** Array / Interval Scheduling / Greedy  
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
| "merge overlapping intervals" | sort + linear scan merge |
| "insert interval into sorted list" | 3-phase insert + merge |
| "find intersection of two interval lists" | two-pointer intersection |
| "minimum meeting rooms / conference rooms" | sort + min-heap or two-pointer on sorted start/end |
| "maximum CPU load / maximum overlap at any point" | sort + min-heap |
| "employee free time / find gaps" | merge all + find gaps |
| "remove minimum intervals to make non-overlapping" | greedy, keep earliest end |
| "minimum arrows to burst balloons" | greedy, shoot at earliest end |
| "check if any two intervals overlap" | sort + check adjacent |
| "total covered length / union of intervals" | merge + sum lengths |

### Brute force test

```
Brute force: for every pair (i, j) check if they overlap → O(n²).
→ Interviewer says "O(n log n)" → cannot check all pairs.
→ Key insight: if you SORT by start time, you only need to check
  each interval against the PREVIOUS merged interval → O(n) scan.
→ Total: O(n log n) sort + O(n) scan = O(n log n).
```

### The 5 confirming signals

**Signal 1 — Input is a list of intervals `[start, end]`**
> Any problem where data is given as pairs representing ranges.
> The first step is almost always: sort by start time.

**Signal 2 — "Overlapping" or "non-overlapping" in the problem statement**
> Two intervals `[a,b]` and `[c,d]` overlap if `a <= d && c <= b`.
> This is the single overlap check you need to memorise.

**Signal 3 — "Minimum rooms / resources needed at the same time"**
> This asks for the maximum number of simultaneously active intervals.
> Pattern: sort starts and ends separately, use two-pointer or min-heap.

**Signal 4 — "Find free time / gaps between intervals"**
> Merge all intervals first, then scan for gaps between consecutive merged intervals.

**Signal 5 — "Remove minimum intervals" or "minimum arrows"**
> Greedy: sort by end time, always keep/shoot at the earliest ending interval.
> This maximises the number of intervals handled by one action.

### Decision flowchart

```
Problem involves a list of intervals [start, end]?
        │
        ▼
What are you asked to do?
        │
        ├── MERGE overlapping → sort by start, linear scan merge
        │
        ├── INSERT new interval → 3-phase: add before, merge overlap, add after
        │
        ├── INTERSECTION of two lists → two-pointer, advance the one that ends first
        │
        ├── CHECK any overlap exists → sort by start, check adjacent ends
        │
        ├── MIN ROOMS / MAX OVERLAP at any point
        │       ├── Heap approach  → min-heap of end times, size = rooms needed
        │       └── Two-pointer    → sort starts[], sort ends[] separately
        │
        ├── FREE TIME / GAPS → merge all intervals, find gaps between consecutive
        │
        ├── REMOVE MIN to make non-overlapping → sort by end, greedy keep earliest end
        │
        └── MIN ARROWS / MIN POINTS to cover all → sort by end, greedy shoot at end
```

---

## 2. What is this pattern?

**Core idea:** Sort intervals by start time. After sorting, any overlapping intervals are always adjacent. You only need to compare each interval with the last merged result.

```
Two intervals [a, b] and [c, d] (a ≤ c after sorting):
  Overlap condition:  c <= b   (new start ≤ current end)
  Merge result:       [a, max(b, d)]
  No overlap:         b < c    → emit [a,b], start fresh with [c,d]
```

**Visual:**
```
Before sort: [3,5], [1,4], [6,8], [2,3]
After sort:  [1,4], [2,3], [3,5], [6,8]

Scan:
  curr=[1,4], next=[2,3]: 2<=4 → merge → [1,4]   (3 absorbed)
  curr=[1,4], next=[3,5]: 3<=4 → merge → [1,5]
  curr=[1,5], next=[6,8]: 6>5  → emit [1,5], start [6,8]
Result: [[1,5],[6,8]]
```

**Why sorting works:**
After sorting by start, if interval `i` doesn't overlap with the current merged interval, no future interval (with start ≥ start[i]) can overlap with it either. So you never need to look back.

---

## 3. Core rules

**Rule 1 — Always sort by start time first (unless input is already sorted)**
```java
// WRONG — without sorting, non-adjacent intervals may overlap
for (int[] interval : intervals) { ... }   // misses [1,4] and [3,5] if not adjacent

// CORRECT
Arrays.sort(intervals, (a, b) -> a[0] - b[0]);   // sort by start
// Now overlapping intervals are always adjacent → single pass works
```

**Rule 2 — Overlap condition: `newStart <= currentEnd` (not strictly less than)**
```java
// WRONG — misses touching intervals like [1,3] and [3,5]
if (intervals[i][0] < end) { merge; }   // [3,5] would not merge with [1,3]

// CORRECT — touching intervals (sharing an endpoint) ARE overlapping
if (intervals[i][0] <= end) { merge; }
// [1,3] and [3,5]: 3 <= 3 → merge → [1,5] ✓
```

**Rule 3 — For "min rooms" use min-heap of end times, NOT start times**
```java
// WRONG — heap of start times tells you nothing about when rooms free up
PriorityQueue<Integer> heap = new PriorityQueue<>();
heap.offer(intervals[i][0]);   // meaningless

// CORRECT — heap of END times: peek = earliest room that becomes free
PriorityQueue<Integer> heap = new PriorityQueue<>();   // min-heap
Arrays.sort(intervals, (a, b) -> a[0] - b[0]);         // sort by start

for (int[] interval : intervals) {
    if (!heap.isEmpty() && heap.peek() <= interval[0]) {
        heap.poll();   // room is free — reuse it
    }
    heap.offer(interval[1]);   // assign room, track end time
}
// heap.size() = minimum rooms needed
```

---

## 4. 2-Question framework

### Question 1 — What operation are you doing on intervals?

| Answer | Variant |
|--------|---------|
| Combine overlapping into fewer intervals | Merge Intervals |
| Add one new interval to sorted list | Insert Interval |
| Find common portions of two lists | Interval Intersection |
| Count how many overlap at any moment | Min Rooms / Max CPU Load |
| Find time slots with no intervals | Employee Free Time |
| Remove fewest to eliminate all overlaps | Non-overlapping Intervals |
| Minimum shots/points to cover all | Minimum Arrows |

### Question 2 — What data structure / technique?

| Technique | When to use | Key operation |
|-----------|-------------|---------------|
| **Sort + linear scan** | Merge, detect overlap, count removals | `curr.end = max(curr.end, next.end)` |
| **Sort + min-heap** | Min rooms, max CPU load | `heap.peek()` = earliest free resource |
| **Two-pointer** | Intersection of two lists, min rooms (alternative) | advance the pointer with smaller end |
| **Sort by end + greedy** | Non-overlapping, min arrows | keep/shoot at earliest end |
| **Merge all + gap scan** | Employee free time | find gaps between merged intervals |

> **Decision shortcut:**
> - "merge / combine" → sort by start, linear scan
> - "insert one interval" → 3-phase: before / overlap / after
> - "intersection" → two-pointer on two sorted lists
> - "how many rooms / max overlap" → min-heap of end times
> - "free time / gaps" → merge all, scan gaps
> - "remove min / min arrows" → sort by end, greedy

---

## 5. Variants table

> **Common core:** sort by start time → compare with previous result  
> **What differs:** what you track and what you return

| Variant | Sort by | Data structure | Key condition | Return |
|---------|---------|----------------|---------------|--------|
| Merge Intervals | start | result list | `newStart <= currEnd` | merged list |
| Insert Interval | already sorted | result list | 3-phase scan | merged list |
| Interval Intersection | already sorted | result list | `max(s1,s2) <= min(e1,e2)` | intersection list |
| Check Any Overlap | start | — | adjacent `end >= next start` | `true/false` |
| Min Meeting Rooms | start (heap) / both | min-heap of ends | `heap.peek() <= newStart` | `heap.size()` |
| Max CPU Load | start | min-heap of ends | same as rooms | max heap size |
| Employee Free Time | start | merge result | gap between `merged[i].end` and `merged[i+1].start` | gap list |
| Non-overlapping | end | — | greedy keep earliest end | count removed |
| Min Arrows | end | — | greedy: arrow at `curr.end`, skip all covered | arrow count |

---

## 6. Universal Java template

```java
// ─── TEMPLATE A: Merge Overlapping Intervals ──────────────────────────────────
public int[][] merge(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);   // sort by start
    List<int[]> res = new ArrayList<>();

    int start = intervals[0][0];
    int end   = intervals[0][1];

    for (int i = 1; i < intervals.length; i++) {
        if (intervals[i][0] <= end) {               // overlap condition
            end = Math.max(end, intervals[i][1]);   // extend end
        } else {
            res.add(new int[]{start, end});          // emit merged interval
            start = intervals[i][0];
            end   = intervals[i][1];
        }
    }
    res.add(new int[]{start, end});                  // add last interval
    return res.toArray(new int[res.size()][]);
}


// ─── TEMPLATE B: Insert Interval (3-phase) ────────────────────────────────────
public int[][] insert(int[][] intervals, int[] newInterval) {
    List<int[]> res = new ArrayList<>();
    int i = 0, n = intervals.length;

    // Phase 1: add all intervals that end BEFORE newInterval starts
    while (i < n && intervals[i][1] < newInterval[0])
        res.add(intervals[i++]);

    // Phase 2: merge all overlapping intervals into newInterval
    while (i < n && intervals[i][0] <= newInterval[1]) {
        newInterval[0] = Math.min(newInterval[0], intervals[i][0]);
        newInterval[1] = Math.max(newInterval[1], intervals[i][1]);
        i++;
    }
    res.add(newInterval);

    // Phase 3: add remaining intervals
    while (i < n) res.add(intervals[i++]);

    return res.toArray(new int[res.size()][]);
}


// ─── TEMPLATE C: Interval Intersection (Two-pointer) ─────────────────────────
public int[][] intervalIntersection(int[][] A, int[][] B) {
    List<int[]> res = new ArrayList<>();
    int i = 0, j = 0;

    while (i < A.length && j < B.length) {
        int start = Math.max(A[i][0], B[j][0]);
        int end   = Math.min(A[i][1], B[j][1]);

        if (start <= end)                            // valid intersection
            res.add(new int[]{start, end});

        if (A[i][1] <= B[j][1]) i++;                // advance the one ending first
        else                    j++;
    }
    return res.toArray(new int[res.size()][]);
}


// ─── TEMPLATE D: Min Meeting Rooms (Min-Heap) ─────────────────────────────────
public int minMeetingRooms(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);   // sort by start
    PriorityQueue<Integer> heap = new PriorityQueue<>();  // min-heap of end times

    for (int[] interval : intervals) {
        if (!heap.isEmpty() && heap.peek() <= interval[0])
            heap.poll();                              // reuse freed room
        heap.offer(interval[1]);                      // assign room
    }
    return heap.size();
}


// ─── TEMPLATE D2: Min Meeting Rooms (Two-pointer alternative) ─────────────────
public int minMeetingRooms(int[] start, int[] end) {
    Arrays.sort(start);
    Arrays.sort(end);
    int i = 0, j = 0, rooms = 0, res = 0;

    while (i < start.length) {
        if (start[i] < end[j]) {
            rooms++;
            res = Math.max(res, rooms);
            i++;
        } else {
            rooms--;
            j++;
        }
    }
    return res;
}


// ─── TEMPLATE E: Non-overlapping Intervals (Greedy, sort by end) ──────────────
public int eraseOverlapIntervals(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[1] - b[1]);   // sort by END time
    int count = 0;
    int prevEnd = intervals[0][1];

    for (int i = 1; i < intervals.length; i++) {
        if (intervals[i][0] < prevEnd) {              // overlap → remove this one
            count++;
        } else {
            prevEnd = intervals[i][1];                // no overlap → keep, update end
        }
    }
    return count;
}


// ─── TEMPLATE F: Minimum Arrows to Burst Balloons ────────────────────────────
public int findMinArrowShots(int[][] points) {
    Arrays.sort(points, (a, b) -> Integer.compare(a[1], b[1]));  // sort by end
    int arrows = 1;
    int arrowPos = points[0][1];                      // shoot at first balloon's end

    for (int i = 1; i < points.length; i++) {
        if (points[i][0] > arrowPos) {                // balloon not hit
            arrows++;
            arrowPos = points[i][1];                  // shoot at this balloon's end
        }
    }
    return arrows;
}


// ─── TEMPLATE G: Employee Free Time (Merge + Gap scan) ───────────────────────
// Input: list of lists of intervals per employee
public List<Interval> employeeFreeTime(List<List<Interval>> schedule) {
    List<Interval> all = new ArrayList<>();
    for (List<Interval> emp : schedule) all.addAll(emp);
    all.sort((a, b) -> a.start - b.start);

    List<Interval> merged = new ArrayList<>();
    int start = all.get(0).start, end = all.get(0).end;
    for (Interval iv : all) {
        if (iv.start <= end) end = Math.max(end, iv.end);
        else { merged.add(new Interval(start, end)); start = iv.start; end = iv.end; }
    }
    merged.add(new Interval(start, end));

    List<Interval> res = new ArrayList<>();
    for (int i = 1; i < merged.size(); i++)
        res.add(new Interval(merged.get(i-1).end, merged.get(i).start));
    return res;
}
```

---

## 7. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                          → VARIANT               → KEY CODE
──────────────────────────────────────────────────────────────────────────────────────
"merge overlapping intervals"              → Sort + scan           → sort start; if newStart<=end: end=max(end,newEnd)
"insert interval into sorted list"         → 3-phase insert        → before / merge-overlap / after
"intersection of two interval lists"       → Two-pointer           → max(s1,s2)<=min(e1,e2); advance smaller end
"any two intervals overlap?"               → Sort + adjacent check → sorted[i].end >= sorted[i+1].start
"min meeting rooms / min resources"        → Min-heap of ends      → heap.peek()<=newStart → reuse room
"max CPU load / max overlap count"         → Min-heap of ends      → same as rooms, track max heap size
"employee free time / find gaps"           → Merge + gap scan      → gap between merged[i].end & merged[i+1].start
"remove min intervals → non-overlapping"   → Sort by end, greedy   → keep earliest end; count skipped
"min arrows / min points to cover all"     → Sort by end, greedy   → shoot at currEnd; skip all covered
```

**The overlap rules — burn these into memory:**
```java
// Two intervals [a,b] and [c,d] where a <= c (after sorting):
// OVERLAP:    c <= b          (touching counts as overlap)
// NO OVERLAP: c > b           (gap between them)
// MERGE:      [a, max(b,d)]

// Insert interval — 3 cases:
// Before:    intervals[i][1] < newInterval[0]   → add as-is
// Overlap:   intervals[i][0] <= newInterval[1]  → expand newInterval
// After:     remaining after merge              → add as-is

// Min rooms — when to REUSE a room:
// heap.peek() <= interval[0]   (room freed before or exactly when new meeting starts)
```

---

## 8. Common mistakes

### Mistake 1 — Forgetting to sort before merging

```java
// BUG — intervals not sorted, adjacent check misses non-adjacent overlaps
for (int i = 1; i < intervals.length; i++) {
    if (intervals[i][0] <= end) ...   // [3,5] and [1,4] won't be adjacent

// FIX — always sort by start first
Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
```

### Mistake 2 — Wrong overlap condition (strict < instead of <=)

```java
// BUG — touching intervals [1,3] and [3,5] are NOT merged
if (intervals[i][0] < end) { merge; }   // 3 < 3 is false → not merged → WRONG

// FIX — use <= to handle touching endpoints
if (intervals[i][0] <= end) { merge; }  // 3 <= 3 is true → merged → [1,5] ✓
```

### Mistake 3 — Not updating `end` with max in merge

```java
// BUG — contained interval shrinks the merged end
// e.g., current=[1,10], next=[2,5]: end = 5 (WRONG — loses [5,10])
end = intervals[i][1];

// FIX — always take max of both ends
end = Math.max(end, intervals[i][1]);   // end stays 10 ✓
```

### Mistake 4 — Forgetting to add the last interval after the loop

```java
// BUG — the last merged interval is never emitted (loop ends without adding it)
for (int i = 1; i < intervals.length; i++) {
    if (overlap) { merge; }
    else { res.add(...); }   // last interval added only on overlap detection
}
// If last interval doesn't overlap with anything, it's never added!

// FIX — always add after the loop
res.add(new int[]{start, end});   // add the last pending interval
```

### Mistake 5 — Wrong heap condition for meeting rooms (strict < instead of <=)

```java
// BUG — room freed at time 5, new meeting starts at 5 → should reuse
if (heap.peek() < interval[0]) heap.poll();   // 5 < 5 is false → new room allocated (WRONG)

// FIX — use <= (room freed at exactly the start time can be reused)
if (heap.peek() <= interval[0]) heap.poll();  // 5 <= 5 is true → reuse ✓
```

### Mistake 6 — Sorting by start instead of end for greedy problems

```java
// BUG — sorting by start for non-overlapping removal gives wrong greedy choice
Arrays.sort(intervals, (a, b) -> a[0] - b[0]);   // sort by start → WRONG for greedy

// FIX — sort by END for all greedy interval problems
Arrays.sort(intervals, (a, b) -> a[1] - b[1]);   // sort by end → always correct greedy
// Keeping the interval with earliest end leaves maximum room for future intervals
```

### Mistake 7 — Using Integer subtraction in comparator (overflow risk)

```java
// BUG — if a[1] is very negative and b[1] is very positive, a[1]-b[1] overflows
Arrays.sort(points, (a, b) -> a[1] - b[1]);

// FIX — use Integer.compare() for safety
Arrays.sort(points, (a, b) -> Integer.compare(a[1], b[1]));
```

---

## 9. Complexity summary

| Problem | Time | Space | Notes |
|---------|------|-------|-------|
| Merge Intervals | O(n log n) | O(n) | sort + single pass |
| Insert Interval | O(n) | O(n) | input already sorted, 3-phase scan |
| Interval Intersection | O(m + n) | O(m + n) | two-pointer, one pass each list |
| Check Any Overlap | O(n log n) | O(1) | sort + single adjacent check |
| Min Meeting Rooms (heap) | O(n log n) | O(n) | sort + heap, heap size ≤ n |
| Min Meeting Rooms (two-ptr) | O(n log n) | O(n) | sort both arrays separately |
| Max CPU Load | O(n log n) | O(n) | same as meeting rooms |
| Employee Free Time | O(n log n) | O(n) | merge all employees' intervals |
| Non-overlapping Intervals | O(n log n) | O(1) | sort by end, greedy count |
| Min Arrows to Burst Balloons | O(n log n) | O(1) | sort by end, greedy shoot |

**General rules:**
- Sorting dominates: all variants are **O(n log n)** minimum.
- Space is **O(n)** when building a result list, **O(1)** extra for in-place greedy problems.
- Heap-based variants add **O(n log n)** heap operations on top of sorting — same asymptotic.
- Two-pointer approach for min rooms is **O(1)** extra space vs O(n) for heap.
- When you see "already sorted" in the problem → Insert Interval drops to **O(n)**.

---

*Merge Interval is one of the most frequently tested patterns at FAANG.*
*Master the overlap condition `c <= b` and the 3-phase insert — these cover 80% of all interval problems.*
