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

**Events:**
- $H, M, L$ = high, medium, low activity levels
- $R$ = the customer renewed the subscription

---

## Part 1 — Why $H$, $M$, $L$ Form a Partition

A **partition** of the sample space requires two properties:

1. **Mutually exclusive:** The events cannot overlap — no customer can have two activity levels simultaneously.
   $$H\cap M = \emptyset, \quad H\cap L = \emptyset, \quad M\cap L = \emptyset$$

2. **Exhaustive:** The events cover the entire sample space — every customer has exactly one activity level.
   $$H\cup M\cup L = \Omega, \quad \text{i.e., } P(H)+P(M)+P(L) = 1$$

Both properties hold by construction: each customer is assigned to exactly one of three activity tiers. Partitions are the foundation for the Law of Total Probability.

---

## Part 2 — Marginal Probabilities of Each Activity Level

$$P(H) = \frac{100}{400} = \boxed{0.25}$$

$$P(M) = \frac{150}{400} = \boxed{0.375}$$

$$P(L) = \frac{150}{400} = \boxed{0.375}$$

**Check:** $0.25 + 0.375 + 0.375 = 1.00$ ✓

---

## Part 3 — Renewal Rate Within Each Activity Level

**$P(R\mid H)$** — renewal rate among high-activity customers:

$$P(R\mid H) = \frac{80}{100} = \boxed{0.80}$$

**$P(R\mid M)$** — renewal rate among medium-activity customers:

$$P(R\mid M) = \frac{90}{150} = \boxed{0.60}$$

**$P(R\mid L)$** — renewal rate among low-activity customers:

$$P(R\mid L) = \frac{30}{150} = \boxed{0.20}$$

**Pattern:** Renewal rate drops sharply with activity level — from 80% (high) to 60% (medium) to just 20% (low). Activity level is a strong predictor of renewal.

---

## Part 4 — Law of Total Probability

Since $H$, $M$, $L$ partition the sample space, the overall renewal probability is the weighted average of the conditional renewal rates:

$$P(R) = P(R\mid H)\cdot P(H) + P(R\mid M)\cdot P(M) + P(R\mid L)\cdot P(L)$$

$$P(R) = 0.80\times 0.25 + 0.60\times 0.375 + 0.20\times 0.375$$

$$P(R) = 0.20 + 0.225 + 0.075 = \boxed{0.50}$$

**Verification from the table:** $\frac{200}{400} = 0.50$ ✓

The law of total probability is powerful when you know conditional rates within subgroups but not the overall rate directly. The overall rate is the weighted sum, where weights are the group sizes.

---

## Part 5 — Bayes' Formula: Who Are the Renewers?

Given that a customer renewed, what is the probability they came from each activity group? These are computed using Bayes' formula:

$$P(H\mid R) = \frac{P(R\mid H)\cdot P(H)}{P(R)} = \frac{0.80\times 0.25}{0.50} = \frac{0.20}{0.50} = \boxed{0.40}$$

$$P(M\mid R) = \frac{P(R\mid M)\cdot P(M)}{P(R)} = \frac{0.60\times 0.375}{0.50} = \frac{0.225}{0.50} = \boxed{0.45}$$

$$P(L\mid R) = \frac{P(R\mid L)\cdot P(L)}{P(R)} = \frac{0.20\times 0.375}{0.50} = \frac{0.075}{0.50} = \boxed{0.15}$$

**Check:** $0.40 + 0.45 + 0.15 = 1.00$ ✓

**Composition of renewers:**

| Activity group | Share of all customers | Share of renewers |
|----------------|------------------------|-------------------|
| High | 25% | 40% |
| Medium | 37.5% | 45% |
| Low | 37.5% | 15% |

High-activity customers make up only 25% of the total customer base but **40%** of all renewers — they are overrepresented among renewers. Low-activity customers make up 37.5% of the base but only **15%** of renewers — severely underrepresented.

---

## Part 6 — Interpreting $P(R\mid H)$ vs $P(H\mid R)$

| Probability | Value | Question answered |
|-------------|-------|------------------|
| $P(R\mid H)$ | 0.80 | Given a customer is high-activity: how likely to renew? |
| $P(H\mid R)$ | 0.40 | Given a customer renewed: how likely they were high-activity? |

**$P(R\mid H) = 0.80$** is a **prediction**: Looking at a specific high-activity customer, what is their renewal probability? This is forward-looking — used before the renewal decision is made. It tells the sales team how to target customers.

**$P(H\mid R) = 0.40$** is a **retrospective description**: After observing that a customer renewed, what was their likely profile? This is backward-looking — used after the fact. It tells the analytics team what their renewed customers look like.

**Why are they different?**

$P(R\mid H) = 0.80$ is large partly because high-activity customers have a strong tendency to renew. But $P(H\mid R) = 0.40$ also depends on how many high-activity customers there are in total (only 25% of the base). The medium group has a lower renewal rate (60%) but is larger (37.5% of customers), so it contributes even more renewers in total ($45\%$ of renewers).

This is a concrete example of **Bayes' theorem in practice**: both the conditional rate and the base rate jointly determine the posterior probability.

---

## Summary

| Quantity | Value |
|----------|-------|
| $P(H), P(M), P(L)$ | 0.25, 0.375, 0.375 |
| $P(R\mid H)$ | 0.80 |
| $P(R\mid M)$ | 0.60 |
| $P(R\mid L)$ | 0.20 |
| $P(R)$ (total probability) | **0.50** |
| $P(H\mid R)$ | 0.40 |
| $P(M\mid R)$ | 0.45 |
| $P(L\mid R)$ | 0.15 |
