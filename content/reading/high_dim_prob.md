+++
title = "High-Dimensional Probability"
date = "2024-01-14T12:01:56+08:00"
tags = ["probability"]

+++

This file is for the notes and exercises for the book [High-Dimensional Probability](/pdfs/HDP-book.pdf.)

Errata and update of the book: [errata](/pdfs/Vershynin-Errata-2020.pdf), [update](Vershynin-Updates-2020.pdf).

Exercises solns reference: [soln](https://zhuanlan.zhihu.com/p/338822722).

# 0. Appetizer

## Key Takeaways
1. **convex combination** $\sum^{m}_{i=1}\lambda_iz_i$ where $\lambda_i\ge 0$ and $\sum^{m}_{i=1}\lambda_i=1$.

2. **convex hull of a set $T$**, $\mathrm{conv}(T)=\{\text{convex combinations of }z_1,\cdots,z_m\in T\text{ for }m\in \mathbb{N}\}$.

3. **Theorem 0.0.1 (Caratheodory's Theorem)**: Every point in the convex hull of a set $T\subseteq \mathbb{R}^n$ can be expressed as a convex combination of at most $n+1$ points from $T$. 

4. **Theorem 0.0.2 (Approximate form of Caratheodory's Theorem)**: Consider a set $T\subseteq \mathbb{R}^n$ whose diameter is bounded by $1$. Then, for every point $x\in \mathrm{conv}(T)$ and every integer $k$, one can find points $x_1,\cdots,x_k\in T$ such that
   $$
   \left\Vert x-\frac{1}{k}\sum^{k}_{j=1}x_j\right\Vert^2_2\le \frac{1}{\sqrt{k}}
   $$

5. **Corollary 0.0.4 (Covering polytopes by balls)**: Let $P$ be a polytope in $\mathbb{R}^n$ with $N$ vertices and whose diameter is bounded by $1$. Then $P$ can be covered by at most $N^{\lceil{1}/{\varepsilon^2}\rceil}$ Euclidean balls of radii $\varepsilon>0$.

## Exercises

### Exercise 0.0.3

Check the following variance identities, which we used in the proof of Theorem 0.0.2:

(a) Let $Z_1, \ldots, Z_k$ be independent mean-zero random vectors in $\mathbb{R}^n$. Show that
$$
\mathbb{E}\left\|\sum_{j=1}^k Z_j\right\|_2^2=\sum_{j=1}^k \mathbb{E}\left\|Z_j\right\|_2^2 .
$$
(b) Let $Z$ be a random vector in $\mathbb{R}^n$. Show that
$$
\mathbb{E}\|Z-\mathbb{E} Z\|_2^2=\mathbb{E}\|Z\|_2^2-\|\mathbb{E} Z\|_2^2
$$
*Soln*: routine (write each random vector as a tuple of random variables and remember to use independency and zero-mean).

### Exercise 0.0.5

(The sum of binomial coefficients). Prove the inequalities
$$
\left(\frac{n}{m}\right)^m \leq\left(\begin{array}{c}
n \newline
m
\end{array}\right) \leq \sum_{k=0}^m\left(\begin{array}{l}
n \newline
k
\end{array}\right) \leq\left(\frac{e n}{m}\right)^m
$$
for all integers $m \in[1, n]$.
Hint: To prove the upper bound, multiply both sides by the quantity $(m / n)^m$, replace this quantity by $(m / n)^k$ in the left side, and use the Binomial Theorem.

*Soln*: For the first inequality:
$$
\begin{aligned}
\mathrm{RHS}&=\frac{n!}{(n-m)!m!}=\frac{(n-m+1)\times\cdots\times n}{1\times \cdots\times m}\newline&=\left(\frac{n-m+1}{1}\right)\left(\frac{n-m+2}{2}\right)\cdots\left(\frac{n-1}{m-1}\right)\left(\frac{n}{m}\right)\newline
&\ge \left(\frac{n}{m}\right)\left(\frac{n}{m}\right)\cdots\left(\frac{n}{m}\right)\left(\frac{n}{m}\right)\newline
&=\mathrm{LHS}
\end{aligned}
$$
The second inequality is trivial as the right hand side contains $n\choose m$.

#### Lemma $\lim _{n \rightarrow \infty}\left(1+\frac{x}{n}\right)^n=e^x$

*proof*: 
$$
\begin{aligned}
\lim_{n\to\infty}\left(1+\frac{x}{n}\right)^n&=\lim_{n\to\infty}e^{n \log \left(1+\frac{x}{n}\right)}\newline
&=e^{\lim_{n\to\infty}\frac{\log(1+x/n)}{1/n}}\newline
&=e^{\lim_{n\to\infty}\frac{(-x/n^2)(1/(1+x/n))}{-1/n^2}}\newline
&=e^{\lim_{n\to\infty}\frac{nx}{(x+n)}}\newline
&=e^{\lim_{n\to\infty}\frac{x}{1}}\newline
&=e^x
\end{aligned}
$$
The thrid inequality is then obtained using above lemma:
$$
\sum_{k=0}^m\left(\begin{array}{c}n \newline k\end{array}\right)\left(\frac{m}{n}\right)^m \leq \sum_{k=0}^n\left(\begin{array}{c}n \newline k\end{array}\right)\left(\frac{m}{n}\right)^k=\left(1+\frac{m}{n}\right)^n \leq e^m
$$


### Exercise 0.0.6

(Improved covering). Check that in Corollary 0.0.4,
$$
\left(C+C \varepsilon^2 N\right)^{\left\lceil 1 / \varepsilon^2\right\rceil}
$$
suffice. Here $C$ is a suitable absolute constant. (Note that this bound is slightly stronger than $N^{\left\lceil 1 / \varepsilon^2\right\rceil}$ for small $\varepsilon$.)
Hint: The number of ways to choose $k$ elements from an $N$-element set with repetitions is $\left(\begin{array}{c}N+k-1 \newline k\end{array}\right)$. Simplify using Exercise 0.0.5.

*soln*:

The number of ways to choose $k$ out of $N$ objects with repetition is
$$
\left(\begin{array}{c}
N+k-1 \newline
k
\end{array}\right) .
$$

Then, use inequalities in Exercise 0.0.5 to obtain
$$
\begin{aligned}
\left(\begin{array}{c}
N+k-1 \newline
k
\end{array}\right) & \leq\left[\frac{e(N+k-1)}{k}\right]^k=\left[\frac{e(k-1)}{k}+\frac{e N}{k}\right]^k \newline
& =\left[\frac{e(k-1)}{k}+\frac{e}{k \epsilon^2} \epsilon^2 N\right]^k \leq\left[C_\epsilon\left(1+\epsilon^2 N\right)\right]^{\left\lceil 1 / \epsilon^2\right\rceil}
\end{aligned}
$$
where $C_\epsilon=\frac{e}{\left[1 / \epsilon^2\right] \epsilon^2}$.

# 1. Preliminaries on Random Variables

## Key Takeaways

