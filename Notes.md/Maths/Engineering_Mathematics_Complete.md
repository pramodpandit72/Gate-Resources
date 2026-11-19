# GATE CSE – Engineering Mathematics: Complete Study Material

> Complete notes for the supplied Engineering Mathematics syllabus. This combined file contains all four parts. Separate topic files are also provided for easier study.


---

# GATE CSE – Engineering Mathematics
# Part 1: Discrete Mathematics

> Beginner-friendly notes progressing to GATE CSE level. The material follows the supplied syllabus: logic; sets, relations and functions; partial orders and lattices; monoids and groups; graphs; and combinatorics.

## How to use these notes

1. Learn the definition and the reason behind each property.
2. Work through the solved examples without looking at the solution first.
3. Memorise a formula only after understanding what it counts or represents.
4. Attempt the practice set and then check the detailed solutions.

## Syllabus checklist

- [ ] Propositional logic
- [ ] First-order logic
- [ ] Sets
- [ ] Relations
- [ ] Functions
- [ ] Partial orders and lattices
- [ ] Monoids and groups
- [ ] Graphs: connectivity, matching and colouring
- [ ] Combinatorics: counting
- [ ] Recurrence relations
- [ ] Generating functions

---

# 1. Logic

Logic gives rules for deciding whether a statement is true and whether a conclusion follows from given statements. It is used in digital circuits, program conditions, verification, databases and formal reasoning.

## 1.1 Propositions

A **proposition** is a declarative statement that has exactly one truth value: true (T) or false (F).

- “7 is prime” is a proposition and is true.
- “10 is odd” is a proposition and is false.
- “Close the door” is not a proposition because it is a command.
- “Is 5 greater than 2?” is a question, not a proposition.
- “x is greater than 2” is not yet a proposition when the value of `x` is unknown. It is an open statement or predicate.

A proposition is often represented by a letter such as `p`, `q` or `r`.

## 1.2 Logical connectives

| Symbol | Name | Meaning |
|---|---|---|
| `¬p` | NOT | True when `p` is false |
| `p ∧ q` | AND | True only when both are true |
| `p ∨ q` | OR (inclusive) | True when at least one is true |
| `p → q` | Implication | False only when `p` is true and `q` is false |
| `p ↔ q` | Biconditional | True when both have the same truth value |
| `p ⊕ q` | Exclusive OR | True when exactly one is true |

### Truth tables

| p | q | ¬p | p ∧ q | p ∨ q | p → q | p ↔ q | p ⊕ q |
|---|---|---|---|---|---|---|---|
| T | T | F | T | T | T | T | F |
| T | F | F | F | T | F | F | T |
| F | T | T | F | T | T | F | T |
| F | F | T | F | F | T | T | F |

**Important point about implication:** `p → q` does not say that `p` causes `q`. It only says that whenever `p` is true, `q` must also be true. When `p` is false, the implication is true.

### Solved example 1

**Question:** Find the truth value of `(p ∧ q) → p` for all possible values of `p` and `q`.

**Solution:**

| p | q | p ∧ q | (p ∧ q) → p |
|---|---|---|---|
| T | T | T | T |
| T | F | F | T |
| F | T | F | T |
| F | F | F | T |

The final column is always true. Therefore, the expression is a **tautology**.

## 1.3 Tautology, contradiction and contingency

- **Tautology:** true for every assignment of truth values. Example: `p ∨ ¬p`.
- **Contradiction:** false for every assignment. Example: `p ∧ ¬p`.
- **Contingency:** true for some assignments and false for others. Example: `p ∧ q`.

Two propositions are **logically equivalent** if their truth values match in every row of their truth table. Write `p ≡ q`.

## 1.4 Important logical equivalences

| Law | Equivalence |
|---|---|
| Double negation | `¬(¬p) ≡ p` |
| De Morgan | `¬(p ∧ q) ≡ ¬p ∨ ¬q` |
| De Morgan | `¬(p ∨ q) ≡ ¬p ∧ ¬q` |
| Implication | `p → q ≡ ¬p ∨ q` |
| Contrapositive | `p → q ≡ ¬q → ¬p` |
| Biconditional | `p ↔ q ≡ (p → q) ∧ (q → p)` |
| Commutative | `p ∧ q ≡ q ∧ p`; `p ∨ q ≡ q ∨ p` |
| Associative | `(p ∧ q) ∧ r ≡ p ∧ (q ∧ r)`; similarly for OR |
| Distributive | `p ∧ (q ∨ r) ≡ (p ∧ q) ∨ (p ∧ r)` |
| Distributive | `p ∨ (q ∧ r) ≡ (p ∨ q) ∧ (p ∨ r)` |
| Absorption | `p ∨ (p ∧ q) ≡ p`; `p ∧ (p ∨ q) ≡ p` |

### Converse, inverse and contrapositive

For the statement `p → q`:

- Converse: `q → p`.
- Inverse: `¬p → ¬q`.
- Contrapositive: `¬q → ¬p`.

The original statement is equivalent to its contrapositive, not necessarily to its converse or inverse.

**Example:** “If a number is divisible by 4, then it is even.” Its contrapositive is “If a number is not even, then it is not divisible by 4.” The converse (“if even, then divisible by 4”) is false.

## 1.5 Predicates and first-order logic

A **predicate** is a statement containing one or more variables. Its truth depends on the values assigned to those variables.

Example: `P(x): x > 5`.

If the domain is the set of integers, `P(8)` is true and `P(3)` is false.

A **domain of discourse** is the collection of values over which a variable ranges. Always identify the domain before interpreting a quantified statement.

### Quantifiers

| Symbol | Name | Meaning |
|---|---|---|
| `∀x P(x)` | Universal | P is true for every x in the domain |
| `∃x P(x)` | Existential | P is true for at least one x in the domain |
| `∃!x P(x)` | Unique existence | Exactly one x satisfies P |

### Negating quantified statements

- `¬(∀x P(x)) ≡ ∃x ¬P(x)`
- `¬(∃x P(x)) ≡ ∀x ¬P(x)`

In words: “not every” means “there is at least one that does not”; “there does not exist” means “every one fails.”

**Example:** Negate “Every student passed.” The correct negation is “There is at least one student who did not pass,” not “No student passed.”

### Nested quantifiers

The order of quantifiers can change the meaning.

- `∀x ∃y (x < y)` over integers: for every integer x, there is a larger integer y. This is true.
- `∃y ∀x (x < y)` over integers: there is one integer y larger than every integer x. This is false.

### Rules of inference

| Rule | Form |
|---|---|
| Modus ponens | `p`, `p → q` therefore `q` |
| Modus tollens | `¬q`, `p → q` therefore `¬p` |
| Hypothetical syllogism | `p → q`, `q → r` therefore `p → r` |
| Disjunctive syllogism | `p ∨ q`, `¬p` therefore `q` |
| Addition | `p` therefore `p ∨ q` |
| Simplification | `p ∧ q` therefore `p` |

An argument is **valid** when there is no assignment that makes all premises true and the conclusion false.

### Solved example 2

**Question:** Determine whether the argument is valid: `p → q`, `q → r`, `p`; therefore `r`.

**Solution:** From `p → q` and `p`, modus ponens gives `q`. From `q → r` and `q`, modus ponens gives `r`. Therefore, the argument is valid.

## 1.6 CNF and DNF

- A **literal** is a variable or its negation, such as `p` or `¬q`.
- **CNF (conjunctive normal form):** an AND of OR-clauses. Example: `(p ∨ q) ∧ (¬p ∨ r)`.
- **DNF (disjunctive normal form):** an OR of AND-terms. Example: `(p ∧ q) ∨ (¬p ∧ r)`.

To get a CNF or DNF, use equivalence laws, especially implication removal and De Morgan's laws. A truth-table method is also possible: DNF is formed from rows where the expression is true; CNF is formed from rows where it is false.

### GATE focus and common traps

- For `n` independent propositions, a full truth table has `2^n` rows.
- Implication is false in only one case: true premise and false conclusion.
- Negation must pass through a quantifier and change `∀` to `∃`, or `∃` to `∀`.
- Quantifier order matters.
- A statement and its contrapositive are equivalent; its converse need not be.

---

# 2. Sets

A **set** is a well-defined collection of distinct objects. The objects are called elements.

Example: `A = {1, 2, 3}`. The notation `2 ∈ A` means 2 belongs to A; `5 ∉ A` means 5 does not belong to A.

## 2.1 Basic set concepts

- Empty set: `∅`, containing no elements.
- Universal set: `U`, the complete collection under discussion.
- Subset: `A ⊆ B` when every element of A is in B.
- Proper subset: `A ⊂ B` when `A ⊆ B` and `A ≠ B`.
- Equal sets: `A = B` when they contain exactly the same elements.
- Power set: `P(A)`, the set of all subsets of A.
- Cartesian product: `A × B = {(a,b) : a ∈ A, b ∈ B}`.

If `|A| = n`, then `|P(A)| = 2^n`. If `|A| = m` and `|B| = n`, then `|A × B| = mn` for finite sets.

## 2.2 Set operations

| Operation | Definition |
|---|---|
| Union | `A ∪ B`: in A or B or both |
| Intersection | `A ∩ B`: in both A and B |
| Difference | `A − B`: in A but not in B |
| Complement | `Aᶜ = U − A` |
| Symmetric difference | `A △ B = (A − B) ∪ (B − A)` |

### Set identities

- `A ∪ ∅ = A`; `A ∩ U = A`.
- `A ∪ U = U`; `A ∩ ∅ = ∅`.
- `A ∪ A = A`; `A ∩ A = A`.
- `A ∪ Aᶜ = U`; `A ∩ Aᶜ = ∅`.
- `(A ∪ B)ᶜ = Aᶜ ∩ Bᶜ`.
- `(A ∩ B)ᶜ = Aᶜ ∪ Bᶜ`.
- `A − B = A ∩ Bᶜ`.

## 2.3 Cardinality and inclusion–exclusion

For finite sets, `|A|` is the number of elements in A.

For two sets:

`|A ∪ B| = |A| + |B| − |A ∩ B|`.

For three sets:

`|A ∪ B ∪ C| = |A| + |B| + |C| − |A ∩ B| − |A ∩ C| − |B ∩ C| + |A ∩ B ∩ C|`.

Subtract intersections because shared elements were counted more than once; add the triple intersection back because it was subtracted too many times.

### Solved example 3

**Question:** In a class of 60 students, 35 know C, 28 know Python and 15 know both. How many know at least one of the two languages?

**Solution:**

`|C ∪ P| = 35 + 28 − 15 = 48`.

Therefore, 48 students know at least one language. The number who know neither is `60 − 48 = 12`.

---

# 3. Relations

A **binary relation** from A to B is any subset of `A × B`. A relation on A is a subset of `A × A`.

If `(a,b) ∈ R`, we write `aRb`.

## 3.1 Properties of relations

For a relation R on set A:

| Property | Required condition |
|---|---|
| Reflexive | `aRa` for every `a ∈ A` |
| Irreflexive | `aRa` is false for every `a ∈ A` |
| Symmetric | `aRb ⇒ bRa` |
| Antisymmetric | `aRb` and `bRa ⇒ a=b` |
| Asymmetric | `aRb ⇒ not bRa`; it is irreflexive |
| Transitive | `aRb` and `bRc ⇒ aRc` |

**Do not confuse symmetric and antisymmetric.** A symmetric relation allows both directions. An antisymmetric relation allows both directions only when the elements are equal.

### Solved example 4

**Question:** On integers, define `aRb` if `a − b` is even. Identify its key properties.

**Solution:**

- Reflexive: `a − a = 0`, which is even.
- Symmetric: if `a − b` is even, then `b − a = −(a − b)` is also even.
- Transitive: if `a − b` and `b − c` are even, their sum `a − c` is even.

Thus, R is reflexive, symmetric and transitive. It is an **equivalence relation**.

## 3.2 Equivalence relations and equivalence classes

A relation that is reflexive, symmetric and transitive is an **equivalence relation**.

The equivalence class of a is `[a] = {x ∈ A : xRa}`. Equivalence classes form a partition: they are non-empty, pairwise disjoint and their union is A.

For the relation “same remainder when divided by 3” on integers, there are three equivalence classes: numbers congruent to 0, 1 and 2 modulo 3.

## 3.3 Closures

A closure is the smallest relation containing R that has a chosen property.

- Reflexive closure: add every missing `(a,a)` pair.
- Symmetric closure: add `(b,a)` whenever `(a,b)` is present.
- Transitive closure: add pairs required by transitivity. It can be found using reachability (for example, Warshall's algorithm on a finite relation graph).

A closure should add only what is necessary; it must not remove original pairs.

## 3.4 Relation representation

A finite relation can be shown as:

- Ordered pairs.
- A zero-one matrix, where entry `(i,j)` is 1 exactly when `a_i R a_j`.
- A directed graph, with an edge `a_i → a_j` for each related pair.

For a relation matrix M: reflexivity means all diagonal entries are 1; symmetry means `M = Mᵀ`; antisymmetry means no two distinct indices i,j have both `M[i,j]=1` and `M[j,i]=1`.

---

# 4. Functions

A function `f: A → B` assigns **exactly one** output in B to every input in A. A is the domain and B is the codomain. The range/image is the set of outputs actually produced.

## 4.1 Types of functions

- **Injective (one-to-one):** different inputs have different outputs. `f(a₁)=f(a₂) ⇒ a₁=a₂`.
- **Surjective (onto):** every element of the codomain is an output.
- **Bijective:** both injective and surjective.
- **Many-to-one:** at least two inputs can have the same output.
- **Into:** at least one codomain element is not reached.

A function has an inverse function `f⁻¹: B → A` exactly when it is bijective.

## 4.2 Composition

If `f: A → B` and `g: B → C`, then `(g ∘ f)(x) = g(f(x))`. Apply f first, then g.

Composition is associative: `h ∘ (g ∘ f) = (h ∘ g) ∘ f`, but it is generally not commutative.

### Solved example 5

**Question:** Let `f(x)=2x+1` and `g(x)=x²`. Find `g∘f` and `f∘g`.

**Solution:**

- `(g∘f)(x) = g(2x+1) = (2x+1)² = 4x²+4x+1`.
- `(f∘g)(x) = f(x²) = 2x²+1`.

The two compositions are different, so composition is not commutative in general.

## 4.3 Finite-set facts

For finite sets A and B:

- If `|A| > |B|`, no function from A to B can be injective (pigeonhole principle).
- If `|A| > |B|`, a function from A to B cannot be bijective.
- If `|A| = |B|`, an injective function from A to B is also surjective, and vice versa.

---

# 5. Partial Orders and Lattices

## 5.1 Partial order and poset

A relation `≤` on A is a **partial order** if it is reflexive, antisymmetric and transitive. A set together with a partial order is a **poset**.

Example: subset inclusion `⊆` on the power set of `{a,b}` is a partial order.

A partial order need not compare every pair. If for all a,b, either `a≤b` or `b≤a`, it is a **total (linear) order**.

## 5.2 Hasse diagrams

A Hasse diagram is a simplified drawing of a finite poset:

- Put smaller elements below larger elements.
- Omit self-loops (reflexive edges).
- Omit edges implied by transitivity.
- Draw only cover relations: `x` is covered by `y` when `x<y` and no z satisfies `x<z<y`.

## 5.3 Minimal, maximal, least and greatest elements

- **Minimal element:** no distinct element is below it.
- **Maximal element:** no distinct element is above it.
- **Least element:** it is below every element.
- **Greatest element:** it is above every element.

A least element, if it exists, is unique. A minimal element need not be unique. The same distinction applies to greatest and maximal.

A **lower bound** of a subset S is an element below every element of S. A **greatest lower bound (GLB)** is the largest such lower bound. An **upper bound** is above every element of S, and a **least upper bound (LUB)** is the smallest such upper bound.

## 5.4 Lattices

A poset is a **lattice** if every pair `a,b` has:

- a unique greatest lower bound, called the **meet**, written `a ∧ b`;
- a unique least upper bound, called the **join**, written `a ∨ b`.

For the power set `P(S)` ordered by subset inclusion:

- Meet is intersection: `A ∧ B = A ∩ B`.
- Join is union: `A ∨ B = A ∪ B`.
- Bottom element is `∅`; top element is S.

### Important lattice properties

- Idempotent: `a∨a=a`, `a∧a=a`.
- Commutative: `a∨b=b∨a`, `a∧b=b∧a`.
- Associative: grouping does not change the result.
- Absorption: `a∨(a∧b)=a`, `a∧(a∨b)=a`.
- Distributive lattice: meet distributes over join and join distributes over meet.
- Complemented lattice: every element has a complement relative to bottom and top.

A Boolean algebra is a complemented distributive lattice. The power set of a set, with union and intersection, is a standard example.

### Solved example 6

**Question:** In `P({a,b})` ordered by subset inclusion, find the meet and join of `{a}` and `{b}`.

**Solution:**

- Meet = intersection = `{a} ∩ {b} = ∅`.
- Join = union = `{a} ∪ {b} = {a,b}`.

The bottom is `∅` and the top is `{a,b}`.

### GATE focus

- A poset can have multiple minimal or maximal elements.
- A least/greatest element, when present, is unique.
- A poset is a lattice only if every pair has both a meet and a join.
- A finite chain is always a lattice; not every poset is a lattice.

---

# 6. Monoids and Groups

These structures describe sets with an operation that follows specified rules. They are useful in algebra, symmetry, automata and theoretical computer science.

## 6.1 Binary operation

A binary operation `*` on a set S combines any two elements of S and produces an element of S. This requirement is called **closure**.

Example: addition on integers is closed because the sum of two integers is an integer. Subtraction on natural numbers is not closed if zero or negative results are excluded.

## 6.2 Semigroup and monoid

A **semigroup** is a non-empty set with a closed, associative binary operation.

Associativity means `(a*b)*c = a*(b*c)` for all a,b,c.

A **monoid** is a semigroup that also has an identity element e satisfying `e*a = a*e = a` for every a.

Examples:

- Integers under addition form a monoid; identity is 0.
- Positive integers under multiplication form a monoid; identity is 1.
- Strings under concatenation form a monoid; identity is the empty string.

The identity element of a monoid is unique.

## 6.3 Groups

A **group** is a monoid in which every element has an inverse. For each a, there is an element `a⁻¹` such that `a*a⁻¹ = a⁻¹*a = e`.

A group is **abelian** (commutative) if `a*b = b*a` for every pair.

Examples:

- Integers under addition form an abelian group. Identity is 0 and inverse of a is −a.
- Non-zero real numbers under multiplication form an abelian group. Identity is 1 and inverse of a is `1/a`.
- Natural numbers under addition are not a group if negative numbers are not included, because most elements have no additive inverse in the set.

### Key properties

- Identity is unique.
- The inverse of each element is unique.
- `(a⁻¹)⁻¹ = a`.
- `(a*b)⁻¹ = b⁻¹*a⁻¹` (order reverses).
- Cancellation holds in a group: if `a*b=a*c`, then `b=c`.

## 6.4 Cyclic groups and order

A group is **cyclic** if one element generates every element by repeated operation. In additive notation, `⟨a⟩ = {na : n ∈ Z}`.

The **order of a group** is its number of elements when finite. The **order of an element** is the smallest positive number of repetitions that produces the identity.

### Structure comparison

| Structure | Closure | Associativity | Identity | Inverses |
|---|---:|---:|---:|---:|
| Magma (set with binary operation) | Yes | Not required | Not required | Not required |
| Semigroup | Yes | Yes | Not required | Not required |
| Monoid | Yes | Yes | Yes | Not required |
| Group | Yes | Yes | Yes | Every element |
| Abelian group | Yes | Yes | Yes | Every element; operation commutative |

### Solved example 7

**Question:** Do the integers under subtraction form a group?

**Solution:** Subtraction is closed on integers, but it is not associative:

`(5−3)−1 = 1`, while `5−(3−1)=3`.

Since associativity fails, integers under subtraction do not form a semigroup, monoid or group.

---

# 7. Graphs

A graph represents objects and connections. It is used in networks, routing, dependencies, social networks and scheduling.

A graph is written `G=(V,E)`, where V is the set of vertices (nodes) and E is the set of edges.

## 7.1 Basic graph terms

- **Undirected graph:** edges have no direction.
- **Directed graph (digraph):** edges are ordered pairs.
- **Simple graph:** no self-loops and no multiple edges.
- **Degree:** number of edges incident on a vertex in an undirected graph.
- **Isolated vertex:** degree 0.
- **Pendant/leaf vertex:** degree 1.
- **Walk:** sequence of adjacent vertices; repetition is allowed.
- **Trail:** walk with no repeated edge.
- **Path:** walk with no repeated vertex (under the usual simple-path convention).
- **Cycle:** closed path.
- **Connected graph:** every pair of vertices has a path between them.
- **Component:** a maximal connected subgraph.

For a directed graph, indegree counts incoming edges and outdegree counts outgoing edges.

## 7.2 Degree sum theorem

For every finite undirected graph:

`Σ(deg(v)) = 2|E|`.

Each edge contributes 1 to the degree of each endpoint, so it is counted twice. Therefore, the number of odd-degree vertices is always even.

For a directed graph:

`Σ indegree(v) = Σ outdegree(v) = |E|`.

### Solved example 8

**Question:** A graph has 5 vertices with degrees 3, 3, 2, 2 and 2. How many edges does it have?

**Solution:** Degree sum = `3+3+2+2+2 = 12`. By the degree sum theorem, `2|E|=12`, so `|E|=6`.

## 7.3 Connectivity

A graph is connected if a path exists between every pair of vertices. Removing a vertex or edge may disconnect it.

- **Bridge (cut-edge):** an edge whose removal increases the number of connected components.
- **Articulation point (cut-vertex):** a vertex whose removal (along with its incident edges) increases the number of components.
- **Vertex connectivity:** minimum number of vertices whose removal disconnects the graph (with standard special-case conventions).
- **Edge connectivity:** minimum number of edges whose removal disconnects the graph.

For a connected graph, a bridge cannot lie on any cycle. Conversely, an edge on a cycle is not a bridge.

A tree is a connected, acyclic, undirected graph. A tree with n vertices has exactly `n−1` edges. Between every pair of vertices in a tree, there is exactly one simple path.

## 7.4 Matching

A **matching** is a set of edges with no shared endpoints. A vertex is matched if it is an endpoint of a selected matching edge.

- **Maximum matching:** a matching with the largest possible number of edges.
- **Maximal matching:** a matching to which no additional edge can be added. A maximal matching need not be maximum.
- **Perfect matching:** every vertex is matched.

A graph is **bipartite** if its vertices can be divided into two disjoint sets such that every edge joins vertices from different sets.

A graph is bipartite if and only if it has no odd cycle.

### Hall's marriage theorem

For a finite bipartite graph with sides X and Y, there is a matching that matches every vertex of X if and only if, for every subset `S ⊆ X`, the neighbourhood N(S) satisfies `|N(S)| ≥ |S|`.

This condition checks whether every group of vertices on one side collectively has enough possible partners.

### Solved example 9

**Question:** Can a bipartite graph with parts X and Y, where `|X|=4` and `|Y|=3`, have a perfect matching?

**Solution:** A perfect matching must match every vertex on both sides. Each matching edge uses one vertex from each side. Since the side sizes differ, one vertex on X must remain unmatched. Therefore, a perfect matching is impossible. A matching that covers all four vertices of X is also impossible because Y has only three vertices.

## 7.5 Graph colouring

A **proper vertex colouring** assigns colours to vertices so that adjacent vertices have different colours.

The smallest number of colours needed is the **chromatic number**, written `χ(G)`.

Key facts:

- An edgeless graph with at least one vertex has chromatic number 1.
- A non-empty bipartite graph has chromatic number at most 2; it needs 1 if it has no edges and 2 if it has an edge.
- A complete graph `K_n` has `χ(K_n)=n`.
- A cycle with an even number of vertices has chromatic number 2.
- A cycle with an odd number of vertices has chromatic number 3.
- A graph containing a clique of size k needs at least k colours.

**Greedy colouring** colours vertices one at a time using the smallest available colour. It gives a valid colouring, but may not use the minimum possible number of colours.

### Solved example 10

**Question:** Find the chromatic number of a triangle `K₃`.

**Solution:** Every pair of its three vertices is adjacent. Therefore, no two vertices can share a colour. Three colours are necessary and sufficient, so `χ(K₃)=3`.

### GATE focus and common traps

- Sum of degrees is twice the number of edges in an undirected graph.
- The number of odd-degree vertices is even.
- Connectedness is about paths, not direct edges.
- A maximal matching is not necessarily maximum.
- A bipartite graph has no odd cycle; an even cycle is allowed.
- Greedy colouring does not always find the chromatic number.

---

# 8. Combinatorics: Counting

Combinatorics counts arrangements and selections without listing every possibility.

## 8.1 Addition and multiplication principles

- **Addition principle:** if one task can be done in m ways and a mutually exclusive alternative in n ways, the total is `m+n`.
- **Multiplication principle:** if a process has successive stages with m, n, ... choices, multiply the numbers of choices: `m×n×...`.

### Factorial

For a non-negative integer n:

`n! = n(n−1)(n−2)...2·1`, and `0! = 1`.

## 8.2 Permutations and combinations

A permutation is an arrangement where order matters. A combination is a selection where order does not matter.

- Permutations of n distinct objects taken r at a time: `P(n,r)=n!/(n−r)!`.
- Combinations of n distinct objects taken r at a time: `C(n,r)=n!/[r!(n−r)!]`.
- Relation: `P(n,r)=C(n,r)r!`.

With repetition allowed, the number of length-r sequences from n choices is `n^r`.

For arrangements of n objects where some are identical, if multiplicities are `n₁,n₂,...,n_k`, the number of distinct arrangements is:

`n!/(n₁! n₂! ... n_k!)`.

For circular arrangements of n distinct objects, when rotations are considered the same, the number is `(n−1)!`. If reflections are also treated as the same, additional care is needed; for n distinct objects with rotations and reflections equivalent, the count is `n!/ (2n)` for n≥3.

## 8.3 Binomial theorem

`(x+y)^n = Σ[k=0 to n] C(n,k)x^(n−k)y^k`.

Useful identities:

- `C(n,r)=C(n,n−r)`.
- `C(n,r)+C(n,r−1)=C(n+1,r)`.
- `Σ C(n,r) = 2^n`.

## 8.4 Pigeonhole principle

If N objects are placed into k boxes, at least one box contains at least `ceil(N/k)` objects.

In particular, if more than k objects are placed into k boxes, at least one box contains at least two objects.

### Solved example 11

**Question:** How many 4-digit PINs can be made using digits 0–9 if repetition is allowed?

**Solution:** Each of the four positions has 10 choices. Leading zero is allowed for a PIN. Total = `10⁴ = 10,000`.

### Solved example 12

**Question:** From 8 students, how many different committees of 3 can be selected?

**Solution:** Order does not matter, so use combinations:

`C(8,3) = 8!/(3!5!) = (8×7×6)/(3×2×1)=56`.

## 8.5 Inclusion–exclusion in counting

Use inclusion–exclusion when categories overlap. For two finite sets:

`|A∪B|=|A|+|B|−|A∩B|`.

For three sets, add the individual sizes, subtract pairwise intersections and add the triple intersection.

## 8.6 Derangements (useful extension)

A **derangement** is a permutation in which no object remains in its original position. The number is:

`!n = n! (1 − 1/1! + 1/2! − 1/3! + ... + (−1)^n/n!)`.

This follows from inclusion–exclusion. For example, `!3 = 2`.

---

# 9. Recurrence Relations

A recurrence relation defines a sequence using earlier terms. It is useful for analysing recursive algorithms and counting recursive structures.

Example: Fibonacci sequence: `F₀=0`, `F₁=1`, and `Fₙ=Fₙ₋₁+Fₙ₋₂` for n≥2.

## 9.1 Types

- **Order:** how many previous terms are used. `aₙ=3aₙ₋₁+2` is first order; `aₙ=aₙ₋₁+aₙ₋₂` is second order.
- **Linear:** sequence terms appear to the first power and are not multiplied together.
- **Homogeneous:** no separate forcing term, e.g. `aₙ−5aₙ₋₁+6aₙ₋₂=0`.
- **Non-homogeneous:** has a non-zero forcing term, e.g. `aₙ−2aₙ₋₁=3`.
- **Constant coefficients:** coefficients do not depend on n.

Initial conditions are needed to determine a unique sequence.

## 9.2 First-order recurrence

For `aₙ = r aₙ₋₁`, with `a₀=c`, repeated substitution gives `aₙ=crⁿ`.

For `aₙ = aₙ₋₁ + d`, with `a₀=c`, we get `aₙ=c+nd`.

## 9.3 Characteristic equation method

For a homogeneous linear recurrence with constant coefficients:

`aₙ + c₁aₙ₋₁ + ... + c_kaₙ₋k = 0`,

assume a solution `aₙ=rⁿ` and form the characteristic equation:

`r^k + c₁r^(k−1) + ... + c_k = 0`.

- Distinct roots `r₁,...,r_k`: `aₙ = A₁r₁ⁿ + ... + A_kr_kⁿ`.
- A root r repeated m times contributes `(A₀ + A₁n + ... + A_(m−1)n^(m−1))rⁿ`.
- Use initial conditions to find the constants.

### Solved example 13

**Question:** Solve `aₙ = 5aₙ₋₁ − 6aₙ₋₂`, with `a₀=2`, `a₁=5`.

**Solution:** Rearrange: `aₙ−5aₙ₋₁+6aₙ₋₂=0`.

Characteristic equation: `r²−5r+6=0=(r−2)(r−3)`.

Roots are 2 and 3, so `aₙ=A2ⁿ+B3ⁿ`.

Using `a₀=2`: `A+B=2`.

Using `a₁=5`: `2A+3B=5`.

Subtract twice the first equation from the second: `B=1`, hence `A=1`.

Therefore, `aₙ=2ⁿ+3ⁿ`.

## 9.4 Non-homogeneous recurrence

A common method is:

1. Solve the associated homogeneous recurrence to get the complementary solution.
2. Guess a particular solution based on the forcing term.
3. If the guess duplicates a homogeneous term, multiply it by n (and by a higher power if necessary).
4. Add the two parts and apply initial conditions.

For a constant forcing term, first try a constant particular solution. For a polynomial forcing term, try a polynomial of the same degree. This is a method to try, not a guarantee that the first guess works.

## 9.5 Recurrences in algorithm analysis

For example, merge sort satisfies approximately `T(n)=2T(n/2)+cn`, with `T(1)=d`. Its solution is `Θ(n log n)`. This example connects recurrence solving with algorithm running time.

---

# 10. Generating Functions

A **generating function** represents a sequence as coefficients of a power series.

For sequence `a₀,a₁,a₂,...`, its ordinary generating function (OGF) is:

`A(x)=a₀+a₁x+a₂x²+... = Σ[n≥0] aₙxⁿ`.

The coefficient of `xⁿ` in A(x) is `aₙ`.

## 10.1 Standard generating functions

| Sequence | Ordinary generating function |
|---|---|
| `1,1,1,1,...` | `1/(1−x)` |
| `1,r,r²,r³,...` | `1/(1−rx)` |
| `0,1,2,3,...` | `x/(1−x)²` |
| `1,2,3,4,...` | `1/(1−x)²` |
| `1,0,0,0,...` | `1` |

These formulas are interpreted as formal power series; analytically, the geometric series also converges for suitable x.

## 10.2 Useful operations

- Addition: `A(x)+B(x)` adds corresponding sequence terms.
- Scaling: `cA(x)` multiplies every term by c.
- Shift: multiplication by x shifts coefficients one position to the right.
- Differentiation: `A'(x)=Σ[n≥1] n aₙ x^(n−1)`.
- Multiplication: coefficients are convolved. If `C(x)=A(x)B(x)`, then `cₙ=Σ[k=0 to n]a_k b_(n−k)`.

## 10.3 Solving a recurrence using a generating function

The usual steps are:

1. Define `A(x)=Σaₙxⁿ`.
2. Multiply the recurrence by `xⁿ` and sum over valid n.
3. Rewrite shifted sums in terms of A(x), separating initial terms.
4. Solve algebraically for A(x).
5. Expand into known power series or use partial fractions to extract `aₙ`.

### Solved example 14

**Question:** Find the OGF of the sequence `aₙ=1` for all n≥0.

**Solution:**

`A(x)=1+x+x²+x³+...`.

This is a geometric series with first term 1 and ratio x, so `A(x)=1/(1−x)`.

### Solved example 15

**Question:** Find the OGF of `aₙ=n` for n≥0.

**Solution:** Start from `1+x+x²+...=1/(1−x)`. Differentiate:

`1+2x+3x²+... = 1/(1−x)²`.

Multiplying by x gives `x+2x²+3x³+... = x/(1−x)²`, whose coefficient of `xⁿ` is n. Hence `A(x)=x/(1−x)²`.

---

# 11. Quick Revision Sheet

## Logic

- `p→q ≡ ¬p∨q ≡ ¬q→¬p`.
- `¬(p∧q) ≡ ¬p∨¬q`; `¬(p∨q) ≡ ¬p∧¬q`.
- `¬∀xP(x) ≡ ∃x¬P(x)`; `¬∃xP(x) ≡ ∀x¬P(x)`.
- Tautology: always true; contradiction: always false.

## Sets, relations and functions

- `|A∪B|=|A|+|B|−|A∩B|`.
- `|P(A)|=2^|A|` for finite A.
- Equivalence relation = reflexive + symmetric + transitive.
- Partial order = reflexive + antisymmetric + transitive.
- Bijective ⇔ inverse function exists.

## Orders and algebraic structures

- Lattice: every pair has a meet and join.
- Monoid = associative operation + identity.
- Group = monoid + inverse for every element.
- Abelian group additionally has commutativity.

## Graphs and counting

- `Σdeg(v)=2|E|` for undirected graphs.
- Number of odd-degree vertices is even.
- Tree with n vertices has n−1 edges.
- Bipartite ⇔ no odd cycle.
- `P(n,r)=n!/(n−r)!`; `C(n,r)=n!/[r!(n−r)!]`.
- Pigeonhole: some box has at least `ceil(N/k)` objects.

## Recurrences and generating functions

- For distinct characteristic roots, combine `A r₁ⁿ + B r₂ⁿ + ...`.
- Repeated root r of multiplicity m gives polynomial-in-n factor of degree m−1 times `rⁿ`.
- OGF: `A(x)=Σaₙxⁿ`.
- `1,1,1,... ↔ 1/(1−x)`; `0,1,2,... ↔ x/(1−x)²`.

---

# 12. Practice Questions

Try all questions before reading the answer key. Unless specified, assume standard finite sets and ordinary undirected simple graphs.

### Q1 – MCQ (Logic)

Which expression is logically equivalent to `p → q`?

A. `p ∧ q`  B. `¬p ∨ q`  C. `p ∨ ¬q`  D. `¬p ∧ q`

### Q2 – MSQ (First-order logic)

Which statements are equivalent to the negation of `∀x P(x)`?

A. `∃x ¬P(x)`  B. `∀x ¬P(x)`  C. “At least one x does not satisfy P”  D. “No x satisfies P”

### Q3 – NAT (Sets)

A set has 5 elements. How many elements does its power set have?

### Q4 – MCQ (Relations)

A relation that is reflexive, symmetric and transitive is called:

A. Partial order  B. Equivalence relation  C. Asymmetric relation  D. Function

### Q5 – NAT (Functions)

How many functions are there from a 3-element set to a 2-element set?

### Q6 – MCQ (Posets)

Which statement is always true?

A. Every poset is a total order.
B. Every maximal element is a greatest element.
C. A least element, if it exists, is unique.
D. Every poset is a lattice.

### Q7 – NAT (Lattice)

In the power-set lattice of `{a,b,c}`, what is the meet of `{a,b}` and `{b,c}`? Enter the number of elements in the result.

### Q8 – MCQ (Algebraic structures)

Which structure requires an identity and an inverse for every element?

A. Semigroup  B. Monoid  C. Group  D. Magma

### Q9 – NAT (Graphs)

An undirected graph has degree sequence `4,3,3,2,2,2`. Find the number of edges.

### Q10 – MCQ (Matching)

Which statement is correct?

A. Every maximal matching is maximum.
B. A perfect matching covers every vertex.
C. A matching can contain two edges sharing a vertex.
D. A bipartite graph must contain an odd cycle.

### Q11 – MCQ (Colouring)

The chromatic number of a cycle with 7 vertices is:

A. 1  B. 2  C. 3  D. 7

### Q12 – NAT (Counting)

How many ways can 2 students be selected from 7 students?

### Q13 – NAT (Recurrence)

For `aₙ=3aₙ₋₁`, with `a₀=2`, find `a₄`.

### Q14 – NAT (Generating function)

What is the coefficient of `x⁵` in `1/(1−x)`?

### Q15 – Difficult (Recurrence)

Solve `aₙ−4aₙ₋₁+4aₙ₋₂=0`, with `a₀=1`, `a₁=4`.

---

# 13. Answer Key with Solutions

### A1

**Answer: B.** `p→q` is false only when p is true and q is false. `¬p∨q` has exactly the same truth values, so they are equivalent.

### A2

**Answers: A and C.** The quantifier-negation rule gives `¬(∀xP(x)) ≡ ∃x¬P(x)`. This means at least one domain element fails P. “No x satisfies P” is stronger and corresponds to `∀x¬P(x)`.

### A3

**Answer: 32.** A set of n elements has `2ⁿ` subsets. Thus `2⁵=32`.

### A4

**Answer: B.** Reflexive, symmetric and transitive are exactly the three requirements for an equivalence relation.

### A5

**Answer: 8.** Each of the 3 domain elements can independently map to either of 2 codomain elements. Total functions = `2³=8`.

### A6

**Answer: C.** If two least elements existed, each would be below the other. Antisymmetry would force them to be equal. Maximal and greatest are different notions.

### A7

**Answer: 1.** Meet in a power-set lattice is intersection: `{a,b}∩{b,c}={b}`, which has one element.

### A8

**Answer: C.** A group has closure, associativity, identity and an inverse for every element.

### A9

**Answer: 8.** Degree sum is `4+3+3+2+2+2=16`. The number of edges is `16/2=8`.

### A10

**Answer: B.** A perfect matching is a matching that covers every vertex. Maximal only means no more edge can be added; it need not be largest.

### A11

**Answer: C.** An odd cycle cannot be coloured with two colours. Three colours are sufficient for every odd cycle, so the answer is 3.

### A12

**Answer: 21.** Order does not matter: `C(7,2)=7×6/(2×1)=21`.

### A13

**Answer: 162.** `aₙ=2×3ⁿ`; therefore `a₄=2×81=162`.

### A14

**Answer: 1.** `1/(1−x)=1+x+x²+x³+...`; every coefficient is 1.

### A15

**Answer:** `aₙ=(1+ n)2ⁿ`.

**Solution:** The characteristic equation is `r²−4r+4=0=(r−2)²`. Since r=2 is a repeated root, the general solution is `(A+Bn)2ⁿ`.

From `a₀=1`, A=1.

From `a₁=4`, `(1+B)2=4`, so B=1.

Therefore, `aₙ=(1+n)2ⁿ`.

---

## Final GATE preparation advice

- Build truth tables carefully; do not guess implication values.
- For relations, check each property using its exact definition and a counterexample.
- For posets, distinguish minimal/maximal from least/greatest.
- For algebraic structures, test associativity before identity and inverses.
- For graphs, use the degree sum theorem and check odd-cycle conditions.
- For counting, decide first whether order matters and whether repetition is allowed.
- For recurrence relations, write the characteristic equation correctly and apply every initial condition.
- For generating functions, identify the sequence coefficients before manipulating the power series.


---

# GATE CSE – Engineering Mathematics
# Part 2: Linear Algebra

> Beginner-friendly notes progressing to GATE CSE level. Scope: matrices, determinants, systems of linear equations, eigenvalues and eigenvectors, and LU decomposition.

## Syllabus checklist

- [ ] Matrix basics, types and operations
- [ ] Determinants and their properties
- [ ] System of linear equations
- [ ] Rank and consistency (essential tools for systems)
- [ ] Eigenvalues and eigenvectors
- [ ] LU decomposition

---

# 1. Matrices

A **matrix** is a rectangular arrangement of numbers in rows and columns. A matrix with m rows and n columns has order `m×n`.

Example:

`A = [[1, 2, 3], [4, 5, 6]]`

This is a `2×3` matrix. Its element in row i and column j is written `aᵢⱼ`.

Matrices are used to represent systems of equations, transformations, graphs, data and linear operations.

## 1.1 Types of matrices

| Type | Meaning |
|---|---|
| Row matrix | One row |
| Column matrix | One column |
| Rectangular | Rows ≠ columns |
| Square | Rows = columns |
| Zero matrix | Every entry is 0 |
| Diagonal | Square; all off-diagonal entries are 0 |
| Scalar | Diagonal with equal diagonal entries |
| Identity `I` | Diagonal entries 1, others 0 |
| Upper triangular | Entries below main diagonal are 0 |
| Lower triangular | Entries above main diagonal are 0 |
| Symmetric | `Aᵀ=A` |
| Skew-symmetric | `Aᵀ=−A` |
| Singular | Square matrix with determinant 0 |
| Non-singular | Square matrix with non-zero determinant |

For a real skew-symmetric matrix, all diagonal entries are zero because `aᵢᵢ=−aᵢᵢ`.

## 1.2 Matrix equality and operations

Two matrices are equal when they have the same order and corresponding entries are equal.

- Addition/subtraction: possible only for matrices of the same order; operate entry by entry.
- Scalar multiplication: multiply every entry by the scalar.
- Matrix multiplication: if A is `m×n` and B is `n×p`, then AB exists and has order `m×p`.

The entry in row i, column j of AB is:

`(AB)ᵢⱼ = Σ[k=1 to n] aᵢₖ bₖⱼ`.

**Matrix multiplication is generally not commutative:** `AB` need not equal `BA`. Even if both products exist, their values or dimensions may differ.

### Solved example 1

**Question:** Let `A=[[1,2],[3,4]]` and `B=[[2,0],[1,5]]`. Find AB.

**Solution:**

- First row, first column: `1×2 + 2×1 = 4`.
- First row, second column: `1×0 + 2×5 = 10`.
- Second row, first column: `3×2 + 4×1 = 10`.
- Second row, second column: `3×0 + 4×5 = 20`.

Therefore, `AB=[[4,10],[10,20]]`.

## 1.3 Transpose

The transpose `Aᵀ` is obtained by converting rows into columns.

Properties:

- `(Aᵀ)ᵀ=A`.
- `(A+B)ᵀ=Aᵀ+Bᵀ`.
- `(kA)ᵀ=kAᵀ`.
- `(AB)ᵀ=BᵀAᵀ` (the order reverses).

Every square matrix A can be decomposed as the sum of a symmetric and a skew-symmetric matrix:

`A = (A+Aᵀ)/2 + (A−Aᵀ)/2`.

## 1.4 Inverse of a matrix

For a square matrix A, its inverse `A⁻¹` satisfies:

`AA⁻¹=A⁻¹A=I`.

A matrix has an inverse if and only if it is non-singular, equivalently `det(A)≠0`.

For a 2×2 matrix:

`A=[[a,b],[c,d]]`,

`A⁻¹ = (1/(ad−bc)) [[d,−b],[−c,a]]`, provided `ad−bc ≠ 0`.

Properties:

- `(A⁻¹)⁻¹=A`.
- `(AB)⁻¹=B⁻¹A⁻¹` when both inverses exist.
- `(Aᵀ)⁻¹=(A⁻¹)ᵀ`.
- `(kA)⁻¹=(1/k)A⁻¹` for non-zero k.

---

# 2. Determinants

A **determinant** is a scalar associated with a square matrix. It helps identify invertibility and solve linear systems.

## 2.1 Determinant of a 2×2 matrix

For `A=[[a,b],[c,d]]`:

`det(A)=ad−bc`.

For a 3×3 matrix, expand along a row or column using cofactors. For row i:

`det(A)=Σ[j=1 to n] aᵢⱼ Cᵢⱼ`,

where `Cᵢⱼ=(−1)^(i+j) Mᵢⱼ` and `Mᵢⱼ` is the minor obtained by deleting row i and column j.

The cofactor signs follow a checkerboard pattern:

`+ − + ...`

`− + − ...`

`+ − + ...`

## 2.2 Important determinant properties

- `det(Aᵀ)=det(A)`.
- Swapping two rows (or columns) changes the sign.
- Multiplying one row by k multiplies the determinant by k.
- Adding a multiple of one row to another row does not change the determinant.
- If two rows (or columns) are equal or proportional, determinant is 0.
- A zero row or column makes the determinant 0.
- For triangular matrices, determinant is the product of diagonal entries.
- `det(AB)=det(A)det(B)` for square matrices of the same order.
- `det(I)=1`.
- `det(A⁻¹)=1/det(A)` when A is invertible.
- For an n×n matrix, `det(kA)=kⁿdet(A)`.

### Solved example 2

**Question:** Find the determinant of `A=[[2,3],[1,4]]`.

**Solution:** `det(A)=2×4−3×1=8−3=5`.

Since the determinant is non-zero, A is invertible.

### Solved example 3

**Question:** A 3×3 upper triangular matrix has diagonal entries 2, −1 and 4. Find its determinant.

**Solution:** For a triangular matrix, multiply the diagonal entries: `2×(−1)×4 = −8`.

---

# 3. Systems of Linear Equations

A linear equation in variables `x₁,...,xₙ` has the form `a₁x₁+...+aₙxₙ=b`, where the coefficients are constants.

A system of m equations in n unknowns can be written as:

`Ax=b`,

where A is the coefficient matrix, x is the variable column vector and b is the constants vector.

The **augmented matrix** is `[A | b]`.

## 3.1 Possible numbers of solutions

A system may have:

1. Exactly one solution (consistent and unique).
2. Infinitely many solutions (consistent with free variables).
3. No solution (inconsistent).

A system is **homogeneous** if `Ax=0`. It always has the trivial solution `x=0`. It has non-trivial solutions if the null space contains a non-zero vector; for an n×n matrix, this happens exactly when `det(A)=0`.

## 3.2 Gaussian elimination

Gaussian elimination transforms the augmented matrix using elementary row operations:

1. Swap two rows.
2. Multiply a row by a non-zero scalar.
3. Add a multiple of one row to another row.

The goal is row-echelon form. Then use back-substitution.

A row such as `[0 0 0 | 5]` represents `0=5`, so the system is inconsistent.

### Solved example 4

**Question:** Solve `x+y=5` and `2x−y=1`.

**Solution:** Add the equations: `3x=6`, so `x=2`. Substitute into `x+y=5`: `2+y=5`, so `y=3`. The unique solution is `(2,3)`.

### Solved example 5

**Question:** Determine whether the equations `x+y=2` and `2x+2y=5` are consistent.

**Solution:** Doubling the first equation gives `2x+2y=4`, but the second says `2x+2y=5`. This is a contradiction, so there is no solution.

## 3.3 Rank and consistency

The **rank** of a matrix is the maximum number of linearly independent rows or columns. It is also the number of pivots in row-echelon form.

For `Ax=b`, the Rouché–Capelli consistency condition is:

`rank(A) = rank([A|b])`.

If the ranks differ, there is no solution.

If the ranks are equal to r:

- Unique solution when `r=n` (number of unknowns).
- Infinitely many solutions when `r<n`.

This assumes the ordinary finite-dimensional linear system over a field such as the real numbers.

### Rank example

If A has 3 columns and `rank(A)=rank([A|b])=2`, the system is consistent and has `3−2=1` free variable, hence infinitely many solutions.

## 3.4 Cramer's rule

For a square system `Ax=b` with `det(A)≠0`:

`xᵢ = det(Aᵢ)/det(A)`,

where Aᵢ is obtained by replacing column i of A with b.

Cramer's rule is useful for small systems and theoretical questions. For large systems, elimination or factorisation is usually more efficient.

## 3.5 Inverse method

If A is square and invertible, then:

`x=A⁻¹b`.

The inverse method is not available when A is singular. A singular system may still be consistent, but it cannot have a unique solution.

---

# 4. Eigenvalues and Eigenvectors

An eigenvector of a square matrix A is a non-zero vector v whose direction is unchanged by multiplication by A; only its scale changes.

`Av = λv`, where v≠0.

λ is the **eigenvalue** and v is the corresponding **eigenvector**.

Rearrange:

`(A−λI)v=0`.

For a non-zero solution v to exist, `A−λI` must be singular:

`det(A−λI)=0`.

This is the **characteristic equation**.

## 4.1 Finding eigenvalues

Steps:

1. Form `A−λI`.
2. Calculate `det(A−λI)`.
3. Set the determinant equal to zero.
4. Solve for λ.

The roots are the eigenvalues, counted with algebraic multiplicity.

For a 2×2 matrix `[[a,b],[c,d]]`, the characteristic polynomial is:

`λ² − (a+d)λ + (ad−bc)`.

Thus, the sum of the two eigenvalues (counting multiplicity) is the trace `a+d`, and their product is the determinant `ad−bc`.

## 4.2 Finding eigenvectors

For each eigenvalue λ, solve:

`(A−λI)v=0`.

This is a homogeneous system. Any non-zero solution is an eigenvector. All scalar multiples of an eigenvector are also eigenvectors, except the zero vector.

### Solved example 6

**Question:** Find the eigenvalues and one eigenvector for each eigenvalue of `A=[[2,0],[0,3]]`.

**Solution:**

`det(A−λI) = (2−λ)(3−λ)=0`.

Eigenvalues are λ=2 and λ=3.

- For λ=2: `(A−2I)v=0` gives `[[0,0],[0,1]][x,y]ᵀ=0`, so y=0. Choose v=`[1,0]ᵀ`.
- For λ=3: `(A−3I)v=0` gives `[[−1,0],[0,0]][x,y]ᵀ=0`, so x=0. Choose v=`[0,1]ᵀ`.

## 4.3 Important eigenvalue properties

For an n×n matrix, with eigenvalues counted with algebraic multiplicity:

- Sum of eigenvalues = `trace(A)`.
- Product of eigenvalues = `det(A)`.
- A is singular iff 0 is an eigenvalue.
- If A is triangular, its eigenvalues are its diagonal entries.
- If λ is an eigenvalue of A, then `λᵏ` is an eigenvalue of `Aᵏ` for positive integer k.
- If A is invertible, `1/λ` is an eigenvalue of `A⁻¹`.
- If c is a scalar, `cλ` is an eigenvalue of `cA`.
- Similar matrices have the same characteristic polynomial and eigenvalues.

For a real symmetric matrix, all eigenvalues are real, and eigenvectors associated with distinct eigenvalues are orthogonal.

## 4.4 Algebraic and geometric multiplicity

- **Algebraic multiplicity:** how many times λ appears as a root of the characteristic polynomial.
- **Geometric multiplicity:** dimension of the eigenspace `N(A−λI)`.

For every eigenvalue:

`1 ≤ geometric multiplicity ≤ algebraic multiplicity`.

A matrix is diagonalizable when it has enough linearly independent eigenvectors to form a basis. An n×n matrix with n linearly independent eigenvectors can be written `A=PDP⁻¹`, where D is diagonal.

---

# 5. LU Decomposition

LU decomposition factors a square matrix A into:

`A=LU`,

where L is lower triangular and U is upper triangular. It helps solve systems efficiently, especially when the same A is used with many different right-hand-side vectors.

Different conventions are used:

- **Doolittle:** diagonal entries of L are 1.
- **Crout:** diagonal entries of U are 1.

Some matrices require row exchanges. Then the factorisation is commonly written `PA=LU`, where P is a permutation matrix recording the row swaps.

## 5.1 Doolittle method

For a 3×3 matrix, assume:

`L = [[1,0,0],[l21,1,0],[l31,l32,1]]`

`U = [[u11,u12,u13],[0,u22,u23],[0,0,u33]]`.

Multiply L and U and equate corresponding entries with A to determine the unknowns.

### Solved example 7

**Question:** Find an LU decomposition of `A=[[2,1],[4,3]]` using Doolittle's convention.

**Solution:** Let

`L=[[1,0],[l21,1]]`, `U=[[u11,u12],[0,u22]]`.

Multiplying gives `LU=[[u11,u12],[l21u11,l21u12+u22]]`.

Compare with A:

- `u11=2`.
- `u12=1`.
- `l21×2=4`, so `l21=2`.
- `2×1+u22=3`, so `u22=1`.

Therefore,

`L=[[1,0],[2,1]]`, `U=[[2,1],[0,1]]`.

Check: `LU=[[2,1],[4,3]]=A`.

## 5.2 Solving Ax=b using LU

Given `A=LU`, solve in two triangular steps:

1. Solve `Ly=b` using forward substitution.
2. Solve `Ux=y` using back substitution.

### Solved example 8

**Question:** Use the LU decomposition from Example 7 to solve `Ax=[5,11]ᵀ`.

**Solution:** We have:

`L=[[1,0],[2,1]]`, `U=[[2,1],[0,1]]`.

First solve `Ly=b`:

- `y₁=5`.
- `2y₁+y₂=11`, so `10+y₂=11`, hence `y₂=1`.

Now solve `Ux=y`:

- `x₂=1`.
- `2x₁+x₂=5`, so `2x₁+1=5`, hence `x₁=2`.

Therefore, `x=[2,1]ᵀ`.

## 5.3 When pivoting is needed

If the next pivot is zero, or numerically very small, a row exchange may be required. A zero pivot cannot be used for division. Pivoting improves numerical stability and is represented by a permutation matrix P in `PA=LU`.

---

# 6. Quick Revision Sheet

- Matrix product AB exists only when columns of A = rows of B.
- `(AB)ᵀ=BᵀAᵀ`; `(AB)⁻¹=B⁻¹A⁻¹`.
- A is invertible iff `det(A)≠0` iff `rank(A)=n` for an n×n matrix.
- `det(AB)=det(A)det(B)`.
- Triangular determinant = product of diagonal entries.
- `Ax=b` is consistent iff `rank(A)=rank([A|b])`.
- If consistent, unique solution iff rank = number of unknowns.
- Eigenvalues solve `det(A−λI)=0`.
- Sum of eigenvalues = trace; product = determinant.
- `A=LU`; solve `Ly=b`, then `Ux=y`.

---

# 7. Practice Questions

### Q1 – MCQ

A is `2×3` and B is `3×4`. What is the order of AB?

A. `2×4`  B. `3×3`  C. `4×2`  D. Product undefined

### Q2 – NAT

Find the determinant of `[[3,2],[1,4]]`.

### Q3 – MCQ

If two rows of a square matrix are identical, its determinant is:

A. 1  B. −1  C. 0  D. Cannot be determined

### Q4 – NAT

A triangular 3×3 matrix has diagonal entries 2, 3 and 5. Find its determinant.

### Q5 – MSQ

Which statements are always true for compatible matrices?

A. `(AB)ᵀ=BᵀAᵀ`  B. `AB=BA`  C. `det(AB)=det(A)det(B)` for square A and B of the same order  D. `(A+B)ᵀ=Aᵀ+Bᵀ`

### Q6 – NAT

How many solutions does a consistent system with 4 unknowns and coefficient rank 3 have?

A. Zero  B. One  C. Infinitely many

### Q7 – NAT

Find the eigenvalues of `[[4,0],[0,−2]]`.

### Q8 – MCQ

An n×n matrix is singular exactly when:

A. Its trace is zero  B. Zero is an eigenvalue  C. All eigenvalues are positive  D. It is symmetric

### Q9 – NAT

For the matrix `[[2,1],[4,3]]`, give the lower-left entry of its Doolittle L factor.

### Q10 – Difficult (Eigenvalues)

A 2×2 matrix has eigenvalues 2 and 5. Find its trace and determinant.

---

# 8. Answer Key with Solutions

### A1

**Answer: A.** For A of order `m×n` and B of order `n×p`, AB has order `m×p`. Thus the result is `2×4`.

### A2

**Answer: 10.** Determinant = `3×4−2×1=12−2=10`.

### A3

**Answer: C.** Equal rows make the rows linearly dependent. A determinant is zero when rows or columns are linearly dependent.

### A4

**Answer: 30.** For a triangular matrix, multiply diagonal entries: `2×3×5=30`.

### A5

**Answers: A, C and D.** Transpose reverses the order of a product; determinant of a product equals the product of determinants for square matrices of matching order; transpose distributes over addition. Matrix multiplication is not commutative in general.

### A6

**Answer: C.** The system is consistent and rank 3 is less than 4 unknowns. There is one free variable, so infinitely many solutions.

### A7

**Answer: 4 and −2.** A diagonal matrix has its diagonal entries as eigenvalues.

### A8

**Answer: B.** A is singular iff `det(A)=0`, which is equivalent to 0 being a root of its characteristic polynomial.

### A9

**Answer: 2.** In Example 7, `l₂₁=4/2=2`.

### A10

**Answer:** Trace = 7; determinant = 10.

**Solution:** The trace equals the sum of eigenvalues: `2+5=7`. The determinant equals their product: `2×5=10`.

---

## Final GATE preparation advice

- Check dimensions before attempting matrix multiplication.
- Use row operations carefully; determinant changes only for row swaps and row scaling, not row replacement by adding a multiple of another row.
- For systems, compare coefficient rank and augmented rank before deciding the number of solutions.
- Do not use the zero vector as an eigenvector.
- Check an LU factorisation by multiplying L and U back to A.
- Keep row-pivoting in mind when a pivot is zero.


---

# GATE CSE – Engineering Mathematics
# Part 3: Calculus

> Beginner-friendly notes progressing to GATE CSE level. Scope: limits, continuity, differentiability, maxima and minima, mean value theorem and integration.

## Syllabus checklist

- [ ] Limits and one-sided limits
- [ ] Continuity
- [ ] Differentiability
- [ ] Derivative rules
- [ ] Maxima and minima
- [ ] Mean value theorem
- [ ] Integration and the fundamental theorem of calculus

---

# 1. Functions: Basic Language

A function assigns one output to each allowed input. It is written `y=f(x)`, where x is the input and f(x) is the output.

- **Domain:** allowed input values.
- **Codomain:** declared set of possible outputs.
- **Range:** outputs actually produced.
- **Graph:** set of points `(x,f(x))`.

Before evaluating limits or derivatives, check where the function is defined. For example, `1/x` is not defined at x=0, and `√x` is real-valued only for `x≥0`.

---

# 2. Limits

A limit describes the value that a function approaches as x approaches a particular point. We write:

`lim[x→a] f(x) = L`.

This does not require f(a) to be defined or equal to L. The limit depends on values near a, not necessarily at a.

## 2.1 One-sided limits

- Left-hand limit: `lim[x→a⁻] f(x)`; approach a using values below a.
- Right-hand limit: `lim[x→a⁺] f(x)`; approach a using values above a.

A two-sided limit exists exactly when both one-sided limits exist and are equal.

## 2.2 Limit laws

When the individual limits exist:

- `lim(f+g)=lim f + lim g`.
- `lim(f−g)=lim f − lim g`.
- `lim(fg)=(lim f)(lim g)`.
- `lim(f/g)=(lim f)/(lim g)` if the denominator limit is non-zero.
- Constant multiples can be taken outside the limit.

For polynomials, substitute directly. For rational functions, direct substitution works when the denominator does not become zero.

## 2.3 Important standard limits

Angles in the following trigonometric limits are measured in radians.

- `lim[x→0] (sin x)/x = 1`.
- `lim[x→0] (tan x)/x = 1`.
- `lim[x→0] (1−cos x)/x² = 1/2`.
- `lim[x→0] (eˣ−1)/x = 1`.
- `lim[x→0] ln(1+x)/x = 1`.
- `lim[x→0] (aˣ−1)/x = ln(a)` for a>0.
- `lim[n→∞] (1+1/n)ⁿ = e`.

## 2.4 Indeterminate forms

Common indeterminate forms include `0/0`, `∞/∞`, `0×∞`, `∞−∞`, `0⁰`, `1^∞` and `∞⁰`.

They are called indeterminate because the form alone does not determine the limit. Algebraic simplification, factorisation, rationalisation, standard limits or (when conditions apply) L'Hôpital's rule may be used.

### L'Hôpital's rule

If a limit produces `0/0` or `∞/∞`, and the required differentiability and non-zero derivative conditions hold in a suitable deleted neighbourhood, then:

`lim f(x)/g(x) = lim f'(x)/g'(x)`

provided the limit on the right exists (finite or an appropriate infinite limit). Do not apply the rule directly to other forms before converting them to a quotient of type `0/0` or `∞/∞`.

### Solved example 1

**Question:** Find `lim[x→2] (x²−4)/(x−2)`.

**Solution:** Direct substitution gives `0/0`, so factorise:

`(x²−4)/(x−2) = (x−2)(x+2)/(x−2) = x+2` for x≠2.

The limit is `2+2=4`.

### Solved example 2

**Question:** Find `lim[x→0] sin(3x)/x`.

**Solution:** Multiply and divide by 3:

`sin(3x)/x = 3 × [sin(3x)/(3x)]`.

As x→0, 3x→0 and the standard limit is 1. The answer is 3.

## 2.5 Limits at infinity

For a rational function, compare the highest powers:

- Degree numerator < degree denominator: limit is 0.
- Degrees equal: limit is ratio of leading coefficients.
- Degree numerator > degree denominator: magnitude generally grows without bound; determine sign and direction carefully.

### Solved example 3

**Question:** Find `lim[x→∞] (3x²+2)/(5x²−x)`.

**Solution:** Numerator and denominator have equal degree. Divide leading coefficients: the limit is `3/5`.

---

# 3. Continuity

A function f is continuous at x=a if all three conditions hold:

1. `f(a)` is defined.
2. `lim[x→a] f(x)` exists.
3. `lim[x→a] f(x)=f(a)`.

If any condition fails, the function is discontinuous at a.

## 3.1 Types of discontinuities

- **Removable:** the two-sided limit exists and is finite, but the function value is missing or different.
- **Jump:** left and right limits exist but are unequal.
- **Infinite:** the function grows without bound near the point (vertical asymptote behaviour).
- **Oscillatory:** the function does not approach one value because it keeps oscillating.

Polynomials are continuous everywhere. Rational functions are continuous wherever their denominators are non-zero. Standard exponential, logarithmic and trigonometric functions are continuous on their domains.

## 3.2 Continuity on an interval

Continuity on a closed interval `[a,b]` means continuity inside `(a,b)`, right-continuity at a and left-continuity at b.

The **intermediate value theorem** says that if f is continuous on `[a,b]`, it takes every value between `f(a)` and `f(b)` at some point in the interval. In particular, if f(a) and f(b) have opposite signs, there is at least one root in `(a,b)`.

### Solved example 4

**Question:** Is `f(x)=(x²−1)/(x−1)` continuous at x=1 as written?

**Solution:** The expression is not defined at x=1, so it is not continuous there. For x≠1 it simplifies to x+1, and the limit at 1 is 2. Defining f(1)=2 would remove the discontinuity.

---

# 4. Differentiability

The derivative measures the instantaneous rate of change of a function. Geometrically, it is the slope of the tangent to the graph.

The derivative at x=a is defined by:

`f'(a)=lim[h→0] [f(a+h)−f(a)]/h`,

provided the limit exists.

Differentiability at a implies continuity at a. The reverse is not always true. For example, `f(x)=|x|` is continuous at 0 but not differentiable there because its left and right slopes differ.

## 4.1 Basic derivative rules

| Function | Derivative |
|---|---|
| Constant c | 0 |
| `xⁿ` | `nxⁿ⁻¹` |
| `eˣ` | `eˣ` |
| `aˣ` | `aˣ ln(a)` |
| `ln x` | `1/x` for x>0 |
| `sin x` | `cos x` |
| `cos x` | `−sin x` |
| `tan x` | `sec²x` |

Angles are in radians.

### Rules

- Sum: `(f+g)'=f'+g'`.
- Constant multiple: `(cf)'=cf'`.
- Product: `(fg)'=f'g+fg'`.
- Quotient: `(f/g)'=(f'g−fg')/g²`, where g≠0.
- Chain rule: if `y=f(g(x))`, then `dy/dx=f'(g(x))g'(x)`.

## 4.2 Chain rule example

**Question:** Differentiate `y=(3x²+1)⁵`.

**Solution:** Outer function is u⁵ and inner function is `u=3x²+1`.

`dy/dx = 5(3x²+1)⁴ × 6x = 30x(3x²+1)⁴`.

## 4.3 Implicit differentiation

Sometimes x and y are mixed in one equation and y is not written as an explicit function of x. Differentiate both sides with respect to x, treating y as a function of x.

Example: `x²+y²=25`.

Differentiate: `2x+2y(dy/dx)=0`, so `dy/dx=−x/y` when y≠0.

## 4.4 Higher derivatives

The second derivative is the derivative of the first derivative: `f''(x)`. It describes how the slope changes and helps identify concavity and local extrema.

---

# 5. Maxima and Minima

A maximum is a high function value; a minimum is a low function value. A **local** maximum/minimum is compared with nearby points, while an **absolute/global** maximum/minimum is compared with all points in the domain or interval.

## 5.1 Critical points

A critical point occurs at an interior point where `f'(x)=0` or the derivative does not exist, provided f itself is defined there.

Not every critical point is an extremum. It may be a local maximum, local minimum or neither.

## 5.2 First derivative test

Study the sign of f′ on either side of the critical point:

- Positive to negative: local maximum.
- Negative to positive: local minimum.
- No sign change: generally neither a local maximum nor a local minimum.

## 5.3 Second derivative test

If `f'(c)=0`:

- `f''(c)>0`: local minimum.
- `f''(c)<0`: local maximum.
- `f''(c)=0`: test is inconclusive; use another method.

## 5.4 Absolute extrema on a closed interval

If f is continuous on `[a,b]`, it attains an absolute maximum and minimum. To find them:

1. Find critical points inside `(a,b)`.
2. Evaluate f at each critical point.
3. Evaluate f(a) and f(b).
4. Compare all values.

### Solved example 5

**Question:** Find the local extrema of `f(x)=x²−4x+3`.

**Solution:**

`f'(x)=2x−4`. Set equal to zero: x=2.

`f''(x)=2>0`, so x=2 is a local minimum.

`f(2)=4−8+3=−1`.

The parabola opens upward, so this is also its absolute minimum on the real line. There is no maximum on the real line.

### Solved example 6

**Question:** Find the absolute maximum and minimum of `f(x)=x²` on `[−1,2]`.

**Solution:** The critical point is x=0. Evaluate:

- `f(−1)=1`.
- `f(0)=0`.
- `f(2)=4`.

Absolute minimum is 0 at x=0. Absolute maximum is 4 at x=2.

---

# 6. Mean Value Theorem

The mean value theorem (MVT) connects the average rate of change over an interval with an instantaneous rate of change at some point inside it.

## 6.1 Rolle's theorem

If f is:

1. continuous on `[a,b]`;
2. differentiable on `(a,b)`; and
3. `f(a)=f(b)`,

then there is at least one `c∈(a,b)` such that `f'(c)=0`.

## 6.2 Lagrange mean value theorem

If f is continuous on `[a,b]` and differentiable on `(a,b)`, then there exists at least one `c∈(a,b)` such that:

`f'(c) = [f(b)−f(a)]/(b−a)`.

The right side is the slope of the secant line joining the endpoints. The theorem says that at some interior point, the tangent has the same slope.

## 6.3 Cauchy's mean value theorem

If f and g are continuous on `[a,b]`, differentiable on `(a,b)`, and the required denominator is non-zero, there is a c in `(a,b)` such that:

`[f(b)−f(a)]g'(c) = [g(b)−g(a)]f'(c)`.

Lagrange's MVT follows by choosing `g(x)=x`.

### Solved example 7

**Question:** Apply MVT to `f(x)=x²` on `[1,3]` and find c.

**Solution:** f is continuous on `[1,3]` and differentiable on `(1,3)`, so MVT applies.

Average slope = `[f(3)−f(1)]/(3−1) = (9−1)/2 = 4`.

Since `f'(x)=2x`, set `2c=4`, giving `c=2`, which lies in `(1,3)`.

### GATE focus

Always verify the continuity and differentiability conditions before applying an MVT. The point c is guaranteed to exist, but it need not be unique.

---

# 7. Integration

Integration is the reverse process of differentiation in indefinite integration. Definite integration also measures accumulated quantity and signed area.

## 7.1 Indefinite integrals

`∫ f(x) dx = F(x)+C` when `F'(x)=f(x)`. C is the constant of integration because the derivative of a constant is zero.

### Basic integration formulas

| Function | Integral |
|---|---|
| `xⁿ`, n≠−1 | `xⁿ⁺¹/(n+1)+C` |
| `1/x` | `ln|x|+C` |
| `eˣ` | `eˣ+C` |
| `aˣ` | `aˣ/ln(a)+C` for a>0, a≠1 |
| `cos x` | `sin x+C` |
| `sin x` | `−cos x+C` |
| `sec²x` | `tan x+C` |

## 7.2 Substitution

Use substitution when an inner function and (a constant multiple of) its derivative both appear.

Let `u=g(x)`, so `du=g'(x)dx`. Then rewrite the integral in u.

**Example:** `∫ 2x cos(x²) dx`.

Let `u=x²`, `du=2x dx`. Integral becomes `∫cos u du = sin u + C = sin(x²)+C`.

## 7.3 Integration by parts

`∫u dv = uv − ∫v du`.

It is useful for products such as polynomial × exponential, polynomial × trigonometric, or logarithmic functions. Choose u so its derivative becomes simpler.

**Example:** `∫x eˣ dx`.

Take `u=x`, `dv=eˣdx`. Then `du=dx`, `v=eˣ`.

Integral = `xeˣ−∫eˣdx = xeˣ−eˣ+C = eˣ(x−1)+C`.

## 7.4 Partial fractions

For a rational function, if the numerator degree is less than the denominator degree, factor the denominator and split the expression into simpler fractions. If the numerator degree is at least the denominator degree, perform polynomial division first.

**Example:**

`1/[x(x+1)] = 1/x − 1/(x+1)`.

So the integral is `ln|x|−ln|x+1|+C`.

## 7.5 Definite integrals

A definite integral has limits:

`∫[a to b] f(x) dx`.

If F is an antiderivative of f and f is suitably continuous, the fundamental theorem of calculus gives:

`∫[a to b] f(x) dx = F(b)−F(a)`.

It represents signed area: area above the x-axis contributes positively and area below it negatively.

### Properties of definite integrals

- `∫[a to a] f(x)dx=0`.
- `∫[a to b] f(x)dx = −∫[b to a] f(x)dx`.
- `∫[a to b] f = ∫[a to c] f + ∫[c to b] f`.
- `∫[a to b] [f+g] = ∫f + ∫g`.
- If f is even, `∫[−a to a] f(x)dx = 2∫[0 to a]f(x)dx`.
- If f is odd, `∫[−a to a] f(x)dx = 0`.

## 7.6 Symmetry property

For suitable f:

`∫[0 to a] f(x)dx = ∫[0 to a] f(a−x)dx`.

A common consequence:

`∫[0 to a] [f(x)+f(a−x)]dx = 2∫[0 to a]f(x)dx`.

### Solved example 8

**Question:** Evaluate `∫[0 to 2] 3x² dx`.

**Solution:** An antiderivative is x³. Therefore:

`[x³]₀² = 2³−0³=8`.

### Solved example 9

**Question:** Evaluate `∫[0 to 1] 2x e^(x²) dx`.

**Solution:** Let `u=x²`, so `du=2x dx`. Limits change from x=0 to u=0 and x=1 to u=1.

Integral = `∫[0 to 1] eᵘ du = [eᵘ]₀¹ = e−1`.

---

# 8. Quick Revision Sheet

- A two-sided limit exists iff left and right limits exist and are equal.
- A function is continuous at a if it is defined there, the limit exists and equals its value.
- Differentiability implies continuity; continuity does not imply differentiability.
- Product rule: `(fg)'=f'g+fg'`.
- Chain rule: derivative of outside × derivative of inside.
- Critical points: derivative zero or undefined (where f is defined).
- Second derivative test: positive → local min; negative → local max; zero → inconclusive.
- MVT conditions: continuous on closed interval, differentiable on open interval.
- `∫u dv=uv−∫v du`.
- Definite integral: antiderivative at upper limit minus lower limit.
- Odd function over symmetric limits integrates to zero; even function doubles the half-interval integral.

---

# 9. Practice Questions

### Q1 – NAT (Limits)

Find `lim[x→3] (x²−9)/(x−3)`.

### Q2 – MCQ (Limits)

The two-sided limit at x=a exists when:

A. Only the left-hand limit exists.
B. Only the right-hand limit exists.
C. Both one-sided limits exist and are equal.
D. f(a) must be zero.

### Q3 – MCQ (Continuity)

Which statement is always true?

A. Continuity implies differentiability.
B. Differentiability implies continuity.
C. A discontinuous function is differentiable.
D. Every continuous function has derivative zero.

### Q4 – NAT (Differentiation)

Differentiate `f(x)=x³−5x+2` and evaluate f′(2).

### Q5 – NAT (Maxima/minima)

Find the x-coordinate of the local minimum of `f(x)=x²+6x+10`.

### Q6 – MCQ (Second derivative test)

If `f′(c)=0` and `f″(c)<0`, then c is:

A. Local maximum  B. Local minimum  C. Always an inflection point  D. Not a critical point

### Q7 – NAT (MVT)

For `f(x)=x²` on `[0,2]`, find a value of c guaranteed by MVT.

### Q8 – NAT (Integration)

Evaluate `∫ 4x³ dx`.

### Q9 – NAT (Definite integration)

Evaluate `∫[0 to 3] 2x dx`.

### Q10 – Difficult (Integration)

Evaluate `∫ x cos(x²) dx`.

---

# 10. Answer Key with Solutions

### A1

**Answer: 6.** Factorise: `(x²−9)/(x−3)=(x−3)(x+3)/(x−3)=x+3` for x≠3. Limit is 6.

### A2

**Answer: C.** The left and right limits must both exist and have the same value.

### A3

**Answer: B.** Differentiability at a point guarantees continuity there. The converse fails, as shown by `|x|` at 0.

### A4

**Answer: 7.** `f′(x)=3x²−5`; at x=2, `12−5=7`.

### A5

**Answer: −3.** `f′(x)=2x+6=0` gives x=−3. Since `f″(x)=2>0`, it is a local minimum.

### A6

**Answer: A.** A negative second derivative at a stationary point indicates the graph is locally concave down, hence a local maximum.

### A7

**Answer: 1.** Average slope = `(4−0)/(2−0)=2`. Since `f′(x)=2x`, solve `2c=2`, so c=1, which lies in `(0,2)`.

### A8

**Answer: `x⁴+C`.** By the power rule for integration, `4×x⁴/4=x⁴`.

### A9

**Answer: 9.** Antiderivative of 2x is x². Evaluate `3²−0²=9`.

### A10

**Answer: `(1/2)sin(x²)+C`.** Let `u=x²`; then `du=2x dx`, so `x dx=du/2`. Integral becomes `(1/2)∫cos u du = (1/2)sin u+C`.

---

## Final GATE preparation advice

- In limit questions, identify the form before choosing a method.
- Check one-sided limits for piecewise functions.
- Test continuity and differentiability separately.
- For extrema, do not assume every point where f′=0 is an extremum.
- Verify all MVT conditions before applying the theorem.
- For definite integrals, change the limits when using substitution.
- Remember that a definite integral is signed area, not always ordinary geometric area.


---

# GATE CSE – Engineering Mathematics
# Part 4: Probability and Statistics

> Beginner-friendly notes progressing to GATE CSE level. Scope: random variables; uniform, normal, exponential, Poisson and binomial distributions; mean, median, mode, standard deviation; conditional probability and Bayes' theorem.

## Syllabus checklist

- [ ] Probability basics and events
- [ ] Conditional probability
- [ ] Independence
- [ ] Bayes' theorem
- [ ] Random variables, PMF, PDF and CDF
- [ ] Mean and variance
- [ ] Uniform distribution
- [ ] Normal distribution
- [ ] Exponential distribution
- [ ] Poisson distribution
- [ ] Binomial distribution
- [ ] Mean, median and mode
- [ ] Standard deviation

---

# 1. Probability Basics

Probability measures how likely an event is. Its value is between 0 and 1:

- 0 means impossible.
- 1 means certain.
- A value near 1 means highly likely.

## 1.1 Experiment, sample space and event

- **Random experiment:** a process whose outcome is not known in advance, such as tossing a coin.
- **Sample space (S):** set of all possible outcomes.
- **Event (A):** a subset of the sample space.
- **Complement (Aᶜ):** outcomes in S that are not in A.

For a fair six-sided die, `S={1,2,3,4,5,6}`. The event of rolling an even number is `A={2,4,6}`.

If all outcomes are equally likely:

`P(A)=|A|/|S|`.

This formula must not be used blindly when outcomes are not equally likely.

## 1.2 Probability axioms and basic rules

- `P(A)≥0`.
- `P(S)=1`.
- For mutually exclusive events A and B, `P(A∪B)=P(A)+P(B)`.

Derived rules:

- `P(∅)=0`.
- `P(Aᶜ)=1−P(A)`.
- `P(A∪B)=P(A)+P(B)−P(A∩B)`.
- If `A⊆B`, then `P(A)≤P(B)`.

## 1.3 Mutually exclusive versus independent

| Mutually exclusive | Independent |
|---|---|
| Events cannot happen together: `P(A∩B)=0` | Occurrence of one does not change probability of the other: `P(A∩B)=P(A)P(B)` |
| If both have positive probability, they are not independent | Independent events can occur together |

This is a common GATE distinction. Two events with positive probabilities cannot be both mutually exclusive and independent.

### Solved example 1

**Question:** A fair die is rolled. Find the probability of getting an even number.

**Solution:** Even outcomes are `{2,4,6}`: 3 favourable outcomes out of 6 equally likely outcomes. Probability = `3/6=1/2`.

---

# 2. Conditional Probability

Conditional probability is the probability of A when it is already known that B has occurred.

Provided `P(B)>0`:

`P(A|B)=P(A∩B)/P(B)`.

The condition B becomes the new restricted sample space. The denominator is P(B), not P(A).

## 2.1 Multiplication rule

Rearranging the definition:

`P(A∩B)=P(A|B)P(B)=P(B|A)P(A)`.

For three events:

`P(A∩B∩C)=P(A)P(B|A)P(C|A∩B)`.

## 2.2 Independence

A and B are independent if:

`P(A∩B)=P(A)P(B)`.

When the relevant conditional probability is defined, independence also means `P(A|B)=P(A)` and `P(B|A)=P(B)`.

For mutually independent events, the corresponding product rule holds for every subset, not merely every pair.

### Solved example 2

**Question:** In a class, 40% of students know Python, 30% know Java, and 20% know both. Find the probability that a student knows Python given that the student knows Java.

**Solution:** Let P be Python and J be Java.

`P(P|J)=P(P∩J)/P(J)=0.20/0.30=2/3`.

---

# 3. Bayes' Theorem

Bayes' theorem reverses a conditional probability. It is useful when we know the probability of evidence under different possible causes and want the probability of a cause after observing the evidence.

If `B₁,...,Bₙ` form a partition of the sample space and `P(A)>0`, then:

`P(Bᵢ|A) = [P(A|Bᵢ)P(Bᵢ)] / [Σⱼ P(A|Bⱼ)P(Bⱼ)]`.

The denominator is the law of total probability:

`P(A)=ΣⱼP(A|Bⱼ)P(Bⱼ)`.

### Solved example 3 – Medical test style

**Question:** A condition affects 1% of a population. A test is positive for 90% of people who have the condition and is positive for 5% of people who do not have it. If a person tests positive, find the probability that the person has the condition.

**Solution:**

Let D = has condition and + = positive result.

- `P(D)=0.01`.
- `P(Dᶜ)=0.99`.
- `P(+|D)=0.90` (sensitivity).
- `P(+|Dᶜ)=0.05` (false-positive probability).

By Bayes' theorem:

`P(D|+) = [0.90×0.01]/[(0.90×0.01)+(0.05×0.99)]`.

`=0.009/(0.009+0.0495)=0.009/0.0585≈0.1538`.

So the probability is about 15.38%, not 90%. The low base rate matters.

> Remember: conditional probability measures the part of event A that lies inside the restricted event B. Always divide the intersection probability by P(B), provided P(B) is non-zero.

---

# 4. Random Variables

A **random variable** assigns a numerical value to each outcome of a random experiment.

- **Discrete random variable:** has a finite or countable set of possible values, such as number of heads in three coin tosses.
- **Continuous random variable:** can take values throughout intervals, such as time or height.

## 4.1 PMF, PDF and CDF

### Probability mass function (PMF)

For a discrete random variable X:

`pₓ(x)=P(X=x)`.

Properties: `pₓ(x)≥0` and `Σₓ pₓ(x)=1`.

### Probability density function (PDF)

For a continuous random variable X, the density f(x) satisfies:

- `f(x)≥0`.
- Total area `∫[−∞ to ∞] f(x)dx=1`.
- `P(a≤X≤b)=∫[a to b]f(x)dx`.

For a continuous random variable, `P(X=a)=0` at any single point. The density value f(a) is not itself the probability at a.

### Cumulative distribution function (CDF)

`Fₓ(x)=P(X≤x)`.

Properties:

- Non-decreasing.
- Values lie between 0 and 1.
- Right-continuous.
- Approaches 0 as x approaches negative infinity and 1 as x approaches positive infinity.

For a continuous distribution, where differentiable, `F'(x)=f(x)`.

## 4.2 Expectation (mean)

For discrete X:

`E[X]=Σₓ x pₓ(x)`.

For continuous X:

`E[X]=∫[−∞ to ∞] x f(x)dx`.

For a function g(X):

- Discrete: `E[g(X)]=Σg(x)pₓ(x)`.
- Continuous: `E[g(X)]=∫g(x)f(x)dx`.

Linearity:

`E[aX+b]=aE[X]+b`.

More generally, `E[X+Y]=E[X]+E[Y]`, whether or not X and Y are independent, provided the expectations exist.

## 4.3 Variance and standard deviation

Variance measures spread around the mean:

`Var(X)=E[(X−μ)²]`, where `μ=E[X]`.

A useful formula:

`Var(X)=E[X²]−(E[X])²`.

Standard deviation is the non-negative square root:

`σ=√Var(X)`.

Properties:

- `Var(X)≥0`.
- `Var(aX+b)=a²Var(X)`.
- Adding a constant does not change variance.
- For independent X and Y, `Var(X+Y)=Var(X)+Var(Y)`.
- In general, `Var(X+Y)=Var(X)+Var(Y)+2Cov(X,Y)`.

### Solved example 4

**Question:** X takes values 0 and 2 with probabilities 0.25 and 0.75. Find its mean, variance and standard deviation.

**Solution:**

`E[X]=0×0.25+2×0.75=1.5`.

`E[X²]=0²×0.25+2²×0.75=3`.

`Var(X)=3−(1.5)²=3−2.25=0.75`.

`σ=√0.75≈0.866`.

---

# 5. Discrete and Continuous Distributions

A probability distribution describes how probability is assigned to the possible values of a random variable.

## 5.1 Discrete uniform distribution

A discrete uniform random variable has n equally likely values. Each value has probability `1/n`.

For values `1,2,...,n`:

- Mean: `(n+1)/2`.
- Variance: `(n²−1)/12`.

A fair die is discrete uniform on `{1,2,3,4,5,6}`.

## 5.2 Continuous uniform distribution

If X is uniform on `[a,b]`, its density is:

`f(x)=1/(b−a)` for `a≤x≤b`, and 0 otherwise.

- Mean: `(a+b)/2`.
- Variance: `(b−a)²/12`.
- CDF inside the interval: `(x−a)/(b−a)`.

### Solved example 5

**Question:** X is uniform on `[2,10]`. Find `P(4≤X≤7)`, the mean and variance.

**Solution:**

`P(4≤X≤7)=(7−4)/(10−2)=3/8`.

Mean = `(2+10)/2=6`.

Variance = `(10−2)²/12=64/12=16/3`.

## 5.3 Bernoulli distribution

A Bernoulli random variable represents one trial with success probability p and failure probability `1−p`.

- `P(X=1)=p`; `P(X=0)=1−p`.
- Mean: p.
- Variance: `p(1−p)`.

It is the building block of the binomial distribution.

## 5.4 Binomial distribution

Use a binomial distribution when:

1. There are a fixed number n of trials.
2. Each trial has two outcomes (success/failure).
3. Success probability p is the same for each trial.
4. Trials are independent.

If X is the number of successes:

`P(X=k)=C(n,k)pᵏ(1−p)^(n−k)`, for `k=0,1,...,n`.

- Mean: `np`.
- Variance: `np(1−p)`.
- Standard deviation: `√[np(1−p)]`.

### Solved example 6

**Question:** A fair coin is tossed 4 times. Find the probability of exactly 2 heads.

**Solution:** Here n=4, p=1/2 and k=2.

`P(X=2)=C(4,2)(1/2)²(1/2)² = 6/16=3/8`.

Mean = `4×1/2=2`; variance = `4×1/2×1/2=1`.

## 5.5 Poisson distribution

The Poisson distribution models the number of occurrences in a fixed interval when events occur at an average rate λ under suitable independence and constant-rate assumptions.

`P(X=k)=e^(−λ) λᵏ/k!`, for `k=0,1,2,...`.

- Mean: λ.
- Variance: λ.
- Standard deviation: `√λ`.

Examples include the number of calls arriving in a fixed time interval under a Poisson-arrival model.

### Solved example 7

**Question:** A help desk receives an average of 2 calls per minute. Under a Poisson model, find the probability of receiving exactly 3 calls in a minute.

**Solution:** λ=2, k=3.

`P(X=3)=e^(−2)2³/3! = 8e^(−2)/6 = (4/3)e^(−2)≈0.1804`.

## 5.6 Exponential distribution

The exponential distribution models waiting time between events in a Poisson process with rate λ>0.

For `x≥0`:

`f(x)=λe^(−λx)`.

CDF:

`F(x)=1−e^(−λx)`.

Survival probability:

`P(X>x)=e^(−λx)`.

- Mean: `1/λ`.
- Variance: `1/λ²`.
- Standard deviation: `1/λ`.

**Memoryless property:** `P(X>s+t | X>s)=P(X>t)` for s,t≥0. The remaining waiting time does not depend on how long one has already waited.

### Solved example 8

**Question:** The waiting time X is exponential with rate λ=0.5 per minute. Find the probability of waiting more than 3 minutes.

**Solution:** `P(X>3)=e^(−0.5×3)=e^(−1.5)≈0.2231`.

Mean waiting time = `1/0.5=2` minutes.

## 5.7 Normal distribution

A normal random variable with mean μ and variance σ² is written `X~N(μ,σ²)`.

Its density is:

`f(x)= [1/(σ√(2π))] exp(−(x−μ)²/(2σ²))`.

Key properties:

- Bell-shaped and symmetric around μ.
- Mean = median = mode = μ.
- Variance = σ²; standard deviation = σ.
- Total area under the curve is 1.
- For a continuous variable, probability over an interval is the area under the density curve over that interval.

### Standard normal distribution

The standard normal variable is `Z~N(0,1)`. Convert X to Z using:

`Z=(X−μ)/σ`.

Then use a standard normal table or a calculator to find probabilities.

The approximate empirical rule is:

- About 68% of values lie within μ±σ.
- About 95% lie within μ±2σ.
- About 99.7% lie within μ±3σ.

These are approximations, not exact percentages.

### Solved example 9

**Question:** X is normal with μ=50 and σ=10. Convert x=70 to a z-score.

**Solution:** `z=(70−50)/10=2`. Thus, 70 is two standard deviations above the mean.

### Solved example 10

**Question:** If `Z~N(0,1)`, express `P(−1≤Z≤1)` using the standard normal CDF Φ.

**Solution:** `P(−1≤Z≤1)=Φ(1)−Φ(−1)`. By symmetry, `Φ(−1)=1−Φ(1)`, so the probability is `2Φ(1)−1`, approximately 0.6827.

---

# 6. Mean, Median, Mode and Standard Deviation

These are descriptive statistics that summarise a dataset.

## 6.1 Mean

For observations `x₁,...,xₙ`:

`Mean = (x₁+x₂+...+xₙ)/n`.

The mean uses every observation but is sensitive to extreme values.

## 6.2 Median

Sort the observations.

- If n is odd, the median is the middle observation.
- If n is even, the median is the average of the two middle observations.

The median is less affected by extreme values than the mean.

## 6.3 Mode

The mode is the value that occurs most often. A dataset may have one mode, multiple modes or no unique mode.

## 6.4 Standard deviation

For a population of N values:

`μ = (1/N)Σxᵢ`.

`σ = √[(1/N)Σ(xᵢ−μ)²]`.

For a sample, the commonly used sample variance is:

`s² = [1/(n−1)]Σ(xᵢ−x̄)²`, and sample standard deviation is `s=√s²`.

The denominator n−1 is Bessel's correction; it is used for the usual unbiased estimator of population variance under independent sampling. Do not mix the population and sample formulas.

### Solved example 11

**Question:** For data `2, 4, 4, 6`, find mean, median, mode and population standard deviation.

**Solution:**

Mean = `(2+4+4+6)/4=4`.

The data are already sorted. Median = `(4+4)/2=4`.

Mode = 4 because it appears most often.

Population variance = `[(2−4)²+(4−4)²+(4−4)²+(6−4)²]/4`.

`=(4+0+0+4)/4=2`.

Population standard deviation = `√2≈1.414`.

## 6.5 Effect of transformations

For `Y=aX+b`:

- Mean: `E[Y]=aE[X]+b`.
- Variance: `Var(Y)=a²Var(X)`.
- Standard deviation: `SD(Y)=|a|SD(X)`.

Adding b shifts all values but does not change spread. Multiplying by a scales the spread by `|a|`.

> Visual intuition: standard deviation describes how far observations typically spread around the mean. A larger standard deviation means a wider spread; changing every value by adding a constant does not change the spread.

---

# 7. Distribution Comparison Table

| Distribution | Type | PMF/PDF or key form | Mean | Variance | Typical use |
|---|---|---|---:|---:|---|
| Discrete uniform on n values | Discrete | Each value `1/n` | `(n+1)/2` for 1,...,n | `(n²−1)/12` | Equally likely finite outcomes |
| Continuous uniform `[a,b]` | Continuous | `1/(b−a)` on interval | `(a+b)/2` | `(b−a)²/12` | Constant density over interval |
| Bernoulli(p) | Discrete | `P(1)=p`, `P(0)=1−p` | p | `p(1−p)` | One success/failure trial |
| Binomial(n,p) | Discrete | `C(n,k)pᵏ(1−p)^(n−k)` | np | `np(1−p)` | Success count in n independent trials |
| Poisson(λ) | Discrete | `e^(−λ)λᵏ/k!` | λ | λ | Count in a fixed interval |
| Exponential(λ) | Continuous | `λe^(−λx)`, x≥0 | `1/λ` | `1/λ²` | Waiting time between Poisson events |
| Normal(μ,σ²) | Continuous | Bell-shaped density | μ | σ² | Continuous measurements and normal models |

---

# 8. Important Relationships and GATE Traps

- For `X~Binomial(n,p)`, if n is large and p is small with `np=λ`, a Poisson(λ) approximation may be useful. It is an approximation, not an identity.
- The sum of independent Poisson random variables is Poisson with parameter equal to the sum of their parameters.
- The sum of independent normal random variables is normal; means add and variances add.
- A binomial variable counts successes in a fixed number of trials; a Poisson variable counts occurrences in a fixed interval or region.
- An exponential variable measures waiting time; a Poisson variable measures count.
- For continuous X, `P(X=a)=0`; do not confuse f(a) with P(X=a).
- Variance has squared units; standard deviation has the same units as the original data.
- Mean is not always the most representative centre when outliers are present; median may be more robust.
- Conditional probability changes the reference sample space.
- Bayes' theorem requires base rates as well as test accuracy or likelihood information.

---

# 9. Quick Revision Sheet

- `P(Aᶜ)=1−P(A)`.
- `P(A∪B)=P(A)+P(B)−P(A∩B)`.
- `P(A|B)=P(A∩B)/P(B)`.
- Independence: `P(A∩B)=P(A)P(B)`.
- Bayes: posterior = likelihood × prior / evidence.
- `E[X]=Σxp(x)` or `∫xf(x)dx`.
- `Var(X)=E[X²]−(E[X])²`; `SD=√Var`.
- Binomial: mean np, variance np(1−p).
- Poisson: mean λ, variance λ.
- Exponential(rate λ): mean 1/λ, variance 1/λ².
- Uniform `[a,b]`: mean `(a+b)/2`, variance `(b−a)²/12`.
- Normal: standardise using `Z=(X−μ)/σ`.
- Median is the middle of sorted data; mode is most frequent.

---

# 10. Practice Questions

### Q1 – NAT (Probability)

A fair die is rolled. Find the probability of getting a number greater than 4.

### Q2 – MCQ (Events)

If A and B are mutually exclusive, then:

A. `P(A∩B)=P(A)P(B)` always
B. `P(A∩B)=0`
C. A and B must be independent
D. `P(A∪B)=0`

### Q3 – NAT (Conditional probability)

If `P(A∩B)=0.12` and `P(B)=0.30`, find `P(A|B)`.

### Q4 – MCQ (Independence)

If A and B are independent and `P(A)=0.4`, `P(B)=0.5`, find `P(A∩B)`.

A. 0.1  B. 0.2  C. 0.4  D. 0.9

### Q5 – NAT (Bayes' theorem)

A factory has two machines. M1 makes 60% of products and has a 2% defect rate. M2 makes 40% and has a 5% defect rate. A selected product is defective. Find `P(M2 | defective)`.

### Q6 – NAT (Expectation)

X takes values 1, 2 and 3 with probabilities 0.2, 0.5 and 0.3. Find E[X].

### Q7 – NAT (Variance)

For Q6, find `E[X²]` and `Var(X)`.

### Q8 – NAT (Binomial)

A fair coin is tossed 5 times. Find the probability of exactly 3 heads.

### Q9 – NAT (Poisson)

For a Poisson random variable with λ=3, find `P(X=0)`.

### Q10 – NAT (Exponential)

For an exponential distribution with rate λ=2, find `P(X>1)`.

### Q11 – NAT (Uniform)

X is uniform on `[0,8]`. Find `P(2≤X≤6)`.

### Q12 – NAT (Normal)

X has mean 100 and standard deviation 15. Find the z-score corresponding to x=130.

### Q13 – NAT (Descriptive statistics)

Find mean and median of `3, 5, 7, 9, 16`.

### Q14 – NAT (Standard deviation)

Find the population variance and standard deviation of `1, 3, 5`.

---

# 11. Answer Key with Solutions

### A1

**Answer: 1/3.** Outcomes greater than 4 are `{5,6}`. Probability = `2/6=1/3`.

### A2

**Answer: B.** Mutually exclusive events cannot occur together, so their intersection is empty and its probability is zero.

### A3

**Answer: 0.4.** `P(A|B)=P(A∩B)/P(B)=0.12/0.30=0.4`.

### A4

**Answer: B.** Independence gives `P(A∩B)=P(A)P(B)=0.4×0.5=0.2`.

### A5

**Answer: 5/8 = 0.625.** Let D be defective.

`P(M2|D)=[P(D|M2)P(M2)]/P(D)`.

`P(D)=0.02×0.60+0.05×0.40=0.012+0.020=0.032`.

`P(M2|D)=0.020/0.032=0.625`.

### A6

**Answer: 2.1.** `E[X]=1×0.2+2×0.5+3×0.3=0.2+1+0.9=2.1`.

### A7

**Answer: `E[X²]=4.9`; `Var(X)=0.49`.**

`E[X²]=1²×0.2+2²×0.5+3²×0.3=0.2+2+2.7=4.9`.

`Var(X)=4.9−(2.1)²=4.9−4.41=0.49`.

### A8

**Answer: 5/16 = 0.3125.** Here n=5, p=1/2 and k=3.

`P(X=3)=C(5,3)(1/2)³(1/2)²=10/32=5/16`.

### A9

**Answer: `e^(−3)≈0.0498`.** For k=0:

`P(X=0)=e^(−3)3⁰/0!=e^(−3)`.

### A10

**Answer: `e^(−2)≈0.1353`.** Exponential survival probability is `P(X>t)=e^(−λt)`. Substitute λ=2 and t=1.

### A11

**Answer: 1/2.** Uniform probability is interval length divided by total length: `(6−2)/(8−0)=4/8=1/2`.

### A12

**Answer: 2.** `z=(130−100)/15=30/15=2`.

### A13

**Answer: Mean = 8; median = 7.** Sum = `3+5+7+9+16=40`; mean = 40/5=8. The middle value of the sorted data is 7.

### A14

**Answer: Variance = 8/3; standard deviation = `√(8/3)≈1.633`.**

Mean = `(1+3+5)/3=3`.

Population variance = `[(1−3)²+(3−3)²+(5−3)²]/3 = (4+0+4)/3=8/3`.

Standard deviation is the square root of the variance.

---

## Final GATE preparation advice

- Identify the random experiment and sample space before applying a probability formula.
- Write the condition clearly in conditional-probability questions.
- In Bayes questions, calculate the total probability of the evidence in the denominator.
- Confirm whether a variable is discrete or continuous before using a PMF or PDF.
- For expectation and variance, calculate E[X] and E[X²] carefully.
- Match the wording to the distribution: fixed number of trials → binomial; count in an interval → Poisson; waiting time → exponential.
- In normal questions, standardise first and then read the table or use a calculator.
- Check whether the question asks for population or sample standard deviation.
