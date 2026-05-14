# Task 4 — Geometric Distribution

---

## Background & Key Concepts

The **Geometric distribution** models the **waiting time until the first success** in a sequence of independent, identical Bernoulli trials.

Unlike the Binomial (fixed number of trials), here the number of trials is itself random — we keep going until we see a success. The key question is: "How many trials does it take?"

It is the only discrete distribution with the **memoryless property**: past failures give no information about future trials.

---

## Task 0 — The Experiment

**Experiment:** Repeatedly flip a (possibly biased) coin with $P(\text{heads}) = p$ until the first heads appears.

**Sample space:** $\Omega = \{S, FS, FFS, FFFS, \ldots\}$

In general: $\omega_k$ = "fail $k-1$ times, then succeed on trial $k$."

Written out:
- $\omega_1 = S$ (succeed immediately)
- $\omega_2 = FS$ (fail once, then succeed)
- $\omega_3 = FFS$ (fail twice, then succeed)
- $\omega_k = \underbrace{FF\cdots F}_{k-1} S$

**Elementary outcome:** $\omega = $ a specific string of F's followed by one S.

**Random variable:** $X(\omega)$ = the **trial number** on which the first success occurs.

So $X(\omega_k) = k$.

**Support:** $\{1, 2, 3, 4, \ldots\}$ — a countably infinite set.

---

## Task 1 — PMF and CDF

### PMF

For the first success to occur on trial $k$, we need:
- Trials $1, 2, \ldots, k-1$ to be failures: probability $(1-p)^{k-1}$
- Trial $k$ to be a success: probability $p$

$$\boxed{P(X = k) = (1-p)^{k-1} \cdot p, \quad k = 1, 2, 3, \ldots}$$

Let $q = 1-p$ (failure probability). Then: $P(X = k) = q^{k-1} \cdot p$.

**Mean and Variance:**
$$E[X] = \frac{1}{p}, \qquad \text{Var}(X) = \frac{1-p}{p^2} = \frac{q}{p^2}$$

Intuitively: if success probability is $p = 0.25$, we expect to wait $\frac{1}{0.25} = 4$ trials on average.

### CDF

$$F(k) = P(X \le k) = \sum_{j=1}^{k} (1-p)^{j-1} p = 1 - (1-p)^k$$

$$\boxed{F(k) = 1 - (1-p)^k = 1 - q^k, \quad k = 1, 2, 3, \ldots}$$

**Verify:** As $k \to \infty$, $(1-p)^k \to 0$, so $F(k) \to 1$ ✓

**Also:** $F(0) = P(X \le 0) = 0$ — we cannot have 0 or fewer trials.

---

## Task 2 — Why the Support is Infinite

In the Binomial distribution, you perform exactly $n$ trials, so $X \le n$ always. Here, there is no upper bound on the number of trials — in principle, a success might never occur (though with probability 1 it eventually does).

**Formal argument:** $P(X > k) = (1-p)^k$ for any $k$. For any finite $k$, this is positive (as long as $p < 1$), meaning there is always some chance the first success hasn't occurred yet.

**But:** $\sum_{k=1}^{\infty} P(X=k) = \sum_{k=1}^{\infty} q^{k-1} p = p \cdot \frac{1}{1-q} = p \cdot \frac{1}{p} = 1$ ✓

The support is infinite, yet the probabilities still sum to 1.

---

## Task 3 — PMF Graphs for Several Values of $p$

The PMF always starts high at $k=1$ (first trial) and decreases geometrically — hence the name.

**$p = 0.5$** (fair coin):
```
P(X=k)
0.50 | ↑
0.25 |    ↑
0.13 |       ↑
0.06 |          ↑
0.03 |             ↑
     +--+--+--+--+--+--+--+--> k
     1  2  3  4  5  6  7
```

**$p = 0.3$** (less likely success):
```
P(X=k)
0.30 | ↑
0.21 |    ↑
0.15 |       ↑
0.10 |          ↑
0.07 |             ↑
0.05 |                ↑
     +--+--+--+--+--+--+--+--> k
     1  2  3  4  5  6  7
```

**$p = 0.1$** (rare success, very heavy tail):
```
P(X=k)
0.10 | ↑  ↑  ↑  ↑  ↑  ↑  ↑  ↑  ↑  ↑
0.09 |
0.08 |
     +--+--+--+--+--+--+--+--+--+--> k
     1  2  3  4  5  6  7  8  9 10
     (probabilities decrease very slowly)
```

---

## Task 4 — CDF Graphs

The CDF $F(k) = 1 - (1-p)^k$ grows quickly for large $p$ and slowly for small $p$.

**Values of $F(k) = P(X \le k)$:**

| $k$ | $p=0.5$ | $p=0.3$ | $p=0.1$ |
|-----|---------|---------|---------|
| 1 | 0.500 | 0.300 | 0.100 |
| 2 | 0.750 | 0.510 | 0.190 |
| 3 | 0.875 | 0.657 | 0.271 |
| 5 | 0.969 | 0.832 | 0.410 |
| 10 | 0.999 | 0.972 | 0.651 |
| 20 | ≈1 | 0.999 | 0.878 |

```
F(k)
1.0 |         p=0.5 ─────────────
    |       p=0.3 ─────────────────
0.5 |     p=0.1 ─────────────────────────
    |
0.0 +------+------+------+------+--> k
    0      5     10     15     20
```

For large $p$: the CDF reaches 1 quickly (success comes soon).
For small $p$: the CDF grows slowly (long wait).

---

## Task 5 — How Graphs Change with $p$

| Change | Effect on PMF | Effect on CDF |
|--------|--------------|---------------|
| **$p$ increases** | Spike at $k=1$ taller; probabilities drop faster | CDF climbs steeply; reaches 1 sooner |
| **$p$ decreases** | Spike at $k=1$ shorter; heavy tail extends further | CDF climbs gently; long flat region before reaching 1 |

**The geometric rate of decay** is $q = 1-p$. Each step multiplies the probability by $q$:
$$\frac{P(X = k+1)}{P(X = k)} = q$$

This constant ratio is the hallmark of geometric decay.

---

## Task 6 — Computing Probabilities

**Setup:** $X \sim \text{Geo}(0.3)$, so $p = 0.3$, $q = 0.7$.

**$P(X = 4)$** (first success on trial 4):
$$P(X=4) = (0.7)^3 \cdot 0.3 = 0.343 \cdot 0.3 = 0.1029$$

**$P(X \le 5)$** (first success within 5 trials):
$$P(X \le 5) = 1 - (0.7)^5 = 1 - 0.16807 = 0.83193$$

**$P(X > 5)$** (first success after trial 5 — still waiting):
$$P(X > 5) = 1 - P(X \le 5) = (0.7)^5 = 0.16807$$

**$P(3 \le X \le 6)$:**
$$P(3 \le X \le 6) = F(6) - F(2) = (1 - 0.7^6) - (1 - 0.7^2) = 0.7^2 - 0.7^6$$
$$= 0.49 - 0.117649 = 0.372351$$

---

## Task 7 — Tail Probabilities and Waiting Time

$P(X > k) = (1-p)^k$ has a direct interpretation:

> "The probability that you have to wait more than $k$ trials for the first success equals $(1-p)^k$."

**The Memoryless Property:**

$$P(X > m + n \mid X > m) = P(X > n)$$

**Proof:**
$$P(X > m+n \mid X > m) = \frac{P(X > m+n)}{P(X > m)} = \frac{q^{m+n}}{q^m} = q^n = P(X > n)$$

**Interpretation:** If you've already failed $m$ times, your remaining waiting time has the same distribution as if you were starting fresh. Past failures are irrelevant — each trial is independent.

This is why the geometric distribution describes **forgetful** processes: a slot machine that has not paid out for 100 pulls is no more (or less) likely to pay on the next pull.

---

## Task 8 — Practical Applications

| Application | Variable $X$ |
|-------------|-------------|
| **Manufacturing** | Number of items inspected until the first defective one is found |
| **Telecommunications** | Number of transmission attempts until first successful delivery |
| **Clinical testing** | Number of patients enrolled until first adverse reaction observed |
| **Gambling** | Number of rounds until first win |
| **Web servers** | Number of requests handled until first timeout |
| **Biology** | Number of cell divisions until a mutation occurs |
| **Reliability** | Number of uses of a component until first failure |

**When does the model apply?**
- Trials must be **independent**.
- Success probability $p$ must be **constant** (no learning or fatigue).
- We are counting trials until the **first** success.

---

## Task 9 — Application Concept

Extending the distribution visualizer:

```
Controls:
  Distribution: [Geometric]
  p = [slider 0.01 – 0.99]
  k_max = [slider for display range]

Show:
  PMF bar chart (truncated at k_max)
  CDF staircase
  Mean = 1/p  displayed numerically
  P(X > k) = (1-p)^k computed for user-input k
```

**Comparison to add:** Plot Geometric($p$) vs Geometric($2p$) side by side to demonstrate the faster decay.

---

## Summary

| Feature | Geometric$(p)$ |
|---------|----------------|
| Support | $\{1, 2, 3, \ldots\}$ (infinite) |
| PMF | $(1-p)^{k-1} \cdot p$ |
| CDF | $1 - (1-p)^k$ |
| Mean | $\frac{1}{p}$ |
| Variance | $\frac{1-p}{p^2}$ |
| Key property | Memoryless |
| Shape | Always strictly decreasing |
| Tail | $P(X>k) = (1-p)^k$ |
