# Task 7 — Negative Binomial Distribution

---

## Background & Key Concepts

The **Negative Binomial distribution** is the natural generalization of the Geometric distribution. While the Geometric asks "how many trials until the **first** success?", the Negative Binomial asks "how many trials until the **$r$-th** success?"

It counts the total number of trials (successes + failures) needed to reach a pre-specified number of successes. The random part is the number of failures accumulated along the way.

**Special case:** When $r = 1$, the Negative Binomial reduces to the Geometric distribution.

---

## Task 0 — The Experiment

**Experiment:** Repeatedly roll a die with $P(\text{six}) = p = 1/6$ until the $r = 3$rd six appears. Count the total number of rolls.

**Sample space:** $\Omega = $ all finite binary sequences that end in a success (S) and contain exactly $r-1$ successes before the last position.

For $r = 3$, an elementary outcome looks like:
$$\omega = \underbrace{F F S F F F S F S}_{9 \text{ total rolls, 3rd success on roll 9}}$$

Formally, $\omega$ is a sequence of length $k$ where:
- The last symbol is always $S$ (success),
- Among the first $k-1$ symbols, exactly $r-1$ are $S$.

**Random variable:** $X(\omega)$ = total number of trials (rolls) until the $r$-th success.

For $\omega$ above: $X(\omega) = 9$.

**Support:** $\{r, r+1, r+2, \ldots\}$

We need at least $r$ trials (if all first $r$ are successes), and in principle the wait could be arbitrarily long.

---

## Task 1 — PMF and Parameters

**Counting argument:** For $X = k$ (the $r$-th success occurs on trial $k$):
- Trial $k$ must be a success: probability $p$.
- Among the first $k-1$ trials, exactly $r-1$ must be successes: $\binom{k-1}{r-1}$ arrangements, each with probability $p^{r-1}(1-p)^{k-r}$.

$$\boxed{P(X = k) = \binom{k-1}{r-1} p^r (1-p)^{k-r}, \quad k = r, r+1, r+2, \ldots}$$

**Parameters:**
- $r \ge 1$: number of successes we wait for (a positive integer).
- $0 < p < 1$: probability of success on each trial.

**Notation:** $X \sim \text{NegBin}(r, p)$ or $X \sim \text{NB}(r, p)$.

**Mean and Variance:**
$$E[X] = \frac{r}{p}, \qquad \text{Var}(X) = \frac{r(1-p)}{p^2}$$

**Intuition:** The mean is $r$ times the expected wait for a single success ($1/p$). Makes sense — waiting for $r$ successes takes $r$ times as long on average.

---

## Task 2 — Support

The support is $\{r, r+1, r+2, \ldots\}$.

**Why starts at $r$?** The minimum number of trials to achieve $r$ successes is exactly $r$ (if every trial is a success).

**Why infinite?** Just like the Geometric, there is no upper bound — failures can accumulate indefinitely, though with probability 1 the $r$-th success eventually occurs.

**Validity check:**
$$\sum_{k=r}^{\infty} \binom{k-1}{r-1} p^r (1-p)^{k-r} = 1$$

This follows from the **negative binomial series** expansion (the name of the distribution comes from this algebraic identity).

---

## Task 3 — PMF Graphs for Several Parameters

### Varying $r$ (fixed $p = 0.4$)

**$r=1$ (Geometric):**
```
P(X=k)
0.40 |↑
0.24 |  ↑
0.14 |    ↑
0.09 |      ↑
0.05 |        ↑
     +--+--+--+--+--+--+--> k
     1  2  3  4  5  6
     (strictly decreasing — Geometric)
```

**$r=3$:**
```
P(X=k)
0.23 |         ↑
0.21 |      ↑     ↑
0.14 |            ↑
0.08 |   ↑           ↑
0.02 |                  ↑
     +--+--+--+--+--+--+--+--> k
     3  4  5  6  7  8  9
     (bell-shaped, peak shifts right)
```

**$r=6$:**
```
P(X=k)
0.20 |               ↑
0.17 |            ↑     ↑
0.12 |         ↑           ↑
0.06 |      ↑                 ↑
0.02 |                           ↑
     +--+--+--+--+--+--+--+--+--> k
     6  8 10 12 14 16 18
     (wider, peaks further right, more symmetric)
```

### Varying $p$ (fixed $r = 3$)

| $p$ | Mean $=r/p$ | Shape |
|-----|-------------|-------|
| 0.2 | 15 | Spread out far right |
| 0.4 | 7.5 | Moderate spread |
| 0.6 | 5 | Compact, near $r=3$ |
| 0.8 | 3.75 | Very concentrated near $k=3$ |

---

## Task 4 — CDF Graphs

**Example: $\text{NB}(3, 0.4)$**

| $k$ | $P(X=k)$ | $F(k)$ |
|-----|----------|--------|
| 3 | 0.0640 | 0.0640 |
| 4 | 0.1152 | 0.1792 |
| 5 | 0.1382 | 0.3174 |
| 6 | 0.1382 | 0.4557 |
| 7 | 0.1244 | 0.5801 |
| 8 | 0.1037 | 0.6838 |
| 9 | 0.0829 | 0.7667 |
| 10 | 0.0621 | 0.8289 |
| 12 | 0.0319 | 0.9134 |
| 15 | 0.0091 | 0.9730 |

The CDF climbs from 0 at $k=r$ and asymptotically approaches 1, forming a staircase.

---

## Task 5 — How Parameters Change the Distribution

### Effect of changing $p$ (fixed $r$):
- **Larger $p$:** Success is easier, so fewer trials needed. Distribution shifts **left** (toward $k = r$). Becomes more concentrated.
- **Smaller $p$:** Success is rare, so many trials needed. Distribution shifts **right**. Heavy tail extends far.

### Effect of changing $r$ (fixed $p$):
- **Larger $r$:** Waiting for more successes. Distribution shifts **right** (mean $= r/p$ grows). Becomes wider and more **symmetric** (by CLT, approaches Normal for large $r$).
- **Smaller $r$:** Fewer successes needed. Distribution is more **right-skewed**.

---

## Task 6 — Computing Probabilities

**Setup:** $X \sim \text{NB}(3, 0.4)$

**$P(X = 5)$** (3rd success on trial 5 — 2 successes and 2 failures in first 4 trials, then success):
$$P(X=5) = \binom{4}{2}(0.4)^3(0.6)^2 = 6 \cdot 0.064 \cdot 0.36 = 0.1382$$

**$P(X \le 6)$** (3rd success by trial 6):
$$P(X \le 6) = F(6) \approx 0.4557$$

**$P(X > 7)$** (still haven't gotten 3rd success after 7 trials):
$$P(X > 7) = 1 - F(7) = 1 - 0.5801 = 0.4199$$

**$P(4 \le X \le 7)$:**
$$P(4 \le X \le 7) = F(7) - F(3) = 0.5801 - 0.0640 = 0.5161$$

---

## Task 7 — Generalization of the Geometric

The Geometric distribution is the special case $r = 1$:

$$\text{NB}(1, p): \quad P(X = k) = \binom{k-1}{0} p^1 (1-p)^{k-1} = p(1-p)^{k-1}$$

This is exactly the Geometric PMF.

**Additive property:** If $X_1, X_2, \ldots, X_r$ are independent $\text{Geo}(p)$ random variables (waiting times for successes 1, 2, ..., $r$), then:

$$X_1 + X_2 + \cdots + X_r \sim \text{NB}(r, p)$$

This is the deepest insight: the Negative Binomial is the **sum of $r$ independent Geometric random variables**. Each Geometric counts the wait for one success; summing them counts the total wait for all $r$ successes.

| Feature | Geometric$(p)$ | NegBin$(r, p)$ |
|---------|----------------|-----------------|
| Successes waited for | 1 | $r$ |
| Support | $\{1, 2, \ldots\}$ | $\{r, r+1, \ldots\}$ |
| Mean | $1/p$ | $r/p$ |
| Variance | $(1-p)/p^2$ | $r(1-p)/p^2$ |
| Shape | Always decreasing | Bell-shaped for $r \ge 2$ |

---

## Task 8 — Practical Applications

| Application | Setup |
|-------------|-------|
| **Quality testing** | A batch passes when the $r$-th non-defective item is found. $X$ = total items inspected. |
| **Clinical trials** | Trial ends when $r$ patients have recovered. $X$ = total patients enrolled. |
| **Sports** | Team wins series when it has $r$ victories. $X$ = total games played. |
| **Ecology** | Researcher needs $r$ specimens of a rare species. $X$ = total animals captured. |
| **Insurance** | Policy expires after $r$ claims. $X$ = total time periods until expiration. |
| **Machine learning** | Training stops after $r$ consecutive improvements. $X$ = total iterations. |
| **Overdispersed counts** | When $\text{Var}(X) > E[X]$, the NegBin often fits better than Poisson. |

The last point is particularly important: the Negative Binomial is widely used in statistics as an **alternative to Poisson** for count data when the variance exceeds the mean (overdispersion).

---

## Task 9 — Application Concept

```
Controls:
  r = [slider: 1 – 20 successes]
  p = [slider: 0.01 – 0.99]
  k range: [display range]

Display:
  PMF bars for NegBin(r, p)
  Overlay: Geometric(p) in different color when r=1 confirmed same
  Mean = r/p, Variance = r(1-p)/p² displayed numerically
  CDF staircase

Educational note:
  Show NB(1, p) == Geo(p) when r=1
  Show that for large r, shape approaches Normal by CLT
```

---

## Summary

| Feature | NegBin$(r, p)$ |
|---------|-----------------|
| Support | $\{r, r+1, r+2, \ldots\}$ |
| PMF | $\binom{k-1}{r-1} p^r (1-p)^{k-r}$ |
| Mean | $r/p$ |
| Variance | $r(1-p)/p^2$ |
| Special case | NB$(1, p)$ = Geometric$(p)$ |
| Additive property | Sum of $r$ independent Geo$(p)$ variables |
| Shape | Right-skewed for small $r$; more symmetric for large $r$ |
