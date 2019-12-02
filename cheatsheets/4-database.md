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


## Relational (SQL)

```sql
-- CREATE TABLE
CREATE TABLE teams (
  id integer not null,
  name varchar(50) not null,
  primary key(id),
  unique(name)
);

-- CREATE TABLE
CREATE TABLE matches (
  id integer not null,
  host_id integer not null,
  guest_id integer not null,
  host_goals integer not null,
  guest_goals integer not null,
  primary key(id),
  key(host_id),
  key(guest_id)
);

-- SELECT
SELECT * FROM teams
SELECT host_goals, guest_goals FROM matches
SELECT t.name FROM teams AS t
SELECT name AS team_name FROM teams

-- WHERE
SELECT * FROM matches WHERE host_id = 12
SELECT * FROM matches WHERE host_goals - guest_goals = 0
SELECT * FROM matches WHERE host_id = 21 OR guest_id = 21
SELECT * FROM matches WHERE host_id IN (11, 12, 13, 14, 15)
SELECT * FROM teams WHERE teams.id BETWEEN 10 AND 20

-- ORDER BY
SELECT * FROM teams ORDER BY name
SELECT * FROM matches ORDER BY host_goals, guest_goals
SELECT * FROM matches ORDER BY host_goals ASC, guest_goals DESC

-- LIMT
SELECT * FROM teams ORDER BY name LIMIT 3
SELECT * FROM teams ORDER BY name LIMIT 3 OFFSET 5

-- GROUP BY and AGGREGATION
SELECT host_id, SUM(host_goals) FROM matches GROUP BY host_id
SELECT host_id, guest_id, SUM(host_goals) FROM matches GROUP BY host_id, guest_id

-- HAVING
SELECT host_id, SUM(host_goals) AS goals FROM matches GROUP BY host_id HAVING goals > 1

-- EXISTS
SELECT name FROM teams WHERE EXISTS (SELECT 1 FROM matches WHERE matches.host_id = teams.id OR matches.guest_id = teams.id)
SELECT name FROM teams WHERE NOT EXISTS (SELECT 1 FROM matches WHERE matches.host_id = teams.id OR matches.guest_id = teams.id)

-- ANY
SELECT name FROM teams WHERE id = ANY (SELECT host_id FROM matches)

-- ALL
SELECT * FROM matches WHERE host_id > ALL (SELECT id FROM teams WHERE id < 30)

-- UNION
(SELECT * FROM teams WHERE id BETWEEN 10 AND 20) UNION (SELECT * FROM teams WHERE id BETWEEN 30 AND 40)

-- INTERSECT
(SELECT * FROM teams WHERE id BETWEEN 10 AND 30) INTERSECT (SELECT * FROM teams WHERE id BETWEEN 20 AND 30)

-- ?
SELECT * FROM teams, matches

-- JOIN
SELECT t.name, m.host_goals FROM teams AS t INNER JOIN matches AS m ON t.id = m.host_id
SELECT t.name, m.host_goals FROM teams AS t LEFT JOIN matches AS m ON t.id = m.host_id
SELECT t.name, m.host_goals FROM teams AS t RIGHT JOIN matches AS m ON t.id = m.host_id
SELECT t.name, m.host_goals FROM teams AS t OUTER JOIN matches AS m ON t.id = m.host_id

-- CASE
SELECT
  id,
  CASE name
    WHEN 'Manchester United' THEN 'Man. U'
    WHEN 'Manchester City' THEN 'Man. C'
    ELSE name
  END short_name
FROM teams

-- CASE
SELECT
  id,
  CASE
    WHEN (host_goals - guest_goals) < 0 THEN 'lost'
    WHEN (host_goals - guest_goals) = 0 THEN 'draw'
    ELSE 'won'
  END result
FROM matches

-- INSERT
INSERT INTO teams (id, name) VALUES (101, 'Toronto FC');
INSERT INTO teams (id, name) VALUES (101, 'Toronto FC'), (102, 'Montreal Impact');

-- UPDATE
UPDATE teams SET name = 'Esteghlal FC' WHERE id = 1001
UPDATE matches SET host_goals = 4, guest_goals = 0 WHERE host_id = 1001 AND guest_id = 1002

-- DELETE
DELETE FROM teams WHERE id = 1002
DELETE FROM matches WHERE host_goals = guest_goals
```

