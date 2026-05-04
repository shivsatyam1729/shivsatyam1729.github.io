---

layout: post
title: "Number Theory I: Divisibility"
date: 2026-03-25
----------------

A concise introduction to divisibility and the foundations of number theory. This post develops core ideas such as the greatest common divisor, Bézout’s lemma, and the Euclidean algorithm, illustrated with clear examples and a problem solving perspective to build intuition for deeper results.

# Divisibility

Some definitions that are consistent through this article are listed below. Make sure to be familiar with these.

( a \mid b ) means that ( a ) divides ( b )

( a \nmid b ) means that ( a ) does not divide ( b )

( (a,b) = \gcd(a,b) )

( (a,b),[a,b] = |ab| )

### Introduction

Let ( a, b, c ) be integers.

If ( a \mid b ) then ( a \mid bc ) for any integer ( c )

If ( a \mid b ) and ( b \mid c ) then ( a \mid c )

If ( a \mid b ) and ( b \mid a ) then ( a = \pm b )

Its not very tough to prove each of them. In fact, I would let the readers do it as an exercise. Let me prove something relatively difficult to set a baseline.

Using the basic principles, find all ( n ) such that ( n^2 + 1 ) is divisible by ( n + 1 ). That is, find all ( n ) such that
( (n+1) \mid (n^2+1) ).

We write
[
n^2 + 1 = (n+1)^2 - 2n
]

So
[
\frac{n^2+1}{n+1} = (n+1) - \frac{2n}{n+1}
]

Since ( (n+1) \mid (n+1) ), we get
[
(n+1) \mid 2n
]

Now
[
(n+1) \mid \big(2n - 2(n+1)\big) = -2
]

Hence
[
(n+1) \mid 2
]

So
[
n+1 \in {\pm1, \pm2}
]

Thus
[
\boxed{n \in {-3, -2, 0, 1}}
]

### Greatest Common Divisor

Let ( d ) be a common divisor of ( a ) and ( b ) such that ( d \mid a ) and ( d \mid b ). A positive integer ( g ) is said to be the greatest common divisor of ( a ) and ( b ) if and only if:

* ( g \mid a ) and ( g \mid b )
* If ( d \mid a ) and ( d \mid b ), then ( d \mid g )

It is denoted by ( \gcd(a,b) ) or ( (a,b) ). This ( g ) is unique.

Two integers are said to be relatively coprime if
[
\gcd(a,b) = 1
]

### Bezout's Lemma

If ( a, b ) are integers, not both zero, then ( \gcd(a,b) ) exists and there exist integers ( x_0, y_0 ) such that
[
\gcd(a,b) = ax_0 + by_0
]

*Proof by contradiction:*

Let
[
S = { ax + by \mid x,y \in \mathbb{Z},\ ax + by > 0 }
]

By the well-ordering principle, ( S ) has a smallest element, say ( g ). So
[
g = ax + by
]

Suppose ( g \nmid a ). Then
[
a = gq + r, \quad 0 < r < g
]

So
[
r = a - gq = a(1 - qx) + b(-qy)
]

This contradicts the minimality of ( g ). Hence ( g \mid a ). Similarly, ( g \mid b ). Therefore ( g = \gcd(a,b) ).

### Euclidean Algorithm

Given integers ( b, c ) with ( c > 0 ), apply the division algorithm repeatedly:

[
b = cq + r_1, \quad 0 < r_1 < c
]
[
c = r_1 q_1 + r_2, \quad 0 < r_2 < r_1
]
[
r_1 = r_2 q_2 + r_3, \quad 0 < r_3 < r_2
]
[
\cdots
]
[
r_{j-2} = r_{j-1} q_{j-1} + r_j
]
[
r_{j-1} = r_j q_j
]

The last nonzero remainder ( r_j ) is ( \gcd(b,c) ).

Useful consequences:

* ( \gcd(a,b) = \gcd(a, b-a) ) for ( b > a )
* ( \gcd(a,b) = \gcd(a, b+a) )

### Example

Find ( \gcd(4840, 1512) ) and integers ( x_0, y_0 ) such that
[
4840x_0 + 1512y_0 = \gcd(4840,1512)
]

[
4840 = 3(1512) + 304
]
[
1512 = 4(304) + 296
]
[
304 = 1(296) + 8
]
[
296 = 37(8) + 0
]

So ( \gcd(4840,1512) = 8 ).

Back-substitute:
[
8 = 304 - 296
]
[
8 = 304 - (1512 - 4 \cdot 304) = 5 \cdot 304 - 1512
]
[
8 = 5(4840 - 3 \cdot 1512) - 1512 = 5 \cdot 4840 - 16 \cdot 1512
]

Thus
[
x_0 = 5,\quad y_0 = -16
]

### Code

```cpp
int eucledian(int a, int b, int &x, int &y) {
    if (!b) return x = 1, y = 0, a;
    
    int x1, y1;
    int g = eucledian(b, a % b, x1, y1);
    
    x = y1;
    y = x1 - (a / b) * y1;
    
    return g;
}
```

### Conclusion

In this post, we covered divisibility, GCD, Bezout's lemma, and the Euclidean algorithm. The next post will focus on primes and induction-based arguments.
