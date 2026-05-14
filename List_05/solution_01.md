# Task 1 — Discrete Distribution Given by a PMF Table

---

## Background & Key Concepts

A **random variable** $X$ is a function that assigns a real number to each outcome of a random experiment. When $X$ can only take a finite or countably infinite set of values, it is called **discrete**.

The **Probability Mass Function (PMF)** tells us the probability of each individual value:

$$P(X = x) = p(x) \quad \text{for each } x \text{ in the support}$$

The **Cumulative Distribution Function (CDF)** answers the question "what is the probability that $X$ is at most $x$?":

$$F(x) = P(X \le x) = \sum_{t \le x} P(X = t)$$

---

## The Given Distribution

| $x$ | $-2$ | $0$ | $1$ | $3$ | $5$ |
|-----|------|-----|-----|-----|-----|
| $P(X=x)$ | $0.10$ | $0.25$ | $0.30$ | $0.20$ | $0.15$ |

The **support** of $X$ is the set $\{-2, 0, 1, 3, 5\}$ — these are the only values $X$ can take.

---

## Task 0 — Constructing a Probability Space

Before working with formulas, we must ground the random variable in a concrete experiment.

**Experiment:** Draw one ball at random from an urn containing 20 balls labelled as follows:
- 2 balls labelled $-2$
- 5 balls labelled $0$
- 6 balls labelled $1$
- 4 balls labelled $3$
- 3 balls labelled $5$

**Sample space:** $\Omega = \{\omega_1, \omega_2, \ldots, \omega_{20}\}$ where each $\omega_i$ is one specific ball.

**Elementary outcome:** $\omega$ = "the particular ball drawn."

**Random variable:** $X(\omega)$ = the number written on the drawn ball.

**Probability of each ball:** Since the draw is fair, $P(\{\omega_i\}) = \frac{1}{20}$ for each ball.

**Check:**
$$P(X = -2) = \frac{2}{20} = 0.10, \quad P(X = 0) = \frac{5}{20} = 0.25, \quad P(X = 1) = \frac{6}{20} = 0.30$$
$$P(X = 3) = \frac{4}{20} = 0.20, \quad P(X = 5) = \frac{3}{20} = 0.15 \checkmark$$

> **Key distinction:** The sample space $\Omega$ consists of 20 individual balls (elementary outcomes). The support $\{-2,0,1,3,5\}$ consists of the 5 values that the random variable $X$ maps those balls to. These are different objects.

---

## Task 1 — Validity Check

For a PMF to be valid, two conditions must hold:

**Condition 1:** All probabilities are non-negative.
$$0.10 \ge 0, \quad 0.25 \ge 0, \quad 0.30 \ge 0, \quad 0.20 \ge 0, \quad 0.15 \ge 0 \checkmark$$

**Condition 2:** All probabilities sum to 1.
$$0.10 + 0.25 + 0.30 + 0.20 + 0.15 = 1.00 \checkmark$$

**Conclusion:** This is a valid probability distribution.

---

## Task 2 — Graph of the PMF

The PMF is drawn as **vertical spikes** (arrows or stems) at each support point. The height of each spike equals the probability.

```
P(X=x)
  0.30 |           ↑
  0.25 |     ↑     |
  0.20 |     |     |     ↑
  0.15 |     |     |     |     ↑
  0.10 | ↑   |     |     |     |
  0.00 +--+--+--+--+--+--+--+--+--> x
        -2   0    1    3    5
```

**Reading the graph:**
- The tallest spike is at $x = 1$ (most likely value, $P = 0.30$).
- The shortest spike is at $x = -2$ (least likely, $P = 0.10$).
- There are **no** spikes between support points — those values have zero probability.

---

## Task 3 — Constructing the CDF

The CDF $F(x) = P(X \le x)$ is built by **accumulating** (adding up) probabilities as $x$ increases.

**Step-by-step construction:**

| Region | Calculation | $F(x)$ |
|--------|-------------|--------|
| $x < -2$ | No values yet | $0$ |
| $-2 \le x < 0$ | $P(X=-2) = 0.10$ | $0.10$ |
| $0 \le x < 1$ | $0.10 + 0.25$ | $0.35$ |
| $1 \le x < 3$ | $0.35 + 0.30$ | $0.65$ |
| $3 \le x < 5$ | $0.65 + 0.20$ | $0.85$ |
| $x \ge 5$ | $0.85 + 0.15$ | $1.00$ |

**Formal piecewise definition:**

$$F(x) = \begin{cases} 0 & x < -2 \\ 0.10 & -2 \le x < 0 \\ 0.35 & 0 \le x < 1 \\ 0.65 & 1 \le x < 3 \\ 0.85 & 3 \le x < 5 \\ 1.00 & x \ge 5 \end{cases}$$

---

## Task 4 — Graph of the CDF

The CDF is a **staircase function**: flat between support points, with a jump at each support point.

```
F(x)
1.00 |                              ●────────────────
     |
0.85 |                    ●─────────○
     |
0.65 |          ●──────────○
     |
0.35 |   ●───────○
     |
0.10 |○──●
     |
0.00 ○
     +-----+-----+----+-----+------> x
          -2     0    1     3     5
```

**Legend:** `●` = closed endpoint (CDF includes this point), `○` = open endpoint.

> The CDF is **right-continuous**: at each jump point, the CDF takes the *higher* value (the filled dot is on the right side of the jump).

---

## Task 5 — Jumps of the CDF and the PMF

Each jump in the CDF corresponds exactly to a mass in the PMF.

| Jump location $x$ | CDF before jump | CDF after jump | Jump size | PMF value $P(X=x)$ |
|--------------------|-----------------|----------------|-----------|---------------------|
| $x = -2$ | $0$ | $0.10$ | $0.10$ | $0.10$ ✓ |
| $x = 0$ | $0.10$ | $0.35$ | $0.25$ | $0.25$ ✓ |
| $x = 1$ | $0.35$ | $0.65$ | $0.30$ | $0.30$ ✓ |
| $x = 3$ | $0.65$ | $0.85$ | $0.20$ | $0.20$ ✓ |
| $x = 5$ | $0.85$ | $1.00$ | $0.15$ | $0.15$ ✓ |

**Rule:** $P(X = x) = F(x) - F(x^-)$, where $F(x^-)$ is the CDF value just before the jump.

This means: **you can always recover the PMF from the CDF** by measuring the jump sizes.

---

## Task 6 — Computing Probabilities

### Using the PMF directly

**$P(X = 1)$**
$$P(X = 1) = 0.30$$

**$P(X \le 1)$**
$$P(X \le 1) = P(X=-2) + P(X=0) + P(X=1) = 0.10 + 0.25 + 0.30 = 0.65$$

**$P(X < 1)$** *(strictly less than)*
$$P(X < 1) = P(X=-2) + P(X=0) = 0.10 + 0.25 = 0.35$$

> Note: $P(X < 1) \ne P(X \le 1)$ because $X = 1$ has positive probability!

**$P(0 < X \le 3)$**
$$P(0 < X \le 3) = P(X=1) + P(X=3) = 0.30 + 0.20 = 0.50$$

**$P(X \ge 3)$**
$$P(X \ge 3) = P(X=3) + P(X=5) = 0.20 + 0.15 = 0.35$$

**$P(X \ge 3) = 1 - P(X < 3) = 1 - P(X \le 1) = 1 - 0.65 = 0.35 \checkmark$**

---

## Task 7 — PMF vs CDF: Comparison

| Quantity | From PMF | From CDF |
|----------|----------|----------|
| $P(X = 1)$ | Look up directly: $0.30$ | Jump at $x=1$: $0.65 - 0.35 = 0.30$ |
| $P(X \le 1)$ | Sum up to 1: $0.65$ | Read off: $F(1) = 0.65$ |
| $P(X < 1)$ | Sum strictly below: $0.35$ | Left limit: $F(1^-) = 0.35$ |
| $P(0 < X \le 3)$ | Sum $k \in \{1,3\}$: $0.50$ | $F(3) - F(0) = 0.85 - 0.35 = 0.50$ |
| $P(X \ge 3)$ | Sum $k \in \{3,5\}$: $0.35$ | $1 - F(3^-) = 1 - 0.65 = 0.35$ |

**Key insight:**
- The **PMF** is better when you want the probability of *specific individual values*.
- The **CDF** is better when you want *cumulative or interval* probabilities — you only need to read two values and subtract.

---

## Task 8 — Interactive Application (Concept)

An interactive tool for this distribution would:

1. Display the PMF as a bar/spike chart with labeled heights.
2. Display the CDF as a step function.
3. Allow the user to click on a region and see the corresponding probability highlighted.
4. Let the user enter values $a, b$ and compute $P(a \le X \le b)$ automatically.

**Implementation hint (JavaScript sketch):**
```javascript
const pmf = { "-2": 0.10, "0": 0.25, "1": 0.30, "3": 0.20, "5": 0.15 };

// Compute CDF at any x
function cdf(x) {
  return Object.entries(pmf)
    .filter(([val, _]) => Number(val) <= x)
    .reduce((sum, [_, prob]) => sum + prob, 0);
}

// Interval probability P(a < X <= b)
function intervalProb(a, b) {
  return cdf(b) - cdf(a);
}
```

---

## Summary

| Concept | What it tells you |
|---------|------------------|
| PMF $P(X=x)$ | Probability of one specific value |
| CDF $F(x) = P(X \le x)$ | Probability of being at or below $x$ |
| Support | The set of values with positive probability |
| Jump of CDF at $x$ | Equals $P(X=x)$ |
| CDF is right-continuous | At a jump, CDF takes the higher value |
| $P(X < x)$ | $= F(x^-) = F(x) - P(X=x)$ |
| $P(a < X \le b)$ | $= F(b) - F(a)$ |
