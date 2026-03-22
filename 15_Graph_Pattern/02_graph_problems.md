# Graph Pattern — Solved Problems (43 Problems)

> **Notes & Templates:** [01_graph_notes.md](./01_graph_notes.md)
> **Language:** Java

---

## Table of Contents

### Category 1 — BFS / DFS / Grid (13 problems)
- [P1 — Number of Islands](#problem-1--number-of-islands)
- [P2 — Friend Circles (Number of Provinces)](#problem-2--friend-circles-number-of-provinces)
- [P3 — Max Area of Island](#problem-3--max-area-of-island)
- [P4 — Surrounded Regions](#problem-4--surrounded-regions)
- [P5 — Shortest Path in Binary Matrix](#problem-5--shortest-path-in-binary-matrix)
- [P6 — Word Ladder](#problem-6--word-ladder)
- [P7 — Path with Minimum Effort](#problem-7--path-with-minimum-effort)
- [P8 — Swim in Rising Water](#problem-8--swim-in-rising-water)
- [P9 — Minimum Moves to Move Box to Target](#problem-9--minimum-moves-to-move-box-to-target)
- [P10 — Find Eventual Safe States](#problem-10--find-eventual-safe-states)
- [P11 — All Paths Source to Target](#problem-11--all-paths-source-to-target)
- [P12 — Longest Increasing Path in a Matrix](#problem-12--longest-increasing-path-in-a-matrix)
- [P13 — Longest Path in a DAG](#problem-13--longest-path-in-a-dag)

### Category 2 — Shortest Path (8 problems)
- [P14 — Network Delay Time (Dijkstra)](#problem-14--network-delay-time)
- [P15 — Cheapest Flights Within K Stops (Bellman-Ford)](#problem-15--cheapest-flights-within-k-stops)
- [P16 — Path with Maximum Probability (Dijkstra)](#problem-16--path-with-maximum-probability)
- [P17 — Minimum Cost to Reach Destination](#problem-17--minimum-cost-to-reach-destination)
- [P18 — Find the City with Smallest Neighbours (Floyd-Warshall)](#problem-18--find-the-city-with-smallest-neighbours)
- [P19 — Min Cost (Dijkstra variant)](#problem-19--min-cost)
- [P20 — Minimum Cost to reach destination in Time](#problem-20--minimum-cost-to-reach-destination-in-time)
- [P21 — Minimum Obstacle Removal to Reach Corner](#problem-21--minimum-obstacle-removal-to-reach-corner)

### Category 3 — Topological Sort (6 problems)
- [P22 — Course Schedule](#problem-22--course-schedule)
- [P23 — Course Schedule II](#problem-23--course-schedule-ii)
- [P24 — Course Schedule IV](#problem-24--course-schedule-iv)
- [P25 — Alien Dictionary](#problem-25--alien-dictionary)
- [P26 — Sequence Reconstruction](#problem-26--sequence-reconstruction)
- [P27 — Strange Printer II](#problem-27--strange-printer-ii)

### Category 4 — Union Find (8 problems)
- [P28 — Redundant Connection](#problem-28--redundant-connection)
- [P29 — Redundant Connection II](#problem-29--redundant-connection-ii)
- [P30 — Accounts Merge](#problem-30--accounts-merge)
- [P31 — Number of Operations to Make Network Connected](#problem-31--number-of-operations-to-make-network-connected)
- [P32 — Satisfiability of Equality Equations](#problem-32--satisfiability-of-equality-equations)
- [P33 — Min Cost to Connect All Points (Kruskal)](#problem-33--min-cost-to-connect-all-points)
- [P34 — Connecting Cities with Minimum Cost](#problem-34--connecting-cities-with-minimum-cost)
- [P35 — Min Cost to Provide Water](#problem-35--min-cost-to-provide-water)

### Category 5 — Bipartite / Graph Coloring (5 problems)
- [P36 — Is Graph Bipartite?](#problem-36--is-graph-bipartite)
- [P37 — Possible Bipartition](#problem-37--possible-bipartition)
- [P38 — Flower Planting With No Adjacent](#problem-38--flower-planting-with-no-adjacent)
- [P39 — Graph Coloring / M-Coloring Problem](#problem-39--m-coloring-problem)
- [P40 — Detect Cycle in Directed Graph](#problem-40--detect-cycle-in-directed-graph)

### Category 6 — MST (3 problems)
- [P41 — Minimum Spanning Tree (Kruskal)](#problem-41--minimum-spanning-tree)
- [P42 — Min Cost to Connect All Points (Prim)](#problem-42--min-cost-to-connect-all-points-prims)
- [P43 — Minimum Cost to Connect Sticks](#problem-43--minimum-cost-to-connect-sticks)

---

## Category 1 — BFS / DFS / Grid

---

### Problem 1 — Number of Islands
**LeetCode #200 | Difficulty: Medium | Company: Amazon, Google | Algorithm: DFS/BFS**

#### Approach

Count disconnected components of '1's. DFS from each unvisited '1', mark all connected cells visited.

#### Java code

```java
public int numIslands(char[][] grid) {
    int rows = grid.length, cols = grid[0].length, count = 0;
    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++)
            if (grid[r][c] == '1') { dfs(grid, r, c); count++; }
    return count;
}
private void dfs(char[][] grid, int r, int c) {
    if (r<0||r>=grid.length||c<0||c>=grid[0].length||grid[r][c]!='1') return;
    grid[r][c] = '0';   // mark visited
    dfs(grid,r+1,c); dfs(grid,r-1,c); dfs(grid,r,c+1); dfs(grid,r,c-1);
}
```

#### Example

```
Input: grid = [["1","1","0"],["0","1","0"],["0","0","1"]]
DFS from (0,0): marks (0,0),(0,1),(1,1) → island 1
DFS from (2,2): marks (2,2) → island 2
Output: 2 ✓
```

---

### Problem 2 — Friend Circles (Number of Provinces)
**LeetCode #547 | Difficulty: Medium | Company: Amazon, Facebook | Algorithm: DFS / Union Find**

> Adjacency matrix given. Count connected components.

#### Java code

```java
public int findCircleNum(int[][] isConnected) {
    int n = isConnected.length;
    boolean[] visited = new boolean[n];
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (!visited[i]) { dfs(isConnected, visited, i); count++; }
    }
    return count;
}
private void dfs(int[][] mat, boolean[] visited, int i) {
    visited[i] = true;
    for (int j = 0; j < mat.length; j++)
        if (mat[i][j] == 1 && !visited[j]) dfs(mat, visited, j);
}
```

---

### Problem 3 — Max Area of Island
**LeetCode #695 | Difficulty: Medium | Company: Amazon | Algorithm: DFS**

#### Java code

```java
public int maxAreaOfIsland(int[][] grid) {
    int max = 0;
    for (int r = 0; r < grid.length; r++)
        for (int c = 0; c < grid[0].length; c++)
            if (grid[r][c] == 1) max = Math.max(max, dfs(grid, r, c));
    return max;
}
private int dfs(int[][] grid, int r, int c) {
    if (r<0||r>=grid.length||c<0||c>=grid[0].length||grid[r][c]!=1) return 0;
    grid[r][c] = 0;
    return 1 + dfs(grid,r+1,c) + dfs(grid,r-1,c) + dfs(grid,r,c+1) + dfs(grid,r,c-1);
}
```

---

### Problem 4 — Surrounded Regions
**LeetCode #130 | Difficulty: Medium | Company: Google | Algorithm: DFS from border**

> Any 'O' connected to border is safe. Mark safe 'O's first (DFS from all border 'O's), then flip remaining 'O' → 'X'.

#### Java code

```java
public void solve(char[][] board) {
    int rows = board.length, cols = board[0].length;
    // Mark safe 'O's (connected to border) with 'S'
    for (int r = 0; r < rows; r++) {
        if (board[r][0] == 'O') dfs(board, r, 0);
        if (board[r][cols-1] == 'O') dfs(board, r, cols-1);
    }
    for (int c = 0; c < cols; c++) {
        if (board[0][c] == 'O') dfs(board, 0, c);
        if (board[rows-1][c] == 'O') dfs(board, rows-1, c);
    }
    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++)
            board[r][c] = board[r][c]=='S' ? 'O' : board[r][c]=='O' ? 'X' : board[r][c];
}
private void dfs(char[][] board, int r, int c) {
    if (r<0||r>=board.length||c<0||c>=board[0].length||board[r][c]!='O') return;
    board[r][c] = 'S';
    dfs(board,r+1,c); dfs(board,r-1,c); dfs(board,r,c+1); dfs(board,r,c-1);
}
```

---

### Problem 5 — Shortest Path in Binary Matrix
**LeetCode #1091 | Difficulty: Medium | Company: Facebook, Amazon | Algorithm: BFS**

> 8-directional BFS. Level = path length.

#### Java code

```java
public int shortestPathBinaryMatrix(int[][] grid) {
    int n = grid.length;
    if (grid[0][0] == 1 || grid[n-1][n-1] == 1) return -1;
    int[] dr = {-1,-1,-1,0,0,1,1,1}, dc = {-1,0,1,-1,1,-1,0,1};
    Queue<int[]> q = new LinkedList<>();
    q.offer(new int[]{0,0,1});
    grid[0][0] = 1;
    while (!q.isEmpty()) {
        int[] cur = q.poll();
        int r=cur[0], c=cur[1], dist=cur[2];
        if (r==n-1 && c==n-1) return dist;
        for (int d=0; d<8; d++) {
            int nr=r+dr[d], nc=c+dc[d];
            if (nr>=0&&nr<n&&nc>=0&&nc<n&&grid[nr][nc]==0) {
                grid[nr][nc]=1; q.offer(new int[]{nr,nc,dist+1});
            }
        }
    }
    return -1;
}
```

---

### Problem 6 — Word Ladder
**LeetCode #127 | Difficulty: Hard | Company: Amazon, Google | Algorithm: BFS**

> Minimum transformations from beginWord to endWord, changing one letter at a time.

#### Java code

```java
public int ladderLength(String beginWord, String endWord, List<String> wordList) {
    Set<String> wordSet = new HashSet<>(wordList);
    if (!wordSet.contains(endWord)) return 0;
    Queue<String> q = new LinkedList<>();
    q.offer(beginWord); wordSet.remove(beginWord);
    int steps = 1;
    while (!q.isEmpty()) {
        int size = q.size(); steps++;
        for (int i = 0; i < size; i++) {
            char[] word = q.poll().toCharArray();
            for (int j = 0; j < word.length; j++) {
                char orig = word[j];
                for (char ch = 'a'; ch <= 'z'; ch++) {
                    word[j] = ch;
                    String next = new String(word);
                    if (next.equals(endWord)) return steps;
                    if (wordSet.contains(next)) { q.offer(next); wordSet.remove(next); }
                }
                word[j] = orig;
            }
        }
    }
    return 0;
}
```

---

### Problem 7 — Path with Minimum Effort
**LeetCode #1631 | Difficulty: Medium | Company: Google | Algorithm: Dijkstra on grid**

> Minimum effort = minimize the maximum absolute difference along any path.

#### Java code

```java
public int minimumEffortPath(int[][] heights) {
    int rows = heights.length, cols = heights[0].length;
    int[][] dist = new int[rows][cols];
    for (int[] row : dist) Arrays.fill(row, Integer.MAX_VALUE);
    dist[0][0] = 0;
    int[] dr = {0,0,1,-1}, dc = {1,-1,0,0};
    PriorityQueue<int[]> pq = new PriorityQueue<>((a,b)->a[0]-b[0]);
    pq.offer(new int[]{0,0,0});  // {effort, r, c}
    while (!pq.isEmpty()) {
        int[] cur = pq.poll();
        int effort=cur[0], r=cur[1], c=cur[2];
        if (r==rows-1&&c==cols-1) return effort;
        if (effort > dist[r][c]) continue;
        for (int d=0; d<4; d++) {
            int nr=r+dr[d], nc=c+dc[d];
            if (nr>=0&&nr<rows&&nc>=0&&nc<cols) {
                int newEffort = Math.max(effort, Math.abs(heights[nr][nc]-heights[r][c]));
                if (newEffort < dist[nr][nc]) {
                    dist[nr][nc] = newEffort;
                    pq.offer(new int[]{newEffort,nr,nc});
                }
            }
        }
    }
    return 0;
}
```

---

### Problem 8 — Swim in Rising Water
**LeetCode #778 | Difficulty: Hard | Company: Google | Algorithm: Dijkstra / Binary Search + BFS**

> Minimize the maximum elevation seen along any path from (0,0) to (n-1,n-1).

#### Java code

```java
public int swimInWater(int[][] grid) {
    int n = grid.length;
    int[] dr = {0,0,1,-1}, dc = {1,-1,0,0};
    int[][] dist = new int[n][n];
    for (int[] row : dist) Arrays.fill(row, Integer.MAX_VALUE);
    dist[0][0] = grid[0][0];
    PriorityQueue<int[]> pq = new PriorityQueue<>((a,b)->a[0]-b[0]);
    pq.offer(new int[]{grid[0][0], 0, 0});
    while (!pq.isEmpty()) {
        int[] cur = pq.poll();
        int t=cur[0], r=cur[1], c=cur[2];
        if (r==n-1&&c==n-1) return t;
        if (t > dist[r][c]) continue;
        for (int d=0; d<4; d++) {
            int nr=r+dr[d], nc=c+dc[d];
            if (nr>=0&&nr<n&&nc>=0&&nc<n) {
                int newT = Math.max(t, grid[nr][nc]);
                if (newT < dist[nr][nc]) { dist[nr][nc]=newT; pq.offer(new int[]{newT,nr,nc}); }
            }
        }
    }
    return -1;
}
```

---

### Problem 9 — Minimum Moves to Move Box to Target
**LeetCode #1263 | Difficulty: Hard | Company: Google | Algorithm: BFS (state = box+player pos)**

> State = (boxRow, boxCol, playerRow, playerCol). BFS on states. Player must be able to reach push position (inner BFS).

#### Java code

```java
public int minPushBox(char[][] grid) {
    int rows=grid.length, cols=grid[0].length;
    int[] dr={0,0,1,-1}, dc={1,-1,0,0};
    int[] box=new int[2], player=new int[2], target=new int[2];
    for (int r=0;r<rows;r++) for (int c=0;c<cols;c++) {
        if(grid[r][c]=='B'){box[0]=r;box[1]=c;}
        if(grid[r][c]=='S'){player[0]=r;player[1]=c;}
        if(grid[r][c]=='T'){target[0]=r;target[1]=c;}
    }
    // BFS on {boxR,boxC,playerR,playerC}
    boolean[][][][] visited = new boolean[rows][cols][rows][cols];
    Queue<int[]> q=new LinkedList<>();
    q.offer(new int[]{box[0],box[1],player[0],player[1],0});
    visited[box[0]][box[1]][player[0]][player[1]]=true;
    while(!q.isEmpty()){
        int[]cur=q.poll();
        int br=cur[0],bc=cur[1],pr=cur[2],pc=cur[3],pushes=cur[4];
        if(br==target[0]&&bc==target[1]) return pushes;
        for(int d=0;d<4;d++){
            int nbr=br+dr[d], nbc=bc+dc[d];  // new box pos
            int needR=br-dr[d], needC=bc-dc[d];  // player must be here to push
            if(nbr<0||nbr>=rows||nbc<0||nbc>=cols||grid[nbr][nbc]=='#') continue;
            if(visited[nbr][nbc][br][bc]) continue;
            // Check if player can reach (needR,needC) without going through box
            if(canReach(grid,pr,pc,needR,needC,br,bc,rows,cols)){
                visited[nbr][nbc][br][bc]=true;
                q.offer(new int[]{nbr,nbc,br,bc,pushes+1});
            }
        }
    }
    return -1;
}
private boolean canReach(char[][]grid,int sr,int sc,int er,int ec,int br,int bc,int rows,int cols){
    if(sr==er&&sc==ec) return true;
    boolean[][]vis=new boolean[rows][cols];
    vis[sr][sc]=true; vis[br][bc]=true;
    int[]dr={0,0,1,-1},dc={1,-1,0,0};
    Queue<int[]>q=new LinkedList<>(); q.offer(new int[]{sr,sc});
    while(!q.isEmpty()){
        int[]cur=q.poll();
        for(int d=0;d<4;d++){
            int nr=cur[0]+dr[d],nc=cur[1]+dc[d];
            if(nr<0||nr>=rows||nc<0||nc>=cols||vis[nr][nc]||grid[nr][nc]=='#') continue;
            if(nr==er&&nc==ec) return true;
            vis[nr][nc]=true; q.offer(new int[]{nr,nc});
        }
    }
    return false;
}
```

---

### Problem 10 — Find Eventual Safe States
**LeetCode #802 | Difficulty: Medium | Company: Google | Algorithm: DFS coloring / Reverse Topo Sort**

> A node is safe if all paths from it lead to a terminal node (no cycle).

#### Java code

```java
public List<Integer> eventualSafeNodes(int[][] graph) {
    int n = graph.length;
    int[] color = new int[n];  // 0=unvisited, 1=in-path(unsafe), 2=safe
    List<Integer> result = new ArrayList<>();
    for (int i=0;i<n;i++) if (dfs(graph,color,i)) result.add(i);
    return result;
}
private boolean dfs(int[][] graph, int[] color, int node) {
    if (color[node] == 2) return true;
    if (color[node] == 1) return false;
    color[node] = 1;
    for (int next : graph[node])
        if (!dfs(graph,color,next)) return false;
    color[node] = 2;
    return true;
}
```

---

### Problem 11 — All Paths Source to Target
**LeetCode #797 | Difficulty: Medium | Company: Google | Algorithm: DFS backtracking**

#### Java code

```java
public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
    List<List<Integer>> result = new ArrayList<>();
    dfs(graph, 0, new ArrayList<>(Arrays.asList(0)), result);
    return result;
}
private void dfs(int[][] graph, int node, List<Integer> path, List<List<Integer>> result) {
    if (node == graph.length-1) { result.add(new ArrayList<>(path)); return; }
    for (int next : graph[node]) {
        path.add(next);
        dfs(graph, next, path, result);
        path.remove(path.size()-1);
    }
}
```

---

### Problem 12 — Longest Increasing Path in a Matrix
**LeetCode #329 | Difficulty: Hard | Company: Google, Amazon | Algorithm: DFS + Memoization**

#### Java code

```java
int[] dr = {0,0,1,-1}, dc = {1,-1,0,0};
public int longestIncreasingPath(int[][] matrix) {
    int rows=matrix.length, cols=matrix[0].length, max=0;
    int[][] memo = new int[rows][cols];
    for (int r=0;r<rows;r++)
        for (int c=0;c<cols;c++)
            max = Math.max(max, dfs(matrix,memo,r,c,rows,cols));
    return max;
}
private int dfs(int[][]matrix, int[][]memo, int r, int c, int rows, int cols) {
    if (memo[r][c] != 0) return memo[r][c];
    memo[r][c] = 1;
    for (int d=0;d<4;d++) {
        int nr=r+dr[d], nc=c+dc[d];
        if (nr>=0&&nr<rows&&nc>=0&&nc<cols&&matrix[nr][nc]>matrix[r][c])
            memo[r][c] = Math.max(memo[r][c], 1+dfs(matrix,memo,nr,nc,rows,cols));
    }
    return memo[r][c];
}
```

---

### Problem 13 — Longest Path in a DAG
**GFG | Difficulty: Medium | Algorithm: Topological Sort + DP**

> Longest path from any source to any sink in a DAG.

#### Java code

```java
public int longestPath(int n, int[][] edges) {
    List<List<Integer>> adj = new ArrayList<>();
    for (int i=0;i<n;i++) adj.add(new ArrayList<>());
    int[] indegree = new int[n];
    for (int[] e : edges) { adj.get(e[0]).add(e[1]); indegree[e[1]]++; }

    Queue<Integer> q = new LinkedList<>();
    int[] dp = new int[n];
    for (int i=0;i<n;i++) if (indegree[i]==0) { q.offer(i); dp[i]=1; }

    while (!q.isEmpty()) {
        int u = q.poll();
        for (int v : adj.get(u)) {
            dp[v] = Math.max(dp[v], dp[u]+1);
            if (--indegree[v]==0) q.offer(v);
        }
    }
    int max=0; for (int d:dp) max=Math.max(max,d);
    return max;
}
```

---

## Category 2 — Shortest Path

---

### Problem 14 — Network Delay Time
**LeetCode #743 | Difficulty: Medium | Company: Amazon, Google | Algorithm: Dijkstra**

> Signal sent from node `k`. Find time for ALL nodes to receive signal (max of shortest paths).

#### Java code

```java
public int networkDelayTime(int[][] times, int n, int k) {
    List<int[]>[] adj = new List[n+1];
    for (int i=1;i<=n;i++) adj[i]=new ArrayList<>();
    for (int[] t:times) adj[t[0]].add(new int[]{t[1],t[2]});

    int[] dist = new int[n+1];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[k] = 0;
    PriorityQueue<int[]> pq = new PriorityQueue<>((a,b)->a[0]-b[0]);
    pq.offer(new int[]{0,k});

    while (!pq.isEmpty()) {
        int[] cur=pq.poll();
        if (cur[0]>dist[cur[1]]) continue;
        for (int[] next:adj[cur[1]])
            if (dist[cur[1]]+next[1]<dist[next[0]]) {
                dist[next[0]]=dist[cur[1]]+next[1];
                pq.offer(new int[]{dist[next[0]],next[0]});
            }
    }
    int max=0;
    for (int i=1;i<=n;i++) { if (dist[i]==Integer.MAX_VALUE) return -1; max=Math.max(max,dist[i]); }
    return max;
}
```

---

### Problem 15 — Cheapest Flights Within K Stops
**LeetCode #787 | Difficulty: Medium | Company: Amazon, Google | Algorithm: Bellman-Ford with K limit**

> Shortest path with at most K edges. Use Bellman-Ford (relax exactly K+1 times).

#### Java code

```java
public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
    int[] dist = new int[n];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[src] = 0;

    for (int i=0; i<=k; i++) {          // relax k+1 times (k stops = k+1 edges)
        int[] temp = Arrays.copyOf(dist, n);
        for (int[] f : flights) {
            int u=f[0], v=f[1], w=f[2];
            if (dist[u]!=Integer.MAX_VALUE && dist[u]+w<temp[v])
                temp[v]=dist[u]+w;
        }
        dist = temp;
    }
    return dist[dst]==Integer.MAX_VALUE ? -1 : dist[dst];
}
```

#### Example

```
flights = [[0,1,100],[1,2,100],[0,2,500]], src=0, dst=2, k=1
dist after relax 0: [0, 100, 500]
dist after relax 1: [0, 100, 200]  → [0,1,2] costs 200 ✓
```

---

### Problem 16 — Path with Maximum Probability
**LeetCode #1514 | Difficulty: Medium | Company: Google | Algorithm: Dijkstra (maximize)**

> Maximize probability. Use max-heap, multiply probabilities.

#### Java code

```java
public double maxProbability(int n, int[][] edges, double[] succProb, int start, int end) {
    List<double[]>[] adj = new List[n];
    for (int i=0;i<n;i++) adj[i]=new ArrayList<>();
    for (int i=0;i<edges.length;i++) {
        adj[edges[i][0]].add(new double[]{edges[i][1], succProb[i]});
        adj[edges[i][1]].add(new double[]{edges[i][0], succProb[i]});
    }
    double[] prob = new double[n];
    prob[start] = 1.0;
    PriorityQueue<double[]> pq = new PriorityQueue<>((a,b)->Double.compare(b[0],a[0])); // max heap
    pq.offer(new double[]{1.0, start});
    while (!pq.isEmpty()) {
        double[] cur=pq.poll();
        int u=(int)cur[1]; double p=cur[0];
        if (u==end) return p;
        if (p<prob[u]) continue;
        for (double[] next:adj[u]) {
            int v=(int)next[0]; double np=p*next[1];
            if (np>prob[v]) { prob[v]=np; pq.offer(new double[]{np,v}); }
        }
    }
    return 0.0;
}
```

---

### Problem 17 — Minimum Cost to Reach Destination
**LeetCode #787 variant / GFG | Algorithm: Dijkstra**

> Same as Network Delay Time but find cost to single destination.

```java
// Use Dijkstra template — return dist[destination] once popped from PQ
if (u == dst) return d;   // early termination
```

---

### Problem 18 — Find the City with Smallest Neighbours
**LeetCode #1334 | Difficulty: Medium | Company: Google | Algorithm: Floyd-Warshall**

#### Java code

```java
public int findTheCity(int n, int[][] edges, int distanceThreshold) {
    int[][] dp = new int[n][n];
    for (int[] row:dp) Arrays.fill(row, Integer.MAX_VALUE/2);
    for (int i=0;i<n;i++) dp[i][i]=0;
    for (int[] e:edges) { dp[e[0]][e[1]]=e[2]; dp[e[1]][e[0]]=e[2]; }

    for (int k=0;k<n;k++)
        for (int i=0;i<n;i++)
            for (int j=0;j<n;j++)
                dp[i][j]=Math.min(dp[i][j], dp[i][k]+dp[k][j]);

    int result=-1, minCount=n+1;
    for (int i=0;i<n;i++) {
        int count=0;
        for (int j=0;j<n;j++) if (i!=j && dp[i][j]<=distanceThreshold) count++;
        if (count<=minCount) { minCount=count; result=i; }  // prefer higher index on tie
    }
    return result;
}
```

---

### Problem 19 — Min Cost (Dijkstra on grid)
**LeetCode #1368 / GFG | Algorithm: 0-1 BFS or Dijkstra**

> Min cost to make all cells point to destination. Moving along arrow = cost 0, changing = cost 1.

```java
// Use Dijkstra with cost 0 (follow arrow) or 1 (change arrow)
// Add to front of deque (0-1 BFS) for cost 0, back for cost 1
```

---

### Problem 20 — Minimum Cost to Reach Destination in Time
**LeetCode #1928 | Difficulty: Hard | Algorithm: Dijkstra with time constraint**

```java
// State = {cost, time, node}
// dist[node][time] = min cost to reach node in exactly `time` minutes
```

---

### Problem 21 — Minimum Obstacle Removal to Reach Corner
**LeetCode #2290 | Difficulty: Hard | Algorithm: 0-1 BFS**

> Moving to empty cell = cost 0, moving to obstacle = cost 1. Use deque (0-1 BFS).

```java
public int minimumObstacles(int[][] grid) {
    int rows=grid.length, cols=grid[0].length;
    int[][] dist = new int[rows][cols];
    for (int[] row:dist) Arrays.fill(row, Integer.MAX_VALUE);
    dist[0][0]=0;
    Deque<int[]> dq = new ArrayDeque<>();
    dq.addFirst(new int[]{0,0,0});
    int[] dr={0,0,1,-1}, dc={1,-1,0,0};
    while (!dq.isEmpty()) {
        int[] cur=dq.pollFirst();
        int d=cur[0],r=cur[1],c=cur[2];
        if (d>dist[r][c]) continue;
        for (int i=0;i<4;i++) {
            int nr=r+dr[i],nc=c+dc[i];
            if (nr>=0&&nr<rows&&nc>=0&&nc<cols) {
                int nd=d+grid[nr][nc];
                if (nd<dist[nr][nc]) {
                    dist[nr][nc]=nd;
                    if (grid[nr][nc]==0) dq.addFirst(new int[]{nd,nr,nc});
                    else dq.addLast(new int[]{nd,nr,nc});
                }
            }
        }
    }
    return dist[rows-1][cols-1];
}
```

---

## Category 3 — Topological Sort

---

### Problem 22 — Course Schedule
**LeetCode #207 | Difficulty: Medium | Company: Amazon, Google | Algorithm: Topo Sort (cycle detection)**

#### Java code

```java
public boolean canFinish(int numCourses, int[][] prerequisites) {
    List<List<Integer>> adj = new ArrayList<>();
    int[] indegree = new int[numCourses];
    for (int i=0;i<numCourses;i++) adj.add(new ArrayList<>());
    for (int[] p:prerequisites) { adj.get(p[1]).add(p[0]); indegree[p[0]]++; }

    Queue<Integer> q = new LinkedList<>();
    for (int i=0;i<numCourses;i++) if (indegree[i]==0) q.offer(i);
    int count=0;
    while (!q.isEmpty()) {
        int u=q.poll(); count++;
        for (int v:adj.get(u)) if (--indegree[v]==0) q.offer(v);
    }
    return count==numCourses;  // all processed = no cycle
}
```

---

### Problem 23 — Course Schedule II
**LeetCode #210 | Difficulty: Medium | Company: Amazon | Algorithm: Topo Sort (return order)**

```java
public int[] findOrder(int numCourses, int[][] prerequisites) {
    // Same as P22 but collect order[] instead of count
    int[] order = new int[numCourses]; int idx=0;
    // ... (Kahn's BFS, add to order[idx++] on poll)
    return idx==numCourses ? order : new int[0];
}
```

---

### Problem 24 — Course Schedule IV
**LeetCode #1462 | Difficulty: Medium | Algorithm: Topo Sort + reachability**

> After topo order, build reachability matrix: if u→v directly OR u→k→v.

```java
// For each node in topo order, propagate reachability to all ancestors
boolean[][] reach = new boolean[n][n];
// process in topo order, for each edge u→v: reach[u] |= reach[v], reach[u][v]=true
```

---

### Problem 25 — Alien Dictionary
**LeetCode #269 | Difficulty: Hard | Company: Google, Facebook | Algorithm: Topo Sort on character order**

> Compare adjacent words to extract character ordering. Build graph, topo sort.

#### Java code

```java
public String alienOrder(String[] words) {
    Map<Character,Set<Character>> adj = new HashMap<>();
    Map<Character,Integer> indegree = new HashMap<>();
    for (String w:words) for (char c:w.toCharArray()) { adj.putIfAbsent(c,new HashSet<>()); indegree.putIfAbsent(c,0); }

    for (int i=0;i<words.length-1;i++) {
        String w1=words[i], w2=words[i+1];
        if (w1.length()>w2.length()&&w1.startsWith(w2)) return ""; // invalid
        for (int j=0;j<Math.min(w1.length(),w2.length());j++) {
            if (w1.charAt(j)!=w2.charAt(j)) {
                if (!adj.get(w1.charAt(j)).contains(w2.charAt(j))) {
                    adj.get(w1.charAt(j)).add(w2.charAt(j));
                    indegree.put(w2.charAt(j), indegree.get(w2.charAt(j))+1);
                }
                break;
            }
        }
    }
    Queue<Character> q=new LinkedList<>();
    for (char c:indegree.keySet()) if (indegree.get(c)==0) q.offer(c);
    StringBuilder sb=new StringBuilder();
    while (!q.isEmpty()) {
        char u=q.poll(); sb.append(u);
        for (char v:adj.get(u)) if (indegree.merge(v,-1,Integer::sum)==0) q.offer(v);
    }
    return sb.length()==indegree.size() ? sb.toString() : "";
}
```

---

### Problem 26 — Sequence Reconstruction
**LeetCode #444 | Difficulty: Medium | Algorithm: Topo Sort (unique order check)**

> Check if `org` is the ONLY shortest supersequence of all seqs.

```java
// Build graph from seqs. Topo sort — at each step exactly ONE node should have indegree 0.
// If >1 node has indegree 0 → not unique.
```

---

### Problem 27 — Strange Printer II
**LeetCode #1591 | Difficulty: Hard | Algorithm: Topo Sort on color dependencies**

> Color u must be printed before color v if v's rectangle is inside u's range.

```java
// Build directed graph: if color A's range contains color B → A before B
// Cycle = impossible
```

---

## Category 4 — Union Find

---

### Problem 28 — Redundant Connection
**LeetCode #684 | Difficulty: Medium | Company: Amazon | Algorithm: Union Find**

#### Java code

```java
public int[] findRedundantConnection(int[][] edges) {
    int n = edges.length;
    UnionFind uf = new UnionFind(n+1);
    for (int[] e:edges)
        if (!uf.union(e[0],e[1])) return e;  // union returns false = already connected = redundant
    return new int[0];
}
```

---

### Problem 29 — Redundant Connection II
**LeetCode #685 | Difficulty: Hard | Company: Google | Algorithm: Union Find + in-degree**

> Directed graph. Find the edge that creates a cycle or gives a node 2 parents.

```java
// Case 1: a node has 2 parents → one of those 2 edges is redundant
// Case 2: cycle without double-parent → UF cycle detection
// Try removing candidate edge(s) and check if tree is valid
```

---

### Problem 30 — Accounts Merge
**LeetCode #721 | Difficulty: Medium | Company: Amazon, Google | Algorithm: Union Find**

> Merge accounts sharing an email. Union emails, group by root.

#### Java code

```java
public List<List<String>> accountsMerge(List<List<String>> accounts) {
    Map<String,String> parent = new HashMap<>();
    Map<String,String> owner = new HashMap<>();

    // Initialize
    for (List<String> acc:accounts)
        for (int i=1;i<acc.size();i++) { parent.put(acc.get(i),acc.get(i)); owner.put(acc.get(i),acc.get(0)); }

    // Union emails within same account
    for (List<String> acc:accounts)
        for (int i=2;i<acc.size();i++) union(parent, acc.get(1), acc.get(i));

    // Group by root
    Map<String,TreeSet<String>> groups = new HashMap<>();
    for (String email:parent.keySet()) groups.computeIfAbsent(find(parent,email), k->new TreeSet<>()).add(email);

    List<List<String>> result = new ArrayList<>();
    for (Map.Entry<String,TreeSet<String>> e:groups.entrySet()) {
        List<String> list=new ArrayList<>(); list.add(owner.get(e.getKey())); list.addAll(e.getValue()); result.add(list);
    }
    return result;
}
private String find(Map<String,String> parent, String x) {
    if (!parent.get(x).equals(x)) parent.put(x, find(parent,parent.get(x)));
    return parent.get(x);
}
private void union(Map<String,String> parent, String x, String y) {
    String px=find(parent,x), py=find(parent,y);
    if (!px.equals(py)) parent.put(px,py);
}
```

---

### Problem 31 — Number of Operations to Make Network Connected
**LeetCode #1319 | Difficulty: Medium | Algorithm: Union Find**

> Count extra cables (edges in same component). Need (components-1) moves.

```java
public int makeConnected(int n, int[][] connections) {
    if (connections.length < n-1) return -1;  // not enough cables
    UnionFind uf = new UnionFind(n);
    for (int[] c:connections) uf.union(c[0],c[1]);
    return uf.components-1;  // need to connect (components-1) pairs
}
```

---

### Problem 32 — Satisfiability of Equality Equations
**LeetCode #990 | Difficulty: Medium | Algorithm: Union Find**

> `a==b` → union a and b. `a!=b` → check find(a) != find(b).

```java
public boolean equationsPossible(String[] equations) {
    UnionFind uf = new UnionFind(26);
    for (String eq:equations) if (eq.charAt(1)=='=') uf.union(eq.charAt(0)-'a',eq.charAt(3)-'a');
    for (String eq:equations) if (eq.charAt(1)=='!') if (uf.connected(eq.charAt(0)-'a',eq.charAt(3)-'a')) return false;
    return true;
}
```

---

### Problem 33 — Min Cost to Connect All Points (Kruskal)
**LeetCode #1584 | Difficulty: Medium | Company: Google | Algorithm: Kruskal's MST**

#### Java code

```java
public int minCostConnectPoints(int[][] points) {
    int n = points.length;
    List<int[]> edges = new ArrayList<>();  // {cost, i, j}
    for (int i=0;i<n;i++)
        for (int j=i+1;j<n;j++)
            edges.add(new int[]{Math.abs(points[i][0]-points[j][0])+Math.abs(points[i][1]-points[j][1]),i,j});
    edges.sort((a,b)->a[0]-b[0]);
    UnionFind uf = new UnionFind(n);
    int cost=0, count=0;
    for (int[] e:edges) {
        if (uf.union(e[1],e[2])) { cost+=e[0]; if (++count==n-1) break; }
    }
    return cost;
}
```

---

### Problem 34 — Connecting Cities with Minimum Cost
**LeetCode #1135 | Difficulty: Medium | Algorithm: Kruskal's MST**

> Same as Min Cost Connect Points but edges given explicitly.

```java
// Sort edges by cost, union with UF, sum until n-1 edges added
```

---

### Problem 35 — Min Cost to Provide Water
**LeetCode #1168 | Difficulty: Hard | Algorithm: Kruskal + virtual node**

> Add a virtual node 0 connected to each house with well cost. Then MST.

```java
// Add virtual edges: (0, i, wells[i-1]) for each house i
// Then run Kruskal on all edges (pipes + virtual edges)
```

---

## Category 5 — Bipartite / Graph Coloring

---

### Problem 36 — Is Graph Bipartite?
**LeetCode #785 | Difficulty: Medium | Company: Amazon | Algorithm: BFS 2-coloring**

#### Java code

```java
public boolean isBipartite(int[][] graph) {
    int n = graph.length;
    int[] color = new int[n]; Arrays.fill(color,-1);
    for (int start=0;start<n;start++) {
        if (color[start]!=-1) continue;
        Queue<Integer> q=new LinkedList<>(); q.offer(start); color[start]=0;
        while (!q.isEmpty()) {
            int u=q.poll();
            for (int v:graph[u]) {
                if (color[v]==-1) { color[v]=1-color[u]; q.offer(v); }
                else if (color[v]==color[u]) return false;
            }
        }
    }
    return true;
}
```

---

### Problem 37 — Possible Bipartition
**LeetCode #886 | Difficulty: Medium | Company: Google | Algorithm: BFS 2-coloring**

> Same as bipartite — build adjacency list from dislikes, then 2-color.

---

### Problem 38 — Flower Planting With No Adjacent
**LeetCode #1042 | Difficulty: Easy | Algorithm: Greedy coloring (4 colors, max degree 3)**

> 4 colors available, each garden has ≤ 3 neighbors → always solvable. Assign any color not used by neighbors.

```java
public int[] gardenNoAdj(int n, int[][] paths) {
    List<Set<Integer>> adj = new ArrayList<>();
    for (int i=0;i<n;i++) adj.add(new HashSet<>());
    for (int[] p:paths) { adj.get(p[0]-1).add(p[1]-1); adj.get(p[1]-1).add(p[0]-1); }
    int[] color = new int[n];
    for (int i=0;i<n;i++) {
        Set<Integer> used = new HashSet<>();
        for (int nb:adj.get(i)) used.add(color[nb]);
        for (int c=1;c<=4;c++) if (!used.contains(c)) { color[i]=c; break; }
    }
    return color;
}
```

---

### Problem 39 — M-Coloring Problem
**GFG | Difficulty: Medium | Algorithm: Backtracking**

> Color graph with M colors such that no two adjacent vertices have same color.

```java
public boolean graphColoring(boolean[][] graph, int m, int n) {
    int[] color = new int[n];
    return solve(graph, m, color, 0, n);
}
private boolean solve(boolean[][] graph, int m, int[] color, int node, int n) {
    if (node==n) return true;
    for (int c=1;c<=m;c++) {
        if (isSafe(graph,color,node,c,n)) {
            color[node]=c;
            if (solve(graph,m,color,node+1,n)) return true;
            color[node]=0;
        }
    }
    return false;
}
private boolean isSafe(boolean[][] graph, int[] color, int node, int c, int n) {
    for (int i=0;i<n;i++) if (graph[node][i]&&color[i]==c) return false;
    return true;
}
```

---

### Problem 40 — Detect Cycle in Directed Graph
**GFG | Difficulty: Medium | Algorithm: DFS 3-color**

```java
// color: 0=white(unvisited), 1=gray(in stack), 2=black(done)
// back edge (gray→gray) = cycle
```

---

## Category 6 — MST

---

### Problem 41 — Minimum Spanning Tree (Kruskal)
**GFG | Difficulty: Medium | Algorithm: Kruskal**

> Classic MST — sort edges by weight, add if no cycle (Union Find).

```java
// Sort edges, iterate, union if different components
// Sum of n-1 edges = MST weight
```

---

### Problem 42 — Min Cost to Connect All Points (Prim's)
**LeetCode #1584 | Algorithm: Prim's MST**

```java
public int minCostConnectPoints(int[][] points) {
    int n=points.length; boolean[] inMST=new boolean[n];
    int[] minCost=new int[n]; Arrays.fill(minCost,Integer.MAX_VALUE);
    minCost[0]=0; int total=0;
    PriorityQueue<int[]> pq=new PriorityQueue<>((a,b)->a[0]-b[0]);
    pq.offer(new int[]{0,0});
    while (!pq.isEmpty()) {
        int[] cur=pq.poll(); int cost=cur[0], u=cur[1];
        if (inMST[u]) continue;
        inMST[u]=true; total+=cost;
        for (int v=0;v<n;v++) if (!inMST[v]) {
            int d=Math.abs(points[u][0]-points[v][0])+Math.abs(points[u][1]-points[v][1]);
            if (d<minCost[v]) { minCost[v]=d; pq.offer(new int[]{d,v}); }
        }
    }
    return total;
}
```

---

### Problem 43 — Minimum Cost to Connect Sticks
**LeetCode #1167 | Difficulty: Medium | Algorithm: Greedy + Min-Heap (Huffman)**

> Always merge 2 cheapest sticks. Use min-heap.

```java
public int connectSticks(int[] sticks) {
    PriorityQueue<Integer> pq = new PriorityQueue<>();
    for (int s:sticks) pq.offer(s);
    int cost=0;
    while (pq.size()>1) { int a=pq.poll(),b=pq.poll(); cost+=a+b; pq.offer(a+b); }
    return cost;
}
```

---

## Quick Pattern Reference

| Problem | Algorithm | Key insight |
|---------|-----------|-------------|
| Number of Islands | DFS | mark visited, count calls |
| Friend Circles | DFS/UF | components in adjacency matrix |
| Max Area | DFS | return 1+sum of neighbors |
| Surrounded Regions | DFS border | mark safe from border, flip rest |
| Shortest Path Binary Matrix | BFS | 8-directional, level=distance |
| Word Ladder | BFS | try all 1-letter changes |
| Path Min Effort | Dijkstra | minimize max difference |
| Swim in Water | Dijkstra | minimize max elevation |
| Network Delay Time | Dijkstra | max of all shortest paths |
| Cheapest Flights K Stops | Bellman-Ford | relax k+1 times with copy |
| Find City | Floyd-Warshall | all-pairs + count under threshold |
| Course Schedule | Topo Sort | cycle = can't finish |
| Course Schedule II | Topo Sort | return order if no cycle |
| Alien Dictionary | Topo Sort | build order from word comparisons |
| Redundant Connection | Union Find | union returns false = redundant |
| Accounts Merge | Union Find | union same-account emails |
| Min Cost Connect Points | Kruskal | sort Manhattan edges + UF |
| Is Bipartite | BFS 2-color | conflict = not bipartite |
| M-Coloring | Backtracking | try each color, backtrack on conflict |
