# Database

## Normalization

  - **Functional Dependency**
    - If two tuples have same values for attributes X<sub>1</sub>, X<sub>2</sub>,..., X<sub>n</sub>,
      then those two tuples must have the same values for attributes Y<sub>1</sub>, Y<sub>2</sub>, ..., Y<sub>m</sub>
      - **Trivial:** If a functional dependency X → Y holds, where Y is a subset of X, then it is called a trivial FD.
      - **Non-trivial:** If an FD X → Y holds, where Y is not a subset of X, then it is called a non-trivial FD.
      - **Completely non-trivial:** If an FD X → Y holds, where X intersect Y = Φ, it is said to be a completely non-trivial FD.
    - If `F` is a set of functional dependencies then the closure of `F(F+)` is the set of all functional dependencies logically implied by F.


  - **Armstrong's Axioms**
    - **Reflexive rule:** if α is a set of attributes and β is subset of α, then α → β holds.
    - **Augmentation rule:** if α → β holds and γ is attribute set, then αγ → βγ also holds.
    - **Transitivity rule:** if α → β holds and β → γ holds, then α → γ also holds.


  - **Anomalies**
    - **Insert Anomaly**
    - **Update Anomaly**
    - **Delete Anomaly**


  - **Normal Forms**
    - **First Normal Form (1NF):**
      - Each table should be organized into rows, and each row should have a primary key that distinguishes it uniquely.
      - All the attributes in a relation must have atomic domains. The values in an atomic domain are indivisible units.
    - **Second Normal Form (2NF):**
      - For a relation to be in second normal form, it must be in first normal form.
      - Every non-prime attribute should be fully functionally dependent on prime key attribute.
      - If X → A holds, then there should not be any proper subset Y of X, for which Y → A also holds true.
      - If any column depends only on one part of the concatenated primary key, then the table fails second normal form.
    - **Third Normal Form (3NF):**
      - For a relation to be in third normal form, it must be in second normal form.
      - No non-prime attribute is transitively dependent on prime key attribute.
      - There should not be the case that a non-prime attribute is determined by another non-prime attribute.
      - For any non-trivial functional dependency, X → A, then either X is a superkey or, A is prime attribute.
    - **Boyce-Codd Normal Form (BCNF):**
      - For a relation to be in Boyce-Codd normal form, it must be in third normal form.
      - For any non-trivial functional dependency, X → A, then X must be a super-key.
      - A 3NF table which does not have multiple overlapping candidate keys is said to be in BCNF.

