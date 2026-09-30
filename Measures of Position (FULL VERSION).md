# Measures of Position (FULL VERSION)

> Note: THIS IS THE FULL VERSION. The simple version is in README. 

## Definition

A **measure of position** tells you **where a value stands relative to the rest of the data**. It answers questions like:

- "Is a score of 36 good *compared to the class*?"
- "What score do you need to be in the top 10%?"
- "Where does the middle half of the data sit?"

Statistics describes data in three ways, and each asks a different question:

| Family | Question | Examples |
|---|---|---|
| **Measures of center** | What is a typical value? | mean, median, mode |
| **Measures of spread** | How scattered are the values? | range, variance, standard deviation, IQR |
| **Measures of position** | Where does a particular value rank? | quartiles, deciles, percentiles, percentile rank, z-scores |

The core idea is **cut points**. Sort the data from smallest to largest, then place markers that split it into equal-sized groups:

| Name | Splits the data into | Markers | Notation |
|---|---|---|---|
| **Quartiles** | 4 equal parts | 3 | $Q_1, Q_2, Q_3$ |
| **Deciles** | 10 equal parts | 9 | $D_1, \dots, D_9$ |
| **Percentiles** | 100 equal parts | 99 | $P_1, \dots, P_{99}$ |

The general name for all of these is a **quantile**. Any quantile is "the value below which a fraction $p$ of the data falls."

## First Requirements

1. **Sorting.** Every measure of position starts by arranging the data in **increasing order**. Unsorted data gives nonsense.
2. **The median** is the middle value of sorted data. With $n$ values it sits at position $\frac{n+1}{2}$. For odd $n$ that's an actual data point. For even $n$ it's halfway between the two middle values.
3. **Position vs. value.** "The 4th value" is a *position*. "30" is a *value*. Most mistakes in this topic come from mixing these up. Every formula below first finds a **position**, then reads off the **value** there.

---

## Part 1: Relationships between the three families

Quartiles, deciles, and percentiles are the same idea at different resolutions, so they overlap:

$$
Q_1 = P_{25} \qquad Q_2 = D_5 = P_{50} = \text{median} \qquad Q_3 = P_{75}
$$

$$
D_k = P_{10k} \qquad (D_1 = P_{10},\ D_3 = P_{30},\ \dots)
$$

So you only need one master formula, the percentile one. Quartiles and deciles are special cases.

> [!warning] Percentile ≠ percentage
> Scoring at the **90th percentile** means you scored higher than about 90% of the people who took the test. It says nothing about getting 90% of the items right. On a very hard exam, a raw score of 45% could be the 90th percentile.

---

## Part 2: Computing quantiles from ungrouped data

### The problem: where exactly is "25%"?

With 12 data points, "one quarter of the way through" is position 3, or maybe 3.25, or between 3 and 4. Data is discrete, so the 25% mark usually falls **between** two data points. The different ways of handling this gap give slightly different answers (see Part 3). This section uses the method most Philippine textbooks and DepEd modules use (the Mendenhall & Sincich method): **find the position with $(n+1)$, then interpolate.**

### The formulas (position first)

For a sorted data set of size $n$:

$$
\text{Position of } Q_k = \frac{k(n+1)}{4}
\qquad
\text{Position of } D_k = \frac{k(n+1)}{10}
\qquad
\text{Position of } P_k = \frac{k(n+1)}{100}
$$

They all say the same thing: position $= p \cdot (n+1)$, where $p$ is the fraction you want ($\frac14$, $\frac{3}{10}$, $0.9$...).

**Why $n+1$ and not $n$?** Imagine $n$ values that split the number line into $n+1$ gaps. If the values were perfectly evenly spread, the $i$-th value would sit a fraction $\frac{i}{n+1}$ of the way through. So the value at fraction $p$ is at position $p(n+1)$. A quick check: the median ($p = \frac12$) comes out at $\frac{n+1}{2}$, the median position you already know.

### Reading off the value: linear interpolation

If the position is a whole number, the answer is that data value. If it's a decimal like $3.25$, split it into a whole part and a fractional part:

$$
\text{value} = x_{(3)} + 0.25\,\big(x_{(4)} - x_{(3)}\big)
$$

where $x_{(i)}$ means "the $i$-th value in sorted order." You go 25% of the way from the 3rd value toward the 4th.

In general, if the position is $L = w + f$ (with $w$ the whole part and $f$ the decimal part):

$$
\boxed{\text{value} = x_{(w)} + f\,\big(x_{(w+1)} - x_{(w)}\big)}
$$

> [!note] Rounding shortcut
> Some textbooks round the position instead of interpolating (for example, round $3.25$ down to $3$, or take the average when the position ends in $.5$). This is fine for a rough answer, but interpolation is more precise and is the standard in DepEd modules.

### Worked example

Quiz scores of 12 students (already sorted):

| Position | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Score | 10 | 26 | 28 | 30 | 31 | 33 | 35 | 36 | 38 | 40 | 42 | 47 |

Here $n = 12$, so $n + 1 = 13$.

**First quartile $Q_1$**

$$
L = \frac{1 \cdot 13}{4} = 3.25 \quad\Rightarrow\quad Q_1 = 28 + 0.25(30 - 28) = 28.5
$$

**Median $Q_2$**

$$
L = \frac{2 \cdot 13}{4} = 6.5 \quad\Rightarrow\quad Q_2 = 33 + 0.5(35 - 33) = 34
$$

**Third quartile $Q_3$**

$$
L = \frac{3 \cdot 13}{4} = 9.75 \quad\Rightarrow\quad Q_3 = 38 + 0.75(40 - 38) = 39.5
$$

**Third decile $D_3$**

$$
L = \frac{3 \cdot 13}{10} = 3.9 \quad\Rightarrow\quad D_3 = 28 + 0.9(30 - 28) = 29.8
$$

**First decile $D_1$** (note the big jump between the first two values)

$$
L = \frac{1 \cdot 13}{10} = 1.3 \quad\Rightarrow\quad D_1 = 10 + 0.3(26 - 10) = 14.8
$$

**90th percentile $P_{90}$**

$$
L = \frac{90 \cdot 13}{100} = 11.7 \quad\Rightarrow\quad P_{90} = 42 + 0.7(47 - 42) = 45.5
$$

Interpretation: about 90% of the class scored at or below 45.5. To be in the top 10%, you'd need more than 45.5.

> [!warning] Edge cases
> If the position is **below 1** (e.g. $P_5$ with $n = 12$ gives $L = 0.65$), use the smallest value. If it's **above $n$**, use the largest. With only 12 data points you can't really tell the 5th percentile apart from the minimum. Extreme percentiles need a lot of data to mean anything.

---

## Part 3: Why different sources give different answers

Ask three calculators for $Q_1$ and $Q_3$ of the quiz data above and you'll get three answers:

| Method | Used by | $Q_1$ | $Q_3$ |
|---|---|---|---|
| Position $p(n+1)$, interpolate | DepEd modules, Minitab, Excel `QUARTILE.EXC`, R `type=6` | 28.5 | 39.5 |
| Median of each half (Tukey's hinges) | Many US textbooks, TI-83/84 | 29 | 39 |
| Position $1 + p(n-1)$, interpolate | Excel `QUARTILE.INC`, Google Sheets, R default (`type=7`), NumPy default | 29.5 | 38.5 |

**Median-of-halves method:** split the sorted data at the median. $Q_1$ is the median of the lower half and $Q_3$ is the median of the upper half. Here the lower half is $10, 26, 28, 30, 31, 33$, whose median is $\frac{28+30}{2} = 29$. (When $n$ is odd, textbooks disagree on whether to include the median itself in each half. That's yet another split.)

**None of these is wrong.** A quantile of a *sample* is an estimate, and there are at least nine standard ways to define it (Hyndman & Fan, 1996, catalogued them). The differences shrink as $n$ grows. For $n = 1000$ they're negligible. For $n = 12$ they matter.

> [!tip] Practical rule
> On a DepEd exam, use $p(n+1)$ with interpolation unless the problem says otherwise. In real work, **state which method you used**, and use the same one when comparing groups.

---

## Part 4: Percentile rank (the reverse question)

A **percentile** goes from a *percentage* to a *score*: "What score is at the 90th percentile?" → 45.5.

A **percentile rank** goes the other way, from a *score* to a *percentage*: "Scoring 36, what percent of the class did I beat?"

The DepEd formula for ungrouped data:

$$
\boxed{PR = \frac{B + 0.5E}{n} \times 100}
$$

- $B$ = number of values **below** the score
- $E$ = number of values **equal** to the score
- $n$ = total number of values

**Why the $0.5E$?** If you tie with others, it's unfair to say you beat all of them and also unfair to say you beat none. Counting ties as half is the compromise. It puts you in the middle of your tied group.

**Example.** Percentile rank of 36 in the quiz data: 7 scores are below 36 ($10, 26, 28, 30, 31, 33, 35$) and 1 score equals it.

$$
PR = \frac{7 + 0.5(1)}{12} \times 100 = 62.5
$$

The student who scored 36 did better than about 62.5% of the class.

**Percentile rank of 40:** $B = 9$, $E = 1$, so $PR = \frac{9.5}{12} \times 100 \approx 79.2$.

> [!note] Why the round trip isn't exact
> Going back from PR 62.5 to a score with the $p(n+1)$ formula gives $P_{62.5} = 36.25$, not exactly 36. The two formulas use slightly different conventions for "fraction below." With small data sets, don't expect percentile and percentile rank to be perfect inverses.

Other common versions: some books use $\frac{B}{n} \times 100$ (strictly below only) or $\frac{B+E}{n} \times 100$ (at or below). Again, check which one your source uses.

---

## Part 5: The five-number summary and the box-and-whisker plot

### Five-number summary

Five numbers give a quick picture of a whole distribution:

$$
\text{Min},\quad Q_1,\quad Q_2,\quad Q_3,\quad \text{Max}
$$

They split the data into **four parts that each hold about 25%** of the values. For the quiz data: $10,\ 28.5,\ 34,\ 39.5,\ 47$.

### Interquartile range (IQR)

$$
\boxed{IQR = Q_3 - Q_1}
$$

The IQR is the spread of the **middle 50%** of the data. For the quiz data, $IQR = 39.5 - 28.5 = 11$.

Compare it to the **range** ($47 - 10 = 37$). The range depends on only the two most extreme values, so one strange score can make it huge. The IQR ignores the outer quarters, so it's **resistant** to extreme values.

### Outliers: Tukey's fences

An **outlier** is a value unusually far from the bulk of the data. The standard rule (John Tukey, 1977) builds "fences" 1.5 IQRs beyond the box:

$$
\text{Lower fence} = Q_1 - 1.5 \cdot IQR \qquad \text{Upper fence} = Q_3 + 1.5 \cdot IQR
$$

Any value **outside** the fences is an outlier.

For the quiz data:

$$
\text{Lower fence} = 28.5 - 1.5(11) = 12 \qquad \text{Upper fence} = 39.5 + 1.5(11) = 56
$$

The score **10 is below 12, so it's an outlier.** Nothing is above 56.

Some texts add a second pair of fences at $3 \cdot IQR$. Values beyond those are **extreme outliers**. Values between the $1.5$ and $3$ fences are **mild outliers**.

> [!question]- Why 1.5, specifically?
> It's a convention, but a well-chosen one. For data from a normal (bell-shaped) distribution, $Q_1$ and $Q_3$ sit about $0.674\sigma$ from the mean, so $IQR \approx 1.349\sigma$. The upper fence lands at about
> $$\mu + 0.674\sigma + 1.5(1.349\sigma) \approx \mu + 2.7\sigma$$
> Only about **0.7%** of normal data falls outside the two fences. So the rule rarely flags ordinary values, but it catches points that really are unusual. Tukey reportedly said 1 was too small and 2 too large.

### Drawing the box plot

1. Draw a number line that covers all the data.
2. Draw a **box** from $Q_1$ to $Q_3$. Its width is the IQR.
3. Draw a line inside the box at the **median**.
4. Draw **whiskers** from the box out to the **smallest and largest values that are not outliers**.
5. Plot each **outlier** as a separate dot.

(A simpler version draws the whiskers all the way to the min and max and doesn't mark outliers. The version above, called a *modified box plot*, is more informative.)

Box plot of the quiz data. The left whisker stops at 26, the smallest non-outlier, and 10 is plotted on its own:

![[measures-of-position-boxplot.svg|600]]

### Reading a box plot

**Shape (skewness).** Compare the two halves of the box and the two whiskers:

| What you see | Shape |
|---|---|
| Median in the middle of the box, whiskers about equal | Roughly **symmetric** |
| Median closer to $Q_1$, longer right whisker | **Skewed right** (positively skewed): a long tail of high values |
| Median closer to $Q_3$, longer left whisker | **Skewed left** (negatively skewed): a long tail of low values |

In the quiz plot, the median ($34$) is exactly in the center of the box ($28.5$ to $39.5$), so the middle half of the class is symmetric. The tails disagree: the right whisker is longer, but the single most extreme value (the outlier at 10) is on the left. When the signals are mixed like this, the fair summary is "roughly symmetric, with one unusually low score." That score is worth investigating. Maybe the student was absent or there was a recording error.

**Comparing groups.** Box plots are best when stacked side by side. For two sections that took the same test, compare:
- **Medians**: which group did better typically?
- **Box widths (IQRs)**: which group is more consistent?
- **Overlap**: if one group's box lies entirely above the other's, the difference is large. If the boxes overlap heavily, the groups are similar.

> [!warning] What box plots hide
> A box plot doesn't show how many data points there are, and it can't show two peaks (bimodality). Two very different data sets can have identical box plots. When possible, look at a histogram too.

---

## Part 6: Grouped data

When data comes as a **frequency distribution** (classes and counts), you no longer know the individual values. You only know how many fall in each class. You can still estimate quantiles by assuming the values are **spread evenly within each class**.

### Cumulative frequency

The **cumulative frequency** ($cf$) of a class is the number of values in that class *and all classes below it*. It's what you need to find which class contains a given position.

Example: math test scores of 40 students.

| Class | Frequency $f$ | Class boundaries | $cf$ (less than) |
|---|---|---|---|
| 41–50 | 3 | 40.5–50.5 | 3 |
| 51–60 | 5 | 50.5–60.5 | 8 |
| 61–70 | 9 | 60.5–70.5 | 17 |
| 71–80 | 12 | 70.5–80.5 | 29 |
| 81–90 | 8 | 80.5–90.5 | 37 |
| 91–100 | 3 | 90.5–100.5 | 40 |

$N = 40$, class width $i = 10$.

### The formula

$$
\boxed{Q_k = LB + \left(\frac{\frac{kN}{4} - cf_b}{f_Q}\right) i}
$$

- $LB$ = lower boundary of the class containing the quartile (the **quartile class**)
- $\frac{kN}{4}$ = the position you're looking for
- $cf_b$ = cumulative frequency of the class **before** the quartile class
- $f_Q$ = frequency of the quartile class
- $i$ = class width

For deciles, replace $\frac{kN}{4}$ with $\frac{kN}{10}$. For percentiles, use $\frac{kN}{100}$. Everything else stays the same.

**Where it comes from.** Say you want position 10. The first two classes hold 8 values, so you need **2 more** from the third class ($60.5$–$70.5$), which holds 9. If those 9 values are spread evenly across the class's 10 units, going 2 values in means going $\frac{2}{9}$ of the way across:

$$
60.5 + \frac{2}{9}(10) \approx 62.72
$$

That's the formula. It's the same linear interpolation as Part 2, applied inside a class.

> [!note] $N$ vs. $n+1$
> Grouped-data formulas use $\frac{kN}{4}$, not $\frac{k(N+1)}{4}$. The class is treated as a continuous stretch with no individual points, so the "gaps between points" argument for $n+1$ doesn't apply.

### Worked example

**$Q_1$:** position $\frac{40}{4} = 10$. The $cf$ first reaches 10 in the class 61–70 ($cf = 17$).

$$
Q_1 = 60.5 + \frac{10 - 8}{9}(10) \approx 62.72
$$

**Median $Q_2$:** position $20$ → class 71–80.

$$
Q_2 = 70.5 + \frac{20 - 17}{12}(10) = 73
$$

**$Q_3$:** position $30$ → class 81–90.

$$
Q_3 = 80.5 + \frac{30 - 29}{8}(10) = 81.75
$$

**$D_3$:** position $\frac{3 \cdot 40}{10} = 12$ → class 61–70.

$$
D_3 = 60.5 + \frac{12 - 8}{9}(10) \approx 64.94
$$

**$P_{90}$:** position $\frac{90 \cdot 40}{100} = 36$ → class 81–90.

$$
P_{90} = 80.5 + \frac{36 - 29}{8}(10) = 89.25
$$

$IQR \approx 81.75 - 62.72 = 19.03$.

### Cumulative frequency histogram and polygon (ogive)

- A **cumulative frequency histogram** is a bar graph with one bar per class, where each bar's height is the class's $cf$ (not its $f$). The bars always rise from left to right.
- A **cumulative frequency polygon**, or **ogive** ("oh-jive"), plots each class's **upper boundary** against its $cf$ and connects the points with straight lines. It starts at $cf = 0$ at the lowest boundary.

The ogive is a picture of the formula above. **To read a quantile off it,** go to the position on the vertical axis ($10$ for $Q_1$, $20$ for the median, $30$ for $Q_3$), move right until you hit the curve, then drop down to the horizontal axis:

![[measures-of-position-ogive.svg|600]]

The straight segments between points *are* the "values spread evenly within a class" assumption. So a carefully drawn ogive gives the same answers as the formula.

The ogive also shows density. Where it's **steep** (70.5 to 80.5 here), lots of values are packed together. Where it's **flat** (the ends), values are sparse.

---

## Part 7: Z-scores, a different kind of position

Quantiles describe position by **rank** ("what fraction is below me?"). A **z-score** describes position by **distance from the mean**, measured in standard deviations:

$$
\boxed{z = \frac{x - \bar{x}}{s}}
$$

For the quiz data, $\bar{x} = 33$ and $s \approx 9.44$.

- Score 47: $z = \frac{47 - 33}{9.44} \approx 1.48$, about one and a half standard deviations above the mean.
- Score 10: $z = \frac{10 - 33}{9.44} \approx -2.44$, far below. This agrees with the box plot that 10 is unusual.

**Z-scores let you compare across different scales.** Say you got 85 on a math test (mean 75, SD 5) and 90 on an English test (mean 85, SD 10). Which was the better performance?

$$
z_{\text{math}} = \frac{85 - 75}{5} = 2 \qquad z_{\text{English}} = \frac{90 - 85}{10} = 0.5
$$

Math, by a lot, even though the raw score was lower.

**Z-scores and percentiles for bell-shaped data.** If the data is roughly normal, each z-score corresponds to a percentile:

| $z$ | $-2$ | $-1$ | $-0.674$ | $0$ | $0.674$ | $1$ | $2$ |
|---|---|---|---|---|---|---|---|
| Percentile | 2.3 | 15.9 | 25 ($Q_1$) | 50 | 75 ($Q_3$) | 84.1 | 97.7 |

> [!tip] Quantiles or z-scores?
> Use **quantiles** when the data is skewed or has outliers. They depend only on order, so extreme values barely move them. Use **z-scores** when the data is roughly symmetric and bell-shaped. The mean and standard deviation are both pulled around by outliers, so z-scores inherit that weakness.

---

## Part 8: Going deeper

### The quantile function

For a whole population (or a probability distribution), let $F(x)$ be the **cumulative distribution function**: the fraction of values $\le x$. The ogive is a sketch of $F$. The $p$-th quantile is the value where $F$ first reaches $p$:

$$
Q(p) = \min\{\, x : F(x) \ge p \,\}
$$

(For technical reasons the precise definition uses "inf" instead of "min.") $Q$ is essentially the **inverse** of $F$: $F$ takes a value and returns a proportion, $Q$ takes a proportion and returns a value. That's exactly the percentile rank / percentile pair from Part 4. For a sample, $F$ is a step function (it jumps by $\frac1n$ at each data point), and the different quantile methods in Part 3 are different ways of inverting that staircase.

### Robustness and the breakdown point

The **breakdown point** of a statistic is the fraction of the data you'd have to corrupt (replace with arbitrarily wild values) to make the statistic arbitrarily wrong.

| Statistic | Breakdown point |
|---|---|
| Mean | $0\%$: one wild value can move it anywhere |
| Standard deviation, range | $0\%$ |
| $Q_1$, $Q_3$, IQR | $25\%$ |
| Median | $50\%$, the highest possible |

This is why income, house prices, and hospital wait times are usually reported with **medians and percentiles**, not means. A handful of billionaires drags the mean income up but barely moves the median.

### Quantiles survive transformations

If you apply an **increasing** function $g$ to every value, the quantiles transform the same way:

$$
Q_p\big(g(X)\big) = g\big(Q_p(X)\big)
$$

Convert temperatures from °C to °F and the median converts with them. Take logarithms of incomes and the median log-income is the log of the median income. **The mean does not have this property** (the mean of logs is not the log of the mean). Quantiles only care about order, and increasing functions keep order.

### Quantiles as optimization

The mean minimizes the sum of squared distances: $\sum (x_i - c)^2$ is smallest at $c = \bar{x}$. The median minimizes the sum of **absolute** distances: $\sum |x_i - c|$ is smallest at $c = \text{median}$.

Every other quantile has a similar characterization. The $p$-th quantile minimizes a tilted absolute loss (the "pinball loss") that charges $p$ for each unit you undershoot and $1-p$ for each unit you overshoot. This is the basis of **quantile regression**, which predicts, say, the 90th-percentile delivery time instead of the average one.

---

## Part 9: Where you'll see measures of position

- **Growth charts.** Pediatricians plot a child's height and weight against percentile curves. "Your child is at the 40th percentile for height" means 40% of children that age are shorter.
- **Standardized tests.** The NAT, NCAE, SAT, and college entrance exams report percentile ranks so scores can be compared across years and test versions.
- **Income and inequality.** Economists compare the 90th and 10th income percentiles (the "90/10 ratio"). Poverty lines are sometimes defined relative to the median.
- **Software performance.** Engineers track "p95" and "p99" latency, the response time that 95% or 99% of requests beat. The average hides the slow requests that users actually notice.
- **Grading and admissions.** "Top 10% of the class" is a $P_{90}$ cutoff.
- **Quality control.** Box plots and IQR fences flag defective or mis-measured items.

---

## Common mistakes

1. **Forgetting to sort** before counting positions.
2. **Reporting the position as the answer.** $L = 3.25$ is where $Q_1$ is, not what it is.
3. **Confusing percentile with percentage** (Part 1).
4. **Confusing percentile with percentile rank.** Percentile: percent → score. Percentile rank: score → percent.
5. **Using class limits instead of class boundaries** in grouped data. $LB$ for 61–70 is $60.5$, not $61$.
6. **Using the wrong $cf_b$.** It's the $cf$ of the class *before* the quantile class, not of the quantile class itself.
7. **Drawing whiskers to an outlier.** In a modified box plot, whiskers stop at the last value inside the fences.
8. **Mixing methods** when comparing two data sets.

---

## Formula summary

| What | Ungrouped | Grouped |
|---|---|---|
| Position of $Q_k$ | $\frac{k(n+1)}{4}$ | $\frac{kN}{4}$ |
| Position of $D_k$ | $\frac{k(n+1)}{10}$ | $\frac{kN}{10}$ |
| Position of $P_k$ | $\frac{k(n+1)}{100}$ | $\frac{kN}{100}$ |
| Value | $x_{(w)} + f\,(x_{(w+1)} - x_{(w)})$ | $LB + \frac{\text{position} - cf_b}{f}\, i$ |
| Percentile rank | $\frac{B + 0.5E}{n} \times 100$ | |
| IQR | $Q_3 - Q_1$ | |
| Fences | $Q_1 - 1.5\,IQR,\ \ Q_3 + 1.5\,IQR$ | |
| z-score | $\frac{x - \bar{x}}{s}$ | |

---

## Practice

Data (sorted): $5, 8, 12, 15, 18, 21, 24, 30, 60$

**1.** Find $Q_1$, $Q_2$, and $Q_3$.

> [!success]- Answer
> $n = 9$, $n + 1 = 10$.
> - $Q_1$: $L = 2.5$ → $8 + 0.5(12 - 8) = 10$
> - $Q_2$: $L = 5$ → $18$
> - $Q_3$: $L = 7.5$ → $24 + 0.5(30 - 24) = 27$

**2.** Find the IQR and the fences. Are there any outliers?

> [!success]- Answer
> $IQR = 27 - 10 = 17$. Fences: $10 - 25.5 = -15.5$ and $27 + 25.5 = 52.5$. **60 is an outlier.**

**3.** Find $D_4$ and $P_{80}$.

> [!success]- Answer
> - $D_4$: $L = \frac{4 \cdot 10}{10} = 4$ → $15$
> - $P_{80}$: $L = \frac{80 \cdot 10}{100} = 8$ → $30$

**4.** Find the percentile rank of 21.

> [!success]- Answer
> $B = 5$, $E = 1$: $PR = \frac{5.5}{9} \times 100 \approx 61.1$

**5.** Using the grouped table in Part 6, find $P_{25}$ and $D_8$.

> [!success]- Answer
> - $P_{25}$ is the same as $Q_1 \approx 62.72$.
> - $D_8$: position $\frac{8 \cdot 40}{10} = 32$ → class 81–90. $80.5 + \frac{32 - 29}{8}(10) = 84.25$

**6.** (Conceptual) Two sections take the same test. Section A has median 30 and IQR 4. Section B has median 30 and IQR 15. What can you conclude?

> [!success]- Answer
> The typical student did equally well in both. Section A's scores are much more tightly clustered, so its students performed more consistently. Section B has a wider mix of strong and weak performers.

**7.** (Conceptual) A student scored at the 95th percentile on a test where the mean was 40%. Did they get 95% of the items right?

> [!success]- Answer
> Not necessarily, and probably not. The 95th percentile means they beat about 95% of test-takers. On a hard test, that could be a raw score of 70% or even lower.

---

## Related

- [[Measures of Central Tendency]]
- [[Measures of Variability]]
- [[Normal Distribution]]
