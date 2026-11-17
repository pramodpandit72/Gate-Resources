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
