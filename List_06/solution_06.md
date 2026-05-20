# Problem 6 — Dependence from data

---

## Setup

A delivery company recorded data for 600 parcels.

| | Delayed ($D$) | Not delayed ($D^c$) | Total |
|---|---|---|---|
| Domestic ($I^c$) | 24 | 376 | 400 |
| International ($I$) | 36 | 164 | 200 |
| **Total** | **60** | **540** | **600** |

**Events:**
- $I$ = the parcel is international
- $D$ = the parcel is delayed

All probabilities are counts divided by $n = 600$.

---

## Part 1 — Basic Probabilities

$$P(I) = \frac{200}{600} = \boxed{0.3333}$$

$$P(D) = \frac{60}{600} = \boxed{0.10}$$

$$P(I\cap D) = \frac{36}{600} = \boxed{0.06}$$

---

## Part 2 — Conditional Delay Probabilities

**$P(D\mid I)$** — delay rate for international parcels:

$$P(D\mid I) = \frac{P(I\cap D)}{P(I)} = \frac{36/600}{200/600} = \frac{36}{200} = \boxed{0.18}$$

**18%** of international parcels are delayed.

**$P(D\mid I^c)$** — delay rate for domestic parcels:

$$P(D\mid I^c) = \frac{P(I^c\cap D)}{P(I^c)} = \frac{24/600}{400/600} = \frac{24}{400} = \boxed{0.06}$$

Only **6%** of domestic parcels are delayed.

---

## Part 3 — Are $I$ and $D$ Independent?

Check: $P(D\mid I) = P(D)$?

$$P(D) = 0.10, \qquad P(D\mid I) = 0.18$$

$$0.18 \ne 0.10$$

**No, $I$ and $D$ are not independent.**

Equivalently: $P(I\cap D) \ne P(I)\cdot P(D)$:
$$P(I)\cdot P(D) = 0.3333 \times 0.10 = 0.0333 \ne 0.06 = P(I\cap D)$$

The actual overlap is nearly twice the size we would expect under independence.

---

## Part 4 — Does International Shipping Increase Delay Probability?

**Yes, substantially.**

| Parcel type | Delay rate |
|-------------|-----------|
| Domestic | 6% |
| International | 18% |
| Overall | 10% |

International parcels are **3 times more likely** to be delayed than domestic ones ($18\%$ vs $6\%$). The difference is 12 percentage points.

**Reasons this might occur:**
- Customs clearance and border checks add time and uncertainty.
- Greater distance means more handoffs between carriers.
- Weather and logistics disruptions are harder to control across borders.

---

## Part 5 — Reverse Conditional: $P(I\mid D)$

$$P(I\mid D) = \frac{P(I\cap D)}{P(D)} = \frac{36/600}{60/600} = \frac{36}{60} = \boxed{0.60}$$

Among **delayed** parcels, **60%** are international.

---

## Part 6 — Difference Between $P(D\mid I)$ and $P(I\mid D)$

These two probabilities look similar but answer completely different questions:

| Probability | Condition | Question |
|-------------|-----------|----------|
| $P(D\mid I) = 0.18$ | We know the parcel is international | How likely is it to be delayed? |
| $P(I\mid D) = 0.60$ | We know the parcel is delayed | How likely is it to be international? |

**$P(D\mid I) = 0.18$** is a **forward-looking risk assessment**: "Given this parcel is international, what is its delay risk?" Useful for setting customer expectations and pricing.

**$P(I\mid D) = 0.60$** is a **backward-looking diagnostic**: "Given we observe a delay, what type of parcel is it most likely to be?" Useful for investigating the root cause of delays.

**Why they differ so dramatically (0.18 vs 0.60):**

The key is the **base rate**: only $\frac{1}{3}$ of all parcels are international, but international parcels have 3× the delay rate. When a delay does occur, it is disproportionately drawn from the international pool — even though international parcels are less common overall. This is the same logic as Bayes' theorem: a rarer group can dominate a conditional probability if its per-group rate is high enough.

---

## Summary

| Quantity | Value |
|----------|-------|
| $P(I)$ | 0.333 |
| $P(D)$ | 0.100 |
| $P(I\cap D)$ | 0.060 |
| $P(D\mid I)$ | 0.180 |
| $P(D\mid I^c)$ | 0.060 |
| $P(I\mid D)$ | 0.600 |
| Independent? | **No** — delay rate 3× higher for international |
| International increases delay? | **Yes** — from 6% to 18% |
