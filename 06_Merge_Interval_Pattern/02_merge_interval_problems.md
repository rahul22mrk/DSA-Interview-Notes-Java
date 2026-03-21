# Merge Interval Pattern — Solved Problems (13 Problems)

> **Pattern family:** Array / Interval Scheduling / Greedy
> **Notes & Templates:** [01_merge_interval_notes.md](./01_merge_interval_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — Core Merge / Insert
- [P1 — Merge Intervals](#problem-1--merge-intervals)
- [P2 — Insert Interval](#problem-2--insert-interval)

### Category 2 — Intersection / Overlap Detection
- [P3 — Interval List Intersections](#problem-3--interval-list-intersections)
- [P4 — Overlapping Intervals (Check)](#problem-4--overlapping-intervals-check)

### Category 3 — Resource Scheduling (Heap)
- [P5 — Minimum Meeting Rooms](#problem-5--minimum-meeting-rooms)
- [P6 — Maximum CPU Load](#problem-6--maximum-cpu-load)
- [P7 — Task Scheduler](#problem-7--task-scheduler)

### Category 4 — Greedy (Sort by End)
- [P8 — Non-overlapping Intervals](#problem-8--non-overlapping-intervals)
- [P9 — Minimum Number of Arrows to Burst Balloons](#problem-9--minimum-number-of-arrows-to-burst-balloons)
- [P10 — Meeting Scheduler](#problem-10--meeting-scheduler)

### Category 5 — Hard / FAANG
- [P11 — Employee Free Time](#problem-11--employee-free-time)
- [P12 — Remove Covered Intervals](#problem-12--remove-covered-intervals)
- [P13 — Data Stream as Disjoint Intervals](#problem-13--data-stream-as-disjoint-intervals)

---

## Category 1 — Core Merge / Insert

---

### Problem 1 — Merge Intervals
**LeetCode #56 | Difficulty: Medium | Company: Amazon, Google, Facebook | Category: Sort + Linear Scan**

> Given an array of intervals, merge all overlapping intervals and return the result.

#### Core insight

Sort by start time. After sorting, overlapping intervals are always adjacent. Track `start` and `end` of current merged interval. When the next interval's start exceeds `end`, emit and reset.

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Sort | — | by start time |
| Init | — | `start = intervals[0][0]`, `end = intervals[0][1]` |
| Overlap | `intervals[i][0] <= end` | `end = max(end, intervals[i][1])` |
| No overlap | `intervals[i][0] > end` | emit `[start, end]`, reset to `intervals[i]` |
| After loop | — | emit last `[start, end]` |

#### My Solution

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        if (intervals.length == 0) return new int[0][0];
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        List<int[]> res = new ArrayList<>();
        int start = intervals[0][0];
        int end = intervals[0][1];
        for (int i = 1; i < intervals.length; i++) {
            if (end >= intervals[i][0]) {
                end = Math.max(end, intervals[i][1]);
            } else {
                res.add(new int[]{start, end});
                start = intervals[i][0];
                end = intervals[i][1];
            }
        }
        res.add(new int[]{start, end});
        return res.toArray(new int[res.size()][]);
    }
}
```

> **Note:** Tracks `start` and `end` as separate variables — clear and interview-friendly. Both solutions are identical in logic.

#### Reference Solution

```java
public int[][] merge(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
    List<int[]> res = new ArrayList<>();

    int[] curr = intervals[0];
    for (int i = 1; i < intervals.length; i++) {
        if (intervals[i][0] <= curr[1]) {
            curr[1] = Math.max(curr[1], intervals[i][1]);   // extend in place
        } else {
            res.add(curr);
            curr = intervals[i];
        }
    }
    res.add(curr);
    return res.toArray(new int[res.size()][]);
}
```

#### Example

```
Input: [[1,3],[2,6],[8,10],[15,18]]
Sorted: [[1,3],[2,6],[8,10],[15,18]]

start=1, end=3
i=1: [2,6] → 2<=3 → end=max(3,6)=6
i=2: [8,10] → 8>6 → emit [1,6], start=8,end=10
i=3: [15,18] → 15>10 → emit [8,10], start=15,end=18
After loop: emit [15,18]

Output: [[1,6],[8,10],[15,18]] ✓
```

---

### Problem 2 — Insert Interval
**LeetCode #57 | Difficulty: Medium | Company: Google, LinkedIn | Category: 3-Phase Insert**

> Insert a new interval into a sorted non-overlapping list, merging if necessary.

#### Core insight

3-phase scan: (1) add all intervals ending before newInterval starts, (2) merge all overlapping into newInterval, (3) add remaining. No sorting needed — input is already sorted.

#### Approach table

| Phase | Condition | Action |
|-------|-----------|--------|
| 1 — Before | `intervals[i][1] < newInterval[0]` | add as-is, advance i |
| 2 — Overlap | `intervals[i][0] <= newInterval[1]` | expand newInterval, advance i |
| Add | — | add merged newInterval |
| 3 — After | remaining | add as-is |

#### My Solution

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> res = new ArrayList<>();
        int i = 0;
        int n = intervals.length;
        // 1️⃣ Add all intervals before newInterval
        while (i < n && intervals[i][1] < newInterval[0]) {
            res.add(intervals[i]);
            i++;
        }
        // 2️⃣ Merge overlapping intervals
        while (i < n && intervals[i][0] <= newInterval[1]) {
            newInterval[0] = Math.min(newInterval[0], intervals[i][0]);
            newInterval[1] = Math.max(newInterval[1], intervals[i][1]);
            i++;
        }
        res.add(newInterval);
        // 3️⃣ Add remaining intervals
        while (i < n) {
            res.add(intervals[i]);
            i++;
        }
        return res.toArray(new int[res.size()][]);
    }
}
```

> **Note:** The 3-phase structure with comments is exactly the right way to write this in an interview — clear phases, easy to trace. Reference condenses into one loop but is harder to explain.

#### Reference Solution

```java
public int[][] insert(int[][] intervals, int[] newInterval) {
    List<int[]> res = new ArrayList<>();
    int i = 0, n = intervals.length;

    while (i < n && intervals[i][1] < newInterval[0]) res.add(intervals[i++]);
    while (i < n && intervals[i][0] <= newInterval[1]) {
        newInterval[0] = Math.min(newInterval[0], intervals[i][0]);
        newInterval[1] = Math.max(newInterval[1], intervals[i][1]);
        i++;
    }
    res.add(newInterval);
    while (i < n) res.add(intervals[i++]);
    return res.toArray(new int[res.size()][]);
}
```

#### Example

```
intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]

Phase 1: [1,2] ends at 2 < 4 → add. [3,5] ends at 5 >= 4 → stop.  res=[[1,2]]
Phase 2: [3,5]: 3<=8 → new=[min(4,3),max(8,5)]=[3,8]
         [6,7]: 6<=8 → new=[min(3,6),max(8,7)]=[3,8]
         [8,10]: 8<=8 → new=[min(3,8),max(8,10)]=[3,10]
         [12,16]: 12>8 → stop.  add [3,10]
Phase 3: add [12,16]

Output: [[1,2],[3,10],[12,16]] ✓
```

---

## Category 2 — Intersection / Overlap Detection

---

### Problem 3 — Interval List Intersections
**LeetCode #986 | Difficulty: Medium | Company: Facebook, Amazon | Category: Two-pointer**

> Given two sorted lists of intervals, return their intersection.

#### Core insight

Two pointers `i` and `j`. Check if current pair intersects: `max(start1,start2) <= min(end1,end2)`. Advance the pointer whose interval ends first — it can't intersect with any future interval from the other list.

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Intersect check | `max(s1,s2) <= min(e1,e2)` | add `[max(s1,s2), min(e1,e2)]` |
| Advance | `end1 <= end2` | `i++` |
| Advance | `end1 > end2` | `j++` |

#### My Solution

```java
class Solution {
    public int[][] intervalIntersection(int[][] firstList, int[][] secondList) {
        List<int[]> res = new ArrayList<>();
        int i = 0, j = 0;
        while (i < firstList.length && j < secondList.length) {
            int start1 = firstList[i][0],  end1 = firstList[i][1];
            int start2 = secondList[j][0], end2 = secondList[j][1];
            if (start1 <= start2) {
                if (end1 >= start2) {
                    int start = Math.max(start1, start2);
                    int end   = Math.min(end1, end2);
                    res.add(new int[]{start, end});
                }
            } else {
                if (end2 >= start1) {
                    int start = Math.max(start1, start2);
                    int end   = Math.min(end1, end2);
                    res.add(new int[]{start, end});
                }
            }
            if (end1 <= end2) i++;
            else              j++;
        }
        return res.toArray(new int[res.size()][]);
    }
}
```

> **Note:** Splits the check into two cases (start1 <= start2 vs start2 < start1). Reference unifies both cases into a single `max/min` check which is cleaner — both produce the same result.

#### Reference Solution

```java
public int[][] intervalIntersection(int[][] A, int[][] B) {
    List<int[]> res = new ArrayList<>();
    int i = 0, j = 0;

    while (i < A.length && j < B.length) {
        int start = Math.max(A[i][0], B[j][0]);
        int end   = Math.min(A[i][1], B[j][1]);

        if (start <= end) res.add(new int[]{start, end});   // valid intersection

        if (A[i][1] <= B[j][1]) i++;
        else                    j++;
    }
    return res.toArray(new int[res.size()][]);
}
```

#### Example

```
A = [[0,2],[5,10],[13,23],[24,25]]
B = [[1,5],[8,12],[15,24],[25,26]]

i=0,j=0: max(0,1)=1, min(2,5)=2 → 1<=2 → [1,2]. A ends first → i=1
i=1,j=0: max(5,1)=5, min(10,5)=5 → 5<=5 → [5,5]. B ends first → j=1
i=1,j=1: max(5,8)=8, min(10,12)=10 → 8<=10 → [8,10]. A ends first → i=2
i=2,j=1: max(13,8)=13, min(23,12)=12 → 13>12 → no intersection. B ends → j=2
i=2,j=2: max(13,15)=15, min(23,24)=23 → 15<=23 → [15,23]. A ends → i=3
i=3,j=2: max(24,15)=24, min(25,24)=24 → 24<=24 → [24,24]. B ends → j=3
i=3,j=3: max(24,25)=25, min(25,26)=25 → 25<=25 → [25,25]. A ends → i=4

Output: [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]] ✓
```

---

### Problem 4 — Overlapping Intervals (Check)
**GFG | Difficulty: Easy | Company: Amazon | Category: Sort + Adjacent Check**

> Given a list of intervals, check if any two intervals overlap.

#### Core insight

Sort by start. After sorting, any overlap must be between adjacent intervals. Check if `end of previous >= start of next`.

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Sort | — | by start time |
| Check adjacent | `prev.end >= curr.start` | return `true` |
| Update | — | `prev.end = curr.end`, advance |

#### My Solution

```java
class Solution {
    static boolean isIntersect(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        int e1 = intervals[0][1];
        for (int i = 1; i < intervals.length; i++) {
            if (e1 >= intervals[i][0]) {
                return true;
            }
            e1 = intervals[i][1];
        }
        return false;
    }
}
```

#### Reference Solution

```java
public boolean isOverlapping(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
    for (int i = 1; i < intervals.length; i++) {
        if (intervals[i][0] < intervals[i-1][1])   // strict < : touching not counted
            return true;
    }
    return false;
}
```

#### Example

```
intervals = [[1,3],[2,5],[7,9]]
Sorted: [[1,3],[2,5],[7,9]]

e1=3
i=1: [2,5] → 3>=2 → return true ✓ (overlap between [1,3] and [2,5])
```

---

## Category 3 — Resource Scheduling (Heap)

---

### Problem 5 — Minimum Meeting Rooms
**LeetCode #253 | Difficulty: Hard | Company: Google, Facebook, Amazon | Category: Min-Heap**

> Given meeting intervals, find the minimum number of conference rooms required.

#### Core insight

Sort by start. Use a min-heap of end times. For each new meeting: if the earliest-ending room is free (heap.peek() <= start), reuse it. Otherwise allocate a new room. Heap size = rooms in use.

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Sort | — | by start time |
| Free room exists | `heap.peek() <= interval[0]` | `heap.poll()` — reuse room |
| No free room | heap empty or all busy | allocate new room |
| Always | — | `heap.offer(interval[1])` — track end |
| Result | — | `heap.size()` |

#### My Solution

```java
class Solution {
    public int minMeetingRooms(int[] start, int[] end) {
        Arrays.sort(start);
        Arrays.sort(end);
        int i = 0, j = 0, room = 0, res = 0;
        while (i < start.length) {
            if (start[i] < end[j]) {
                room++;
                res = Math.max(room, res);
                i++;
            } else {
                room--;
                j++;
            }
        }
        return res;
    }
}
```

> **Note:** Two-pointer approach — sort `start[]` and `end[]` separately. If a new meeting starts before the earliest-ending meeting ends → need a new room. Otherwise a room frees up. O(1) extra space vs O(n) for heap. Reference uses min-heap with `int[][]` input format.

#### Reference Solution

```java
public int minMeetingRooms(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
    PriorityQueue<Integer> heap = new PriorityQueue<>();   // min-heap of end times

    for (int[] interval : intervals) {
        if (!heap.isEmpty() && heap.peek() <= interval[0])
            heap.poll();           // earliest room is free — reuse it
        heap.offer(interval[1]);   // assign room, track its end time
    }
    return heap.size();
}
```

#### Example

```
intervals = [[0,30],[5,10],[15,20]]
Sorted: [[0,30],[5,10],[15,20]]

[0,30]: heap empty → offer 30.  heap=[30]
[5,10]: peek=30 > 5 → new room, offer 10. heap=[10,30]
[15,20]: peek=10 <= 15 → reuse! poll 10, offer 20. heap=[20,30]

heap.size() = 2 ✓
```

---

### Problem 6 — Maximum CPU Load
**Educative | Difficulty: Hard | Company: Amazon, Google | Category: Min-Heap**

> Given jobs with start, end, and CPU load, find the maximum CPU load at any time.

#### Core insight

Same structure as Min Meeting Rooms, but instead of counting rooms, accumulate CPU load. Subtract load of completed jobs (heap by end time), add current job's load, track maximum.

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Sort | — | by start time |
| Pop completed | `heap.peek()[1] <= job[0]` | subtract load, pop |
| Add job | — | push `[job[2], job[1]]` (load, end), add load |
| Track | — | `maxLoad = max(maxLoad, currentLoad)` |

#### Java code

```java
public int findMaxCPULoad(int[][] jobs) {
    Arrays.sort(jobs, (a, b) -> a[0] - b[0]);
    PriorityQueue<int[]> heap = new PriorityQueue<>((a, b) -> a[1] - b[1]); // min by end

    int currentLoad = 0, maxLoad = 0;

    for (int[] job : jobs) {
        // Remove all jobs that ended before this one starts
        while (!heap.isEmpty() && heap.peek()[1] <= job[0]) {
            currentLoad -= heap.poll()[0];   // subtract their load
        }
        heap.offer(new int[]{job[2], job[1]});   // [load, endTime]
        currentLoad += job[2];
        maxLoad = Math.max(maxLoad, currentLoad);
    }
    return maxLoad;
}
```

#### Example

```
jobs = [[1,4,3],[2,5,4],[7,9,6]]  (start, end, load)
Sorted: [[1,4,3],[2,5,4],[7,9,6]]

[1,4,3]: heap empty, add. heap=[[3,4]], load=3, max=3
[2,5,4]: peek.end=4 > 2 → no pop. add. heap=[[3,4],[4,5]], load=7, max=7
[7,9,6]: peek.end=4<=7 → pop [3,4], load=4
         peek.end=5<=7 → pop [4,5], load=0
         add [6,9]. heap=[[6,9]], load=6, max=7

Output: 7 ✓
```

---

### Problem 7 — Task Scheduler
**LeetCode #621 | Difficulty: Medium | Company: Facebook, Amazon | Category: Greedy + Heap**

> Given tasks with a cooldown `n`, find the minimum time to execute all tasks.

#### Core insight

Always execute the most frequent remaining task. Use a max-heap. After each cooldown window of `n+1` slots, push back tasks with decremented counts. Answer = total slots used.

#### Java code

```java
public int leastInterval(char[] tasks, int n) {
    int[] freq = new int[26];
    for (char c : tasks) freq[c - 'A']++;

    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    for (int f : freq) if (f > 0) maxHeap.offer(f);

    int time = 0;
    while (!maxHeap.isEmpty()) {
        List<Integer> temp = new ArrayList<>();
        int cycle = n + 1;                          // one full cooldown window

        while (cycle > 0 && !maxHeap.isEmpty()) {
            temp.add(maxHeap.poll() - 1);           // execute task
            cycle--;
        }
        for (int t : temp) if (t > 0) maxHeap.offer(t);

        time += maxHeap.isEmpty() ? (n + 1 - cycle) : (n + 1);  // idle or full cycle
    }
    return time;
}
```

#### Example

```
tasks = ['A','A','A','B','B','B'], n = 2

freq: A=3, B=3. maxHeap=[3,3]

Cycle 1: execute A(→2), B(→2). cycle=1 left → idle 1.  time=3
Cycle 2: execute A(→1), B(→1). cycle=1 left → idle 1.  time=6
Cycle 3: execute A(→0), B(→0). heap empty → time += 2.  time=8

Output: 8  (A B idle A B idle A B) ✓
```

---

## Category 4 — Greedy (Sort by End)

---

### Problem 8 — Non-overlapping Intervals
**LeetCode #435 | Difficulty: Medium | Company: Google, Amazon | Category: Greedy Sort by End**

> Find the minimum number of intervals to remove to make the rest non-overlapping.

#### Core insight

Greedy: sort by end time. Keep as many intervals as possible. When two overlap, always remove the one with the later end (keep the earlier end — leaves more room for future intervals). Count removals.

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Sort | — | by end time |
| No overlap | `intervals[i][0] >= prevEnd` | keep it, `prevEnd = intervals[i][1]` |
| Overlap | `intervals[i][0] < prevEnd` | remove (count++), keep prevEnd unchanged |

#### Java code

```java
public int eraseOverlapIntervals(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[1] - b[1]);   // sort by END
    int count = 0;
    int prevEnd = intervals[0][1];

    for (int i = 1; i < intervals.length; i++) {
        if (intervals[i][0] < prevEnd) {
            count++;                          // overlap → remove current (later end)
        } else {
            prevEnd = intervals[i][1];        // no overlap → keep, advance end
        }
    }
    return count;
}
```

#### Example

```
intervals = [[1,2],[2,3],[3,4],[1,3]]
Sort by end: [[1,2],[2,3],[1,3],[3,4]]

prevEnd=2
i=1: [2,3] → 2>=2 → keep. prevEnd=3
i=2: [1,3] → 1<3 → overlap! count=1
i=3: [3,4] → 3>=3 → keep. prevEnd=4

Output: 1  (remove [1,3]) ✓
```

---

### Problem 9 — Minimum Number of Arrows to Burst Balloons
**LeetCode #452 | Difficulty: Medium | Company: Microsoft, Amazon | Category: Greedy Sort by End**

> Balloons are represented as `[xstart, xend]`. An arrow shot at x bursts all balloons with `xstart <= x <= xend`. Find minimum arrows needed.

#### Core insight

Identical greedy to Non-overlapping. Sort by end. Shoot at the end of the first balloon. Any balloon whose start ≤ current arrow position is burst. When a balloon's start > arrow position, shoot a new arrow at its end.

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Sort | — | by end (xend) |
| Init | — | `arrows=1`, `arrowPos=points[0][1]` |
| Not hit | `points[i][0] > arrowPos` | `arrows++`, `arrowPos = points[i][1]` |
| Already hit | `points[i][0] <= arrowPos` | skip (same arrow bursts it) |

#### Java code

```java
public int findMinArrowShots(int[][] points) {
    Arrays.sort(points, (a, b) -> Integer.compare(a[1], b[1]));   // sort by end
    int arrows = 1;
    int arrowPos = points[0][1];

    for (int i = 1; i < points.length; i++) {
        if (points[i][0] > arrowPos) {        // balloon not burst by current arrow
            arrows++;
            arrowPos = points[i][1];           // shoot new arrow at this balloon's end
        }
    }
    return arrows;
}
```

#### Example

```
points = [[10,16],[2,8],[1,6],[7,12]]
Sort by end: [[1,6],[2,8],[7,12],[10,16]]

arrows=1, arrowPos=6
i=1: [2,8] → 2<=6 → burst by arrow at 6. skip.
i=2: [7,12] → 7>6 → new arrow! arrows=2, arrowPos=12
i=3: [10,16] → 10<=12 → burst by arrow at 12. skip.

Output: 2 ✓
```

---

### Problem 10 — Meeting Scheduler
**LeetCode #1229 | Difficulty: Medium | Company: Facebook, Google | Category: Two-pointer on sorted**

> Given availability slots of two people and a meeting duration, find the earliest slot where both are free for the required duration.

#### Core insight

Sort both slot lists. Use two pointers. For each pair of overlapping slots, check if the intersection is long enough. Advance the pointer with the earlier end.

#### Java code

```java
public List<Integer> minAvailableDuration(int[][] slots1, int[][] slots2, int duration) {
    Arrays.sort(slots1, (a, b) -> a[0] - b[0]);
    Arrays.sort(slots2, (a, b) -> a[0] - b[0]);
    int i = 0, j = 0;

    while (i < slots1.length && j < slots2.length) {
        int start = Math.max(slots1[i][0], slots2[j][0]);
        int end   = Math.min(slots1[i][1], slots2[j][1]);

        if (end - start >= duration)
            return Arrays.asList(start, start + duration);

        if (slots1[i][1] <= slots2[j][1]) i++;
        else                              j++;
    }
    return new ArrayList<>();
}
```

#### Example

```
slots1=[[10,50],[60,120],[140,210]], slots2=[[0,15],[60,70]], duration=8

Sort both (already sorted).
i=0,j=0: max(10,0)=10, min(50,15)=15 → 15-10=5 < 8. slots2 ends first → j=1
i=0,j=1: max(10,60)=60, min(50,70)=50 → 50<60 → no overlap. slots1 ends first → i=1
i=1,j=1: max(60,60)=60, min(120,70)=70 → 70-60=10 >= 8 → return [60, 68] ✓
```

---

## Category 5 — Hard / FAANG

---

### Problem 11 — Employee Free Time
**LeetCode #759 | Difficulty: Hard | Company: Uber, Airbnb, Google | Category: Merge All + Gap Scan**

> Given schedules of multiple employees, find the list of finite intervals representing their common free time.

#### Core insight

Flatten all intervals into one list, sort by start, merge overlapping. Then scan the merged list for gaps between consecutive intervals — those gaps are free time for everyone.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| Flatten | collect all intervals | from all employees |
| Sort | by start | treat as one big list |
| Merge | standard merge | same as Problem 1 |
| Gaps | `merged[i].end` to `merged[i+1].start` | free time intervals |

#### Java code

```java
public List<Interval> employeeFreeTime(List<List<Interval>> schedule) {
    // Flatten all intervals
    List<int[]> all = new ArrayList<>();
    for (List<Interval> emp : schedule)
        for (Interval iv : emp)
            all.add(new int[]{iv.start, iv.end});

    all.sort((a, b) -> a[0] - b[0]);

    // Merge overlapping
    List<int[]> merged = new ArrayList<>();
    int[] curr = all.get(0);
    for (int[] iv : all) {
        if (iv[0] <= curr[1]) curr[1] = Math.max(curr[1], iv[1]);
        else { merged.add(curr); curr = iv; }
    }
    merged.add(curr);

    // Find gaps
    List<Interval> res = new ArrayList<>();
    for (int i = 1; i < merged.size(); i++)
        res.add(new Interval(merged.get(i-1)[1], merged.get(i)[0]));

    return res;
}
```

#### Example

```
Employee 1: [[1,3],[6,7]]
Employee 2: [[2,4]]
Employee 3: [[2,5],[9,12]]

Flattened + sorted: [1,3],[2,4],[2,5],[6,7],[9,12]
Merged: [1,5],[6,7],[9,12]
Gaps:   [5,6] and [7,9]

Output: [[5,6],[7,9]] ✓
```

---

### Problem 12 — Remove Covered Intervals
**LeetCode #1288 | Difficulty: Medium | Company: Google | Category: Sort + Greedy**

> Given a list of intervals, remove all intervals that are covered by another interval. Return the count of remaining intervals.

#### Core insight

Sort by start ascending, then by end **descending** (so for same start, longer interval comes first). Walk through — if current interval's end ≤ `maxEnd` seen so far, it's covered. Otherwise keep it.

#### Approach table

| Step | Condition | Action |
|------|-----------|--------|
| Sort | start asc, end desc | longer interval first for same start |
| Covered | `interval[1] <= maxEnd` | skip (covered) |
| Not covered | `interval[1] > maxEnd` | keep, `count++`, update `maxEnd` |

#### Java code

```java
public int removeCoveredIntervals(int[][] intervals) {
    // Sort by start asc; for same start, by end desc (longer first)
    Arrays.sort(intervals, (a, b) -> a[0] != b[0] ? a[0] - b[0] : b[1] - a[1]);

    int count = 0, maxEnd = 0;
    for (int[] interval : intervals) {
        if (interval[1] > maxEnd) {
            count++;
            maxEnd = interval[1];
        }
        // else: covered by a previous interval, skip
    }
    return count;
}
```

#### Example

```
intervals = [[1,4],[3,6],[2,8]]
Sort (start asc, end desc): [[1,8],[1,4] wait... → [[1,4],[1,8] → no]
Actually: [[1,4],[2,8],[3,6]]
Sort: start=1→[1,4]; start=2→[2,8]; start=3→[3,6]

maxEnd=0
[1,4]: 4>0 → count=1, maxEnd=4
[2,8]: 8>4 → count=2, maxEnd=8
[3,6]: 6<=8 → covered, skip

Output: 2 ✓
```

---

### Problem 13 — Data Stream as Disjoint Intervals
**LeetCode #352 | Difficulty: Hard | Company: Google, Palantir | Category: TreeMap + Merge**

> A data stream generates integers. After each `addNum(val)`, `getIntervals()` returns the sorted disjoint intervals covering all numbers added.

#### Core insight

Use a `TreeMap<Integer, Integer>` where key = start, value = end. For each new number, find if it can extend an existing interval or merge adjacent ones. `floorKey` and `ceilingKey` give the neighbours in O(log n).

#### Java code

```java
class SummaryRanges {
    TreeMap<Integer, Integer> map = new TreeMap<>();

    public void addNum(int val) {
        if (map.containsKey(val)) return;

        Integer lo = map.floorKey(val);    // interval starting at or before val
        Integer hi = map.ceilingKey(val);  // interval starting at or after val

        boolean mergeLeft  = lo != null && map.get(lo) + 1 >= val;
        boolean mergeRight = hi != null && hi <= val + 1;

        if (mergeLeft && mergeRight) {
            map.put(lo, map.get(hi));   // merge both sides
            map.remove(hi);
        } else if (mergeLeft) {
            map.put(lo, Math.max(map.get(lo), val));
        } else if (mergeRight) {
            map.put(val, map.get(hi));
            map.remove(hi);
        } else {
            map.put(val, val);           // new standalone interval
        }
    }

    public int[][] getIntervals() {
        int[][] res = new int[map.size()][2];
        int i = 0;
        for (Map.Entry<Integer, Integer> e : map.entrySet())
            res[i++] = new int[]{e.getKey(), e.getValue()};
        return res;
    }
}
```

#### Example

```
addNum(1): map={1:1}  → [[1,1]]
addNum(3): map={1:1,3:3} → [[1,1],[3,3]]
addNum(7): map={1:1,3:3,7:7} → [[1,1],[3,3],[7,7]]
addNum(2): lo=1(end=1), hi=3: mergeLeft(1+1>=2✓) mergeRight(3<=3✓)
           → merge both: map={1:3,7:7} → [[1,3],[7,7]]
addNum(6): lo=1(end=3), hi=7: mergeRight(7<=7✓)
           → map.put(6,7), remove 7: map={1:3,6:7} → [[1,3],[6,7]]
```

---

## Quick Pattern Reference

| Problem | Category | Key technique |
|---------|----------|---------------|
| Merge Intervals | Sort + scan | sort start; `newStart<=end` → extend |
| Insert Interval | 3-phase | before / merge-overlap / after |
| Interval Intersections | Two-pointer | `max(s1,s2)<=min(e1,e2)`; advance smaller end |
| Overlapping Check | Sort + adjacent | sorted `end[i] >= start[i+1]` |
| Min Meeting Rooms | Min-heap / two-ptr | heap of ends; `peek <= newStart` → reuse |
| Max CPU Load | Min-heap | same as rooms, track running load |
| Task Scheduler | Max-heap + greedy | most frequent first per cooldown window |
| Non-overlapping | Greedy sort end | keep earliest end; count removed |
| Min Arrows | Greedy sort end | shoot at `curr.end`; skip all covered |
| Meeting Scheduler | Two-pointer | sort both, intersect, check duration |
| Employee Free Time | Merge + gap scan | flatten, merge, find gaps |
| Remove Covered | Sort + maxEnd | sort start↑ end↓; track maxEnd |
| Data Stream Intervals | TreeMap merge | floorKey/ceilingKey to find neighbours |
