---
layout: post
title: Cryptography - Polynimial Rings And Finite Field
---
Group, ring and field

## Group

**Definition:** A Group is a set G together with a binary operation · on G such that the following three properties hold:

1. Associative:

$$a \cdot (b \cdot c) =(a \cdot b) \cdot c$$

2. Identity element:

$$a \cdot e = e \cdot a = a$$

3. Inverse element:

$$a · a ^{−1} = a ^{−1} · a = e$$

### Commutative(abelian) group

$$a · b = b · a$$

## Ring

**Definition:** $(R, +, \cdot)$ is a set R,together with two binary operations,

denoted by + and $\cdot$, such that:

1. R is an abelian group with respect to +.
2. · is associative
3. Distributive laws hold

$$ a \cdot (b + c) = a \cdot b + a \cdot c $$and $$(b + c) \cdot a = b \cdot a + c \cdot a $$

## Field

$$ Z_p = {0, 1, · · · , p − 1} $$, where p is a prime numbers

1. The set is closed under addition
2. Since p is prime number, any nonzero element in Z p has an inverse (Use Extended Euclidean algorithm).
3. Additions and multiplications are distributive.

$Z_p^*$ as a set of non-zero elements of $Z_p$

### Characteristics of F

Let F be a field with the multiplicative identity 1 and the additive identity 0. The characteristic of F , sometimes written as $char (F)$, is the smallest integer n $\ge$ 0 such that addition of the 1 with itself n times results in 0. i.e n(1) = 0.

## Polynomial Rings

$$ f(x) = f_nx^n + f_{n-1}x^{n-1} + ... + f_1x +f_0 = \sum_{i=0}^nf_ix^i$$

where

* x is an indeterminate
* $f_i$ is coeffcients
* $0\le i \ne n$ are elements of the field

**Facts and Definitions**:

* The zero polynomial is $f(x) = 0$, the degree is $-\infty$
* The degree of a polynomial $f(x)$, denoted $degf(x)$, is the largest index of a nonzero coefficient.

E.g.: $deg(1 +x + 2x^3)$ is 3, and $deg(1)=deg(1x^0)=0$.

* The degree of a nonzero polynomial is always finite.
* **Monic** if the leading cofficient is 1

E.g. $1 + x +2x^3$ is not monic while $1 + x$ is monic

* Two polynomials are equal if $f_i=g_i$
* $F\[x]$ represents set of all polynomials over a field F

### Sum:

$$f(x) +g(x) = \sum_{i=0}^{\infty}(f_i+g_i)x^i$$

E.g.

$$(1 + x +3x^3) + (1 +2x +2x^3) = 2 + 3x+4x^3 = 2 + x^3$$

### Product:

$$f(x)g(x) = \sum_i(\sum_{j=0}^i(f_jg_{i-j})x^i)$$

E.g.

$$ (1 + x+ 2x^3)(1 + x) = (1 +2x+x^2 +2x^3 +2x^4$$

> $(a + b)^p = (a^p +b^p)$
> Where:
> a and b are any two polynomials over $F_p$

### Facts and Definitions

* In any $F\[x]$ substraction is always possible but division is not always possible
* If a polynimial $r(x)$ divides another polynomial is $s(x)$, we say $r(x)|s(x)$, or $s(x)$ is divisible $r(x)$ or $r(x)$ is a factor of $s(x)$, when $r(x)a(x) = s(x)$
* A nonzero polynomial $p(x)$ that is divisible by $p(x)$ or by $\alpha$, where $\alpha$ is an arbitrary field element, is called an irreducible polynomial
* A monic irreducible polynomial is called a prime polynomial.
* $GCD\[r (x), s(x)]$ : Greatest common divisor of two polynomials $r (x)$ and $s(x$), is the monic polynomial of the greatest degree that divides both of them.
* If the $GCD\[r (x), s(x)]$ is 1 then the polynomials $r (x)$ and $s(x)$ are relatively prime.
* $LCM\[r (x), s(x)]$: Least common multiple of two polynomials $r (x)$ and $s(x)$, is the monic polynomial of the smallest degree that is divisible by both of them.

## Finite Fields of size $p^k$

> Hard Integer factorization problem, but not for factorizing a polynomial over $Z_p$ using Berlekamp
>
> $$GF(p^k) = GF(p)[x] \mod m(x)$$
> Where

* p is prime
* $m(x)$ is an irreducible polynomial of degree k
* $GF^*(p^k )$ to denote all non-zero elements of $GF(p^k )$

### Method

* Long Devision

![](/images/screenshot-from-2019-11-06-10-11-14.png)

* Euclidean Algorithm

### Example

$$GF(3^2) = GF(3)[x] \mod (2 + 2x + x^2 )$$

![](/images/screenshot-from-2019-11-06-14-43-46.png)

## Primitive Irreducible Polynomials

The **multiplicative order** of the indeterminate x is exactly
equal to $p^{k − 1}$
