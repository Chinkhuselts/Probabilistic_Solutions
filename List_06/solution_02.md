# Problem 2 — Four regions of a sample space

---

## Setup

A company classified 350 support tickets.

| | Solved first contact ($S$) | Not solved ($S^c$) | Total |
|---|---|---|---|
| Technical ($T$) | 90 | 60 | 150 |
| Non-technical ($T^c$) | 160 | 40 | 200 |
| **Total** | **250** | **100** | **350** |

**Events:**
- $T$ = the ticket is technical
- $S$ = the ticket was solved during the first contact

All probabilities are computed by dividing counts by the total $n = 350$.

---

## Part 1 — The Four Disjoint Regions

$$P(T\cap S) = \frac{90}{350} = \boxed{0.2571}$$

> Technical AND solved at first contact.

$$P(T\cap S^c) = \frac{60}{350} = \boxed{0.1714}$$

> Technical AND NOT solved at first contact.

$$P(T^c\cap S) = \frac{160}{350} = \boxed{0.4571}$$

> Non-technical AND solved at first contact.

$$P(T^c\cap S^c) = \frac{40}{350} = \boxed{0.1143}$$

> Non-technical AND NOT solved at first contact.

---

## Part 2 — Verification

The four regions are **mutually exclusive** (no ticket belongs to two regions) and **exhaustive** (every ticket belongs to exactly one). Their probabilities must sum to 1:

$$0.2571 + 0.1714 + 0.4571 + 0.1143 = 0.9999 \approx 1.00 \checkmark$$

*(Small rounding difference; exact fractions: $\frac{90+60+160+40}{350} = \frac{350}{350} = 1$.)*

---

## Part 3 — Union Probabilities

**$P(T\cup S)$** — the ticket is technical OR solved at first contact (or both):

Using inclusion–exclusion:
$$P(T\cup S) = P(T) + P(S) - P(T\cap S)$$

First compute the marginals:
$$P(T) = \frac{150}{350} = 0.4286, \qquad P(S) = \frac{250}{350} = 0.7143$$

$$P(T\cup S) = 0.4286 + 0.7143 - 0.2571 = \boxed{0.8857}$$

Verification by summing three regions:
$$P(T\cap S) + P(T\cap S^c) + P(T^c\cap S) = 0.2571 + 0.1714 + 0.4571 = 0.8857 \checkmark$$

**$P(T^c\cup S)$** — the ticket is non-technical OR solved at first contact (or both):

$$P(T^c) = 1 - P(T) = 1 - 0.4286 = 0.5714$$

$$P(T^c\cup S) = P(T^c) + P(S) - P(T^c\cap S) = 0.5714 + 0.7143 - 0.4571 = \boxed{0.8286}$$

Or equivalently: $P(T^c\cup S) = 1 - P(T\cap S^c) = 1 - 0.1714 = 0.8286$ ✓

> The complement of $(T^c\cup S)$ is the region where the ticket IS technical AND NOT solved — exactly $T\cap S^c$.

---

## Part 4 — Conditional Probabilities

**$P(S\mid T)$** — probability of being solved at first contact, given the ticket is technical:

$$P(S\mid T) = \frac{P(T\cap S)}{P(T)} = \frac{90/350}{150/350} = \frac{90}{150} = \boxed{0.60}$$

Among technical tickets, 60% are solved on first contact.

**$P(S\mid T^c)$** — probability of being solved at first contact, given the ticket is non-technical:

$$P(S\mid T^c) = \frac{P(T^c\cap S)}{P(T^c)} = \frac{160/350}{200/350} = \frac{160}{200} = \boxed{0.80}$$

Among non-technical tickets, 80% are solved on first contact.

---

## Part 5 — Does Ticket Type Change the Probability of Being Solved?

**Yes, significantly.**

| Group | Solved at first contact |
|-------|------------------------|
| Technical tickets | 60% |
| Non-technical tickets | 80% |
| All tickets combined | $250/350 \approx 71.4\%$ |

Technical tickets are solved on first contact at a **lower rate** (60%) than non-technical tickets (80%). Being a technical ticket is associated with a 20 percentage-point decrease in the probability of first-contact resolution.

**Independence check:** If ticket type and resolution were independent, $P(S\mid T) = P(S\mid T^c) = P(S)$.

$$P(S) = 0.7143, \quad P(S\mid T) = 0.60, \quad P(S\mid T^c) = 0.80$$

Since $P(S\mid T) \ne P(S)$, the events $T$ and $S$ are **not independent** — knowing the ticket type changes the probability of first-contact resolution.

**Practical interpretation:** Technical tickets require more specialized knowledge and are harder to resolve immediately. This is consistent with the 20% gap between the two groups.

---

## Summary Table

| Quantity | Value | Meaning |
|----------|-------|---------|
| $P(T\cap S)$ | 0.2571 | Technical AND solved first |
| $P(T\cap S^c)$ | 0.1714 | Technical AND not solved first |
| $P(T^c\cap S)$ | 0.4571 | Non-technical AND solved first |
| $P(T^c\cap S^c)$ | 0.1143 | Non-technical AND not solved first |
| $P(T)$ | 0.4286 | Ticket is technical |
| $P(S)$ | 0.7143 | Solved at first contact |
| $P(T\cup S)$ | 0.8857 | Technical OR solved (or both) |
| $P(T^c\cup S)$ | 0.8286 | Non-technical OR solved (or both) |
| $P(S\mid T)$ | 0.60 | Solved, given technical |
| $P(S\mid T^c)$ | 0.80 | Solved, given non-technical |
| Independent? | **No** | $P(S\mid T) \ne P(S\mid T^c)$ |
