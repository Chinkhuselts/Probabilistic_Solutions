# Problem 9 — Law of total probability without a full table

---

## Setup

A company receives orders through three channels with the following data:

| Channel | Proportion of orders | Cancellation rate |
|---------|---------------------|------------------|
| Website ($W$) | $P(W) = 0.50$ | $P(C\mid W) = 0.04$ |
| Mobile app ($A$) | $P(A) = 0.35$ | $P(C\mid A) = 0.06$ |
| Phone ($H$) | $P(H) = 0.15$ | $P(C\mid H) = 0.10$ |

**Events:**
- $W, A, H$ = order channel (website, app, phone)
- $C$ = the order is cancelled

Unlike previous problems, we are not given a full table — only marginal and conditional probabilities. The Law of Total Probability and Bayes' formula let us work entirely from these.

---

## Part 1 — Why $W$, $A$, $H$ Form a Partition

Three requirements:

1. **Mutually exclusive:** Each order comes through exactly one channel — impossible for an order to arrive via both website and phone simultaneously.

2. **Exhaustive:** Every order comes through one of the three listed channels — no other channels exist.

3. **Probabilities sum to 1:**
$$P(W) + P(A) + P(H) = 0.50 + 0.35 + 0.15 = 1.00 \checkmark$$

Because $W$, $A$, $H$ form a partition, we can apply the Law of Total Probability.

---

## Part 2 — Total Probability of Cancellation

The Law of Total Probability states: for any partition $\{W, A, H\}$ of $\Omega$,

$$P(C) = P(C\mid W)\cdot P(W) + P(C\mid A)\cdot P(A) + P(C\mid H)\cdot P(H)$$

**Computation:**

| Channel | Cancellation rate | Channel share | Contribution |
|---------|------------------|---------------|-------------|
| Website | 0.04 | 0.50 | $0.04\times 0.50 = 0.0200$ |
| Mobile app | 0.06 | 0.35 | $0.06\times 0.35 = 0.0210$ |
| Phone | 0.10 | 0.15 | $0.10\times 0.15 = 0.0150$ |
| **Total** | | | $\mathbf{P(C) = 0.0560}$ |

$$\boxed{P(C) = 0.0560}$$

On average, **5.6%** of all orders are cancelled.

**Interpretation of the three contributions:**
- Website orders (large volume, low rate) contribute 0.020 — the biggest absolute contribution despite the lowest cancellation rate, simply because the website handles the most orders.
- App orders (moderate volume, moderate rate) contribute 0.021 — very close to the website.
- Phone orders (small volume, high rate) contribute only 0.015 — their high cancellation rate is offset by their small share.

---

## Part 3 — Bayes' Formula: Source of Cancelled Orders

Given an order is cancelled, what is the probability it came from each channel?

$$P(W\mid C) = \frac{P(C\mid W)\cdot P(W)}{P(C)} = \frac{0.0200}{0.0560} = \boxed{0.3571 \approx 35.7\%}$$

$$P(A\mid C) = \frac{P(C\mid A)\cdot P(A)}{P(C)} = \frac{0.0210}{0.0560} = \boxed{0.3750 = 37.5\%}$$

$$P(H\mid C) = \frac{P(C\mid H)\cdot P(H)}{P(C)} = \frac{0.0150}{0.0560} = \boxed{0.2679 \approx 26.8\%}$$

**Check:** $0.3571 + 0.3750 + 0.2679 = 1.00$ ✓

**Summary table:**

| Channel | Share of all orders | Share of cancelled orders |
|---------|--------------------|-----------------------------|
| Website | 50.0% | 35.7% |
| Mobile app | 35.0% | 37.5% |
| Phone | 15.0% | 26.8% |

---

## Part 4 — Which Channel Is Most Likely Among Cancelled Orders?

**The mobile app** ($P(A\mid C) = 37.5\%$) is the most common source of cancelled orders, despite having neither the largest volume (website does) nor the highest cancellation rate (phone does).

The app achieves the highest share of cancellations because its moderate volume (35%) and moderate cancellation rate (6%) combine to produce the largest contribution: $0.06\times 0.35 = 0.021$.

---

## Part 5 — Is the Most Common Source Necessarily the Highest-Cancellation Channel?

**No.** These are two different questions answered by two different probabilities:

| Question | Probability | Answer |
|----------|------------|--------|
| Which channel has the highest cancellation rate? | $P(C\mid H) = 0.10$ | **Phone** |
| Among cancelled orders, which channel is most represented? | $P(H\mid C) = 0.268$ | **App** wins |

**Why the discrepancy?**

$P(C\mid H) = 0.10$ is the cancellation rate for phone orders — 10 out of every 100 phone orders cancel. But phone orders make up only 15% of all orders. So in absolute terms, phone contributes $0.10\times 0.15 = 0.015$ to the cancellation pool.

$P(C\mid A) = 0.06$ is a lower rate, but app orders make up 35% of all orders. In absolute terms, the app contributes $0.06\times 0.35 = 0.021$ — more than phone despite its lower rate.

**Key insight:** Having the highest per-channel cancellation rate does not mean a channel dominates the total pool of cancellations. The channel's **volume** matters just as much as its **rate**.

This is why Bayes' theorem is essential: $P(H\mid C) \ne P(C\mid H)$. Confusing these two leads to incorrect conclusions about where to focus cancellation-reduction efforts.

---

## Summary

| Quantity | Value |
|----------|-------|
| $P(W)$, $P(A)$, $P(H)$ | 0.50, 0.35, 0.15 |
| $P(C\mid W)$, $P(C\mid A)$, $P(C\mid H)$ | 0.04, 0.06, 0.10 |
| $P(C)$ (total probability) | **0.056** |
| $P(W\mid C)$ | 0.357 |
| $P(A\mid C)$ | **0.375** (highest) |
| $P(H\mid C)$ | 0.268 |
| Highest cancellation rate | Phone ($10\%$) |
| Most cancellations sourced from | App ($37.5\%$ of pool) |
