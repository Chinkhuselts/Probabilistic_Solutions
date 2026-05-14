# Task 8 — Beta Distribution

---

## Background & Key Concepts

The **Beta distribution** is a continuous probability distribution defined on the interval $[0, 1]$. This makes it the natural choice for modeling **proportions, probabilities, and rates** — quantities that are always between 0 and 1.

Unlike the discrete distributions studied earlier, $X$ can take **any real value** in $[0,1]$, not just isolated points. Probability is no longer assigned to individual points (every single point has probability zero) but to **intervals** — computed as areas under the probability density function (PDF).

The Beta distribution is also remarkably flexible: by tuning two parameters, it can produce a wide variety of shapes — uniform, bell-shaped, skewed left, skewed right, U-shaped, or concentrated near the endpoints.

---

## Task 0 — The Experiment

**Experiment:** Spin a perfectly uniform wheel of fortune and record where the pointer lands. The pointer can stop at any position from 0% to 100% of the wheel.

**Sample space:** $\Omega = [0, 1]$ — the interval of all possible proportions.

**Elementary outcome:** $\omega \in [0, 1]$ — a single real number representing the position.

**Random variable:** $X(\omega) = \omega$ — the position itself.

**Support:** $[0, 1]$ — all real numbers between 0 and 1 inclusive.

> In a continuous experiment, we cannot list individual outcomes — there are uncountably many. Instead, we specify probabilities of intervals via the density function.

---

## Task 1 — PDF and Parameters

$$\boxed{f(x; \alpha, \beta) = \frac{x^{\alpha-1}(1-x)^{\beta-1}}{B(\alpha, \beta)}, \quad x \in [0,1]}$$

where $B(\alpha, \beta)$ is the **Beta function** — a normalizing constant ensuring the total area equals 1:

$$B(\alpha, \beta) = \int_0^1 t^{\alpha-1}(1-t)^{\beta-1}\, dt = \frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha + \beta)}$$

For positive integers: $\Gamma(n) = (n-1)!$, so $B(a,b) = \frac{(a-1)!(b-1)!}{(a+b-1)!}$.

**Parameters:** $\alpha > 0$ and $\beta > 0$ (both strictly positive).

**Notation:** $X \sim \text{Beta}(\alpha, \beta)$.

**Mean and Variance:**
$$E[X] = \frac{\alpha}{\alpha + \beta}, \qquad \text{Var}(X) = \frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}$$

**Intuition for the mean:** It is the proportion of $\alpha$ in the total $\alpha + \beta$. Balanced at 0.5 when $\alpha = \beta$.

---

## Task 2 — Support

The support is the closed interval $[0, 1]$.

- $f(x) = 0$ for $x < 0$ or $x > 1$.
- At the endpoints: $f(0)$ is 0 if $\alpha > 1$, and $+\infty$ if $\alpha < 1$. Similarly for $f(1)$ and $\beta$.
- Every individual point has probability zero: $P(X = x) = 0$ for all $x$.
- Probabilities are computed over intervals: $P(a \le X \le b) = \int_a^b f(x)\, dx$.

---

## Task 3 — PDF Shapes for Several Parameter Choices

### Case 1: Symmetric ($\alpha = \beta$)

**$\text{Beta}(1, 1)$ — Uniform:**
```
f(x)
1.0 |────────────────────────────────
    |
    +-----+-----+-----+-----+-----> x
    0    0.25  0.5   0.75   1
    (completely flat — all values equally likely)
```

**$\text{Beta}(2, 2)$ — Bell-shaped, symmetric:**
```
f(x)
1.5 |          ╱▔▔▔▔╲
1.0 |        ╱         ╲
0.5 |      ╱             ╲
0.0 |────╱─────────────────╲──
    +-----+-----+-----+-----+-> x
    0    0.25  0.5   0.75   1
    (peak at x = 0.5)
```

**$\text{Beta}(5, 5)$ — Narrow bell, more concentrated:**
```
f(x)
3.0 |          ╱▔▔▔╲
2.0 |        ╱       ╲
1.0 |      ╱           ╲
0.0 |────╱───────────────╲──
    (even sharper peak at 0.5)
```

### Case 2: Skewed Right ($\alpha < \beta$)

**$\text{Beta}(1, 3)$** — most mass near $x = 0$:
```
f(x)
3.0 |╲
2.0 |  ╲
1.0 |    ╲___
0.0 |─────────╲─────
    (peak at x = 0, decreasing)
    Mean = 1/(1+3) = 0.25
```

**$\text{Beta}(2, 5)$** — peak before center:
```
f(x)
    |    ╱▔╲
    |   ╱    ╲
    |  ╱       ╲____
    +--+--+--+--+---> x
    0       0.5      1
    Mean = 2/7 ≈ 0.29
```

### Case 3: Skewed Left ($\alpha > \beta$)

**$\text{Beta}(5, 2)$** — mirror image of above:
```
f(x)
    |        ╱▔╲
    |      ╱     ╲
    |___╱          ╲
    +--+--+--+--+---> x
    0       0.5      1
    Mean = 5/7 ≈ 0.71
```

### Case 4: Concentrated Near Endpoints ($\alpha < 1$ and $\beta < 1$)

**$\text{Beta}(0.5, 0.5)$** — U-shaped (bimodal):
```
f(x)
   ↑                ↑
   ↑    ╲        ╱  ↑
   |      ╲    ╱
   |        ╲╱
   +--+--+--+--+---> x
   0       0.5      1
   (mass concentrates near 0 and 1)
```

**Interpretation:** Values near the extremes (0% or 100%) are more likely than values in the middle. Models bimodal behavior.

---

## Task 4 — CDF Graphs

The CDF of the Beta distribution is the **Incomplete Beta function**:

$$F(x; \alpha, \beta) = I_x(\alpha, \beta) = \frac{1}{B(\alpha, \beta)} \int_0^x t^{\alpha-1}(1-t)^{\beta-1}\, dt$$

There is no simple closed form in general — it is computed numerically.

**Key values:**

| Distribution | $F(0.25)$ | $F(0.5)$ | $F(0.75)$ |
|-------------|-----------|----------|-----------|
| Beta(1,1) | 0.250 | 0.500 | 0.750 |
| Beta(2,2) | 0.156 | 0.500 | 0.844 |
| Beta(5,5) | 0.046 | 0.500 | 0.954 |
| Beta(1,3) | 0.578 | 0.875 | 0.984 |
| Beta(5,2) | 0.016 | 0.125 | 0.422 |

**Observation:** For symmetric distributions ($\alpha = \beta$), $F(0.5) = 0.5$ always — the median is exactly 0.5.

```
F(x)
1.0 |                      Beta(5,2)──────
    |               Beta(2,2) ──
0.5 |         Beta(1,1)─/──/
    |   Beta(1,3)/──/
    |─/
0.0 +-----+-----+-----+-----+---------> x
    0    0.25  0.5   0.75   1
```

---

## Task 5 — How Parameters Influence Shape and CDF

| $\alpha$ vs $\beta$ | Mean | Shape of PDF | CDF growth |
|--------------------|------|-------------|------------|
| $\alpha = \beta = 1$ | 0.5 | Flat (Uniform) | Linear |
| $\alpha = \beta > 1$ | 0.5 | Symmetric bell | S-curve centered at 0.5 |
| $\alpha = \beta < 1$ | 0.5 | U-shaped | S-curve, slower in middle |
| $\alpha > \beta$ | $> 0.5$ | Left-skewed | Slowly at start, steeply near 1 |
| $\alpha < \beta$ | $< 0.5$ | Right-skewed | Steeply at start, slowly near 1 |

**As both parameters increase together** (keeping $\alpha/\beta$ constant), the distribution **concentrates** around its mean — variance shrinks, peak gets taller and narrower.

---

## Task 6 — Computing Probabilities

For the Beta distribution, probabilities are areas under the PDF and are found using the CDF (Incomplete Beta function):

$$P(X \le a) = F(a; \alpha, \beta)$$
$$P(X \ge a) = 1 - F(a; \alpha, \beta)$$
$$P(a \le X \le b) = F(b; \alpha, \beta) - F(a; \alpha, \beta)$$

**Example:** $X \sim \text{Beta}(2, 5)$

$$E[X] = \frac{2}{7} \approx 0.286, \qquad \text{Var}(X) = \frac{10}{392} \approx 0.026$$

$P(X \le 0.3)$: Computed numerically $\approx 0.580$

$P(0.2 \le X \le 0.5)$: $= F(0.5) - F(0.2) \approx 0.891 - 0.345 = 0.546$

$P(X \ge 0.5)$: $= 1 - F(0.5) \approx 1 - 0.891 = 0.109$

**In practice:** Use a statistics table, software function (e.g., `pbeta(x, alpha, beta)` in R, `scipy.stats.beta.cdf(x, a, b)` in Python), or a CAS.

---

## Task 7 — Why Probabilities Are Areas

For a continuous distribution, $P(X = x) = 0$ for every single point. This seems paradoxical, but it is correct: with uncountably many possible values in $[0,1]$, any finite probability assigned to each point would make the total infinite.

Instead, probability is a **measure of sets** (intervals):
$$P(a \le X \le b) = \int_a^b f(x)\, dx = \text{area under } f \text{ between } a \text{ and } b$$

The PDF $f(x)$ is not a probability itself — it is a **density**. It can exceed 1. What matters is the integral:
$$\int_0^1 f(x)\, dx = 1 \quad \text{(total area = 1)}$$

**Consequence:** For continuous distributions, $P(a \le X \le b) = P(a < X < b)$ — open and closed endpoints make no difference.

---

## Task 8 — Practical Applications

| Application | Role of $X \in [0,1]$ |
|-------------|----------------------|
| **Bayesian statistics** | $X$ = unknown probability of success; Beta is the conjugate prior for the Binomial likelihood |
| **Project management** | $X$ = proportion of project completed; Beta(PERT) used in PERT networks |
| **Machine learning** | $X$ = probability parameter in models; Beta prior placed on $p$ |
| **A/B testing** | $X$ = click-through rate or conversion rate |
| **Reliability engineering** | $X$ = fraction of components functioning at a given time |
| **Finance** | $X$ = market share proportion; recovery rates in credit risk |
| **Ecology** | $X$ = fraction of habitat occupied by a species |

**Why Beta is special in Bayesian statistics:** If we observe $k$ successes in $n$ Bernoulli trials and use a $\text{Beta}(\alpha, \beta)$ prior, the posterior distribution is $\text{Beta}(\alpha + k, \beta + n - k)$ — the same family, updated easily.

---

## Task 9 — Application Concept

```
Controls:
  α = [slider 0.1 – 10]
  β = [slider 0.1 – 10]

Display:
  PDF curve (smooth) on [0, 1]
  Shaded region for P(a ≤ X ≤ b) — user inputs a and b
  CDF curve
  Mean = α/(α+β)  and  Mode = (α-1)/(α+β-2) [if α,β > 1]

Educational presets:
  [Uniform]   α=1,  β=1
  [Symmetric] α=β=3
  [Skewed R]  α=2,  β=5
  [Skewed L]  α=5,  β=2
  [U-shaped]  α=0.5, β=0.5
```

---

## Summary

| Feature | Beta$(\alpha, \beta)$ |
|---------|----------------------|
| Support | $[0, 1]$ |
| PDF | $\frac{x^{\alpha-1}(1-x)^{\beta-1}}{B(\alpha,\beta)}$ |
| Mean | $\frac{\alpha}{\alpha+\beta}$ |
| Variance | $\frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}$ |
| Mode | $\frac{\alpha-1}{\alpha+\beta-2}$ (if $\alpha, \beta > 1$) |
| Special case | Beta$(1,1)$ = Uniform$[0,1]$ |
| Shape $\alpha=\beta>1$ | Symmetric bell |
| Shape $\alpha<\beta$ | Right-skewed |
| Shape $\alpha>\beta$ | Left-skewed |
| Shape $\alpha<1, \beta<1$ | U-shaped |
| Key application | Prior for proportions in Bayesian statistics |
