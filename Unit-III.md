# Unit-III: Graph Algorithms

## 1. INTRODUCTION TO GRAPHS

### 1.1 Graph Representation

A **Graph G = (V, E)** consists of:

- **V**: Set of vertices (nodes)
- **E**: Set of edges connecting vertices

**Types of Graphs:**

- **Directed Graph (Digraph)**: Edges have direction
- **Undirected Graph**: Edges have no direction
- **Weighted Graph**: Edges have associated weights/costs
- **Unweighted Graph**: All edges have same weight (usually 1)

### 1.2 Graph Representation Methods

#### 1.2.1 Adjacency Matrix

**Definition**: 2D array where A[i][j] = 1 if edge exists from vertex i to j, 0 otherwise.

**For Weighted Graphs**: A[i][j] = weight of edge from i to j, ∞ if no edge.

**Properties:**

- **Space Complexity**: O(V²)
- **Edge Lookup**: O(1)
- **Add/Remove Edge**: O(1)
- **Add/Remove Vertex**: O(V²)

**Example:**

```
Vertices: {0, 1, 2}
Edges: {(0,1), (1,2), (2,0)}

Adjacency Matrix:
    0  1  2
0 [ 0  1  0 ]
1 [ 0  0  1 ]
2 [ 1  0  0 ]
```

#### 1.2.2 Adjacency List

**Definition**: Array of lists where each vertex has a list of its adjacent vertices.

**Properties:**

- **Space Complexity**: O(V + E)
- **Edge Lookup**: O(degree of vertex)
- **Add Edge**: O(1)
- **Remove Edge**: O(degree of vertex)

**Example:**

```
Adjacency List:
0 → [1]
1 → [2]
2 → [0]
```

**Comparison:**

|Operation  |Adjacency Matrix|Adjacency List|
|-----------|----------------|--------------|
|Space      |O(V²)           |O(V + E)      |
|Add Edge   |O(1)            |O(1)          |
|Remove Edge|O(1)            |O(V)          |
|Check Edge |O(1)            |O(V)          |
|Traverse   |O(V²)           |O(V + E)      |

-----

## 2. GRAPH TRAVERSAL ALGORITHMS

### 2.1 Breadth-First Search (BFS)

**Concept**: Explore graph level by level using a queue.

**Algorithm:**

```
BFS(G, s) // G = graph, s = source vertex
1. Create queue Q
2. Mark s as visited and enqueue s
3. while Q is not empty do
4.    v = dequeue(Q)
5.    process vertex v
6.    for each adjacent vertex u of v do
7.       if u is not visited then
8.          mark u as visited
9.          enqueue u
```

**Detailed Implementation:**

```
BFS(G, s)
1. Initialize visited[1...V] = false
2. Initialize queue Q
3. visited[s] = true
4. enqueue(Q, s)
5. while Q ≠ ∅ do
6.    v = dequeue(Q)
7.    print v
8.    for each u ∈ Adj[v] do
9.       if visited[u] = false then
10.         visited[u] = true
11.         enqueue(Q, u)
```

**Analysis:**

- **Time Complexity**: O(V + E)
- **Space Complexity**: O(V) for queue and visited array
- **Applications**: Shortest path in unweighted graphs, level-order traversal

**Properties:**

- Visits vertices in order of their distance from source
- Finds shortest path in unweighted graphs
- Can detect bipartiteness of graph

**BFS Tree**: Tree formed by BFS edges (edges used to discover new vertices)

### 2.2 Depth-First Search (DFS)

**Concept**: Explore graph by going as deep as possible before backtracking using recursion or stack.

**Recursive Algorithm:**

```
DFS(G, v)
1. mark v as visited
2. process vertex v
3. for each adjacent vertex u of v do
4.    if u is not visited then
5.       DFS(G, u)
```

**Iterative Algorithm:**

```
DFS_Iterative(G, s)
1. Initialize stack S
2. push s onto S
3. while S is not empty do
4.    v = pop(S)
5.    if v is not visited then
6.       mark v as visited
7.       process v
8.       for each adjacent vertex u of v do
9.          if u is not visited then
10.            push u onto S
```

**Analysis:**

- **Time Complexity**: O(V + E)
- **Space Complexity**: O(V) for recursion stack/explicit stack
- **Applications**: Topological sorting, detecting cycles, finding strongly connected components

**DFS Classification of Edges:**

1. **Tree Edges**: Edges in DFS tree (lead to new vertices)
1. **Back Edges**: Edges to ancestors (indicate cycles in undirected graphs)
1. **Forward Edges**: Edges to descendants (in directed graphs)
1. **Cross Edges**: Edges between different subtrees

### 2.3 Difference Between BFS and DFS

|Aspect          |BFS             |DFS              |
|----------------|----------------|-----------------|
|Data Structure  |Queue           |Stack/Recursion  |
|Memory Usage    |O(V)            |O(V)             |
|Shortest Path   |Yes (unweighted)|No               |
|Completeness    |Yes             |Yes              |
|Optimality      |Yes (unweighted)|No               |
|Space Complexity|Higher (queue)  |Lower (recursion)|

-----

## 3. TOPOLOGICAL SORTING

### 3.1 Concept

**Topological Sort**: Linear ordering of vertices in a directed acyclic graph (DAG) such that for every directed edge (u,v), vertex u comes before v in the ordering.

**Prerequisites**: Graph must be a DAG (no cycles)

### 3.2 Applications

- Course scheduling with prerequisites
- Build systems (compile dependencies)
- Task scheduling

### 3.3 Algorithms

#### 3.3.1 DFS-Based Topological Sort

**Algorithm:**

```
TopologicalSort(G)
1. Initialize stack S
2. Initialize visited[1...V] = false
3. for each vertex v ∈ V do
4.    if visited[v] = false then
5.       TopologicalSortUtil(G, v, visited, S)
6. while S is not empty do
7.    print pop(S)

TopologicalSortUtil(G, v, visited, S)
1. visited[v] = true
2. for each u ∈ Adj[v] do
3.    if visited[u] = false then
4.       TopologicalSortUtil(G, u, visited, S)
5. push v onto S
```

**Analysis:**

- **Time Complexity**: O(V + E)
- **Space Complexity**: O(V)

#### 3.3.2 Kahn’s Algorithm (BFS-Based)

**Algorithm:**

```
KahnsTopologicalSort(G)
1. Calculate in-degree for all vertices
2. Initialize queue Q with all vertices having in-degree 0
3. Initialize count = 0
4. while Q is not empty do
5.    v = dequeue(Q)
6.    print v
7.    count = count + 1
8.    for each u ∈ Adj[v] do
9.       in-degree[u] = in-degree[u] - 1
10.       if in-degree[u] = 0 then
11.          enqueue(Q, u)
12. if count ≠ V then
13.    print "Graph has cycle"
```

**Analysis:**

- **Time Complexity**: O(V + E)
- **Space Complexity**: O(V)
- **Advantage**: Can detect cycles

-----

## 4. DATA STRUCTURES FOR DISJOINT SETS

### 4.1 Union-Find Data Structure

**Purpose**: Keep track of elements partitioned into disjoint sets.

**Operations:**

- **MakeSet(x)**: Create set containing only x
- **Find(x)**: Return representative of set containing x
- **Union(x, y)**: Merge sets containing x and y

### 4.2 Implementation Approaches

#### 4.2.1 Simple Array Implementation

```
MakeSet(x): parent[x] = x

Find(x):
1. if parent[x] ≠ x then
2.    return Find(parent[x])
3. return x

Union(x, y):
1. root_x = Find(x)
2. root_y = Find(y)
3. if root_x ≠ root_y then
4.    parent[root_y] = root_x
```

#### 4.2.2 Union by Rank

```
Union(x, y):
1. root_x = Find(x)
2. root_y = Find(y)
3. if root_x ≠ root_y then
4.    if rank[root_x] < rank[root_y] then
5.       parent[root_x] = root_y
6.    else if rank[root_x] > rank[root_y] then
7.       parent[root_y] = root_x
8.    else
9.       parent[root_y] = root_x
10.      rank[root_x] = rank[root_x] + 1
```

#### 4.2.3 Path Compression

```
Find(x):
1. if parent[x] ≠ x then
2.    parent[x] = Find(parent[x])  // Path compression
3. return parent[x]
```

**Analysis:**

- **Without optimization**: O(n) per operation
- **With Union by Rank**: O(log n) per operation
- **With Path Compression**: Nearly O(1) amortized
- **With both optimizations**: O(α(n)) where α is inverse Ackermann function

-----

## 5. CYCLE DETECTION

### 5.1 Cycle Detection in Undirected Graphs

#### 5.1.1 Using DFS

**Concept**: If we find a back edge during DFS, graph has cycle.

**Algorithm:**

```
HasCycleDFS(G)
1. Initialize visited[1...V] = false
2. for each vertex v ∈ V do
3.    if visited[v] = false then
4.       if HasCycleUtil(G, v, visited, -1) then
5.          return true
6. return false

HasCycleUtil(G, v, visited, parent)
1. visited[v] = true
2. for each u ∈ Adj[v] do
3.    if visited[u] = false then
4.       if HasCycleUtil(G, u, visited, v) then
5.          return true
6.    else if u ≠ parent then
7.       return true
8. return false
```

#### 5.1.2 Using Union-Find

**Algorithm:**

```
HasCycleUnionFind(G)
1. Initialize Union-Find structure
2. for each edge (u, v) ∈ E do
3.    if Find(u) = Find(v) then
4.       return true
5.    Union(u, v)
6. return false
```

### 5.2 Cycle Detection in Directed Graphs

**Algorithm using DFS:**

```
HasCycleDirected(G)
1. Initialize visited[1...V] = false
2. Initialize recStack[1...V] = false
3. for each vertex v ∈ V do
4.    if HasCycleDirectedUtil(G, v, visited, recStack) then
5.       return true
6. return false

HasCycleDirectedUtil(G, v, visited, recStack)
1. visited[v] = true
2. recStack[v] = true
3. for each u ∈ Adj[v] do
4.    if not visited[u] and HasCycleDirectedUtil(G, u, visited, recStack) then
5.       return true
6.    else if recStack[u] then
7.       return true
8. recStack[v] = false
9. return false
```

-----

## 6. STRONGLY CONNECTED COMPONENTS

### 6.1 Definition

**Strongly Connected Component (SCC)**: Maximal set of vertices such that there is a path from every vertex to every other vertex in the set.

### 6.2 Applications

- Social network analysis
- Deadlock detection
- Compiler optimization

### 6.3 Algorithms

#### 6.3.1 Kosaraju’s Algorithm

**Steps:**

1. Perform DFS on original graph and store vertices by finish time
1. Create transpose graph (reverse all edges)
1. Perform DFS on transpose graph in decreasing order of finish time

**Algorithm:**

```
KosarajuSCC(G)
1. Create empty stack S
2. Perform DFS on G and push vertices to S by finish time
3. Create transpose graph Gt
4. Mark all vertices as not visited
5. while S is not empty do
6.    v = pop(S)
7.    if v is not visited then
8.       DFS(Gt, v)  // This DFS gives one SCC
```

**Analysis:**

- **Time Complexity**: O(V + E)
- **Space Complexity**: O(V)

#### 6.3.2 Tarjan’s Algorithm

**Concept**: Single DFS with low-link values and stack.

**Key Ideas:**

- **Discovery Time**: When vertex is first visited
- **Low-link Value**: Lowest discovery time reachable from vertex
- **On Stack**: Whether vertex is currently on stack

**Algorithm:**

```
TarjanSCC(G)
1. Initialize time = 0, stack S
2. Initialize disc[], low[], onStack[] arrays
3. for each vertex v ∈ V do
4.    if disc[v] = -1 then
5.       TarjanSCCUtil(G, v)

TarjanSCCUtil(G, v)
1. disc[v] = low[v] = ++time
2. push v onto S, onStack[v] = true
3. for each u ∈ Adj[v] do
4.    if disc[u] = -1 then
5.       TarjanSCCUtil(G, u)
6.       low[v] = min(low[v], low[u])
7.    else if onStack[u] then
8.       low[v] = min(low[v], disc[u])
9. if low[v] = disc[v] then  // v is root of SCC
10.   repeat
11.      w = pop(S), onStack[w] = false
12.      print w
13.   until w = v
```

**Analysis:**

- **Time Complexity**: O(V + E)
- **Space Complexity**: O(V)
- **Advantage**: Single pass algorithm

-----

## 7. MINIMUM SPANNING TREES

### 7.1 Definition

**Spanning Tree**: Subgraph that connects all vertices with exactly V-1 edges and no cycles.

**Minimum Spanning Tree (MST)**: Spanning tree with minimum total edge weight.

**Properties:**

- Has exactly V-1 edges
- Connects all vertices
- No cycles
- May not be unique

### 7.2 Applications

- Network design (telecommunications, electrical, transportation)
- Cluster analysis
- Approximation algorithms

### 7.3 Kruskal’s Algorithm

**Concept**: Greedy algorithm that adds edges in increasing order of weight, avoiding cycles.

**Algorithm:**

```
KruskalMST(G)
1. Sort all edges in increasing order of weight
2. Initialize MST as empty set
3. Initialize Union-Find structure
4. for each edge (u, v) in sorted order do
5.    if Find(u) ≠ Find(v) then
6.       add edge (u, v) to MST
7.       Union(u, v)
8.       if |MST| = V - 1 then break
9. return MST
```

**Detailed Steps:**

```
KruskalMST(G = (V, E))
1. A = ∅  // MST edges
2. for each vertex v ∈ V do
3.    MakeSet(v)
4. Sort edges E by weight
5. for each edge (u, v) ∈ E in sorted order do
6.    if Find(u) ≠ Find(v) then
7.       A = A ∪ {(u, v)}
8.       Union(u, v)
9. return A
```

**Analysis:**

- **Time Complexity**: O(E log E) or O(E log V) - mainly for sorting
- **Space Complexity**: O(V) for Union-Find structure
- **Correctness**: Based on cut property of MSTs

### 7.4 Prim’s Algorithm

**Concept**: Greedy algorithm that grows MST one vertex at a time by adding minimum weight edge.

**Algorithm:**

```
PrimMST(G, r) // r is root vertex
1. Initialize key[v] = ∞ for all v ∈ V
2. key[r] = 0, parent[r] = NIL
3. Q = V  // Priority queue
4. while Q ≠ ∅ do
5.    u = ExtractMin(Q)
6.    for each v ∈ Adj[u] do
7.       if v ∈ Q and weight(u, v) < key[v] then
8.          parent[v] = u
9.          key[v] = weight(u, v)
```

**Using Adjacency Matrix:**

```
PrimMST(G)
1. Initialize key[V], parent[V], inMST[V]
2. key[0] = 0, parent[0] = -1
3. for i = 1 to V-1 do key[i] = ∞
4. for count = 0 to V-1 do
5.    u = minimum key vertex not in MST
6.    inMST[u] = true
7.    for v = 0 to V-1 do
8.       if G[u][v] ≠ 0 and not inMST[v] and G[u][v] < key[v] then
9.          parent[v] = u, key[v] = G[u][v]
```

**Analysis:**

- **Time Complexity**:
  - O(V²) with adjacency matrix
  - O(E log V) with binary heap
  - O(E + V log V) with Fibonacci heap
- **Space Complexity**: O(V)

### 7.5 Comparison: Kruskal vs Prim

|Aspect         |Kruskal’s    |Prim’s             |
|---------------|-------------|-------------------|
|Approach       |Edge-based   |Vertex-based       |
|Data Structure |Union-Find   |Priority Queue     |
|Time Complexity|O(E log E)   |O(V²) or O(E log V)|
|Best for       |Sparse graphs|Dense graphs       |
|Implementation |Simpler      |More complex       |

-----

## 8. SINGLE SOURCE SHORTEST PATH

### 8.1 Dijkstra’s Algorithm (Greedy Approach)

**Prerequisites**: Non-negative edge weights

**Concept**: Greedy algorithm that maintains shortest distances and updates them.

**Algorithm:**

```
Dijkstra(G, s) // s is source vertex
1. Initialize dist[v] = ∞ for all v ∈ V
2. dist[s] = 0
3. Q = V  // Priority queue
4. while Q ≠ ∅ do
5.    u = ExtractMin(Q)  // vertex with minimum distance
6.    for each v ∈ Adj[u] do
7.       if dist[u] + weight(u, v) < dist[v] then
8.          dist[v] = dist[u] + weight(u, v)
9.          parent[v] = u
```

**Detailed Implementation:**

```
Dijkstra(G, src)
1. Create distance array dist[] and initialize all distances as ∞
2. dist[src] = 0
3. Create boolean array visited[] and mark all vertices as not visited
4. for count = 0 to V-1 do
5.    u = minimum distance vertex from set of unvisited vertices
6.    visited[u] = true
7.    for each vertex v adjacent to u do
8.       if not visited[v] and dist[u] + weight(u,v) < dist[v] then
9.          dist[v] = dist[u] + weight(u,v)
```

**Analysis:**

- **Time Complexity**:
  - O(V²) with array implementation
  - O((V + E) log V) with binary heap
  - O(E + V log V) with Fibonacci heap
- **Space Complexity**: O(V)
- **Limitation**: Cannot handle negative weights

**Correctness**: Based on optimal substructure and greedy choice property.

### 8.2 Bellman-Ford Algorithm (Dynamic Programming)

**Advantages**: Can handle negative weights and detect negative cycles.

**Algorithm:**

```
BellmanFord(G, s)
1. Initialize dist[v] = ∞ for all v ∈ V
2. dist[s] = 0
3. for i = 1 to V-1 do
4.    for each edge (u, v) ∈ E do
5.       if dist[u] + weight(u, v) < dist[v] then
6.          dist[v] = dist[u] + weight(u, v)
7. // Check for negative cycles
8. for each edge (u, v) ∈ E do
9.    if dist[u] + weight(u, v) < dist[v] then
10.      return "Graph contains negative cycle"
11. return dist[]
```

**Analysis:**

- **Time Complexity**: O(VE)
- **Space Complexity**: O(V)
- **Applications**: Currency arbitrage, network routing protocols

**Key Insight**: After V-1 iterations, shortest paths are found. If distances can still be reduced, negative cycle exists.

-----

## 9. ALL PAIRS SHORTEST PATH

### 9.1 Floyd-Warshall Algorithm

**Concept**: Dynamic programming algorithm to find shortest paths between all pairs of vertices.

**Can handle**: Negative weights (but not negative cycles)

**Algorithm:**

```
FloydWarshall(G)
1. Initialize dist[i][j] for all pairs (i,j)
2. for i = 1 to V do
3.    for j = 1 to V do
4.       if i = j then dist[i][j] = 0
5.       else if edge (i,j) exists then dist[i][j] = weight(i,j)
6.       else dist[i][j] = ∞
7. for k = 1 to V do
8.    for i = 1 to V do
9.       for j = 1 to V do
10.         if dist[i][k] + dist[k][j] < dist[i][j] then
11.            dist[i][j] = dist[i][k] + dist[k][j]
```

**Analysis:**

- **Time Complexity**: O(V³)
- **Space Complexity**: O(V²)

**Applications:**

- Finding shortest paths in dense graphs
- Transitive closure
- Detecting negative cycles

**Optimization**: Can detect negative cycles by checking if dist[i][i] < 0 for any i.

-----

## EXAM PREPARATION GUIDE

### Expected Question Types:

1. **Graph Traversal**
- Implement BFS/DFS (4-5 marks)
- Trace execution on given graph (3-4 marks)
- Compare BFS vs DFS (2-3 marks)
1. **Shortest Path Algorithms**
- Dijkstra’s algorithm implementation (5-6 marks)
- Trace Dijkstra’s/Bellman-Ford on graph (3-4 marks)
- Floyd-Warshall for all pairs (4-5 marks)
1. **MST Algorithms**
- Kruskal’s vs Prim’s comparison (3-4 marks)
- Find MST using either algorithm (4-5 marks)
- Trace algorithm execution (3-4 marks)

### Key Points to Remember:

1. **Time Complexities**:
- BFS/DFS: O(V + E)
- Dijkstra: O(V²) or O(E log V)
- Bellman-Ford: O(VE)
- Floyd-Warshall: O(V³)
- Kruskal: O(E log E)
- Prim: O(V²) or O(E log V)
1. **When to Use Which Algorithm**:
- Dijkstra: Non-negative weights, single source
- Bellman-Ford: Negative weights possible, detect cycles
- Floyd-Warshall: All pairs shortest path
- Kruskal: Sparse graphs, MST
- Prim: Dense graphs, MST
1. **Data Structures**:
- BFS uses Queue
- DFS uses Stack/Recursion
- Dijkstra uses Priority Queue
- Kruskal uses Union-Find
- Prim uses Priority Queue

### Practice Problems:

1. Trace BFS and DFS on a given graph
1. Find shortest path using Dijkstra’s algorithm
1. Find MST using Kruskal’s and Prim’s algorithms
1. Detect cycles in directed and undirected graphs
1. Find strongly connected components
1. Apply Floyd-Warshall algorithm
1. Compare graph representation methods

### Common Exam Questions:

1. “Apply Dijkstra’s algorithm to find shortest path from vertex A to all other vertices.”
1. “Find the minimum spanning tree using Kruskal’s algorithm.”
1. “Compare BFS and DFS traversal methods with examples.”
1. “Detect if the given directed graph has a cycle.”
1. “Find all pairs shortest paths using Floyd-Warshall algorithm.”
