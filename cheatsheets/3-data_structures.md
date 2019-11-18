# Data Structures

## Summary

  * **Lists**
    - Linked-List
    - Skip-List
    - Stack (LIFO)
    - Queue (FIFO)
  * **[Heaps](#heap)**
    - Binary Heaps
    - Binomial Heaps
    - Fibonacci Heaps
    - Pairing Heaps
  * **[Symbol Tables](#symbol-table)**
    - Ordered:
      - [Binary Search Tree](#binary-search-tree)
      - AVL Binary Search Tree
      - Red-Black Binary Search Tree
      - B-Tree, B<sup>+</sup>-Tree, B<sup>\*</sup>-Tree
      - Trie Tree, Patricia Tree
    - Unordered:
      - [Hash Table](#hash-tables)
  * **[Spatial](#spatial-data-structures)**
    - Range Tree
    - Quadtree
    - k-d Tree
    - BSP Tree
    - Interval Tree
    - R-Tree, R<sup>+</sup>-Tree, R<sup>\*</sup>-Tree
  * **[Graphs](#graphs)**
    - Undirected Graph
    - Directed Graph
    - Weighted Graph


## Heap

  - Heaps are **tree-based** abstract data types for implementing priority queues.
  - Max Heap property, the keys of parent nodes are greater than or equal to keys of children and the highest key is in the root.
  - Min Heap property, the keys of parent nodes are less than or equal to keys of children and the lowest key is in the root.
  - A **binary heap** is a **complete binary tree** which can be represented using an array.
  - In binary heap, parent of node at `k` is at `k/2` and children of node at `k` are at `2k` and `2k+1`.
  - **Promotion** in binary heap: exchange key in child with key in parent until heap order is restored.
  - **Demotion** in binary heap: exchange key in parent with key in larger/smaller child until heap order is restored.

| Heap      | Insert           | Delete             |             |
|-----------|------------------|--------------------|-------------|
| Binary    | Θ(lgN)           | Θ(lgN)             |             |
| Binomial  | Θ(1)<sup>*</sup> | Θ(lgN)<sup>*</sup> | * amortized |
| Fibonacci | Θ(1)<sup>*</sup> | Θ(lgN)<sup>*</sup> | * amortized |
| Pairing   | Θ(1)<sup>*</sup> | Θ(lgN)<sup>*</sup> | * amortized |


## Symbol Table

  - Keys are **immutable** and **distinct** for symbol table.
  - **Key**  is
    - a **Comparable** type using `compareTo()` method for ordered symbol tables.
    - any generic type using `equals()` and `hashCode()` methods for unordered symbol tables.
  - **Value** is any generic type.

```java
// Unordered symbol tables
public interface ST<Key, Value> {
  void      insert(Key key, Value val);
  void      delete(Key key);
  Value     get(Key key);
  boolean   contains(Key key);
  boolean   isEmpty();
  int       size();
  Iterable  keys();
}

// Ordered symbol tables
public interface ST<Key, Value> {
  void      insert(Key key, Value value);
  void      delete(Key key);
  Value     get(Key key);
  boolean   contains(Key key);
  boolean   isEmpty();
  int       size();
  Key       min();
  Key       max();
  void      deleteMin();
  void      deleteMax();
  Key       floor(Key key);
  Key       ceiling(Key key);
  int       rank(Key key);
  Key       select(int rank);
  int       size(Key lo, key hi);
  Iterable  keys();
  Iterable  keys(Key lo, Key hi);
}
```


### Binary Search Tree

  - A BST is a binary tree in symmetric order, every node's key is
    - Largest than all keys in its left sub-tree.
    - Smaller than all keys in its right sub-tree.
  - Number of compares for search/insert in BST is equal to **1 + depth** of node.
  - The worst-case height of BST is **N**.
  - If **N** distinct keys are inserted into a BST in **random** order, the expected number of compares for a search/insert is **1.39lgN ~ 2lnN**.
  - The number of compares for deletion in BST is **N<sup>1/2</sup>**. If we allow deletion, the number of compares for search/insert in average case also degenerates to **N<sup>1/2</sup>**.


### Balanced Search Trees

  - **AVL** tree is a **self-balancing** binary search tree.
  - In an AVL tree, the heights of the two child sub-trees of any node differ by at most one.
  - Two rotation operations re-balance the tree in four cases:
    - **Left-Left:** a right rotation balances the tree.
    - **Right-Right:** a left rotation balances the tree.
    - **Left-Right:** a right rotation and then a left rotation balance the tree.
    - **Right-Left:** a left rotation and then a right rotation balance the tree.


  - **Red-Black** tree is a **self-balancing** binary search tree.
  - Each node in RB tree can be either Red or Black. A Red node is connected to its parent with a Red link.
  - In a left-leaning Red-Black tree:
    - Red nodes are always the left child of their parents (Red links lean left).
    - No Red node is connected to another Red node (No node has two Red links connected to it).
    - Every path from root to null links has the same number of Black nodes/links (perfect black balance).
  - Search in Red-Black tree is the same as for elementary BST (ignoring color).
  - Two rotation operations and one color operation re-balance the tree in two cases:
    - Case 1: inserting into a node with no Red link connected to it
      - Do standard BST insert, and color new node/link Red.
      - If new Red node/link is right leaning, do a **left rotation**.
    - Case 2: inserting into a node with a Red link connected to it
      - Do standard BST insert, and color new node/link Red.
      - Do a **left/right rotation** to balance the tree if needed.
      - Do a **color flip** to pass Red link up one level.
      - Do a **left/right rotation** to make lean left if needed.
      - Repeat case 1 or case 2 up the tree as needed.


  - **B-Tree** is a generalization of binary search trees.
  - B-trees are optimized for reading and writing large blocks of data. B-tree is a data structure for external memory.
  - In a B-tree of order **M**:
    - There are internal nodes and external nodes.
    - Each node can have at most **M-1** key-link pairs.
    - The root node has at least **2** key-link pairs, and all other nodes have at least **M/2** key-link pairs.
    - Internal nodes contain copies of keys to guide search, and external nodes are leaf nodes which contain keys and pointers to data.
  - The order of a B-tree, **M**, should be large enough so that a B-tree node can fit in a data block (page).
  - Search:
    - Start at root.
    - Find interval for search key and take corresponding links.
    - Search terminates in an external/leaf node.
  - Insertion:
    - Search for new key.
    - Insert at an external/leaf node.
    - Split nodes with **M** key-link pairs on the way up the tree.
  - A search or insertion in a B-tree of order **M** with **N** keys requires between **log<sub>M-1</sub><sup>N</sup>** and **log<sub>M/2</sub><sup>N</sup>** external accesses.
  - In B<sup>+</sup>-Tree, each external/leaf node has pointer to next external/leaf node for sequential access.

| Tree      | Search (worst) | Insert (worst) | Delete (worst) | Search (average) | Insert (average) | Delete (average) |
|-----------|----------------|----------------|----------------|------------------|------------------|------------------|
| BST       | N              | N              | N              | 1.39lgN          | 1.39lgN          | ?                |
| AVL       | 1.44lgN        | 1.44lgN*       | 1.44lgN*       | lgN              | lgN*             | lgN*             |
| Red-Black | 2lgN           | 2lgN           | 2lgN           | lgN*             | lgN*             | lgN*             |

  - AVL trees maintain a more rigid balance than red-black trees.
    Lookup in an AVL tree is typically faster, but this comes at the cost of slower insertion and deletion.


### Hash Tables

- Hash function is a function to map an arbitrary size data to a fixed-size number.
  - A hash function should be efficiently computable in a reasonable amount of time.
  - **Requirement:** if `k1 = k2`, then `hashCode(k1) = hashCode(k2)`
  - **Desirable:** if `k1 != k2`, then `hashCode(k1) != hashCode(k2)`
  - **Determinism:** for a given input value, a hash function must always generate the same hash value.
  - **Uniformity:** A hash function should map the expected inputs evenly over its output range (each hash value is equally likely for each key).
    - **Non-invertible:** In cryptographic applications, hash functions are expected to be practically non-invertible (one-way hash functions).
- Computing a hash value for user-defined types:
  - If the field is null, return 0
  - String: s[0]31<sup>L-1</sup> + s[1]31<sup>L-2</sup> + ... + s[L-2]31 + s[L-1]
  - Combine the hash value of each significant field: hash = 31 * hash + field_hash
  - If the field is an array, apply to each entry.
- If we have a table of size M, and the hash value is an int between -2<sup>31</sup> and 2<sup>31</sup> - 1
  - index = (key.hashCode() & 0x7fffffff) % M


- Hash table is a space-time trade-off.
- Hash function maps key to an integer `i` between `0` and `M-1`.
- **Separate Chaining**:
  - An array of M < N linked-lists (chains or buckets).
  - Insert: put at front of i<sup>th</sup> chain.
  - Search: need to search only i<sup>th</sup> chain.
  - Number of probes for search/insert is proportional to N/M. Typical choice for M is M ~ N/5.
- **Open Addressing**:
  - **Linear Probing**:
    - When a new key collides, find next empty slot, and put it there.
    - When a collision occurs at index H, the next indices are: H+1, H+2, H+3, ...
    - Array size M must be greater than number of key-value pairs N. Typical choice is α = N/M ~ 1/2.
    - Linear probing has a great spatial locality and, thus, better cache performance.
  - **Quadratic Probing**:
    - Quadratic probing better avoids the clustering problem that can occur with linear probing.
    - When a collision occurs at index H, the next indices are: H+1<sup>2</sup>, H+2<sup>2</sup>, H+3<sup>2</sup>, ...
  - **Double Hashing**:
    - Double hashing is similar to linear probing, but skips a variable amount each time using a second hash function.
    - Double hashing effectively eliminates clustering and can allow table to be become nearly full.
    - Given h<sub>1</sub> and h<sub>2</sub> hash functions, and a key k, the i+1 hash location is: h(i,k) = (h<sub>1</sub>(k) + i * h<sub>2</sub>(k)) mod M

| Collision Resolution | Search (worst) | Insert (worst) | Delete (worst) | Search (average) | Insert (average) | Delete (average) |
|----------------------|----------------|----------------|----------------|------------------|------------------|------------------|
| Separate Chaining    | lgN            | lgN            | lgN            | 3-5              | 3-5              | 3-5              |
| Linear Probing       | lgN            | lgN            | lgN            | 3-5              | 3-5              | 3-5              |


### Spatial Data Structures

  - **k-d Tree** is a space partitioning data structure for **k-dimensional points**. It allows range search, range count, and other queries.
  - The k-d tree is a **self-balancing** binary search tree in which:
    - Every node represents a k-dimensional point.
    - The 1st dimension is the key of node (root) in level 1, the 2nd dimension is the key of nodes in level 2, and so on (circular).
    - Every node divides the space into two half-spaces by a splitting hyperplane (every node is associated with one of the k-dimensions).
    - Points with i-dimension value less than i-dimension value of the hyperplane are represented by the left sub-tree.
    - Points with i-dimension value greater than i-dimension value of the hyperplane are represented by the right sub-tree.


  - **Interval Tree** is a data structure for holding intervals and finding overlapping ones.
  - Interval tree is implemented using a self-balancing binary search tree.
    - Each node contains left and right endpoints of an interval, and the left endpoint is the key of node.
    - Each node also stores the maximum endpoint in sub-tree rooted at node.
  - To search for any one interval that intersects query interval **(lo, hi)**:
    - If interval in node intersects query interval, return it.
    - Else if left sub-tree is null, go right.
    - Else if max endpoint in left sub-tree is less than lo, go right.
    - Else go left.


  - **R-Tree** is a balanced search tree for indexing spatial data optimized for external memory.
  - In an R-tree of order **M**:
    - Each node (except root) can contain a number of entries between a minimum fill **30%-40%** and **M**.
    - Each entry within a non-leaf node stores the pointer to a child node and the bounding box of all entries within the child node.
    - Leaf nodes store a point or bounding box representing the child and an external identifier for the child.
  - The order of an R-tree, **M**, should be large enough so that a node can fit in a data block (page).
  - In an R-tree, the average search time is **O(Mlog<sub>M</sub><sup>N</sup>)** and the worst-case insertion time is **O(N)**.
  - Coverage is the entire area to cover all related rectangles and Overlap is the entire area which is contained in two or more nodes.
  - **R<sup>+</sup>-Tree** avoids overlapping of internal nodes by inserting an object into multiple leaves if necessary.
  - **R<sup>*</sup>-Tree** attempts to minimize both coverage and overlap using a revised node split algorithm and forced reinsertion at node overflow.


## Graphs

  - **Graph**: set of vertices connected pairwise by edges.
  - **Digraph**: set of vertices connected pairwise by directed edges.
  - **Path**: sequence of vertices connected by edges.
  - **Cycle**: path whose first and last vertices are the same.
  - **DAG**: a directed graph which has no cycle.
  - **Connectivity**: Two vertices are connected if there is a path between them (equivalence relation: reflexive, symmetric, and transitive).
  - **Strong-Connectivity**: v and w are strongly-connected if there is a directed path from v to w and a directed path from w to v. (equivalence relation)
  - **Connected Component**: a maximal set of connected vertices.
  - **Strongly-Connected Component**: a maximal set of strongly-connected vertices.
  - **Connected Graph**: a graph in which every pair of vertices are connected.
  - **Biconnected Graph**: a connected graph that is not broken into disconnected parts by deleting any single vertex (and its incident edges).
  - **Cut**: a partition of graph vertices into two (non-empty) sets.
  - **Crossing Edge**: connects a vertex in one set with a vertex in the other.
  - **Euler Path**: a path in a graph which visits every edge exactly once.
  - **Hamilton Path**: a path in a graph that visits each vertex exactly once.
  - **Planar Graph**: a graph whose vertices and edges can be drawn in a plane such that no two edges intersect.
  - **Bipartite Graph**: a graph whose vertices can be divided into two disjoint sets U and V such that every edge connects a vertex in U to one in V.
  - **Isomorphic Graphs**: two graphs which contain the same number of vertices connected in the same way are said to be isomorphic.


### Implementation

  - Graphs and Digraphs are represented with adjacency-list:
    - An array of size `V` (the number of vertices)
    - Each entry `v` points to the collection of other vertices connected to the vertex `v`.
    - The needed space is proportional to `E + V`.

| Data Structure   | Space         | Add Edge | Check v-w adjacency | Check adjacent vertices |
|------------------|---------------|----------|---------------------|-------------------------|
| List of Edges    | E             | 1        | E                   | E                       |
| Adjacency Matrix | V<sup>2</sup> | 1        | 1                   | V                       |
| Adjacency List   | E + V         | 1        | degree(v)           | degree(v)               |
| Adjacency Set    | E + V         | logV     | logV                | logV + degree(v)        |


### Algorithms

#### DFS

  - **Depth-First Search** puts unvisited vertices on a stack.
  - DFS marks all vertices connected to `s` in time proportional to the sum of their degrees.

```java
public class DepthFirstSearch {
  private int count;
  private boolean[] marked;

  public void DFS(Graph G, int s) {
    marked = new boolean[G.V()];
    dfs(G, s);
  }

  private void dfs(Graph G, int v) {
    count++;
    marked[v] = true;
    for (int w : G.adj(v))
      if (!marked[w])
        dfs(G, w);
  }
}
```


#### BFS

  - **Breadth-First Search** puts unvisited vertices on queue.
  - BFS computes the shortest-paths from `s` to all other vertices in a graph in time proportional to `E + V`.
  - Multiple-source shortest paths: to find the shortest path from any vertex in a set of vertices to each other vertex,
    we can use BFS initialized by enqueueing all source vertices in the set.

```java
private void bfs(Graph G, int s) {
  Queue<Integer> q = new Queue<Integer>();
  q.enqueue(s);
  marked[s] = true;
  while (!q.isEmpty()) {
    int v = q.dequeue();
    for (int w : G.adj(v))
      if (!marked[w]) {
        q.enqueue(w);
        marked[w] = true;
      }
  }
}
```


####

  - Having pre-processed a graph, we can answer connectivity queries in constant time.

```java
private void connected_components(Graph G) {
  marked = new boolean[G.V()];
  id = new int[G.V()];
  for (int v = 0; v < G.V(); v++)
    if (!marked[v]) {
      dfs(G, v);
      comp++;
    }
}
```


  - A directed graph has a topological order if and only if no directed cycle exists.
  - The reverse DFS post-order of a DAG is a topological order.
  - Topological sort gives an order to redraw DAG so all edges point upwards/outwards.

```java
private void depth_first_order(Digraph G) {
  reversePost = new Stack<Integer>();
  marked = new boolean[G.V()];
  for (int v = 0; v < G.V(); v++)
    if (!marked[v])
      dfs(G, v);
}
```


  - **Strongly-connected components** in directed graph `G` are same as in the reverse of `GR`.
  - **Kosaraju-Sharir algorithm** computes the strongly-connected components of a digraph in time proportional to `E + V`.
    - Phase 1: run DFS on GR to compute reverse post-order.
    - Phase 2: run DFS on G, considering vertices in order given by first DFS.

```java
private void kosaraju_sharir_scc(Digraph G) {
  marked = new boolean[G.V()];
  id = new int[G.V()];
  depth_first_order(G.reverse());
  for (int v : reversePost())
    if (!marked[v]) {
      dfs(G, v);
      comp++;
    }
}
```


  - **Minimum Spanning Tree:** given an edge-weighted undirected graph `G` with positive edge weights, an MST of `G` is a sub-graph `T` that is:
    - Tree: connected and acyclic
    - Spanning: includes all of the vertices
    - Minimum: sum of the edge wights are minimum
  - Given any cut, the crossing edge of minimum weight is in the MST.
  - Greedy MST algorithm:
    - Start with all edges colored gray.
    - Find a cut with no black crossing edge, and color its minimum-weight edge black.
    - Repeat until `V - 1` edges are colored black.
  - **Kruskal algorithm** computes MST in time proportional to `ElgE`  in the worst case.
  - **Lazy Prim algorithm** computes MST in time proportional to `ElgE` and extra space proportional to `E` in the worst case.

```java
private void mst_kruskal(WeightedGraph G) {
  UnionFind uf = new UnionFind(G.V());
  MinPQ<Edge> pq = new MinPQ<Edge>();
  Queue<Edge> mst = new Queue<Edge>();
  for (Edge e : G.edges())
    pq.insert(e);
  while (!pq.isEmpty() && mst.size() < G.V() - 1) {
    Edge e = pq.delete();
    int v = e.either(), w = e.other(v);
    if (!uf.connected(v, w)) {  // edge v-w does not create cycle (lgV*)
      uf.union(v, w);           // merge sets (lgV*)
      mst.enqueue(e);           // add edge to mst
    }
  }
}

private void visit(WeightedGraph G, int v) {
  marked[v] = true;
  for (Edge e : G.adj(v))
    if (!marked[e.other(v)])
      pq.insert(e);
}

private void mst_prim_lazy(WeightedGraph G) {
  pq = new MinPQ<Edge>();
  mst = new Queue<Edge>();
  marked = new boolean[G.V()];
  visit(G, 0);  // assume G is connected
  while (!pq.isEmpty() && mst.size() < G.V() - 1) {
    Edge e = pq.delete();
    int v = e.either(), w = e.other(v);
    if (marked[v] && marked[w]) continue;   // ignore if both endpoints are in T
    mst.enqueue(e);                         // add edge e to tree
    if (!marked[v]) visit(G, v);
    if (!marked[w]) visit(G, w);
  }
}
```


  - **Shortest-Path Tree:** given an edge-weighted directed graph, the shortest path from `s` to every other vertex is a tree.
    - `edgeTo` : a vertex-indexed array in which `edgeTo[v]` is last edge on shortest path from `s` to `v`.
    - `distTo` : a vertex-indexed array in which `distTo[v]` is length of shortest path from `s` to `v`.
  - **Dijkstra algorithm** computes a SPT in any directed graph with non-negative edge weights in time proportional to `ElgV` (using binary heap).

```java
private void relax(DirectedEdge e) {
    int v = e.from(), w = e.to();
    if (distTo[w] > distTo[v] + e.weight()) {
        distTo[w] = distTo[v] + e.weight()
        edgeTo[w] = e;
        if (pq.contains(w))  pq.decreaseKey(w, distTo[w]);
        else                 pq.insert     (w, distTo[w]);
    }
}

public void spt_dijkstra(WeightedGraph G, int s) {
  edgeTo = new DirectedEdge[G.V()];
  distTo = new double[G.V()];
  pq = new IndexMinPQ<Double>(G.V());
  for (int v = 0; v < G.V(); v++)
    distTo[v] = Double.POSITIVE_INFINITY;
  distTo[s] = 0.0;
  pq.insert(s, 0.0);
  while (!pq.isEmpty()) {
    int v = pq.delete();
    for (DirectedEdge e : G.adj(v))
      relax(e);
  }
}
```
