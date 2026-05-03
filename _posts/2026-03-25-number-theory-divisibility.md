---
layout: post
title: "Number Theory I: Divisibility"
date: 2026-03-25
---

# Divisibility

Some definitions that are consistent through this article are listed below. Make sure to be familiar with these.

$a | b$ means that $a$ divides $b$
$a \not | \space b$  means that $a$ doesn't divide $b$ 
$(a,b) = gcd(a,b)$
$(a,b) \cdot [a,b] = |ab|$

### Introduction
Let $a,b,c$ are integers then
 - If $a|b$ then $a|bc$ for any integer $c$ 
 - if $a|b$ and $b|c$ then $a|c$ 
 - If $a|b$ and $b|a$ then $a=\pm b$

Its not very tough to prove each of them. Infact, I would let the readers do it as an exercise. Let me prove something **relatively** difficult to set a baseline.

Using the basic principles, lets find all $n$'s such that $n^2+1$ is divisible by $n+1$. Mathematically, we need to find $S$ such that $\forall n \in S$:  $(n+1)|(n^2+1)$

We have $n^2 + 1 = (n + 1)^2 - 2n$ or $\dfrac{n^2+1}{n+1} = (n + 1) - \dfrac{2n}{n+1}$

Since $(n+1)|(n+1) \implies (n+1) | 2n$

Thus $(n+1)|2n$, $(n+1) \space |$ $[(n + 1) + (n+1)-2] \implies (n+1)|2$

Thus, $\boxed{n \in \{-3, -2, 0,1\}}$

### Greatest Common Divisor
Let $d$ be a common divisor of $a$ and $b$ such that $d|a$ and $d|b$. A positive integer $g$ is said to be the **greatest common divisor** of $a$ and $b$ if and only if these two conditions are met
 - $g|a$ and $g|b$ 
 - If $d|a$ and $d|b$ then $d|g$ 

It is used like $gcd(a,b)$ or $(a,b)$ in context of number theory. Also, such a $g$ is unique.
Two integers are said to be relatively **coprime** if $\boxed{gcd(a,b) = 1 = (a,b)}$ 

### Bezout's Lemma
If $a,b$ are integers, not both zero, then $gcd(a,b)$ exists   and there exist integers $x_0$, $y_0$ such that $gcd(a,b)=ax_0 + by_0$ 

*Proof By Contradiction-:*

Let $S = \{ax_0 + by_0|x,y \in Z, ax+by>0\}$. We can say that there is a minimum element (say $g$) by the well-ordering principle.

$ax + by = g$ 

Suppose that $g \not | \space a$. Then $a=gq + r, 0<r<g$. Hence,

$r = a - gq = a(1-qx) + b(-qy)$

This is a contradiction since $0 < r < g$ and $g$ is the smallest element in $S$. Hence $g|a$. Using the same flow we get $g|b$. Hence by the definition of gcd, we say that $g$ is the gcd of $a$ and $b$.

### The Eucledian Algorithm

Given integers $b,c$, $c>0$, we make a repeated application of the division algorithm to obtain a series of equations.

$b \space \space \space =  \space \space \space cq + r_1, \space \space \space 0 < r_1 < c$

$c \space \space \space =  \space \space \space r_1q_1 + r_2, \space \space \space 0 < r_2 < r_1$


$r_1\space \space=  \space r_2q_2 + r_3, \space \space \space 0 < r_3 < r_2$

.
.
.

$r_{j-2} \space \space=  \space r_{j-1}q_{j-1} + r_j, \space \space \space 0 < r_j < r_{j-1}$
$r_{j-1} \space \space=  \space r_{j}q_{j}, \space \space \space \space \space \space \space \space \space \space \space \space \space \space \space \space \space \space 0 < r_j < r_{j-1}$

It is said that $r_j$ is the greatest common divisor of the integers $b,c$ or $(b,c)=r_j$. Remember, Eucledian theorem is also used to find the integral coefficients from Bezout's theorem.

Euclid's theorem implies
 - $gcd(a,b) = gcd(a, b-a), \space b>a$
 - $gcd(a,b) = gcd(a, b+a)$
 - and much more

A simple example to understand the application of the Eucledian theorem would be to find $(4840, 1512)$ and the integral coefficients $x_0, y_0$ such that $4840x_0 + 1512y_0 = (4840, 1512)$.

We have
$4840\space \space=  \space 3(1512) + 304$ ............  (i)
$1512\space \space=  \space 4(304) + 296$    ............  (ii)
$304\space \space \space \space=  \space 1(296) + 8$    ............  (iii)
$296\space \space \space \space = \space 8(37) + 0$ 

The last non-zero remainder is $8$ which is $g = (4840, 1512)$. Now for the coefficients to the bezout equation, We rewrite (iii) as $8 = 304 - 296$. Substituting for $296$ in (ii),

$8 = 304 - (1512 - 4(304)) = 5(304) - 1512$ 

Substuting for $304$ from (i),

$8 = 5(4840 - 3(1512)) - 1512 = 5(4840) - 16(1512)$

so that $x_0=5,y_0=-16$

In context of competitive programming or implementation, you could use a recursive function like 
```c++
int eucledian(int a, int b, int &x, int &y) {
    if (!b) return x = 1, y = 0, a;
    
    int x1, y1;
    int g = eucledian(b, a % b, x1, y1);
    
    x = y1;
    y = x1 - (a / b) * y1;
    
    return g;
}
```

we try to solve a subproblem, maybe $\text{eucledian(b, a mod b)}$ such that $bx_1 + (a \text{ \% } b)y_1 = gcd(a, b)$, now for the real inputs $(a, b)$ mapped to $(x, y)$ we use $x = y_1$ and $y = x_1 - \lfloor \frac{a}{b} \rfloor \cdot y_1$



## Conclusion

In this post, I explained some number theory basics like GCD, Eucledian theorem, and how to relate the theorem to Bezout's Lemma. The next blog i'll write will be about Primes and It will have some interesting induction based proofs. Thank you.
