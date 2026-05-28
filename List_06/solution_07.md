# Problem 7 — Conditional probability with three categories

---

## Setup

A company classified 400 customers by activity level and renewal.

| Activity | Renewed ($R$) | Did not renew ($R^c$) | Total |
|---------|---|---|---|
| High ($H$) | 80 | 20 | 100 |
| Medium ($M$) | 90 | 60 | 150 |
| Low ($L$) | 30 | 120 | 150 |
| **Total** | **200** | **200** | **400** |

**Events (subsets of the sample space $\Omega$):**
- $H, M, L \subseteq \Omega$ — high, medium, low activity levels
- $R \subseteq \Omega$ — the customer renewed the subscription

---

## Part 1 — Why $H$, $M$, $L$ Form a Partition

A **partition** of $\Omega$ requires two properties:

**1. Mutually exclusive** (pairwise disjoint sets):
$$H \cap M = \emptyset, \quad H \cap L = \emptyset, \quad M \cap L = \emptyset$$

By the **additivity axiom** of probability, disjoint sets satisfy:
$$P(A \cup B) = P(A) + P(B) \quad \text{whenever } A \cap B = \emptyset$$

So in particular:
$$P(H \cup M) = P(H) + P(M), \quad \text{etc.}$$

**2. Exhaustive** (the union covers the entire sample space):
$$H \cup M \cup L = \Omega$$

Since $P(\Omega) = 1$ and the three sets are pairwise disjoint:
$$P(H \cup M \cup L) = P(H) + P(M) + P(L) = P(\Omega) = 1$$

Both properties hold by construction: each customer belongs to exactly one activity tier.

---

## Part 2 — Marginal Probabilities of Each Activity Level

We assign probabilities from the empirical frequencies. The events $H$, $M$, $L$ are **disjoint**, so their probabilities add. We verify this using the **inclusion–exclusion principle**:

$$P(H \cup M \cup L) = P(H) + P(M) + P(L) - \underbrace{P(H \cap M)}_{=0} - \underbrace{P(H \cap L)}_{=0} - \underbrace{P(M \cap L)}_{=0} + \underbrace{P(H \cap M \cap L)}_{=0}$$

The three intersection terms vanish because the sets are disjoint. This reduces to:

$$P(H \cup M \cup L) = P(H) + P(M) + P(L)$$

Assigning:

$$P(H) = 0.25, \quad P(M) = 0.375, \quad P(L) = 0.375$$

**Check (exhaustiveness):**
$$P(H) + P(M) + P(L) = 0.25 + 0.375 + 0.375 = 1 = P(\Omega) \checkmark$$

---

## Part 3 — Conditional Probabilities (Renewal Rate Within Each Group)

The **definition of conditional probability** for any events $A, B$ with $P(B) > 0$:

$$P(A \mid B) = \frac{P(A \cap B)}{P(B)}$$

This is not a formula derived from counting — it is the **axiomatic definition** that links the probability of the intersection $A \cap B$ to the probability of the conditioning event $B$.

**$P(R \mid H)$:**

We need $P(R \cap H)$ and $P(H)$. The intersection $R \cap H$ is the event "renewed **and** high activity":

$$P(R \mid H) = \frac{P(R \cap H)}{P(H)} = \frac{0.20}{0.25} = \boxed{0.80}$$

*(Here $P(R \cap H) = 80/400 = 0.20$ and $P(H) = 100/400 = 0.25$.)*

**$P(R \mid M)$:**

$$P(R \mid M) = \frac{P(R \cap M)}{P(M)} = \frac{0.225}{0.375} = \boxed{0.60}$$

*(Here $P(R \cap M) = 90/400 = 0.225$.)*

**$P(R \mid L)$:**

$$P(R \mid L) = \frac{P(R \cap L)}{P(L)} = \frac{0.075}{0.375} = \boxed{0.20}$$

*(Here $P(R \cap L) = 30/400 = 0.075$.)*

**Pattern:** Renewal rate drops sharply — 80% (high) → 60% (medium) → 20% (low).

---

## Part 4 — Law of Total Probability

Since $H$, $M$, $L$ partition $\Omega$, the event $R$ can be decomposed into **disjoint pieces**:

$$R = (R \cap H) \cup (R \cap M) \cup (R \cap L)$$

These three pieces are disjoint (because $H, M, L$ are disjoint), so by the **additivity axiom**:

$$P(R) = P(R \cap H) + P(R \cap M) + P(R \cap L)$$

Now apply the **definition of conditional probability** in the form $P(R \cap B) = P(R \mid B) \cdot P(B)$ to each term:

$$\boxed{P(R) = P(R \mid H)\cdot P(H) + P(R \mid M)\cdot P(M) + P(R \mid L)\cdot P(L)}$$

$$P(R) = 0.80 \times 0.25 + 0.60 \times 0.375 + 0.20 \times 0.375$$

$$P(R) = 0.20 + 0.225 + 0.075 = \boxed{0.50}$$

**Note:** This formula is nothing more than applying additivity to disjoint events plus the definition of conditional probability — no counting argument required.

---

## Part 5 — Bayes' Formula

We want $P(H \mid R)$, $P(M \mid R)$, $P(L \mid R)$. Apply the **definition of conditional probability** with the roles reversed:

$$P(H \mid R) = \frac{P(H \cap R)}{P(R)}$$

The numerator is the same intersection as before — $P(H \cap R) = P(R \cap H)$ (intersection is commutative). Apply the definition of conditional probability again in the other direction:

$$P(H \cap R) = P(R \mid H) \cdot P(H)$$

Substituting, and using the Law of Total Probability for $P(R)$ in the denominator:

$$P(H \mid R) = \frac{P(R \mid H)\cdot P(H)}{P(R \mid H)\cdot P(H) + P(R \mid M)\cdot P(M) + P(R \mid L)\cdot P(L)}$$

This is **Bayes' formula** — it follows directly from the definition of conditional probability applied twice, plus additivity.

**Computing each posterior:**

$$P(H \mid R) = \frac{0.80 \times 0.25}{0.50} = \frac{0.20}{0.50} = \boxed{0.40}$$

$$P(M \mid R) = \frac{0.60 \times 0.375}{0.50} = \frac{0.225}{0.50} = \boxed{0.45}$$

$$P(L \mid R) = \frac{0.20 \times 0.375}{0.50} = \frac{0.075}{0.50} = \boxed{0.15}$$

**Check** (the posteriors must sum to 1, since $H, M, L$ partition $\Omega$ and $P(\cdot \mid R)$ is itself a valid probability measure):

$$P(H \mid R) + P(M \mid R) + P(L \mid R) = 0.40 + 0.45 + 0.15 = 1 \checkmark$$

---

## Part 6 — Interpreting $P(R \mid H)$ vs $P(H \mid R)$

Both quantities are defined by the **same formula** — conditional probability — but they condition on different events:

$$P(R \mid H) = \frac{P(R \cap H)}{P(H)} = 0.80 \qquad P(H \mid R) = \frac{P(H \cap R)}{P(R)} = 0.40$$

The numerators are identical ($P(R \cap H) = P(H \cap R) = 0.20$), but the denominators differ — $P(H) = 0.25$ versus $P(R) = 0.50$.

This is why **conditioning is not symmetric**: $P(R \mid H) \ne P(H \mid R)$ in general. The denominator shifts the reference universe from "all customers" to "the subset $H$" or "the subset $R$", respectively.

**$P(R \mid H) = 0.80$** — forward/predictive: the measure is restricted to $H$; within that reduced space, how large is $R$?

**$P(H \mid R) = 0.40$** — retrospective/diagnostic: the measure is restricted to $R$; within that reduced space, how large is $H$?

The asymmetry captures a fundamental fact: knowing the renewal rate of high-activity customers tells you nothing directly about what fraction of renewers are high-activity — you need the base rates $P(H), P(M), P(L)$ as well. That is precisely what Bayes' formula encodes.

---

## Summary

| Quantity | Set-algebra origin | Value |
|----------|-------------------|-------|
| $P(H), P(M), P(L)$ | Additivity + exhaustiveness | 0.25, 0.375, 0.375 |
| $P(R \cap H),\ P(R \cap M),\ P(R \cap L)$ | Direct assignment | 0.20, 0.225, 0.075 |
| $P(R \mid H),\ P(R \mid M),\ P(R \mid L)$ | Definition: $P(A\mid B) = P(A\cap B)/P(B)$ | 0.80, 0.60, 0.20 |
| $P(R)$ | Additivity of disjoint events | **0.50** |
| $P(H\mid R),\ P(M\mid R),\ P(L\mid R)$ | Bayes = definition applied twice | 0.40, 0.45, 0.15 |
