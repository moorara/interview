# Algorithms

**References:**

  - Introduction to Algorithms (_Thomas H. Cormen, Charles E. Leiserson, Ronald Rivest, Clifford Stein_)

## Complexity Classes

  * **P**
    - All **decision/decidable** problems that can be solved by a **deterministic Turing machine** in polynomial time.
    - Examples:
      - Linear Search: O(n)
      - Binary Search: O(lg<sup>n</sup>)
      - Merge Sort: O(nlg<sup>n</sup>)
      - Matrix Multiplication: O(n<sup>3</sup>)
  * **NP**
    - All **decision/decidable** problems that can be solved by a **non-deterministic Turing machine** (non-deterministic polynomial time).
    - All **decision/decidable** problems for which a given solution (yes-answer) can be verified in polynomial time.
    - P problems are a subset of NP problems (`P ⊆ NP`).
    - Examples:
      - Traveling Salesman Problem: O(2<sup>n</sup>)
      - Knapsack Problem: O(2<sup>n</sup>)
      - Graph Coloring Problem: O(2<sup>n</sup>)
  * **NP-Complete**
    - A **decision/decidable** problem in NP is NP-Complete (`NP-Complete ⊆ NP`) if every other problem in NP can be reduced to it in polynomial time.
    - NP-complete problems are the most difficult problems in NP.
    - Examples:
      - SAT Problem
      - Subset Sum Problem
      - Knapsack Decision Problem
      - Hamiltonian Path/Cycle Problem
      - Traveling Salesman Decision Problem
      - Subgraph Isomorphism Problem
      - Graph Coloring Decision Problem
  * **NP-Hard**
    - A **problem** is NP-Hard if all other problems in NP can be reduced to it in polynomial time.
    - NP-hard problems do not have to be in NP, and they do not have to be *decision/decidable* problems.
    - NP-Hard problems are at least as hard as the hardest problems in NP (`NP-Complete ⊆ NP-Hard`).
    - Examples:
      - Knapsack Optimization Problem
      - Traveling Salesman (Optimization) Problem
      - Graph Coloring Optimization Problem


## Algorithm Complexity

**Notations:**
  - Asymptotic Lower Bound: f(n) = Ω(g(n)) --> ∃c,n<sub>0</sub> >= 0 s.t ∀n >= n<sub>0</sub> : 0 <= cg(n) <= f(n)
  - Asymptotic Upper Bound: f(n) = O(g(n)) --> ∃c,n<sub>0</sub> >= 0 s.t ∀n >= n<sub>0</sub> : 0 <= f(n) <= cg(n)
  - Asymptotic Tight Bound: f(n) = Θ(g(n)) --> ∃c<sub>1</sub>,c<sub>2</sub>,n<sub>0</sub> >= 0 s.t ∀n >= n<sub>0</sub> : 0 <= c<sub>1</sub>g(n) <= f(n) <= c<sub>2</sub>g(n)
  - f(n) = ω(g(n)) --> ∃ c,n<sub>0</sub> >= 0 s.t ∀ n >= n<sub>0</sub> : 0 <= cg(n) < f(n)
  - f(n) = o(g(n)) --> ∃ c,n<sub>0</sub> >= 0 s.t ∀ n >= n<sub>0</sub> : 0 <= f(n) < cg(n)

**Theorems:**
  - f(n) = Θ(g(n)) iff g(n) = Θ(f(n))
  - f(n) = O(g(n)) iff g(n) = Ω(f(n))
  - f(n) = Ω(g(n)) and g(n) = Ω(h(n)) --> f(n) = Ω(h(n))
  - f(n) = O(g(n)) and g(n) = O(h(n)) --> f(n) = O(h(n))
  - f(n) = Θ(g(n)) and g(n) = Θ(h(n)) --> f(n) = Θ(h(n))
  - f(n) = Θ(g(n)) iff f(n) = Ω(g(n)) and f(n) = O(g(n))

**Notes:**
  - A **structural analysis** on **worst-case** running time of an algorithm gives an **upper bound (Big-O)** on the running time of the algorithm for every input.
  - A **structural analysis** on **best-case** running time of an algorithm gives a **lower bound (Big-Ω)** on the running time of the algorithm for every input.
  - Big-O notation may or may not be asymptotically tight while small-o notation is a upper bound that is not asymptotically tight.
  - Big-Ω notation may or may not be asymptotically tight while small-ω notation is a lower bound that is not asymptotically tight.


### Structural Analysis

  1. Having an algorithm, assign a cost c<sub>i</sub> to each statement besides the running times t<sub>i</sub> for that statement.
  2. Calculate a sum over c<sub>i</sub>t<sub>i</sub> terms for all statements.


### Growth of Functions

  - c < log<sup>n</sup> < n<sup>c</sup> (0<c<1) < n < nlog<sup>n</sup> < n<sup>2</sup> < n<sup>c</sup> (c>2) < c<sup>n</sup> < n! < n<sup>n</sup>

### Math Summary

  - 1 + 2 + 3 + ... + n = (1/2)n(n+1)
  - 1<sup>2</sup> + 2<sup>2</sup> + 3<sup>2</sup> + ... + n<sup>2</sup> = (1/6)n(n+1)(2n+1)
  - 1<sup>3</sup> + 2<sup>3</sup> + 3<sup>3</sup> + ... + n<sup>3</sup> = (1/4)n<sup>2</sup>(n+1)<sup>2</sup>
  - 1  + x<sup>1</sup> + x<sup>2</sup> + ... + x<sup>n</sup> = (x<sup>n+1</sup> - 1) / (x - 1)
  - 1  + x<sup>1</sup> + x<sup>2</sup> + x<sup>3</sup> + ... = 1 / (1 -x) if |x| < 1
  - 1 + (1/2) + ... + (1/n) = ln(n) + O(1)
  - e<sup>x</sup> = 1 + x + (x<sup>2</sup>/2!) + (x<sup>3</sup>/3!) + ...  -->  x + 1 <= e<sup>x</sup> <= x<sup>2</sup> + x + 1
  - ln(x + 1) = x - (x<sup>2</sup>/2) + (x<sup>3</sup>/3) - ...  -->  x / (x + 1) <= ln(x + 1) <= x


### Recurrence Analysis

The running time of a recursive algorithm can be written as follows:

```
       ┌ Θ(1) if n <= c
T(n) = │
       └ T(n1) + T(n2) + ... + T(nk) + D(n) + C(n)

  k:     the number of sub-problems at each stage
  ni:    the size of the sub-problem i as a fraction of n
  D(n):  the time to divide the problem into k sub-problems
  C(n):  the time to combine the sub-problem solutions into the original problem solution
```

  1. Draw a recursion tree  --> each node represents the cost of a single sub-problem as a function of n.
  2. Sum the costs within each level of the tree to obtain a set of per-level costs.
  3. Sum all the per-level costs to determine the total cost of all levels of the recursion.


**Master Theorem.** Let a >= 1 and b > 1 be constants, let f(n) be a function, and let T(n) be defined on the non-negative integers by the recurrence

  T(n) = aT(n/b) + f(n)

where we interpret n/b to mean either floor or ceiling. Then T(n) has the following asymptotic bound:

If f(n) = O(n<sup>log<sub>b</sub><sup>a-ε</sup></sup>)
for some constant ε > 0, then  T(n) = Θ(n<sup>log<sub>b</sub><sup>a</sup></sup>)

If f(n) = Θ(n<sup>log<sub>b</sub><sup>a</sup></sup>)
then T(n) = Θ(n<sup>log<sub>b</sub><sup>a</sup></sup>ln(n))

If f(n) = Ω(n<sup>log<sub>b</sub><sup>a+ε</sup></sup>)
for some constant ε > 0, and if af(n/b) <= c(f(n))
for some constant c < 1 and all sufficiently large n, then  T(n) = Θ(f(n))


## Algorithm Design


### Divide-and-Conquer

  1. **Divide** the problem into a number of **sub-problems** that are smaller instances of the same problem.
  2. **Conquer** the sub-problems by solving them **recursively**. If the sub-problem sizes are small enough, solve them in a straightforward manner.
  3. **Combine** the solutions to the sub-problems into the solution for the original problem.

#### Recursion

  - Identify a notion of **size** for the problem and formulate the problem in form of a **recursive function**:
  - Examples:
    - Factorial: f(n) = n ✕ f(n-1)
    - Fibonacci: f(n) = f(n-1) + f(n-2)

  1. Check for the **end condition** of recursion and solve the problem for the smallest size(s) straightly.
  2. Call the function recursively to solve the problem(s) with smaller size(s).
  3. Combine the solutions to the smaller problems and return the solution.


### Dynamic Programming

  - Dynamic programming typically applies to **optimization problems**.
    - Optimization problems have many possible solutions.
    - Each solution has a value, and we are interested in a solution with the optimal (minimum or maximum) value.
  - Dynamic programming uses additional memory to save computation time.
  - With dynamic programming, an exponential-time solution can be transformed into a polynomial-time solution if:
    - The number of distinct subproblems involved is polynomial in the input size
    - Each subproblem can be solved in polynomial time

A problem must have two key elements in order for dynamic programming to apply:

  - **Optimal substructure:** an optimal solution to the problem incorporates optimal solutions to the related subproblems.
  - **Overlapping subproblems:** A recursive algorithm revisits the same subproblems over and over (the subproblems share sub-subproblems).

**Optimal Substructure**

  1. A solution to the problem consists of making a choice that leaves one or more subproblems to be solved.
  1. We assume that for a given problem, we are given the choice that leads to an optimal solution.
  1. Given this choice, we determine which subproblems best characterize the resulting space of subproblems. 
  1. The solution to the problem must have optimal solutions to the subproblems.
      - Suppose each of the subproblem solutions is not optimal and then derive a contradiction.
      - By _cutting out_ the non-optimal solution to each subproblem and _pasting in_ the optimal one, you show that you can get a better solution to the original problem.

Optimal substructure varies across problem domains in two ways:

  1. How many subproblems an optimal solution to the original problem uses?
  1. How many choices we have in determining which subproblems to use in an optimal solution?

**Overlapping Subproblems**

  - **Top-down with memoization**:
    1. Implement a simple recursive algorithm for the problem using the optimal sub-structure.
    2. modify the recursive algorithm to save the result of each subproblem and do not solve the same subproblems again.
    - Top-down method is a _depth first search (DFS)_ of the _subproblem graph_. 
  - **Bottom-up**:
    - Solve the subproblems from the smallest size to the largest, and save the solution (a notion of size for the problem is required).
    - Each subproblem is solved only once, and when solving a subproblem, all of the smaller subproblems are already solved.
    - Bottom-up method is the _reverse topological sort_ of the _subproblem graph_ (or the _topological sort_ of the _transpose subproblem graph_).
    - The bottom-up approach often has much better constant factors.

**Subproblem Graph**

  - Each vertex corresponds to a distinct subproblem.
  - The choices for a subproblem are the outgoing edges for that subproblem.
  - The running time of a dynamic programming algorithm is the sum of the times needed to solve each subproblem.
  - The time to compute the solution to a subproblem is proportional to the outgoing degree of the corresponding vertex.


### Greedy Algorithms

  - A greedy algorithm makes a **locally optimal** choice in the hope that this choice will lead to a **globally optimal** solution.
  - A greedy algorithm first makes a greedy choice that seems the best at the moment and then solves the remaining subproblem.
  - A dynamic programming algorithm proceeds bottom-up, whereas a greedy strategy usually progresses in a **top-down** fashion.
  - Greedy algorithms do not always yield optimal solutions.

  1. Determine the optimal substructure of the problem.
  1. Develop a recursive solution.
  1. Show that if we make the greedy choice, then only one subproblem remains.
  1. Prove that a greedy choice at each step yields a globally optimal solution.
  1. Develop a recursive algorithm that implements the greedy strategy.
  1. Convert the recursive algorithm to an iterative algorithm.

Demonstrate optimal substructure by showing that, having made the greedy choice, what remains is a subproblem with the property that if we combine an optimal solution to the subproblem with the greedy choice, we arrive at an optimal solution to the original problem.

