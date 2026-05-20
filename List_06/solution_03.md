# Problem 3 — Conditional probabilities are not symmetric

---

## Setup

An online course platform recorded data for 150 users.

| | Passed quiz ($Q$) | Did not pass ($Q^c$) | Total |
|---|---|---|---|
| Watched lecture ($W$) | 72 | 18 | 90 |
| Did not watch ($W^c$) | 28 | 32 | 60 |
| **Total** | **100** | **50** | **150** |

**Events:**
- $W$ = the user watched the lecture
- $Q$ = the user passed the quiz

All probabilities are counts divided by $n = 150$.

---

## Part 1 — Conditional Probabilities Given Watching

**$P(Q\mid W)$** — probability of passing the quiz, given the user watched the lecture:

$$P(Q\mid W) = \frac{P(W\cap Q)}{P(W)} = \frac{72/150}{90/150} = \frac{72}{90} = \boxed{0.80}$$

Among users who watched the lecture, **80%** passed the quiz.

**$P(W\mid Q)$** — probability of having watched the lecture, given the user passed the quiz:

$$P(W\mid Q) = \frac{P(W\cap Q)}{P(Q)} = \frac{72/150}{100/150} = \frac{72}{100} = \boxed{0.72}$$

Among users who passed the quiz, **72%** had watched the lecture.

---

## Part 2 — Conditional Probabilities Given Not Watching

**$P(Q\mid W^c)$** — probability of passing the quiz, given the user did NOT watch the lecture:

$$P(Q\mid W^c) = \frac{P(W^c\cap Q)}{P(W^c)} = \frac{28/150}{60/150} = \frac{28}{60} = \boxed{0.4\overline{6} \approx 46.7\%}$$

Among users who did not watch the lecture, only **46.7%** passed.

**$P(W\mid Q^c)$** — probability of having watched the lecture, given the user did NOT pass:

$$P(W\mid Q^c) = \frac{P(W\cap Q^c)}{P(Q^c)} = \frac{18/150}{50/150} = \frac{18}{50} = \boxed{0.36}$$

Among users who failed the quiz, **36%** had still watched the lecture.

---

## Part 3 — Why $P(Q\mid W)$ and $P(W\mid Q)$ Answer Different Questions

Although both probabilities involve the same two events $W$ and $Q$, they condition on **different known facts** and answer fundamentally different questions:

| Probability | Known fact | Question asked |
|-------------|-----------|----------------|
| $P(Q\mid W)$ | User watched the lecture | How likely is it that they pass? |
| $P(W\mid Q)$ | User passed the quiz | How likely is it that they watched? |

**$P(Q\mid W) = 0.80$** looks forward from behavior to outcome: "If we know a user watched, what are their chances of passing?"

**$P(W\mid Q) = 0.72$** looks backward from outcome to cause: "Among those who succeeded, how many did the preparatory work?"

These are not interchangeable. Confusing them is called the **base-rate neglect** or more formally, **the confusion of the inverse** — a common error in medical diagnosis, legal reasoning, and data science.

**Numerical demonstration of asymmetry:**

$$P(Q\mid W) = 0.80 \ne 0.72 = P(W\mid Q)$$

The difference arises because the denominators are different: $P(W) = 90/150 = 0.60$ while $P(Q) = 100/150 = 0.667$. The two conditional probabilities share the same numerator $P(W\cap Q) = 0.48$, but divide it by different things.

---

## Part 4 — Which Probability Tells Us Whether Watching Helps?

**$P(Q\mid W)$ and $P(Q\mid W^c)$ together** are the most useful.

We compare:
$$P(Q\mid W) = 0.80 \quad \text{vs} \quad P(Q\mid W^c) = 0.467$$

The question "does watching the lecture help?" asks: **does watching change the probability of passing?**

- Watchers pass at 80%.
- Non-watchers pass at only 46.7%.
- The gap is $0.80 - 0.467 = 0.333$ — a 33 percentage-point difference.

This strongly suggests that watching the lecture is associated with better quiz performance.

> Note: This is correlation/association, not necessarily causation. Students who choose to watch may also be more motivated, which could explain part of the gap.

---

## Part 5 — Which Probability Describes Users Who Passed?

**$P(W\mid Q) = 0.72$** is most useful here.

This describes the **profile of successful users**: among those who passed the quiz, 72% had watched the lecture, while 28% passed without watching.

This is useful for:
- Identifying common traits of successful learners.
- Understanding whether the platform's content is being used by those who succeed.
- Calculating "what fraction of our top performers used the lecture feature?"

---

## All Four Conditional Probabilities — Summary

| Probability | Value | Question answered |
|-------------|-------|------------------|
| $P(Q\mid W)$ | **0.800** | If watched: chance of passing? |
| $P(Q\mid W^c)$ | **0.467** | If didn't watch: chance of passing? |
| $P(W\mid Q)$ | **0.720** | If passed: chance they watched? |
| $P(W\mid Q^c)$ | **0.360** | If failed: chance they watched? |

**Key pattern:** Users who watched are more likely to pass ($0.80$ vs $0.467$), and users who passed are more likely to have watched ($0.72$ vs $0.36$ for non-passers). Both perspectives are consistent with a positive association between watching and passing.
