# Sorting

**References:**

  - Algorithms, 4th Edition (_Robert Sedgewick and Kevin Wayne_)

## Sorting Summary

| Algorithm                                 | Best Case       | Average Case      | Worst Case      | Space | Remarks                                            |
|-------------------------------------------|-----------------|-------------------|-----------------|-------|----------------------------------------------------|
| [Selection](#selection-sort)              | N<sup>2</sup>/2 | N<sup>2</sup>/2   | N<sup>2</sup>/2 | 1     | N exchanges                                        |
| [Insertion](#insertion-sort)              | N               | N<sup>2</sup>/4   | N<sup>2</sup>/2 | 1     | **Stable**, For small N or partially ordered       |
| [Shell](#shell-sort)                      | N               | ?                 | ?               | 1     | Tight code, Subquadratic                           |
| [Merge](#merge-sort)                      | NlgN            | NlgN              | NlgN            | N     | **Stable**, **NlgN guarantee**, Extra memory       |
| [Quick](#quick-sort)                      | NlgN            | 2NlnN             | N<sup>2</sup>/2 | clgN  | **NlgN probabilistic guarantee**                   |
| [3-Way Quick](#3-way-quick-sort)          | N               | 2NlnN             | N<sup>2</sup>/2 | clgN  | Faster in presence of **duplicate keys**           |
| [Heap](#heap-sort)                        | NlgN            | NlgN              | NlgN            | 1     | **NlgN guarantee**                                 |
| [LSD Radix](#lsd-least-significant-digit) |                 | 2NW               | 2NW             | N+R   | Stable, **Non-comparative**, Fixed-length W keys   |
| [MSD Radix](#msd-most-significant-digit)  |                 | Nlog<sub>R</sub>N | 2NW             | N+DR  | Stable, **Non-comparative**, Average-length W keys |
| [Radix Quick](#3-way-radix-quick-sort)    |                 | 2NlnN             | 2NWlnR          | lgN+W | Char/Digit compare-based, Cache-friendly           |

  - Any **compare-based** sorting algorithm must use at least **lg(N!) ~ NlgN** compares in the worst case.


### Selection Sort

```java
public static void sort(Comparable[] a) {
  int N = a.length;
  for (int i = 0; i < N; i++) {
    int min = i;
    for (int j = i + 1; j < N; j++)
      if (a[j] < a[min]) min = j;
    exchange(a, i, min);
  }
}
```


### Insertion Sort

```java
public static void sort(Comparable[] a) {
  int N = a.length;
  for (int i = 0; i < N; i++)
    for (int j = i; j > 0 && a[j] < a[j-1]; j--)
      exchange(a, j, j-1);
}
```

  - For partially sorted (the number of inversions is linear) arrays,
    insertion sort runs in linear time (the number of exchanges equals the number of inversions).


### Shell Sort

```java
public static void sort(Comparable[] a) {
  int N = a.length;
  int h = 1;
  while (h < N/3)
    h = 3*h + 1;  // 1, 4, 13, 40, 121, ...
  while (h >= 1) {
    for (int i = h; i < N; i++)                         // h-sort the array
      for (int j = i; j >= h && a[j] < a[j-h]; j -= h)  // insert a[i] among a[i-h], a[i-2*h], a[i-3*h], ...
        exchange(a, j, j-h);
    h = h/3;
  }
}
```

  - An h-sorted array is h independent sorted subsequences, interleaved together (starting anywhere, taking every h<sup>th</sup> entry yields a sorted subsequence).
  - A g-sorted array remains g-sorted after h-sorting.
  - Shell sort _h-sorts_ array for decreasing sequence of h values. In order to h-sort, we use insertion sort with stride length h.
  - The worst-case number of compares used by Shell sort with 3h+1 increment is O(N<sup>3/2</sup>).
  - Shell sort gains efficiency by making a trade-off between size and partial order in the subsequences.
  - Read more [1](https://en.wikipedia.org/wiki/Shellsort), [2](https://www.tutorialspoint.com/data_structures_algorithms/shell_sort_algorithm.htm)


### Merge Sort

```java
private static void merge(Comparable[] a, Comparable[] aux, int lo, int mid, int hi) {
  int i = lo; j = mid + 1;
  for (int k = lo; k <= hi; k++)
    aux[k] = a[k];
  for (int k = lo; k <= hi; k++) {
    if      (i > mid)          a[k] = aux[j++];
    else if (j > hi)           a[k] = aux[i++];
    else if (aux[j] < aux[i])  a[k] = aux[j++];
    else                       a[k] = aux[i++];
  }
}

// Recursive function
private static void sort(Comparable[] a, Comparable[] aux, int lo, int hi) {
  if (hi <= lo)
    return;
  int mid = (lo + hi) / 2;
  sort(a, aux, lo, mid);
  sort(a, aux, mid + 1, hi);
  if (a[mid + 1] >= a[mid]) return;  // improvement for partially-ordered arrays
  merge(a, aux, lo, mid, hi);
}

// Driver function
public static void sort(Comparable[] a) {
  Comparable[] aux = new Comparable[a.length];
  sort(a, aux, 0, a.length - 1);
}
```

```java
// Iterative
public static void sort(Comparable[] a) {
  int n = a.length;
  Comparable[] aux = new Comparable[n];
  for (int size = 1; size < n; size += size)
    for (int lo = 0; lo < n - size; lo += size + size)
      merge(a, aux, lo, lo + size - 1, Math.min(lo + size + size - 1, n - 1));
}
```

  - Merge sort is **optimal w.r.t. number of compares**, but not optimal w.r.t. space usage.
  - Merge sort has too much overhead for tiny arrays (cut-off to insertion sort = 7).
  - We can eliminate the copy to the auxiliary array and save more time by switching the role of the input and auxiliary array in each recursive call.


### Quick Sort

**Partitioning** the array for some `j` such that:
  - entry `a[j]` is in place
  - no larger entry to the left of `j`
  - no smaller entry to the right of `j`

```java
private static int partition(Comparable[] a, int lo, int hi) {
  int i = lo, j = hi + 1;
  Comparable v = a[lo]
  while (true) {
    while (a[++i] < v)
      if (i == hi) break;
    while (a[--j] > v)
      if (j == lo) break;
    if (i >= j) break;
    exchange(a, i, j);
  }
  exchange(a, lo, j);
  return j;  // a[lo..j-1] <= a[j] <= a[j+1..hi]
}

// Recursive function
private static void sort(Comparable[] a, int lo, int hi) {
  if (hi <= lo) return;
  int j = partition(a, lo, hi);
  sort(a, lo, j - 1);
  sort(a, j + 1, hi);
}

// Driver function
public static void sort(Comparable[] a) {
  shuffle(a);  // can be done in Θ(n)
  sort(a, 0, a.length - 1);
}

```

```java
// Quick Select
public static Comparable select(Comparable[] a, int k) {
  shuffle(a);
  int lo = 0, hi = a.length - 1;
  while (hi > lo) {
    int j = partition(a, lo, hi);
    if      (j < k)  lo = j + 1;
    else if (j > k)  hi = j - 1;
    else return a[k];
  }
  return a[k];
}
```

  - **Shuffling** is needed for probabilistic guarantee against the worst case.
  - Quick sort has 39% more compares than Merge sort, but it is faster in practice.
  - Quick sort has too much overhead for tiny sub-arrays (cut-off to insertion sort = 10).
  - Using an extra array makes partitioning stable, but is not worth the cost.
  - Best choice for pivot item is median, and it can be estimated by taking median of a sample (3 random items).
  - **Quick-select** takes linear time on average.


### 3-Way Quick Sort

**3-Way Partitioning**: partition array into three parts so that:
  - entries between `lt` and `gt` equal to partition item `v`
  - no larger entries to the left of `lt`.
  - no smaller entries to the right of `gt`.

```java
// Recursive function
private static void sort(Comparable[] a, int lo, int hi) {
  if (hi <= lo) return;
  int lt = lo, i = lo + 1, gt = hi;
  Comparable v = a[lo];
  while (i <= gt) {
    int cmp = a[i].compareTo(v);
    if      (cmp < 0)  exchange(a, lt++, i++);
    else if (cmp > 0)  exchange(a, i, gt--);
    else               i++;
  } // a[lo..lt-1] < v = a[lt..gt] < a[gt+1..hi].
  sort(a, lo, lt - 1);
  sort(a, gt + 1, hi);
}

// Driver function
public static void sort(Comparable[] a) {
  shuffle(a);  // can be done in Θ(n)
  sort(a, 0, a.length - 1);
}
```

  - Quick sort with 3-way partitioning is **entropy-optimal**.


### Heap Sort

```java
// Top-down Reheapification
private static void sink(Comparable[] a, int k, int n) {
  while (2 * k <= n) {
    int j = 2 * k;
    if (j < n && a[j] < a[j + 1]) j++;
    if (a[k] >= a[j]) break;
    exchange(a, k, j);
    k = j;
  }
}

public static void sort(Comparable[] a) {
  int n = a.length;
  for (int k = n / 2; k >= 1; k--)  // build heap using bottom-up method
    sink(a, k, n);
  while (n > 1) {  // remove the maximum, one at a time
    exchange(a, 1, n);
    sink(a, 1, --n);
  }
}
```

  - Heap sort is the only **in-place** sorting algorithm with **NlgN** compares in the **worst-case**.
  - Heap sort is **optimal w.r.t. both time and space**, but its inner loop is longer than Quick sort, and it makes poor use of cache memory.


### Radix Sorts

  - Key-indexed counting is efficient for sorting keys with integer digits between `0` and `R-1` (_R_ is a small number).
  - LSD and MSD Radix sorting algorithms are efficient for a large number of keys with small constant width.


#### LSD (_Least Significant Digit_)

```java
// fixed-length W strings
public static void sort(String[] a, int w) {
  int R = 256;  // extended ASCII size
  int N = a.length;
  String[] aux = new String[N];
  for (int d = w-1; d >= 0; d--) {            // sort by key-indexed counting on dth char (stable)
    int[] count = new int[R+1];
    for (int i = 0; i < N; i++)               // compute frequency counts
      count[a[i].charAt(d) + 1]++;
    for (int r = 0; r < R; r++)               // compute cumulative counts
      count[r+1] += count[r];
    for (int i = 0; i < N; i++)               // distribute keys to aux
      aux[count[a[i].charAt(d)]++] = a[i];
    for (int i = 0; i < N; i++)               // copy back aux to a
      a[i] = aux[i];
  }
}
```

  - LSD string sort stably sorts **fixed-length** strings.


#### MSD (_Most Significant Digit_)

```java
private static int charAt(String s, int d) {
  if (d < s.length())
    return s.charAt(d);
  else
    return -1;
}

// Recursive
// variable-length strings
private static void sort(String[] a, String[] aux, int lo, int hi, int d) {
  if (hi <= lo)
    return;
  int[] count = new int[R+2];
  for (int i = lo; i <= hi; i++)                              // compute frequency counts
    count[charAt(a[i], d) + 2]++;
  for (int r = 0; r < R + 1; r++)                             // transform counts to indicies
    count[r+1] += count[r];
  for (int i = lo; i <= hi; i++)                              // distribute keys to aux
    aux[count[charAt(a[i], d) + 1]++] = a[i];
  for (int i = lo; i <= hi; i++)                              // copy back aux to a
    a[i] = aux[i - lo];
  for (int r = 0; r < R; r++)                                 // recursively sort for each character (excludes -1)
    sort(a, aux, lo + count[r], lo + count[r+1] - 1, d+1);
}

// Driver
public static void sort(String[] a) {
  int N = a.length;
  aux = new String[N];
  sort(a, aux, 0, N-1, 0);
}
```

  - MSD Radix sorting algorithm accesses memory randomly, and it is **cache inefficient**.
  - MSD Radix sorting algorithm creates huge number of small sub-arrays due to recursion, and it is much too slow for small sub-arrays.
  - Cut-off to insertion sort for small sub-arrays can be implemented.

```java
private static void less(String a, String b, int d) {
  return a.substring(d).compareTo(b.substring(d));
}

public static void insertion_sort(String[] a, int lo, int hi, int d) {
  for (int i = lo; i <= hi; i++)
    for (int j = i; j > lo && less(a[j], a[j-1], d); j--)
      exchange(a, j, j-1);
}
```


#### 3-Way Radix Quick Sort

```java
private static int charAt(String s, int d) {
  if (d < s.length())
    return s.charAt(d);
  else
    return -1;
}

private static void sort(String[] a, int lo, int hi, int d) {
  if (hi <= lo)
    return;
  int lt = lo, i = lo+1, gt = hi;
  int v = charAt(a[lo], d);
  while (i <= gt) {  // 3-way partitioning on dth char
    int c = charAt(a[i], d);
    if      (c < v)  exchange(a, lt++, i++);
    else if (c > v)  exchange(a, i, gt--);
    else             i++;
  }
  sort(a, lo, lt-1, d);
  if (v >= 0)
    sort(a, lt, gt, d+1);
  sort(a, gt+1, hi, d);
}

public static void sort(String[] a) {
  shuffle(a);  // can be done in Θ(n)
  sort(a, 0, a.length - 1, 0);
}
```

  - 3-Way Radix Quick sort algorithm avoids re-comparing long common prefixes.
  - Cut-off to insertion sort for small sub-arrays can be implemented.

