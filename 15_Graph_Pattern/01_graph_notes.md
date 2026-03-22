# Graph Pattern — Notes & Templates

> **Pattern family:** Graph Traversal / Shortest Path / Connectivity
> **Difficulty range:** Easy → Hard
> **Language:** Java
> **Problems file:** [02_graph_problems.md](./02_graph_problems.md)
> **Beginners guide:** [03_graph_beginners_guide.md](./03_graph_beginners_guide.md)
> **Advanced algorithms:** [04_graph_algorithms_advanced.md](./04_graph_algorithms_advanced.md)

---

## Table of Contents

1. [How to identify this pattern](#1-how-to-identify-this-pattern) ← **start here**
2. [What is this pattern?](#2-what-is-this-pattern)
3. [Graph representation](#3-graph-representation)
4. [Core algorithms](#4-core-algorithms)
5. [Variants table](#5-variants-table)
6. [Universal Java templates](#6-universal-java-templates)
7. [Quick reference cheatsheet](#7-quick-reference-cheatsheet)
8. [Common mistakes](#8-common-mistakes)
9. [Complexity summary](#9-complexity-summary)

---

## 1. How to identify this pattern

### Keyword scanner

| If you see this... | Algorithm |
|--------------------|-----------|
| `"connected components / islands / provinces"` | DFS / BFS / Union Find |
| `"shortest path in unweighted graph"` | BFS (level by level) |
| `"shortest path in weighted graph"` | Dijkstra (non-negative) / Bellman-Ford (negative) |
| `"shortest path between ALL pairs"` | Floyd-Warshall |
| `"task ordering / dependency resolution"` | Topological Sort (Kahn's BFS) |
| `"cycle detection in directed graph"` | Topological Sort / DFS coloring |
| `"cycle detection in undirected graph"` | Union Find / DFS |
| `"minimum cost to connect all nodes"` | MST — Kruskal's / Prim's |
| `"group connectivity / find / merge"` | Union Find (DSU) |
| `"2-colorable / divide into 2 groups"` | Bipartite check (BFS coloring) |
| `"flood fill / spreading / rotting"` | Multi-source BFS |
| `"all paths from source to target"` | DFS backtracking |
| `"longest path in DAG"` | Topological Sort + DP |

### Decision flowchart

```
Graph problem?
        │
        ├── Unweighted graph + shortest path?
        │       └── BFS (level = distance)
        │
        ├── Weighted graph + shortest path (no negative)?
        │       └── Dijkstra (min-heap)
        │
        ├── Weighted graph + negative edges?
        │       └── Bellman-Ford (relax V-1 times)
        │
        ├── All-pairs shortest path?
        │       └── Floyd-Warshall (DP, 3 loops)
        │
        ├── Connected components / islands?
        │       └── DFS or BFS (visited array)
        │              OR Union Find (connect-find)
        │
        ├── Minimum spanning tree?
        │       └── Kruskal (sort edges + UF)
        │              OR Prim (min-heap from source)
        │
        ├── Task ordering / dependencies?
        │       └── Topological Sort (Kahn's BFS / DFS)
        │
        ├── 2-colorable / bipartite?
        │       └── BFS coloring (alternate 0/1)
        │
        └── Merge groups / detect cycles in undirected?
                └── Union Find (DSU)
```

---

## 2. What is this pattern?

A **graph** is a set of nodes (vertices) connected by edges. Graphs can be:
- **Directed** (edges have direction) or **Undirected**
- **Weighted** (edges have cost) or **Unweighted**
- **Cyclic** (contains cycles) or **Acyclic** (DAG)

```
Undirected:   1 — 2 — 3        Directed:  1 → 2 → 3
              |       |                    ↑       ↓
              4 — — — 5                   4 ← ← ← 5
```

**The two fundamental operations:**
1. **Traversal** — visit all reachable nodes (BFS / DFS)
2. **Query** — shortest path, connectivity, cycle detection

---

## 3. Graph Representation

### Adjacency List (most common for LC problems)

```java
// Build from edge list
int n = 5;   // number of nodes
List<List<Integer>> adj = new ArrayList<>();
for (int i = 0; i < n; i++) adj.add(new ArrayList<>());

// Undirected
adj.get(u).add(v);
adj.get(v).add(u);

// Directed
adj.get(u).add(v);

// Weighted undirected: int[] = {neighbor, weight}
List<int[]>[] adj = new List[n];
for (int i = 0; i < n; i++) adj[i] = new ArrayList<>();
adj[u].add(new int[]{v, w});
adj[v].add(new int[]{u, w});
```

### Grid as Graph (very common)

```java
// 4-directional neighbors
int[] dr = {0, 0, 1, -1};
int[] dc = {1, -1, 0, 0};

for (int d = 0; d < 4; d++) {
    int nr = r + dr[d];
    int nc = c + dc[d];
    if (nr >= 0 && nr < rows && nc >= 0 && nc < cols) {
        // valid neighbor
    }
}

// 8-directional (diagonal too)
int[] dr = {-1,-1,-1, 0, 0, 1, 1, 1};
int[] dc = {-1, 0, 1,-1, 1,-1, 0, 1};
```

---

## 4. Core algorithms

### BFS — Breadth First Search

**Use when:** shortest path in unweighted graph, level-by-level traversal, multi-source spreading.

```
Key insight: BFS visits nodes level by level.
Level 0 = source, Level 1 = neighbors, Level 2 = neighbors of neighbors...
→ First time you reach a node = shortest path in unweighted graph.
```

### DFS — Depth First Search

**Use when:** connected components, cycle detection, all paths, topological sort, backtracking.

```
Key insight: DFS goes as deep as possible before backtracking.
→ Good for exploring ALL paths, not shortest path.
→ Uses recursion (implicit stack) or explicit stack.
```

### Dijkstra

**Use when:** shortest path, weighted graph, NO negative weights.

```
Key insight: Greedy — always process the node with smallest known distance.
Uses min-heap (PriorityQueue). Guarantees optimal for non-negative weights.
Time: O((V + E) log V)
```

### Bellman-Ford

**Use when:** shortest path, weighted graph, CAN have negative weights (but no negative cycles).

```
Key insight: Relax ALL edges V-1 times.
→ After V-1 relaxations, shortest paths are guaranteed.
→ V-th relaxation: if any update happens → negative cycle detected.
Time: O(V × E)
```

### Floyd-Warshall

**Use when:** shortest path between ALL pairs of nodes.

```
Key insight: DP — dp[i][j] = shortest from i to j using intermediate nodes 0..k.
dp[i][j] = min(dp[i][j], dp[i][k] + dp[k][j])
Time: O(V³)
```

### Topological Sort (Kahn's BFS)

**Use when:** task ordering, dependency resolution, DAG processing.

```
Key insight: Node with in-degree 0 has no dependencies → process it first.
BFS using queue of in-degree-0 nodes.
If processed count < total nodes → cycle exists.
```

### Union Find (DSU)

**Use when:** connected components, cycle detection in undirected, merging groups.

```
Key insight: Each component has one "root". find(x) returns root.
union(x, y) merges two components.
Path compression + union by rank → near O(1) amortized.
```

### Kruskal's MST

**Use when:** minimum cost to connect all nodes.

```
Key insight: Sort edges by weight. Add edge if it doesn't form a cycle (use UF).
Greedy: always add cheapest valid edge.
Time: O(E log E)
```

### Prim's MST

**Use when:** minimum cost to connect all nodes (dense graphs).

```
Key insight: Start from any node. Greedily add cheapest edge connecting 
a visited node to an unvisited node. Use min-heap.
Time: O(E log V)
```

---

## 5. Variants table

| Algorithm | Graph type | Handles negative? | Time | Space | Use case |
|-----------|-----------|-------------------|------|-------|----------|
| BFS | Unweighted | N/A | O(V+E) | O(V) | Shortest path (hops) |
| DFS | Any | N/A | O(V+E) | O(V) | All paths, cycle, components |
| Dijkstra | Weighted | ❌ No | O((V+E)logV) | O(V) | Single-source shortest |
| Bellman-Ford | Weighted | ✅ Yes | O(V×E) | O(V) | Single-source, negative edges |
| Floyd-Warshall | Weighted | ✅ Yes | O(V³) | O(V²) | All-pairs shortest |
| Topo Sort (Kahn) | Directed DAG | N/A | O(V+E) | O(V) | Task ordering |
| Union Find | Undirected | N/A | O(α(n)) | O(V) | Components, cycle detect |
| Kruskal | Weighted | N/A | O(E logE) | O(V) | MST (sparse graph) |
| Prim | Weighted | N/A | O(E logV) | O(V) | MST (dense graph) |

---

## 6. Universal Java templates

```java
// ─── TEMPLATE A: BFS — Shortest Path (Unweighted) ────────────────────────────
public int bfs(int start, int end, List<List<Integer>> adj) {
    boolean[] visited = new boolean[adj.size()];
    Queue<Integer> queue = new LinkedList<>();
    queue.offer(start);
    visited[start] = true;
    int dist = 0;

    while (!queue.isEmpty()) {
        int size = queue.size();          // snapshot current level size
        for (int i = 0; i < size; i++) {
            int node = queue.poll();
            if (node == end) return dist;
            for (int next : adj.get(node)) {
                if (!visited[next]) {
                    visited[next] = true;
                    queue.offer(next);
                }
            }
        }
        dist++;
    }
    return -1;
}

// ─── TEMPLATE B: DFS — Connected Components ──────────────────────────────────
public int countComponents(int n, List<List<Integer>> adj) {
    boolean[] visited = new boolean[n];
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (!visited[i]) { dfs(adj, visited, i); count++; }
    }
    return count;
}
private void dfs(List<List<Integer>> adj, boolean[] visited, int node) {
    visited[node] = true;
    for (int next : adj.get(node))
        if (!visited[next]) dfs(adj, visited, next);
}

// ─── TEMPLATE C: Grid BFS — Multi-source ─────────────────────────────────────
// (e.g. Rotting Oranges — start BFS from ALL rotten oranges simultaneously)
int[] dr = {0,0,1,-1}, dc = {1,-1,0,0};
Queue<int[]> queue = new LinkedList<>();
// seed all sources
for (int r = 0; r < rows; r++)
    for (int c = 0; c < cols; c++)
        if (grid[r][c] == SOURCE) queue.offer(new int[]{r, c});
int time = 0;
while (!queue.isEmpty()) {
    int size = queue.size();
    for (int i = 0; i < size; i++) {
        int[] cur = queue.poll();
        for (int d = 0; d < 4; d++) {
            int nr = cur[0]+dr[d], nc = cur[1]+dc[d];
            if (valid(nr,nc) && grid[nr][nc] == FRESH) {
                grid[nr][nc] = ROTTEN;
                queue.offer(new int[]{nr, nc});
            }
        }
    }
    time++;
}

// ─── TEMPLATE D: Dijkstra ─────────────────────────────────────────────────────
public int[] dijkstra(int src, int n, List<int[]>[] adj) {
    int[] dist = new int[n];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[src] = 0;
    // min-heap: {dist, node}
    PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> a[0]-b[0]);
    pq.offer(new int[]{0, src});

    while (!pq.isEmpty()) {
        int[] cur = pq.poll();
        int d = cur[0], u = cur[1];
        if (d > dist[u]) continue;        // stale entry — skip
        for (int[] edge : adj[u]) {
            int v = edge[0], w = edge[1];
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.offer(new int[]{dist[v], v});
            }
        }
    }
    return dist;
}

// ─── TEMPLATE E: Bellman-Ford ────────────────────────────────────────────────
public int[] bellmanFord(int src, int n, int[][] edges) {
    int[] dist = new int[n];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[src] = 0;

    for (int i = 1; i <= n-1; i++) {          // relax V-1 times
        for (int[] e : edges) {
            int u = e[0], v = e[1], w = e[2];
            if (dist[u] != Integer.MAX_VALUE && dist[u]+w < dist[v])
                dist[v] = dist[u]+w;
        }
    }
    // check negative cycle
    for (int[] e : edges)
        if (dist[e[0]] != Integer.MAX_VALUE && dist[e[0]]+e[2] < dist[e[1]])
            return null;  // negative cycle exists
    return dist;
}

// ─── TEMPLATE F: Floyd-Warshall ──────────────────────────────────────────────
public int[][] floydWarshall(int n, int[][] edges) {
    int[][] dp = new int[n][n];
    for (int[] row : dp) Arrays.fill(row, Integer.MAX_VALUE/2);
    for (int i = 0; i < n; i++) dp[i][i] = 0;
    for (int[] e : edges) dp[e[0]][e[1]] = e[2];

    for (int k = 0; k < n; k++)
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                dp[i][j] = Math.min(dp[i][j], dp[i][k] + dp[k][j]);
    return dp;
}

// ─── TEMPLATE G: Topological Sort (Kahn's BFS) ───────────────────────────────
public int[] topoSort(int n, List<List<Integer>> adj) {
    int[] indegree = new int[n];
    for (int u = 0; u < n; u++)
        for (int v : adj.get(u)) indegree[v]++;

    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < n; i++) if (indegree[i] == 0) queue.offer(i);

    int[] order = new int[n]; int idx = 0;
    while (!queue.isEmpty()) {
        int u = queue.poll();
        order[idx++] = u;
        for (int v : adj.get(u))
            if (--indegree[v] == 0) queue.offer(v);
    }
    return idx == n ? order : new int[0]; // empty = cycle exists
}

// ─── TEMPLATE H: Union Find (DSU) with path compression + union by rank ───────
class UnionFind {
    int[] parent, rank;
    int components;

    UnionFind(int n) {
        parent = new int[n]; rank = new int[n]; components = n;
        for (int i = 0; i < n; i++) parent[i] = i;
    }
    int find(int x) {
        if (parent[x] != x) parent[x] = find(parent[x]); // path compression
        return parent[x];
    }
    boolean union(int x, int y) {
        int px = find(x), py = find(y);
        if (px == py) return false;             // already same component
        if (rank[px] < rank[py]) { int t=px; px=py; py=t; }
        parent[py] = px;
        if (rank[px] == rank[py]) rank[px]++;
        components--;
        return true;
    }
    boolean connected(int x, int y) { return find(x) == find(y); }
}

// ─── TEMPLATE I: Kruskal's MST ───────────────────────────────────────────────
public int kruskalMST(int n, int[][] edges) {
    Arrays.sort(edges, (a,b) -> a[2]-b[2]);  // sort by weight
    UnionFind uf = new UnionFind(n);
    int cost = 0, edgeCount = 0;
    for (int[] e : edges) {
        if (uf.union(e[0], e[1])) {           // add if no cycle
            cost += e[2]; edgeCount++;
            if (edgeCount == n-1) break;       // MST complete (n-1 edges)
        }
    }
    return edgeCount == n-1 ? cost : -1;      // -1 if not fully connected
}

// ─── TEMPLATE J: Cycle Detection — Directed (DFS coloring) ───────────────────
// 0=unvisited, 1=in current path, 2=done
public boolean hasCycleDirected(int n, List<List<Integer>> adj) {
    int[] color = new int[n];
    for (int i = 0; i < n; i++)
        if (color[i] == 0 && dfsCycle(adj, color, i)) return true;
    return false;
}
private boolean dfsCycle(List<List<Integer>> adj, int[] color, int u) {
    color[u] = 1;                             // mark as in-path
    for (int v : adj.get(u)) {
        if (color[v] == 1) return true;       // back edge → cycle
        if (color[v] == 0 && dfsCycle(adj, color, v)) return true;
    }
    color[u] = 2;                             // done
    return false;
}

// ─── TEMPLATE K: Bipartite Check (BFS 2-coloring) ────────────────────────────
public boolean isBipartite(List<List<Integer>> adj) {
    int n = adj.size();
    int[] color = new int[n];
    Arrays.fill(color, -1);

    for (int start = 0; start < n; start++) {
        if (color[start] != -1) continue;
        Queue<Integer> q = new LinkedList<>();
        q.offer(start); color[start] = 0;
        while (!q.isEmpty()) {
            int u = q.poll();
            for (int v : adj.get(u)) {
                if (color[v] == -1) { color[v] = 1-color[u]; q.offer(v); }
                else if (color[v] == color[u]) return false; // same color → not bipartite
            }
        }
    }
    return true;
}
```

---

## 7. Quick reference cheatsheet

```
SIGNAL IN PROBLEM                          → ALGORITHM         → KEY CODE
─────────────────────────────────────────────────────────────────────────────────
"number of islands / connected components" → DFS/BFS           → visited array, call from each unvisited
"shortest path, no weights"                → BFS               → level = distance, queue
"shortest path, positive weights"          → Dijkstra          → min-heap {dist, node}
"shortest path, negative weights"          → Bellman-Ford      → relax all edges V-1 times
"shortest path between ALL pairs"          → Floyd-Warshall    → dp[i][j]=min(dp[i][j],dp[i][k]+dp[k][j])
"task ordering / course prerequisites"     → Topological Sort  → indegree + Kahn's BFS
"cycle in directed graph"                  → Topo sort / DFS   → color: 0=unseen, 1=path, 2=done
"merge groups / redundant connection"      → Union Find        → find(x)==find(y) → cycle
"min cost to connect all nodes"            → Kruskal / Prim    → sort edges + UF (Kruskal)
"2-colorable / bipartite / divide groups"  → BFS coloring      → alternate 0/1, conflict=not bipartite
"flood fill / spread from sources"         → Multi-source BFS  → seed all sources in queue first
"all paths from source to target"          → DFS backtracking  → try all edges, backtrack
"longest path in DAG"                      → Topo Sort + DP    → dp[node] = max(dp[next]+1)
```

**Algorithm selector — 3 questions:**
```
1. Is it weighted?
   NO  → BFS (shortest path) or DFS (everything else)
   YES → go to 2

2. Are there negative weights?
   NO  → Dijkstra
   YES → Bellman-Ford (single source) / Floyd-Warshall (all pairs)

3. Need to connect all nodes at min cost?
   → Kruskal (sort edges + Union Find)
```

---

## 8. Common mistakes

### Mistake 1 — BFS without level tracking (lose distance info)

```java
// BUG — can't track distance
while (!q.isEmpty()) { int u = q.poll(); ... }

// FIX — snapshot size per level
while (!q.isEmpty()) {
    int size = q.size();         // level size snapshot
    for (int i = 0; i < size; i++) {
        int u = q.poll(); ...
    }
    dist++;
}
```

### Mistake 2 — Dijkstra with negative weights (gives wrong answer)

```java
// BUG — Dijkstra assumes once a node is settled, it's optimal
// Negative edge can make a "settled" node have a shorter path later
// → Use Bellman-Ford instead
```

### Mistake 3 — Forgetting stale entry check in Dijkstra

```java
// BUG — processes same node multiple times with outdated distances
int[] cur = pq.poll();
// ... process immediately

// FIX — skip stale entries
int[] cur = pq.poll();
if (cur[0] > dist[cur[1]]) continue;   // stale — already found better
```

### Mistake 4 — Topological sort doesn't detect cycle

```java
// BUG — just returns some order even if graph has cycle
// FIX — check if all nodes were processed
return idx == n ? order : null;  // null = cycle exists
```

### Mistake 5 — Grid BFS without boundary check

```java
// BUG — ArrayIndexOutOfBoundsException
int nr = r+dr[d], nc = c+dc[d];
if (grid[nr][nc] == 0) ...   // nr/nc might be out of bounds!

// FIX — always check bounds first
if (nr>=0 && nr<rows && nc>=0 && nc<cols && grid[nr][nc]==0) ...
```

### Mistake 6 — Union Find without path compression (TLE)

```java
// BUG — O(n) find without compression
int find(int x) { return parent[x]==x ? x : find(parent[x]); }

// FIX — path compression
int find(int x) {
    if (parent[x] != x) parent[x] = find(parent[x]);
    return parent[x];
}
```

### Mistake 7 — Floyd-Warshall overflow

```java
// BUG — MAX_VALUE + weight overflows to negative
dp[i][j] = Integer.MAX_VALUE;
dp[i][j] = Math.min(dp[i][j], dp[i][k] + dp[k][j]);  // overflow!

// FIX — use MAX_VALUE/2
Arrays.fill(row, Integer.MAX_VALUE / 2);
```

---

## 9. Complexity summary

| Algorithm | Time | Space | Notes |
|-----------|------|-------|-------|
| BFS | O(V+E) | O(V) | V=vertices, E=edges |
| DFS | O(V+E) | O(V) | recursion stack O(V) |
| Dijkstra | O((V+E) log V) | O(V) | min-heap implementation |
| Bellman-Ford | O(V×E) | O(V) | slower but handles negatives |
| Floyd-Warshall | O(V³) | O(V²) | all-pairs, small V only |
| Topological Sort | O(V+E) | O(V) | Kahn's BFS |
| Union Find | O(α(n)) ≈ O(1) | O(V) | with path compression + rank |
| Kruskal's MST | O(E log E) | O(V) | dominated by sorting |
| Prim's MST | O(E log V) | O(V) | min-heap |
| Bipartite Check | O(V+E) | O(V) | BFS/DFS coloring |

**Grid problems:** V = rows×cols, E = 4×rows×cols → O(rows×cols)
