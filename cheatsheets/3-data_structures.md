# Data Structures

**References:**

  - Algorithms, 4th Edition (_Robert Sedgewick and Kevin Wayne_)

## Summary

  * [**Sets**](#sets)
    - [Bloom Filter](#bloom-filter)
  * [**Lists**](#lists)
    - Linked-List
    - Stack (LIFO)
    - Queue (FIFO)
    - [Skip-List](#skip-list)
  * [**Heaps**](#heap)
    - Binary Heaps
    - Binomial Heaps
    - Fibonacci Heaps
    - Pairing Heaps
  * [**Symbol Tables**](#symbol-table)
    - Ordered:
      - [Binary Search Tree](#binary-search-tree)
      - [AVL Binary Search Tree](#avl)
      - [Red-Black Binary Search Tree](#red-black)
      - [B-Tree, B<sup>+</sup>-Tree, B<sup>\*</sup>-Tree](#b-tree)
      - Splay Tree
      - Trie/Prefix Tree
      - Radix/Patricia Tree
    - Unordered:
      - [Hash Table](#hash-tables)
  * [**Spatial**](#spatial-data-structures)
    - [Range Tree](#range-tree)
    - [Segment Tree](#segment-tree)
    - [Interval Tree](#interval-tree)
    - [Quadtree](#quadtree)
    - [Octree](#octree)
    - [k-d Tree](#k-d-tree)
    - [R-Tree, R<sup>+</sup>-Tree, R<sup>\*</sup>-Tree](#r-tree)
  * [**Graphs**](#graphs)
    - Undirected Graph
    - Directed Graph
    - Weighted Graph


## Sets

### Bloom Filter

  - A Bloom filter is a space-efficient _probabilistic_ set data structure.
  - False positives are possible, but false negatives are not.
  - **Implementation:**
    - An empty Bloom filter is a _bit array_ of `m` bits, all set to `0`.
    - To add an element, `k` distinct hash functions each maps the element to a position in the array and all such positions are set to `1`.
    - To query an element, the same `k` hash functions each map the element to a position:
      - If any of those positions is set to `0`, the element does not exist in the set.
      - Otherwise if all those positions are set to `1`, the element may be or not be in the set.
  - For a bit array of `m` bits and `n` elements, the optimmum number of hash functions is `k = (m/n)ln2`.

## Lists

### Skip-List

  - A skip-list is a data structure that allows `O(logN)` search complexity as well as `O(logN)` insertion complexity.
  - **Implementation:**
    - A skip-list is built in layers.
    - The bottom layer is a regular linked-list.
    - Each higher layer is a _fast lane_ for the list below.

## Heaps

  - Heaps are **tree-based** abstract data types for implementing priority queues.
  - Max Heap property, the keys of parent nodes are greater than or equal to keys of children and the highest key is in the root.
  - Min Heap property, the keys of parent nodes are less than or equal to keys of children and the lowest key is in the root.
  - A **binary heap** is a **complete binary tree** which can be represented using an array.
  - In binary heap, parent of node at `k` is at `k/2` and children of node at `k` are at `2k` and `2k+1`.
  - **Promotion (Swim)** in binary heap: exchange key in child with key in parent until heap order is restored.
  - **Demotion (Sink)** in binary heap: exchange key in parent with key in larger/smaller child until heap order is restored.

| Heap      | Insert           | Delete             |             |
|-----------|------------------|--------------------|-------------|
| Binary    | Θ(lgN)           | Θ(lgN)             |             |
| Binomial  | Θ(1)<sup>*</sup> | Θ(lgN)<sup>*</sup> | * amortized |
| Fibonacci | Θ(1)<sup>*</sup> | Θ(lgN)<sup>*</sup> | * amortized |
| Pairing   | Θ(1)<sup>*</sup> | Θ(lgN)<sup>*</sup> | * amortized |


## Symbol Tables

  - Keys are **immutable** and **distinct** for symbol table.
  - **Key**  is
    - a **Comparable** type using `compareTo()` method for ordered symbol tables.
    - any generic type using `equals()` and `hash()` methods for unordered symbol tables.
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


### Summary

| Tree      | Search (worst) | Insert (worst) | Delete (worst) | Search (average) | Insert (average) | Delete (average) |
|-----------|----------------|----------------|----------------|------------------|------------------|------------------|
| BST       | N              | N              | N              | 1.39lgN          | 1.39lgN          | ?                |
| AVL       | 1.44lgN        | 1.44lgN*       | 1.44lgN*       | lgN              | lgN*             | lgN*             |
| Red-Black | 2lgN           | 2lgN           | 2lgN           | lgN*             | lgN*             | lgN*             |

  - AVL trees maintain a more rigid balance than red-black trees.
  - Lookup in an AVL tree is typically faster, but this comes at the cost of slower insertion and deletion.


### Binary Search Tree

  - A BST is a binary tree in symmetric order, every node's key is
    - Largest than all keys in its left sub-tree.
    - Smaller than all keys in its right sub-tree.
  - Number of compares for search/insert in BST is equal to **1 + depth** of node.
  - The worst-case height of BST is **N**.
  - If **N** distinct keys are inserted into a BST in **random** order, the expected number of compares for a search/insert is **1.39lgN ~ 2lnN**.
  - The number of compares for deletion in BST is **N<sup>1/2</sup>**. If we allow deletion, the number of compares for search/insert in average case also degenerates to **N<sup>1/2</sup>**.


### Balanced Search Trees

#### AVL

  - **AVL** tree is a **self-balancing** binary search tree.
  - In an AVL tree, the heights of the two child sub-trees of any node differ by at most one.
  - Two rotation operations re-balance the tree in four cases:
    - **Left-Left:** a right rotation balances the tree.
    - **Right-Right:** a left rotation balances the tree.
    - **Left-Right:** a right rotation and then a left rotation balance the tree.
    - **Right-Left:** a left rotation and then a right rotation balance the tree.

#### Red-Black

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

#### B-Tree

  - **B-Tree** is a **self-balancing** tree and generalization of binary search trees.
  - Search, insertion, and deletion are done in **logarithmic time**.
  - B-trees are optimized for reading and writing large blocks of data from and to **external storage systems**.
  - B-trees are commonly used in _databases_ and _file systems_ for indexing purposes.
  - In a B-tree of order `M`:
    - There are internal nodes and external nodes.
    - Each node can have at most `M-1` key-link pairs.
    - The root node has at least `2` key-link pairs, and all other nodes have at least `M/2` key-link pairs.
    - Internal nodes contain copies of keys to guide search, and external nodes are leaf nodes which contain keys and pointers to data.
  - The order of a B-tree, `M`, should be large enough so that a B-tree node can fit in a data block (page).
  - Search:
    - Start at root.
    - Find interval for search key and take corresponding links.
    - Search terminates in an external/leaf node.
  - Insertion:
    - Search for new key.
    - Insert at an external/leaf node.
    - Split nodes with `M` key-link pairs on the way up the tree.
  - A search or insertion in a B-tree of order `M` with `N` keys requires between **log<sub>M-1</sub><sup>N</sup>** and **log<sub>M/2</sub><sup>N</sup>** external accesses.
  - In B<sup>+</sup>-Tree, each external/leaf node has pointer to next external/leaf node for sequential access.


### Hash Tables

  - Hash table is a space-time trade-off.
  - Hash function maps key to an integer `i` between `0` and `M-1`.

#### Hash Function

Hash function is a function to map an arbitrary size data to a fixed-size number.

  - A hash function should be efficiently computable in a reasonable amount of time.
  - **Requirement:** if `k1 = k2`, then `hash(k1) = hash(k2)`
  - **Desirable:** if `k1 != k2`, then `hash(k1) != hash(k2)`
  - **Determinism:** for a given input value, a hash function must always generate the same hash value.
  - **Uniformity:** A hash function should map the expected inputs evenly over its output range (each hash value is equally likely for each key).
  - **Non-invertible:** In cryptographic applications, hash functions are expected to be practically non-invertible (one-way hash functions).

Computing a hash value for user-defined types:

  - If the field is null, return 0
  - **String**: s[0]31<sup>L-1</sup> + s[1]31<sup>L-2</sup> + ... + s[L-2]31 + s[L-1]
  - Combine the hash value of each significant field: hash = 31 * hash + field_hash
  - If the field is an array, apply to each entry.

If we have a table of size M, and the hash value is an int between -2<sup>31</sup> and 2<sup>31</sup> - 1, `i = (key.hash() & 0x7fffffff) % M`.

#### Hash Collision Resolutions:

  - **Separate Chaining**
    - An array of `M < N` linked-lists (chains or buckets).
    - Insert: put at front of i<sup>th</sup> chain.
    - Search: need to search only i<sup>th</sup> chain.
    - Number of probes for search/insert is proportional to `N/M`.
    - A typical choice for `M` is `M ~ N/5`.
  - **Open Addressing**
    - **Linear Probing**
      - When a new key collides, find the next empty slot, and put it there.
      - When a collision occurs at index h, the next indices are: h+1, h+2, h+3, ...
      - Array size (`M`) must be greater than number of key-value pairs (`N`).
      - A typical choice is `M ~ 2N` (load factor is `α = N/M ~ 1/2`).
      - Linear probing has a great spatial locality and, thus, better cache performance.
      - Using linear probing, long clusters are more likely to increase in length.
    - **Quadratic Probing**
      - When a collision occurs at index h, the next indices are: h+1<sup>2</sup>, h+2<sup>2</sup>, h+3<sup>2</sup>, ...
      - Quadratic probing better avoids the clustering problem that can occur with linear probing.
    - **Double Hashing**
      - Double hashing skips a variable amount each time using a second hash function.
      - Double hashing effectively eliminates clustering and can allow table to be become nearly full.
      - Given h<sub>1</sub> and h<sub>2</sub> hash functions, and a key k, the i+1 hash location is: h(i,k) = (h<sub>1</sub>(k) + i * h<sub>2</sub>(k)) mod M

| Collision Resolution | Search (worst) | Insert (worst) | Delete (worst) | Search (average) | Insert (average) | Delete (average) |
|----------------------|----------------|----------------|----------------|------------------|------------------|------------------|
| Separate Chaining    | lgN            | lgN            | lgN            | 3-5              | 3-5              | 3-5              |
| Linear Probing       | lgN            | lgN            | lgN            | 3-5              | 3-5              | 3-5              |


## Spatial Data Structures

### Range Tree

  - Range tree is a data structure for storing **points**.
  - It is optimized for querying and finding which points fall within a given interval.

### Segment Tree

  - Segment tree is a data structure for storing **intervals**.
  - It is optimized for querying and finding which intervals contain a given point.

### Interval Tree

  - Interval tree is a data structure for storing **intervals**.
  - It is optimized for querying and finding which intervals overlap with a given interval.
  - Interval tree is implemented using a self-balancing binary search tree (_AVL_, _Red-Black_, ...).
    - Each node contains left and right endpoints of an interval, and the left endpoint is the key of node.
    - Each node also stores the maximum endpoint in sub-tree rooted at node.
  - To search for any one interval that intersects query interval `(lo, hi)`:
    - If interval in node intersects query interval, return it.
    - Else if left sub-tree is null, go right.
    - Else if max endpoint in left sub-tree is less than `lo`, go right.
    - Else go left.

### Quadtree

  - Quadtree is a **space-partitioning** data structure for 2D spaces.
  - It partitions a 2D space by recursively subdividing it into four quadrants.

### Octree

  - Octree is a **space-partitioning** data structure for 3D spaces.
  - It partitions a 3D space by recursively subdividing it into eight octants.

### k-d Tree

  - k-d Tree is a **space-partitioning** data structure for k-dimensional space.
  - It allows range search, range count, and other queries.
  - The k-d tree is a **self-balancing** binary search tree in which:
    - Every node represents a k-dimensional point.
    - The 1st dimension is the key of node (root) in level 1, the 2nd dimension is the key of nodes in level 2, and so on.
    - Every node divides the space into two half-spaces by a splitting hyperplane (every node is associated with one of the k-dimensions).
    - Points with i-dimension value less than i-dimension value of the hyperplane are represented by the left sub-tree.
    - Points with i-dimension value greater than i-dimension value of the hyperplane are represented by the right sub-tree.

### R-Tree

  - R-Tree is a balanced search tree for indexing spatial data optimized for **external storage systems**.
  - In an R-tree of order `M`:
    - Each node (except root) can contain a number of entries between a minimum fill `30%-40%` and `M`.
    - Each entry within a non-leaf node stores the pointer to a child node and the bounding box of all entries within the child node.
    - Leaf nodes store a point or bounding box representing the child and an external identifier for the child.
  - The order of an R-tree, `M`, should be large enough so that a node can fit in a data block (page).
  - In an R-tree, the average search time is O(Mlog<sub>M</sub><sup>N</sup>) and the worst-case insertion time is O(N).
  - Coverage is the entire area to cover all related rectangles and Overlap is the entire area which is contained in two or more nodes.
  - **R<sup>+</sup>-Tree** avoids overlapping of internal nodes by inserting an object into multiple leaves if necessary.
  - **R<sup>*</sup>-Tree** attempts to minimize both coverage and overlap using a revised node split algorithm and forced reinsertion at node overflow.


## Graphs

  - **Graph**: a set of vertices connected pairwise by edges.
  - **Digraph**: a set of vertices connected pairwise by directed edges.
  - **Path**: a sequence of vertices connected by edges.
  - **Cycle**: a path whose first and last vertices are the same.
  - **DAG**: a directed graph which has no cycle.
  - **Connectivity**: Two vertices are connected if there is a path between them (equivalence relation: _reflexive_, _symmetric_, and _transitive_).
  - **Strong-Connectivity**: `v` and `w` are strongly-connected if there is a directed path from `v` to `w` and a directed path from `w` to `v`. (equivalence relation)
  - **Connected Component**: a maximal set of connected vertices.
  - **Strongly-Connected Component**: a maximal set of strongly-connected vertices.
  - **Connected Graph**: a graph in which every pair of vertices are connected.
  - **Biconnected Graph**: a connected graph that is not broken into disconnected parts by deleting any single vertex (and its incident edges).
  - **Cut**: a partition of graph vertices into two non-empty disjoint sets.
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
    - The needed space is proportional to `V+E`.

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
// Non-Recursive
private void dfs(Graph G, int s) {
  boolean[] visited = new boolean[G.V()];
  Stack<Integer> s = new Stack<Integer>();

  visited[s] = true;
  s.push(s);
  while (!s.isEmpty()) {
    int v = s.pop();
    for (int w : G.adj(v))
      if (!visited[w]) {
        visited[w] = true;
        s.push(w);
      }
  }
}
```

```java
public class DepthFirstSearch {
  private boolean[] visited;
  private int count;

  public void DepthFirstSearch(Graph G, int s) {
    visited = new boolean[G.V()];
    dfs(G, s);
  }

  // Recursive
  private void dfs(Graph G, int v) {
    visited[v] = true;
    count++;
    for (int w : G.adj(v))
      if (!visited[w])
        dfs(G, w);
  }
}
```

```java
public class DepthFirstPaths {
  private boolean[] visited;
  private int[] edgeTo;
  private int s;

  public DepthFirstPaths(Graph G, int s) {
    visited = new boolean[G.V()];
    edgeTo = new int[G.V()];
    this.s = s;
    dfs(G, s);
  }

  // Recursive
  private void dfs(Graph G, int v) {
    visited[v] = true;
    for (int w : G.adj(v))
      if (!visited[w]) {
        edgeTo[w] = v;
        dfs(G, w);
      }
  }

  public Iterable<Integer> pathTo(int v) {
    if (!visited(v)) return null;
    Stack<Integer> path = new Stack<Integer>();
    for (int x = v; x != s; x = edgeTo[x])
      path.push(x);
    path.push(s);
    return path;
  }
}
```


#### BFS

  - **Breadth-First Search** puts unvisited vertices on queue.
  - BFS computes the **shortest-paths** from `s` to all other vertices in a graph in time proportional to `V+E`.
  - Multiple-source shortest paths: to find the shortest path from any vertex in a set of vertices to each other vertex,
    we can use BFS initialized by enqueueing all source vertices in the set.

```java
private void bfs(Graph G, int s) {
  boolean[] visited = new boolean[G.V()];
  Queue<Integer> q = new Queue<Integer>();

  visited[s] = true;
  q.enqueue(s);
  while (!q.isEmpty()) {
    int v = q.dequeue();
    for (int w : G.adj(v))
      if (!visited[w]) {
        visited[w] = true;
        q.enqueue(w);
      }
  }
}
```

```java
public class BreadthFirstPaths {
  private boolean[] visited;
  private int[] edgeTo;
  private int s;

  public BreadthFirstPaths(Graph G, int s) {
    visited = new boolean[G.V()];
    edgeTo = new int[G.V()];
    this.s = s;
    bfs(G, s);
  }

  private void bfs(Graph G, int s) {
    Queue<Integer> q = new Queue<Integer>();

    visited[s] = true;
    q.enqueue(s);
    while (!q.isEmpty()) {
      int v = q.dequeue();
      for (int w : G.adj(v))
        if (!visited[w]) {
          visited[w] = true;
          edgeTo[w] = v;
          q.enqueue(w);
        }
    }
  }

  public Iterable<Integer> pathTo(int v) {
    if (!visited(v)) return null;
    Stack<Integer> path = new Stack<Integer>();
    for (int x = v; x != s; x = edgeTo[x])
      path.push(x);
    path.push(s);
    return path;
  }
}
```


#### Connected Components

  - Having pre-processed a graph, we can answer connectivity queries in constant time.
  - DFS uses preprocessing time and space proportional to `V+E` to support constant-time connectivity queries.

```java
public class ConnectedComponents {
  private boolean[] visited;
  private int[] id;
  private int count;

  private void ConnectedComponents(Graph G) {
    visited = new boolean[G.V()];
    id = new int[G.V()];

    for (int s = 0; s < G.V(); s++)
      if (!visited[v]) {
        dfs(G, v);
        count++;
      }
  }

  // Recursive
  private void dfs(Graph G, int v) {
    visited[v] = true;
    id[v] = count;
    for (int w : G.adj(v))
      if (!visited[w])
        dfs(G, w);
  }

  public int id(int v) {
    return id[v]
  }

  public boolean connected(int v, int w) {
    return id[v] == id[w];
  }
}
```



#### Directed Cycle

```java
public class DirectedCycle {
  private boolean[] visited;
  private int[] edgeTo;
  private boolean[] onStack;     // vertices on recursive call stack
  private Stack<Integer> cycle;  // vertices on a cycle if any

  public DirectedCycle(Digraph G) {
    visited = new boolean[G.V()];
    edgeTo = new int[G.V()];
    onStack = new boolean[G.V()];

    for (int v = 0; v < G.V(); v++)
      if (!visited[v])
        dfs(G, v);
  }

  private void dfs(Digraph G, int v) {
    visited[v] = true;
    onStack[v] = true;
    for (int w : G.adj(v))
      if (cycle != null) {
        // Cycle already detected
        return;
      } else if (!visited[w]) {
        edgeTo[w] = v;
        dfs(G, w);
      } else if (onStack[w]) {
        // Cycle found
        cycle = new Stack<Integer>();
        for (int x = v; x != w; x = edgeTo[x])
          cycle.push(x);
        cycle.push(w);
        cycle.push(v);
      }
    onStack[v] = false;
  }
}
```


#### Topological Sort

  - A **directed** graph has a topological order if and only if no directed cycle exists (**DAG**).
  - The _reverse DFS post-order_ of a DAG is a topological order.
  - DFS can topologically sort a DAG in time proportional to `V+E`.
  - Topological sort gives an order to redraw DAG so all edges point upwards/outwards.

```java
public class DepthFirstOrder {
  private boolean[] visited;
  private Queue<Integer> pre;          // vertices in preorder
  private Queue<Integer> post;         // vertices in postorder
  private Stack<Integer> reversePost;  // vertices in reverse postorder

  public DepthFirstOrder(Digraph G) {
    visited = new boolean[G.V()];
    pre = new Queue<Integer>();
    post = new Queue<Integer>();
    reversePost = new Stack<Integer>();

    for (int v = 0; v < G.V(); v++)
      if (!visited[v])
        dfs(G, v);
  }

  private void dfs(Digraph G, int v) {
    visited[v] = true;
    pre.enqueue(v);
    for (int w : G.adj(v))
      if (!visited[w])
        dfs(G, w);
    post.enqueue(v);
    reversePost.push(v);
  }

  public Iterable<Integer> reversePost() {
    return reversePost;
  }
}
```


#### Strongly-Connected Components

  - **Strongly-connected components** in directed graph G are same as in the reverse of G (G<sup>R</sup>).
  - Algorithms:
    - **Kosaraju** computes the strongly-connected components of a digraph in time proportional to `V+E`.
      - Phase 1: run DFS on G<sup>R</sup> to compute reverse post-order.
      - Phase 2: run DFS on G, considering vertices in order given by first DFS phase.

```java
public class KosarajuSCC {
  private boolean[] visited;
  private int[] id;
  private int count;

  public KosarajuSCC(Digraph G) {
    visited = new boolean[G.V()];
    id = new int[G.V()];

    DepthFirstOrder order = new DepthFirstOrder(G.reverse());
    for (int s : order.reversePost())
      if (!visited[v]) {
        dfs(G, v);
        count++;
      }
  }

  // Recursive
  private void dfs(Digraph G, int v) {
    visited[v] = true;
    id[v] = count;
    for (int w : G.adj(v))
      if (!visited[w])
        dfs(G, w);
  }

  public int id(int v) {
    return id[v]
  }

  public boolean stronglyConnected(int v, int w) {
    return id[v] == id[w];
  }
}
```


#### Union-Find

```java
public class UnionFind {
  private int count;  // number of components
  private int[] id;

  public UnionFind(int N) {
    count = N;
    id = new int[N];

    for (int i = 0; i < N; i++)
      id[i] = i;
  }

  public int find(int p) {
    return id[p];
  }

  public boolean connected(int p, int q) {
    return find(p) == find(q);
  }

  public void union(int p, int q) {
    int pid = find(p);
    int qid = find(q);

    // p and q are already in the same component
    if (pid == qid)
      return;

    // Rename p component to q component.
    for (int i = 0; i < id.length; i++)
      if (id[i] == pid)
        id[i] = qid;
    count--;
  }
}
```

```java
public class QuickUnionFind {
  private int count;  // number of components
  private int[] id;

  public UnionFind(int N) {
    count = N;
    id = new int[N];

    for (int i = 0; i < N; i++)
      id[i] = i;
  }

  public int find(int p) {
    while (p != id[p]) p = id[p];  // follow links to find a root
    return p;
  }

  public boolean connected(int p, int q) {
    return find(p) == find(q);
  }

  public void union(int p, int q) {
    int pRoot = find(p);
    int qRoot = find(q);

    // p and q are already in the same component
    if (pRoot == qRoot)
      return;

    // Rename p component to q component.
    id[pRoot] = qRoot;
    count--;
  }
}
```

```java
public class WeightedQuickUnionFind {
  private int count;   // number of components
  private int[] id;    // parent link
  private int[] size;  // size of component for roots

  public WeightedQuickUnionUF(int N) {
    count = N;
    id = new int[N];
    size = new int[N];

    for (int i = 0; i < N; i++) id[i] = i;
    for (int i = 0; i < N; i++) size[i] = 1;
  }

  private int find(int p) {
    while (p != id[p]) p = id[p];  // follow links to find a root
    return p;
  }

  public boolean connected(int p, int q) {
    return find(p) == find(q);
  }

  public void union(int p, int q) {
    int pRoot = find(p);
    int qRoot = find(q);

    // p and q are already in the same component
    if (pRoot == qRoot)
      return;

    // Make smaller root point to larger one
    if (size[i] < size[j]) {
      id[i] = j;
      size[j] += size[i];
    } else {
      id[j] = i;
      size[i] += size[j];
    }
    count--;
  }
}
```


#### Minimum Spanning Tree

  - Given an **edge-weighted undirected** graph `G` with positive edge weights, an MST of `G` is a sub-graph `T` that is:
    - Tree: connected and acyclic
    - Spanning: includes all of the vertices
    - Minimum: sum of the edge wights are minimum
  - Given any cut in an edge-weighted graph, the crossing edge of minimum weight is in the MST of the graph.
  - Greedy MST algorithm:
    1. Start with all edges colored gray.
    1. Find a cut with no black crossing edge, and color its minimum-weight edge black.
    1. Repeat until `V-1` edges are colored black.
  - Algorithms:
    - **Kruskal** computes MST in time proportional to `ElgE` in the worst case.
    - **Lazy Prim** computes MST in time proportional to `ElgE` and extra space proportional to `E` in the worst case.
    - **Eager Prim** computes MST in time proportional to `ElgV` and extra space proportional to `V` in the worst case.

```java
public class KruskalMST {
  private Queue<Edge> mst;

  public KruskalMST(EdgeWeightedGraph G) {
    mst = new Queue<Edge>();

    MinPQ<Edge> pq = new MinPQ<Edge>(G.edges());
    UnionFind uf = new UnionFind(G.V());

    while (!pq.isEmpty() && mst.size() < G.V() - 1) {
      Edge e = pq.delete();                // get minimum-weight edge
      int v = e.either(), w = e.other(v);
      if (uf.connected(v, w)) continue;    // ineligible edge
      uf.union(v, w);                      // merge components
      mst.enqueue(e);                      // add edge to mst
    }
  }
}
```

```java
public class LazyPrimMST {
  private boolean[] visited;  // MST vertices
  private Queue<Edge> mst;    // MST edges
  private MinPQ<Edge> pq;     // crossing and ineligible edges

  public LazyPrimMST(EdgeWeightedGraph G) {
    visited = new boolean[G.V()];
    mst = new Queue<Edge>();
    pq = new MinPQ<Edge>();

    visit(G, 0);                               // assuming G is a connected graph
    while (!pq.isEmpty()) {
      Edge e = pq.delete();                    // get minimum-weight edge
      int v = e.either(), w = e.other(v);
      if (visited[v] && visited[w]) continue;  // ineligible edge
      mst.enqueue(e);                          // Add edge to tree
      if (!visited[v]) visit(G, v);            // Add vertex to tree
      if (!visited[w]) visit(G, w);            // Add vertex to tree
    }
  }

  private void visit(EdgeWeightedGraph G, int v) {
    visited[v] = true;
    for (Edge e : G.adj(v)) {
      if (!visited[e.other(v)])
        pq.insert(e);
    }
  }
}
```

```java
public class EagerPrimMST {
  private boolean[] visited;      // true if v on tree
  private Edge[] edgeTo;          // shortest edge from tree vertex
  private double[] distTo;        // distTo[w] = edgeTo[w].weight()
  private IndexMinPQ<Double> pq;  // eligible crossing edges

  public EagerPrimMST(EdgeWeightedGraph G) {
    visited = new boolean[G.V()];
    edgeTo = new Edge[G.V
    distTo = new double[G.V()];
    pq = new IndexMinPQ<Double>(G.V());

    for (int v = 0; v < G.V(); v++)
      distTo[v] = Double.POSITIVE_INFINITY;

    distTo[0] = 0.0;
    pq.insert(0, 0.0);
    while (!pq.isEmpty())
      visit(G, pq.delete());  // add closest vertex to tree
  }

  private void visit(EdgeWeightedGraph G, int v) {
    visited[v] = true;
    for (Edge e : G.adj(v)) {
      int w = e.other(v);
      if (visited[w]) continue;      // v-w is ineligible
      if (e.weight() < distTo[w]) {  // e is the new best connection from tree to w
        edgeTo[w] = e;
        distTo[w] = e.weight();
        if (pq.contains(w))
          pq.change(w, distTo[w]);
        else
          pq.insert(w, distTo[w]);
      }
    }
  }
}
```


#### Shortest-Path Tree

  - **Shortest Path:** A shortest path from vertex `s` to vertex `t` in an **edge-weighted digraph**:
    - is a directed path from `s` to `t`
    - no other such path has a lower weight
  - Given an **edge-weighted directed** graph, the _shortest path_ from `s` to every other vertex is a tree:
    - rooted at `s`
    - every tree path is a _shortest path_ in the digraph.
  - Algorithms:
    - **Dijkstra** computes a SPT in any digraph with non-negative edge weights in time proportional to `ElgV` (using binary heap).
      - `edgeTo` : a vertex-indexed array in which `edgeTo[v]` is last edge on shortest path from `s` to `v`.
      - `distTo` : a vertex-indexed array in which `distTo[v]` is length of shortest path from `s` to `v`.

```java
public class DijkstraShortestPath {
  private DirectedEdge[] edgeTo;
  private double[] distTo;
  private IndexMinPQ<Double> pq;

  public DijkstraShortestPath(EdgeWeightedDigraph G, int s) {
    edgeTo = new DirectedEdge[G.V()];
    distTo = new double[G.V()];
    pq = new IndexMinPQ<Double>(G.V());

    for (int v = 0; v < G.V(); v++)
      distTo[v] = Double.POSITIVE_INFINITY;

    distTo[s] = 0.0;
    pq.insert(s, 0.0);
    while (!pq.isEmpty())
      relax(G, pq.delete())
  }

  private void relax(EdgeWeightedDigraph G, int v) {
    for(DirectedEdge e : G.adj(v)) {
      int w = e.to();
      if (distTo[w] > distTo[v] + e.weight()) {
        edgeTo[w] = e;
        distTo[w] = distTo[v] + e.weight();
        if (pq.contains(w))
          pq.change(w, distTo[w]);
        else
          pq.insert(w, distTo[w])
      }
    }
  }
}
```
