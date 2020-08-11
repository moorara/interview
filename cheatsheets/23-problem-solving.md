# Problem Solving Questions


## Algorithms

**Q.** Solve the 8-Queens problem by backtracking.

**Q.** Implement a function that receives a string and an integer `K` and returns another string.
The string is a message with an arbitrary length and the interger is the limit for maximum length of expected output string.
Your function should crop the input string with the longest possbile length equal or less than `K`.
You cannot crop a word in the middle and your output string should end with a word (not space).

**Q.** Given a list of words, find a pair of words with no letter in common which the product of their lengths is maximum.

**Q.** Given an array of integers, compute another array with the same size such that
every element in the resulting array is product of all elements in input array except the one with the same index in resulting array.

**Q.** Given `N` unique positive integers, we want to count the total pairs of numbers whose difference is `K`.
The solution should minimize computational time complexity to the best of your ability.

**Q.** Given the set of cuisines and features for every restaurant, find the most recurring pair of `<cuisine, feature>` among all restaurants.

**Q.** Given a sequence of digits,
first compute a list of all strings that can be represented by that sequence of digits (using _T9 keyboard_),
and then return a list of all strings from a dictionary that starts with either of those calculated strings (prefixes).

**Q.** Count and find all palindromes in a given string. A palindrome is a string which reads the same backward or forward.

**Q.** There are N objects positioned in a row. Each of them is either black or white. Every time, we can swap only two adjacent objects.
We want to arrange all the white objects together in one segment. Determine the minimum number of swaps required to format white objects.

**Q.** Consider an NxN array specifying heights of buildings at each position.
You can go up and down across rooftops with a fixed-size ladder.
At each building, you can move in four directions (up, right, down, left).
Given a length for you ladder, write an algorithm to get to bottom-right corner starting from top-left corner.

```
  ┌───┬───┬───┬───┬───┐
  │ 0 │ 1 │ 1 │ 4 │ 6 │
  ├───┼───┼───┼───┼───┤
  │ 4 │ 4 │ 3 │ 1 │ 0 │
  ├───┼───┼───┼───┼───┤
  │ 4 │ 2 │ 4 │ 7 │ 5 │
  ├───┼───┼───┼───┼───┤
  │ 3 │ 8 │ 4 │ 2 │ 0 │
  ├───┼───┼───┼───┼───┤
  │ 2 │ 2 │ 3 │ 3 │ 1 │
  └───┴───┴───┴───┴───┘

Given a ladder of length 2, an answer is:
0 > 1 > 1 v 3 v 4 v 4 v 3 > 3 > 1
```

**Q.** Your given an array that each element is an integer specifying the height of a building.
Write an algorithm to compute the volume water that can be trapped between the buildings if it rains.

```
    █       █
    █       █   █
  █ █     █ █ █ █
  █ █ █ █ █ █ █ █
  █ █ █ █ █ █ █ █

Array: [ 3, 5, 2, 2, 3, 5, 3, 4 ]
Answer: 9
```

<details>
<summary>Solution</summary>
<p>

```go
func min(a, b int) int {
  if a < b {
    return a
  }
  return b
}

func calcVolume(heights []int) int {
  total := 0
  n := len(heights)

  // O(n)
  leftMax := make([]int, n)
  leftMax[0] = heights[0]
  for i := 1; i < n; i++ {
    if heights[i] > leftMax[i-1] {
      leftMax[i] = heights[i]
    } else {
      leftMax[i] = leftMax[i-1]
    }
  }

  // O(n)
  rightMax := make([]int, n)
  rightMax[n-1] = heights[n-1]
  for i := n-2; i >= 0; i-- {
    if heights[i] > rightMax[i+1] {
      rightMax[i] = heights[i]
    } else {
      rightMax[i] = rightMax[i+1]
    }
  }

  // O(n)
  for i := 1; i < n-1; i++ {
    m := min(leftMax[i], rightMax[i])
    total += m - heights[i]
  }

  return total
}
```

</p>
</details>

**Q.** You are given a map of city divided into a number of plots and the cost of each plot is also given.
Given a budget, determine the largest rectangular area of land we can purchase.

```
  ┌───┬───┬───┐
  │ 2 │ 4 │ 7 │
  ├───┼───┼───┤
  │ 3 │ 1 │ 1 │
  ├───┼───┼───┤
  │ 5 │ 2 │ 2 │
  └───┴───┴───┘
```


## Lists

**Q.** Implement a circular sorted linked-list.

**Q.** Implement a Queue (FIFO) using only standard Stacks (LIFO) data structures.

**Q.** Implement a Stack which can give the maximum pushed entry as well using only standard Stacks.


## Trees

**Q.** Consider an arbitrary tree in which every node is annotated with an integer greater than zero.
A path is defined as a sequence of integers from the root to a leaf. A zero can match any node (wildcard). A query is a union of paths.
A path matches a node if it ends with that node. A query matches a node if at least one of its paths matches the node.

```
        1
     /  |   \
    2   3    4
   / \     / | \
  5   6   7  8  9

Paths:
  <1,2,5>  matches 5
  <1,4,0>  matches 7, 8, 9

Queries:
  <1,2,6> U <1,3>    matches 6, 3
  <1,2,0> U <1,4,0>  matches 5, 6, 7, 8, 9
```

Write an algorithm to evaluate a query and determines the list of matching nodes.

**Q.** Trie is a tree for indexing keys represented as strings. It is also called radix tree or prefix tree.
For the purpose of this question we consider a binary trie.
A binary trie is a binary tree in which the left child represents the next character in a string and the right child represents the next character in the same level.
Here is an example:

```
_
|
b-------------d
|             |
a---------o   a
|         |   |
b--d*--n  x*  d*--n
|      |          |
y*     k*         c
                  |
                  e*
```

Left children are represented by vertical lines and right children are represented by horizontal (dashed) lines.
Any node marked with * represents a word in the tree.
In this example we have the following words in the tree:

`"baby", "bad", "bank", "box", "dad", "dance"`

  1. Write an algorithm to search for a word in the tree.
  1. Write an algorithm to print all the words in tree.
  1. Write an algorithm to insert a word in the tree.
  1. Write an algorithm to print all the words in tree sorted.


## Graphs

**Q.** Solve a 2D maze. Try finding the shortest path.

**Q.** In a dependency graph, determine if there is going to be any _deadlock_.
If no deadlock, come up with an execution plan (the order in which the transactions should be executed).

**Q.** Image Contour: given the bitmap of a black-and-white image in which each pixel is either white or black,
write an algorithm to change the color of middle pixels to white and only keep the border pixels black. Use as minimum as memory possible.


## System Design

**Q.** Design a system for processing (aggregating and minimizing) a list of transactions.
The transactions can be generated in _real-time_ and in a very _large scale_.


## Database

**Q.** You are given two tables as follows:

```
 teams                                 matches
+---------------+---------+           +---------------+---------+
| id            | int     |<----|     | id            | int     |
| name          | varchar |     |-----| host_id       | int .   |
+---------------+---------+     |-----| guest_id      | int     |
                                      | host_goals    | int     |
                                      | guest_goals   | int     |
                                      +---------------+---------+
```

Write a query to calculate the total number of points for each team.
Teams should be sorted by points from the highest to lowest.

```
  | team_name | total_points |
  |-----------+--------------|
  |           |              |
  |           |              |
  |           |              |
  |-----------+--------------|
```

Here are the rules for points:

  - A win has 3 points
  - A draw has only 1 point
  - A loss has no point

<details>
<summary>Solution</summary>
<p>

```sql
SELECT u.team_name, SUM(u.score) AS total_points FROM (
  SELECT
    t.id AS team_id,
    t.name AS team_name,
    CASE
      WHEN (m.host_goals - m.guest_goals) > 0 THEN 3
      WHEN (m.host_goals - m.guest_goals) = 0 THEN 1
      ELSE 0
    END score
  FROM teams AS t LEFT JOIN matches AS m ON t.id = m.host_id
  UNION ALL
  SELECT
    t.id AS team_id,
    t.name AS team_name,
    CASE
      WHEN (m.guest_goals - m.host_goals) > 0 THEN 3
      WHEN (m.guest_goals - m.host_goals) = 0 THEN 1
      ELSE 0
    END score
  FROM teams AS t LEFT JOIN matches AS m ON t.id = m.guest_id
) AS u
GROUP BY u.team_name
ORDER BY total_points DESC
```

</p>
</details>


## Open Discussions

  - REST API
    - Why do you think RESTful APIs need to be _stateless_?
    - Why do you think RESTful APIs need to be _idempotent_?
    - What are some of the challenges with REST APIs?
  - Database
    - How do you compare SQL vs NoSQL?
  - Distributed Systems
    - How is a microservices architecture different from a monolithic architecture?
    - What are some of the challenges about microservices architecture?
    - How do you implement _joins_ in microservices?
    - How do you implement _atomic transactions_ in microservices?
    - How would you implement _caching_ in microservices?
    - When would you use a _message broker_ for services to communicate?
  - Containerization
    - What is a container made of?
    - How is a container different from a virtual machine?
    - What is Kubernetes architecture like? What are the different components?
  - Testing
    - What is _unit testing_?
    - Would you spend more time writing _unit tests_ or _integration tests_?
    - How do you compare _unit testing_ vs. _component testing_ vs. _integration testing_ vs. _API testing_ vs. _system testing_?
  - CI/CD
    - What is the difference between _continuous integration_ and _continuous delivery_?

