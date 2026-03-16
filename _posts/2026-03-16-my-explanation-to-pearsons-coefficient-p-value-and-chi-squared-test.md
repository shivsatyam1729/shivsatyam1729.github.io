---
layout: post
title: "My explanation to Pearson's coefficient, p-value and chi squared test"
date: 2026-03-16
---

Pearson was an extraordinary man, probably one of the most important figures in the history of statistics. His teacher was also a half cousin to Charles Darwin.

## Pearson's coefficient

The Pearson coefficient is also called the **r value** of two data points. Let us define a pair of variables. The Pearson coefficient, the correlation between them, is given by a formula.

The formula is

$\rho_{xy} = \dfrac{cov(X, Y)}{\sigma_X \cdot \sigma_Y}$

Lets assume that we have two data columns, height and weight.

| Height | Weight |
|--------|--------|
| 160    | 55     |
| 181    | 66     |
| 175    | 77     |

What do we mean when we want the covariance between $H$ and $W$, denoting height and weight respectively.

Let me define $\bar{H}$ and $\bar{W}$ as the expected value of $H$ and $W$ respectively.

If we look at the formula of covariance, we get

$Cov(H, W) = \sum_{i=0}^{n} (H_i - E[H]) \cdot (W_i - E[W])$

where $cov$ is the covariance between $X$ and $Y$ and the sigmas represent the standard deviation terms in the Pearson coefficient.

But why is correlation dependent on covariance?

Observe that two values are correlated when they move smoothly with each other. If one moves above the mean the other moves above the average too. If one moves above the average and the other moves below the average, we get a negative correlation.

For example, if $H_i < E[H]$ and $W_i > E[W]$, we get a negative product and it contributes negatively to the total sum.

But the formula mentioned earlier has two standard deviations in the denominator. Why?

For a coefficient it is necessary that we obtain a **bounded and dimensionless answer**. This is exactly why we have the scaling factor $(\sigma_X \cdot \sigma_Y)$.

### Python example

```python
import numpy as np
import pandas as pd

data = pd.read_csv(...)

x: pd.Series = data["height"]
y: pd.Series = data["weight"]

r = x.corr(y)

# or
```
r = np.corrcoef(x, y)[0, 1]

print(r)
