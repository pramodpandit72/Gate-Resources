# GATE CSE Digital Logic — Complete Study Material

> **Syllabus covered:** Boolean algebra and minimization (algebraic technique, Karnaugh map, tabular method); design of combinational and sequential circuits; number representation and arithmetic (fixed-point and floating-point).
>
> **Level:** Beginner foundations to GATE CSE problem-solving.
>
> **Notation:** `+` means OR, `·` or adjacency means AND, and `'` means NOT. Unless stated otherwise, variables are binary.

---

## Table of Contents

1. [Syllabus checklist and prerequisites](#1-syllabus-checklist-and-prerequisites)
2. [Digital logic foundations](#2-digital-logic-foundations)
3. [Boolean algebra](#3-boolean-algebra)
4. [Boolean function representation and canonical forms](#4-boolean-function-representation-and-canonical-forms)
5. [Boolean minimization using algebra](#5-boolean-minimization-using-algebra)
6. [Karnaugh maps](#6-karnaugh-maps)
7. [Tabular minimization: Quine–McCluskey method](#7-tabular-minimization-quine-mccluskey-method)
8. [Combinational circuit design](#8-combinational-circuit-design)
9. [Sequential circuit design](#9-sequential-circuit-design)
10. [Number representation](#10-number-representation)
11. [Fixed-point arithmetic](#11-fixed-point-arithmetic)
12. [Floating-point representation and arithmetic](#12-floating-point-representation-and-arithmetic)
13. [GATE examination strategy, traps and revision sheet](#13-gate-examination-strategy-traps-and-revision-sheet)
14. [Practice questions](#14-practice-questions)
15. [Detailed answer key](#15-detailed-answer-key)

---

# 1. Syllabus checklist and prerequisites

## 1.1 Coverage checklist

- [ ] Binary variables, logic levels, gates and truth tables
- [ ] Boolean operators and Boolean algebra laws
- [ ] De Morgan's laws and duality
- [ ] SOP, POS, minterms and maxterms
- [ ] Canonical and standard forms
- [ ] Algebraic minimization
- [ ] Karnaugh maps, adjacency, wrap-around and grouping
- [ ] Don't-care conditions
- [ ] Prime implicants and essential prime implicants
- [ ] Quine–McCluskey tabular method
- [ ] Combinational circuit design procedure
- [ ] Adders, subtractors and arithmetic circuits
- [ ] Multiplexers, demultiplexers, encoders and decoders
- [ ] Comparators, parity circuits and code converters
- [ ] Latches and flip-flops
- [ ] Characteristic tables and equations
- [ ] Excitation tables
- [ ] Registers and counters
- [ ] Synchronous and asynchronous sequential circuits
- [ ] State diagrams and state tables
- [ ] Number systems and base conversion
- [ ] Signed number representation
- [ ] Fixed-point representation and arithmetic
- [ ] Overflow and range
- [ ] Floating-point format, normalization and IEEE 754
- [ ] Floating-point addition, subtraction, multiplication and rounding

## 1.2 Prerequisites

You need only a few mathematical ideas:

- **Binary digit (bit):** a digit that can be 0 or 1.
- **Truth table:** a table listing the output for every possible input combination.
- **Set of inputs:** for `n` binary inputs there are `2^n` possible input combinations.
- **Complement:** the opposite binary value; complement of 0 is 1 and of 1 is 0.
- **Place value:** in base `r`, positions have weights `r^0, r^1, r^2, ...` to the left of the radix point and `r^-1, r^-2, ...` to its right.

---

# 2. Digital logic foundations

## 2.1 What is digital logic?

Digital logic is the study of circuits that process information using discrete values, usually represented by 0 and 1.

A digital circuit receives binary inputs, applies logical operations, and produces binary outputs.

Examples include:
- A processor's arithmetic logic unit (ALU).
- Memory address and control circuits.
- Counters and timers.
- Digital communication equipment.

A physical circuit uses voltage ranges to represent logical values. The exact voltage levels depend on the technology. In logical analysis, we work with abstract values 0 and 1.

## 2.2 Basic logic gates

### NOT gate

The NOT gate reverses its input.

| A | Y = A' |
|---:|---:|
| 0 | 1 |
| 1 | 0 |

### AND gate

The output is 1 only when all inputs are 1.

| A | B | Y = A·B |
|---:|---:|---:|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

### OR gate

The output is 1 when at least one input is 1.

| A | B | Y = A+B |
|---:|---:|---:|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

### NAND and NOR gates

- NAND: `(A·B)'`, the complement of AND.
- NOR: `(A+B)'`, the complement of OR.

| A | B | NAND | NOR |
|---:|---:|---:|---:|
| 0 | 0 | 1 | 1 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 |

### XOR and XNOR gates

- XOR is 1 when the inputs are different.
- XNOR is 1 when the inputs are equal.

| A | B | A XOR B | A XNOR B |
|---:|---:|---:|---:|
| 0 | 0 | 0 | 1 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

For two inputs:
\[
A\oplus B=A'B+AB'
\]
\[
A\odot B=AB+A'B'
\]

## 2.3 Universal gates

A gate is called universal if any Boolean function can be implemented using only that type of gate.

NAND and NOR are universal.

Using NAND:
\[
A' = A\ NAND\ A
\]
\[
AB = (A\ NAND\ B)\ NAND\ (A\ NAND\ B)
\]
\[
A+B = (A\ NAND\ A)\ NAND\ (B\ NAND\ B)
\]

Using NOR:
\[
A' = A\ NOR\ A
\]
\[
A+B = (A\ NOR\ B)\ NOR\ (A\ NOR\ B)
\]
\[
AB = (A\ NOR\ A)\ NOR\ (B\ NOR\ B)
\]

**GATE point:** A circuit expressed in NAND-only or NOR-only form can be obtained by applying these identities and De Morgan's laws.

---

# 3. Boolean algebra

## 3.1 Definition

Boolean algebra is an algebra in which each variable takes only one of two values: 0 or 1. It is used to describe and simplify digital circuits.

A Boolean expression such as
\[
F=A'B+AC
\]
describes a circuit whose output is 1 for selected combinations of `A`, `B` and `C`.

## 3.2 Fundamental laws

| Law | OR form | AND form |
|---|---|---|
| Identity | `A+0=A` | `A·1=A` |
| Null / domination | `A+1=1` | `A·0=0` |
| Idempotent | `A+A=A` | `A·A=A` |
| Complement | `A+A'=1` | `A·A'=0` |
| Involution | `(A')'=A` | |
| Commutative | `A+B=B+A` | `AB=BA` |
| Associative | `(A+B)+C=A+(B+C)` | `(AB)C=A(BC)` |
| Distributive | `A(B+C)=AB+AC` | `A+BC=(A+B)(A+C)` |
| Absorption | `A+AB=A` | `A(A+B)=A` |

The two distributive laws are both valid. The second one may look unfamiliar because it distributes OR over AND.

## 3.3 Useful reduction identities

These are especially useful in algebraic minimization.

1. `A + A'B = A + B`
2. `A(A' + B) = AB`
3. `AB + AB' = A`
4. `(A+B)(A+B') = A`
5. `AB + A'C + BC = AB + A'C` (consensus theorem)
6. `A + A' = 1`
7. `AA' = 0`

### Example: absorption

Simplify:
\[
F=A+AB
\]
Take `A` common:
\[
F=A(1+B)=A\cdot1=A
\]

### Example: using the covering identity

\[
F=A+A'B
\]
Insert the identity `A+A'=1`:
\[
F=(A+A')(A+B)=1\cdot(A+B)=A+B
\]

## 3.4 De Morgan's theorems

\[
(A+B)'=A'B'
\]
\[
(AB)'=A'+B'
\]

For more than two variables:
\[
(A+B+C)'=A'B'C'
\]
\[
(ABC)'=A'+B'+C'
\]

**Memory rule:** Complement every variable and interchange AND with OR.

### Example

\[
F=(A+BC)'
\]
Apply De Morgan:
\[
F=A'(BC)'=A'(B'+C')
\]

## 3.5 Principle of duality

The dual of a Boolean expression is obtained by interchanging:
- OR (`+`) with AND (`·`)
- 0 with 1

Variables and complements remain unchanged.

Example:
- Original: `A+0=A`
- Dual: `A·1=A`

If a Boolean identity is valid, its dual is also valid.

## 3.6 SOP and POS

### Sum of Products (SOP)

An OR of one or more product terms.

Example:
\[
F=A'B+BC+AC'
\]

Each product term is an AND of literals.

### Product of Sums (POS)

An AND of one or more sum terms.

Example:
\[
F=(A+B')(B+C)(A'+C')
\]

Each sum term is an OR of literals.

A function may have many equivalent SOP and POS expressions. A **minimal** expression is one with a low implementation cost under the chosen cost measure (for example, number of terms or literals).

---

# 4. Boolean function representation and canonical forms

## 4.1 Minterms

A minterm is an AND term containing every input variable exactly once, either complemented or uncomplemented.

For variables `A,B,C`:
- `A'B'C'` represents input `000`.
- `A'B'C` represents input `001`.
- `A'BC'` represents input `010`.
- `ABC` represents input `111`.

A minterm is 1 for exactly one input combination.

With variable order `A,B,C`, the minterm index is the binary value of the input combination.

| A B C | Binary index | Minterm |
|---|---:|---|
| 000 | 0 | `m0=A'B'C'` |
| 001 | 1 | `m1=A'B'C` |
| 010 | 2 | `m2=A'BC'` |
| 011 | 3 | `m3=A'BC` |
| 100 | 4 | `m4=AB'C'` |
| 101 | 5 | `m5=AB'C` |
| 110 | 6 | `m6=ABC'` |
| 111 | 7 | `m7=ABC` |

## 4.2 Maxterms

A maxterm is an OR term containing every variable exactly once. It is 0 for exactly one input combination.

For a maxterm:
- If the corresponding input bit is 0, write the variable uncomplemented.
- If the corresponding input bit is 1, write the variable complemented.

For example, for input `101`, the maxterm is:
\[
M_5=(A'+B+C')
\]

## 4.3 Canonical SOP

Canonical SOP is the sum of minterms for which the function is 1.

Notation:
\[
F(A,B,C)=\Sigma m(1,2,5,7)
\]

This means the function is 1 at input indices 1, 2, 5 and 7.

Expanded:
\[
F=A'B'C+A'BC'+AB'C+ABC
\]

## 4.4 Canonical POS

Canonical POS is the product of maxterms for which the function is 0.

If:
\[
F=\Sigma m(1,2,5,7)
\]
then the zero indices are `0,3,4,6`, so:
\[
F=\Pi M(0,3,4,6)
\]

**Important:** For `n` variables, there are `2^n` rows. The minterm indices where `F=1` and maxterm indices where `F=0` together cover all rows.

## 4.5 Converting a term to canonical form

Every term must contain all variables.

Example:
\[
F=AB
\]
For variables `A,B,C`, expand using `C+C'=1`:
\[
F=AB(C+C')=ABC+ABC'
\]
Thus:
\[
F=\Sigma m(6,7)
\]
for variable order `A,B,C`.

---

# 5. Boolean minimization using algebra

## 5.1 Purpose

Minimization reduces a Boolean expression while preserving its truth table. A simpler expression can require fewer gates, fewer inputs per gate, less area and often less power and delay.

There may be multiple minimal expressions. The best implementation depends on the cost metric and available gates.

## 5.2 Algebraic technique: worked examples

### Example 1

Simplify:
\[
F=AB+AB'
\]
Take `A` common:
\[
F=A(B+B')=A\cdot1=\boxed{A}
\]

### Example 2

Simplify:
\[
F=A+A'B
\]
Using `X+X'Y=X+Y`:
\[
\boxed{F=A+B}
\]

### Example 3

Simplify:
\[
F=(A+B)(A+B')
\]
Using `(X+Y)(X+Y')=X`:
\[
\boxed{F=A}
\]

### Example 4: consensus theorem

Simplify:
\[
F=AB+A'C+BC
\]
The term `BC` is the consensus term and is redundant:
\[
\boxed{F=AB+A'C}
\]

### Example 5: multi-step

\[
F=AB+A'B+AC
\]
Group the first two terms:
\[
F=B(A+A')+AC=B+AC
\]
Therefore:
\[
\boxed{F=B+AC}
\]

## 5.3 How to approach algebraic minimization

1. Look for common literals and take them outside brackets.
2. Search for a variable and its complement, such as `X` and `X'`.
3. Apply absorption and covering identities.
4. Apply De Morgan's laws when complemented brackets appear.
5. Use consensus to remove redundant terms.
6. Verify the final expression against the original truth table if the expression is complicated.

**Limitation:** Algebraic minimization does not have a single mechanical grouping procedure. It can be difficult to know which identity to apply. K-map and tabular methods provide more systematic procedures.

---

# 6. Karnaugh maps

## 6.1 What is a K-map?

A Karnaugh map (K-map) is a visual method for minimizing Boolean functions. Each cell represents one minterm. Adjacent cells differ in exactly one variable.

K-maps are most convenient for a small number of variables, commonly up to 4 or 5 in hand calculations.

## 6.2 Gray-code ordering

K-map rows and columns use Gray-code order:
\[
00,\ 01,\ 11,\ 10
\]

Adjacent labels differ in only one bit. Do not use ordinary binary order `00,01,10,11`.

## 6.3 Two-variable K-map

For `F(A,B)`:

| A \ B | 0 | 1 |
|---|---:|---:|
| 0 | m0 | m1 |
| 1 | m2 | m3 |

Each cell is one input combination.

## 6.4 Three-variable K-map

Use `A` for rows and `BC` for columns.

| A \ BC | 00 | 01 | 11 | 10 |
|---|---:|---:|---:|---:|
| 0 | m0 | m1 | m3 | m2 |
| 1 | m4 | m5 | m7 | m6 |

## 6.5 Four-variable K-map

Use `AB` for rows and `CD` for columns.

| AB \ CD | 00 | 01 | 11 | 10 |
|---|---:|---:|---:|---:|
| 00 | m0 | m1 | m3 | m2 |
| 01 | m4 | m5 | m7 | m6 |
| 11 | m12 | m13 | m15 | m14 |
| 10 | m8 | m9 | m11 | m10 |

The first and last rows are adjacent. The first and last columns are also adjacent.

## 6.6 Rules for grouping 1s (SOP minimization)

1. Make rectangular groups containing `1, 2, 4, 8, ...` cells.
2. A group must contain a power of two number of cells.
3. Make groups as large as possible.
4. Every required 1 must be covered by at least one group.
5. Groups may overlap when overlap helps produce larger groups.
6. Diagonal cells are not adjacent.
7. Opposite edges wrap around and are adjacent.
8. A group may contain only cells that are 1 or allowed don't-care cells.
9. Do not include a 0 in an SOP group.

For a group of `2^k` cells in an `n`-variable map, the resulting product term contains `n-k` literals.

## 6.7 Reading a group

Keep only variables that have the same value throughout the group:
- Constant 1 → uncomplemented literal.
- Constant 0 → complemented literal.
- Changing variable → eliminate it.

### Example 1: pair

\[
F(A,B,C)=\Sigma m(1,3)
\]

Minterms:
- `m1 = 001`
- `m3 = 011`

`A=0` and `C=1` remain fixed; `B` changes.

Therefore:
\[
\boxed{F=A'C}
\]

### Example 2: four-cell group

\[
F(A,B,C)=\Sigma m(0,1,2,3)
\]

All four cells have `A=0`; `B` and `C` vary.

\[
\boxed{F=A'}
\]

### Example 3: wrap-around adjacency

In a four-variable K-map, columns `CD=00` and `CD=10` are adjacent because the map wraps around. Their labels differ only in `D`.

This edge adjacency is frequently tested.

## 6.8 SOP minimization example

Given:
\[
F(A,B,C)=\Sigma m(1,3,5,7)
\]

Binary minterms:
- `m1=001`
- `m3=011`
- `m5=101`
- `m7=111`

All have `C=1`, while `A` and `B` vary. They form one group of four.

\[
\boxed{F=C}
\]

## 6.9 POS minimization

For POS, group the **0s** rather than the 1s.

Within a zero-group:
- A variable fixed at 0 appears uncomplemented in the sum term.
- A variable fixed at 1 appears complemented in the sum term.
- A changing variable is eliminated.

Example: if a zero-group has `A=0` and `B` changes, the corresponding sum term is `A`.

The final POS is the AND of the sum terms from all zero-groups.

## 6.10 Don't-care conditions

A don't-care input combination is one for which the output is irrelevant or is not expected to occur in normal operation.

Notation:
\[
F=\Sigma m(1,3,7),\quad d=\Sigma m(5)
\]

A don't-care cell may be treated as 0 or 1, whichever gives a simpler expression. It does not have to be used.

**Crucial rule:** Do not cover a required 1 with a 0. A don't-care may be included in a group, but it need not be.

## 6.11 Prime implicants

- **Implicant:** a product term that covers one or more 1-cells and no 0-cell.
- **Prime implicant (PI):** an implicant that cannot be combined into a larger valid implicant.
- **Essential prime implicant (EPI):** a prime implicant that covers at least one 1-cell not covered by any other prime implicant.

All essential prime implicants must be selected in a minimum cover.

## 6.12 K-map mistakes to avoid

- Using binary order instead of Gray-code order.
- Forgetting wrap-around adjacency.
- Grouping diagonal cells.
- Making groups of 3, 5 or 6 cells.
- Leaving a required 1 uncovered.
- Including a 0 in a group.
- Assuming every don't-care must be used.
- Removing a variable that is actually constant in a group.
- Confusing SOP grouping of 1s with POS grouping of 0s.

---

# 7. Tabular minimization: Quine–McCluskey method

## 7.1 Why use the tabular method?

The Quine–McCluskey method is a systematic Boolean minimization procedure. It is especially useful when the number of variables is too large for a hand-drawn K-map or when a repeatable algorithm is needed.

It has two main phases:
1. Find all prime implicants by combining minterms.
2. Select a minimum set of prime implicants that covers all required minterms.

## 7.2 Combining terms

Two binary terms can be combined if:
- They have the same number of 1s in their uncombined forms' group stage.
- They differ in exactly one bit.
- The differing bit is replaced with `-`.

Example:
\[
0101,\ 0111 \rightarrow 01-1
\]

The dash means that variable can be either 0 or 1.

Terms with more than one differing bit cannot be combined in one step.

## 7.3 Procedure

1. List all ON-set minterms in binary.
2. Group them by number of 1s.
3. Compare terms in adjacent groups.
4. Combine pairs differing in exactly one bit.
5. Mark every term that was combined.
6. Repeat with the newly generated terms.
7. Terms that cannot be combined further are prime implicants.
8. Build a prime implicant chart.
9. Select essential prime implicants.
10. Cover any remaining minterms with a minimum-cost selection.

Don't-care terms can participate in combinations, but they do not have to be covered in the final function.

## 7.4 Worked example

Minimize:
\[
F(A,B,C)=\Sigma m(1,3,5,7)
\]

Binary list:

| Minterm | Binary |
|---:|---|
| 1 | 001 |
| 3 | 011 |
| 5 | 101 |
| 7 | 111 |

Group by number of 1s:
- One 1: `001`
- Two 1s: `011`, `101`
- Three 1s: `111`

First combinations:
- `001` and `011` → `0-1`
- `001` and `101` → `-01`
- `011` and `111` → `-11`
- `101` and `111` → `1-1`

Second combinations:
- `0-1` and `1-1` → `--1`
- `-01` and `-11` → `--1`

The pattern `--1` means `C=1`, so:
\[
\boxed{F=C}
\]

## 7.5 Prime implicant chart

Rows are prime implicants and columns are required minterms. Mark a cell when the implicant covers that minterm. A column with only one mark identifies an essential prime implicant.

If several covers remain, choose a cover with the required coverage and minimum cost. For larger charts, Petrick's method can systematically enumerate combinations, but the basic GATE-level skill is to construct and interpret the chart correctly.

## 7.6 K-map versus tabular method

| Feature | K-map | Quine–McCluskey |
|---|---|---|
| Method | Visual grouping | Table-based algorithm |
| Best suited | Small variable counts | More variables / systematic processing |
| Prime implicants | Seen as maximal groups | Found by repeated combination |
| Computer implementation | Less convenient | Algorithm-friendly |
| Human error | Gray-code/grouping errors | Binary comparison/chart errors |

---

# 8. Combinational circuit design

## 8.1 Definition

A combinational circuit is a digital circuit whose outputs depend only on the **current inputs**.

It has no memory of earlier inputs.

Examples:
- Adders and subtractors.
- Multiplexers and decoders.
- Comparators.
- Encoders.
- Code converters.

General model:
\[
Y=f(X)
\]
where `X` is the current input vector and `Y` is the output vector.

## 8.2 Design procedure

1. Understand the problem statement.
2. Identify input and output variables.
3. Assign symbols to inputs and outputs.
4. Construct the truth table.
5. Derive Boolean expressions for each output.
6. Minimize the expressions.
7. Implement with suitable gates or standard building blocks.
8. Verify every truth-table row.

## 8.3 Half adder

A half adder adds two one-bit inputs `A` and `B`.

Outputs:
- Sum `S`
- Carry `C`

| A | B | S | C |
|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

\[
S=A\oplus B
\]
\[
C=AB
\]

A half adder has no carry input.

## 8.4 Full adder

A full adder adds `A`, `B` and carry input `Cin`.

\[
S=A\oplus B\oplus C_{in}
\]
\[
C_{out}=AB+AC_{in}+BC_{in}
\]

Equivalent carry form:
\[
C_{out}=AB+C_{in}(A\oplus B)
\]

| A | B | Cin | S | Cout |
|---:|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 | 0 |
| 0 | 1 | 0 | 1 | 0 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 1 | 0 | 1 |
| 1 | 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 | 1 |

A full adder can be built from two half adders and one OR gate:
- First half adder adds `A,B`.
- Second half adder adds the first sum and `Cin`.
- OR the two carry outputs.

## 8.5 Half subtractor

Subtract `B` from `A`.

Outputs:
- Difference `D`
- Borrow `Bout`

| A | B | D | Bout |
|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 |

\[
D=A\oplus B
\]
\[
B_{out}=A'B
\]

## 8.6 Full subtractor

Inputs: `A`, `B`, borrow input `Bin`.

\[
D=A\oplus B\oplus B_{in}
\]
\[
B_{out}=A'B+A'B_{in}+BB_{in}
\]

## 8.7 Ripple-carry adder

An n-bit ripple-carry adder connects n full adders. Each stage's carry output feeds the next stage's carry input.

- Hardware is simple.
- Carry must propagate through stages.
- Delay increases approximately linearly with the number of bits in a simple ripple implementation.

## 8.8 Multiplexer (MUX)

A multiplexer selects one of several data inputs and forwards it to one output.

A `2^n : 1` MUX has:
- `2^n` data inputs.
- `n` select lines.
- One output.

### 2:1 MUX

Inputs `I0,I1`, select `S`:
\[
Y=S'I_0+SI_1
\]

| S | Output |
|---:|---|
| 0 | `I0` |
| 1 | `I1` |

### 4:1 MUX

With select lines `S1,S0`:
- `00` selects `I0`
- `01` selects `I1`
- `10` selects `I2`
- `11` selects `I3`

\[
Y=S_1'S_0'I_0+S_1'S_0I_1+S_1S_0'I_2+S_1S_0I_3
\]

**Implementing a Boolean function using a MUX:** Use some function variables as select lines and connect data inputs to 0, 1, a variable or its complement as required by the truth table.

## 8.9 Demultiplexer (DEMUX)

A demultiplexer routes one data input to one of several outputs based on select lines.

A `1:2^n` DEMUX has one data input, `n` select lines and `2^n` outputs.

A MUX is many-to-one; a DEMUX is one-to-many.

## 8.10 Decoder

A decoder converts an n-bit input code into up to `2^n` output lines. For an active-high 2-to-4 decoder:

| A | B | Y0 | Y1 | Y2 | Y3 |
|---:|---:|---:|---:|---:|---:|
| 0 | 0 | 1 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 | 0 | 0 |
| 1 | 0 | 0 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 | 0 | 1 |

Each output corresponds to a minterm:
\[
Y_0=A'B',\quad Y_1=A'B,\quad Y_2=AB',\quad Y_3=AB
\]

Enable inputs and active-low outputs are common in real ICs; always read the stated polarity.

## 8.11 Encoder and priority encoder

An encoder performs the reverse type of operation: it converts an asserted input line into a binary code.

A simple encoder assumes only one input is active at a time. If multiple inputs may be active, a **priority encoder** assigns priority and encodes the highest-priority active input.

## 8.12 Comparator

A comparator determines whether two binary numbers are equal, or which is larger.

For one bit:
\[
A=B \iff A\odot B
\]
\[
A>B \iff AB'
\]
\[
A<B \iff A'B
\]

For multi-bit numbers, compare from the most significant bit (MSB). The first unequal bit determines the result.

## 8.13 Parity generator and checker

Parity adds a bit to make the number of 1s either even or odd.

For data bits `A,B,C`:
- Even-parity bit: `P_even=A XOR B XOR C` when the parity bit is appended so the total number of 1s is even.
- Odd-parity bit: `P_odd=(A XOR B XOR C)'`.

An XOR of all received bits is:
- 0 for even parity.
- 1 for odd parity.

Parity can detect any odd number of bit errors, but it cannot detect every even number of bit errors and cannot identify the erroneous bit.

## 8.14 Code converters

A code converter maps one binary coding system to another, for example binary to Gray code or BCD to Excess-3.

### Binary to Gray code

For binary bits `B_(n-1)...B_0`, Gray bits are:
\[
G_{n-1}=B_{n-1}
\]
\[
G_i=B_{i+1}\oplus B_i
\]

Example: binary `1011`:
- `G3=1`
- `G2=1 XOR 0=1`
- `G1=0 XOR 1=1`
- `G0=1 XOR 1=0`

Gray code = `1110`.

### Gray to binary

\[
B_{n-1}=G_{n-1}
\]
\[
B_i=B_{i+1}\oplus G_i
\]

Example: Gray `1110`:
- `B3=1`
- `B2=1 XOR 1=0`
- `B1=0 XOR 1=1`
- `B0=1 XOR 0=1`

Binary = `1011`.

---

# 9. Sequential circuit design

## 9.1 Definition

A sequential circuit's output depends on current inputs **and stored past information**, called the state.

It contains memory elements such as latches or flip-flops.

General model:
\[
Q(t+1)=f(Q(t),X(t))
\]
\[
Y(t)=g(Q(t),X(t))
\]

`Q(t)` is the present state; `Q(t+1)` is the next state.

## 9.2 Combinational versus sequential circuits

| Feature | Combinational | Sequential |
|---|---|---|
| Output depends on | Current inputs | Current inputs and state |
| Memory | No | Yes |
| Feedback | Not required | Commonly present |
| Clock | Not required | Often used |
| Examples | Adder, MUX, decoder | Counter, register, FSM |

## 9.3 Latches and flip-flops

Both store one bit, but their triggering behavior differs.

- **Latch:** level-sensitive; responds while its enable or gate signal is at an active level.
- **Flip-flop:** edge-triggered; responds at a specified clock edge (rising or falling).

## 9.4 SR latch

An active-high NOR-based SR latch has inputs `S` (set) and `R` (reset).

| S | R | Next Q |
|---:|---:|---|
| 0 | 0 | Hold previous state |
| 0 | 1 | 0 (reset) |
| 1 | 0 | 1 (set) |
| 1 | 1 | Invalid / forbidden |

The invalid case is specific to this active-high NOR implementation. A NAND SR latch uses active-low inputs and has a different input table.

## 9.5 D latch

A gated D latch follows input `D` when enable `E=1`; when `E=0`, it holds its previous value.

| E | D | Next Q |
|---:|---:|---|
| 0 | X | Q (hold) |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

`X` means don't care.

## 9.6 Flip-flop types

### SR flip-flop

| S | R | Q(next) |
|---:|---:|---|
| 0 | 0 | Q |
| 0 | 1 | 0 |
| 1 | 0 | 1 |
| 1 | 1 | Invalid |

### JK flip-flop

| J | K | Q(next) |
|---:|---:|---|
| 0 | 0 | Q |
| 0 | 1 | 0 |
| 1 | 0 | 1 |
| 1 | 1 | Q' |

Characteristic equation:
\[
Q^+=JQ'+K'Q
\]

JK removes the invalid input condition of the SR flip-flop; `J=K=1` toggles the state.

### D flip-flop

| D | Q(next) |
|---:|---:|
| 0 | 0 |
| 1 | 1 |

Characteristic equation:
\[
Q^+=D
\]

The next state equals the D input at the active clock edge.

### T flip-flop

| T | Q(next) |
|---:|---:|
| 0 | Q |
| 1 | Q' |

Characteristic equation:
\[
Q^+=T\oplus Q
\]

## 9.7 Characteristic table and excitation table

A **characteristic table** tells the next state for given inputs and present state.

An **excitation table** tells which inputs are required to move from a given present state to a desired next state.

### Excitation table

| Q | Q+ | SR (S,R) | JK (J,K) | D | T |
|---:|---:|---|---|---:|---:|
| 0 | 0 | 0,X | 0,X | 0 | 0 |
| 0 | 1 | 1,0 | 1,X | 1 | 1 |
| 1 | 0 | 0,1 | X,1 | 0 | 1 |
| 1 | 1 | X,0 | X,0 | 1 | 0 |

`X` denotes an input that can be either 0 or 1 for that transition. The SR input `S=R=1` must be avoided.

## 9.8 Registers

A register is a group of flip-flops used to store multiple bits.

An n-bit register stores n bits. Common register types:
- Parallel-in/parallel-out (PIPO).
- Serial-in/serial-out (SISO).
- Serial-in/parallel-out (SIPO).
- Parallel-in/serial-out (PISO).

A shift register moves stored bits left or right on clock events.

## 9.9 Counters

A counter is a sequential circuit that moves through a prescribed sequence of states.

- **Asynchronous (ripple) counter:** a flip-flop's output clocks a later flip-flop. Clock transitions ripple through the chain.
- **Synchronous counter:** all flip-flops receive the same clock; next-state logic determines which bits toggle.

An n-bit binary counter has `2^n` states, from 0 to `2^n-1`, before repeating.

For a modulo-M counter, the sequence contains M distinct states. The number of flip-flops required is at least:
\[
n=\lceil\log_2 M\rceil
\]

A counter with unused states needs defined or safely handled behavior if recovery is required.

## 9.10 Finite-state machines (FSM)

An FSM is a sequential model with:
- A finite set of states.
- Inputs.
- Outputs.
- A next-state function.
- An output function.

### Moore machine

Output depends only on the current state:
\[
Y=g(Q)
\]

### Mealy machine

Output depends on current state and current input:
\[
Y=g(Q,X)
\]

| Feature | Moore | Mealy |
|---|---|---|
| Output depends on | State | State and input |
| Output changes | Typically after state changes | Can respond to input changes within a state |
| State count | Often more | Often fewer |
| Output timing | Usually more stable relative to clock | May respond faster but can be input-sensitive |

## 9.11 Sequential circuit design procedure

1. Understand the required behavior.
2. Identify inputs and outputs.
3. Draw a state diagram.
4. Create a state table.
5. Assign binary codes to states.
6. Choose a flip-flop type.
7. Use the excitation table to derive flip-flop inputs.
8. Minimize the input and output Boolean expressions.
9. Draw the circuit.
10. Verify the state transitions, including reset and unused states.

## 9.12 Timing concepts

- **Clock period:** time between successive active clock edges.
- **Frequency:** reciprocal of clock period, `f=1/T`.
- **Setup time:** minimum time data must be stable before the active clock edge.
- **Hold time:** minimum time data must remain stable after the active clock edge.
- **Propagation delay:** time taken for a change at an input or clock to affect an output.

A synchronous design must satisfy setup and hold constraints. A common simplified setup constraint is:
\[
T_{clk}\ge t_{clk\to Q}+t_{comb}+t_{setup}
\]
Clock skew and other implementation effects may also matter.

---

# 10. Number representation

## 10.1 Positional number systems

A base-r number uses digits from 0 to `r-1`.

For example:
- Binary: base 2, digits 0 and 1.
- Octal: base 8, digits 0 to 7.
- Decimal: base 10.
- Hexadecimal: base 16, digits 0 to 9 and A to F.

For a number:
\[
(a_n a_{n-1}\ldots a_0.a_{-1}a_{-2})_r
\]
its value is:
\[
\sum_i a_i r^i
\]

## 10.2 Base conversion

### Binary to decimal

\[
(101101)_2=1(2^5)+0(2^4)+1(2^3)+1(2^2)+0(2^1)+1(2^0)
\]
\[
=32+8+4+1=\boxed{45}
\]

### Decimal integer to binary

Repeatedly divide by 2 and read remainders from bottom to top.

Example: 13
- 13 / 2 → remainder 1
- 6 / 2 → remainder 0
- 3 / 2 → remainder 1
- 1 / 2 → remainder 1

So:
\[
(13)_{10}=(1101)_2
\]

### Binary to octal and hexadecimal

- Group binary digits in sets of 3 for octal.
- Group binary digits in sets of 4 for hexadecimal.
- For integer parts, group from the radix point towards the left.
- For fractional parts, group from the radix point towards the right.
- Add leading or trailing zeros as needed.

Example:
\[
(11010110)_2=(D6)_{16}
\]
because `1101=D` and `0110=6`.

## 10.3 Signed number representation

An n-bit signed representation can encode positive and negative values in different ways.

### Sign-magnitude

- Most significant bit is sign: 0 positive, 1 negative.
- Remaining bits represent magnitude.
- Has positive zero and negative zero.
- Range:
\[
-(2^{n-1}-1)\ \text{to}\ +(2^{n-1}-1)
\]

### One's complement

A negative number is formed by complementing every bit of the positive number.
- Has two representations of zero.
- Range is the same as sign-magnitude.

### Two's complement

A negative number is formed by:
1. Inverting all bits.
2. Adding 1.

For n bits, range:
\[
-2^{n-1}\ \text{to}\ 2^{n-1}-1
\]

It has only one zero and is the common signed integer representation in modern processors.

## 10.4 Two's-complement examples

Represent `-5` in 8 bits.

Positive 5:
`00000101`

Invert:
`11111010`

Add 1:
`11111011`

Therefore, `-5` is:
\[
\boxed{11111011}
\]

### Interpreting a two's-complement number

If MSB is 0, the number is nonnegative and can be read as ordinary binary.

If MSB is 1, find its magnitude by inverting and adding 1, then attach a minus sign.

Example: `11110110`
- Invert: `00001001`
- Add 1: `00001010` = 10
- Value = `-10`.

Alternative weighted interpretation for n bits:
\[
V=-b_{n-1}2^{n-1}+\sum_{i=0}^{n-2}b_i2^i
\]

## 10.5 Sign extension

To increase the width of a two's-complement number, copy the sign bit into the new higher-order positions.

Example:
`11110110` (8-bit -10) → `11111111 11110110` (16-bit -10).

Do not append zeros to the left of a negative two's-complement value.

## 10.6 Overflow

For signed two's-complement addition, overflow occurs when:
- Two positive numbers produce a negative result, or
- Two negative numbers produce a nonnegative result.

Equivalently, when adding two numbers with the same sign, if the result has a different sign, overflow occurred.

Carry-out alone does **not** determine signed overflow.

For unsigned addition, a carry-out beyond the most significant bit indicates overflow.

### Example: 4-bit signed overflow

Maximum 4-bit signed value is `+7`; minimum is `-8`.

\[
0111+0001=1000
\]

The mathematical result is +8, which is outside the 4-bit signed range. The stored result `1000` represents -8, so overflow occurred.

---

# 11. Fixed-point arithmetic

## 11.1 What is fixed-point representation?

In fixed-point representation, the radix point is assumed to be at a fixed position. The stored bits represent an integer scaled by a constant power of two.

If there are `f` fractional bits:
\[
\text{Value}=\text{stored signed integer}\times 2^{-f}
\]

For example, with 4 fractional bits, stored integer 24 represents:
\[
24/16=1.5
\]

Fixed-point is useful when hardware cost, predictable precision or deterministic arithmetic is important.

## 11.2 Q-format

A common notation is `Qm.n`, but conventions differ on whether the sign bit is counted in `m`. Always check the convention stated in a question.

Under a convention where there are `m` integer bits including sign and `n` fractional bits:
- Total width = `m+n`.
- Fractional resolution = `2^-n`.
- Two's-complement range:
\[
-2^{m-1}\ \text{to}\ 2^{m-1}-2^{-n}
\]

## 11.3 Fixed-point addition and subtraction

If two values have the same number of fractional bits, add or subtract their stored integers directly. The binary point remains in the same position.

Example with 4 fractional bits:
- `1.25` is represented as `0001.0100`.
- `0.50` is represented as `0000.1000`.

Addition:
\[
0001.0100+0000.1000=0001.1100=1.75
\]

If the scales differ, align them before arithmetic.

## 11.4 Fixed-point multiplication

If A has `f_A` fractional bits and B has `f_B` fractional bits, their full product has:
\[
f_{product}=f_A+f_B
\]
fractional bits.

Example:
- `1.5` in a format with 2 fractional bits is stored as integer 6 (`01.10`).
- `2.0` is stored as integer 8 (`10.00`).
- Integer product = 48.
- Product has 4 fractional bits, so value = `48/16=3.0`.

To return to the original scale, shift or round appropriately. Truncation may lose precision.

## 11.5 Fixed-point division

Division requires scale management. If stored integers are `A_int` and `B_int`, and the desired output has `f_out` fractional bits, a typical scaled integer calculation is:
\[
Q_{int}=\frac{A_{int}\,2^{f_{out}+f_B-f_A}}{B_{int}}
\]
provided the exponent shift is implemented safely and the denominator is nonzero.

The exact scaling depends on the input and output formats.

## 11.6 Quantization, truncation and rounding

- **Quantization:** mapping a real value to one of the representable fixed-point values.
- **Truncation:** discard lower-order bits.
- **Rounding:** choose the nearest representable value according to a specified rule.

Truncation is simple but can introduce systematic error. Rounding usually reduces average error but requires extra logic.

---

# 12. Floating-point representation and arithmetic

## 12.1 Why floating point?

Fixed-point has a fixed radix-point position. Floating-point uses a significand and an exponent, allowing the radix point to move.

A normalized binary floating-point number is represented conceptually as:
\[
(-1)^s\times 1.f\times 2^e
\]
for a normal binary value, where:
- `s` is the sign bit.
- `f` is the fractional part of the significand.
- `e` is the unbiased exponent.

Floating-point supports a very wide range of magnitudes, with finite precision.

## 12.2 General fields

A floating-point format commonly contains:
1. Sign field.
2. Exponent field.
3. Fraction (mantissa field).

The term **significand** is more precise for the full precision-bearing value. The fraction field stores only part of it in normalized binary formats because the leading 1 is implicit for normal numbers.

## 12.3 IEEE 754 binary formats

| Format | Total bits | Sign | Exponent | Fraction |
|---|---:|---:|---:|---:|
| Binary32 (single precision) | 32 | 1 | 8 | 23 |
| Binary64 (double precision) | 64 | 1 | 11 | 52 |

Exponent bias:
\[
Bias=2^{k-1}-1
\]
where `k` is the number of exponent bits.

- Binary32 bias = 127.
- Binary64 bias = 1023.

For a normal number:
\[
E=e_{stored}-Bias
\]
\[
Value=(-1)^s\times(1.f)\times2^E
\]

## 12.4 Normalized numbers

A nonzero binary number is normalized by moving the binary point so that exactly one nonzero digit (1) appears before the point.

Example:
\[
101.101_2=1.01101_2\times2^2
\]

The exponent is 2 and the normalized significand is `1.01101`.

## 12.5 Special IEEE 754 values

For binary32:
- Exponent all zeros, fraction zero: signed zero.
- Exponent all zeros, fraction nonzero: subnormal number.
- Exponent neither all zeros nor all ones: normal finite number.
- Exponent all ones, fraction zero: positive or negative infinity.
- Exponent all ones, fraction nonzero: NaN (Not a Number).

For binary64, the same classification applies with its own field widths.

### Subnormal numbers

Subnormal numbers use no implicit leading 1. Their significand is `0.f`, and the exponent uses the minimum normal exponent. They provide gradual underflow near zero.

## 12.6 Worked IEEE 754 binary32 example: 5.75

Convert 5.75 to binary:
- 5 = `101`
- 0.75 = `.11`
- Therefore `5.75 = 101.11₂`

Normalize:
\[
101.11_2=1.0111_2\times2^2
\]

Fields:
- Sign = `0`
- Actual exponent = 2
- Biased exponent = `2+127=129`
- 129 in binary = `10000001`
- Fraction = `01110000000000000000000`

Binary32 representation:
`0 10000001 01110000000000000000000`

Hexadecimal representation:
`0x40B80000`

## 12.7 Floating-point addition and subtraction

Steps:
1. Compare exponents.
2. Shift the significand of the number with the smaller exponent right until exponents match.
3. Add or subtract significands, considering signs.
4. Normalize the result.
5. Round to the available precision.
6. Check for overflow or underflow.

### Example (conceptual)

\[
1.01_2\times2^3+1.10_2\times2^1
\]

Align exponents:
\[
1.01\times2^3+0.0110\times2^3
\]
Add significands:
\[
(1.0100+0.0110)\times2^3=1.1010\times2^3
\]

Result:
\[
1.101_2\times2^3
\]

The smaller operand loses some low-order precision during alignment in finite formats.

## 12.8 Floating-point multiplication

Steps:
1. Result sign = XOR of operand signs.
2. Add unbiased exponents.
3. Multiply significands.
4. Normalize.
5. Round.
6. Check overflow and underflow.

For normalized operands:
\[
(s_1,e_1,m_1)\times(s_2,e_2,m_2)
\]
has sign `s1 XOR s2`, exponent `e1+e2`, and significand `m1×m2`, followed by normalization and rounding.

With stored biased exponents, care is required to subtract one bias when adding the stored exponents.

## 12.9 Floating-point division

Steps:
1. Result sign = XOR of signs.
2. Subtract exponents.
3. Divide significands.
4. Normalize.
5. Round.
6. Check special cases and range.

## 12.10 Rounding modes and error

IEEE 754 defines rounding behavior. Common modes include:
- Round to nearest, ties to even.
- Round toward zero.
- Round toward positive infinity.
- Round toward negative infinity.

**Round to nearest, ties to even** chooses the nearest representable value; if exactly halfway, it chooses the result whose least significant retained bit is even.

Floating-point arithmetic is not exact real arithmetic. Many decimal fractions, such as 0.1, have repeating binary expansions and must be approximated.

## 12.11 Floating-point limitations

- Finite precision causes rounding error.
- Adding numbers with very different magnitudes may lose the smaller contribution.
- Overflow produces infinity under IEEE 754 arithmetic in common cases.
- Underflow can produce subnormal values or zero.
- NaN comparisons have special behavior; NaN is not equal to itself.

---

# 13. GATE examination strategy, traps and revision sheet

## 13.1 Important problem patterns

1. Simplify a Boolean expression using identities.
2. Convert between truth table, minterm and maxterm notation.
3. Find minimal SOP or POS using a K-map.
4. Use don't-care conditions to form larger groups.
5. Identify prime and essential prime implicants.
6. Perform Quine–McCluskey combination stages.
7. Design a circuit from a word description or truth table.
8. Derive sum and carry equations.
9. Determine MUX/decoder output for a given input.
10. Derive next-state equations for flip-flops.
11. Determine counter modulus and number of flip-flops.
12. Convert signed binary values and detect overflow.
13. Decode IEEE 754 fields and perform floating-point arithmetic steps.

## 13.2 High-value formulas

### Boolean algebra
\[
A+A'B=A+B
\]
\[
A(A'+B)=AB
\]
\[
AB+AB'=A
\]
\[
(A+B)(A+B')=A
\]
\[
(A+B)'=A'B'
\]
\[
(AB)'=A'+B'
\]

### Adders and subtractors
\[
S_{HA}=A\oplus B,\quad C_{HA}=AB
\]
\[
S_{FA}=A\oplus B\oplus C_{in}
\]
\[
C_{out}=AB+AC_{in}+BC_{in}
\]
\[
D_{HS}=A\oplus B,\quad B_{out}=A'B
\]
\[
D_{FS}=A\oplus B\oplus B_{in}
\]

### Flip-flops
\[
Q^+_D=D
\]
\[
Q^+_T=T\oplus Q
\]
\[
Q^+_{JK}=JQ'+K'Q
\]

### Number representation
\[
\text{Two's complement range}=-2^{n-1}\text{ to }2^{n-1}-1
\]
\[
\text{Unsigned n-bit range}=0\text{ to }2^n-1
\]
\[
n_{counter}=\lceil\log_2 M\rceil
\]

### Floating point
\[
Bias=2^{k-1}-1
\]
\[
Value=(-1)^s(1.f)2^{e_{stored}-Bias}
\]
for normal numbers.

## 13.3 Frequent traps

- Minterm index depends on the variable order.
- Maxterm construction uses the opposite literal polarity rule from minterms.
- K-map ordering is Gray code.
- K-map edges wrap around; diagonals do not.
- Don't-care cells are optional.
- A prime implicant is not necessarily essential.
- Carry-out and signed overflow are different.
- Two's complement has one zero; sign-magnitude and one's complement have two.
- A JK flip-flop toggles when `J=K=1`.
- A D flip-flop copies D at the active clock edge.
- Moore outputs depend only on state; Mealy outputs depend on state and input.
- IEEE 754 normal numbers have an implicit leading 1; subnormal numbers do not.
- The exponent field is biased, not stored as an ordinary signed integer.
- Floating-point addition requires exponent alignment before significand addition.

## 13.4 Quick revision checklist

Before the exam, make sure you can:
- [ ] Write truth tables for all basic gates.
- [ ] Apply De Morgan's laws without error.
- [ ] Convert `Σm` and `ΠM` notation.
- [ ] Minimize a 4-variable function with wrap-around groups.
- [ ] Use don't-cares correctly.
- [ ] Complete a Quine–McCluskey table.
- [ ] Derive half-adder and full-adder outputs.
- [ ] Explain MUX, DEMUX, decoder and encoder.
- [ ] Fill characteristic and excitation tables.
- [ ] Analyze a simple counter or FSM.
- [ ] Convert negative values to and from two's complement.
- [ ] Identify signed and unsigned overflow.
- [ ] Decode a normal IEEE 754 number.
- [ ] Explain floating-point alignment and rounding.

---

# 14. Practice questions

**Try these before reading the answer key.** Unless specified, use conventional positive logic and the variable order shown.

## A. Conceptual questions

**Q1.** Why are NAND and NOR called universal gates?

**Q2.** State the two De Morgan's theorems.

**Q3.** What is the difference between a minterm and a maxterm?

**Q4.** Why does a K-map use Gray-code ordering?

**Q5.** Distinguish between a latch and a flip-flop.

**Q6.** What is the difference between a Moore and a Mealy machine?

**Q7.** Why does carry-out alone not determine signed two's-complement overflow?

**Q8.** What is the purpose of a biased exponent in floating-point representation?

## B. MCQs

**Q9.** Simplify `A + A'B`.

A. `AB`  
B. `A+B`  
C. `A'B`  
D. `A' + B`

**Q10.** The number of minterms for a Boolean function of 5 variables is:

A. 5  
B. 10  
C. 16  
D. 32

**Q11.** Which flip-flop toggles when both its inputs are 1?

A. SR  
B. D  
C. JK  
D. None

**Q12.** A 4:1 MUX requires how many select lines?

A. 1  
B. 2  
C. 3  
D. 4

**Q13.** The range of an n-bit two's-complement integer is:

A. `-(2^n-1)` to `2^n-1`  
B. `-2^(n-1)` to `2^(n-1)-1`  
C. `0` to `2^n-1`  
D. `-(2^(n-1)-1)` to `+(2^(n-1)-1)`

**Q14.** In binary32 IEEE 754, the exponent bias is:

A.  complementation of 127  
B. 127  
C. 128  
D. 1023

**Q15.** Which statement about K-map adjacency is correct?

A. Diagonal cells are adjacent.  
B. Only cells in the same row are adjacent.  
C. Opposite edges are adjacent.  
D. Only cells in the same column are adjacent.

## C. MSQs

**Q16.** Select all universal gates.

A. AND  
B. NAND  
C. NOR  
D. XOR

**Q17.** Which statements about two's complement are true?

A. It has only one zero.  
B. The MSB has negative weight.  
C. It has symmetric positive and negative range.  
D. Sign extension replicates the sign bit.

**Q18.** Select the true statements about a D flip-flop.

A. Its next state equals D at the active clock edge.  
B. It is edge-triggered in the standard flip-flop model.  
C. It toggles whenever D is 1.  
D. It can be used in a register.

## D. Numerical Answer Type (NAT)

**Q19.** Convert `(101101)₂` to decimal.

**Q20.** What is the 8-bit two's-complement representation of `-13`? Give the 8-bit binary answer.

**Q21.** How many flip-flops are minimally required to construct a modulo-10 counter?

**Q22.** For binary32, what is the biased exponent field (decimal) for a normal number whose unbiased exponent is 5?

## E. Boolean minimization and circuit problems

**Q23.** Simplify algebraically:
\[
F=AB+AB'+A'C
\]

**Q24.** Minimize using a K-map:
\[
F(A,B,C)=\Sigma m(0,2,4,6)
\]

**Q25.** Minimize:
\[
F(A,B,C)=\Sigma m(1,3,5,7)
\]
State the simplest expression.

**Q26.** A full adder has inputs `A=1`, `B=1`, `Cin=1`. Find `S` and `Cout`.

**Q27.** A 2:1 MUX has `I0=0`, `I1=1`, and `S=1`. Find its output.

**Q28.** A JK flip-flop has `J=K=1` and present state `Q=0`. Find the next state.

**Q29.** A 4-bit two's-complement circuit computes `0110 + 0011`. Find the 4-bit result and state whether signed overflow occurs.

**Q30.** Normalize `1101.01₂` into the form `1.xxxxx × 2^e`.

**Q31.** Decode the binary32 number:
`0 10000001 01110000000000000000000`
Give its decimal value.

**Q32.** A combinational function is 1 for minterms 0, 1, 2 and 3 of variables `A,B,C`. Minimize it.

---

# 15. Detailed answer key

## A. Conceptual answers

**A1.** NAND and NOR are universal because NOT, AND and OR can each be constructed using only NAND gates or only NOR gates. Since any Boolean function can be expressed using AND, OR and NOT, either gate type can implement any Boolean function.

**A2.**
\[
(A+B)'=A'B',\quad (AB)'=A'+B'
\]

**A3.** A minterm is an AND term containing all variables and is 1 for exactly one input row. A maxterm is an OR term containing all variables and is 0 for exactly one input row.

**A4.** Gray-code ordering ensures adjacent cells differ in exactly one variable. This allows adjacent minterms to combine by eliminating that variable.

**A5.** A latch is level-sensitive and responds while enable is active. A flip-flop is edge-triggered and samples at a specified clock edge.

**A6.** A Moore output depends only on the current state. A Mealy output depends on the current state and current input.

**A7.** In signed addition, overflow is about the representable signed range. It occurs when equal-sign operands produce a result with the opposite sign. Carry-out can occur without signed overflow, and signed overflow can occur without a carry-out.

**A8.** A bias lets the exponent be stored as an unsigned bit pattern while representing both negative and positive exponents. For k exponent bits, the usual bias is `2^(k-1)-1`.

## B. MCQ answers

**A9. B — `A+B`.**
\[
A+A'B=(A+A')(A+B)=1(A+B)=A+B
\]

**A10. D — 32.** There are `2^5=32` possible input combinations and hence 32 minterms.

**A11. C — JK.** `J=K=1` causes toggling.

**A12. B — 2.** A 4:1 MUX needs `log2(4)=2` select lines.

**A13. B.** The n-bit two's-complement range is `-2^(n-1)` through `2^(n-1)-1`.

**A14. B — 127.** Binary32 has 8 exponent bits, so bias is `2^7-1=127`.

**A15. C.** K-map edges wrap around, so opposite edges are adjacent.

## C. MSQ answers

**A16. B and C.** NAND and NOR are universal gates.

**A17. A, B and D.**
- A: true — there is one zero.
- B: true — the MSB has weight `-2^(n-1)`.
- C: false — the negative range has one extra value.
- D: true — sign extension repeats the sign bit.

**A18. A, B and D.**
A D flip-flop copies D at the active edge, is edge-triggered, and is commonly used in registers. It does not toggle merely because D is 1.

## D. NAT solutions

**A19.**
\[
(101101)_2=32+8+4+1=\boxed{45}
\]

**A20.** Positive 13 in 8 bits:
`00001101`

Invert:
`11110010`

Add 1:
`11110011`

Answer: **11110011**.

**A21.**
\[
n=\lceil\log_2 10\rceil=\lceil3.322...\rceil=\boxed{4}
\]

**A22.**
\[
E_{stored}=E_{actual}+Bias=5+127=\boxed{132}
\]

## E. Worked solutions

**A23.**
\[
F=AB+AB'+A'C
\]
Take A common in the first two terms:
\[
F=A(B+B')+A'C=A+A'C
\]
Use `X+X'Y=X+Y`:
\[
\boxed{F=A+C}
\]

**A24.**
\[
F=\Sigma m(0,2,4,6)
\]
Binary minterms:
- 0 = 000
- 2 = 010
- 4 = 100
- 6 = 110

All have `C=0`; A and B vary. They form a group of four:
\[
\boxed{F=C'}
\]

**A25.**
Minterms 1, 3, 5 and 7 are:
`001, 011, 101, 111`.

All have `C=1`, so:
\[
\boxed{F=C}
\]

**A26.**
\[
S=1\oplus1\oplus1=1
\]
\[
Cout=AB+ACin+BCin=1+1+1=1
\]
Answer: **S=1, Cout=1**.

**A27.** `S=1` selects `I1`. Since `I1=1`, output is **1**.

**A28.** A JK flip-flop toggles when `J=K=1`. Present state is 0, so next state is **1**.

**A29.**
\[
0110(+6)+0011(+3)=1001
\]
The 4-bit signed range is -8 to +7. The mathematical result +9 is outside the range. The bit result `1001` represents -7, so **signed overflow occurs**.

**A30.**
\[
1101.01_2=1.10101_2\times2^3
\]
Answer: **`1.10101₂ × 2³`**.

**A31.**
- Sign = 0, so positive.
- Stored exponent = `10000001₂ = 129`.
- Bias = 127.
- Unbiased exponent = `129-127=2`.
- Fraction = `.0111` followed by zeros.
- Significand = `1.0111₂`.

\[
1.0111_2=1+0.25+0.125+0.0625=1.4375
\]
\[
Value=1.4375\times2^2=\boxed{5.75}
\]

**A32.**
Minterms 0, 1, 2, 3 are `000,001,010,011`. In all four rows `A=0`, while B and C vary. Therefore:
\[
\boxed{F=A'}
\]

---

## Final self-assessment

You are ready to move to mixed GATE-level Digital Logic questions when you can do all of the following without relying on the answer key:

1. Minimize Boolean functions in algebraic, K-map and tabular forms.
2. Explain why each selected implicant is needed.
3. Derive and verify combinational circuit equations.
4. Use characteristic and excitation tables to design simple sequential circuits.
5. Solve signed binary arithmetic and overflow problems.
6. Decode IEEE 754 normal values and explain the steps in floating-point arithmetic.

**Study recommendation:** First master Sections 2–7, then Sections 8–9, and finally Sections 10–12. Solve the practice questions after each major section rather than waiting until the end.
