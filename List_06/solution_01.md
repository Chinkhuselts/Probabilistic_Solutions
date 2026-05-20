# Problem 1 — Event algebra from a two-way table

---

## Setup

A university collected data on 100 students' study habits.

| | Submits on time ($B$) | Does not submit ($B^c$) | Total |
|---|---|---|---|
| Attends regularly ($A$) | 48 | 12 | 60 |
| Does not attend ($A^c$) | 22 | 18 | 40 |
| **Total** | **70** | **30** | **100** |

**Events:**
- $A$ = the student attends lectures regularly
- $B$ = the student submits homework on time

Since there are 100 students, dividing each cell by 100 converts counts into probabilities.

---

## Part 1 — The Four Disjoint Regions

Every student belongs to exactly one of four regions. Together these four regions cover the entire sample space and do not overlap.

$$A\cap B: \quad \frac{48}{100} = \boxed{0.48}$$

> Attends regularly AND submits on time.

$$A\cap B^c: \quad \frac{12}{100} = \boxed{0.12}$$

> Attends regularly AND does NOT submit on time.

$$A^c\cap B: \quad \frac{22}{100} = \boxed{0.22}$$

> Does NOT attend regularly AND submits on time.

$$A^c\cap B^c: \quad \frac{18}{100} = \boxed{0.18}$$

> Does NOT attend regularly AND does NOT submit on time.

**Sanity check:** $0.48 + 0.12 + 0.22 + 0.18 = 1.00$ ✓

---

## Part 2 — Marginal Probabilities and Union

**$P(A)$** — probability a student attends regularly:
$$P(A) = P(A\cap B) + P(A\cap B^c) = 0.48 + 0.12 = \boxed{0.60}$$

**$P(B)$** — probability a student submits on time:
$$P(B) = P(A\cap B) + P(A^c\cap B) = 0.48 + 0.22 = \boxed{0.70}$$

**$P(A\cup B)$** — probability a student attends regularly OR submits on time (or both):

Using **inclusion–exclusion**:
$$P(A\cup B) = P(A) + P(B) - P(A\cap B) = 0.60 + 0.70 - 0.48 = \boxed{0.82}$$

Or equivalently, by summing the three relevant regions:
$$P(A\cup B) = P(A\cap B) + P(A\cap B^c) + P(A^c\cap B) = 0.48 + 0.12 + 0.22 = 0.82 \checkmark$$

The only region excluded from $A\cup B$ is $A^c\cap B^c = 0.18$ — students who neither attend nor submit on time. Check: $1 - 0.18 = 0.82$ ✓

---

## Part 3 — Conditional Probabilities

**$P(A\mid B)$** — probability that a student attends regularly, *given* they submit on time:

$$P(A\mid B) = \frac{P(A\cap B)}{P(B)} = \frac{0.48}{0.70} = \boxed{0.6857 \approx 68.6\%}$$

**$P(B\mid A)$** — probability that a student submits on time, *given* they attend regularly:

$$P(B\mid A) = \frac{P(A\cap B)}{P(A)} = \frac{0.48}{0.60} = \boxed{0.80}$$

---

## Part 4 — Are $A$ and $B$ Mutually Exclusive?

**No.** Two events are mutually exclusive if they cannot happen at the same time — i.e., $P(A\cap B) = 0$.

Here, $P(A\cap B) = 0.48 \ne 0$. In fact, 48 students both attend regularly and submit on time. Being a regular attender is perfectly compatible with submitting homework on time.

---

## Part 5 — Are $A$ and $B$ Independent?

Two events are **independent** if $P(A\cap B) = P(A)\cdot P(B)$.

$$P(A)\cdot P(B) = 0.60 \times 0.70 = 0.42$$

$$P(A\cap B) = 0.48 \ne 0.42$$

**No, $A$ and $B$ are not independent.**

Alternatively, check via conditional probability: if $A$ and $B$ were independent, $P(B\mid A)$ would equal $P(B)$.

$$P(B\mid A) = 0.80 \ne 0.70 = P(B)$$

Knowing a student attends regularly raises the probability of submitting on time from 70% to 80%. There is a positive association between the two behaviors.

---

## Part 6 — Interpretation in Words

**$P(A\mid B) = 0.686$:**

> "Among all students who submit homework on time, approximately 68.6% also attend lectures regularly."

This is a question about the **composition of on-time submitters** — given we already know someone is on time, what fraction are also regular attenders?

**$P(B\mid A) = 0.80$:**

> "Among all students who attend lectures regularly, 80% submit homework on time."

This is a question about the **behavior of regular attenders** — given we already know someone attends regularly, how likely are they to submit on time?

**Key insight:** These two conditional probabilities ask fundamentally different questions even though they use the same two events. $P(A\mid B)$ looks at the submitters and asks about attendance; $P(B\mid A)$ looks at the attenders and asks about submission.

---

## Summary Table

| Quantity | Value | Interpretation |
|----------|-------|----------------|
| $P(A\cap B)$ | 0.48 | Attend AND submit on time |
| $P(A\cap B^c)$ | 0.12 | Attend AND do not submit |
| $P(A^c\cap B)$ | 0.22 | Do not attend AND submit on time |
| $P(A^c\cap B^c)$ | 0.18 | Do not attend AND do not submit |
| $P(A)$ | 0.60 | Attend regularly |
| $P(B)$ | 0.70 | Submit on time |
| $P(A\cup B)$ | 0.82 | Attend OR submit (or both) |
| $P(A\mid B)$ | 0.686 | Attend, given submitted on time |
| $P(B\mid A)$ | 0.80 | Submit on time, given attend |
| Mutually exclusive? | No | $P(A\cap B) = 0.48 \ne 0$ |
| Independent? | No | $P(B\mid A)=0.80 \ne 0.70=P(B)$ |
