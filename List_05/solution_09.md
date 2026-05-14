# Task 9 — Gamma Distribution

---

## Background & Key Concepts

The **Gamma distribution** is a continuous distribution defined on $[0, \infty)$ — it models non-negative quantities, most naturally **waiting times** or **accumulated durations**. It generalizes the exponential distribution (waiting for 1 event) to the waiting time until the $k$-th event in a Poisson process.

The **Chi-square distribution** ($\chi^2$) is a special case of the Gamma family, widely used in statistical hypothesis testing.

Just as the Negative Binomial generalized the Geometric to "wait for the $r$-th success," the Gamma generalizes the exponential to "wait for the $r$-th arrival."

---

## Task 0 — The Experiment

**Experiment:** Measure the total time (in hours) until a service center receives its 3rd complaint call, given that calls arrive at a Poisson rate of $\lambda = 2$ calls per hour.

**Sample space:** $\Omega = [0, \infty)$ — any non-negative duration is possible.

**Elementary outcome:** $\omega \in [0, \infty)$ — the specific elapsed time when the 3rd call arrives.

**Random variable:** $X(\omega) = \omega$ — the elapsed time.

**Support:** $(0, \infty)$ — the wait is strictly positive (takes some positive time).

---

## Task 1 — PDF and Parameters

**Two common parametrizations exist:**

### Shape-Rate parametrization: $\text{Gamma}(k, \theta)$

$$\boxed{f(x; k, \theta) = \frac{x^{k-1} e^{-x/\theta}}{\theta^k \Gamma(k)}, \quad x > 0}$$

- $k > 0$: **shape parameter** — controls how many "events" we're waiting for.
- $\theta > 0$: **scale parameter** — stretches or compresses the time axis ($\theta = 1/\lambda$ where $\lambda$ is the Poisson rate).

**Mean and Variance:**
$$E[X] = k\theta, \qquad \text{Var}(X) = k\theta^2$$

### Shape-Rate parametrization: $\text{Gamma}(\alpha, \beta)$ (alternative)

Some textbooks use $\beta = 1/\theta$ (the **rate**):
$$f(x; \alpha, \beta) = \frac{\beta^\alpha x^{\alpha-1} e^{-\beta x}}{\Gamma(\alpha)}, \quad x > 0$$

**Notation:** $X \sim \text{Gamma}(k, \theta)$ (or $\text{Gamma}(\alpha, \beta)$ depending on convention).

The **Gamma function** $\Gamma(k)$ normalizes the PDF:
$$\Gamma(k) = \int_0^{\infty} t^{k-1} e^{-t}\, dt$$

For positive integers: $\Gamma(n) = (n-1)!$. For non-integers: $\Gamma(1/2) = \sqrt{\pi}$.

---

## Task 2 — Support

The support is $(0, \infty)$ — the positive real line (strictly greater than 0).

- The distribution is **unbounded above** — waiting time can be arbitrarily long.
- The PDF **starts at 0** at the origin (for $k > 1$), rises to a peak, then falls.
- For $k \le 1$: the PDF is **decreasing** from $x = 0$ (like the exponential).
- As $x \to \infty$: the exponential term $e^{-x/\theta}$ dominates, so the PDF decays to 0.

---

## Task 3 — PDF Graphs for Several Parameters

### Varying shape $k$ (fixed $\theta = 1$)

**$k = 1$** (Exponential — waiting for 1st event):
```
f(x)
1.0 |╲
0.5 |   ╲
0.2 |      ╲___
0.0 |           ╲────────────────
    +--+--+--+--+--+--+--> x
    0  1  2  3  4  5  6
    (strictly decreasing from x=0)
```

**$k = 2$** (waiting for 2nd event):
```
f(x)
0.4 |   ╱▔╲
0.2 | ╱     ╲
0.0 |╱        ╲__________
    +--+--+--+--+--+--+--> x
    0  1  2  3  4  5  6
    (peak at x = (k-1)θ = 1)
```

**$k = 5$** (waiting for 5th event):
```
f(x)
0.2 |         ╱▔▔╲
0.1 |       ╱      ╲
0.0 |─────╱           ╲────
    +--+--+--+--+--+--+--+-> x
    0  2  4  6  8  10 12
    (peak at x = 4, more symmetric)
```

**$k = 10$** (waiting for 10th event):
```
f(x)
0.13|              ╱▔▔▔╲
0.06|           ╱         ╲
0.00|─────────╱              ╲─────
    +----+----+----+----+-------> x
    0    5   10   15   20
    (nearly bell-shaped, peak at x = 9)
```

### Varying scale $\theta$ (fixed $k = 3$)

| $\theta$ | Mean $= k\theta$ | Shape | Stretch |
|---------|------------------|-------|---------|
| 0.5 | 1.5 | Compressed toward 0 | Tall, narrow |
| 1.0 | 3.0 | Standard | Medium |
| 2.0 | 6.0 | Stretched right | Short, wide |

**The scale $\theta$ stretches the time axis** without changing the overall shape — just the horizontal scale.

---

## Task 4 — CDF Graphs

The CDF of the Gamma distribution is the **regularized incomplete gamma function**:

$$F(x; k, \theta) = \frac{\gamma(k, x/\theta)}{\Gamma(k)} = P\left(k, \frac{x}{\theta}\right)$$

where $\gamma(k, z) = \int_0^z t^{k-1} e^{-t}\, dt$ is the lower incomplete gamma function.

For integer $k$, there is a finite explicit formula:

$$F(x; k, \theta) = 1 - e^{-x/\theta} \sum_{j=0}^{k-1} \frac{(x/\theta)^j}{j!}$$

**Example: $\text{Gamma}(3, 1)$, CDF values:**

| $x$ | $F(x)$ |
|-----|--------|
| 0.5 | 0.014 |
| 1.0 | 0.080 |
| 2.0 | 0.323 |
| 3.0 | 0.577 |
| 4.0 | 0.762 |
| 5.0 | 0.875 |
| 7.0 | 0.970 |
| 10.0 | 0.9997 |

The CDF is a smooth S-curve (not a staircase, since $X$ is continuous).

---

## Task 5 — How Parameters Change Shape

### Effect of shape parameter $k$:

| $k$ | Interpretation | Shape |
|-----|---------------|-------|
| $k = 1$ | Exponential | Strictly decreasing |
| $1 < k < 2$ | Slightly rounded at start | Mild peak, then decay |
| $k \ge 2$ | Clear peak at $(k-1)\theta$ | Unimodal, right-skewed |
| $k \gg 1$ | Many events accumulated | Nearly Normal (by CLT) |

**Mode formula (for $k \ge 1$):** $\text{Mode} = (k-1)\theta$

As $k \to \infty$, by CLT: $\text{Gamma}(k, \theta) \approx N(k\theta, k\theta^2)$.

### Effect of scale parameter $\theta$:

- Larger $\theta$: distribution stretches **right** — longer waiting times (slower rate $\lambda = 1/\theta$).
- Smaller $\theta$: distribution compressed **left** — shorter waiting times (faster rate).
- $\theta$ does **not** change the shape — only the scale.

---

## Task 6 — Chi-Square as a Special Case

The **Chi-square distribution with $\nu$ degrees of freedom**, $\chi^2(\nu)$, is:

$$\chi^2(\nu) = \text{Gamma}\!\left(\frac{\nu}{2},\; 2\right)$$

That is: shape $k = \nu/2$ and scale $\theta = 2$.

**PDF:**
$$f(x; \nu) = \frac{x^{\nu/2 - 1} e^{-x/2}}{2^{\nu/2}\,\Gamma(\nu/2)}, \quad x > 0$$

**Mean and Variance:**
$$E[\chi^2] = \nu, \qquad \text{Var}(\chi^2) = 2\nu$$

**Key fact from statistics:** If $Z_1, Z_2, \ldots, Z_\nu$ are independent standard Normal variables, then:
$$Z_1^2 + Z_2^2 + \cdots + Z_\nu^2 \sim \chi^2(\nu)$$

**Shapes of $\chi^2(\nu)$:**

| $\nu$ | Shape |
|-------|-------|
| 1 | Extremely right-skewed, spike near 0 |
| 2 | Exponential (exactly) |
| 3 | Moderate skew |
| 5 | Bell-shaped, right-skewed |
| 10 | Approaching Normal |
| 30+ | Nearly Normal |

---

## Task 7 — Computing Probabilities

**Setup:** $X \sim \text{Gamma}(3, 2)$ (mean $= 6$, variance $= 12$).

$$P(X \le a) = F(a; 3, 2)$$

For integer $k=3$:
$$F(x; 3, 2) = 1 - e^{-x/2}\left(1 + \frac{x}{2} + \frac{x^2}{8}\right)$$

**$P(X \le 4)$:**
$$F(4; 3, 2) = 1 - e^{-2}\left(1 + 2 + 2\right) = 1 - 5e^{-2} \approx 1 - 0.677 = 0.323$$

**$P(X \ge 8)$:**
$$P(X \ge 8) = 1 - F(8; 3, 2) = e^{-4}(1 + 4 + 8) = 13e^{-4} \approx 0.238$$

**$P(2 \le X \le 6)$:**
$$P(2 \le X \le 6) = F(6; 3, 2) - F(2; 3, 2) \approx 0.577 - 0.080 = 0.497$$

In practice, use software: `pgamma(x, shape=3, scale=2)` in R, or `scipy.stats.gamma.cdf(x, a=3, scale=2)` in Python.

---

## Task 8 — Practical Applications

### Gamma Distribution

| Application | $X$ represents |
|-------------|----------------|
| **Reliability engineering** | Time until $k$-th component failure |
| **Insurance** | Total claim amounts (sum of exponential losses) |
| **Hydrology** | Total monthly rainfall |
| **Queuing theory** | Service time when service has multiple stages |
| **Pharmacokinetics** | Drug concentration over time |
| **Finance** | Variance in stochastic volatility models |
| **Ecology** | Time between population bottlenecks |

### Chi-Square Distribution

| Application | $\nu$ is |
|-------------|---------|
| **Goodness-of-fit tests** | (number of categories $-1$) |
| **Independence tests** | (rows $-1$) $\times$ (columns $-1$) |
| **Confidence intervals for variance** | Sample size $-1$ |
| **Likelihood ratio tests** | Number of constrained parameters |

**Why Chi-square matters:** Nearly every classical statistical test (t-test, F-test, ANOVA) involves distributions derived from the Gamma family.

---

## Task 9 — Application Concept

```
Controls:
  Distribution: [Gamma] or [Chi-square]
  k (shape) = [slider 0.5 – 15]
  θ (scale) = [slider 0.1 – 5]

  If Chi-square:  ν = [slider 1 – 30]  (k = ν/2, θ = 2 auto-set)

Display:
  PDF curve on [0, x_max]
  CDF curve
  Mean = kθ, Variance = kθ² shown
  Shaded region for P(a ≤ X ≤ b)

Educational overlay:
  Show Gamma(k=1, θ) == Exponential(λ=1/θ)
  Show χ²(ν) == Gamma(ν/2, 2) by overlapping
  Show convergence to Normal as k grows
```

---

## Summary

| Feature | Gamma$(k, \theta)$ | $\chi^2(\nu)$ |
|---------|-------------------|--------------|
| Support | $(0, \infty)$ | $(0, \infty)$ |
| PDF | $\frac{x^{k-1}e^{-x/\theta}}{\theta^k \Gamma(k)}$ | $\frac{x^{\nu/2-1}e^{-x/2}}{2^{\nu/2}\Gamma(\nu/2)}$ |
| Mean | $k\theta$ | $\nu$ |
| Variance | $k\theta^2$ | $2\nu$ |
| Mode | $(k-1)\theta$ (for $k\ge1$) | $\nu - 2$ (for $\nu\ge2$) |
| Special case $k=1$ | Exponential$(\lambda=1/\theta)$ | — |
| $\chi^2$ as Gamma | $k=\nu/2$, $\theta=2$ | — |
| Shape for large $k$ | Approximately Normal | Approximately Normal |
