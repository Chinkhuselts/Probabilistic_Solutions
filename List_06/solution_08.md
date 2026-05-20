# Problem 8 — Bayes' formula from a table

---

## Setup

A fraud detection system classified 10,000 transactions.

| | Marked suspicious ($S$) | Not marked suspicious ($S^c$) | Total |
|---|---|---|---|
| Fraudulent ($F$) | 98 | 2 | 100 |
| Legitimate ($F^c$) | 297 | 9,603 | 9,900 |
| **Total** | **395** | **9,605** | **10,000** |

**Events:**
- $F$ = the transaction is fraudulent
- $S$ = the transaction is marked suspicious by the system

---

## Part 1 — Base Rate and Detection Rate

**$P(F)$** — base rate of fraud (prior probability):
$$P(F) = \frac{100}{10{,}000} = \boxed{0.01}$$

Only 1% of all transactions are fraudulent. This is the **base rate** — before seeing any flag, a random transaction has a 1% chance of being fraud.

**$P(S\mid F)$** — sensitivity: how well does the system detect fraud?
$$P(S\mid F) = \frac{98}{100} = \boxed{0.98}$$

The system flags 98% of fraudulent transactions. This is the **true positive rate** (sensitivity).

**$P(S\mid F^c)$** — false alarm rate: how often does the system flag legitimate transactions?
$$P(S\mid F^c) = \frac{297}{9{,}900} = \boxed{0.03}$$

The system flags 3% of legitimate transactions. This is the **false positive rate**.

---

## Part 2 — Law of Total Probability: $P(S)$

Since $F$ and $F^c$ partition the sample space:

$$P(S) = P(S\mid F)\cdot P(F) + P(S\mid F^c)\cdot P(F^c)$$

$$P(S) = 0.98\times 0.01 + 0.03\times 0.99$$

$$P(S) = 0.0098 + 0.0297 = \boxed{0.0395}$$

**Verification from table:** $\frac{395}{10{,}000} = 0.0395$ ✓

About 3.95% of all transactions are flagged as suspicious.

**Breakdown of the 395 suspicious flags:**
- 98 are truly fraudulent (true positives)
- 297 are legitimate but flagged (false positives)

---

## Part 3 — Bayes' Formula: $P(F\mid S)$

Given that a transaction is flagged suspicious, what is the probability it is actually fraudulent?

$$P(F\mid S) = \frac{P(S\mid F)\cdot P(F)}{P(S)} = \frac{0.98\times 0.01}{0.0395} = \frac{0.0098}{0.0395} = \boxed{0.2481 \approx 24.8\%}$$

Despite the system detecting 98% of fraud, a flagged transaction has only about a **1 in 4 chance** of being genuinely fraudulent.

---

## Part 4 — Among Suspicious Transactions, Are Most Fraudulent or Legitimate?

**Most are legitimate.**

| Among the 395 flagged transactions: | Count | Proportion |
|------------------------------------|-------|-----------|
| Truly fraudulent (true positives) | 98 | 24.8% |
| Legitimate but flagged (false positives) | 297 | 75.2% |

Despite the system's high sensitivity, about **3 out of 4 flagged transactions are actually legitimate**.

---

## Part 5 — Why Does This Happen Even With a Good System?

This counterintuitive result is caused by the **low base rate** of fraud ($P(F) = 1\%$).

**Intuitive explanation:**

Imagine examining 10,000 transactions:
- 100 are fraudulent → the system correctly catches 98 of them.
- 9,900 are legitimate → even with only a 3% false-alarm rate, the system incorrectly flags $9{,}900\times 0.03 = 297$ of them.

The pool of legitimate transactions (9,900) is so much larger than the pool of fraudulent ones (100) that even a small false-alarm rate (3%) generates far more false positives (297) than there are true positives (98).

This phenomenon is known as the **base-rate fallacy** or the **paradox of the false positive**. It is a fundamental challenge in any rare-event detection problem: medical screening, spam filtering, intrusion detection, and lie detection all suffer from the same effect.

---

## Part 6 — The Role of the Base Rate $P(F)$

The base rate $P(F) = 0.01$ is the **prior probability** — what we believe about fraud before seeing any flag. Bayes' formula updates this belief:

$$P(F\mid S) = \frac{P(S\mid F)}{P(S)} \cdot P(F)$$

The factor $\frac{P(S\mid F)}{P(S)} = \frac{0.98}{0.0395} \approx 24.8$ is the **Bayes factor** — it tells us how much the flag updates our belief. The posterior ($\approx 24.8\%$) is about 24.8 times the prior ($1\%$).

**What happens if the base rate changes?**

| Base rate $P(F)$ | $P(F\mid S)$ (approx.) |
|-----------------|------------------------|
| 0.001 (0.1%) | ≈ 3.2% |
| 0.01 (1%) | ≈ 24.8% |
| 0.05 (5%) | ≈ 63.2% |
| 0.10 (10%) | ≈ 78.5% |

The lower the base rate, the less a positive flag means — the system needs to be even more precise to be useful. This is why fraud detection in populations with very low fraud rates is so difficult.

**Key lesson:** A test's usefulness depends on **both** its accuracy (sensitivity, false-alarm rate) **and** the prevalence of what it is testing for.

---

## Summary

| Quantity | Value | Meaning |
|----------|-------|---------|
| $P(F)$ | 0.010 | Base rate of fraud |
| $P(S\mid F)$ | 0.980 | System catches 98% of fraud |
| $P(S\mid F^c)$ | 0.030 | 3% false alarm rate |
| $P(S)$ | 0.0395 | Overall flagging rate |
| $P(F\mid S)$ | **0.248** | Probability fraud given flag |
| $P(F^c\mid S)$ | **0.752** | Probability legitimate given flag |
| Majority of flags | **Legitimate** | Base rate effect |
