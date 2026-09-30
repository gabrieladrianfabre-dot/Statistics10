# Measures of Position (Simplified)

> About this note:
> A simpler, Grade 10-level version of [[Measures of Position (FULL VERSION)]]. It covers only the basics: quartiles, deciles, and percentiles for ungrouped data.

## What is a measure of position?

A **measure of position** tells you **where a value stands compared to the rest of the data**.

Say you scored 36 on a quiz. Is that good? It depends on how everyone else did. If most of the class scored below 36, you did well. If most scored above, not so much. Measures of position give you a way to answer that question with numbers.

The idea is simple:

1. **Arrange the data from smallest to largest.**
2. **Cut it into equal parts.**

How many parts you cut it into gives each measure its name:

| Name | Cuts the data into | Number of cut points | Written as |
|---|---|---|---|
| **Quartiles** | 4 equal parts | 3 | $Q_1, Q_2, Q_3$ |
| **Deciles** | 10 equal parts | 9 | $D_1, D_2, \dots, D_9$ |
| **Percentiles** | 100 equal parts | 99 | $P_1, P_2, \dots, P_{99}$ |

Think of cutting a cake. Quartiles cut it into 4 slices, deciles into 10, and percentiles into 100. Same cake, just thinner slices.

## Before you start: two things to remember

1. **Always sort the data first**, from smallest to largest. If you skip this, every answer will be wrong.
2. **Position is not the same as value.** "The 4th number in the list" is a *position*. "30" is a *value*. The formulas below first tell you the **position**, and then you look up the **value** at that position.

---

## Quartiles

Quartiles split the data into **4 equal parts**. Each part holds about 25% of the data.

- $Q_1$ (**first quartile / lower quartile**): about 25% of the data is at or below it.
- $Q_2$ (**second quartile**): about 50% is at or below it. This is the **median**.
- $Q_3$ (**third quartile / upper quartile**): about 75% is at or below it.

### Formula

$$
\text{Position of } Q_k = \frac{k(n+1)}{4}
$$

- $k$ = which quartile you want (1, 2, or 3)
- $n$ = how many values are in the data

### Example

Quiz scores of 12 students, already sorted:

| Position | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Score | 10 | 26 | 28 | 30 | 31 | 33 | 35 | 36 | 38 | 40 | 42 | 47 |

There are 12 scores, so $n = 12$.

**Finding $Q_1$:**

$$
\text{Position} = \frac{1(12+1)}{4} = \frac{13}{4} = 3.25
$$

Position $3.25$ is between the **3rd** value (28) and the **4th** value (30). What do we do with the $.25$?

### What to do when the position is a decimal

We move **that fraction of the way** from one value to the next. This is called **interpolation**.

Position $3.25$ means "start at the 3rd value, then go $0.25$ (one quarter) of the way to the 4th value."

1. Start at the 3rd value: **28**
2. Find the gap to the next value: $30 - 28 = 2$
3. Take $0.25$ of the gap: $0.25 \times 2 = 0.5$
4. Add it on: $28 + 0.5 = 28.5$

$$
Q_1 = 28.5
$$

**Finding $Q_2$ (the median):**

$$
\text{Position} = \frac{2(13)}{4} = 6.5
$$

Between the 6th value (33) and the 7th value (35). Gap is $2$, and half of it is $1$.

$$
Q_2 = 33 + 0.5(2) = 34
$$

**Finding $Q_3$:**

$$
\text{Position} = \frac{3(13)}{4} = 9.75
$$

Between the 9th value (38) and the 10th value (40). Gap is $2$.

$$
Q_3 = 38 + 0.75(2) = 39.5
$$

**What this means:** about a quarter of the class scored 28.5 or lower, half scored 34 or lower, and three quarters scored 39.5 or lower.

> [!tip] If the position is a whole number
> No interpolation needed. Just take the value at that position. For example, if the position comes out to exactly $5$, the answer is the 5th value.

---

## Deciles

Deciles split the data into **10 equal parts**. Each part holds about 10% of the data.

- $D_1$: about 10% of the data is at or below it.
- $D_3$: about 30% is at or below it.
- $D_5$: about 50% is at or below it. This is the **median** again.
- ...and so on up to $D_9$ (about 90%).

### Formula

$$
\text{Position of } D_k = \frac{k(n+1)}{10}
$$

It's the quartile formula with **10** instead of **4**.

### Example (same quiz scores)

**Finding $D_3$:**

$$
\text{Position} = \frac{3(13)}{10} = \frac{39}{10} = 3.9
$$

Between the 3rd value (28) and the 4th value (30). Gap is $2$.

$$
D_3 = 28 + 0.9(2) = 28 + 1.8 = 29.8
$$

About 30% of the class scored 29.8 or lower.

**Finding $D_7$:**

$$
\text{Position} = \frac{7(13)}{10} = 9.1
$$

Between the 9th value (38) and the 10th value (40). Gap is $2$.

$$
D_7 = 38 + 0.1(2) = 38.2
$$

About 70% of the class scored 38.2 or lower.

---

## Percentiles

Percentiles split the data into **100 equal parts**. Each part holds about 1% of the data.

- $P_{10}$: about 10% of the data is at or below it.
- $P_{50}$: about 50%. The **median** again.
- $P_{90}$: about 90% is at or below it.

### Formula

$$
\text{Position of } P_k = \frac{k(n+1)}{100}
$$

Same pattern, with **100** this time.

### Example (same quiz scores)

**Finding $P_{90}$:**

$$
\text{Position} = \frac{90(13)}{100} = \frac{1170}{100} = 11.7
$$

Between the 11th value (42) and the 12th value (47). Gap is $5$.

$$
P_{90} = 42 + 0.7(5) = 42 + 3.5 = 45.5
$$

About 90% of the class scored 45.5 or lower. So to be in the **top 10%**, a student needed to score **higher than 45.5**.

> [!warning] Percentile is not percentage
> Being in the **90th percentile** means you did better than about 90% of the people who took the test. It does **not** mean you got 90% of the items right. On a very hard test, a score of 60% could still be in the 90th percentile.

---

## How they connect

All three are the same idea with different-sized slices, so some of them are equal:

| Quartile | Decile | Percentile |
|---|---|---|
| $Q_1$ | | $P_{25}$ |
| $Q_2$ (median) | $D_5$ | $P_{50}$ |
| $Q_3$ | | $P_{75}$ |
| | $D_1$ | $P_{10}$ |
| | $D_3$ | $P_{30}$ |

So if a problem asks for $P_{25}$, you can use the quartile formula for $Q_1$ instead. You'll get the same answer.

---

## Summary

**Steps for any quartile, decile, or percentile:**

1. **Sort** the data from smallest to largest.
2. **Count** the values to get $n$.
3. **Find the position** using the right formula:

| Measure | Position formula |
|---|---|
| Quartile $Q_k$ | $\dfrac{k(n+1)}{4}$ |
| Decile $D_k$ | $\dfrac{k(n+1)}{10}$ |
| Percentile $P_k$ | $\dfrac{k(n+1)}{100}$ |

4. **Find the value** at that position.
   - Whole number: take that value.
   - Decimal: start at the lower value and add (decimal part) × (gap to the next value).

---

## Practice

Data (already sorted): $5, 8, 12, 15, 18, 21, 24, 30, 60$

**1.** Find $Q_1$, $Q_2$, and $Q_3$.


**2.** Find $D_4$.


**3.** Find $P_{80}$.


**4.** Find $D_5$ and $P_{50}$ without using their formulas.

**5.** Maria is in the 75th percentile of her class. Which quartile is she at, and what does it mean?
