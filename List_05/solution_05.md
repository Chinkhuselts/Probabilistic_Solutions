# Task 5 — Poisson Distribution

---

## Background & Key Concepts

The **Poisson distribution** models the number of random events that occur in a fixed interval of time, space, or volume, when:
- Events occur **independently** of each other,
- Events occur at a **constant average rate** $\lambda > 0$,
- Two events cannot occur at exactly the same instant (events are rare enough in any tiny sub-interval).

It is named after the French mathematician Siméon Denis Poisson (1837) and is one of the most important distributions in applied probability.

---

## Task 0 — The Experiment

**Experiment:** Count the number of customers arriving at a coffee shop between 8:00 and 9:00 AM, given that on average $\lambda = 12$ customers arrive per hour.

**Sample space:** $\Omega = \{0, 1, 2, 3, \ldots\}$ — any non-negative integer number of arrivals is possible (in principle).

**Elementary outcome:** $\omega = k$ means "exactly $k$ customers arrived during the hour."

**Random variable:** $X(\omega) = \omega$ = the observed count of arrivals.

**Support:** $\{0, 1, 2, 3, \ldots\}$ — the support is infinite, since arbitrarily many events could occur.

---

## Task 1 — PMF and Parameter

$$\boxed{P(X = k) = \frac{\lambda^k e^{-\lambda}}{k!}, \quad k = 0, 1, 2, \ldots}$$

**The parameter $\lambda$** is the **average number of events** in the interval. It must satisfy $\lambda > 0$.

**Notation:** $X \sim \text{Poisson}(\lambda)$ or $X \sim \text{Poi}(\lambda)$.

**Mean and Variance:**
$$E[X] = \lambda, \qquad \text{Var}(X) = \lambda$$

A remarkable property: **the mean and variance are equal**, both equal to $\lambda$.

**Validity check:**
$$\sum_{k=0}^{\infty} \frac{\lambda^k e^{-\lambda}}{k!} = e^{-\lambda} \sum_{k=0}^{\infty} \frac{\lambda^k}{k!} = e^{-\lambda} \cdot e^{\lambda} = 1 \checkmark$$

---

## Task 2 — Support

The support of $X \sim \text{Poi}(\lambda)$ is $\{0, 1, 2, 3, \ldots\}$ — all non-negative integers.

- **No upper bound:** Any number of events is possible.
- **Lower bound:** $k \ge 0$ — we count events, so negative values are impossible.
- $P(X = 0) = e^{-\lambda} > 0$ — it is always possible that no events occur.

---

## Task 3 — PMF Graphs for Several $\lambda$

**$\lambda = 1$** (rare events):
```
P(X=k)
0.37 | ↑
0.37 |    ↑
0.18 |       ↑
0.06 |          ↑
0.02 |             ↑
0.00 +--+--+--+--+--+--+--> k
     0  1  2  3  4  5
     (maximum at k=0 or k=1)
```

**$\lambda = 4$** (moderate):
```
P(X=k)
0.20 |          ↑
0.19 |       ↑     ↑
0.15 |    ↑        ↑
0.09 |                ↑
0.05 | ↑
0.01 |                   ↑
0.00 +--+--+--+--+--+--+--+--+--> k
     0  1  2  3  4  5  6  7  8
     (peak near k=3 or k=4)
```

**$\lambda = 10$** (common events):
```
P(X=k)
0.13 |                   ↑  ↑
0.12 |                ↑     ↑
0.10 |             ↑           ↑
0.06 |          ↑                 ↑
0.02 |       ↑                       ↑
0.00 +--+--+--+--+--+--+--+--+--+--+--+--+--> k
     0  2  4  6  8 10 12 14 16 18 20
     (bell-shaped, centered around k=10)
```

**Pattern:** As $\lambda$ increases, the distribution shifts right and becomes more symmetric (bell-shaped). The peak is near $k = \lambda$.

---

## Task 4 — CDF Graphs

The CDF $F(k) = P(X \le k) = \sum_{j=0}^{k} \frac{\lambda^j e^{-\lambda}}{j!}$ has no simple closed form and is computed by summation.

**Example: $\text{Poi}(3)$**

| $k$ | $P(X=k)$ | $F(k)$ |
|-----|----------|--------|
| 0 | 0.0498 | 0.0498 |
| 1 | 0.1494 | 0.1991 |
| 2 | 0.2240 | 0.4232 |
| 3 | 0.2240 | 0.6472 |
| 4 | 0.1680 | 0.8153 |
| 5 | 0.1008 | 0.9161 |
| 6 | 0.0504 | 0.9665 |
| 7 | 0.0216 | 0.9881 |
| 8 | 0.0081 | 0.9962 |
| 9 | 0.0027 | 0.9989 |
| 10 | 0.0008 | 0.9997 |

The CDF is again a staircase function, with smaller and smaller jumps as $k$ grows.

---

## Task 5 — How Shape Changes When $\lambda$ Increases

| $\lambda$ | Mean | Mode | Shape |
|-----------|------|------|-------|
| 0.5 | 0.5 | 0 | Very right-skewed, heavily concentrated at 0 and 1 |
| 1 | 1 | 0 or 1 | Right-skewed |
| 3 | 3 | 2 or 3 | Moderately right-skewed |
| 5 | 5 | 4 or 5 | Mildly skewed |
| 10 | 10 | 9 or 10 | Nearly symmetric |
| 50 | 50 | 49 or 50 | Very close to Normal (by CLT) |

**Key result (Poisson approximation to Binomial):** If $n$ is large and $p$ is small with $np \approx \lambda$, then $\text{Bin}(n,p) \approx \text{Poi}(\lambda)$. The Poisson distribution is the limiting case of the Binomial when trials are very many and each success is very rare.

---

## Task 6 — Computing Probabilities

**Setup:** $X \sim \text{Poi}(3)$.

**$P(X = 0)$** (no events at all):
$$P(X = 0) = \frac{3^0 e^{-3}}{0!} = e^{-3} \approx 0.0498$$

**$P(X = 2)$**:
$$P(X = 2) = \frac{3^2 e^{-3}}{2!} = \frac{9 e^{-3}}{2} \approx 0.2240$$

**$P(X \le 4)$** (from CDF table):
$$P(X \le 4) = F(4) \approx 0.8153$$

**$P(X \ge 5)$** (complement):
$$P(X \ge 5) = 1 - P(X \le 4) = 1 - 0.8153 = 0.1847$$

**$P(2 \le X \le 5)$**:
$$P(2 \le X \le 5) = F(5) - F(1) = 0.9161 - 0.1991 = 0.7170$$

---

## Task 7 — CDF vs Direct Summation

**$P(2 \le X \le 5)$ using PMF (direct sum):**
$$P(X=2) + P(X=3) + P(X=4) + P(X=5) = 0.2240 + 0.2240 + 0.1680 + 0.1008 = 0.7168$$

**$P(2 \le X \le 5)$ using CDF:**
$$F(5) - F(1) = 0.9161 - 0.1991 = 0.7170$$

*(Small rounding differences; both methods agree.)*

**Which is better?**
- **PMF summation** is intuitive for small ranges (2–3 terms).
- **CDF subtraction** is faster for wider ranges (e.g., $P(0 \le X \le 20)$ would require 21 terms from the PMF but just 1 CDF lookup).

---

## Task 8 — Practical Applications

| Application | $\lambda$ represents |
|-------------|---------------------|
| **Call centers** | Average number of calls per minute |
| **Radioactive decay** | Average number of particles emitted per second |
| **Traffic engineering** | Average number of cars passing a point per minute |
| **Insurance** | Average number of claims per year |
| **Epidemiology** | Average number of new cases per day in a region |
| **Web servers** | Average number of HTTP requests per second |
| **Astronomy** | Average number of photons reaching a detector per second |
| **Printing** | Average number of defects per page |
| **Biology** | Average number of mutations per gene per generation |

**Key assumption to verify:** Events must be **independent** and must occur at a **constant rate**. If the rate changes over time (e.g., more calls during business hours), a non-homogeneous Poisson process or a different model may be needed.

---

## Task 9 — Application Concept

```
Controls:
  λ = [slider 0.1 – 20]
  k range: [0 to k_max]
  Query: P(a ≤ X ≤ b) where a, b are user inputs

Display:
  PMF bar chart with current λ highlighted
  CDF staircase
  Mean and Variance shown as "λ = ___"
  Comparison: two curves for λ₁ and λ₂ simultaneously

Educational note: Show "Poisson ≈ Bin(n,p) when n large, p small, np=λ"
  by overlaying Poi(3) and Bin(1000, 0.003) — nearly identical!
```

---

## Summary

| Feature | Poisson$(\lambda)$ |
|---------|---------------------|
| Support | $\{0, 1, 2, 3, \ldots\}$ (infinite) |
| PMF | $\frac{\lambda^k e^{-\lambda}}{k!}$ |
| CDF | $e^{-\lambda} \sum_{j=0}^{k} \frac{\lambda^j}{j!}$ (no closed form) |
| Mean | $\lambda$ |
| Variance | $\lambda$ (equal to mean!) |
| Mode | $\lfloor \lambda \rfloor$ (or both $\lfloor \lambda \rfloor$ and $\lambda$ if $\lambda$ is an integer) |
| Shape for small $\lambda$ | Right-skewed |
| Shape for large $\lambda$ | Approximately Normal |
| Limiting case of | $\text{Bin}(n, p)$ when $n \to \infty$, $p \to 0$, $np = \lambda$ |
