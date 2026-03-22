# Graph For Beginners — Solved Problems (30 Problems)

> **Based on:** "Graph For Beginners [Problems | Pattern | Sample Solutions]" — Jayant Shekhar
> **Notes file:** [01_graph_notes.md](./01_graph_notes.md)
> **Language:** Java

---

## Table of Contents

### Pattern 1 — Union Find
- [P1 — Friend Circles (Number of Provinces)](#problem-1--friend-circles-number-of-provinces)
- [P2 — Redundant Connection](#problem-2--redundant-connection)
- [P3 — Most Stones Removed with Same Row or Column](#problem-3--most-stones-removed-with-same-row-or-column)
- [P4 — Number of Operations to Make Network Connected](#problem-4--number-of-operations-to-make-network-connected)
- [P5 — Satisfiability of Equality Equations](#problem-5--satisfiability-of-equality-equations)
- [P6 — Accounts Merge](#problem-6--accounts-merge)
- [P7 — Connecting Cities with Minimum Cost](#problem-7--connecting-cities-with-minimum-cost)

### Pattern 2 — DFS from Boundary
- [P8 — Surrounded Regions](#problem-8--surrounded-regions)
- [P9 — Number of Enclaves](#problem-9--number-of-enclaves)

### Pattern 3 — DFS: Time Propagation
- [P10 — Time Needed to Inform All Employees](#problem-10--time-needed-to-inform-all-employees)

### Pattern 4 — DFS: Island Variants
- [P11 — Number of Islands](#problem-11--number-of-islands)
- [P12 — Max Area of Island](#problem-12--max-area-of-island)
- [P13 — Number of Closed Islands](#problem-13--number-of-closed-islands)
- [P14 — Flood Fill](#problem-14--flood-fill)
- [P15 — Keys and Rooms](#problem-15--keys-and-rooms)
- [P16 — Employee Importance](#problem-16--employee-importance)
- [P17 — Find the Town Judge](#problem-17--find-the-town-judge)

### Pattern 5 — DFS: Cycle Detection
- [P18 — Find Eventual Safe States](#problem-18--find-eventual-safe-states)

### Pattern 6 — BFS: Shortest Path (Multi-source)
- [P19 — 01 Matrix](#problem-19--01-matrix)
- [P20 — Rotting Oranges](#problem-20--rotting-oranges)
- [P21 — As Far from Land as Possible](#problem-21--as-far-from-land-as-possible)
- [P22 — Shortest Path in Binary Matrix](#problem-22--shortest-path-in-binary-matrix)

### Pattern 7 — BFS: Graph Coloring / Bipartite
- [P23 — Is Graph Bipartite?](#problem-23--is-graph-bipartite)
- [P24 — Possible Bipartition](#problem-24--possible-bipartition)

### Pattern 8 — Topological Sort
- [P25 — Course Schedule](#problem-25--course-schedule)
- [P26 — Course Schedule II](#problem-26--course-schedule-ii)

### Pattern 9 — Shortest Path Algorithms
- [P27 — Network Delay Time (Dijkstra)](#problem-27--network-delay-time)
- [P28 — Network Delay Time (Bellman-Ford)](#problem-28--network-delay-time-bellman-ford)
- [P29 — Find the City with Smallest Neighbours (Floyd-Warshall)](#problem-29--find-the-city-with-smallest-number-of-neighbours)
- [P30 — Cheapest Flights Within K Stops](#problem-30--cheapest-flights-within-k-stops)

---

## Pattern 1 — Union Find

> **Identify:** Problem talks about finding groups, components, merging, connectivity.
> **Template:** `find(x)` returns root. `union(x,y)` merges components.

---

### Problem 1 — Friend Circles (Number of Provinces)
**LeetCode #547 | Difficulty: Medium | Company: Amazon, Facebook**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | For each `i`, union with all `j` where `isConnected[i][j] == 1` | build components |
| 2 | Count distinct roots | = number of provinces |

#### Java code

```java
public int findCircleNum(int[][] isConnected) {
    int n = isConnected.length;
    int[] parent = new int[n];
    for (int i = 0; i < n; i++) parent[i] = i;

    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            if (isConnected[i][j] == 1) union(parent, i, j);

    int count = 0;
    for (int i = 0; i < n; i++)
        if (find(parent, i) == i) count++;   // root node = new province
    return count;
}
int find(int[] parent, int x) {
    if (parent[x] != x) parent[x] = find(parent, parent[x]);
    return parent[x];
}
void union(int[] parent, int x, int y) {
    parent[find(parent, x)] = find(parent, y);
}
```

#### Example

```
isConnected = [[1,1,0],[1,1,0],[0,0,1]]

union(0,1) → same group
Node 2 → separate group
Roots: find(0)=1, find(1)=1, find(2)=2
Count = 2 provinces ✓
```

---

### Problem 2 — Redundant Connection
**LeetCode #684 | Difficulty: Medium | Company: Amazon**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Process each edge `(u, v)` | try to union |
| 2 | If `find(u) == find(v)` | already connected → this edge is redundant |
| 3 | Else `union(u, v)` | add to graph |

#### Java code

```java
public int[] findRedundantConnection(int[][] edges) {
    int n = edges.length;
    int[] parent = new int[n + 1];
    for (int i = 0; i <= n; i++) parent[i] = i;

    for (int[] edge : edges) {
        int u = find(parent, edge[0]);
        int v = find(parent, edge[1]);
        if (u == v) return edge;       // already in same component → redundant
        parent[v] = u;
    }
    return new int[]{};
}
int find(int[] parent, int x) {
    if (parent[x] != x) parent[x] = find(parent, parent[x]);
    return parent[x];
}
```

#### Example

```
edges = [[1,2],[1,3],[2,3]]

Process [1,2]: find(1)=1, find(2)=2 → different → union → parent[2]=1
Process [1,3]: find(1)=1, find(3)=3 → union → parent[3]=1
Process [2,3]: find(2)=1, find(3)=1 → SAME → return [2,3] ✓
```

---

### Problem 3 — Most Stones Removed with Same Row or Column
**LeetCode #947 | Difficulty: Medium | Company: Google**

> Max stones removed = total stones - number of connected components.
> Two stones are connected if they share a row or column.

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Union stones that share same row or column | any order |
| 2 | Count distinct components | = stones that cannot be removed |
| 3 | Answer = total - components | |

#### Java code

```java
public int removeStones(int[][] stones) {
    int n = stones.length;
    int[] parent = new int[n];
    for (int i = 0; i < n; i++) parent[i] = i;

    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            if (stones[i][0] == stones[j][0] || stones[i][1] == stones[j][1])
                union(parent, i, j);   // same row or col → connect

    int components = 0;
    for (int i = 0; i < n; i++)
        if (find(parent, i) == i) components++;

    return n - components;
}
int find(int[] parent, int x) {
    if (parent[x] != x) parent[x] = find(parent, parent[x]);
    return parent[x];
}
void union(int[] parent, int x, int y) {
    parent[find(parent, x)] = find(parent, y);
}
```

#### Example

```
stones = [[0,0],[0,1],[1,0],[1,2],[2,1],[2,2]]  n=6

Unions: (0,1)same row0, (0,2)same col0, (1,3)same row1, (2,4)same col1, (3,5)same col2, (4,5)same row2
All 6 stones in 1 component → components=1
Answer = 6-1 = 5 ✓
```

---

### Problem 4 — Number of Operations to Make Network Connected
**LeetCode #1319 | Difficulty: Medium | Company: Amazon**

> Min cables needed = components - 1. Only possible if extra cables ≥ components - 1.

#### Java code

```java
public int makeConnected(int n, int[][] connections) {
    if (connections.length < n - 1) return -1;   // not enough cables

    int[] parent = new int[n];
    for (int i = 0; i < n; i++) parent[i] = i;

    int components = n;
    for (int[] c : connections) {
        int u = find(parent, c[0]), v = find(parent, c[1]);
        if (u != v) { parent[v] = u; components--; }   // merged → one less component
    }
    return components - 1;   // need this many cables to connect remaining components
}
int find(int[] parent, int x) {
    if (parent[x] != x) parent[x] = find(parent, parent[x]);
    return parent[x];
}
```

#### Example

```
n=4, connections=[[0,1],[0,2],[1,2]]

Start: 4 components
Union(0,1): 3 components
Union(0,2): 2 components
Union(1,2): find(1)=0, find(2)=0 → same → skip (this is extra cable!)
connections.length=3 >= n-1=3 ✓
Return 2-1 = 1 ✓ (need 1 cable to connect node 3)
```

---

### Problem 5 — Satisfiability of Equality Equations
**LeetCode #990 | Difficulty: Medium | Company: Google**

> Step 1: Union all `a==b` pairs. Step 2: Check all `a!=b` — if same root → impossible.

#### Java code

```java
public boolean equationsPossible(String[] equations) {
    int[] parent = new int[26];
    for (int i = 0; i < 26; i++) parent[i] = i;

    // First pass: union all == pairs
    for (String eq : equations)
        if (eq.charAt(1) == '=')
            union(parent, eq.charAt(0) - 'a', eq.charAt(3) - 'a');

    // Second pass: check != pairs
    for (String eq : equations)
        if (eq.charAt(1) == '!')
            if (find(parent, eq.charAt(0) - 'a') == find(parent, eq.charAt(3) - 'a'))
                return false;   // equal variables declared not equal → contradiction

    return true;
}
int find(int[] parent, int x) {
    if (parent[x] != x) parent[x] = find(parent, parent[x]);
    return parent[x];
}
void union(int[] parent, int x, int y) {
    parent[find(parent, x)] = find(parent, y);
}
```

#### Example

```
equations = ["a==b","b!=a"]
Pass1: union(a,b)
Pass2: a!=a? find(a)==find(a) → return false ✓

equations = ["a==b","b==c","a!=c"]
Pass1: union(a,b), union(b,c) → a,b,c all same root
Pass2: a!=c? find(a)==find(c) → return false ✓
```

---

### Problem 6 — Accounts Merge
**LeetCode #721 | Difficulty: Medium | Company: Amazon, Google**

> Union all emails within the same account. Group by root → each group is a merged account.

#### Java code

```java
public List<List<String>> accountsMerge(List<List<String>> accounts) {
    Map<String, String> parent = new HashMap<>();
    Map<String, String> emailToName = new HashMap<>();

    // Initialize parent for each email
    for (List<String> acc : accounts) {
        String name = acc.get(0);
        for (int i = 1; i < acc.size(); i++) {
            parent.put(acc.get(i), acc.get(i));
            emailToName.put(acc.get(i), name);
        }
    }

    // Union emails in same account
    for (List<String> acc : accounts)
        for (int i = 2; i < acc.size(); i++)
            union(parent, acc.get(1), acc.get(i));

    // Group emails by root
    Map<String, TreeSet<String>> groups = new HashMap<>();
    for (String email : parent.keySet())
        groups.computeIfAbsent(find(parent, email), k -> new TreeSet<>()).add(email);

    // Build result
    List<List<String>> result = new ArrayList<>();
    for (Map.Entry<String, TreeSet<String>> e : groups.entrySet()) {
        List<String> list = new ArrayList<>();
        list.add(emailToName.get(e.getKey()));   // name
        list.addAll(e.getValue());               // sorted emails
        result.add(list);
    }
    return result;
}
String find(Map<String, String> parent, String x) {
    if (!parent.get(x).equals(x)) parent.put(x, find(parent, parent.get(x)));
    return parent.get(x);
}
void union(Map<String, String> parent, String x, String y) {
    String px = find(parent, x), py = find(parent, y);
    if (!px.equals(py)) parent.put(px, py);
}
```

#### Example

```
accounts = [["John","a@a","b@b"],["John","c@c"],["John","b@b","c@c"]]

Union(a,b), Union(b,c) → all three emails in one component
Result: [["John","a@a","b@b","c@c"]] ✓
```

---

### Problem 7 — Connecting Cities with Minimum Cost
**LeetCode #1135 | Difficulty: Medium (Kruskal's MST)**

#### Java code

```java
public int minimumCost(int N, int[][] connections) {
    int[] parent = new int[N + 1];
    for (int i = 0; i <= N; i++) parent[i] = i;

    Arrays.sort(connections, (a, b) -> a[2] - b[2]);   // sort by cost

    int total = 0, edges = 0;
    for (int[] c : connections) {
        int u = find(parent, c[0]), v = find(parent, c[1]);
        if (u != v) {
            parent[v] = u;
            total += c[2];
            if (++edges == N - 1) return total;   // MST complete
        }
    }
    return -1;   // not all connected
}
int find(int[] parent, int x) {
    if (parent[x] != x) parent[x] = find(parent, parent[x]);
    return parent[x];
}
```

#### Example

```
N=3, connections=[[1,2,5],[1,3,6],[2,3,1]]
Sorted: [[2,3,1],[1,2,5],[1,3,6]]
Add [2,3,1]: cost=1, edges=1
Add [1,2,5]: cost=6, edges=2 = N-1 → return 6 ✓
```

---

## Pattern 2 — DFS from Boundary

> **Identify:** Cells connected to border are "safe". Mark border-connected cells first, then process remaining.

---

### Problem 8 — Surrounded Regions
**LeetCode #130 | Difficulty: Medium | Company: Google**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | DFS from all border `'O'` cells, mark as `'S'` (safe) | these cannot be flipped |
| 2 | Traverse entire board | `'O'` → `'X'`, `'S'` → `'O'` |

#### Java code

```java
public void solve(char[][] board) {
    int rows = board.length, cols = board[0].length;

    // Mark all border-connected 'O's as safe
    for (int r = 0; r < rows; r++) {
        if (board[r][0] == 'O') dfs(board, r, 0);
        if (board[r][cols-1] == 'O') dfs(board, r, cols-1);
    }
    for (int c = 0; c < cols; c++) {
        if (board[0][c] == 'O') dfs(board, 0, c);
        if (board[rows-1][c] == 'O') dfs(board, rows-1, c);
    }

    // Flip remaining 'O' → 'X', restore 'S' → 'O'
    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++) {
            if (board[r][c] == 'O') board[r][c] = 'X';
            else if (board[r][c] == 'S') board[r][c] = 'O';
        }
}
void dfs(char[][] board, int r, int c) {
    if (r<0||r>=board.length||c<0||c>=board[0].length||board[r][c]!='O') return;
    board[r][c] = 'S';
    dfs(board,r+1,c); dfs(board,r-1,c); dfs(board,r,c+1); dfs(board,r,c-1);
}
```

#### Example

```
Input:               After DFS border:     Final:
X X X X              X X X X               X X X X
X O O X    →         X O O X      →        X X X X
X X O X              X X O X               X X X X
X O X X              X S X X               X O X X

Border 'O' at (3,1) → marked 'S', stays 'O'
Inner 'O's → flipped to 'X' ✓
```

---

### Problem 9 — Number of Enclaves
**LeetCode #1020 | Difficulty: Medium**

#### Java code

```java
public int numEnclaves(int[][] grid) {
    int rows = grid.length, cols = grid[0].length;

    // DFS from all boundary 1s → mark as visited (-1)
    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++)
            if (r==0||c==0||r==rows-1||c==cols-1)
                dfs(grid, r, c);

    // Count remaining 1s (not connected to boundary)
    int count = 0;
    for (int[] row : grid)
        for (int cell : row)
            if (cell == 1) count++;
    return count;
}
void dfs(int[][] grid, int r, int c) {
    if (r<0||r>=grid.length||c<0||c>=grid[0].length||grid[r][c]!=1) return;
    grid[r][c] = -1;   // mark visited
    dfs(grid,r+1,c); dfs(grid,r-1,c); dfs(grid,r,c+1); dfs(grid,r,c-1);
}
```

#### Example

```
grid = [[0,0,0,0],
        [1,0,1,0],
        [0,1,1,0],
        [0,0,0,0]]

DFS from boundary → no boundary 1s to mark
Count remaining 1s: (1,2),(2,1),(2,2) = 3 ✓
```

---

## Pattern 3 — DFS: Time Propagation

---

### Problem 10 — Time Needed to Inform All Employees
**LeetCode #1376 | Difficulty: Medium | Company: Amazon, Google**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Build tree: manager → list of subordinates | adj list |
| 2 | DFS from headID | track cumulative time |
| 3 | At each node: `time = informTime[node] + max(children)` | |

#### Java code

```java
public int numOfMinutes(int n, int headID, int[] manager, int[] informTime) {
    Map<Integer, List<Integer>> adj = new HashMap<>();
    for (int i = 0; i < n; i++)
        if (manager[i] != -1)
            adj.computeIfAbsent(manager[i], k -> new ArrayList<>()).add(i);

    return dfs(adj, informTime, headID);
}
int dfs(Map<Integer, List<Integer>> adj, int[] informTime, int node) {
    int maxTime = 0;
    for (int sub : adj.getOrDefault(node, new ArrayList<>()))
        maxTime = Math.max(maxTime, dfs(adj, informTime, sub));
    return informTime[node] + maxTime;   // time to inform me + max time among all subordinates
}
```

#### Example

```
n=6, headID=2, manager=[-1,2,0,0,2,2], informTime=[0,0,6,0,0,0]... 
Actually: manager=[-1,2,0,0,2,2] → head is 0 (manager[2]=0, headID=2 → corrected)
Tree: 0→{2,3}, 2→{1,4,5}

dfs(node=1)=0, dfs(4)=0, dfs(5)=0
dfs(2)= informTime[2] + max(0,0,0) = 6
dfs(3)= informTime[3] = 0
dfs(0)= informTime[0] + max(6,0) = 6
Output: 6 ✓
```

---

## Pattern 4 — DFS: Island Variants

> **Identify:** Grid problem, count/measure connected land cells.
> **Template:** DFS from each unvisited '1', mark visited by changing value.

---

### Problem 11 — Number of Islands
**LeetCode #200 | Difficulty: Medium | Company: Amazon, Google**

#### Java code

```java
public int numIslands(char[][] grid) {
    int rows = grid.length, cols = grid[0].length, count = 0;
    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++)
            if (grid[r][c] == '1') { dfs(grid, r, c); count++; }
    return count;
}
void dfs(char[][] grid, int r, int c) {
    if (r<0||r>=grid.length||c<0||c>=grid[0].length||grid[r][c]!='1') return;
    grid[r][c] = '0';   // mark visited
    dfs(grid,r+1,c); dfs(grid,r-1,c); dfs(grid,r,c+1); dfs(grid,r,c-1);
}
```

#### Example

```
grid = [["1","1","0","0"],
        ["1","1","0","0"],
        ["0","0","1","0"],
        ["0","0","0","1"]]

DFS from (0,0) → marks (0,0),(0,1),(1,0),(1,1) → island 1
DFS from (2,2) → marks (2,2) → island 2
DFS from (3,3) → marks (3,3) → island 3
Output: 3 ✓
```

---

### Problem 12 — Max Area of Island
**LeetCode #695 | Difficulty: Medium | Company: Amazon**

#### Java code

```java
public int maxAreaOfIsland(int[][] grid) {
    int max = 0;
    for (int r = 0; r < grid.length; r++)
        for (int c = 0; c < grid[0].length; c++)
            if (grid[r][c] == 1) max = Math.max(max, dfs(grid, r, c));
    return max;
}
int dfs(int[][] grid, int r, int c) {
    if (r<0||r>=grid.length||c<0||c>=grid[0].length||grid[r][c]!=1) return 0;
    grid[r][c] = 0;   // mark visited
    return 1 + dfs(grid,r+1,c) + dfs(grid,r-1,c) + dfs(grid,r,c+1) + dfs(grid,r,c-1);
}
```

#### Example

```
grid = [[0,0,1,0],[0,1,1,0],[0,1,0,0],[1,1,0,0]]

DFS from (0,2): 1 + dfs(1,2)=1+dfs(2,2)=0 + dfs(1,1)=1+dfs(2,1)=1 → total=4
DFS from (3,0): 1+dfs(3,1)=1 → total=2
Output: 4 ✓
```

---

### Problem 13 — Number of Closed Islands
**LeetCode #1254 | Difficulty: Medium**

> Island not touching boundary = closed island.
> Strategy: first mark all boundary-connected 0s (not closed), then count remaining islands.

#### Java code

```java
public int closedIsland(int[][] grid) {
    int rows = grid.length, cols = grid[0].length;

    // Mark boundary-connected 0s as visited
    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++)
            if ((r==0||c==0||r==rows-1||c==cols-1) && grid[r][c]==0)
                dfs(grid, r, c);

    // Count remaining closed islands
    int count = 0;
    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++)
            if (grid[r][c] == 0) { dfs(grid, r, c); count++; }
    return count;
}
void dfs(int[][] grid, int r, int c) {
    if (r<0||r>=grid.length||c<0||c>=grid[0].length||grid[r][c]!=0) return;
    grid[r][c] = 1;   // mark visited (or -1)
    dfs(grid,r+1,c); dfs(grid,r-1,c); dfs(grid,r,c+1); dfs(grid,r,c-1);
}
```

---

### Problem 14 — Flood Fill
**LeetCode #733 | Difficulty: Easy | Company: Amazon, Google**

#### Java code

```java
public int[][] floodFill(int[][] image, int sr, int sc, int color) {
    int original = image[sr][sc];
    if (original != color) dfs(image, sr, sc, original, color);
    return image;
}
void dfs(int[][] image, int r, int c, int original, int color) {
    if (r<0||r>=image.length||c<0||c>=image[0].length) return;
    if (image[r][c] != original) return;
    image[r][c] = color;
    dfs(image,r+1,c,original,color); dfs(image,r-1,c,original,color);
    dfs(image,r,c+1,original,color); dfs(image,r,c-1,original,color);
}
```

#### Example

```
image=[[1,1,1],[1,1,0],[1,0,1]], sr=1, sc=1, color=2
original=1, flood fill all connected 1s with 2
Output: [[2,2,2],[2,2,0],[2,0,1]] ✓
```

---

### Problem 15 — Keys and Rooms
**LeetCode #841 | Difficulty: Medium**

> Can we visit all rooms starting from room 0?

#### Java code

```java
public boolean canVisitAllRooms(List<List<Integer>> rooms) {
    boolean[] visited = new boolean[rooms.size()];
    dfs(rooms, visited, 0);
    for (boolean v : visited) if (!v) return false;
    return true;
}
void dfs(List<List<Integer>> rooms, boolean[] visited, int room) {
    visited[room] = true;
    for (int key : rooms.get(room))
        if (!visited[key]) dfs(rooms, visited, key);
}
```

#### Example

```
rooms = [[1],[2],[3],[]]
DFS(0) → visits 1 → visits 2 → visits 3
All visited → return true ✓

rooms = [[1,3],[3,0,1],[2],[0]]
DFS(0) → 1,3,0 → visits {0,1,3}. Room 2 never visited → false ✓
```

---

### Problem 16 — Employee Importance
**LeetCode #690 | Difficulty: Medium**

#### Java code

```java
public int getImportance(List<Employee> employees, int id) {
    Map<Integer, Employee> map = new HashMap<>();
    for (Employee e : employees) map.put(e.id, e);
    return dfs(map, id);
}
int dfs(Map<Integer, Employee> map, int id) {
    Employee e = map.get(id);
    int total = e.importance;
    for (int sub : e.subordinates) total += dfs(map, sub);
    return total;
}
```

---

### Problem 17 — Find the Town Judge
**LeetCode #997 | Difficulty: Easy**

> Judge: trusted by everyone else (in-degree = n-1), trusts nobody (out-degree = 0).

#### Java code

```java
public int findJudge(int n, int[][] trust) {
    int[] inDegree = new int[n + 1];
    int[] outDegree = new int[n + 1];
    for (int[] t : trust) { outDegree[t[0]]++; inDegree[t[1]]++; }
    for (int i = 1; i <= n; i++)
        if (inDegree[i] == n - 1 && outDegree[i] == 0) return i;
    return -1;
}
```

#### Example

```
n=3, trust=[[1,3],[2,3]]
inDegree:  [0,0,0,2]
outDegree: [0,1,1,0]
Node 3: inDegree=2=n-1, outDegree=0 → return 3 ✓
```

---

## Pattern 5 — DFS: Cycle Detection

---

### Problem 18 — Find Eventual Safe States
**LeetCode #802 | Difficulty: Medium | Company: Google**

> Node is safe if ALL paths from it lead to terminal nodes (no cycle reachable).
> Use 3-color DFS: 0=unvisited, -1=in current path (unsafe), 1=safe.

#### Java code

```java
public List<Integer> eventualSafeNodes(int[][] graph) {
    int n = graph.length;
    int[] color = new int[n];   // 0=unvisited, -1=in-path, 1=safe
    List<Integer> result = new ArrayList<>();
    for (int i = 0; i < n; i++)
        if (dfs(graph, color, i)) result.add(i);
    return result;
}
boolean dfs(int[][] graph, int[] color, int node) {
    if (color[node] != 0) return color[node] == 1;   // already determined
    color[node] = -1;                                 // mark: in current path
    for (int next : graph[node])
        if (!dfs(graph, color, next)) return false;   // cycle found
    color[node] = 1;                                  // all paths safe
    return true;
}
```

#### Example

```
graph = [[1,2],[2,3],[5],[0],[5],[],[]]
Node 5,6: no outgoing edges → safe (color=1)
Node 2→5: safe ✓
Node 1→2,3→0→1 (cycle!) → unsafe
Node 4→5: safe ✓
Output: [2,4,5,6] ✓
```

---

## Pattern 6 — BFS: Shortest Path (Multi-source)

> **Identify:** Minimum steps/distance to/from multiple sources.
> **Key:** Seed ALL sources into queue FIRST. Then BFS — level = distance from nearest source.

---

### Problem 19 — 01 Matrix
**LeetCode #542 | Difficulty: Medium | Company: Amazon, Google**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Seed all 0-cells into queue | all 0s are sources |
| 2 | BFS level by level | level = distance from nearest 0 |
| 3 | For each 1-cell reached | update distance |

#### Java code

```java
public int[][] updateMatrix(int[][] mat) {
    int rows = mat.length, cols = mat[0].length;
    int[][] dist = new int[rows][cols];
    boolean[][] visited = new boolean[rows][cols];
    Queue<int[]> q = new LinkedList<>();

    // Seed all 0s
    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++)
            if (mat[r][c] == 0) { q.offer(new int[]{r,c}); visited[r][c]=true; }

    int[] dr = {0,0,1,-1}, dc = {1,-1,0,0};
    while (!q.isEmpty()) {
        int[] cur = q.poll();
        for (int d = 0; d < 4; d++) {
            int nr=cur[0]+dr[d], nc=cur[1]+dc[d];
            if (nr>=0&&nr<rows&&nc>=0&&nc<cols&&!visited[nr][nc]) {
                dist[nr][nc] = dist[cur[0]][cur[1]] + 1;
                visited[nr][nc] = true;
                q.offer(new int[]{nr, nc});
            }
        }
    }
    return dist;
}
```

#### Example

```
mat = [[0,0,0],[0,1,0],[1,1,1]]

0-sources: (0,0),(0,1),(0,2),(1,0),(1,2)
BFS level 1: (1,1)=1, (2,0)=1, (2,2)=1
BFS level 2: (2,1)=2
Output: [[0,0,0],[0,1,0],[1,2,1]] ✓
```

---

### Problem 20 — Rotting Oranges
**LeetCode #994 | Difficulty: Medium | Company: Amazon, Google**

#### Java code

```java
public int orangesRotting(int[][] grid) {
    int rows = grid.length, cols = grid[0].length;
    Queue<int[]> q = new LinkedList<>();
    int fresh = 0;

    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++) {
            if (grid[r][c] == 2) q.offer(new int[]{r, c});   // seed rotten
            if (grid[r][c] == 1) fresh++;
        }

    if (fresh == 0) return 0;
    int[] dr = {0,0,1,-1}, dc = {1,-1,0,0};
    int minutes = 0;

    while (!q.isEmpty() && fresh > 0) {
        minutes++;
        int size = q.size();
        for (int i = 0; i < size; i++) {
            int[] cur = q.poll();
            for (int d = 0; d < 4; d++) {
                int nr=cur[0]+dr[d], nc=cur[1]+dc[d];
                if (nr>=0&&nr<rows&&nc>=0&&nc<cols&&grid[nr][nc]==1) {
                    grid[nr][nc] = 2;
                    fresh--;
                    q.offer(new int[]{nr, nc});
                }
            }
        }
    }
    return fresh == 0 ? minutes : -1;
}
```

#### Example

```
grid=[[2,1,1],[1,1,0],[0,1,1]]
fresh=6, rotten sources: (0,0)

min1: (0,1),(1,0) rot → fresh=4
min2: (0,2),(1,1) rot → fresh=2
min3: (2,1) rots  → fresh=1
min4: (2,2) rots  → fresh=0
Output: 4 ✓
```

---

### Problem 21 — As Far from Land as Possible
**LeetCode #1162 | Difficulty: Medium | Company: Google**

> Find max distance from water cell to nearest land. Multi-source BFS from all land cells.

#### Java code

```java
public int maxDistance(int[][] grid) {
    int n = grid.length;
    Queue<int[]> q = new LinkedList<>();
    for (int r=0;r<n;r++)
        for (int c=0;c<n;c++)
            if (grid[r][c]==1) q.offer(new int[]{r,c});   // seed all land

    if (q.size()==0||q.size()==n*n) return -1;   // all water or all land

    int[] dr={0,0,1,-1}, dc={1,-1,0,0};
    int dist = -1;
    while (!q.isEmpty()) {
        dist++;
        int size = q.size();
        for (int i=0;i<size;i++) {
            int[] cur=q.poll();
            for (int d=0;d<4;d++) {
                int nr=cur[0]+dr[d], nc=cur[1]+dc[d];
                if (nr>=0&&nr<n&&nc>=0&&nc<n&&grid[nr][nc]==0) {
                    grid[nr][nc]=1;   // mark visited
                    q.offer(new int[]{nr,nc});
                }
            }
        }
    }
    return dist;
}
```

---

### Problem 22 — Shortest Path in Binary Matrix
**LeetCode #1091 | Difficulty: Medium | Company: Facebook, Amazon**

> 8-directional BFS. Start from (0,0), reach (n-1,n-1). Cells must be 0.

#### Java code

```java
public int shortestPathBinaryMatrix(int[][] grid) {
    int n = grid.length;
    if (grid[0][0]==1||grid[n-1][n-1]==1) return -1;
    int[] dr={-1,-1,-1,0,0,1,1,1}, dc={-1,0,1,-1,1,-1,0,1};
    Queue<int[]> q = new LinkedList<>();
    q.offer(new int[]{0,0,1});
    grid[0][0]=1;
    while (!q.isEmpty()) {
        int[] cur=q.poll();
        if (cur[0]==n-1&&cur[1]==n-1) return cur[2];
        for (int d=0;d<8;d++) {
            int nr=cur[0]+dr[d], nc=cur[1]+dc[d];
            if (nr>=0&&nr<n&&nc>=0&&nc<n&&grid[nr][nc]==0) {
                grid[nr][nc]=1;
                q.offer(new int[]{nr,nc,cur[2]+1});
            }
        }
    }
    return -1;
}
```

---

## Pattern 7 — BFS: Graph Coloring / Bipartite

> **Identify:** "Divide into 2 groups with no conflict", "is graph bipartite?"
> **Algorithm:** BFS 2-coloring — alternate 0/1. Conflict = same color adjacent.

---

### Problem 23 — Is Graph Bipartite?
**LeetCode #785 | Difficulty: Medium | Company: Amazon**

#### Java code

```java
public boolean isBipartite(int[][] graph) {
    int n = graph.length;
    int[] color = new int[n];
    Arrays.fill(color, -1);

    for (int start = 0; start < n; start++) {
        if (color[start] != -1) continue;
        color[start] = 0;
        Queue<Integer> q = new LinkedList<>();
        q.offer(start);
        while (!q.isEmpty()) {
            int u = q.poll();
            for (int v : graph[u]) {
                if (color[v] == -1) { color[v] = 1-color[u]; q.offer(v); }
                else if (color[v] == color[u]) return false;   // conflict
            }
        }
    }
    return true;
}
```

#### Example

```
graph = [[1,3],[0,2],[1,3],[0,2]]
color[0]=0, color[1]=1, color[2]=0, color[3]=1
No conflicts → true ✓

graph = [[1,2,3],[0,2],[0,1,3],[0,2]]
color[0]=0, color[1]=1, color[2]=1 → edge(1,2): both color 1 → false ✓
```

---

### Problem 24 — Possible Bipartition
**LeetCode #886 | Difficulty: Medium | Company: Google**

> Build graph from dislikes list, then same bipartite check.

#### Java code

```java
public boolean possibleBipartition(int n, int[][] dislikes) {
    List<List<Integer>> adj = new ArrayList<>();
    for (int i = 0; i <= n; i++) adj.add(new ArrayList<>());
    for (int[] d : dislikes) { adj.get(d[0]).add(d[1]); adj.get(d[1]).add(d[0]); }

    int[] color = new int[n + 1];
    Arrays.fill(color, -1);
    for (int start = 1; start <= n; start++) {
        if (color[start] != -1) continue;
        color[start] = 0;
        Queue<Integer> q = new LinkedList<>();
        q.offer(start);
        while (!q.isEmpty()) {
            int u = q.poll();
            for (int v : adj.get(u)) {
                if (color[v] == -1) { color[v] = 1-color[u]; q.offer(v); }
                else if (color[v] == color[u]) return false;
            }
        }
    }
    return true;
}
```

---

## Pattern 8 — Topological Sort

> **Identify:** Task dependencies, "can all tasks be done?", ordering in a DAG.
> **Algorithm:** Kahn's BFS — indegree-0 nodes first. If processed < total → cycle.

---

### Problem 25 — Course Schedule
**LeetCode #207 | Difficulty: Medium | Company: Amazon, Google**

#### Java code

```java
public boolean canFinish(int numCourses, int[][] prerequisites) {
    List<List<Integer>> adj = new ArrayList<>();
    int[] indegree = new int[numCourses];
    for (int i=0;i<numCourses;i++) adj.add(new ArrayList<>());
    for (int[] p:prerequisites) { adj.get(p[1]).add(p[0]); indegree[p[0]]++; }

    Queue<Integer> q = new LinkedList<>();
    for (int i=0;i<numCourses;i++) if (indegree[i]==0) q.offer(i);

    int processed = 0;
    while (!q.isEmpty()) {
        int u=q.poll(); processed++;
        for (int v:adj.get(u)) if (--indegree[v]==0) q.offer(v);
    }
    return processed == numCourses;   // all processed = no cycle = can finish
}
```

#### Example

```
numCourses=2, prerequisites=[[1,0]]
adj: 0→[1], indegree=[0,1]
Queue starts: [0]
Process 0: processed=1, indegree[1]→0 → add 1
Process 1: processed=2
processed==2 → return true ✓

prerequisites=[[1,0],[0,1]] → cycle → processed=0 < 2 → false ✓
```

---

### Problem 26 — Course Schedule II
**LeetCode #210 | Difficulty: Medium | Company: Amazon**

#### Java code

```java
public int[] findOrder(int numCourses, int[][] prerequisites) {
    List<List<Integer>> adj = new ArrayList<>();
    int[] indegree = new int[numCourses];
    for (int i=0;i<numCourses;i++) adj.add(new ArrayList<>());
    for (int[] p:prerequisites) { adj.get(p[1]).add(p[0]); indegree[p[0]]++; }

    Queue<Integer> q = new LinkedList<>();
    for (int i=0;i<numCourses;i++) if (indegree[i]==0) q.offer(i);

    int[] order = new int[numCourses]; int idx=0;
    while (!q.isEmpty()) {
        int u=q.poll(); order[idx++]=u;
        for (int v:adj.get(u)) if (--indegree[v]==0) q.offer(v);
    }
    return idx==numCourses ? order : new int[0];
}
```

#### Example

```
numCourses=4, prerequisites=[[1,0],[2,0],[3,1],[3,2]]
adj: 0→[1,2], 1→[3], 2→[3]
indegree: [0,1,1,2]
Queue: [0] → process 0: add 1,2 → process 1: add 3(if indegree=1) → process 2: add 3(indegree=0)
Output: [0,1,2,3] or [0,2,1,3] ✓
```

---

## Pattern 9 — Shortest Path Algorithms

---

### Problem 27 — Network Delay Time (Dijkstra)
**LeetCode #743 | Difficulty: Medium | Company: Amazon, Google**

#### Approach table

| Step | Action | Note |
|------|--------|------|
| 1 | Build adjacency list | `adj[u] = {v, weight}` |
| 2 | Dijkstra from source `k` | min-heap `{dist, node}` |
| 3 | Return max of all shortest paths | if any node unreachable → -1 |

#### Java code

```java
public int networkDelayTime(int[][] times, int n, int k) {
    List<int[]>[] adj = new ArrayList[n+1];
    for (int i=1;i<=n;i++) adj[i]=new ArrayList<>();
    for (int[] t:times) adj[t[0]].add(new int[]{t[1],t[2]});

    int[] dist = new int[n+1];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[k]=0;
    PriorityQueue<int[]> pq=new PriorityQueue<>((a,b)->a[0]-b[0]);
    pq.offer(new int[]{0,k});

    while (!pq.isEmpty()) {
        int[] cur=pq.poll();
        int d=cur[0], u=cur[1];
        if (d>dist[u]) continue;   // stale
        for (int[] edge:adj[u])
            if (dist[u]+edge[1]<dist[edge[0]]) {
                dist[edge[0]]=dist[u]+edge[1];
                pq.offer(new int[]{dist[edge[0]],edge[0]});
            }
    }
    int max=0;
    for (int i=1;i<=n;i++) { if (dist[i]==Integer.MAX_VALUE) return -1; max=Math.max(max,dist[i]); }
    return max;
}
```

#### Example

```
times=[[2,1,1],[2,3,1],[3,4,1]], n=4, k=2
Dijkstra from 2: dist[1]=1, dist[3]=1, dist[4]=2
max=2 → return 2 ✓
```

---

### Problem 28 — Network Delay Time (Bellman-Ford)
**LeetCode #743 | Difficulty: Medium**

#### Java code

```java
public int networkDelayTime(int[][] times, int n, int k) {
    int[] dist = new int[n+1];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[k]=0;

    for (int i=1;i<n;i++)         // relax n-1 times
        for (int[] e:times)
            if (dist[e[0]]!=Integer.MAX_VALUE && dist[e[0]]+e[2]<dist[e[1]])
                dist[e[1]]=dist[e[0]]+e[2];

    int max=0;
    for (int i=1;i<=n;i++) { if (dist[i]==Integer.MAX_VALUE) return -1; max=Math.max(max,dist[i]); }
    return max;
}
```

---

### Problem 29 — Find the City with Smallest Number of Neighbours
**LeetCode #1334 | Difficulty: Medium | Company: Google | Algorithm: Floyd-Warshall**

> Find the city with the fewest cities reachable within `distanceThreshold`. Use all-pairs shortest path.

#### Java code

```java
public int findTheCity(int n, int[][] edges, int distanceThreshold) {
    int INF = Integer.MAX_VALUE/2;
    int[][] dp = new int[n][n];
    for (int[] row:dp) Arrays.fill(row,INF);
    for (int i=0;i<n;i++) dp[i][i]=0;
    for (int[] e:edges) { dp[e[0]][e[1]]=e[2]; dp[e[1]][e[0]]=e[2]; }

    for (int k=0;k<n;k++)
        for (int i=0;i<n;i++)
            for (int j=0;j<n;j++)
                dp[i][j]=Math.min(dp[i][j], dp[i][k]+dp[k][j]);

    int result=-1, minCount=n+1;
    for (int i=0;i<n;i++) {
        int count=0;
        for (int j=0;j<n;j++) if (i!=j&&dp[i][j]<=distanceThreshold) count++;
        if (count<=minCount) { minCount=count; result=i; }  // prefer higher index on tie
    }
    return result;
}
```

#### Example

```
n=4, edges=[[0,1,3],[1,2,1],[1,3,4],[2,3,1]], distanceThreshold=4

Floyd-Warshall all-pairs:
  dp[0][1]=3, dp[0][2]=4, dp[0][3]=5
  dp[1][2]=1, dp[1][3]=2
  dp[2][3]=1

Count within threshold=4:
  City 0: dp[0][1]=3✓, dp[0][2]=4✓, dp[0][3]=5✗ → count=2
  City 1: dp[1][0]=3✓, dp[1][2]=1✓, dp[1][3]=2✓ → count=3
  City 2: dp[2][0]=4✓, dp[2][1]=1✓, dp[2][3]=1✓ → count=3
  City 3: dp[3][0]=5✗, dp[3][1]=2✓, dp[3][2]=1✓ → count=2

Cities 0 and 3 both have count=2, prefer higher index → return 3 ✓
```

---

### Problem 30 — Cheapest Flights Within K Stops
**LeetCode #787 | Difficulty: Medium | Company: Amazon, Google | Algorithm: Bellman-Ford with K limit**

> K stops = K+1 edges. Relax exactly K+1 times. Use temp copy to prevent using same-iteration updates.

#### Java code

```java
public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
    int[] dist = new int[n];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[src]=0;

    for (int i=0; i<=k; i++) {                   // relax k+1 times
        int[] temp = Arrays.copyOf(dist, n);      // copy prevents using same-iter updates
        for (int[] f:flights) {
            int u=f[0], v=f[1], w=f[2];
            if (dist[u]!=Integer.MAX_VALUE && dist[u]+w<temp[v])
                temp[v]=dist[u]+w;
        }
        dist=temp;
    }
    return dist[dst]==Integer.MAX_VALUE ? -1 : dist[dst];
}
```

#### Example

```
n=4, flights=[[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]], src=0, dst=3, k=1

k+1=2 relaxations:
relax0: dist=[0,100,INF,INF] → [0,100,INF,INF]
relax1: temp=[0,100,INF,INF]
  [0,1,100]: dist[0]+100=100=temp[1] → no change
  [1,3,600]: dist[1]+600=700 < INF → temp[3]=700
  Final: dist=[0,100,INF,700]

dist[3]=700 ✓ (0→1→3, 1 stop = k stops)
```

---

## Quick Pattern Reference

| Problem | Pattern | Key technique |
|---------|---------|---------------|
| Friend Circles | Union Find | union connected nodes, count roots |
| Redundant Connection | Union Find | union returns false = redundant |
| Most Stones Removed | Union Find | union same row/col, n - components |
| Network Connected | Union Find | components - 1 moves needed |
| Equality Equations | Union Find | union ==, check != |
| Accounts Merge | Union Find | union same-account emails |
| Connecting Cities | Kruskal (UF) | sort edges + UF |
| Surrounded Regions | DFS boundary | DFS from border, mark safe, flip rest |
| Number of Enclaves | DFS boundary | DFS from border 1s, count remaining |
| Inform Employees | DFS propagation | return informTime + max(children) |
| Number of Islands | DFS island | mark '1'→'0', count DFS calls |
| Max Area of Island | DFS island | return 1 + sum neighbors |
| Closed Islands | DFS island | DFS boundary first, then count |
| Flood Fill | DFS island | change color during DFS |
| Keys and Rooms | DFS island | check all rooms visited |
| Find Safe States | DFS cycle | 3-color: unvisited/in-path/safe |
| 01 Matrix | Multi-source BFS | seed all 0s, BFS outward |
| Rotting Oranges | Multi-source BFS | seed all rotten, count minutes |
| As Far from Land | Multi-source BFS | seed all land, last distance = answer |
| Shortest Path Binary Matrix | BFS 8-dir | level = path length |
| Is Graph Bipartite | BFS 2-color | conflict → false |
| Possible Bipartition | BFS 2-color | build graph from dislikes |
| Course Schedule | Topological Sort | processed < n → cycle |
| Course Schedule II | Topological Sort | collect order during processing |
| Network Delay (Dijkstra) | Dijkstra | min-heap, stale check |
| Network Delay (Bellman-Ford) | Bellman-Ford | relax n-1 times |
| Find the City | Floyd-Warshall | 3 loops, all-pairs, count within threshold |
| Cheapest Flights K Stops | Bellman-Ford K | relax k+1 times with temp copy |
