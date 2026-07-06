---
layout: post
title: "Pearson's coefficient, p-value and chi squared test"
date: 2026-03-16
---

Pearson was an extraordinary man, probably one of the most important figures in the history of statistics. In this blog, I will write my explanation to classic statistics metrics.

## Pearson's coefficient
The Pearsons coefficient is also called the r-value of two data points. Let us define a pair of variables, then the correlation between them is given by the formula

$\rho_{xy} = \dfrac{cov(X, Y)}{\sigma_X \cdot \sigma_Y}$


where $cov$ is the covariance between $X, Y$ . But why is correlation dependent on covariance?

Lets assume that we have two data columns, height and weight.

| Height| Weight 
|--------|-----|
| 160  | 55  |
| 181    | 66  |
| 175  | 77  |



What do we mean when we want the covariance between $H, W$ denoting height and weight respectively? Let me define $\bar{H}$, $\bar{W}$ as the expected value of $H,W$ respectively. 

If we look at the formula of covariance, we see something like
 
$Cov(H,W)=\sum_{i=0}^n (H_i - E[H]) \cdot (W_i - E[W])$



Observe that two values are correlated if they move smoothly with each other. If one moves above the mean the other moves above the mean too, we get a positive correlation. If one moves above the average and one moves below the average, we get a negative correlation.
 

For example, in some case if $H_i < E[H]$ and $W_i > E[W]$, we get a negative product and it contributes negatively in the total sum.

But the formula i mentioned at the top of the introduction has two standard deviations in the denominator. What is it? Well, for a coefficient it is pretty necessary that we get a bounded and dimensionless answer. Its exactly why we have the scaling factor ($\sigma_X \cdot \sigma_Y$).

Let me give a simple example of this function in python
```py
import numpy as np
import pandas as pd

# define some data with two columns [height, weight]
data = pd.read_csv(...)

x: pd.Series = data['height']
y: pd.Series = data['weight']

r = x.corr(y)
// or
r = np.corrcoeff(x, y)[0, 1]
print(r)
```

The $r$ value is bounded between $[-1, 1]$. Well, naturally someone would remember the fundamental trigonometric functions like $sinx$ and $cosx$. The range of $cosx$ is $[-1, 1]$ and we already have techniques like cosine similarity with vectors. If you look closely, the formula i mentioned above (with normalization) looks like the angle between two vectors. 

Because in general, 

$\vec{a} \cdot \vec{b} = \|\vec{a}\| \, \|\vec{b}\| \, \cos(\theta)$

$\cos(\theta) = \frac{\vec{a} \cdot \vec{b}}{\|\vec{a}\| \, \|\vec{b}\|}$

I mean if a basic technique like cosine similarity is used for RAGs or extraction of tokens from multilingual embedding spaces why not statistics.

Also, the below derivation is pretty irrelevant but could be useful for intuition. 

Start with the definition of covariance:

$\mathrm{Cov}(X,Y) = E[(X - E[X])(Y - E[Y])]$ 

$(X - E[X])(Y - E[Y]) = XY - X E[Y] - Y E[X] + E[X]E[Y]$

$E[XY - X E[Y] - Y E[X] + E[X]E[Y]]$


Using linearity of expectation,

$E[XY] - E[XE[Y]] - E[YE[X]] + E[E[X]E[Y]]$


Since \(E[X]\) and \(E[Y]\) are constants,

$E[XE[Y]] = E[X]E[Y]$

$E[YE[X]] = E[X]E[Y]$

$E[E[X]E[Y]] = E[X]E[Y]$


Substitute back:

$E[XY] - E[X]E[Y] - E[X]E[Y] + E[X]E[Y]$

$\mathrm{Cov}(X,Y) = E[XY] - E[X]E[Y]$


Thats it. Simple high-school probability gives you such a simple formula. Just look at the expression. If we assume that $X=Y$ (the distributions are same), $E[XY]-E[X]E[Y]=0$. Which gives such a good intuition to covariance.   

## Chi squared test

Pearson also developed the Chi squared test. The Chi squared test checks whether two variables are independent. What do we mean by independent variables though? Suppose that $P(X)$ and $P(Y)$ are such that

$P(X,Y) = P(X)\cdot P(Y)$

If two variables are independent, the value of one variable does not affect the probability distribution of the other.

For each cell in the table, we compute

$\frac{(O_{ij} - E_{ij})^2}{E_{ij}}$

where

$O_{ij}$ is the **observed** frequency in cell $i,j$  
$E_{ij}$ is the **expected** frequency in cell $i,j$

The full Chi squared statistic is

$\boxed{\chi^2 = \sum \frac{(O_{ij} - E_{ij})^2}{E_{ij}}}$

For an intuitive explanation for people who don't like reading Wikipedia, I would give you the best explanation I could give.

Consider the following dataset.

| Feature 1 | Feature 2 | Target |
|-----------|-----------|--------|
| A | X | Yes |
| A | Y | No |
| B | X | Yes |
| B | Y | No |
| A | X | Yes |
| B | Y | No |

This table has two features and a target variable. After a simple label encoding we can assign numerical values to the categorical variables.

| Feature 1 | Feature 2 | Target |
|-----------|-----------|--------|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |
| 0 | 0 | 1 |
| 1 | 1 | 0 |

Explaining the Chi squared test row by row is difficult, so we construct a frequency table.

| Feature 1 | Target = 1 | Target = 0 | Total |
|-----------|------------|------------|-------|
| 0 | 2 | 1 | 3 |
| 1 | 1 | 2 | 3 |
| Total | 3 | 3 | 6 |

Feature 1 has two distinct values, $0$ and $1$. When Feature 1 is $0$, the target is $1$ two times and $0$ one time. When Feature 1 is $1$, the target is $1$ one time and $0$ two times.

If the two variables are independent, the expected value of each cell is

$E_{ij} = \frac{(\text{row total}) \cdot (\text{column total})}{\text{grand total}}$

In a fancy way, this formula assumed that the *null hypothesis* is true.

For example, the expected value for the cell where Feature 1 is $0$ and Target is $1$ is

$E = \frac{3 \cdot 3}{6} = 1.5$

However, the observed value in this cell is $2$. The contribution of this cell to the Chi squared statistic is

$\frac{(2 - 1.5)^2}{1.5} = 0.1667$

Since there are four cells in the table,

$\chi^2 \approx 4 \cdot 0.1667 = 0.67$

This value measures how far the observed counts deviate from the counts we would expect if Feature 1 and the target were independent.

A simple snippet with the chi squared function
```py
import pandas as pd
from scipy.stats import chi2_contingency

table = pd.crosstab(data['feature_1'], data['target'])
chi2, p, _, _ = chi2_contingency(table)
print(chi2, p)
```
## The brilliance of Pearson and p-value

Assuming that the null hypothesis is true. The two columns $X$ and $Y$ are independent and still give a high chi-squared test.

It is mathematically defined as,  

$p = P(X \geq \chi^2_{\text{observed}} \mid H_0)$

which can be read as the probability of getting a $\chi$ greater than the observed chi given that the "**null hypothesis is true**".

If the variables were actually independent, how likely would it be to see a chi square value this large just by random chance?

How significant is the p-value? Let me tell you something about its history. The p-value became so significant that people started taking it as a school project. People did something that later became known as "p-value hacking". They repeated experiments multiple times just to get a p value close to 0.05, which is sometimes called the alpha value.

We don't need a threshold like $0.05$, we need perfect confidence scores and variations in sample spaces. 

## Conclusion

In this post, we explored some foundational concepts in statistics introduced by Karl Pearson. The Pearson correlation coefficient quantifies the linear relationship between two variables, providing a normalized and bounded measure of association. The Chi squared test allows us to assess whether two categorical variables are independent by comparing observed and expected counts. We also discussed the p-value and its history.

## References

1. Pearson, K. (1895). "Notes on regression and inheritance in the case of two parents." *Proceedings of the Royal Society of London*, 58, 240–242.  
2. Pearson, K. (1900). "On the criterion that a given system of deviations from the probable in the case of a correlated system of variables is such that it can be reasonably supposed to have arisen from random sampling." *Philosophical Magazine*, 50, 157–175.  
3. Moore, D. S., McCabe, G. P., & Craig, B. A. (2021). *Introduction to the Practice of Statistics*. 10th Edition. W. H. Freeman.  
4. [`pandas.Series.corr` documentation](https://pandas.pydata.org/docs/reference/api/pandas.Series.corr.html)  
5. [`numpy.corrcoef` documentation](https://numpy.org/doc/stable/reference/generated/numpy.corrcoef.html)  
6. [`scipy.stats.chi2_contingency` documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.chi2_contingency.html)
