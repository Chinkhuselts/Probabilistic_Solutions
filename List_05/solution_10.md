# Task 10 — Normal Distribution $N(\mu, \sigma^2)$

---

## Background & Key Concepts

The **Normal distribution** (also called the **Gaussian distribution**) is the most important distribution in all of probability and statistics. It appears naturally as the limiting distribution of sums of independent random variables (the **Central Limit Theorem**), and it describes an enormous range of real-world phenomena — from measurement errors to heights, test scores to stock returns.

Its iconic **bell curve** shape is characterized by perfect symmetry around the mean, with most probability concentrated near the center and very little in the tails.

---

## Task 0 — The Experiment

**Experiment:** Measure the height of a randomly selected adult from a population where the average height is $\mu = 170$ cm and individual heights vary with standard deviation $\sigma = 10$ cm.

**Sample space:** $\Omega = \mathbb{R}$ — in principle, the measurement could be any real number.

**Elementary outcome:** $\omega \in \mathbb{R}$ — the specific height recorded.

**Random variable:** $X(\omega) = \omega$ — the observed measurement.

**Support:** $(-\infty, \infty) = \mathbb{R}$ — all real numbers (though physical constraints may make some values implausible, mathematically $X$ can be any real).

> In practice, a negative height has zero physical meaning, but the Normal model assigns tiny probabilities there. For values far enough from $\mu$, these probabilities are negligible.

---

## Task 1 — PDF and Parameters

$$\boxed{f(x; \mu, \sigma^2) = \frac{1}{\sigma\sqrt{2\pi}} \exp\!\left(-\frac{(x-\mu)^2}{2\sigma^2}\right), \quad x \in \mathbb{R}}$$

**Parameters:**
- $\mu \in \mathbb{R}$: the **mean** (also the median and mode) — controls the **location** (where the peak sits).
- $\sigma^2 > 0$: the **variance** — controls the **spread** ($\sigma$ is the standard deviation).

**Notation:** $X \sim N(\mu, \sigma^2)$.

**Standard Normal:** When $\mu = 0$ and $\sigma^2 = 1$: $Z \sim N(0, 1)$.

$$\phi(z) = \frac{1}{\sqrt{2\pi}} e^{-z^2/2} \quad \text{(standard Normal PDF)}$$

$$\Phi(z) = \int_{-\infty}^{z} \phi(t)\, dt \quad \text{(standard Normal CDF)}$$

**Mean, Variance, Mode:**
$$E[X] = \mu, \qquad \text{Var}(X) = \sigma^2, \qquad \text{Mode} = \mu$$

All three coincide at $\mu$ — a hallmark of the Normal distribution's symmetry.

---

## Task 2 — Support

The support is all of $\mathbb{R} = (-\infty, \infty)$.

- The PDF is **never zero** — every real number has a positive density.
- The tails thin rapidly (the exponential $e^{-z^2/2}$ decays faster than any polynomial).
- The **68-95-99.7 rule**:
  - $P(\mu - \sigma \le X \le \mu + \sigma) \approx 68\%$
  - $P(\mu - 2\sigma \le X \le \mu + 2\sigma) \approx 95\%$
  - $P(\mu - 3\sigma \le X \le \mu + 3\sigma) \approx 99.7\%$

---

## Task 3 — PDF Graphs for Several Parameters

### Case A: Fixed $\sigma^2 = 1$, Varying $\mu$

The bell curve **shifts horizontally** — same shape, different location.

```
f(x)
0.40 |    [μ=-2]  [μ=0]   [μ=3]
     |      ╱╲     ╱╲       ╱╲
0.24 |    ╱    ╲ ╱    ╲   ╱    ╲
0.05 |──╱──────╲╱──────╲╱──────╲──
     +--+--+--+--+--+--+--+--+--+-> x
    -5 -4 -3 -2 -1  0  1  2  3  4  5

    (same width, different center)
```

**Observations:**
- Peak height $= \frac{1}{\sigma\sqrt{2\pi}} = \frac{1}{\sqrt{2\pi}} \approx 0.399$ — same for all since $\sigma = 1$.
- The three curves are identical in shape, just translated.

### Case B: Fixed $\mu = 0$, Varying $\sigma^2$

The bell curve **spreads out or concentrates** — same center, different spread.

**$\sigma^2 = 0.25$ ($\sigma = 0.5$)** — tall and narrow:
```
f(x)
0.80 |    ↑↑
0.40 |   ╱  ╲
0.05 |──╱────╲──
     +--+--+--+--> x
        -1  0  1
```

**$\sigma^2 = 1$ ($\sigma = 1$)** — standard:
```
f(x)
0.40 |   ╱╲
0.24 | ╱    ╲
0.05 |╱──────╲
     +--+--+--+--+--+--> x
     -3 -2 -1  0  1  2  3
```

**$\sigma^2 = 4$ ($\sigma = 2$)** — short and wide:
```
f(x)
0.20 |     ╱─╲
0.12 |   ╱     ╲
0.02 |─╱─────────╲──
     +----+----+----+----> x
     -5  -2   0   2   5
```

**Key principle:** Larger $\sigma$ $\Rightarrow$ flatter and wider curve. Smaller $\sigma$ $\Rightarrow$ taller and narrower. **But always: total area = 1.**

---

## Task 4 — CDF Graphs

The Normal CDF is the **error function** and has no closed-form expression:

$$F(x; \mu, \sigma^2) = \Phi\!\left(\frac{x - \mu}{\sigma}\right) = \frac{1}{2}\left[1 + \text{erf}\!\left(\frac{x-\mu}{\sigma\sqrt{2}}\right)\right]$$

where $\Phi$ is the standard Normal CDF.

The CDF is a smooth **S-shaped curve** (sigmoid):

```
F(x)
1.0 |                         ─────────
    |                    ─────
0.5 |──────────────────●────────────────
    |             ─────
0.0 |─────────────
    +------+------+------+------+-----> x
          μ-2σ    μ-σ    μ     μ+σ   μ+2σ

    (●marks the inflection point at x=μ, where F(μ)=0.5 exactly)
```

**Key CDF values for $N(0,1)$:**

| $z$ | $\Phi(z)$ |
|-----|----------|
| $-3$ | 0.0013 |
| $-2$ | 0.0228 |
| $-1$ | 0.1587 |
| $0$ | 0.5000 |
| $1$ | 0.8413 |
| $2$ | 0.9772 |
| $3$ | 0.9987 |

By symmetry: $\Phi(-z) = 1 - \Phi(z)$.

---

## Task 5 — How $\mu$ and $\sigma^2$ Influence the Distribution

| Parameter | Effect on PDF | Effect on CDF |
|-----------|--------------|---------------|
| $\mu$ increases | Curve shifts **right** | S-curve shifts **right** |
| $\mu$ decreases | Curve shifts **left** | S-curve shifts **left** |
| $\sigma^2$ increases | Curve gets **flatter and wider** | S-curve becomes more **gradual** |
| $\sigma^2$ decreases | Curve gets **taller and narrower** | S-curve becomes more **steep** |

The inflection points of the PDF are always at $x = \mu \pm \sigma$ — where the curve changes from concave down to concave up.

---

## Task 6 — Computing Probabilities

All Normal probabilities reduce to the **standard Normal** via standardization:

$$P(X \le a) = \Phi\!\left(\frac{a - \mu}{\sigma}\right)$$

**Setup:** $X \sim N(170, 100)$ (heights in cm, $\mu = 170$, $\sigma = 10$).

**$P(X \le 185)$:**
$$P(X \le 185) = \Phi\!\left(\frac{185-170}{10}\right) = \Phi(1.5) \approx 0.9332$$

**$P(X \ge 155)$:**
$$P(X \ge 155) = 1 - \Phi\!\left(\frac{155-170}{10}\right) = 1 - \Phi(-1.5) = \Phi(1.5) \approx 0.9332$$

*(Symmetric! Being $1.5\sigma$ above the mean has the same tail probability as being $1.5\sigma$ below.)*

**$P(160 \le X \le 180)$:**
$$P(160 \le X \le 180) = \Phi\!\left(\frac{180-170}{10}\right) - \Phi\!\left(\frac{160-170}{10}\right) = \Phi(1) - \Phi(-1) \approx 0.8413 - 0.1587 = 0.6827$$

This is the 68% rule: one standard deviation on each side captures about 68% of probability.

**$P(X \ge 200)$** (tall outlier, 3$\sigma$ above mean):
$$P(X \ge 200) = 1 - \Phi\!\left(\frac{200-170}{10}\right) = 1 - \Phi(3) \approx 1 - 0.9987 = 0.0013$$

Only 0.13% of the population is this tall — rare but not impossible.

---

## Task 7 — Why $P(X = a) = 0$

For any continuous distribution, including the Normal:

$$P(X = a) = \int_a^a f(x)\, dx = 0$$

The integral of any function over a single point (zero-length interval) is always zero.

**Intuition:** The real line $\mathbb{R}$ contains uncountably infinitely many points. If each had positive probability, the total would be infinite — violating the axiom that total probability = 1.

**Consequence:** For the Normal distribution (and all continuous distributions):

$$P(X = a) = 0 \quad \text{for all } a$$
$$P(a < X < b) = P(a \le X < b) = P(a < X \le b) = P(a \le X \le b)$$

Open and closed intervals have identical probabilities — the endpoints contribute nothing.

This contrasts sharply with discrete distributions, where individual points carry positive probability.

---

## Task 8 — Practical Applications

The Normal distribution appears wherever a quantity is determined by many small, independent additive influences:

| Application | $X$ represents |
|-------------|----------------|
| **Anthropometry** | Heights, weights, hand span of adults |
| **Measurement errors** | Random noise in scientific instruments |
| **Test scores** | IQ scores, SAT, standardized exams (by design) |
| **Financial returns** | Daily stock returns (approximately) |
| **Manufacturing** | Diameter of machine-produced parts |
| **Signal processing** | Thermal noise in electronic circuits |
| **Quality control** | Control charts (6-sigma methodology) |
| **Biology** | Phenotypic traits determined by many genes |
| **Weather** | Temperature deviations from seasonal mean |

**The Central Limit Theorem (informal statement):** Let $X_1, X_2, \ldots, X_n$ be i.i.d. random variables with mean $\mu$ and variance $\sigma^2$. Then:
$$\frac{X_1 + X_2 + \cdots + X_n - n\mu}{\sigma\sqrt{n}} \xrightarrow{d} N(0,1) \quad \text{as } n \to \infty$$

**This is why the Normal is everywhere:** any phenomenon resulting from many small, independent additive contributions (genetics, economics, physics) tends to be Normally distributed.

---

## Task 9 — Application Concept

```
Controls:
  μ₁ = [slider -10 – 10]     σ₁ = [slider 0.1 – 5]   Color: Blue
  μ₂ = [slider -10 – 10]     σ₂ = [slider 0.1 – 5]   Color: Red

Display tabs: [PDF]  [CDF]

Probability query:
  Type: [P(X≤a)]  [P(X≥a)]  [P(a≤X≤b)]
  Input: a = [___]   b = [___]
  Result: shown as number + shaded region on graph

Educational annotations:
  Mark μ±σ, μ±2σ, μ±3σ on the PDF curve
  Label "68%", "95%", "99.7%" in shaded bands
  Show standardization: Z = (X-μ)/σ computed live

Presets:
  [Standard Normal]  μ=0, σ=1
  [Heights]          μ=170, σ=10
  [IQ scores]        μ=100, σ=15
```

---

## Summary

| Feature | Normal$(\mu, \sigma^2)$ |
|---------|------------------------|
| Support | $(-\infty, \infty) = \mathbb{R}$ |
| PDF | $\frac{1}{\sigma\sqrt{2\pi}}\exp\!\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)$ |
| Mean | $\mu$ |
| Variance | $\sigma^2$ |
| Mode | $\mu$ (same as mean — symmetric) |
| Median | $\mu$ (same as mean — symmetric) |
| Standard Normal | $\mu=0$, $\sigma^2=1$: CDF is $\Phi$ |
| Standardization | $Z = (X-\mu)/\sigma \sim N(0,1)$ |
| 68-95-99.7 rule | $\pm 1\sigma$: 68%, $\pm 2\sigma$: 95%, $\pm 3\sigma$: 99.7% |
| $P(X=a)$ | $= 0$ for all $a$ (continuous!) |
| Foundational theorem | Central Limit Theorem |
| Key applications | Measurement, biology, finance, quality control |
