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
