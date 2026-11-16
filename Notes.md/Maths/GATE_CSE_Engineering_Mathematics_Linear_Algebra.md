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
