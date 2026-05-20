# Problem 5 — Independence from data

---

## Setup

A streaming platform recorded data for 200 users.

| | Watched a movie ($M$) | Did not watch ($M^c$) | Total |
|---|---|---|---|
| Premium ($A$) | 84 | 36 | 120 |
| Free ($A^c$) | 56 | 24 | 80 |
| **Total** | **140** | **60** | **200** |

**Events:**
- $A$ = the user has a premium account
- $M$ = the user watched a movie during the weekend

All probabilities are counts divided by $n = 200$.

---

## Part 1 — Basic Probabilities

$$P(A) = \frac{120}{200} = \boxed{0.60}$$

$$P(M) = \frac{140}{200} = \boxed{0.70}$$

$$P(A\cap M) = \frac{84}{200} = \boxed{0.42}$$

---

## Part 2 — Conditional Probabilities

**$P(M\mid A)$** — probability of watching, given the user has a premium account:

$$P(M\mid A) = \frac{P(A\cap M)}{P(A)} = \frac{84/200}{120/200} = \frac{84}{120} = \boxed{0.70}$$

Among premium users, **70%** watched a movie.

**$P(M\mid A^c)$** — probability of watching, given the user has a free account:

$$P(M\mid A^c) = \frac{P(A^c\cap M)}{P(A^c)} = \frac{56/200}{80/200} = \frac{56}{80} = \boxed{0.70}$$

Among free users, also **70%** watched a movie.

---

## Part 3 — Are $A$ and $M$ Independent?

Two events are **independent** if any one of the following equivalent conditions holds:

**Condition 1:** $P(A\cap M) = P(A)\cdot P(M)$

$$P(A)\cdot P(M) = 0.60 \times 0.70 = 0.42$$
$$P(A\cap M) = 0.42$$
$$\boxed{0.42 = 0.42} \checkmark$$

**Condition 2:** $P(M\mid A) = P(M)$

$$P(M\mid A) = 0.70 = P(M) \checkmark$$

**Condition 3:** $P(M\mid A^c) = P(M)$

$$P(M\mid A^c) = 0.70 = P(M) \checkmark$$

All three conditions are satisfied. **Yes, $A$ and $M$ are independent.**

---

## Part 4 — What Independence Means Here

Independence means that **knowing a user's account type gives no information about whether they watched a movie**.

In concrete terms:
- Among premium users: 70% watched a movie.
- Among free users: 70% watched a movie.
- Overall: 70% of all users watched a movie.

The account type makes no difference to movie-watching behavior. Premium and free users are equally likely to watch over the weekend.

**What independence does NOT mean:**
- It does not mean the two events are unrelated in every real-world sense.
- It does not mean the same number of people in each group watched — 84 premium vs 56 free users watched, but the rates (proportions) are identical.
- It does not mean $A$ and $M$ cannot occur together — in fact they commonly do ($P(A\cap M) = 0.42$).

Independence is purely a **probabilistic statement about rates**, not about absolute counts.

**Table structure that reveals independence:**

Notice that the ratio of the rows is constant:

| | Watched | Did not watch | Ratio |
|---|---|---|---|
| Premium | 84 | 36 | $84:36 = 7:3$ |
| Free | 56 | 24 | $56:24 = 7:3$ |

When the row proportions are identical across all columns, the two variables are independent. This perfect proportionality is exactly what independence looks like in a table.

---

## Summary

| Quantity | Value |
|----------|-------|
| $P(A)$ | 0.60 |
| $P(M)$ | 0.70 |
| $P(A\cap M)$ | 0.42 |
| $P(M\mid A)$ | 0.70 |
| $P(M\mid A^c)$ | 0.70 |
| $P(A)\cdot P(M)$ | 0.42 |
| Independent? | **Yes** — all three checks pass |

**Key takeaway:** Independence is confirmed when the conditional probabilities equal the unconditional probability — knowing $A$ occurred does not update our belief about $M$.
