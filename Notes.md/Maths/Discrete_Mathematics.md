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
