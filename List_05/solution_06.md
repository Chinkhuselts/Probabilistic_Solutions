# Task 6 — Hypergeometric Distribution

---

## Background & Key Concepts

The **Hypergeometric distribution** arises when we sample **without replacement** from a finite population containing two types of objects. It is the natural model when selection changes the composition of the remaining pool.

**The classic setup:**
- Population of $N$ objects total.
- $K$ objects are "distinguished" (successes, defectives, red balls, etc.).
- $N - K$ objects are "ordinary."
- Draw a sample of $n$ objects **without replacement** (all samples equally likely).
- $X$ = number of distinguished objects in the sample.

The fundamental difference from the Binomial: in the Binomial, each trial is independent with the same $p$. Here, each draw changes the remaining pool, so trials are **not independent**.

---

## Task 0 — The Experiment

**Experiment:** An urn contains $N = 20$ balls: $K = 7$ are red and $13$ are blue. Draw $n = 5$ balls at random without replacement.

**Sample space:** $\Omega = \{\text{all possible sets of 5 balls from 20}\}$

$$|\Omega| = \binom{20}{5} = 15{,}504$$

Each set is equally likely (probability $\frac{1}{15{,}504}$).

**Elementary outcome:** $\omega$ = a specific set of 5 balls, e.g., $\{R_1, R_3, B_2, B_5, B_{11}\}$ (2 red, 3 blue).

**Random variable:** $X(\omega)$ = number of red balls in the drawn set.

For $\omega = \{R_1, R_3, B_2, B_5, B_{11}\}$: $X(\omega) = 2$.

**Support:** $\{\max(0, n+K-N), \ldots, \min(n, K)\} = \{\max(0, 5+7-20), \ldots, \min(5,7)\} = \{0, 1, 2, 3, 4, 5\}$

---

## Task 1 — PMF and Parameters

**Counting argument:** To get exactly $k$ red balls:
- Choose $k$ reds from $K$ available: $\binom{K}{k}$ ways.
- Choose $n-k$ blues from $N-K$ available: $\binom{N-K}{n-k}$ ways.
- Total ways to choose $n$ from $N$: $\binom{N}{n}$.

$$\boxed{P(X = k) = \frac{\binom{K}{k}\binom{N-K}{n-k}}{\binom{N}{n}}}$$

**Parameters:**
- $N$ = population size (total objects)
- $K$ = number of distinguished objects in population
- $n$ = sample size

**Mean and Variance:**
$$E[X] = n \cdot \frac{K}{N}, \qquad \text{Var}(X) = n \cdot \frac{K}{N} \cdot \frac{N-K}{N} \cdot \frac{N-n}{N-1}$$

The factor $\frac{N-n}{N-1}$ is the **finite population correction factor** — it makes the variance smaller than the Binomial variance when sampling without replacement. When $N$ is large relative to $n$, this factor is near 1 and the distributions agree.

---

## Task 2 — Support

$$\text{support} = \Big\{\max(0,\, n+K-N),\; \max(0,\, n+K-N)+1,\; \ldots,\; \min(n,K)\Big\}$$

**Lower bound** $\max(0, n+K-N)$: You might be **forced** to include some red balls if there aren't enough blue balls to fill the sample.

**Upper bound** $\min(n, K)$: You can't draw more reds than are in the population ($K$), nor more than the sample size ($n$).

**Example:** $N=20$, $K=7$, $n=5$:
- Lower: $\max(0, 5+7-20) = \max(0, -8) = 0$ — possible to draw no reds.
- Upper: $\min(5, 7) = 5$ — possible to draw all 5 as reds.
- Support: $\{0, 1, 2, 3, 4, 5\}$ — all 6 values.

**Different example:** $N=10$, $K=8$, $n=6$:
- Lower: $\max(0, 6+8-10) = \max(0, 4) = 4$ — must get at least 4 reds.
- Upper: $\min(6, 8) = 6$ — can get up to 6 reds.
- Support: $\{4, 5, 6\}$ — only 3 values.

---

## Task 3 — PMF Graphs for Several Parameter Choices

**Fixed $N=20$, $K=7$, varying $n$:**

| $k$ | $n=3$ | $n=5$ | $n=10$ |
|-----|-------|-------|--------|
| 0 | 0.298 | 0.128 | 0.006 |
| 1 | 0.466 | 0.367 | 0.074 |
| 2 | 0.218 | 0.367 | 0.259 |
| 3 | 0.019 | 0.122 | 0.373 |
| 4 | — | 0.015 | 0.233 |
| 5 | — | 0.001 | 0.049 |
| 6 | — | — | 0.006 |
| 7 | — | — | 0.000 |

As $n$ increases, the distribution **shifts right** (more reds expected in a bigger sample) and **spreads out**.

**Fixed $N=20$, $n=5$, varying $K$:**

| $K$ | Interpretation | Shape |
|-----|---------------|-------|
| 2 | Very few reds | Strongly right-skewed; mostly 0 or 1 red |
| 7 | Moderate | Bell-shaped, peak at 1 or 2 |
| 10 | Half red | Symmetric around $k = 2.5$ |
| 15 | Mostly red | Left-skewed; mostly 3, 4, or 5 reds |

---

## Task 4 — CDF Graphs

**Example: $N=20$, $K=7$, $n=5$**

| $k$ | $P(X=k)$ | $F(k) = P(X \le k)$ |
|-----|----------|---------------------|
| 0 | 0.1279 | 0.1279 |
| 1 | 0.3666 | 0.4945 |
| 2 | 0.3666 | 0.8611 |
| 3 | 0.1221 | 0.9832 |
| 4 | 0.0153 | 0.9985 |
| 5 | 0.0008 | 1.0000 |

```
F(k)
1.00 |                    ●──────
0.98 |               ●────○
0.86 |       ●────────○
0.49 |   ●────○
0.13 |○────●
0.00 ○
     +----+----+----+----+----+--> k
     0    1    2    3    4    5
```

---

## Task 5 — How Distribution Changes

### When sample size $n$ changes (fixed $N$, $K$):
- **Larger $n$:** Mean = $n \cdot K/N$ increases — more reds expected. Distribution shifts right and widens.
- **Smaller $n$:** Mean decreases, distribution narrows and shifts left.

### When number of distinguished objects $K$ changes (fixed $N$, $n$):
- **Larger $K$:** More reds in the urn — distribution shifts right toward $\min(n, K)$.
- **Smaller $K$:** Fewer reds — distribution shifts left toward 0.
- **$K = N/2$ (balanced urn):** Distribution is symmetric.

---

## Task 6 — Computing Probabilities

**Setup:** $N=20$, $K=7$, $n=5$. $X$ = number of red balls drawn.

**$P(X = 2)$:**
$$P(X=2) = \frac{\binom{7}{2}\binom{13}{3}}{\binom{20}{5}} = \frac{21 \cdot 286}{15504} = \frac{6006}{15504} \approx 0.3873$$

**$P(X \le 2)$:**
$$P(X \le 2) = F(2) \approx 0.8611$$

**$P(X \ge 3)$:**
$$P(X \ge 3) = 1 - F(2) = 1 - 0.8611 = 0.1389$$

**$P(1 \le X \le 3)$:**
$$P(1 \le X \le 3) = F(3) - F(0) = 0.9832 - 0.1279 = 0.8553$$

---

## Task 7 — Comparison with Binomial

Both models count "successes" in a sample of size $n$, but they differ in one crucial way:

| Feature | Binomial $\text{Bin}(n, p)$ | Hypergeometric $\text{Hyp}(N, K, n)$ |
|---------|----------------------------|---------------------------------------|
| Sampling | **With replacement** | **Without replacement** |
| Trials | Independent | Dependent (each draw changes pool) |
| $p$ constant? | Yes, $p$ fixed throughout | No, changes after each draw |
| Population | Infinite (or large enough) | **Finite** |
| Variance | $np(1-p)$ | $np(1-p) \cdot \frac{N-n}{N-1}$ |
| When equivalent | When $N \to \infty$ | Exact for finite populations |

**Intuition:** In a large population, removing one item barely changes the proportions, so sampling without replacement ≈ sampling with replacement. As $N \to \infty$ with $K/N \to p$, $\text{Hyp}(N, K, n) \to \text{Bin}(n, p)$.

**Rule of thumb:** If the sample is less than 5–10% of the population ($n/N < 0.05$), use the Binomial for simplicity.

---

## Task 8 — Practical Applications

| Application | Setup |
|-------------|-------|
| **Quality control** | Lot of $N$ items, $K$ defective. Inspect $n$; $X$ = number defective found. |
| **Card games** | Deck of 52 cards, 13 spades. Draw 5 cards; $X$ = number of spades. |
| **Clinical trials** | $N$ patients: $K$ on drug A, rest on B. Randomly assign $n$ to treatment group. |
| **Ecology (mark-recapture)** | $N$ total animals, $K$ were tagged. Capture $n$; $X$ = tagged ones recaptured. |
| **Election auditing** | $N$ ballots, $K$ from county A. Audit $n$; $X$ = county A ballots in audit. |
| **Genetics** | Genes on a chromosome; select a block; count functional genes. |

---

## Task 9 — Application Concept

```
Controls:
  N = [slider: population size 10–1000]
  K = [slider: distinguished objects 0–N]
  n = [slider: sample size 1–N]

Display:
  PMF bars for Hypergeometric
  Overlay: Binomial(n, K/N) in different color — shows convergence!
  Mean = n·K/N and Variance shown numerically

Educational note:
  Show that as N → ∞ (K/N = p fixed), Hypergeometric → Binomial(n, p)
```

---

## Summary

| Feature | Hypergeometric$(N, K, n)$ |
|---------|---------------------------|
| Support | $\{\max(0,n+K-N), \ldots, \min(n,K)\}$ |
| PMF | $\dfrac{\binom{K}{k}\binom{N-K}{n-k}}{\binom{N}{n}}$ |
| Mean | $n \cdot \dfrac{K}{N}$ |
| Variance | $n \cdot \dfrac{K}{N} \cdot \dfrac{N-K}{N} \cdot \dfrac{N-n}{N-1}$ |
| Sampling type | Without replacement |
| Vs Binomial | Binomial has independent trials; here they depend |
| Limiting case | $\text{Bin}(n, K/N)$ as $N \to \infty$ |
