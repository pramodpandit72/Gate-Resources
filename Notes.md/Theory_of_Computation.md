# GATE CSE – Theory of Computation
## Complete Beginner-Friendly Study Material, Revision Notes and Practice Questions

**Syllabus:** Regular expressions and finite automata; context-free grammars and push-down automata; regular and context-free languages; pumping lemma; Turing machines and undecidability.

These notes are arranged from fundamentals to advanced topics. Study each definition, work through the examples, then attempt the questions before checking the solutions.

---

# 1. Foundations of Theory of Computation

Theory of Computation (TOC) studies what problems computers can solve, how abstract machines solve them, and where computation has limits.

## 1.1 Basic terminology

| Term | Meaning | Example |
|---|---|---|
| Symbol | One basic character | `0`, `1`, `a` |
| Alphabet (`Σ`) | Finite, non-empty set of symbols | `{0,1}` |
| String | Finite sequence of symbols | `0101` |
| Empty string (`ε`) | String with no symbols | `ε` |
| Length (`|w|`) | Number of symbols in `w` | `|010| = 3` |
| `Σ*` | All finite strings over `Σ`, including `ε` | `{ε,0,1,00,...}` |
| `Σ+` | All non-empty strings over `Σ` | `Σ* − {ε}` |
| Language | Any subset of `Σ*` | `{w : w ends in 1}` |

A language may be finite or infinite. For `Σ={a,b}`, `{a,ab,bba}` is finite, while `{aⁿbⁿ : n≥0}` is infinite.

## 1.2 Operations on languages

For languages `L1` and `L2`:

- **Union:** `L1 ∪ L2`, strings in either language.
- **Intersection:** `L1 ∩ L2`, strings in both.
- **Concatenation:** `L1L2 = {xy : x∈L1, y∈L2}`.
- **Kleene star:** `L*`, zero or more concatenations of strings from `L`; always includes `ε`.
- **Positive closure:** `L+ = LL*`, one or more concatenations.
- **Complement:** `Σ* − L`, relative to the chosen alphabet.
- **Difference:** `L1 − L2`.

Example: If `L1={a,ab}` and `L2={b}`, then `L1L2={ab,abb}`. Concatenation is not generally commutative: `L1L2` need not equal `L2L1`.

## 1.3 Chomsky hierarchy

| Type | Grammar | Recognizing machine | Language class |
|---|---|---|---|
| Type 3 | Regular grammar | Finite automaton | Regular |
| Type 2 | Context-free grammar | Push-down automaton | Context-free |
| Type 1 | Context-sensitive grammar | Linear bounded automaton | Context-sensitive |
| Type 0 | Unrestricted grammar | Turing machine | Recursively enumerable |

Strict containment:

`Regular ⊊ Context-Free ⊊ Context-Sensitive ⊊ Recursively Enumerable`

Remember the machine associated with each language class.

---

# 2. Regular Expressions

A regular expression (RE) is an algebraic way to describe a regular language.

## 2.1 Operators

| Expression | Meaning |
|---|---|
| `∅` | Empty language; accepts no strings |
| `ε` | Language containing only the empty string |
| `a` | Language `{a}` |
| `R + S` or `R \| S` | Union: either `R` or `S` |
| `RS` | Concatenation |
| `R*` | Zero or more repetitions |
| `R+` | One or more repetitions (common shorthand) |
| `R?` | Zero or one occurrence (common shorthand) |

Precedence: Kleene star first, concatenation second, union last.

### Important distinction

- `∅` contains no strings.
- `ε` is one string of length zero.
- `ε* = {ε}`.
- `∅* = {ε}` because zero repetitions are allowed.

## 2.2 Common expressions

Assume `Σ={0,1}`.

| Regular expression | Language |
|---|---|
| `0*` | `ε, 0, 00, 000, ...` |
| `(0+1)*` | All binary strings |
| `0(0+1)*` | Strings beginning with `0` |
| `(0+1)*1` | Strings ending in `1` |
| `0*1*` | Zeros followed by ones |
| `(01)*` | `ε, 01, 0101, ...` |
| `(0+1)*00(0+1)*` | Strings containing `00` |
| `1*(01*01*)*` | Strings with an even number of zeros |

Over `{a,b}`:

- Exactly one `a`: `b*ab*`
- No `a`: `b*`
- At least one `a`: `(a+b)*a(a+b)*`

## 2.3 Constructing expressions

**Binary strings ending in `01`:**

`(0+1)*01`

Any binary prefix is allowed, but the final two symbols must be `01`.

**Binary strings containing at least one `1`:**

`(0+1)*1(0+1)*`

**Strings over `{a,b}` with exactly one `a`:**

`b*ab*`

**Strings with an even number of zeros:**

`1*(01*01*)*`

## 2.4 Algebraic laws

| Law | Identity |
|---|---|
| Union commutativity | `R+S=S+R` |
| Union associativity | `(R+S)+T=R+(S+T)` |
| Concatenation associativity | `(RS)T=R(ST)` |
| Distributivity | `R(S+T)=RS+RT` |
| Union idempotence | `R+R=R` |
| Union identity | `R+∅=R` |
| Concatenation identity | `Rε=εR=R` |
| Annihilator | `R∅=∅R=∅` |
| Star identity | `R*=ε+RR*=ε+R*R` |
| Star idempotence | `(R*)*=R*` |

Concatenation is generally not commutative: `RS` need not equal `SR`.

## 2.5 Regular expression–automaton equivalence

A language is regular if and only if it can be described by a regular expression, or recognized by a finite automaton. Thompson's construction converts a regular expression to an ε-NFA by building small automata for symbols and combining them for union, concatenation and star.

---

# 3. Finite Automata

A finite automaton reads input symbols one by one and changes state according to its transition function.

## 3.1 Deterministic Finite Automaton (DFA)

A DFA is a five-tuple:

`M = (Q, Σ, δ, q0, F)`

- `Q`: finite set of states.
- `Σ`: input alphabet.
- `δ: Q × Σ → Q`: transition function.
- `q0`: initial state.
- `F ⊆ Q`: accepting states.

A DFA has exactly one transition for every state-symbol pair, no ε-transitions, and one initial state. It accepts if the state after the entire input is in `F`.

A **dead/trap state** is a non-accepting state that loops on every input symbol.

## 3.2 Example: binary strings ending in `1`

States:

- `q0`: empty so far or currently ends in `0`.
- `q1`: currently ends in `1`.

Start: `q0`. Final: `q1`.

| State | Input `0` | Input `1` |
|---|---|---|
| `q0` | `q0` | `q1` |
| `q1` | `q0` | `q1` |

`101` is accepted; `100` is rejected; `ε` is rejected.

## 3.3 Example: even number of `1`s

- `qE`: even number of ones; start and final.
- `qO`: odd number of ones.

| State | `0` | `1` |
|---|---|---|
| `qE` | `qE` | `qO` |
| `qO` | `qO` | `qE` |

A `0` does not change parity; a `1` switches parity. The empty string is accepted because zero is even.

## 3.4 Example: binary numbers divisible by 3

Use states for remainders modulo 3:

- `q0`: remainder 0.
- `q1`: remainder 1.
- `q2`: remainder 2.

If current remainder is `r` and next bit is `b`, then:

`r' = (2r+b) mod 3`

| State | Input `0` | Input `1` |
|---|---|---|
| `q0` | `q0` | `q1` |
| `q1` | `q2` | `q0` |
| `q2` | `q1` | `q2` |

Start and final state: `q0`. For example, `110₂=6`, so it is accepted.

## 3.5 Nondeterministic Finite Automaton (NFA)

An NFA may have zero, one or multiple next states for a state-symbol pair.

`δ: Q × Σ → 2^Q`

An ε-NFA permits transitions that consume no input:

`δ: Q × (Σ ∪ {ε}) → 2^Q`

An NFA accepts if **at least one** computation path consumes the entire input and ends in a final state.

| DFA | NFA |
|---|---|
| Exactly one next state per state-symbol pair | Zero, one or many next states |
| No ε-transitions | ε-transitions may be allowed |
| One computation path | Multiple possible paths |
| Deterministic | Nondeterministic |

**Key theorem:** DFA, NFA and ε-NFA have the same expressive power. They recognize exactly the regular languages.

## 3.6 Subset construction: NFA to DFA

Each DFA state represents a set of NFA states.

1. Start with the NFA start state; for an ε-NFA, take its ε-closure.
2. For each set `S` and input symbol `a`, collect all NFA destinations from states in `S`.
3. For an ε-NFA, take ε-closure of the destination set.
4. Treat each new set as a DFA state.
5. A DFA set is final if it contains at least one NFA final state.
6. Continue until no new sets appear.

An NFA with `n` states can yield at most `2^n` subset states, including the empty set. Some may be unreachable.

**ε-closure** of a state is the set of states reachable through zero or more ε-transitions, including the state itself.

## 3.7 DFA minimization

A minimal DFA has the fewest states among DFAs recognizing the same language.

Two states are equivalent if no suffix can distinguish them: every possible suffix either leads both to acceptance or both to rejection.

**Table-filling method:**

1. List all unordered pairs of distinct states.
2. Mark pairs where one state is final and the other is not.
3. For each unmarked pair `(p,q)` and each input symbol `a`, inspect `(δ(p,a),δ(q,a))`.
4. If that destination pair is marked, mark `(p,q)`.
5. Repeat until no new pair is marked.
6. Merge unmarked equivalent pairs.
7. Remove unreachable states.

A state is reachable if some input takes the start state to it. Unreachable states can be deleted.

## 3.8 Closure properties of regular languages

Regular languages are closed under:

- Union, intersection, complement and difference.
- Concatenation and Kleene star.
- Reversal.

If `L1` and `L2` are regular, all these resulting languages are regular too.

---

# 4. Regular Languages and the Pumping Lemma

## 4.1 Regular language

A language is regular if it is recognized by a DFA, NFA or ε-NFA, or described by a regular expression (or generated by a regular grammar).

Every finite language is regular. Infinite languages can also be regular, for example `(ab)*`.

## 4.2 Pumping lemma for regular languages

If `L` is regular, there exists a pumping length `p ≥ 1` such that every `w ∈ L` with `|w| ≥ p` can be split:

`w = xyz`

with:

1. `|xy| ≤ p`
2. `|y| > 0`
3. For every `i ≥ 0`, `xyⁱz ∈ L`

A sufficiently long accepted string has a non-empty section near the beginning that can be repeated or removed while remaining in the language.

**Why?** A DFA with `p` states reading at least `p` symbols must revisit a state among the first `p+1` visited states. The input between the repeated visits is a loop.

## 4.3 How to prove a language is not regular

1. Assume `L` is regular.
2. Let `p` be its pumping length.
3. Choose `w ∈ L` with `|w| ≥ p`.
4. Consider every valid split `w=xyz` satisfying `|xy|≤p`, `|y|>0`.
5. Show that an appropriate pumping value (often `i=0` or `i=2`) makes `xyⁱz` leave `L`.
6. This contradicts the lemma; conclude `L` is not regular.

**Quantifier trap:** You choose `w`, but you must handle every valid decomposition. You do not get to select a convenient split.

## 4.4 Worked proof: `{0ⁿ1ⁿ : n≥0}` is not regular

Assume the language is regular and let `p` be its pumping length.

Choose `w=0^p1^p`. It is in the language and is long enough.

For any valid split `w=xyz`, `|xy|≤p` and `|y|>0`. Since the first `p` symbols are all zero, `y=0^k` for some `k≥1`.

Pump down with `i=0`:

`xz = 0^(p-k)1^p`

The numbers of zeros and ones differ, so `xz` is not in the language. Contradiction. Therefore `{0ⁿ1ⁿ:n≥0}` is not regular.

## 4.5 Common mistakes

- Choosing a string shorter than `p`.
- Assuming one convenient split rather than considering all valid splits.
- Forgetting `|y|>0` or `|xy|≤p`.
- Treating the lemma as a sufficient test for regularity.

The pumping lemma is a necessary property of regular languages, not a complete test. Passing the condition does not prove regularity.

---

# 5. Context-Free Grammars (CFG)

A CFG generates strings using production rules.

## 5.1 Formal definition

A CFG is a four-tuple:

`G = (V, Σ, P, S)`

- `V`: variables/non-terminals.
- `Σ`: terminals, disjoint from `V`.
- `P`: productions `A → α`, where `A∈V` and `α∈(V∪Σ)*`.
- `S`: start variable.

It is context-free because a non-terminal can be replaced independently of its surrounding symbols.

## 5.2 Example: grammar for `aⁿbⁿ`

`S → aSb | ε`

Derivation:

`S ⇒ aSb ⇒ aaSbb ⇒ aabb`

The language is `{aⁿbⁿ:n≥0}`.

## 5.3 Leftmost and rightmost derivation

- **Leftmost:** Replace the leftmost non-terminal at every step.
- **Rightmost:** Replace the rightmost non-terminal at every step.

For `S→AB`, `A→a`, `B→b`:

- Leftmost: `S⇒AB⇒aB⇒ab`
- Rightmost: `S⇒AB⇒Ab⇒ab`

## 5.4 Parse trees

- Root is the start symbol.
- Internal nodes are non-terminals.
- Children show the right-hand side of the production used.
- Leaves, read left to right, give the generated string (ignoring ε leaves).

## 5.5 Ambiguous grammar

A CFG is ambiguous if at least one string has more than one parse tree (equivalently, more than one leftmost derivation).

Example:

`E → E+E | E*E | id`

`id+id*id` can be parsed as `(id+id)*id` or `id+(id*id)`. The grammar does not specify precedence.

An unambiguous expression grammar is:

`E → E+T | T`  
`T → T*F | F`  
`F → (E) | id`

Multiplication has higher precedence than addition.

Ambiguity is a grammar property. A language is **inherently ambiguous** if every CFG generating it is ambiguous.

## 5.6 Simplifying CFGs

**Generating variable:** Can derive a terminal-only string.

**Reachable variable:** Can be reached from the start symbol.

A useful symbol must be both generating and reachable. Remove non-generating symbols, then unreachable symbols, repeating if needed.

**ε-production:** A production `A→ε`. A variable is nullable if it can derive ε.

To remove ε-productions:

1. Find nullable variables.
2. Add alternatives formed by optionally omitting nullable occurrences in right-hand sides.
3. Preserve ε for the start symbol if the original language contains ε (often introduce a new start symbol).
4. Remove other ε-productions.

**Unit production:** `A→B`, where both are single non-terminals. Replace unit chains with the non-unit productions they lead to.

### Chomsky Normal Form (CNF)

Productions have forms:

- `A→BC` (two non-terminals), or
- `A→a` (one terminal).

If ε is in the language, the start symbol may also have `S→ε`, with the start symbol not appearing on any right-hand side.

Typical conversion: introduce a new start symbol if needed; remove ε-productions, unit productions and useless symbols; replace terminals in long right-hand sides with variables; split right-hand sides longer than two into binary productions.

### Greibach Normal Form (GNF)

Every production has form:

`A→aA1A2...Ak`

The right-hand side starts with one terminal followed by zero or more non-terminals. An optional start ε-production may be permitted if ε is in the language.

---

# 6. Context-Free Languages (CFL)

A language is context-free if some CFG generates it.

Examples:

- `{aⁿbⁿ:n≥0}` is context-free.
- Balanced parentheses are context-free.
- `{aⁱbʲ:i,j≥0}` is regular and therefore context-free.
- `{aⁿbⁿcⁿ:n≥0}` is not context-free.

## 6.1 Closure properties

CFLs are closed under:

- Union, concatenation and Kleene star.
- Reversal.
- Homomorphism and inverse homomorphism.
- Intersection with a regular language.

CFLs are **not** closed in general under:

- Intersection with another CFL.
- Complement.
- Difference of two CFLs.

Useful theorem: If `L` is context-free and `R` is regular, then `L∩R` is context-free.

## 6.2 Regular vs context-free

| Feature | Regular | Context-free |
|---|---|---|
| Grammar | Regular grammar | CFG |
| Machine | DFA/NFA | NPDA |
| Memory | Finite state | Stack |
| Arbitrary matching counts | Not in general | Can handle one nested/matched dependency |
| Example | `(ab)*` | `{aⁿbⁿ:n≥0}` |
| Arbitrary intersection closure | Yes | No |
| Complement closure | Yes | No, in general |

Every regular language is context-free, but not every context-free language is regular.

---

# 7. Push-Down Automata (PDA)

A PDA is a finite automaton with a stack. The stack is last-in, first-out (LIFO).

## 7.1 Formal definition

A PDA is commonly represented by:

`M = (Q, Σ, Γ, δ, q0, Z0, F)`

- `Q`: states.
- `Σ`: input alphabet.
- `Γ`: stack alphabet.
- `δ`: transition function.
- `q0`: initial state.
- `Z0`: initial stack symbol.
- `F`: final states.

One common transition type is:

`δ: Q × (Σ∪{ε}) × Γ → finite subsets of (Q×Γ*)`

A transition depends on the current state, input symbol (or ε), and stack top. It may consume an input symbol or consume none, and replace the top stack symbol.

## 7.2 Stack operations

- **Push:** Add a symbol to the top.
- **Pop:** Remove the top symbol.
- **No change:** Retain the stack top (notation varies).

## 7.3 Acceptance methods

A PDA may accept by:

1. **Final state:** After consuming all input, it reaches a final state.
2. **Empty stack:** After consuming all input, the stack is empty.

For NPDAs, the two acceptance conventions have equivalent expressive power: both characterize CFLs. For a particular PDA, follow the acceptance convention specified in the question.

## 7.4 PDA for `{aⁿbⁿ:n≥0}`

Idea:

1. Read `a`s and push one marker for each `a`.
2. On the first `b`, switch to the matching phase.
3. Pop one marker for every `b`.
4. Accept only after all input is consumed and the stack returns to its bottom marker (or the specified final-state condition is met).
5. Reject if an `a` occurs after the `b` phase, or if the counts differ.

For `aaabbb`, push three markers while reading `aaa`, then pop one for each of the three `b`s.

## 7.5 DPDA vs NPDA

- DPDA: at most one possible move for a configuration.
- NPDA: may have multiple possible moves.
- NPDAs recognize all CFLs.
- DPDAs recognize deterministic CFLs, a proper subset of all CFLs.

## 7.6 CFG–PDA equivalence

A language is context-free if and only if some NPDA recognizes it.

- **CFG to PDA:** Use the stack to simulate grammar derivations, expanding variables and matching terminals with input.
- **PDA to CFG:** Build grammar variables describing paths that move between states while removing a stack symbol and consuming a substring.

Know the equivalence and the basic construction idea.

---

# 8. Pumping Lemma for Context-Free Languages

## 8.1 Statement

If `L` is context-free, there is a pumping length `p` such that every `z∈L` with `|z|≥p` can be written:

`z = uvwxy`

such that:

1. `|vwx|≤p`
2. `|vx|>0`
3. For every `i≥0`, `uvⁱwxⁱy∈L`

Both `v` and `x` are pumped together; `u`, `w` and `y` remain fixed.

## 8.2 Compare the two pumping lemmas

| Regular | Context-free |
|---|---|
| `w=xyz` | `z=uvwxy` |
| Pump `y` | Pump `v` and `x` together |
| `|xy|≤p` | `|vwx|≤p` |
| `|y|>0` | `|vx|>0` |
| `xyⁱz∈L` | `uvⁱwxⁱy∈L` |

## 8.3 Worked proof: `{aⁿbⁿcⁿ:n≥0}` is not context-free

Assume `L` is context-free, with pumping length `p`. Choose:

`z=a^p b^p c^p`

Write `z=uvwxy` with `|vwx|≤p` and `|vx|>0`.

Because each block has length `p`, `vwx` can lie within one block or cross only one adjacent boundary (`a/b` or `b/c`). It cannot contain both an `a` and a `c`, because that would require including the entire middle `b` block and exceed length `p`.

Pumping `v` and `x` changes symbols in at most two adjacent blocks; the third block remains at length `p`. Since `|vx|>0`, choosing `i=0` or `i=2` makes the three counts unequal or disrupts the required block order. Thus the pumped string is not in `L`, contradicting the lemma.

Therefore `{aⁿbⁿcⁿ:n≥0}` is not context-free.

**Exam tip:** Explicitly discuss the possible positions of `vwx`; do not merely say that pumping changes the counts.

The CFL pumping lemma is a necessary condition, not a complete test. Failure to find a contradiction does not prove context-freeness.

---

# 9. Turing Machines

A Turing machine (TM) is a mathematical model of general-purpose computation. It has a finite control, an unbounded tape, and a read/write head.

## 9.1 Components

- **Tape:** Cells containing input and blanks elsewhere.
- **Tape alphabet (`Γ`):** Symbols that can appear on the tape.
- **Read/write head:** Reads and writes one cell and moves left or right (some definitions allow a stationary move).
- **Finite control:** Current state.
- **Transition function:** Determines the next state, symbol to write and head movement.

## 9.2 Formal definition

One common deterministic TM tuple is:

`M=(Q,Σ,Γ,δ,q0,B,F)`

- `Q`: states.
- `Σ`: input alphabet.
- `Γ`: tape alphabet, with `Σ⊆Γ`.
- `δ`: transition function.
- `q0`: start state.
- `B`: blank symbol.
- `F`: accepting states.

A common transition type is:

`δ: Q×Γ → Q×Γ×{L,R}`

Definitions vary: some use explicit accept/reject halting states; some allow a stationary move.

## 9.3 How it operates

1. Read the symbol under the head.
2. Look up the transition for the current state and symbol.
3. Write a symbol.
4. Move the head.
5. Change state.
6. Continue until it halts or runs forever.

A TM can accept, reject, or loop forever.

## 9.4 Recognizer vs decider

**Turing-recognizable (recursively enumerable):** A TM accepts every string in the language. For a string outside the language, it may reject or loop forever.

**Decidable (recursive):** A TM halts on every input, accepting members and rejecting non-members.

Every decidable language is recognizable, but not every recognizable language is decidable.

## 9.5 Variants of Turing machines

Common variants include multi-tape, multi-track, nondeterministic, two-way infinite tape machines and enumerators.

For the usual computability model, these variants have the same language-recognition power as the standard TM, though their efficiency may differ. A multi-tape TM can be simulated by a single-tape TM; a deterministic TM can simulate a nondeterministic TM for recognition, potentially with substantial time overhead.

## 9.6 Universal Turing machine

A Universal Turing Machine (UTM) takes an encoding of a machine `M` and input `w`, then simulates `M` on `w`:

`U(<M>,w)=M(w)`

This is the theoretical foundation of general-purpose programmable computers: one machine can execute descriptions of other machines.

## 9.7 Church–Turing thesis

The Church–Turing thesis says that anything effectively computable by an algorithm can be computed by a Turing machine. It is a thesis, not a mathematical theorem, because “effectively computable” is an informal notion.

---

# 10. Undecidability

A decision problem asks for a YES/NO answer. It is decidable if an algorithm always halts and answers correctly. It is undecidable if no such algorithm exists.

## 10.1 Decidable vs undecidable

| Decidable | Undecidable |
|---|---|
| A decider exists | No decider exists |
| Always halts with correct answer | No algorithm can always halt with the correct answer |
| Example: DFA membership | Example: general TM acceptance |

## 10.2 Acceptance problem

`A_TM={ <M,w> : M is a TM that accepts input w }`

It asks whether machine `M` accepts `w`. `A_TM` is recognizable but undecidable. A universal TM can simulate `M` on `w`; if `M` accepts, the simulator accepts. If `M` loops, the simulator may also loop.

## 10.3 Halting problem

`HALT_TM={ <M,w> : M halts on input w }`

It asks whether a given TM eventually halts on a given input. The general halting problem is undecidable.

### Diagonalization intuition

Assume a decider `H(M,w)` correctly determines whether `M` halts on `w`.

Construct machine `D`, on input `<M>`:

- Run `H(M,<M>)`.
- If `H` says `M` halts, make `D` loop forever.
- If `H` says `M` does not halt, make `D` halt.

Now run `D` on `<D>`:

- If `H(D,<D>)` says it halts, `D` loops.
- If it says it does not halt, `D` halts.

Both cases contradict `H`. Thus no such decider exists.

## 10.4 Reduction

A reduction transforms instances of one problem into instances of another while preserving the answer.

To prove `B` undecidable:

1. Start with known undecidable problem `A`.
2. Transform any instance of `A` into an instance of `B`.
3. Ensure the transformation is computable and preserves YES/NO.
4. If `B` had a decider, it would decide `A`.
5. Since `A` is undecidable, `B` is undecidable.

`A ≤m B` means `A` many-one reduces to `B`.

**Direction matters:** To prove `B` undecidable, reduce known undecidable problem `A` **to** `B`.

## 10.5 Rice's theorem

Rice's theorem:

Every non-trivial semantic property of the language recognized by an arbitrary Turing machine is undecidable.

- **Semantic:** Depends only on the language recognized, not the machine's code or description.
- **Non-trivial:** True for at least one recognizable language and false for at least one recognizable language.

Examples of undecidable properties for arbitrary TMs:

- Is the recognized language empty?
- Is it finite?
- Is it regular?
- Does it contain all strings over its alphabet?

Rice's theorem does not cover arbitrary syntactic properties of machine descriptions, nor trivial properties true for all or no machines.

## 10.6 Common decision problems

| Problem | Status |
|---|---|
| Does a DFA accept a given string? | Decidable |
| Is a DFA language empty? | Decidable |
| Are two DFAs equivalent? | Decidable |
| Is a regular expression's language empty? | Decidable |
| Is a CFG's language empty? | Decidable |
| Is a CFG ambiguous? | Undecidable in general |
| Is a CFG's language equal to `Σ*`? | Undecidable in general |
| Does a TM accept a given input? | Undecidable in general |
| Does a TM halt on a given input? | Undecidable |
| Is a TM-recognized language empty? | Undecidable (Rice's theorem) |

---

# 11. High-Value Comparisons

## 11.1 DFA, PDA and TM

| Feature | DFA/NFA | PDA | Turing machine |
|---|---|---|---|
| Memory | Finite states | Stack | Unbounded tape |
| Reads input | Yes | Yes | Yes |
| Writes to memory | No | Stack operations | Tape read/write |
| Language class | Regular | CFL (NPDA) | Recursively enumerable |
| Recognizes `{aⁿbⁿ}`? | No | Yes | Yes |
| Recognizes `{aⁿbⁿcⁿ}`? | No | No | Yes |

## 11.2 Recognizable vs decidable

| Recognizable | Decidable |
|---|---|
| Accepts every member | Accepts every member |
| May loop on non-members | Must halt on every input |
| May not reject all non-members | Rejects every non-member |
| Recursively enumerable | Recursive |

## 11.3 Language examples

| Language | Regular? | Context-free? |
|---|---:|---:|
| `{0,1}*` | Yes | Yes |
| `{0ⁿ:n≥0}` | Yes | Yes |
| `{0ⁿ1ᵐ:n,m≥0}` | Yes | Yes |
| `{0ⁿ1ⁿ:n≥0}` | No | Yes |
| `{0ⁿ1ⁿ2ⁿ:n≥0}` | No | No |
| Balanced parentheses | No | Yes |
| `{ww:w∈{0,1}*}` | No | No |

---

# 12. GATE Problem-Solving Strategy

## DFA construction

1. Ask what information about the prefix must be remembered.
2. Create states for the necessary conditions.
3. Define every transition for every symbol.
4. Mark start and final states.
5. Test `ε`, short strings and boundary cases.

Common designs: parity uses two states; remainder modulo `k` uses `k` states; suffix recognition tracks matched suffix length; substring recognition tracks the longest useful prefix matched.

## NFA-to-DFA conversion

1. Start with ε-closure of the start state.
2. For every subset and symbol, collect destinations.
3. Take ε-closure.
4. Create new subsets until no new set appears.
5. Mark subsets containing NFA final states.

## Pumping-lemma questions

- Regular: split `xyz`, pump `y`.
- Context-free: split `uvwxy`, pump `v` and `x` together.

Respect the quantifiers. For a non-membership proof, choose a suitable long string and show that every permitted split fails for some pumping value.

## Decidability questions

Ask whether the machine is finite-state or a general TM; whether the problem is membership, emptiness, equivalence or a semantic property; whether a known algorithm exists; whether a known undecidable problem can be reduced to it; and whether Rice's theorem applies.

---

# 13. Quick Revision Sheet

## Definitions

- **Regular expression:** Algebraic description of a regular language.
- **DFA:** Finite-state machine with exactly one transition per state-symbol pair.
- **NFA:** Finite-state machine with possibly multiple next states.
- **Regular language:** Language recognized by a finite automaton.
- **CFG:** Grammar with one non-terminal on the left of each production.
- **CFL:** Language generated by a CFG.
- **PDA:** Finite automaton with a stack.
- **TM:** Machine with an unbounded read/write tape.
- **Decidable:** A TM halts on every input and decides membership.
- **Recognizable:** A TM accepts members but may loop on non-members.
- **Undecidable:** No algorithm always halts and answers correctly.

## Core statements

| Topic | Key statement |
|---|---|
| DFA | `M=(Q,Σ,δ,q0,F)` |
| NFA | `δ:Q×Σ→2^Q` |
| ε-NFA | `δ:Q×(Σ∪{ε})→2^Q` |
| CFG | `G=(V,Σ,P,S)` |
| PDA | `M=(Q,Σ,Γ,δ,q0,Z0,F)` |
| TM | `M=(Q,Σ,Γ,δ,q0,B,F)` (one convention) |
| Regular pumping | `w=xyz`, `|xy|≤p`, `|y|>0`, `xyⁱz∈L` |
| CFL pumping | `z=uvwxy`, `|vwx|≤p`, `|vx|>0`, `uvⁱwxⁱy∈L` |
| Hierarchy | `Regular ⊊ CFL ⊊ CSL ⊊ RE` |
| TM classes | `Decidable ⊆ Recognizable` |
| NFA/DFA | Same expressive power |
| CFG/NPDA | Same expressive power |

## Common GATE traps

1. `∅` and `{ε}` are different.
2. `∅*={ε}`.
3. DFA and NFA recognize the same class.
4. Every regular language is context-free; the reverse is false.
5. NPDAs recognize all CFLs; DPDAs recognize a proper subset.
6. CFLs are not closed under arbitrary intersection or complement.
7. CFLs are closed under intersection with regular languages.
8. The regular pumping lemma pumps one substring; the CFL lemma pumps two together.
9. Pumping lemmas are necessary properties, not sufficient tests.
10. A recognizable language need not be decidable.
11. The halting problem is undecidable.
12. Rice's theorem concerns non-trivial semantic properties of TM-recognized languages.
13. To prove `B` undecidable from known undecidable `A`, reduce `A` to `B`.

---

# 14. Practice Questions

Attempt these before checking the solutions.

## Section A – Conceptual

**Q1.** Difference between `∅` and `ε`?

**Q2.** Difference between DFA and NFA? Do they recognize different language classes?

**Q3.** What is the purpose of a dead state?

**Q4.** Define a CFG and name its four components.

**Q5.** Why can a PDA recognize `{aⁿbⁿ}` but a finite automaton cannot?

**Q6.** What is an ambiguous grammar?

**Q7.** Give two closure properties of regular languages and two of CFLs.

**Q8.** Difference between a TM recognizer and decider?

**Q9.** State the halting problem.

**Q10.** State Rice's theorem.

## Section B – MCQs

**Q11. Which language is always regular?**

A. `{aⁿbⁿ:n≥0}`  
B. `{aⁿ:n≥0}`  
C. `{aⁿbⁿcⁿ:n≥0}`  
D. `{ww:w∈{0,1}*}`

**Q12. Which machines recognize exactly the regular languages?**

A. DFA only  
B. NFA only  
C. ε-NFA only  
D. All of the above

**Q13. Which is not a general CFL closure property?**

A. Union  
B. Concatenation  
C. Kleene star  
D. Intersection with another CFL

**Q14. In the regular pumping lemma, which part must be non-empty?**

A. `x`  
B. `y`  
C. `z`  
D. `xz`

**Q15. Which condition belongs to the CFL pumping lemma?**

A. `|vwx|≤p`  
B. `|uv|≤p`  
C. `|v|=0`  
D. Only `u` is pumped

**Q16. Which statement is true?**

A. Every recognizable language is decidable.  
B. Every decidable language is recognizable.  
C. Every undecidable language is unrecognizable.  
D. A recognizer must halt on all inputs.

**Q17. The general halting problem is:**

A. Decidable  
B. Regular  
C. Undecidable  
D. Context-free

**Q18. Which is context-free but not regular?**

A. `{a,b}*`  
B. `{aⁿbⁿ:n≥0}`  
C. `a*`  
D. `(ab)*`

**Q19. Which is true about subset construction?**

A. An n-state NFA may produce up to `2^n` DFA states.  
B. It always produces exactly n states.  
C. It cannot handle ε-transitions.  
D. It changes the language.

**Q20. Rice's theorem applies to:**

A. Every syntactic property of a program.  
B. Non-trivial semantic properties of TM-recognized languages.  
C. Only DFA minimization.  
D. Only finite languages.

## Section C – Multiple-select

**Q21. Which are regular-language closure properties?**

A. Union  
B. Complement  
C. Concatenation  
D. Kleene star

**Q22. Which are true for CFLs?**

A. Closed under union  
B. Closed under concatenation  
C. Closed under intersection with a regular language  
D. Closed under arbitrary intersection

**Q23. Which statements are true?**

A. Every regular language is context-free.  
B. Every CFL is regular.  
C. Every DFA language can be described by a regular expression.  
D. Every NFA can be converted to an equivalent DFA.

**Q24. Which are undecidable for arbitrary TMs?**

A. Whether the machine halts on a given input  
B. Whether its recognized language is empty  
C. Whether its recognized language is finite  
D. Whether a DFA accepts a fixed input

## Section D – Construction and numerical

**Q25.** Construct a DFA over `{0,1}` accepting strings with an even number of `1`s.

**Q26.** Construct a DFA over `{0,1}` accepting strings ending in `00`.

**Q27.** Give a regular expression for strings over `{a,b}` containing at least one `a`.

**Q28.** Give a CFG for `{aⁿbⁿ:n≥0}` and derive `aaabbb`.

**Q29.** How many subsets are possible for a 4-state NFA? What is the maximum number of DFA states before removing unreachable subsets?

**Q30.** Classify `{aⁿbⁿcⁿ:n≥0}` as regular, context-free, both or neither.

---

# 15. Answer Key and Detailed Solutions

## Section A

**A1.** `∅` is a language with zero strings. `ε` is the empty string. `{ε}` contains one string; `∅` contains none.

**A2.** A DFA has exactly one next state for each state-symbol pair. An NFA may have zero, one or many. Both recognize exactly the regular languages.

**A3.** A dead state makes transitions total. Once entered, the machine cannot reach an accepting state; it represents an invalid continuation.

**A4.** `G=(V,Σ,P,S)`: variables, terminals, productions and start variable.

**A5.** A finite automaton has only finitely many states and cannot store an arbitrary count of `a`s to compare with later `b`s. A PDA pushes a marker per `a` and pops one per `b`.

**A6.** A grammar is ambiguous if some generated string has more than one parse tree, equivalently more than one leftmost derivation.

**A7.** Regular languages are closed under union and complement. CFLs are closed under union and concatenation (also intersection with a regular language), but not arbitrary intersection or complement.

**A8.** A recognizer accepts members but may loop on non-members. A decider halts on every input, accepting members and rejecting non-members.

**A9.** Given arbitrary TM `M` and input `w`, determine whether `M` eventually halts on `w`. No algorithm correctly decides this for every pair.

**A10.** Every non-trivial semantic property of the language recognized by an arbitrary TM is undecidable.

## Section B – MCQ answers

| Question | Answer | Explanation |
|---|---|---|
| Q11 | B | `a*` is a regular expression. |
| Q12 | D | DFA, NFA and ε-NFA have equal expressive power. |
| Q13 | D | CFLs are not closed under arbitrary intersection. |
| Q14 | B | `y` must have positive length. |
| Q15 | A | The lemma requires `|vwx|≤p` and `|vx|>0`. |
| Q16 | B | Every decider is a recognizer that always halts. |
| Q17 | C | The general halting problem is undecidable. |
| Q18 | B | A stack can match equal counts; finite-state memory cannot. |
| Q19 | A | Subset construction can create up to `2^n` subsets. |
| Q20 | B | Rice's theorem concerns non-trivial semantic language properties. |

## Section C – MSQ answers

**A21.** A, B, C, D. Regular languages are closed under all four operations.

**A22.** A, B, C. CFLs are closed under union, concatenation and intersection with a regular language, but not arbitrary intersection.

**A23.** A, C, D. Every regular language is context-free; every DFA language has a regular expression; every NFA has an equivalent DFA. The reverse inclusion from CFL to regular is false.

**A24.** A, B, C. Halting, emptiness and finiteness for arbitrary TM-recognized languages are undecidable. DFA membership is decidable by simulating the DFA on the input.

## Section D – Worked solutions

**A25. DFA for an even number of `1`s**

States: `qE` (even, start and final) and `qO` (odd).

| State | `0` | `1` |
|---|---|---|
| `qE` | `qE` | `qO` |
| `qO` | `qO` | `qE` |

A zero preserves parity; a one toggles parity.

**A26. DFA for strings ending in `00`**

- `q0`: no useful trailing zero.
- `q1`: current string ends in one zero.
- `q2`: current string ends in `00` (final).

| State | `0` | `1` |
|---|---|---|
| `q0` | `q1` | `q0` |
| `q1` | `q2` | `q0` |
| `q2` | `q2` | `q0` |

Start `q0`; final `q2`.

**A27.** `(a+b)*a(a+b)*`. Any prefix and suffix are allowed, with at least one required `a`.

**A28.** Grammar: `S→aSb | ε`.

`S⇒aSb⇒aaSbb⇒aaaSbbb⇒aaabbb`

**A29.** `2^4=16` subsets, including the empty set. Thus at most 16 DFA states before unreachable subsets are removed.

**A30.** Neither regular nor context-free. It is not regular, and the CFL pumping lemma can prove it is not context-free.

---

# 16. Final Study Checklist

- [ ] Understand alphabets, strings, languages and language operations.
- [ ] Read and write regular expressions.
- [ ] Construct DFAs for parity, suffix, substring and modulo conditions.
- [ ] Understand NFA and ε-NFA transitions.
- [ ] Convert NFA/ε-NFA to DFA using subset construction.
- [ ] Minimize DFAs using state equivalence/table filling.
- [ ] Know regular-language closure properties.
- [ ] Apply the regular pumping lemma correctly.
- [ ] Write CFGs for standard languages.
- [ ] Perform leftmost/rightmost derivations.
- [ ] Identify ambiguity and parse trees.
- [ ] Understand CFG simplification, CNF and GNF.
- [ ] Know CFL closure properties and limitations.
- [ ] Trace PDAs using stack operations.
- [ ] Understand CFG–NPDA equivalence.
- [ ] Apply the CFL pumping lemma correctly.
- [ ] Understand TM configurations and transitions.
- [ ] Distinguish recognizers from deciders.
- [ ] Understand universal TMs and the Church–Turing thesis.
- [ ] Explain the halting problem and diagonalization.
- [ ] Use reductions and Rice's theorem.

**Suggested revision order:** Regular expressions → DFA/NFA → regular pumping lemma → CFG → PDA → CFL pumping lemma → Turing machines → undecidability.

**Exam advice:** Do not memorize only definitions. Practice automaton construction, transition tables, grammar derivations, pumping-lemma proofs, closure-property counterexamples and decidability classifications.
