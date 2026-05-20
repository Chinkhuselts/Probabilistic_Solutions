# Problem 4 — Inclusion–exclusion and double counting

---

## Setup

A survey of 200 employees about two software tools:
- 130 use Tool A
- 90 use Tool B
- 60 use **both** tools

**Events:**
- $A$ = the employee uses Tool A
- $B$ = the employee uses Tool B

---

## Part 1 — Basic Probabilities

$$P(A) = \frac{130}{200} = \boxed{0.65}$$

$$P(B) = \frac{90}{200} = \boxed{0.45}$$

$$P(A\cap B) = \frac{60}{200} = \boxed{0.30}$$

---

## Part 2 — Inclusion–Exclusion

**$P(A\cup B)$** — probability that an employee uses Tool A OR Tool B (or both):

$$\boxed{P(A\cup B) = P(A) + P(B) - P(A\cap B) = 0.65 + 0.45 - 0.30 = 0.80}$$

So 80% of employees (160 out of 200) use at least one of the two tools.

---

## Part 3 — The Three Remaining Regions

Every employee who uses at least one tool belongs to exactly one of three groups:

**$A\setminus B$** — uses Tool A only (not B):
$$P(A\setminus B) = P(A) - P(A\cap B) = 0.65 - 0.30 = \boxed{0.35}$$
*Count: $130 - 60 = 70$ employees.*

**$B\setminus A$** — uses Tool B only (not A):
$$P(B\setminus A) = P(B) - P(A\cap B) = 0.45 - 0.30 = \boxed{0.15}$$
*Count: $90 - 60 = 30$ employees.*

**$A^c\cap B^c$** — uses neither tool:
$$P(A^c\cap B^c) = 1 - P(A\cup B) = 1 - 0.80 = \boxed{0.20}$$
*Count: $200 - 160 = 40$ employees.*

**Verification** (four disjoint regions must sum to 1):

| Region | Count | Probability |
|--------|-------|------------|
| $A$ only: $A\setminus B$ | 70 | 0.35 |
| Both: $A\cap B$ | 60 | 0.30 |
| $B$ only: $B\setminus A$ | 30 | 0.15 |
| Neither: $A^c\cap B^c$ | 40 | 0.20 |
| **Total** | **200** | **1.00** ✓ |

---

## Part 4 — Conditional Probabilities

**$P(A\mid B)$** — probability of using Tool A, given the employee uses Tool B:

$$P(A\mid B) = \frac{P(A\cap B)}{P(B)} = \frac{0.30}{0.45} = \boxed{0.\overline{6} \approx 66.7\%}$$

Among Tool B users, about two-thirds also use Tool A.

**$P(B\mid A)$** — probability of using Tool B, given the employee uses Tool A:

$$P(B\mid A) = \frac{P(A\cap B)}{P(A)} = \frac{0.30}{0.65} = \boxed{0.4615 \approx 46.2\%}$$

Among Tool A users, about 46% also use Tool B.

---

## Part 5 — Why $P(A\cup B) \ne P(A) + P(B)$

$$P(A) + P(B) = 0.65 + 0.45 = 1.10$$

But no probability can exceed 1, and there are clearly employees who use neither tool. The error comes from **counting the overlap twice**:

When we add $P(A) + P(B)$:
- The 70 employees who use A only are counted **once** (in $P(A)$). ✓
- The 30 employees who use B only are counted **once** (in $P(B)$). ✓
- The 60 employees who use **both** are counted **twice** — once in $P(A)$ and once in $P(B)$. ✗

The inclusion–exclusion principle fixes this by subtracting the overlap once:
$$P(A\cup B) = P(A) + P(B) - P(A\cap B) = 1.10 - 0.30 = 0.80$$

This restores each employee to being counted exactly once.

---

## Part 6 — Which Group Is Counted Twice?

The group counted twice is **$A\cap B$** — the 60 employees who use **both** Tool A and Tool B.

They appear in the count for $A$ (because they use Tool A) and again in the count for $B$ (because they also use Tool B). Adding $P(A) + P(B)$ without correction counts them twice. Subtracting $P(A\cap B)$ once brings the count back to the correct total.

**Diagram:**

```
        ┌──────────────────────────────────┐
        │           All 200 employees      │
        │  ┌───────────┐   ┌───────────┐  │
        │  │  A only   │   │  B only   │  │
        │  │    70     │───│    30     │  │
        │  │           │60 │           │  │
        │  └───────────┘   └───────────┘  │
        │         Neither: 40             │
        └──────────────────────────────────┘

P(A) counts: 70 + 60 = 130
P(B) counts: 60 + 30 = 90
P(A) + P(B) counts 60 twice → must subtract P(A∩B) = 60
```

---

## Summary

| Quantity | Value |
|----------|-------|
| $P(A)$ | 0.65 |
| $P(B)$ | 0.45 |
| $P(A\cap B)$ | 0.30 |
| $P(A\cup B)$ | 0.80 |
| $P(A\setminus B)$ | 0.35 |
| $P(B\setminus A)$ | 0.15 |
| $P(A^c\cap B^c)$ | 0.20 |
| $P(A\mid B)$ | 0.667 |
| $P(B\mid A)$ | 0.462 |
