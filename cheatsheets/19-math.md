# Math

## Linear Algebra

### Matrix Operations

  | Operation                                        | Calculation                                      |
  |--------------------------------------------------|--------------------------------------------------|
  | C<sub>nm</sub> = A<sub>mn</sub><sup>T</sup>      | c<sub>ij</sub> = a<sub>ji</sub>                  |
  | C<sub>mn</sub> = b A<sub>mn</sub>                | c<sub>ij</sub> = b a<sub>ij</sub>                |
  | C<sub>mn</sub> = A<sub>mn</sub> + B<sub>mn</sub> | c<sub>ij</sub> = a<sub>ij</sub> + b<sub>ij</sub> |
  | C<sub>mn</sub> = A<sub>mn</sub> - B<sub>mn</sub> | c<sub>ij</sub> = a<sub>ij</sub> - b<sub>ij</sub> |
  | C<sub>mp</sub> = A<sub>mn</sub> B<sub>np</sub>   | Σ<sub>k=1</sub><sup>n</sup> c<sub>ij</sub> = a<sub>ik</sub> b<sub>kj</sub> |


## Discrete Math

**Rule of sum.** the number of ways to choose one element from one of two disjoint sets is the sum of the cardinalities of the sets.

**Rule of product.** the number of ways to choose an ordered pair is the number of ways to choose the first element times the number of ways to choose the second element.


### Probability

Sample space `S` the set of all possible outcomes/events.

```
P(A and B)  =  P(A)P(B)                   if A and B are independent
P(A xor B)  =  P(A) + P(B)                if A and B are mutually exclusive
P(A or B)   =  P(A) + P(B) - P(A and B)   if A and B are not mutually exclusive
P(A | B)    =  P(A and B) / P(B)
P(A and B)  =  P(A|B)P(B)  =  P(B|A)P(A)
```

```
Permutation:  P(n, k)  =  n! / (n - k)!
Combination:  C(n, k)  =  n! / (n - k)! k!
```

