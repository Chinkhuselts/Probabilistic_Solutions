# Task 2 — Discrete Distribution Given by a CDF Table

---

## Background & Key Concepts

In Task 1 we started from a **PMF** and built the CDF by accumulating probabilities.  
Here we reverse the process: we start from a **CDF table** and reconstruct the PMF by measuring jumps.

**Relationship between CDF and PMF:**

$$P(X = x) = F(x) - F(x^-)$$

where $F(x^-)$ denotes the CDF value just *before* (to the left of) the point $x$.

This means:
- If the CDF is flat at $x$, then $P(X = x) = 0$ — that value carries no probability mass.
- If the CDF **jumps** at $x$, then $P(X = x) > 0$ — that value is in the support.

---

## The Given CDF

| $x$ | $-1$ | $0$ | $2$ | $4$ | $6$ |
|-----|------|-----|-----|-----|-----|
| $F(x)$ | $0.15$ | $0.35$ | $0.60$ | $0.85$ | $1.00$ |

These are the **jump points** — the values at which the CDF increases.

---

## Task 0 — Constructing a Probability Space

**Experiment:** Roll a specially weighted die with 20 sides, where the sides are labelled as follows:
- 3 sides labelled $-1$
- 4 sides labelled $0$
- 5 sides labelled $2$
- 5 sides labelled $4$
- 3 sides labelled $6$

**Sample space:** $\Omega = \{\omega_1, \omega_2, \ldots, \omega_{20}\}$, each $\omega_i$ being one specific face.

**Elementary outcome:** $\omega$ = "the face that lands face-up."

**Random variable:** $X(\omega)$ = the number written on the face that lands face-up.

**Key distinction:** $\Omega$ has 20 outcomes; the support of $X$ is $\{-1, 0, 2, 4, 6\}$ — only 5 values.

---

## Task 1 — Reconstructing the PMF from the CDF

**Rule:** At each jump point, $P(X = x) = F(x) - \text{(CDF value just before } x\text{)}$.

We know $F(x) = 0$ for $x < -1$ (no probability accumulated before the first support point).

| Jump at $x$ | CDF before: $F(x^-)$ | CDF after: $F(x)$ | $P(X = x) = F(x) - F(x^-)$ |
|-------------|----------------------|--------------------|------------------------------|
| $x = -1$ | $0$ (nothing yet) | $0.15$ | $0.15$ |
| $x = 0$ | $0.15$ | $0.35$ | $0.20$ |
| $x = 2$ | $0.35$ | $0.60$ | $0.25$ |
| $x = 4$ | $0.60$ | $0.85$ | $0.25$ |
| $x = 6$ | $0.85$ | $1.00$ | $0.15$ |

**Resulting PMF table:**

| $x$ | $-1$ | $0$ | $2$ | $4$ | $6$ |
|-----|------|-----|-----|-----|-----|
| $P(X=x)$ | $0.15$ | $0.20$ | $0.25$ | $0.25$ | $0.15$ |

**Validity check:** $0.15 + 0.20 + 0.25 + 0.25 + 0.15 = 1.00$ ✓

---

## Task 2 — Graph of the PMF

```
P(X=x)
  0.25 |               ↑     ↑
  0.20 |         ↑     |     |
  0.15 | ↑       |     |     |     ↑
  0.10 | |       |     |     |     |
  0.00 +-+-------+-----+-----+-----+--> x
       -1        0     2     4     6
```

**Observations:**
- The distribution is **symmetric** around $x = 2.5$ (roughly): the outer values $-1$ and $6$ have equal probability ($0.15$ each), and the inner pair $2$ and $4$ also equal ($0.25$ each).
- The center values $2$ and $4$ are the most probable.

---

## Task 3 — Redrawing the CDF

The full piecewise definition:

$$F(x) = \begin{cases} 0 & x < -1 \\ 0.15 & -1 \le x < 0 \\ 0.35 & 0 \le x < 2 \\ 0.60 & 2 \le x < 4 \\ 0.85 & 4 \le x < 6 \\ 1.00 & x \ge 6 \end{cases}$$

```
F(x)
1.00 |                              ●────────────────
     |
0.85 |                    ●─────────○
     |
0.60 |          ●──────────○
     |
0.35 |    ●──────○
     |
0.15 |○────●
     |
0.00 ○
     +----+------+--------+--------+---------> x
         -1      0        2        4        6
```

**Legend:** `●` = closed (right-continuous), `○` = open (excluded).

**Key properties of every CDF:**
1. Non-decreasing: it never goes down.
2. Right-continuous: the filled dot is always on the right at each jump.
3. $F(x) \to 0$ as $x \to -\infty$ and $F(x) \to 1$ as $x \to +\infty$.

---

## Task 4 — Jump Points

| Jump location | Jump size | Interpretation |
|---------------|-----------|----------------|
| $x = -1$ | $0.15$ | 15% chance of getting $-1$ |
| $x = 0$ | $0.20$ | 20% chance of getting $0$ |
| $x = 2$ | $0.25$ | 25% chance of getting $2$ |
| $x = 4$ | $0.25$ | 25% chance of getting $4$ |
| $x = 6$ | $0.15$ | 15% chance of getting $6$ |

Between the jump points, the CDF is **flat** — meaning no probability is assigned to values in those intervals. For example, $P(0 < X < 2) = 0$ because the CDF doesn't change between $0$ and $2$.

---

## Task 5 — Why Jump Size = Probability

Consider the jump at $x = 2$:

$$P(X = 2) = P(X \le 2) - P(X \le 2, X \ne 2) = F(2) - F(2^-) = 0.60 - 0.35 = 0.25$$

More intuitively: $F(2) = P(X \le 2)$ includes $P(X=2)$, but the CDF just before $2$ (i.e., $F(2^-)$) does **not** include $P(X=2)$. The difference is exactly the probability of the point.

**General formula:** $\boxed{P(X = x) = F(x) - F(x^-)}$

This is why a CDF with no jumps (a continuous CDF) corresponds to a distribution where every single point has probability zero.

---

## Task 6 — Computing Probabilities from the CDF

**$P(X \le 2)$**
$$P(X \le 2) = F(2) = 0.60$$

**$P(X < 2)$** *(strictly less than — use the left limit)*
$$P(X < 2) = F(2^-) = 0.35$$

**$P(X = 2)$**
$$P(X = 2) = F(2) - F(2^-) = 0.60 - 0.35 = 0.25$$

**$P(0 < X \le 4)$**
$$P(0 < X \le 4) = F(4) - F(0) = 0.85 - 0.35 = 0.50$$

> Note: the formula $P(a < X \le b) = F(b) - F(a)$ excludes $a$ and includes $b$.

**$P(X > 4)$**
$$P(X > 4) = 1 - P(X \le 4) = 1 - F(4) = 1 - 0.85 = 0.15$$

**$P(-1 \le X \le 4)$** *(both endpoints included)*
$$P(-1 \le X \le 4) = F(4) - F(-1^-) = 0.85 - 0 = 0.85$$

---

## Task 7 — Comparison: PMF vs CDF as Starting Point

| What you want to know | Easier from PMF | Easier from CDF |
|-----------------------|-----------------|-----------------|
| $P(X = x)$ for a specific $x$ | ✓ Look up directly | Compute jump: $F(x) - F(x^-)$ |
| $P(X \le b)$ | Sum all values $\le b$ | ✓ Read off $F(b)$ directly |
| $P(a < X \le b)$ | Sum values in $(a,b]$ | ✓ Subtract: $F(b) - F(a)$ |
| $P(X > a)$ | Sum all values $> a$ | ✓ Compute $1 - F(a)$ |
| Whether a value is in the support | ✓ Check if $P(X=x) > 0$ | Check if $F$ jumps at $x$ |
| Shape/symmetry of distribution | ✓ Visually clear from spikes | Less obvious from staircase |

**Summary insight:**
- **Start from PMF** when you want individual point probabilities or visual shape.
- **Start from CDF** when you want cumulative or interval probabilities — subtraction is faster than repeated summation.
- Both representations carry exactly the same information; they are two views of the same distribution.

---

## Task 8 — Extension: Application Accepting CDF Input

Building on the Task 1 application, to accept **CDF input**:

```javascript
// Input: CDF table as sorted array of [x, F(x)] pairs
const cdfTable = [[-1, 0.15], [0, 0.35], [2, 0.60], [4, 0.85], [6, 1.00]];

// Reconstruct PMF by measuring jumps
function reconstructPMF(cdfTable) {
  const pmf = {};
  let prevF = 0;
  for (const [x, Fx] of cdfTable) {
    pmf[x] = Fx - prevF;   // jump size = probability
    prevF = Fx;
  }
  return pmf;
}

// Evaluate CDF at any real x
function evalCDF(x, cdfTable) {
  let result = 0;
  for (const [val, Fval] of cdfTable) {
    if (val <= x) result = Fval;
  }
  return result;
}

// Interval probability P(a < X <= b)
function intervalProb(a, b) {
  return evalCDF(b, cdfTable) - evalCDF(a, cdfTable);
}
```

---

## Summary

| Concept | Rule |
|---------|------|
| PMF from CDF | $P(X=x) = F(x) - F(x^-)$ |
| CDF from PMF | $F(x) = \sum_{t \le x} P(X=t)$ |
| $P(X \le b)$ | $= F(b)$ |
| $P(X < b)$ | $= F(b^-)= F(b) - P(X=b)$ |
| $P(a < X \le b)$ | $= F(b) - F(a)$ |
| $P(a \le X \le b)$ | $= F(b) - F(a^-) = F(b) - F(a) + P(X=a)$ |
| $P(X > a)$ | $= 1 - F(a)$ |
| Support of $X$ | All $x$ where the CDF has a positive jump |
