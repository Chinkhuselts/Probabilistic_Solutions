# Task 3 — Binomial Distribution $\text{Bin}(n, p)$

---

## Background & Key Concepts

The **Binomial distribution** models the number of successes in a fixed number of independent, identical trials — each trial having exactly two outcomes: **success** (with probability $p$) or **failure** (with probability $1-p$).

Think of it as: "I flip a (possibly unfair) coin $n$ times — how many heads do I get?"

The **Bernoulli distribution** $\text{Bin}(1, p)$ is the special case of a single trial.

---

## Task 0 — The Experiment

**Experiment:** Perform $n$ independent Bernoulli trials, each with success probability $p$.

**Sample space:** $\Omega = \{0,1\}^n$ — the set of all binary strings of length $n$.

For example, with $n = 3$:
$$\Omega = \{000, 001, 010, 011, 100, 101, 110, 111\}$$
where $1$ = success, $0$ = failure.

**Elementary outcome:** $\omega = (r_1, r_2, \ldots, r_n)$ where each $r_i \in \{0, 1\}$.

For example, $\omega = (1, 0, 1, 1, 0)$ means: success, fail, success, success, fail.

**Random variable:** $X(\omega) = r_1 + r_2 + \cdots + r_n$ — the **total number of successes**.

For $\omega = (1, 0, 1, 1, 0)$: $X(\omega) = 3$.

**Support:** $\{0, 1, 2, \ldots, n\}$

---

## Task 1 — The PMF

**How many ways can we get exactly $k$ successes in $n$ trials?**

We need to choose which $k$ of the $n$ positions are successes: $\binom{n}{k}$ ways.

Each such arrangement has probability $p^k \cdot (1-p)^{n-k}$ (successes times failures).

$$\boxed{P(X = k) = \binom{n}{k} p^k (1-p)^{n-k}, \quad k = 0, 1, \ldots, n}$$

where $\binom{n}{k} = \frac{n!}{k!(n-k)!}$ is the **binomial coefficient**.

**Notation:** $X \sim \text{Bin}(n, p)$.

**Mean and Variance:**
$$E[X] = np, \qquad \text{Var}(X) = np(1-p)$$

---

## Task 2 — Support

The support of $X \sim \text{Bin}(n, p)$ is $\{0, 1, 2, \ldots, n\}$.

- **Minimum value:** $0$ (all trials failed).
- **Maximum value:** $n$ (all trials succeeded).
- The support is **finite** — there are exactly $n+1$ possible values.

---

## Task 3 — PMF Graphs

### Case A: Fixed $n = 10$, varying $p$

**$\text{Bin}(10, 0.2)$** — low success probability, distribution skewed right:

```
P(X=k)
0.30 |    ↑
0.27 |    |
0.20 |  ↑ |  ↑
0.09 |  | |  |  ↑
0.03 |↑ | |  |  |  ↑
0.00 +--+--+--+--+--+--+--+--+--+--+--> k
     0  1  2  3  4  5  6  7  8  9 10
     (most mass on the left — few successes expected)
```

**$\text{Bin}(10, 0.5)$** — fair coin, distribution symmetric:
```
P(X=k)
0.25 |          ↑  ↑
0.21 |        ↑    ↑  ↑
0.12 |      ↑          ↑
0.04 |   ↑                ↑
0.00 |↑                      ↑
     +--+--+--+--+--+--+--+--+--+--+--> k
     0  1  2  3  4  5  6  7  8  9 10
     (symmetric around k = 5)
```

**$\text{Bin}(10, 0.8)$** — high success probability, distribution skewed left:
```
P(X=k)
0.30 |                   ↑
0.27 |                ↑  |
0.20 |             ↑  |  ↑
0.09 |          ↑  |     |
0.03 |       ↑  |        |  ↑
0.00 +--+--+--+--+--+--+--+--+--+--+--> k
     0  1  2  3  4  5  6  7  8  9 10
     (mirror image of p=0.2 — most mass on the right)
```

### Case B: Fixed $p = 0.4$, varying $n$

| $n$ | Peak at | Spread |
|-----|---------|--------|
| 5 | $k = 2$ | Narrow |
| 10 | $k = 4$ | Medium |
| 20 | $k = 8$ | Wide |

As $n$ grows, the distribution **shifts right** (more successes) and **spreads out** — but by the Central Limit Theorem, it becomes approximately bell-shaped.

---

## Task 4 — CDF

The CDF $F(k) = P(X \le k) = \sum_{j=0}^{k} \binom{n}{j} p^j (1-p)^{n-j}$ has no closed form in general, but is computed by summation.

**Example: $\text{Bin}(5, 0.5)$**

| $k$ | $P(X=k)$ | $F(k) = P(X \le k)$ |
|-----|----------|---------------------|
| 0 | $0.03125$ | $0.03125$ |
| 1 | $0.15625$ | $0.18750$ |
| 2 | $0.31250$ | $0.50000$ |
| 3 | $0.31250$ | $0.81250$ |
| 4 | $0.15625$ | $0.96875$ |
| 5 | $0.03125$ | $1.00000$ |

The CDF is again a staircase, with equal jumps at $k=2$ and $k=3$ (due to symmetry).

---

## Task 5 — How Shape Changes

### When $p$ increases (fixed $n$):
- The distribution **shifts right** — more successes become likely.
- The peak (mode) moves toward $n$.
- At $p = 0.5$: perfectly **symmetric**.
- At $p > 0.5$: **left-skewed** (mass concentrated near $n$).
- At $p < 0.5$: **right-skewed** (mass concentrated near $0$).

### When $n$ increases (fixed $p$):
- The distribution **spreads out** (variance $= np(1-p)$ grows).
- The peak shifts to higher values (mean $= np$ grows).
- The distribution becomes more **bell-shaped** (by CLT).
- Individual probabilities $P(X=k)$ get **smaller** (probability spread over more values).

---

## Task 6 — Computing Probabilities

**Setup:** $X \sim \text{Bin}(5, 0.4)$

PMF values:

| $k$ | $P(X=k)$ | $F(k)$ |
|-----|----------|--------|
| 0 | $0.07776$ | $0.07776$ |
| 1 | $0.25920$ | $0.33696$ |
| 2 | $0.34560$ | $0.68256$ |
| 3 | $0.23040$ | $0.91296$ |
| 4 | $0.07680$ | $0.98976$ |
| 5 | $0.01024$ | $1.00000$ |

**$P(X = 2)$**
$$P(X=2) = \binom{5}{2}(0.4)^2(0.6)^3 = 10 \cdot 0.16 \cdot 0.216 = 0.3456$$

**$P(X \le 3)$**
$$P(X \le 3) = F(3) = 0.91296$$

**$P(X \ge 3)$**
$$P(X \ge 3) = 1 - P(X \le 2) = 1 - F(2) = 1 - 0.68256 = 0.31744$$

**$P(1 \le X \le 3)$**
$$P(1 \le X \le 3) = F(3) - F(0) = 0.91296 - 0.07776 = 0.83520$$

---

## Task 7 — PMF vs CDF Approach

**$P(X \ge 3)$:**

*From PMF (direct sum):*
$$P(X=3) + P(X=4) + P(X=5) = 0.23040 + 0.07680 + 0.01024 = 0.31744$$

*From CDF (complement):*
$$1 - F(2) = 1 - 0.68256 = 0.31744 \checkmark$$

The CDF approach requires only one lookup and a subtraction, whereas the PMF approach requires summing all terms from $k=3$ to $n=5$. For large $n$, the CDF is far more efficient.

---

## Task 8 — Practical Applications

| Application | Description |
|-------------|-------------|
| **Quality control** | $n$ items inspected, $X$ = number defective. $p$ = defect rate. |
| **Clinical trials** | $n$ patients treated, $X$ = number who recover. $p$ = drug efficacy. |
| **Opinion polls** | $n$ voters surveyed, $X$ = number favoring a candidate. |
| **Sports** | $n$ free throws, $X$ = number made. $p$ = player's success rate. |
| **Network reliability** | $n$ packets sent, $X$ = number received. $p$ = success probability. |
| **Genetics** | Each offspring independently inherits a trait with probability $p$. |

**Key assumption to check:** The Binomial model requires **independence** of trials and **constant** $p$. If these fail (e.g., sampling without replacement from a small population), the **Hypergeometric** model should be used instead.

---

## Task 9 — Application Concept

An interactive tool for comparing Binomial distributions:

```
Controls:
  n₁ = [slider 1–50]    p₁ = [slider 0.0–1.0]   Color: Blue
  n₂ = [slider 1–50]    p₂ = [slider 0.0–1.0]   Color: Red

Display: [PMF] or [CDF]
Probability query: P(a ≤ X ≤ b) = ?   a=[input]  b=[input]

Output: Two overlapping bar charts (PMF) or step functions (CDF).
```

**Key comparison to show:** Plot $\text{Bin}(10, 0.3)$ vs $\text{Bin}(10, 0.7)$ to demonstrate how the distribution mirrors around $n/2$ when $p \to 1-p$.

---

## Summary

| Feature | Value for $\text{Bin}(n, p)$ |
|---------|-------------------------------|
| Support | $\{0, 1, 2, \ldots, n\}$ |
| PMF | $\binom{n}{k} p^k (1-p)^{n-k}$ |
| Mean | $np$ |
| Variance | $np(1-p)$ |
| Shape at $p < 0.5$ | Right-skewed |
| Shape at $p = 0.5$ | Symmetric |
| Shape at $p > 0.5$ | Left-skewed |
| Special case | $\text{Bin}(1,p)$ = Bernoulli$(p)$ |
