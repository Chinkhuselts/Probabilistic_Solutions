# Problem 10 — Comprehensive problem: event algebra, conditioning, independence, and Bayes

---

## Setup

A company studied whether 500 users completed an online onboarding process.

| | Completed ($C$) | Did not complete ($C^c$) | Total |
|---|---|---|---|
| Received tutorial ($T$) | 180 | 70 | 250 |
| No tutorial ($T^c$) | 120 | 130 | 250 |
| **Total** | **300** | **200** | **500** |

**Events:**
- $T$ = the user received the tutorial
- $C$ = the user completed onboarding

---

## Part 1 — The Four Disjoint Regions

$$P(T\cap C) = \frac{180}{500} = \boxed{0.36}$$
> Received tutorial AND completed onboarding.

$$P(T\cap C^c) = \frac{70}{500} = \boxed{0.14}$$
> Received tutorial AND did NOT complete onboarding.

$$P(T^c\cap C) = \frac{120}{500} = \boxed{0.24}$$
> No tutorial AND completed onboarding.

$$P(T^c\cap C^c) = \frac{130}{500} = \boxed{0.26}$$
> No tutorial AND did NOT complete onboarding.

**Sanity check:** $0.36 + 0.14 + 0.24 + 0.26 = 1.00$ ✓

---

## Part 2 — Marginal and Union Probabilities

**$P(T)$** — proportion who received the tutorial:
$$P(T) = P(T\cap C) + P(T\cap C^c) = 0.36 + 0.14 = \boxed{0.50}$$

Half the users received the tutorial — the two groups are equally sized.

**$P(C)$** — overall completion rate:
$$P(C) = P(T\cap C) + P(T^c\cap C) = 0.36 + 0.24 = \boxed{0.60}$$

Overall, 60% of users completed onboarding.

**$P(T\cup C)$** — received tutorial OR completed onboarding (or both):
$$P(T\cup C) = P(T) + P(C) - P(T\cap C) = 0.50 + 0.60 - 0.36 = \boxed{0.74}$$

The only group excluded: users who received no tutorial AND did not complete — $P(T^c\cap C^c) = 0.26$.

Check: $1 - 0.26 = 0.74$ ✓

---

## Part 3 — Conditional Completion Rates

**$P(C\mid T)$** — completion rate among users who received the tutorial:

$$P(C\mid T) = \frac{P(T\cap C)}{P(T)} = \frac{180}{250} = \boxed{0.72}$$

**72%** of tutorial users completed onboarding.

**$P(C\mid T^c)$** — completion rate among users who did NOT receive the tutorial:

$$P(C\mid T^c) = \frac{P(T^c\cap C)}{P(T^c)} = \frac{120}{250} = \boxed{0.48}$$

**48%** of non-tutorial users completed onboarding.

---

## Part 4 — Reverse Conditionals: Profile of Completers

**$P(T\mid C)$** — probability of having received the tutorial, given the user completed:

$$P(T\mid C) = \frac{P(T\cap C)}{P(C)} = \frac{180}{300} = \boxed{0.60}$$

Among all users who completed onboarding, **60%** had received the tutorial.

**$P(T\mid C^c)$** — probability of having received the tutorial, given the user did NOT complete:

$$P(T\mid C^c) = \frac{P(T\cap C^c)}{P(C^c)} = \frac{70}{200} = \boxed{0.35}$$

Among all users who did not complete onboarding, only **35%** had received the tutorial.

---

## Part 5 — Are $T$ and $C$ Independent?

Check: $P(T\cap C) = P(T)\cdot P(C)$?

$$P(T)\cdot P(C) = 0.50\times 0.60 = 0.30$$

$$P(T\cap C) = 0.36 \ne 0.30$$

**No, $T$ and $C$ are not independent.**

Alternatively: $P(C\mid T) = P(C)$?

$$P(C\mid T) = 0.72 \ne 0.60 = P(C)$$

Knowing a user received the tutorial increases the completion probability from 60% to 72%. The tutorial and completion are positively associated — they are **dependent**.

---

## Part 6 — Does the Tutorial Appear to Help?

**Yes, clearly.**

| Group | Completion rate |
|-------|----------------|
| Received tutorial | **72%** |
| No tutorial | **48%** |
| All users | **60%** |

The tutorial is associated with a **24 percentage-point increase** in completion rate. This is a substantial gap — tutorial users complete at 1.5 times the rate of non-tutorial users ($72\% / 48\% = 1.5$).

**Caution about causation:** This is observational data. Users who received the tutorial may differ in other ways (e.g., more motivated). A controlled experiment (randomizing who gets the tutorial) would be needed to establish that the tutorial *causes* higher completion.

---

## Part 7 — Difference Between $P(C\mid T)$ and $P(T\mid C)$

| Probability | Value | Question answered |
|-------------|-------|------------------|
| $P(C\mid T)$ | 0.72 | Given user has tutorial: how likely to complete? |
| $P(T\mid C)$ | 0.60 | Given user completed: how likely they had tutorial? |

**$P(C\mid T) = 0.72$** is a **forward prediction**: Given we know a user received the tutorial, what are their chances of completing? This is the question a product manager asks before launch: "If we give users the tutorial, what fraction will complete?"

**$P(T\mid C) = 0.60$** is a **backward description**: After observing that a user completed, what fraction had used the tutorial? This is what an analyst asks when reviewing data: "Of our successful users, who had the tutorial?"

**Why they differ:**

Both share the same numerator: $P(T\cap C) = 0.36$. But:
- $P(C\mid T)$ divides by $P(T) = 0.50$ — the proportion with tutorial.
- $P(T\mid C)$ divides by $P(C) = 0.60$ — the proportion who completed.

Since $P(C) > P(T)$ here ($0.60 > 0.50$), dividing by the smaller number $P(T)$ gives the larger result: $P(C\mid T) = 0.72 > 0.60 = P(T\mid C)$.

**Bayes' theorem connects them directly:**

$$P(T\mid C) = \frac{P(C\mid T)\cdot P(T)}{P(C)} = \frac{0.72\times 0.50}{0.60} = \frac{0.36}{0.60} = 0.60 \checkmark$$

---

## Part 8 — Short Interpretation in Words

> "The tutorial appears to substantially help users complete the onboarding process. Among users who received the tutorial, 72% completed — compared to only 48% among those who did not. This 24-point gap suggests the tutorial is effective. Viewed from the other direction, 60% of those who successfully completed onboarding had received the tutorial, while only 35% of non-completers had received it — showing that tutorial users are overrepresented among completers and underrepresented among non-completers."

---

## Summary Table

| Quantity | Value |
|----------|-------|
| $P(T\cap C)$ | 0.36 |
| $P(T\cap C^c)$ | 0.14 |
| $P(T^c\cap C)$ | 0.24 |
| $P(T^c\cap C^c)$ | 0.26 |
| $P(T)$ | 0.50 |
| $P(C)$ | 0.60 |
| $P(T\cup C)$ | 0.74 |
| $P(C\mid T)$ | **0.72** — completion rate with tutorial |
| $P(C\mid T^c)$ | **0.48** — completion rate without tutorial |
| $P(T\mid C)$ | **0.60** — tutorial rate among completers |
| $P(T\mid C^c)$ | **0.35** — tutorial rate among non-completers |
| Independent? | **No** — $P(C\mid T) = 0.72 \ne 0.60 = P(C)$ |
| Tutorial helps? | **Yes** — +24 percentage points |
