# Graph Algorithms — One Place for Quick Revision

> **Original post:** Graph Algorithms One Place | Dijkstra | Bellman Ford | Floyd Warshall | Prims | Kruskals | DSU — by Naresh Gupta
> **Language:** Java (same as original post)
> **Notes file:** [01_graph_notes.md](./01_graph_notes.md)

One place to revise all standard graph algorithms before interviews. Each algorithm has the **problem it's demonstrated on**, **full Java code** (from the original post), and **complexity notes**.

---

## Time Complexity Summary

| Algorithm | Time Complexity | Type |
|-----------|----------------|------|
| Dijkstra | O(V + E log E) | SSSP — Single Source Shortest Path |
| Bellman-Ford | O(V × E) | SSSP |
| Floyd-Warshall | O(V³) | MSSP — Multi Source Shortest Path (All Pairs) |
| Prim's | O(E log E) | MST |
| Kruskal's | O(E log E) | MST |

**Problem used for SSSP:** [Network Delay Time — LC #743](https://leetcode.com/problems/network-delay-time/)
**Problem used for MST:** [Min Cost to Connect All Points — LC #1584](https://leetcode.com/problems/min-cost-to-connect-all-points/)

---

## Algorithm 1 — Dijkstra

**Use when:** Weighted graph, **no negative edges**, single source shortest path.

```java
class Solution {
    public int networkDelayTime(int[][] times, int N, int K) {
        List<int[]>[] adj = new ArrayList[N];
        for (int i = 0; i < N; i++) {
            adj[i] = new ArrayList<>();
        }
        for (int[] t : times) {
            adj[t[0] - 1].add(new int[]{t[1] - 1, t[2]});
        }

        int[] dist = new int[N];
        Arrays.fill(dist, -1);
        dist[K - 1] = 0;

        Queue<int[]> minHeap = new PriorityQueue<>((a, b) -> Integer.compare(a[1], b[1]));
        minHeap.offer(new int[]{K - 1, 0});

        while (minHeap.size() > 0) {
            int curr = minHeap.peek()[0];
            minHeap.poll();
            for (int[] pair : adj[curr]) {
                int next = pair[0];
                int weight = pair[1];
                int d = dist[curr] + weight;
                if (dist[next] == -1 || dist[next] > d) {
                    dist[next] = d;
                    minHeap.offer(new int[]{next, dist[next]});
                }
            }
        }

        int maxwait = 0;
        for (int i = 0; i < N; i++) {
            if (dist[i] == -1) return -1;
            maxwait = Math.max(maxwait, dist[i]);
        }
        return maxwait;
    }
}
```

> **Note:** This version uses `-1` for unvisited (instead of `MAX_VALUE`). The stale-check is replaced by the `dist[next] == -1 || dist[next] > d` condition.

---

## Algorithm 2 — Bellman-Ford

**Use when:** Weighted graph, **can have negative edges**, single source shortest path. Also used for K-hop constraints.

```java
class Solution {
    public int networkDelayTime(int[][] times, int N, int K) {
        int[] dist = new int[N + 1];
        Arrays.fill(dist, Integer.MAX_VALUE);

        dist[K] = 0;
        for (int i = 1; i < N; i++) {                    // relax N-1 times
            for (int[] e : times) {
                int u = e[0], v = e[1], w = e[2];
                if (dist[u] != Integer.MAX_VALUE && dist[v] > dist[u] + w)
                    dist[v] = dist[u] + w;
            }
        }

        int maxwait = 0;
        for (int i = 1; i <= N; i++)
            maxwait = Math.max(maxwait, dist[i]);
        return maxwait == Integer.MAX_VALUE ? -1 : maxwait;
    }
}
```

### Bellman-Ford — Short version

```java
class Solution {
    public int networkDelayTime(int[][] times, int N, int K) {
        int[] dist = new int[N];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[K - 1] = 0;

        for (int i = 1; i < N; i++)
            for (int[] e : times)
                if (dist[e[0] - 1] != Integer.MAX_VALUE && dist[e[1] - 1] > dist[e[0] - 1] + e[2])
                    dist[e[1] - 1] = dist[e[0] - 1] + e[2];

        int maxwait = Arrays.stream(dist).max().getAsInt();
        return maxwait == Integer.MAX_VALUE ? -1 : maxwait;
    }
}
```

---

## Algorithm 3 — Floyd-Warshall

**Use when:** Need shortest path between **ALL pairs** of nodes. Small V (V ≤ 500 due to O(V³)).

```java
class Solution {
    public int networkDelayTime(int[][] times, int N, int K) {
        int MAX = 1000000;
        int[][] dist = new int[N][N];

        for (int i = 0; i < N; i++) Arrays.fill(dist[i], MAX);
        for (int i = 0; i < N; i++) dist[i][i] = 0;
        for (int[] e : times) dist[e[0] - 1][e[1] - 1] = e[2];

        for (int k = 0; k < N; k++)              // intermediate node
            for (int i = 0; i < N; i++)
                for (int j = 0; j < N; j++)
                    dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);

        int maxwait = 0;
        for (int i = 0; i < N; i++)
            maxwait = Math.max(maxwait, dist[K - 1][i]);
        return maxwait == MAX ? -1 : maxwait;
    }
}
```

> **When to use Floyd-Warshall vs Dijkstra × V:**
> - Floyd-Warshall: O(V³), simpler, handles negatives
> - Dijkstra × V: O(V(E log E)), faster for sparse graphs

---

## Algorithm 4 — Prim's Algorithm (MST)

**Use when:** Minimum cost to connect all nodes. Good for **dense graphs**.

### Shorter version

```java
class Solution {
    public int minCostConnectPoints(int[][] p) {
        int n = p.length;
        PriorityQueue<int[]> pq = new PriorityQueue<>((u, v) -> Integer.compare(u[2], v[2]));
        pq.offer(new int[]{0, 0, 0});     // {from, to, cost}
        boolean[] mst = new boolean[n];
        int selectedEdges = 0, cost = 0;

        while (pq.size() > 0 || selectedEdges < n - 1) {
            int[] e = pq.poll();
            if (mst[e[1]]) continue;          // already in MST
            mst[e[1]] = true;
            cost += e[2];
            selectedEdges++;
            for (int j = 0; j < n; j++)
                if (!mst[j])
                    pq.offer(new int[]{e[1], j,
                        Math.abs(p[e[1]][0] - p[j][0]) + Math.abs(p[e[1]][1] - p[j][1])});
        }
        return cost;
    }
}
```

### Longer version (precompute distance matrix)

```java
class Solution {
    public int minCostConnectPoints(int[][] p) {
        int n = p.length;
        int[][] dist = new int[n][n];

        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                dist[i][j] = Math.abs(p[i][0]-p[j][0]) + Math.abs(p[i][1]-p[j][1]);

        PriorityQueue<int[]> pq = new PriorityQueue<>((u, v) -> Integer.compare(u[2], v[2]));
        pq.offer(new int[]{0, 0, 0});
        boolean[] mst = new boolean[n];
        int selectedEdges = 0, cost = 0;

        while (pq.size() > 0 || selectedEdges < n - 1) {
            int[] e = pq.poll();
            if (mst[e[1]]) continue;
            mst[e[1]] = true;
            cost += e[2];
            selectedEdges++;
            for (int j = 0; j < n; j++)
                if (!mst[j])
                    pq.offer(new int[]{e[1], j, dist[e[1]][j]});
        }
        return cost;
    }
}
```

---

## Algorithm 5 — Kruskal's Algorithm (MST)

**Use when:** Minimum cost to connect all nodes. Good for **sparse graphs**. Requires sorting edges.

```java
class Solution {
    int[] parent;

    int find(int x) {
        if (parent[x] == x) return x;
        return find(parent[x]);
    }

    void union(int x, int y) {
        int u = find(x), v = find(y);
        if (u != v) parent[u] = parent[v];
    }

    public int minCostConnectPoints(int[][] p) {
        int n = p.length;

        // Generate all edges
        PriorityQueue<int[]> pq = new PriorityQueue<>((u, v) -> Integer.compare(u[2], v[2]));
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                pq.offer(new int[]{i, j,
                    Math.abs(p[i][0]-p[j][0]) + Math.abs(p[i][1]-p[j][1])});

        parent = new int[n];
        for (int i = 0; i < n; i++) parent[i] = i;

        int selectedEdges = 0, cost = 0;
        while (pq.size() > 0 || selectedEdges < n - 1) {
            int[] e = pq.poll();
            if (find(e[0]) == find(e[1])) continue;  // same component → skip (cycle)
            selectedEdges++;
            union(e[0], e[1]);
            cost += e[2];
        }
        return cost;
    }
}
```

---

## Algorithm 6 — Generic Union Find (DSU)

**Full implementation with path compression (halving) + union by rank**

```java
class UnionFind {
    private int size;
    private int numComponents;
    private int[] parent;
    private int[] rank;

    public UnionFind(int n) {
        if (n <= 0) throw new IllegalArgumentException("Size <= 0 not allowed");
        size = numComponents = n;
        parent = new int[n];
        rank = new int[n];
        for (int i = 0; i < n; i++) parent[i] = i;
    }

    // Path compression by halving (path-splitting variant)
    public int find(int p) {
        while (p != parent[p]) {
            parent[p] = parent[parent[p]];   // halving — skip one level
            p = parent[p];
        }
        return p;
    }

    // Union by rank
    public void union(int p, int q) {
        int rootP = find(p), rootQ = find(q);
        if (rootP == rootQ) return;

        if (rank[rootQ] > rank[rootP]) {
            parent[rootP] = rootQ;
        } else {
            parent[rootQ] = rootP;
            if (rank[rootP] == rank[rootQ]) rank[rootP]++;
        }
        numComponents--;
    }

    public boolean connected(int p, int q) { return find(p) == find(q); }
    public int components() { return numComponents; }
    public int size() { return size; }
}
```

### Sample usage — Is Graph Bipartite? (UF approach)

```java
class Solution {
    public boolean isBipartite(int[][] graph) {
        UnionFind uf = new UnionFind(graph.length);
        for (int i = 0; i < graph.length; i++) {
            for (int j = 0; j < graph[i].length; j++) {
                // i and graph[i][j] are enemies → they should be in different sets
                // but all neighbors of i should be in the same set (enemy of i)
                if (uf.find(i) == uf.find(graph[i][j]))
                    return false;           // i and its neighbor in same set → conflict
                uf.union(graph[i][0], graph[i][j]);   // union all neighbors of i together
            }
        }
        return true;
    }
}
```

> **Note:** This UF approach for bipartite works because: all neighbors of node `i` must be on the SAME side (opposite to `i`). So we union all of `i`'s neighbors together. If `i` and any neighbor end up in the same set → not bipartite.

---

## Kruskal vs Prim — When to use which?

| | Kruskal | Prim |
|--|---------|------|
| Approach | Sort edges + UF | Grow tree greedily |
| Best for | Sparse graphs | Dense graphs |
| Starting point | Any edge | Specific node |
| Time | O(E log E) | O(E log V) |
| Implementation | Easier (sort + UF) | Slightly more complex |

---

## Dijkstra vs Bellman-Ford — When to use which?

| | Dijkstra | Bellman-Ford |
|--|---------|-------------|
| Negative edges | ❌ No | ✅ Yes |
| Negative cycles | ❌ Cannot detect | ✅ Can detect |
| Time | O((V+E) log V) | O(V×E) |
| K-hop limit | Not natural | ✅ Natural (relax K times) |
| Use when | Non-negative weights | Negative weights or K stops |

---

## Complete Algorithm Quick Reference

```
Need min cost to connect ALL nodes?
    Sparse graph → Kruskal (sort edges + UF)
    Dense graph  → Prim (min-heap from source)

Need shortest path from ONE source?
    No negatives → Dijkstra (min-heap, stale check)
    Negatives    → Bellman-Ford (relax V-1 times)
    K hops max   → Bellman-Ford (relax K+1 times with temp copy)

Need shortest path between ALL pairs?
    → Floyd-Warshall (3 nested loops, O(V³))

Need connected components / merge groups?
    → Union Find (find + union + path compression)

Need task ordering / dependency resolution?
    → Topological Sort — Kahn's BFS (indegree + queue)

Need to detect cycle in directed graph?
    → DFS 3-coloring (0=unvisited, 1=in-path, 2=done)
    → OR Topological Sort (processed < n → cycle)

Need to check 2-colorable?
    → BFS 2-coloring (conflict = not bipartite)
    → OR Union Find (union all neighbors, check conflict)
```
