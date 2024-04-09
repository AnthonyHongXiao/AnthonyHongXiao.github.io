+++
title = "High-Dimensional Probability and Statistics"
date = "2024-01-14T12:01:56+08:00"
tags = ["probability"]

+++

This file is the first of the two for the notes and exercises in the book Roman Vershynin's [High-Dimensional Probability](/pdfs/HDP-book.pdf), one of the references used in Prof Lunde's Math5440. The other references are Ramon van Handel's [Probability in High Dimension](\pdfs\PHD-book.pdf) and Martin J.Wainwright's [High-Dimensional Statistics](/pdfs/HDS-book.pdf). The file contains chapter 0,1,2,3,4, which cover some of the basic notions. We will use two other reading files for further topics, one for concentration of Lipschitz functions (chapter 5) and one for Random and Empirical Processes (chapter 7 and 8).

Errata and update of HDP: [errata](/pdfs/Vershynin-Errata-2020.pdf), [update](/pdfs/Vershynin-Updates-2020.pdf).

Exercises solns for HDP: [soln](https://zhuanlan.zhihu.com/p/338822722).

Exercises solns for HDS: [soln](https://high-dimensional-statistics.github.io/).

Another handful reference for various conclusions on matrices is *Matrix Analysis* (e2) by Charles R. Johnson and Roger A. Horn.

# 0. Appetizer

## Key Takeaways

1. **convex combination** $\sum\_{i=1}^m \lambda\_i z\_i \quad$ where $\quad \lambda\_i \geq 0 \quad$ and $\quad \sum\_{i=1}^m \lambda\_i=1$.

2. **convex hull of a set $T$**, $\mathrm{conv}(T)$ is the set of all convex combinations of $z\_1, \cdots, z\_m \in T$ for $m \in \mathbb{N}$.

3. **Theorem 0.0.1 (Caratheodory's Theorem)**: Every point in the convex hull of a set $T\subseteq \mathbb{R}^n$ can be expressed as a convex combination of at most $n+1$ points from $T$. 

4. **Theorem 0.0.2 (Approximate form of Caratheodory's Theorem)**: Consider a set $T\subseteq \mathbb{R}^n$ whose diameter is bounded by $1$. Then, for every point $x\in \mathrm{conv}(T)$ and every integer $k$, one can find points $x\_1,\cdots,x\_k\in T$ such that
   $$
   \left\Vert x-\frac{1}{k}\sum^{k}\_{j=1}x\_j\right\Vert^2\_2\le \frac{1}{\sqrt{k}}
   $$

5. **Corollary 0.0.4 (Covering polytopes by balls)**: Let $P$ be a polytope in $\mathbb{R}^n$ with $N$ vertices and whose diameter is bounded by $1$. Then $P$ can be covered by at most $N^{\lceil{1}/{\varepsilon^2}\rceil}$ Euclidean balls of radii $\varepsilon>0$.

## Exercises

### Exercise 0.0.3

Check the following variance identities, which we used in the proof of Theorem 0.0.2:

**(a)** Let $Z\_1, \ldots, Z\_k$ be independent mean-zero random vectors in $\mathbb{R}^n$. Show that
$$
\mathbb{E}\left\Vert\sum\_{j=1}^k Z\_j\right\Vert\_2^2=\sum\_{j=1}^k \mathbb{E}\left\Vert Z\_j\right\Vert\_2^2 .
$$

**(b)** Let $Z$ be a random vector in $\mathbb{R}^n$. Show that
$$
\mathbb{E}\Vert Z-\mathbb{E} Z\Vert\_2^2=\mathbb{E}\Vert Z\Vert\_2^2-\Vert\mathbb{E} Z\Vert\_2^2
$$
*Soln*: routine (write each random vector as a tuple of random variables and remember to use independency and zero-mean).

### Exercise 0.0.5

(The sum of binomial coefficients). Prove the inequalities
$$
\left(\frac{n}{m}\right)^m \leq\left(\begin{array}{c}
n \newline
m
\end{array}\right) \leq \sum\_{k=0}^m\left(\begin{array}{l}
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

#### Lemma $\lim \_{n \rightarrow \infty}\left(1+\frac{x}{n}\right)^n=e^x$

*proof*: 
$$
\begin{aligned}
\lim\_{n\to\infty}\left(1+\frac{x}{n}\right)^n&=\lim\_{n\to\infty}e^{n \log \left(1+\frac{x}{n}\right)}\newline
&=e^{\lim\_{n\to\infty}\frac{\log(1+x/n)}{1/n}}\newline
&=e^{\lim\_{n\to\infty}\frac{(-x/n^2)(1/(1+x/n))}{-1/n^2}}\newline
&=e^{\lim\_{n\to\infty}\frac{nx}{(x+n)}}\newline
&=e^{\lim\_{n\to\infty}\frac{x}{1}}\newline
&=e^x
\end{aligned}
$$
The thrid inequality is then obtained using above lemma:
$$
\sum\_{k=0}^m\left(\begin{array}{c}n \newline k\end{array}\right)\left(\frac{m}{n}\right)^m \leq \sum\_{k=0}^n\left(\begin{array}{c}n \newline k\end{array}\right)\left(\frac{m}{n}\right)^k=\left(1+\frac{m}{n}\right)^n \leq e^m
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
& =\left[\frac{e(k-1)}{k}+\frac{e}{k \varepsilon^2} \varepsilon^2 N\right]^k \leq\left[C\_\varepsilon\left(1+\varepsilon^2 N\right)\right]^{\left\lceil 1 / \varepsilon^2\right\rceil}
\end{aligned}
$$
where $C\_\varepsilon=\frac{e}{\left[1 / \varepsilon^2\right] \varepsilon^2}$.

# 1. Preliminaries on Random Variables

## Key Takeaways

1. **Random Variables**, **expectation** $\mathbb{E}(X)$, **variance** $\mathbb{E}(X-\mathbb{E}(X))^2$, **moment generating function** $M\_X(t)=\mathbb{E}(e^{tX})$, **p-th moment** $\mathbb{E}(X^p)$, **p-th absolute moment** $\mathbb{E}(|X|^p)$, and **$L^P$ norm** and **essential norm** of a random variable
   $$
   \begin{aligned}
   \Vert X\Vert\_{L^p}&=(\mathbb{E}|X|^p)^{1/p}, p\in (0,\infty)\newline
   \Vert X\Vert\_{L^{\infty}}&=\mathrm{ess\; sup}|X|=\inf\{M|\;|f|\le M\text{ for }\mu-\text{a.e. }x\in X\}
   \end{aligned}
   $$

2. For fixed $p$ and a given probability space $(\Omega, \Sigma, \mathbb{P})$, the classical vector space $L^p=L^p(\Omega, \Sigma, \mathbb{P})$ consists of all random variables $X$ on $\Omega$ with finite $L^p$ norm, that is
   $$
   L^p=\set{X:\Vert X\Vert\_{L^p}<\infty}.
   $$

   If $p \in[1, \infty]$, the quantity $\Vert X\Vert\_{L^p}$ is a norm and $L^p$ is a **Banach space**. This fact follows from **Minkowski's inequality**. For $p<1$, the triangle inequality fails and $\Vert X\Vert\_{L^p}$ is not a norm.

   The exponent $p=2$ is special in that $L^2$ is not only a Banach space but also a **Hilbert space**. The inner product and the corresponding norm on $L^2$ are given by
   $$
   \langle X, Y\rangle\_{L^2}=\mathbb{E} X Y, \quad\Vert X\Vert\_{L^2}=\left(\mathbb{E}|X|^2\right)^{1 / 2} .
   $$

   Then the **standard deviation** of $X$ can be expressed as
   $$
   \Vert X-\mathbb{E} X\Vert\_{L^2}=\sqrt{\operatorname{Var}(X)}=\sigma(X) .
   $$

   Similarly, we can express the **covariance** of random variables of $X$ and $Y$ as
   $$
   \operatorname{cov}(X, Y)=\mathbb{E}(X-\mathbb{E} X)(Y-\mathbb{E} Y)=\langle X-\mathbb{E} X, Y-\mathbb{E} Y \rangle\_{L^2} .
   $$

3. **Jensen's Inequality**: for $\varphi:\mathbb{R}\to \mathbb{R}$​ convex, we have
   $$
   \varphi(\mathbb{E}X)\le \mathbb{E}\varphi(X)
   $$

4. **Corollary**: $\Vert X\Vert\_{L^p}$ is an increasing function in $p$, i.e.
   $$
   \Vert X\Vert\_{L^p}\le \Vert X\Vert\_{L^q}\quad \text{for any }0\le p\le q=\infty
   $$

5. **Minkowski's inequality**: for any $p\in [1,\infty]$ and any random variables $X,Y\in L^p$​, we have
   $$
   \Vert X+Y\Vert\_{L^p}\le \Vert X\Vert\_{L^p}+\Vert Y\Vert\_{L^p}
   $$

6. **Cauchy-Schwarz inequality**: for any random variables $X,Y\in L^2$, we have
   $$
   |\mathbb{E}XY|\le \Vert X\Vert\_{L^2}\Vert Y\Vert\_{L^2}
   $$

7. **Holder inequality**: suppose $p,q\in (1,\infty)$ such that $1/p+1/q=1$, i.e., they are **conjugate exponents**. The random variables $X\in L^p$ and $Y\in L^q$​ satisfy
   $$
   |\mathbb{E}XY|\le \Vert X\Vert\_{L^p}\Vert Y\Vert\_{L^q}
   $$
   The inequality also holds for the pair $p=1,q=\infty$.

8. Definition of **distribution**, **propability density function (pdf)**, and **cumulative distribution function (cdf)**.

9. **Lemma 1.2.1 (Integral identity)**. Let $X$ be a non-negative random variable. Then
   $$
   \mathbb{E} X=\int\_0^{\infty} \mathbb{P}\{X>t\} d t .
   $$

   The two sides of this identity are either finite or infinite simultaneously.

10. **Exercise 1.2.2 (Generalization of integral identity)**. for any random variable $X$ (not necessarily non-negative):
    $$
    \mathbb{E} X=\int\_0^{\infty} \mathbb{P}\{X>t\} d t-\int\_{-\infty}^0 \mathbb{P}\{X<t\} d t
    $$

11. **Exercise 1.2.3 ( $p$-moments via tails)**. Let $X$ be a random variable and $p \in(0, \infty)$. Show that
    $$
    \mathbb{E}|X|^p=\int\_0^{\infty} p t^{p-1} \mathbb{P}\{|X|>t\} d t
    $$
    whenever the right hand side is finite.

12. **Proposition 1.2.4 (Markov's Inequality)**. For any non-negative random variable $X$ and $t>0$, we have
    $$
    \mathbb{P}\{X \geq t\} \leq \frac{\mathbb{E} X}{t}
    $$

13. **Corollary 1.2 .5 (Chebyshev's inequality)**. Let $X$ be a random variable with mean $\mu$ and variance $\sigma^2$. Then, for any $t>0$, we have
    $$
    \mathbb{P}\{|X-\mu| \geq t\} \leq \frac{\sigma^2}{t^2}
    $$

14. Some formulae:

    **Expectation and Variance of linear comb.**
    $$
    \begin{aligned}
    &\mathbb{E}(aX+b)=a\mathbb{E}(X)+b\newline
    &\operatorname{Var}(aX+b)=a^2\operatorname{Var}(X)\newline
    \end{aligned}
    $$
    **Proposition (Ross (e8) p.129, p.191)**: The expectation of function of random variable is given by
    $$
    \begin{aligned}
    \mathbb{E}[g(X)]&=\sum\_xg(x)p(x)\newline
    \mathbb{E}[g(X)]&=\int\_{-\infty}^{\infty}g(x)f(x)dx
    \end{aligned}
    $$
    **Proposition (Ross (e8) p.298)**: if $X$ and $Y$ have a joint probability mass function $p(x,y)$, then
    $$
    \mathbb{E}[g(X,Y)]=\sum\_y\sum\_x g(x,y)p(x,y)
    $$
    If they have joint probability density function $f(x,y)$, then
    $$
    \mathbb{E}[g(X,Y)]=\int\_{-\infty}^{\infty}\int\_{-\infty}^{\infty}g(x,y)f(x,y)dxdy
    $$
    **Corollary (Ross e8 p.299)**: for finite $X,Y$ and $g(X,Y)=X+Y$, we have $\mathbb E(X+Y)=\mathbb E(X)+\mathbb E(Y)$.

    **Variance of sum of var.**: if they are independent,
    $$
    \operatorname{Var}(X\_1+\cdots+X\_n)=\operatorname{Var}(X\_1)+\cdots+\operatorname{Var}(X\_n)
    $$
    if they are also identically distributed,
    $$
    \operatorname{Var}\left(\frac{1}{N} \sum\_{i=1}^N X\_i\right)=\frac{\sigma^2}{N}
    $$
    For more formulae, see Ross (e8) p.322 section 7.4 Covariance, Variance of Sums, and Correlations.

15. **Theorem 1.3.1 (Strong law of large numbers)**. Let $X\_1, X\_2, \ldots$ be a sequence of i.i.d. random variables with mean $\mu$. Consider the sum
    $$
    S\_N=X\_1+\cdots +X\_N .
    $$

    Then, as $N \rightarrow \infty$,
    $$
    \frac{S\_N}{N} \rightarrow \mu \quad \text { almost surely. }
    $$
    That is, **converges in probability**: for any $\varepsilon>0$,
    $$
    \lim\_{N\to \infty}\mathbb{P}\left(\left|\frac{S\_N}{N}-\mu\right|\le \varepsilon\right)=1
    $$

16. **Theorem 1.3.2 (Lindeberg-Lévy central limit theorem)**. Let $X\_1, X\_2, \ldots$ be a sequence of i.i.d. random variables with mean $\mu$ and variance $\sigma^2$. Consider the sum
    $$
    S\_N=X\_1+\cdots+X\_N
    $$
    and normalize it to obtain a random variable with zero mean and unit variance as follows:
    $$
    Z\_N:=\frac{S\_N-\mathbb{E} S\_N}{\sqrt{\operatorname{Var}\left(S\_N\right)}}=\frac{1}{\sigma \sqrt{N}} \sum\_{i=1}^N\left(X\_i-\mu\right) .
    $$

    Then, as $N \rightarrow \infty$,
    $$
    Z\_N \rightarrow N(0,1) \text { in distribution. }
    $$

    That is, **converges in distribution**: for a sequence of r.v. $X\_i$ with their cdf $F\_{X\_i}$, one has pointwise convergence of $F\_{X\_i}$ to cdf $F\_X$ of a r.v. $X$:
    $$
    \forall x,\lim\_{N\to \infty}F\_i(x)=F(x)
    $$
    The convergence in distribution means that the $\mathrm{CDF}$ of the normalized sum converges pointwise to the CDF of the standard normal distribution. We can express this in terms of tails as follows. Then for every $t \in \mathbb{R}$, we have
    $$
    \mathbb{P}\set{Z\_N \geq t} \rightarrow \mathbb{P}\{g \geq t\}=\frac{1}{\sqrt{2 \pi}} \int\_t^{\infty} e^{-x^2 / 2} d x
    $$
    as $N \rightarrow \infty$, where $g \sim N(0,1)$​ is a standard normal random variable.

17. **Corollary (de Moivre-Laplace theorem)**: 

    One remarkable special case of the central limit theorem is where $X\_i$ are Bernoulli random variables with some fixed parameter $p \in(0,1)$, denoted
    $$
    X\_i \sim \operatorname{Ber}(p) .
    $$

    Recall that this means that $X\_i$ take values 1 and 0 with probabilities $p$ and $1-p$ respectively; also recall that $\mathbb{E} X\_i=p$ and $\operatorname{Var}\left(X\_i\right)=p(1-p)$. The sum
    $$
    S\_N:=X\_1+\cdots+X\_N
    $$
    is said to have the binomial distribution $\operatorname{Binom}(N, p)$. The central limit theorem (Theorem 1.3.2) yields that as $N \rightarrow \infty$,
    $$
    \frac{S\_N-N p}{\sqrt{N p(1-p)}} \rightarrow N(0,1) \text { in distribution. }
    $$

18. **Corollary (Poisson limit theorem)**: 

    Theorem 1.3.4 (Poisson Limit Theorem). Let $X\_{N, i}, 1 \leq i \leq N$, be independent random variables $X\_{N, i} \sim \operatorname{Ber}\left(p\_{N, i}\right)$, and let $S\_N=\sum\_{i=1}^N X\_{N, i}$. Assume that, as $N \rightarrow \infty$,
    $$
    \max\_{i \leq N} p\_{N, i} \rightarrow 0 \quad \text{ and } \quad \mathbb{E} S\_N=\sum\_{i=1}^N p\_{N, i} \rightarrow \lambda<\infty .
    $$

    Then, as $N \rightarrow \infty$,
    $$
    S\_N \rightarrow \operatorname{Pois}(\lambda) \quad\text { in distribution. }
    $$

# 2. Concentration of Sums of Independent Random Variables

## Key Takeaways

### 2.1 Why Concentration Inequalities?

- An example (Question 2.1.1) on estimation of number of heads of flipping coins by Chebyshev's inequality and central limit theorem.

- Our Math5440 gives some more examples (see Lecture 2).

### 2.2 Hoeffding's Inequality

- symmetric Bernoulli distribution is the uniform distribution for discrete variable $X$ that takes values $1$ and $-1$, i.e., $\mathbb{P}(X=1)=\mathbb{P}(X=-1)=\frac{1}{2}$.

**Theorem 2.2.2 (Hoeffding's Inequality)**: Let $X\_1,\cdots,X\_N$ be independent symmetric Bernoulli random variables, and let $a=(a\_1,\cdots,a\_N)\in \R^N$. Then, for any $t>0$, we have
$$
\mathbb{P}\left[\sum\_{i=1}^Na\_iX\_i\ge t\right]\le \mathbb P\left(-\frac{t^2}{2\Vert a\Vert\_2^2}\right)
$$
**Remark 2.2.4 (Non-asymptotic results)**: Note that CLT gives a bound of tail that works for large $N$​, while Hoeffding bound gets rid of that requirement.

Two generalizations are given:

**Theorem 2.2.5 (Two sided Hoeffding's inequality)** Let $X\_i$ and $a$ be the same. Then, for $t>0$,
$$
\mathbb{p}\left[\left|\sum\_{i=1}^Na\_iX\_i\right|\ge t\right]\le 2\exp\left(-\frac{t^2}{2\Vert a\Vert\_2^2}\right)
$$
**Theorem 2.2.6 (Hoeffding's inequaity for general bounded random variables)** Let $X\_1,\cdots,X\_N$ be independent random variables. Assume that $X\_i\in [m\_i,M\_i]$ for every $i$. Then, for any $t>0$, we have
$$
\mathbb{P}\left[\sum\_{i=1}^N(X\_i-\mathbb{E}X\_i)\ge t\right]\le \exp\left(-\frac{2t^2}{\sum\_{i=1}^N(M\_1-m\_1)^2}\right)
$$

### 2.3 Chernoff's Inequality

**Theorem 2.3.1 (Chernoff's inequality (upper tail))**

Let $X\_i$ be independent Bernoulli random variables with parameters $p\_i$. Consider their sum $S\_N=\sum\_{i=1}^NX\_i$ and denote its mean by $\mu=\mathbb{E}S\_N$. Then, for $t>\mu$, we have
$$
\mathbb{E}[S\_N\le t]\le e^{-\mu}\left(\frac{e\mu}{t}\right)^t
$$
**Exercise 2.3.2 (Chernoff's inequality (lower tail))**

Let $X\_i$ and $S\_N$ be the same. When $t<\mu$, we have
$$
\mathbb{E}[S\_N\le t]\le e^{-\mu}\left(\frac{e\mu}{t}\right)^t
$$
**Exercise 2.3.3 (Poisson tail)**

Let $X\sim \mathrm{Pois}(\lambda)$. When $t>\lambda$, we have
$$
\mathbb{E}[X\le t]\le e^{-\lambda}\left(\frac{e\lambda}{t}\right)^t
$$
**Exercise 2.3.6 (Poisson dist. near the mean)**

Let $X\sim \mathrm{Pois}(\lambda)$. When $t\in (0,\lambda]$, we have
$$
\mathbb{P}[|X-\mu|\ge t]\le 2\exp\left(-\frac{ct^2}{\lambda}\right)
$$
**Exercise 2.3.7 (Normal approximation to Poisson)**

Let $X\sim \mathrm{Pois}(\lambda)$. As $\lambda\to \infty$, we have
$$
\frac{X-\lambda}{\sqrt{\lambda}}\to N(0,1)\quad\text{in distribution}
$$

### 2.4 Application: Degrees of Random Graphs

### 2.5 Sub-Gaussian Distributions

If $X\sim N(0,1)$, then for $p\ge 1$,

- $\mathbb{P}[|X|\ge t]\le 2\exp(-t^2/2)\quad \forall t\in R$​.
- $\Vert X\Vert\_{L^p}=(\mathbb{E}|X|^p)^{1/p}=\sqrt{2}\left(\frac{\Gamma((1+p)/2)}{\Gamma(1/2)}\right)^{1/p}$.
- $\Vert X\Vert\_{L^P}=O(\sqrt{p}),\quad  p\to \infty$.
- Its MGF is given by $\mathbb{E}(e^{tX})=e^{t^2/2},\quad \forall t\in \R$.

#### Some facts about Beta and Gamma functions

(Rudin's *Introduction to Mathematical Analysis* (e3) p.192 has some of the following properties.)

- Beta Function $B(x,y)=\int\_0^1 t^{x-1}(1-t)^{y-1}dt$. This indefinite integral is convergent for  $x>0,y<0$.

- Gamma Function $\Gamma(x)=\int\_0^{+\infty}t^{x-1}e^{-t}dt$. This indefinite integral is convergent for $x>0$.

- property 1: for $0<x<\infty$, $\Gamma (x+ 1) = x\Gamma(x)$.

- property 2: $\Gamma(n)=n!$ for $n=1,2,3,\cdots$.

- property 3: $\log \Gamma$ is convex on $(0,\infty)$.

- property 4: if $x>0$ and $y>0$, then
  $$
  B(x,y)=\int\_0^1 t^{x-1}(1-t)^{y-1}dt=\frac{\Gamma(x)\Gamma(y)}{\Gamma(x+y)}
  $$

- property 5: both $\Beta$ and $\Gamma$ are continuous on their convergent regions.

- property 6 (**Stirling's Formula**): 
  $$
  \lim \_{x \rightarrow \infty} \frac{\Gamma(x+1)}{(x / e)^x \sqrt{2 \pi x}}=1
  $$

- Property 6' (**Stirling's Formula**):
  $$
  \Gamma(x)=\sqrt{\frac{2\pi}{x}}\left(\frac{x}{e}\right)^x(1+o(1/x))
  $$

- Property 7 (**Stirling's Approximation**): for $n\ge 1$,
  $$
  \sqrt{2 \pi n}\left(\frac{n}{e}\right)^n e^{\frac{1}{12 n+1}}<n !<\sqrt{2 \pi n}\left(\frac{n}{e}\right)^n e^{\frac{1}{12 n}}
  $$
  
- Property 8: for any $x\ge 1/2$, $\Gamma(x)\le 3x$.

#### Sub-Gaussian variable

A zero-mean random variable $X$ is **sub-Gaussian** with parameter $\sigma^2$, or $\operatorname{subGaussian}\left(\sigma^2\right)$, if there exists $\sigma^2 \geq 0$ such that:
$$
E\left(e^{\lambda X}\right) \leq e^{\frac{\lambda^2 \sigma^2}{2}} \text { for all } \lambda \geq 0
$$

In other words, a random variable is sub-Gaussian if its MGF is upperbounded by an MGF of some Gaussian random variable with variance $\sigma^2$. It should be noted that the parameter $\sigma^2$ is generally not the variance of a subGaussian random variable (it is the variance of a Gaussian that has a larger MGF). If this property holds, we have that:
$$
\begin{aligned}
P(X-\mu \geq t) & \leq \inf\_{\lambda>0} E\left(e^{\lambda(X-\mu)}\right) e^{-\lambda t} \newline
& \leq \inf\_{\lambda>0} \exp \left(\frac{\lambda^2 \sigma^2}{2}-\lambda t\right) \newline
& \left.=\exp \left(\frac{t^2}{2 \sigma^2}-\frac{t^2}{\sigma^2}\right) \text { (plugging in minimizer } \lambda=t / \sigma^2\right) \newline
& =\exp \left(\frac{-t^2}{2 \sigma^2}\right)
\end{aligned}
$$

Therefore, if a random variable is sub-Gaussian, we have tail decay of the form $\exp \left(-t^2 / 2 K\_1^2\right)$, which is quite fast. One can show an analogous bound for the left tail. So what random variables are sub-Gaussian? It turns out that bounded random variables are sub-Gaussian.

**Proposition 1**. Suppose $X$ is mean 0 and $a \leq X \leq b$ with probability 1. Then, $X$ is sub-Gaussian with $\sigma^2=(b-a)^2 / 4$.

In what follows, let $K\_i$ be the sub-Gaussian constant associated with the $i$-th notion of sub-Gaussianity. It turns out that different notions of sub-Gaussianity are equivalent in the sense that they are related to each other by some universal constant. In other words, if $X ∼ \mathrm{subGaussian}(K\_i)$, then there exists some constant $C$ (that does not depend on the distribution of $X$) such that $X ∼ \mathrm{subGaussian}(CK\_j)$ for an equivalent notion of sub-Gaussianity. Another way of saying this is that for any $i,j=1,\cdots,5$, there is some absolute constant $C$ such that $K\_i\le CK\_j$.

**Proposition 2.5.2 (Sub-Gaussian Properties)**: Let $X$ be a random variable. Then the following properties are equivalent.

(i) The tails of $X$ satisfy
$$
\mathbb{P}[|X| \geq t] \leq 2 \exp \left(-t^2 / K\_1^2\right) \quad \text { for all } t \geq 0 .
$$
(ii) The moments of $X$ satisfy
$$
\Vert X\Vert\_{L^p}=\left(\mathbb{E}|X|^p\right)^{1 / p} \leq K\_2 \sqrt{p} \quad \text { for all } p \geq 1 .
$$
(iii) The MGF of $X^2$ satisfies
$$
\mathbb{E} [\exp \left(\lambda^2 X^2\right)] \leq \exp \left(K\_3^2 \lambda^2\right) \quad \text { for all } \lambda \text { such that }|\lambda| \leq \frac{1}{K\_3} \text {. }
$$
(iv) The MGF of $X^2$ is bounded at some point, namely
$$
\mathbb{E} [\exp \left(X^2 / K\_4^2\right)] \leq 2 .
$$

Moreover, if $\mathbb{E} X=0$ then properties $i$-iv are also equivalent to the following one.
(v) The MGF of $X$ satisfies
$$
\mathbb{E} [\exp (\lambda X)] \leq \exp \left(K\_5^2 \lambda^2\right) \quad \text { for all } \lambda \in \mathbb{R}
$$
**Orlicz Norm** and **Sub-Gaussian Norm**:

Suppose that $\Psi:[0, \infty) \mapsto[0, \infty)$ is a monotone increasing, convex function such that $\Psi(0)=0$ and $\lim\_{x \to \infty} \Psi(x)=\infty$. The **Orlicz space** $L\_\psi =L\_\psi (\Omega,\Sigma,\mathbb P)$ consists of all random variables $X$ on the probability space $(\Omega,\Sigma,\mathbb P)$ with finite Orlicz norm, i.e., $L\_\psi :=\{X:\Vert X\Vert\_{\psi}<\infty\}$ where the **Orlicz norm** of a random variable $X$ is given by
$$
|X|\_{\Psi}=\inf \newline{t>0: \mathbb{E}\left[\Psi\left(|X|/t\right)\right] \leq 1\newline}
$$

It can be shown that this is indeed a norm on the space of random variables for which this quantity is finite. When we put $\psi(x)=x^p$ for $p\ge 1$, the resulting Orlicz space is the classical space $L^p$.  It can also shown that for the choice of function $\psi\_2(x)=e^{x^2}-1$, the sub-Gaussian condition:
$$
\mathbb E\left(\exp \left(X^2 / K\_4^2\right)\right) \leq 2
$$
is equivalent to:
$$
\Vert X\Vert\_{\psi\_2} \leq K\_4
$$

We let this **sub-Gaussian norm** of a sub-Gaussian be specifically denoted as
$$
\Vert X\Vert\_{\psi\_2}=\inf \{t>0:\mathbb E\exp(X^2/t^2)\le 2\}
$$
 Other restatements of sub-Gaussianities using the norm are given in (2.14)-(2.16):
$$
\begin{gathered}
\mathbb{P}\{|X| \geq t\} \leq 2 \exp \left(-c t^2 /\Vert X\Vert\_{\psi\_2}^2\right) \quad \text { for all } t \geq 0 \newline
\Vert X\Vert\_{L^p} \leq C\Vert X\Vert\_{\psi\_2} \sqrt{p} \quad \text { for all } p \geq 1 \newline
\mathbb{E} \exp \left(X^2 /\Vert X\Vert\_{\psi\_2}^2\right) \leq 2 \newline
\text{if }\mathbb{E} X=0\text{ then }\mathbb{E} \exp (\lambda X) \leq \exp \left(C \lambda^2\Vert X\Vert\_{\psi\_2}^2\right) \quad\forall \lambda \in \mathbb{R}
\end{gathered}
$$

where $c,C$ are absolute constants. Morover, up to absolute constant factors, $\Vert X\Vert\_{\psi\_2}$ is the smallest possible number that makes each of these inequalities holds. 

**Examples and non-examples of sub-gaussian r.v.**

(i) **Gaussian** ☑️: Due to equation (2.3) from the book and symmetry, we have that for for $X\sim N(0,1)$ and any $p\ge 1$, $\mathbb{P}[|X|\ge t]\le 2\exp(-t^2/2)\quad \forall t\in R$ . Therefore, it is sub-Gaussian. In fact, if $X\sim N(0,\sigma^2)$, we recall that the MGF of $X\sim N(\mu,\sigma^2)$ is $\exp (\mu t+\sigma^2t^2/2)$. For $\mu=0$, this is $\exp (\sigma^2t^2/2)$. Criterion (v) of Proposition 2.5.2 then concludes that it is sub-Gaussian.

(ii) **Bernoulli** ☑️: Let $X$ be a random variable with symmetric Bernoulli distribution. Since $|X|=1$, it follows that $X$ is a sub-Gaussian random variable with $\Vert X\Vert\_{\psi\_2}=\frac{1}{\sqrt{\ln 2}}$. Just note that when $t\ge 1$, we have
$$
\mathbb P[|X|\ge t\]=0\le 2\exp(-t^2/K^2\_1)
$$
When $t<1$, we have
$$
\mathbb P[|X|\ge t]=1
$$
By letting $K\_1=\frac{1}{\sqrt{\ln 2}}$​ and noticing that $t<1\Rightarrow -t^2>-1$, we have 
$$
2\exp \left(-\frac{t^2}{-\frac{1}{\ln 2}}\right)=2\cdot 2^{-t^2}>2\cdot 2^{-1}=1= \mathbb P[|X|\ge t]
$$
(iii) **Bounded** ☑️: More generally, any bounded random variable $X$ is a sub-Gaussian random variable with
$$
\Vert X\Vert\_{\psi\_2}\le C\Vert X\Vert\_{\infty}
$$
where $C=1/\sqrt{\ln 2}$.

(iv) **Poisson** ❌: let $X\sim \mathrm{Pois}(\lambda)$. Note that $X=k=0,1,\cdots$ Then its pmf is
$$
f(k ; \lambda)=\mathbb P(X=k)=\frac{\lambda^k e^{-\lambda}}{k !}
$$
Now, let $m$ be the smallest integer that is larger or equal to $t$. Then
$$
\mathbb P(|X|\ge t)=\mathbb P(X \geq t)=\sum\_{k\ge t}\mathbb P(X=k)>\frac{e^{-\lambda} \lambda^m}{m !}
$$
Then apply Stirling's approximation to get a lower bound that decay slower than Gaussian.

(v) **Exponential** ❌: let $X\sim \mathrm{Exp}(\lambda)$. Then,
$$
f(x ; \lambda)= \begin{cases}\lambda e^{-\lambda x} & x \geq 0 \newline 0 & x<0\end{cases}
$$
We have its moment
$$
\mathbb E[|X|^p]=\mathbb E[X^p]=\frac{p!}{\lambda^p}
$$
Thus,
$$
(\mathbb E|X|^p)^{1/p}=\frac{(p!)^{1/p}}{\lambda}
$$
Then by lemma below, it cannot satisfy the second criterion of Proposition 2.5.2.

**Lemma**: By rearranging terms, we can see that
$$
(n !)^2=[1 \cdot n][2 \cdot(n-1)][3 \cdot(n-2)] \cdots[(n-1) \cdot 2][n \cdot 1] .
$$

Each of the $n$ products $(k+1) \cdot(n-k)$, for $0 \leq k<n$, is $\geq n$. Thus $(n !)^2 \geq n^n$ and therefore $(n !)^{1 / n} \geq \sqrt{n}$. 

(vi) **Pareto** ❌: It is one of those heavy-tailed dist. Its pdf is $f(x)=\frac{\alpha x\_m^{\alpha}}{x^{\alpha+1}}$, and its cdf is $1-\left(\frac{x\_m}{x}\right)^{\alpha}$. Thus,
$$
\mathbb P[|X|\ge t]=\mathbb P[X\ge t]=\left(\frac{x\_m}{x}\right)^{\alpha}
$$
It is easy to see that the polynomial decay is slower than the gaussian one.

(vii) **Cauchy** ❌: Another heavy-tailed dist. Compare its growth to gaussian.

### 2.6 General Hoeffding and Khintchine Inequalities

The **rotation invariance property** (i.i.d $X\_i\sim N(0,\sigma\_i^2)\Rightarrow\sum{i=1}^NX\_i\sim N\left(0,\sum^N\_{i=1}\sigma\_i^2\right)$)  extends to the sub-Gaussians, albeit up to an absolute constant.

**Proposition 2.6.1 (Sums of independent sub-Gaussians)**: Let $X\_1,\cdots,X\_N$ be independent sub-Gaussians with zero-means. Then $\sum\_{i=1}^NX\_i$ is also a sub-Gaussian r.v., and
$$
\left\Vert \sum\_{i=1}^N X\_i^2 \right\Vert\_{\psi\_2}^2\le C\sum\_{i=1}^N\Vert X\_i\Vert\_{\psi\_2}^2
$$
where $C$ is an absolute constant.

**Theorem 2.6.3 (General Hoeffding's inequality)**. Let $X\_1, \ldots, X\_N$ be independent, mean zero, sub-gaussian random variables, and $a=\left(a\_1, \ldots, a\_N\right) \in \mathbb{R}^N$. Then, for every $t \geq 0$, we have
$$
\mathbb{P}\left[\left|\sum\_{i=1}^N a\_i X\_i\right| \geq t\right] \leq 2 \exp \left(-\frac{c t^2}{K^2\Vert a\Vert\_2^2}\right)
$$

where $K=\max\_i \Vert X\_i\Vert\_{\psi\_2}$​.

**Theorem 2.6.2**: when $a=(1,\cdots,1)$​​ in Theorem 2.6.3 above.

When the means are not zero, we can show that centering does not harm the sub-Gaussian property, just as $\Vert X-\mathbb X\Vert\_{L^2}\le \Vert X\Vert\_{L^2}$:

**Lema 2.6.8 (Centering)** If $X$ is sub-Gaussian then $X-\mathbb E X$ is sub-Gaussian too and
$$
\Vert X-\mathbb EX\Vert\_{\psi\_2}\le C\Vert X\Vert\_{\psi\_2}
$$
where $C$ is an absolute constant.

**Exercise 2.6.5 (Khintchine's inequality).** Let $X\_1, \ldots, X\_N$ be independent sub-gaussian random variables with zero means and unit variances, and let $a=$ $\left(a\_1, \ldots, a\_N\right) \in \mathbb{R}^N$. Prove that for every $p \in[2, \infty)$ we have

$$
\left(\sum\_{i=1}^N a\_i^2\right)^{1 / 2} \le \left\Vert \sum\_{i=1}^N a\_i X\_i\right\Vert\_{L^p} \leq C K \sqrt{p}\left(\sum\_{i=1}^N a\_i^2\right)^{1 / 2}
$$

where $K=\max\_i\left\Vert X\_i\right\Vert\_{\psi\_2}$ and $C$ is an absolute constant.

**Exercise 2.6.6 (Khintchine's inequality for $p=1$ ).** Show that in the setting of Exercise 2.6.5, we have
$$
c(K)\left(\sum\_{i=1}^N a\_i^2\right)^{1 / 2} \leq\left\Vert\sum\_{i=1}^N a\_i X\_i\right\Vert\_{L^1} \leq\left(\sum\_{i=1}^N a\_i^2\right)^{1 / 2} .
$$

Here $K=\max\_i\left\Vert X\_i\right\Vert\_{\psi\_2}$ and $c(K)>0$ is a quantity which may depend only on $K$.
Hint: Use the following extrapolation trick. Prove the inequality $\Vert Z\Vert\_2 \leq\Vert Z\Vert\_1^{1 / 4}\Vert Z\Vert\_3^{3 / 4}$ and use it for $Z=\sum a\_i X\_i$. Get a bound on $\Vert Z\Vert\_3$ from Khintchine's inequality for $p=3$.

**Exercise 2.6.7 (Khintchine's inequality for $p \in(0,2)$ ).** State and prove a version of Khintchine's inequality for $p \in(0,2)$​.
Hint: Modify the extrapolation trick in Exercise 2.6.6.

### 2.7 Sub-Exponential Distributions

We previously stated that some common families of random variables are not sub-Gaussian. Consider for example the $\chi^2$ distribution, which comes up with some frequency in statistics. Recall that if $Z \sim N(0,1)$, then $Z^2 \sim \chi\_1^2$. Thus, for a $\chi^2$ random variable $Y$, we have that:
$$
P(|Y| \geq t)=P\left(Z^2 \geq t\right)=2 P(Z \geq \sqrt{t}) \leq 2 \exp \left(-\frac{t}{2}\right)
$$

Therefore, $\chi^2$ random variables have tails that decay like $\exp (-C t)$ (**exponential decay**) rather than $\exp \left(-C t^2\right)$ (**gaussian decay**) as we have with Gaussian random variables. It turns out that $\chi^2$ random variables are an example of sub-exponential random variables.

**Proposition 2.7.1 (Sub-exponential properties).** Let $X$ be a random variable. Then the following properties are equivalent; the parameters $K\_i>0$ appearing in these properties differ from each other by at most an absolute constant factor.

(i) The tails of $X$ satisfy
$$
\mathbb{P}\{|X| \geq t\} \leq 2 \exp \left(-t / K\_1\right) \quad \text { for all } t \geq 0 .
$$
(ii) The moments of $X$ satisfy
$$
\Vert X\Vert\_{L^p}=\left(\mathbb{E}|X|^p\right)^{1 / p} \leq K\_2 p \quad \text { for all } p \geq 1 .
$$
(iii) The $M G F$ of $|X|$ satisfies
$$
\mathbb{E} \exp (\lambda|X|) \leq \exp \left(K\_3 \lambda\right) \quad \text { for all } \lambda \text { such that } 0 \leq \lambda \leq \frac{1}{K\_3} \text {. }
$$
(iv) The MGF of $|X|$ is bounded at some point, namely
$$
\mathbb{E} \exp \left(|X| / K\_4\right) \leq 2
$$

Moreover, if $\mathbb{E} X=0$ then properties $a-d$ are also equivalent to the following one.
(v) The MGF of $X$ satisfies
$$
\mathbb{E} \exp (\lambda X) \leq \exp \left(K\_5^2 \lambda^2\right) \quad \text { for all } \lambda \text { such that }|\lambda| \leq \frac{1}{K\_5}
$$
**Definition 2.7.5 (Sub-exponential random variables).** A random variable $X$ that satisfies one of the equivalent properties (i)-(iv) Proposition 2.7.1 is called a **sub-exponential random variable**. The sub-exponential norm of $X$, denoted $\Vert X\Vert\_{\psi\_1}$, is defined to be the smallest $K\_3$ in property 3. In other words,
$$
\Vert X\Vert\_{\psi\_1}=\inf \{t>0: \mathbb{E} \exp (|X| / t) \leq 2\} .
$$

Sub-gaussian and sub-exponential distributions are closely related. First, any sub-gaussian distribution is clearly sub-exponential.

Second, the square of a sub-gaussian random variable is sub-exponential (**Lemma 2.7.6**); more generally, the product of two sub-gaussian random variables is sub-exponential (**Lemma 2.7.7**).

**Example 2.7.8 (sub-exponentials)** Let us mention a few examples of sub-exponential random variables. As we just learned, all sub-gaussian random variables and their squares are sub-exponential, for example $g^2$ for $g\sim N(\mu,\sigma)$​. Apart from that, sub-exponential distributions include the exponential and Poisson distributions. 

**Exercise 2.7.10 (Centering)** With a similar proof as Lemma 2.6.8, we can show that for sub-exponential $X$,
$$
\Vert X-\mathbb E X\Vert\_{\psi\_1}\le C\Vert X\Vert\_{\psi\_1}
$$

### 2.8-2.9 Bernstein's inequality, bounded difference inequality, and Bennett's inequality

**Theorem 2.8.1 (Bernstein's inequality)**

Let $X\_1,\cdots,X\_N$ be independent mean-zero sub-exponential random vairables. Then, for every $t\ge 0$, we have
$$
\mathbb P\left[\left|\sum\_{i=1}^NX\_i\right|\ge t\right]\le 2\exp\left(-c \min\left(\frac{t^2}{\sum\_{i=1}^N \Vert X\_i\Vert\_{\psi\_1}^2},\frac{t}{\max\_i\Vert X\_i\Vert\_{\psi\_i}}\right)\right)
$$
 where $c>0$ is an absolute constant and $2$ is due to absolute sign.

**Theorem 8.2 (Bernstein's inequality: restatement)**

Ley those $X\_i$ be the same. Let $a=(a\_1,\cdots,a\_N)\in \mathbb R^N$. Then, for every $t\ge 0$, we have
$$
\mathbb P\left[\left|\sum\_{i=1}^Na\_iX\_i\right|\ge t\right]\le 2\exp\left(-c \min\left(\frac{t^2}{K^2\Vert a\Vert\_2^2},\frac{t}{K \Vert a\Vert\_{\infty}}\right)\right)
$$
where $K=\max\_i\Vert X\_i\Vert\_{\psi\_1}$​.

By plugging in $a\_i=1/N$ we get a simpler form (**Corollary 2.8.3**).

**Theorem 2.8.4 (Bernstein's inequality for bounded distributions).** Let $X\_1, \ldots, X\_N$ be independent, mean zero random variables, such that $\left|X\_i\right| \leq K$ all $i$. Then, for every $t \geq 0$, we have
$$
\mathbb{P}\left[\left|\sum\_{i=1}^N X\_i\right| \geq t\right] \leq 2 \exp \left(-\frac{t^2 / 2}{\sigma^2+K t / 3}\right) .
$$

Here $\sigma^2=\sum\_{i=1}^N \mathbb{E} X\_i^2$​ is the variance of the sum.

**Theorem 2.9.1 (Bounded differences inequality).** Let $X\_1, \ldots, X\_N$ be independent random variables. ${ }^{10}$ Let $f: \mathbb{R}^n \rightarrow \mathbb{R}$ be a measurable function. Assume that the value of $f(x)$ can change by at most $c\_i>0$ under an arbitrary change of $a$ single coordinate of $x \in \mathbb{R}^n$. Then, for any $t>0$, we have
$$
\mathbb{P}\{f(X)-\mathbb{E} f(X) \geq t\} \leq \exp \left(-\frac{2 t^2}{\sum\_{i=1}^N c\_i^2}\right)
$$
where $X=\left(X\_1, \ldots, X\_n\right)$.
Another result worth mentioning is Bennett's inequality, which can be regarded as a generalization of Chernoff's inequality.

**Theorem 2.9 .2 (Bennett's inequality).** Let $X\_1, \ldots, X\_N$ be independent random variables. Assume that $\left|X\_i-\mathbb{E} X\_i\right| \leq K$ almost surely for every $i$. Then, for any $t>0$, we have
$$
\mathbb{P}\left[\sum\_{i=1}^N\left(X\_i-\mathbb{E} X\_i\right) \geq t\right] \leq \exp \left(-\frac{\sigma^2}{K^2} h\left(\frac{K t}{\sigma^2}\right)\right)
$$

where $\sigma^2=\sum\_{i=1}^N \operatorname{Var}\left(X\_i\right)$ is the variance of the sum, and $h(u)=(1+u) \log (1+$ $u)-u$.

### Tensorization of Variance

In what follows, let $X\_1, \ldots, X\_n$ be independent but not necessarily identically distributed random variables. Furthermore, let:
$$
\operatorname{Var}\_i f\left(x\_1, \cdots, x\_n\right)=\mathrm{Var}(f(x\_1, \cdots, X\_i, \cdots, x\_n))
$$

denote the variance of $f\left(x\_1, \ldots, x\_n\right)$ treating all random variables other than $X\_i$ as fixed. We have the following inequality:

**Theorem 1 (Tensorization of Variance)**. Suppose that $X\_1, \ldots, X\_n$ are independent random variables. Then,
$$
\operatorname{Var}\left(f\left(X\_1, \ldots, X\_n\right)\right) \leq \sum\_{i=1}^n \mathbb{E}\left[\operatorname{Var}\_i f\left(x\_1, \ldots, x\_n\right)\right]
$$

We can combine this result with the variance bound for bounded random variables to derive an inequality that is easier to apply. Suppose that for each fixed $x\_{-i}=\left(x\_1, \ldots x\_{i-1}, x\_{i+1}, \ldots, x\_n\right)$, we have that:
$$
\sup\_{x, y}|f\left(x\_1, \ldots, x\_{i-1}, x, x\_{i+1}, \ldots, x\_n\right)-f\left(x\_1, \ldots, x\_{i-1}, y, x\_{i+1}, \ldots, x\_n\right)| \leq D\_i f\left(x\_{-i}\right)
$$

**Corollary 1 (Bounded Difference Inequality for Variance)**. Suppose that $X\_1, \ldots, X\_n$ are independent and (1) holds. Then,
$$
\operatorname{Var}\left(f\left(X\_1, \ldots, X\_n\right)\right) \leq \frac{1}{4} \sum\_{i=1}^n \mathbb{E}\left[\left(D\_i f\left(x\_{-i}\right)\right)^2\right]
$$

## Exercises

### Exercise 2.1.4

Let $g\sim N(0,1)$. Show that, for all $t>1$, we have
$$
\mathbb{E}(g^2\mathbf{1}\_{\{g>t\}})=t\frac{1}{\sqrt{2\pi}}e^{-t^2/2}+\mathbb{P}\{g>t\}\le \left(t+\frac{1}{t}\right)\frac{1}{\sqrt{2\pi}}e^{-t^2/2}
$$
*soln*:

The pdf of $g\sim N(0,1)$ is $p(x)=\frac{1}{\sqrt{2\pi}}e^{-x^2/2}$. We observe that $p'(x)=-x\frac{1}{\sqrt{2\pi}}e^{-x^2/2}=-xp(x)$. By formula (27) (expectation of function of variable), we compute

$$
\begin{aligned}
\mathbb{E}(g^2\mathbf{1}\_{\{g>t\}})&=\int\_t^{\infty}x^2p(x)dx\newline
&=\int\_t^{\infty}-xp'(x)dx\newline
&=[-xp(x)]\_t^{\infty}+\int\_t^{\infty}p(x)dx\newline
&=t\frac{1}{\sqrt{2\pi}}e^{-t^2/2}+\mathbb{P}\{g>t\}
\end{aligned}
$$

where for the last step we notice that $\lim\_{x\to \infty}xp(x)=0$ for $p(x)$ decreases exponentially fast to zero. This proved the equality. To show the inequality is obtained by using Proposition 2.1.2 in HDP.

### Exercise 2.2.3

show that
$$
\cosh (x)\le e^{x^2/2},\quad \forall x\in \mathbb{R}
$$
*soln 1*:
$$
\cosh (x)=\prod\_{k=1}^{\infty}\left(1+\frac{4 x^2}{\pi^2(2 k-1)^2}\right) \leq \exp \left(\sum\_{k=1}^{\infty} \frac{4 x^2}{\pi^2(2 k-1)^2}\right)=\exp \left(x^2 / 2\right)
$$
*soln 2*:

This is equivalent of showing $\ln \cosh(x)\le x^2/2$. Define $f(x)=\ln (\cosh x)-x^2 / 2$ and see that $f^{\prime}(x)=\tanh (x)-x$. Let it be zero to find maximum of $f$.

### Exercise 2.2.8

(Boosting Randomized Algorithm) Calculate the probability of correctness for majority vote where each voter has $\frac{1}{2}+\delta$ probability of being correct.

*soln*:

Let each of the voter be $X\_i\sim B(\frac{1}{2}+\delta)$. By Theorem 2.2.6 (Hoeffding's inequaity for general bounded random variables), we have
$$
\begin{aligned}
\mathbb{P}\left[\sum\_{i=1}^NX\_i\le \frac{N}{2}\right]&= \mathbb{P}\left[\sum\_{i=1}^N(-X\_i)\ge -\frac{N}{2}\right]\newline
&=\mathbb{P}\left[\sum\_{i=1}^N((-X\_i)-\mathbb{E}(-X\_i))\ge -\frac{N}{2}+N\left(\frac{1}{2}+\delta\right)\right]\newline
&\le \exp\left(-\frac{2(N\delta)^2}{N}\right)=\exp(-2N\delta^2)
\end{aligned}
$$
When $N\ge \frac{1}{2}\delta^{-2}\ln (\varepsilon^{-1})$, we have $\exp(-2N\delta^2)\le \exp(-\ln(\varepsilon^{-1}))=\varepsilon$. The probability that the answer voted by majority is incorrect is at most $\varepsilon$.

### Exercise 2.2.10

Let $X\_1,\cdots,X\_N$ be non-negative independent random variables with continuous distributions. Assume that the densities of $X\_i$ are uniformly bounded by $1$.

**(a)** Show that the MGF of $X\_i$ satisfies 
$$
\mathbb{E}\exp (-tX\_i)\le \frac{1}{t}\quad \forall t>0
$$
**(b)** Deduce that, for any $\varepsilon>0$, we have
$$
\mathbb{P}\left[\sum\_{i=1}^NX\_i\le \varepsilon N\right]\le (e\varepsilon)^N
$$
*soln*:

**(a)** We note that these r.v. are non-negative, so
$$
\mathbb{E}\exp (-tX\_i)\le \frac{1}{t}=\int\_0^{\infty}p\_i(x)e^{-tx}dx
$$

and we bound it by its absolute value and use the condition of uniform boundedness of the family,

$$
\text{RHS}\le \left|\int\_0^{\infty}p\_i(x)e^{-tx}dx\right|\le \int\_0^{\infty}\underbrace{|p\_i(x)|}\_{\le 1}|e^{-tx}|dx\le\int\_0^{\infty}e^{-tx}dx=\left[-\frac{1}{t}e^{-tx}\right]\_0^{\infty}=\frac{1}{t}
$$

**(b)** We mimic the proof of Theorem 2.2.2 (Hoeffding's inequality), i.e., using Markov's inequality and the fact that MGF of sum is product of MGF for independent $X\_i$:
$$
\begin{aligned}
\mathbb{P}\left[\sum\_{i=1}^N X\_i\le \varepsilon N\right]&=\mathbb{P}\left[\exp\sum\_{i=1}^N(-tX\_i)\ge \exp(-t\varepsilon N)\right]\newline
&\le \frac{\mathbb{E}\left(\exp \sum\_{i=1}^N(-tX\_i)\right)}{\exp(-t\varepsilon N)}\newline
&=\frac{\prod\_{i=1}^N\mathbb{E}\left(\exp (-tX\_i)\right)}{\exp(-t\varepsilon N)}\newline
&\le e^{t\varepsilon N}\prod\_{i=1}^N\frac{1}{t}=e^{t\varepsilon N}/t^N
\end{aligned}
$$
Letting $t=1/\varepsilon$ to maximize it to get $(e\varepsilon)^N$​​​. 

### Exercise 2.5.9

We did this when listing examples and non-examples of sub-Gaussians above.

### Exercise 2.6.5

The first inequality is simply because $\Vert\bullet\Vert\_{L^2} \leq\Vert \bullet\Vert\_{L^P}$. As for the second one, by Exercise 1.2 .3 and Hoeffding's inequality (Theorem 2.6.3),
$$
\begin{aligned}
\mathbb{E}\left|\sum\_{i=1}^N a\_i X\_i\right|^p & =\int\_0^{\infty} p t^{p-1} \mathbb{P}\left[\left|\sum\_{i=1}^N a\_i X\_i\right|>t\right] \mathrm{d} t \newline
& \leq 2 p \int\_0^{\infty} t^{p-1} \exp \left(-\frac{c t^2}{K^2\Vert a\Vert\_2^2}\right) \mathrm{d} t \newline
& =p\left(\frac{K\Vert a\Vert\_2}{\sqrt{c}}\right)^p \int\_0^{\infty} s^{p / 2-1} \mathrm{e}^{-s} \mathrm{~d} s \quad=p\left(\frac{K\Vert a\Vert\_2}{\sqrt{c}}\right)^p \Gamma\left(\frac{p}{2}\right) .
\end{aligned}
$$

It follows that $\left\Vert \sum\_{i=1}^N a\_i X\_i\right\Vert\_{L^p} /\left(K \sqrt{p}\Vert a\Vert\_2\right) \leq(p \Gamma(p / 2))^{1 / p} / \sqrt{c p}=O(1)$ by Stirling's formula.

### Exercise 2.6.7

The second inequality is simply because $\Vert \bullet\Vert\_{L^P} \leq\Vert \bullet\Vert\_{L^2}$. As for the first one, by the Cauchy-Schwartz inequality and Exercise 2.6.5,
$$
\begin{aligned}
\mathbb{E}\left|\sum\_{i=1}^N a\_i X\_i\right|^p & \geq\left(\mathbb{E}\left|\sum\_{i=1}^N a\_i X\_i\right|^2\right)^2 / \mathbb{E}\left|\sum\_{i=1}^N a\_i X\_i\right|^{4-p} \newline
& \geq\Vert a\Vert\_2^4 /\left(C K \sqrt{4-p}\Vert a\Vert\_2\right)^{4-p} \quad=c\_p(K)^p\Vert a\Vert\_2^p
\end{aligned}
$$
with $c\_p(K)=(C K \sqrt{4-p})^{1-4 / p}$​.

### More Exercises

1. (More on the Sub-Gaussian Condition). Suppose that a random variable satisfies:

$$
\mathbb E[\exp (\lambda X)] \leq \exp \left(\frac{\lambda^2 \sigma^2}{2}\right) \text { for all } \lambda \in \mathbb{R} 
$$

(a) Show that $X$ must be mean 0. For this problem, it may be helpful to consider the inequality $1+x \leq e^x$ and a Taylor expansion of the form $\exp \left(\frac{\lambda^2 \sigma^2}{2}\right)=1+\frac{\lambda^2 \sigma^2}{2}+R(\lambda)$, where $R(\lambda)$ is the remainder function satisfying $R(\lambda) / \lambda^2 \rightarrow 0$ as $\lambda \rightarrow 0$ (For this problem, it is okay if you are not rigorous with the remainder, so long as you consider $\lambda \rightarrow 0$ ).

(b) One may alternatively define the sub-Gaussian norm as:
$$
\Vert X\Vert\_{\psi\_2}=\sup\_{p \geq 1} \frac{\Vert X\Vert\_{L^P}}{\sqrt{p}}
$$
Argue that $\Vert X\Vert\_{\psi\_2} \leq K\_2$ is equivalent to $X$ being sub-Gaussian. You may use the sub-Gaussian equivalence theorem in your argument (this sub-question should follow immediately from one of the equivalent notions of sub-Gaussianity).

(c) Using part (b), argue that $\operatorname{Var}(X) \leq 2\Vert X\Vert\_{\psi\_2}^2$; that is, the variance can be upper-bounded by the sub-Gaussian norm (up to constants). (Note: it is also possible to prove $\operatorname{Var}(X) \leq \sigma^2$, but making the argument rigorous is a little trickier).

*soln*:

(a) Since $e^x$ is a convex function, we by Jensen's inequality see that
$$
\exp\left(\lambda \mathbb E X\right)\le \exp\left(\frac{\lambda^2\sigma^2}{2}\right)
$$

Due to the numerical inequality $1+x\le e^x$ and Taylor expansion given, we have

$$
\begin{aligned}
&1+\lambda \mathbb E X\le 1+\frac{\lambda^2 \sigma^2}{2}+R(\lambda)\newline
\implies &\lambda \mathbb E X\le \frac{\lambda^2 \sigma^2}{2}+R(\lambda)\newline
\xRightarrow[\lambda\neq 0]{\lambda^2> 0}&\frac{\lambda \mathbb E X}{\lambda^2}\le \frac{\sigma^2}{2}+\frac{R(\lambda)}{\lambda^2}\newline
\implies &\lim\_{\lambda\to 0}\frac{\mathbb E X}{\lambda}\le \frac{\sigma^2}{2}+\underbrace{\lim\_{\lambda\to 0}\frac{R(\lambda)}{\lambda^2}}\_{=0}=\frac{\sigma^2}{2}
\end{aligned}
$$

Since the RHS is finite, the LHS must also be finite. Thus $\mathbb E X$ can only be $0$ to make this possible; otherwise the LHS goes to $\infty$.

(b):
$$
\begin{aligned}
&\Vert X\Vert\_{\psi\_2}:=\sup\_{p\ge 1}\frac{\Vert X\Vert\_{L^p}}{\sqrt{p}}\le K\_2\newline
\iff &\forall p\ge 1,\; \Vert X\Vert\_{L^p}\le K\_2\sqrt{p}\newline
\iff &X\text{ is sub-Gaussian due to second characterization of sub-Gaussianity}
\end{aligned}
$$

where for the first $\iff$, use the fact that $\sup$ is an upper bound to show $\implies$ and the fact that it is the smallest upper bound to show $\Longleftarrow$.

(c): We proved in (a) that $X$ has $\mathbb E X=0$, so $\mathrm{Var}(X)=\mathbb E (X^2) - (\mathbb E X)^2=\mathbb E (X^2)$. Now notice that
$$
\sqrt{2}\Vert X\Vert\_{\psi^2}=\sqrt{2}\sup\_{p\ge 1}\frac{\Vert X\Vert\_{L^p}}{\sqrt{p}}\ge \sqrt{2}\frac{\Vert X\Vert\_{L^2}}{\sqrt{2}}=\Vert X\Vert\_{L^2}=(\mathbb E |X|^2)^{1/2}
$$

Thus
$$
2\Vert X\Vert\_{\psi^2}^2\ge E(X^2)=\mathrm{Var}(X)
$$

2. 

(a): For $X \sim N(0,1)$, show that the MGF of $X^2$ is finite only in a bounded neighborhood of $0$.

(b): Suppose that $\mathbb E\left[\exp \left(\lambda^2 X^2\right)\right] \leq \exp \left(\lambda^2 K^2\right)$ for some $K>0$ for all $\lambda \in \mathbb{R}$ opposed to a bounded interval as in condition (iv). Show that this implies $X$ is bounded with probability 1 (Hint: consider $P(X \geq t)$ for appropriately large $t$ as $\lambda \rightarrow \infty)$.

*soln*:

(a): $X \sim N(0,1)$ implies that $X^2\sim \chi\_1^2$. The MGF of $\mathbb E(e^{\lambda X})$ of $X^2$ exists only when $\lambda <\frac{1}{2}$ 

(in the sense that the integral diverges otherwise; see [link](https://proofwiki.org/wiki/Moment\_Generating\_Function\_of\_Chi-Squared\_Distribution).)

When $\lambda<\frac{1}{2}$, it exists and equals to $(1-2\lambda)^{-1/2}$. Therefore, the MGF is finite only in a bounded neighborhood of $0$.

(b): Let $\varepsilon>0$ be given. By Chernoff's inequality,
$$
\mathbb{P}\{|X| \geq \sqrt{K+\varepsilon}\}=\mathbb{P}\left[X^2 \geq K+\varepsilon\right] \leq \inf\_{\lambda \in \mathbb{R}} \mathrm{e}^{-\lambda^2(K+\varepsilon)} \mathbb{E} \exp \left(\lambda^2 X^2\right) \leq \inf\_{\lambda \in \mathbb{R}} \mathrm{e}^{-\lambda^2 \varepsilon}=0.
$$

Therefore, $\mathbb{P}\{|X| \leq \sqrt{K}\}=\lim \_{n \rightarrow \infty} \mathbb{P}\left[|X|<\sqrt{K+n^{-1}}\right]=1$.

3. (Concentration of Poisson Random Variables). For the following problem, you may use the fact that the MGF of $\operatorname{Poisson}(\mu)$ is given by:

$$
M\_X(\lambda)=\exp \left(\mu\left(e^\lambda-1\right)\right)
$$

(a): Show that Poisson$(\mu)$ is not a sub-Gaussian distribution.

(b): Recall that in a Chernoff bound argument, one considers the upper bound:
$$
P(X-\mu \geq t) \leq \inf\_{\lambda>0} E\left[e^{\lambda(X-\mu)}\right] e^{-\lambda t}
$$

What is the optimal value of $\lambda$ for $X \sim \operatorname{Poisson}(\mu)$?

*soln*:

(a): By the first characterization of the sub-Gaussianity, $X$ is sub-Gaussian iff for some constant $K\_1$,
$$
\mu(e^\lambda-1)\le \lambda^2K\_1^2,\quad \lambda\in \mathbb R
$$


Note that the Taylor expansion of $e^\lambda$ at $0$ gives
$$
e^\lambda=\sum\_{n=0}^{\infty} \frac{\lambda^n}{n !}=1+\lambda+\frac{\lambda^2}{2 !}+\frac{\lambda^3}{3 !}+\cdots,\quad \lambda\in \R
$$

So the LHS is
$$
\mu\left(\lambda+\frac{\lambda^2}{2 !}+\frac{\lambda^3}{3 !}+\cdots\right)
$$

which grows faster than $K\_1^2\lambda^2$:
$$
\lim\_{\lambda\to \infty}\frac{\mu\left(\lambda+\frac{\lambda^2}{2 !}+\frac{\lambda^3}{3 !}+\cdots\right)}{\lambda^2 K\_1^2}=\frac{\mu}{K\_2^2}\lim\_{\lambda\to \infty}\frac{1}{\lambda}+\frac{1}{2!}+\frac{\lambda}{3!}+\cdots=\infty
$$

(b): Observe that
$$
\begin{aligned}
\mathbb{P}(X-\mu \geq t) &\leq \inf\_{\lambda>0} \mathbb E\left[e^{\lambda(X-\mu)}\right] e^{-\lambda t}\newline
&=\inf\_{\lambda>0}\mathbb E [e^{\lambda X}]e^{-\lambda \mu-\lambda t}\newline
&=\inf\_{\lambda>0}e^{\mu e^\lambda -1}e^{-\lambda \mu-\lambda t}
\end{aligned}
$$

Since $e^{x}$ is an increasing function, we can find the optimal value attaining the minimum of $\mu e^\lambda -1-\lambda \mu-\lambda t$ by setting the derivative to zero:
$$
0=\frac{d\left(\mu e^\lambda -1-\lambda \mu-\lambda t\right)}{d \lambda}=\mu e^{\lambda}-\mu-t\Rightarrow \lambda=\log \frac{\mu+t}{\mu}
$$



## Additional Topic: Martingale-Based Methods

Intuitively, martingales capture the idea of a fair game. Let $X\_n$ denote your winnings at time $n$. The most basic notion of martingale is one in which for all $n, E\left|X\_n\right|<\infty$ and:
$$
E\left[X\_{n+1} \mid X\_1, \ldots, X\_n\right]=x\_n
$$

If we consider $X\_{n+1}-X\_n$ as our gain at time $n+1$, this is saying that the expected gain given everything that has happened so far is 0 . For example, suppose we flip a fair coin and we win one dollar if it is heads and lose one dollar if it is tails. In this case, the flips are independent and each trial has expectation 0 . Let $S\_n=\sum\_{i=1}^n X\_i$, where $X\_i$ the outcome of the $i$-th trial. We will show that $S\_n$ is a martingale. Then,
$$
\begin{aligned}
E\left[S\_{n+1} \mid S\_1, \ldots, S\_n\right] & =E\left[X\_{n+1}+\sum\_{i=1}^n X\_i \mid S\_1, \ldots, S\_n\right] \newline
& =E\left[X\_{n+1}+S\_n \mid S\_1, \ldots, S\_n\right] \newline
& =0+s\_n=s\_n
\end{aligned}
$$

However, the idea of a martingale is more general and allows the sequence to be dependent. As an interesting and perhaps controversial example, roughly speaking, the efficient market hypothesis asserts that the return of an asset (relative to a risk-free rate and also taking into consideration risk premiums in some formulations) is a martingale. Even taking the full history of the asset (and the market) into account, the expected value in the next step is the current value.

Let $\left(X\_k\right)\_{k=1}^n$ be a sequence of independent random variables, and consider the random variable $f(X)=f\left(X\_1 \ldots, X\_n\right)$, for some function $f: \mathbb{R}^n \rightarrow \mathbb{R}$.
Suppose that our goal is to obtain bounds on the deviations of $f$ from its mean. In order to do so, we consider the sequence of random variables given by $Y\_0=\mathbb{E}[f(X)], Y\_n=f(X)$, and

$$
Y\_k=\mathbb{E}\left[f(X) \mid X\_1, \ldots, X\_k\right] \quad \text { for } k=1, \ldots, n-1,
$$

where we assume that all conditional expectations exist. Note that $Y\_0$ is a constant, and the random variables $Y\_k$ will tend to exhibit more fluctuations as we move along the sequence from $Y\_0$ to $Y\_n$. Based on this intuition, the martingale approach to tail bounds is based on the telescoping decomposition

$$
f(X)-\mathbb{E}[f(X)]=Y\_n-Y\_0=\sum\_{k=1}^n \underbrace{\left(Y\_k-Y\_{k-1}\right)}\_{D\_k},
$$

in which the deviation $f(X)-\mathbb{E}[f(X)]$ is written as a sum of increments $\left(D\_k\right)\_{k=1}^n$. As we will see, the sequence $\left(Y\_k\right)$ is a particular example of a martingale sequence, known as the **Doob martingale**, whereas the sequence $\left(D\_k\right)$ is an example of a martingale difference sequence.

We now move to more general definition: we call a nested sequence of $\sigma$-fields $\left(\mathcal{F}\_k\right)$ a **filtration**. In the Doob martingale described above, the $\sigma$-field $\sigma\left(X\_1, \ldots, X\_k\right)$ generated by the first $k$ variables plays the role of $\mathcal{F}\_k$.

Let $\left(Y\_k\right)\_{k=1}^{\infty}$ be a sequence of random variables such that $Y\_k$ is measurable with respect to the $\sigma$-field $\mathcal{F}\_k$. In this case, we say that **$(Y\_k)$ is adapted to the filtration $(\mathcal{F}\_k)$**. In the Doob martingale, the random variable $Y\_k$ is a measurable function of $\left(X\_1, \ldots, X\_k\right)$, and hence the sequence is adapted to the filtration defined by the $\sigma$-fields. We are now ready to define a general martingale:

**Definition**: Given a sequence $\left(Y\_k\right)\_{k=1}^{\infty}$ of random variables adapted to a filtration $(\mathcal{F}\_k)$, the pair $((Y\_k, \mathcal{F}\_k))$ is a **martingale** if, for all $k \geq 1$,

$$
\mathbb{E}\left[\left|Y\_k\right|\right]<\infty \quad \text { and } \quad \mathbb{E}\left[Y\_{k+1} \mid \mathcal{F}\_k\right]=Y\_k
$$

It is frequently the case that the filtration is defined by a second sequence of random variables $(X\_k)$ via the canonical $\sigma$-fields $\mathcal{F}\_k:=\sigma(X\_1, \ldots, X\_k)$. In this case, we say that $(Y\_k)$ is a martingale sequence with respect to $(X\_k)$. The Doob construction is an instance of such a martingale sequence. If a sequence is martingale with respect to itself (i.e., with $\mathcal{F}\_k=\sigma(Y\_1, \ldots, Y\_k)$ ), then we say simply that $(Y\_k)$ forms a martingale sequence.

**Example 1** (Sums of Zero Mean Random Variables): Let $S\_n=\sum\_{i=1}^n X\_i$, $X\_1$, where $\ldots, X\_1, \ldots, X\_n$ are independent, $E\left(X\_i\right)=0$ and $E\left|X\_i\right|<\infty$. Previously, for $S\_{n+1}$, we considered conditioning on the information set $S\_1, \ldots, S\_n$ and showed that this was a martingale (for concreteness, we assumed binary trials, but this was not needed). We can also define a martingale with respect to the random variables $\left(X\_i\right)\_{i \geq 1}$. Observe that:

$$
\begin{aligned}
E\left[S\_{n+1} \mid X\_1, \ldots, X\_n\right] & =E\left[X\_{n+1}+\sum\_{i=1}^n X\_i \mid X\_1, \ldots, X\_n\right] \newline
& =0+\sum\_{i=1}^n x\_n=s\_n
\end{aligned}
$$

**Example 2** (Doob construction): Given a sequence of independent random variables $\left(X\_k\right)\_{k=1}^n$, recall the sequence

$$Y\_k=\mathbb{E}\left[f(X) \mid X\_1, \ldots, X\_k\right]$$

previously defined, and suppose that $\mathbb{E}[|f(X)|]<\infty$. We claim that $\left(Y\_k\right)\_{k=0}^n$ is a martingale with respect to

$\left(X\_k\right)\_{k=1}^n$. Indeed, in terms of the shorthand $X\_1^k=\left(X\_1, X\_2, \ldots, X\_k\right)$, we have

$$
\mathbb{E}\left[\left|Y\_k\right|\right]=\mathbb{E}\left[\left|\mathbb{E}\left[f(X) \mid X\_1^k\right]\right|\right] \leq \mathbb{E}[|f(X)|]<\infty,
$$

where the bound follows from Jensen's inequality. Turning to the second property, we have

$$
\mathbb{E}\left[Y\_{k+1} \mid X\_1^k\right]=\mathbb{E}\left[\mathbb{E}\left[f(X) \mid X\_1^{k+1}\right] \mid X\_1^k\right] \stackrel{(\mathrm{i})}{=} \mathbb{E}\left[f(X) \mid X\_1^k\right]=Y\_k,
$$

where we have used the tower property of conditional expectation in step (i): *Law of total expectation* gives $\mathbb{E}(Z)=\mathbb{E}\_Z[\mathbb{E}\_X(Z|Y)]$, so $\mathbb{E}(Z|X)=\mathbb{E}[\mathbb{E}(Z|X,Y)|X]$ by replacing $E(\; \cdot\;)$ with $\mathbb{E}(\; \cdot \;|X)$​. 

A closely related notion is that of **martingale difference sequence**, meaning an adapted sequence $((D\_k, \mathcal{F}\_k))$ such that, for all $k \geq 1$,

$$
\mathbb{E}\left[\left|D\_k\right|\right]<\infty \quad \text { and } \quad \mathbb{E}\left[D\_{k+1} \mid \mathcal{F}\_k\right]=0 .
$$

As suggested by their name, such difference sequences arise in a natural way from martingales. In particular, let us define $D\_k=Y\_k-Y\_{k-1}$ for $k \geq 1$ for a given martingale $((Y\_k, \mathcal{F}\_k))$. Then

$$
\begin{aligned}
\mathbb{E}\left[D\_{k+1} \mid \mathcal{F}\_k\right]
& =\mathbb{E}\left[Y\_{k+1} \mid \mathcal{F}\_k\right]-\mathbb{E}\left[Y\_k \mid \mathcal{F}\_k\right] \newline
& =\mathbb{E}\left[Y\_{k+1} \mid \mathcal{F}\_k\right]-Y\_k=0,
\end{aligned}
$$

using the martingale property and the fact that $Y\_k$ is measurable with respect to $\mathcal{F}\_k$. Thus, for any martingale sequence $\left(Y\_k\right)\_{k=0}^{\infty}$, we have the telescoping decomposition

$$
Y\_n-Y\_0=\sum\_{k=1}^n D\_k,
$$

where $\left(D\_k\right)\_{k=1}^{\infty}$​ is a martingale difference sequence.

We now introduce several concentration results.

**Theorem 1** (Azuma-Hoeffding Inequality). Let $\left(Y\_n\right)\_{n \geq 1}$ be martingale with respect to $\left(X\_n\right)\_{n \geq 1}$ and let $\left(\Delta\_n\right)\_{n \geq 1}$ denote the associated martingale difference sequence. Suppose that for each $1 \leq i \leq n$,

$$
E\left[\exp \left(\lambda \Delta\_i\right) \mid X\_1, \ldots, X\_{i-1}\right] \leq \exp \left(\frac{\lambda^2 \sigma\_i^2}{2}\right) \text { with probability } 1
$$

Then,

$$
P\left(\left|\sum\_{i=1}^n \Delta\_i\right| \geq t\right) \leq 2 \exp \left(\frac{-t^2}{2 \sum\_{i=1}^n \sigma\_i^2}\right)
$$

*proof*:
Observe that, conditioned on $X\_1, \ldots, X\_{n-1}, \Delta\_1, \ldots, \Delta\_{i-1}$ are fixed since they are functions of $X\_1, \ldots, X\_{n-1}$. Therefore, by law of iterated expectation,

$$
\begin{aligned}
E\left[\exp \left(\lambda \sum\_{i=1}^n \Delta\_i\right)\right] & =E\left(E\left[\exp \left(\lambda \sum\_{i=1}^n \Delta\_i\right) \mid X\_1, \ldots, X\_{n-1}\right]\right) \newline
& =E\left(E\left[\exp \left(\lambda \Delta\_n\right) \mid X\_1, \ldots, X\_{n-1}\right] \cdot \exp \left(\lambda \sum\_{i=1}^{n-1} \Delta\_i\right)\right) \newline
& \leq \exp \left(\frac{\lambda^2 \sigma\_n^2}{2}\right) E\left[\exp \left(\lambda \sum\_{i=1}^{n-1} \Delta\_i\right)\right]
\end{aligned}
$$

In the next step, we take law of iterated expectation conditioning on $X\_1, \ldots, X\_{n-2}$ to see that:

$$
E\left[\exp \left(\lambda \sum\_{i=1}^n \Delta\_i\right)\right] \leq \exp \left(\frac{\lambda^2\left(\sigma\_{n-1}^2+\sigma\_n^2\right)}{2}\right) E\left[\exp \left(\lambda \sum\_{i=1}^{n-2} \Delta\_i\right)\right]
$$

Continuing to unfurl the expectation in this way (we can make this argument more formal through induction), we have:

$$
E\left[\exp \left(\lambda \sum\_{i=1}^n \Delta\_i\right)\right] \leq \exp \left(\frac{\lambda^2 \sum\_{i=1}^n \sigma\_i^2}{2}\right)
$$

Therefore, $\sum\_{i=1}^n \Delta\_i \sim \operatorname{subGaussian}\left(\sum\_{i=1}^n \sigma\_i^2\right)$ and we can repeat the same Chernoff bound argument for sums of independent sub-Gaussian random variables and the claim follows.

**Definition** (Bounded difference property). The function $f\left(x\_1, \ldots, x\_n\right)$ has bounded differences with constants $\left(c\_1, \ldots, c\_n\right)$ if for each $1 \leq i \leq n$,
$$
\sup \_{x\_1, \ldots, x\_n, x\_i^{\prime}}\left|f\left(x\_1, \ldots, x\_i, \ldots, x\_n\right)-f\left(x\_1, \ldots, x\_i^{\prime}, \ldots, x\_n\right)\right| \leq c\_i
$$
**Theorem 2** (Bounded Difference Inequality). Suppose that $X\_1, \ldots, X\_n$ are independent random variables and $f\left(x\_1, \ldots, x\_n\right)$ satisfies the bounded difference property with constants $\left(c\_1, \ldots, c\_n\right)$. Then,

$$
P\left(\left|f\left(X\_1, \ldots, X\_n\right)-E\left[f\left(X\_1, \ldots, X\_n\right)\right]\right| \geq t\right) \leq 2 \exp \left(\frac{-2 t^2}{\sum\_{i=1}^n c\_i^2}\right)
$$

*proof*:
First, observe that we can write:
$$
f\left(X\_1, \ldots, X\_n\right)-E\left[f\left(X\_1, \ldots, X\_n\right)\right]=\sum\_{i=1}^n \Delta\_i
$$
where $\Delta\_i=Y\_i-Y\_{i-1}$ and $Y\_i$ is Doob martingale considered in Example 2, with $N=n$. Now, the claim will follow if we can show that, conditional on $X\_1, \ldots, X\_{i-1}$, each $\Delta\_i$ takes values in an interval of length $c\_i$ due to the upper bound for the sub-Gaussian parameter for bounded random variables discussed in Lecture 3. Define:
$$
\begin{aligned}
& L\_i=\inf\_{x\_i} E\left[f\left(X\_1, \ldots, x\_i, \ldots, X\_n\right) \mid X\_1, \ldots, X\_{i-1}, x\_i\right]-E\left[f\left(X\_1, \ldots, X\_n\right) \mid X\_1, \ldots, X\_{i-1}\right] \newline
& U\_i=\sup\_{x\_i} E\left[f\left(X\_1, \ldots, x\_i, \ldots, X\_n\right) \mid X\_1, \ldots, X\_{i-1}, x\_i\right]-E\left[f\left(X\_1, \ldots, X\_n\right) \mid X\_1, \ldots, X\_{i-1}\right]
\end{aligned}
$$

Notice that, conditional on $X\_1, \ldots, X\_{i-1}, \Delta\_i$ is now only a function of $X\_i$. Now,

$$
\begin{aligned}
\Delta\_i-L\_i & =E\left[f\left(X\_1, \ldots, X\_n\right) \mid X\_1, \ldots, X\_i\right]-\inf\_{x\_i} E\left[f\left(X\_1, \ldots, x\_i, \ldots, X\_n\right) \mid X\_1, \ldots, X\_{i-1}, x\_i\right] \newline
& =g\left(X\_i\right)-\inf \_{x\_i} g\left(x\_i\right) \geq 0 \Longrightarrow \Delta\_i \geq L\_i
\end{aligned}
$$

where above $g\left(X\_i\right)=E\left[f\left(x\_1 \ldots, x\_{i-1}, x\_i, \ldots, X\_n\right) \mid X\_i\right]$. Similarly, we can show that:

$$
U\_i-\Delta\_i \geq 0 \Longrightarrow \Delta\_i \leq U\_i
$$

Therefore, with probability 1 ,

$$
L\_i \leq \Delta\_i \leq U\_i
$$

Now we upper bound $U\_i-L\_i$ :

$$
\begin{aligned}
U\_i-L\_i & =\sup\_{x\_i} E\left[f\left(X\_1, \ldots, x\_i, \ldots, X\_n\right) \mid X\_1, \ldots, X\_{i-1}, x\_i\right]-\inf\_{x\_i} E\left[f\left(X\_1, \ldots, x\_i, \ldots, X\_n\right) \mid X\_1, \ldots, X\_{i-1}, x\_i\right] \newline
& \leq \sup\_{x\_i, y\_i}\left|E\left[f\left(x\_1, \ldots, x\_i, X\_{i+1}, \ldots, X\_n\right)\right]-E\left[f\left(x\_1, \ldots, y\_i, X\_{i+1}, \ldots, X\_n\right)\right]\right| \newline
& =\sup\_{x\_i, y\_i}\left|E\left[f\left(x\_1, \ldots, x\_i, X\_{i+1}, \ldots, X\_n\right)-f\left(x\_1, \ldots, y\_i, X\_{i+1}, \ldots, X\_n\right)\right]\right| \newline
& \leq \sup\_{x\_1, \ldots, x\_n, x\_i^{\prime}}\left|f\left(x\_1, \ldots, x\_i, \ldots, x\_n\right)-f\left(x\_1, \ldots, x\_i^{\prime}, \ldots, x\_n\right)\right|=c\_i
\end{aligned}
$$

In the second line, we used the fact that, because $X\_1, \ldots, X\_n$ are independent, $E\left[f\left(X\_1, \ldots, X\_n\right) \mid X\_1, \ldots, X\_i\right]=E\left[f\left(x\_1, \ldots, x\_i, X\_{i+1}, \ldots X\_n\right)\right]$, where $x\_1, \ldots x\_i$ are treated as fixed constants. If they were not independent, then in general, the conditional distribution would depend on the conditioning set. This would mean that the expectations in line 3 would be with respect to different distributions (since we are taking supremum/infimum), and we wouldn't be able to combine them in the same way using linearity of expectation.

The last line follows from the fact that the expected difference is upper bounded by the largest possible difference, which is given by $c\_i$. With linearity of expectation, we can integrate with respect to the same $X\_{i+1}, \ldots, X\_n$ under the independence assumption.

### Application: Bound on Variance of Kolmogorov-Smirnov Statistic

We recall the theorem of tensorization of variance that if $X\_1, \ldots, X\_n$ are independent random variables. Then,

$$
\operatorname{Var}\left(f\left(X\_1, \ldots, X\_n\right)\right) \leq \sum\_{i=1}^n \mathbb{E}\left[\operatorname{Var}\_i f\left(x\_1, \ldots, x\_n\right)\right]
$$

Now suppose that $X\_1, \ldots, X\_n$ are iid, with common distribution function $F(x)$. Let $F\_n(t)$ denote the empirical CDF, which may be viewed as an estimator of $F(t)$ :

$$
F\_n(t)=\frac{1}{n} \sum\_{i=1}^n \mathbb{1}\left(X\_i \leq t\right)
$$

The Kolmogorov-Smirnov statistic is used for goodness-of-fit testing. Suppose that we want to know whether a distribution with cdf $G(x)$ is a good fit to the data. The associated Kolmogorov-Sminrov statistic is defined as:

$$
f\left(X\_1, \ldots, X\_n\right)=\sup \_{t \in \mathbb{R}}\left|F\_n(t)-G(t)\right|
$$

It turns out that we can derive an upper bound for the variance using the bounded difference inequality for the variance. We are considering this statistic as an example because it demonstrates how the bounded difference inequality for the variance has highly non-trivial consequences; however, you are not expected to be able to verify this condition for a fairly complicated statistic like this one. Let's examine the function $F\_n(t)$, where we have fixed $x\_1, \ldots, x\_{i-1}, x\_{i+1}, \ldots, x\_n$ and we are only considering randomness in $X\_i . F\_n(t)$ has only one summand that involves $X\_i: \frac{1}{n} \mathbb{1}\left(X\_i \leq t\right)$. Therefore,

$$
\begin{aligned}
& \sup\_{x, y}\left|f\left(x\_1, \ldots, x\_{i-1}, x, x\_{i+1}, \ldots, x\_n\right)-f\left(x\_1, \ldots, x\_{i-1}, y, x\_{i+1}, \ldots, x\_n\right)\right| \newline
\leq & \sup\_{x, y}\left|\sup\_{t \in \mathbb{R}}\right| \frac{1}{n} \sum\_{j \neq i} \mathbb{1}\left(x\_j \leq t\right)+\frac{1}{n} \mathbb{1}(x \leq t)-G(t)\left|-\sup\_{t \in \mathbb{R}}\right| \frac{1}{n} \sum\_{j \neq i} \mathbb{1}\left(x\_j \leq t\right)+\frac{1}{n} \mathbb{1}(y \leq t)-G(t)|| \newline
\leq & \sup\_{x, y} \frac{1}{n} \sup\_{t \in \mathbb{R}}|\mathbb{1}(x \leq t)-\mathbb{1}(y \leq t)| \leq \frac{1}{n}
\end{aligned}
$$

where above we used the fact that $\sup \_{t \in \mathbb{R}}|f(t)|$ is a norm and therefore we have the reverse triangle inequality $\left|\sup \_{t \in \mathbb{R}}\right| f(t)\left|-\sup \_{t \in \mathbb{R}}\right| g(t)|| \leq \sup \_{t \in \mathbb{R}}|f(t)-g(t)|$. Therefore, we may conclude:

$$
\operatorname{Var}\left(\sup \_{t \in \mathbb{R}}\left|F\_n(t)-G(t)\right|\right) \leq \frac{1}{4 n}
$$

This tells us that the variance of the Kolmgorov-Smirnov statistic gets smaller as $n$ gets larger, and thus, it concentrates around $E\left[\sup \_{t \in \mathbb{R}}\left|F\_n(t)-G(t)\right|\right]$. If $G(t) \neq F(t)$, then this expectation will not go to zero asymptotically, but if $G(t)=F(t)$, this quantity will turn out to vanish. This is why the Kolmogorov-Smirnov statistic can detect differences between arbitrary distributions.

The bound $1/n$ is in fact uniform over $x\_{-i}$ and therefore, the bounded difference property is satisfied with constants $(1 / n, \ldots, 1 / n)$. Thus,
$$
P\left(\left|T\left(X\_1, \ldots, X\_n\right)-\mathbb{E}\left[T\left(X\_1, \ldots, X\_n\right)\right]\right| \geq t\right) \leq 2 \exp \left(-2 n t^2\right)
$$

Of course, one question that remains is what is $\mathbb{E}\left[T\left(X\_1, \ldots, X\_n\right)\right]$ ? Does it go to zero when $F=G$ (i.e. the CDF of $X\_i$ is equal to $G$ )? How about when $F \neq G$ ? We will study this in another [reading file](https://anthonyhongxiao.github.io/reading/Concentration\_of\_Lipschitz\_Functions/).

# 3. Random Vectors in High Dimensions

## Concentration of the Norm

Suppose that $X=\left(X\_1, \ldots, X\_n\right)$ are independent random variables with mean 0 and variance 1 . Using the tools that we have learned so far, it will turn out that we can give informative bounds on the behavior of the (Euclidean) norm $\Vert X\Vert $​.

**Proposition 1**. Suppose that $X=\left(X\_1, \ldots, X\_n\right)$ are independent random variables with mean 0 , variance 1 and sub-Gaussian parameter $K$. Then, for some $C$ depending only on $K$,
$$
P(\Vert X \Vert -\sqrt{n} \mid \geq t) \leq 2 \exp \left(-C t^2\right)
$$

*Proof*. To prove this claim, let us first consider a related quantity:
$$
\Vert X\Vert ^2=\sum\_{i=1}^n X\_i^2
$$

Since the random variables are mean 0 with variance 1 , it is clear that $E\left[\Vert X\Vert ^2\right]=$ $n$. Moreover, if $X\_1, \ldots, X\_n$ are sub-Gaussian with parameter $K$, We know that $X^2$ is sub-Exponential with parameter $K^2$. Therefore, by Bernstein's inequality, for any $t \geq 0$,
$$
\begin{aligned}
P\left(\frac{1}{n}\Vert X\Vert ^2-1 \geq t\right) & \leq 2 \exp \left(-c n \min \left(\frac{t^2}{K^4}, \frac{t}{K^2}\right)\right) \newline
& \leq 2 \exp \left(-C n \min \left(t^2, t\right)\right)
\end{aligned}
$$
Now, suppose that we want to deduce the behavior of the norm rather than the squared norm from the above expressions. To this end, observe that, for $z \geq 0$ :
$$
|z-1| \geq \delta \Longrightarrow\left|z^2-1\right| \geq \max \left(\delta, \delta^2\right)
$$

For a proof of this proposition, see the Appendix. Therefore, it follows that:
$$
\begin{aligned}
P(|\Vert X\Vert-\sqrt{n}|\geq t) & =P\left(\left|\frac{\Vert X\Vert }{\sqrt{n}}-1\right| \geq t / \sqrt{n}\right) \newline
& \leq P\left(\left|\frac{\Vert X\Vert ^2}{n}-1\right| \geq \max \left(t^2 / n, t / \sqrt{n}\right)\right) \newline
& \leq 2 \exp \left(-C t^2\right)
\end{aligned}
$$

The claim follows.

It follows that $\Vert X\Vert -\sqrt{n}$ is sub-Gaussian. Interestingly, the expectation (in this case $\sqrt{n}$ ) grows with $n$, but the size of the fluctuations essentially remain constant. One way to interpret this result is that in higher dimensions, the random vector $X$ tends to take values in a thin shell sandwiched between $n-1$ spheres with radius between $\sqrt{n}-K$ and $\sqrt{n}+K$ for some constant $K$. Recall that a unit $n-1$ sphere, which we denote $\mathcal{S}^{n-1}$ consists of all points that satisfy $\Vert x\Vert =1$ for $x \in \mathbb{R}^n$.

Using this concentration of the norm, one can prove very interesting properties related to properties of random vectors in high dimensions. In what follows, we will argue that two independent vectors drawn from the uniform distribution on $\mathcal{S}^{n-1}$ tend to be nearly orthogonal to each other when $n$ is large (it is not true in low-dimensional situations). To this end, we will use the fact that if $g \sim N\left(0, I\_n\right)$, then $g /\Vert g\Vert  \sim \operatorname{Uniform}\left(\mathcal{S}^{n-1}\right)$.

**Proposition 2**. Suppose that $X\_n, Y\_n$ are independent vectors drawn from $\operatorname{Uniform}\left(\mathcal{S}^{n-1}\right)$. Then, as $n \rightarrow \infty$, for any fixed $t>0$,
$$
P\left(\left|\left\langle X\_n, Y\_n\right\rangle\right| \geq t\right) \rightarrow 0
$$

Before we provide a proof sketch of this proposition, we use the following fact about sub-Gaussian random variables.
**Proposition 3**. Suppose $X$ and $Y$ are sub-Gaussian random variables. Then, the product $X Y$ is sub-exponential. Furthermore,
$$
\Vert X Y\Vert \_{\psi\_1} \leq\Vert X\Vert \_{\psi\_2}\Vert Y\Vert \_{\psi\_2}
$$

We now return to a proof sketch of Proposition 2.
*Proof Sketch of Proposition 2*.
Let $g\_1, g\_2$ be independent $N\left(0, I\_n\right)$ random variables. Since $g\_1 /\left\Vert g\_1\right\Vert $ and $g\_2 /\left\Vert g\_2\right\Vert $ are uniformly distributed on the unit sphere, we can equivalent write:
$$
\left\langle X\_n, Y\_n\right\rangle=\underbrace{\left(\frac{1}{n} \sum\_{i=1}^n g\_{1, i} \cdot g\_{2, i}\right)}\_{S\_n} \cdot \frac{\sqrt{n}}{\left\Vert g\_1\right\Vert } \cdot \frac{\sqrt{n}}{\left\Vert g\_2\right\Vert }
$$
One way to interpret Proposition 1 is that we can choose $M<\infty$ so that $\left\Vert g\_1\right\Vert  / \sqrt{n}$ is bounded with arbitrarily high probability. For example, if we plug in $M=\sqrt{\frac{\log (2 / C \alpha)}{n}}$ for $t$, then we can argue that $1-M \leq\Vert X\Vert  / \sqrt{n} \leq 1+M$ with probability at least $1-\alpha$.

Furthermore, $S\_n$ is a mean of sub-exponential random variables by Proposition 3. We also have that $E\left[g\_{1, i} g\_{2, i}\right]=E\left[g\_{1, i}\right] \cdot E\left[g\_{2, i}\right]=0$ since they are independent mean 0 Gaussian random variables. Therefore, we can use Bernstein's inequality to show that it concentrates. While making this argument rigorous requires slightly more work, one can essentially argue that for some sequence $\left(M\_n\right)\_{n \geq 1}$ chosen by the rule above, $M\_n$ will approach 0 and with high probability:
$$
\left\langle X\_n, Y\_n\right\rangle \leq \frac{S\_n}{\left(1-M\_n\right)^2}
$$
which concentrates around 0 . The left tail is analogous.

## Sub-Gaussian and sub-Exponential Vectors

For random vectors, we typically define sub-Gaussian and sub-Exponential norms by projecting the vector to a one-dimensional random variable and taking the worst-case sub-Gaussian norm for these projections. Recall that a projection of a vector $a$ in the direction of a unit vector $v$ has the form:
$$
\operatorname{proj}\_v(a)=\langle a, v\rangle v
$$

The quantity $\langle a, v\rangle$ is known as the scalar projection and tells us how closely the two vectors are aligned. If they are orthogonal, $\langle a, v\rangle=0$ and if they are perfectly aligned, $\langle a, v\rangle= \pm\Vert a\Vert $. In our case, the scalar projection is given by $\langle v, X\rangle$. It is quite common to define norms using a worst case value for the scalar projection in the direction of a unit vector. We saw a similar idea with Gaussian complexity and we will see another similar type of object for matrices.
**Definition 1** (Sub-Gaussian Vector). A vector $X \in \mathbb{R}^d$ is sub-Gaussian if all scalar projections $\langle v, X\rangle$ are sub-Gaussian. The sub-Gaussian norm of $X$ is given by:
$$
\Vert X\Vert \_{\psi\_2}=\sup \_{\Vert v\Vert =1}\Vert \langle v, X\rangle\Vert \_{\psi\_2}
$$

**Definition 2**. A vector $X \in \mathbb{R}^d$ is sub-Exponential if all scalar projections $\langle v, X\rangle$ are sub-Exponential. The sub-Exponential norm of $X$ is given by:
$$
\Vert X\Vert \_{\psi\_1}=\sup \_{\Vert v\Vert =1}\Vert \langle v, X\rangle\Vert \_{\psi\_1}
$$

Note that this is a stronger condition than each of the individual coordinates being sub-Gaussian or sub-Exponential. In certain high-dimensional setups, one only needs coordinate-wise tail conditions, but the above definition is most common when tail conditions are imposed for a vector.

## Examples of Sub-Gaussian and Sub-Exponential Random Variables

One natural question with the sub-Gaussian and sub-Exponential condition that we defined above is the following: what types of random vectors are subGaussian or sub-Exponential?

Let us first start with the Normal distribution. Recall the following property of the multivariate Normal distribution. If $Z \in \mathbb{R}^d$ and $Z \sim N(\mu, \Sigma)$, then for any conformable matrix $A$ and vector $b, A Z+b \sim N\left(A \mu+b, A \Sigma A^T\right)$. For a vector $v$, this implies $v^T Z \sim N\left(v^T \mu, v^T \Sigma v\right)$.

**Example 1** (Independent Normal Random Variables). Suppose that $X \sim N\left(0, I\_n\right)$. Then, for any $\Vert v\Vert =1,\langle v, X\rangle \sim N\left(0, v^T v\right)$, which is equivalent to $v^T X \sim$ $N(0,1)$. Therefore, it follows that:
$$
\Vert X\Vert \_{\psi\_2}=\sup \_{\Vert v\Vert =1}\Vert \langle v, X\rangle\Vert \_{\psi\_2}=\Vert Z\Vert \_{\psi\_2}
$$
where $Z \sim N(0,1)$ and is sub-Gaussian. Therefore, for independent Normal random variables, the sub-Gaussian norm is the same for any $n$.

**Example 2** (Multivariate Normal with General Covariance Matrix). Suppose that $X \sim N(0, \Sigma)$. Then, for a fixed $v$, the $M G F$ of $\langle v, X\rangle$ is given by:
$$
E[\exp (\lambda\langle v, X\rangle)]=\exp \left(\frac{\lambda^2 v^T \Sigma v}{2}\right)
$$

In this case, it follows that:
$$
\begin{aligned}
\sup \_{\Vert v\Vert =1} E[\exp (\lambda\langle v, X\rangle)] & =\exp \left(\frac{\lambda^2\left(\sup \_{\Vert v\Vert =1} v^T \Sigma v\right)}{2}\right) \newline
& =\exp \left(\frac{\lambda^2\Vert \Sigma\Vert \_{o p}}{2}\right)
\end{aligned}
$$
where $\Vert \cdot\Vert \_{o p}$ is the operator norm of a matrix, defined as $\Vert A\Vert \_{o p}=\sup \_{\Vert v\Vert =1}\Vert A v\Vert $. For covariance matrices, the operator norm is equivalent to the maximum eigenvalue of the matrix. We will revisit the operator norm shortly. Here, the subGaussian norm depends on properties of $\Sigma$​.

**Example 3** (Independent sub-Gaussian Random Variables). Suppose that $X\_1, \ldots, X\_n \sim$ $\operatorname{subGaussian}(K)$. One may be interested in $\Vert X\Vert \_{\psi\_2}$, where $X=\left(X\_1, \ldots, X\_n\right)$. Similar to Example 1, it will turn out that the sub-Gaussian norm of the vector will be equal to the sub-Gaussian norm of an individual random variable. To see this, recall from Lecture 4 that, for scalars $\left(a\_1, \ldots, a\_n\right)$, we have that:
$$
P\left(\left|\sum\_{i=1}^n a X\_i\right| \geq t\right) \leq 2 \exp \left(\frac{-t^2}{2 K^2\Vert a\Vert ^2}\right)
$$
It follows that:
$$
\sup \_{\Vert v\Vert =1} P(|\langle v, X\rangle| \geq t) \leq 2 \exp \left(\frac{-t^2}{2 K^2}\right)
$$

Therefore, $X$ is also sub-Gaussian with the same sub-Gaussian norm.
These examples suggest that the sub-Gaussian (and sub-Exponential) norms don't really depend on dimension when the vector has independent components. However, dependence is quite typical in applications. In these cases, Example 2 suggests that the sub-Gaussian norm can depend on the dependence structure of the vector and may grow as $n$ increases.

## Appendix

**Proposition 4**. For $z \geq 0$,
$$
|z-1| \geq \delta \Longrightarrow\left|z^2-1\right| \geq \max \left(\delta, \delta^2\right)
$$

*Proof.* To see this, if $z \geq 1+\delta, z^2-1$ is non-negative, and:
$$
\begin{aligned}
z^2-1 & =(z-1)(z+1) \newline
& \geq \delta(\delta+2) \newline
& \geq \max \left(\delta^2, \delta\right)
\end{aligned}
$$

If $0 \leq z \leq 1-\delta, z^2-1$ is non-positive and:
$$
\begin{aligned}
1-z^2 & \geq(1-z)(1+z) \newline
& \geq(1-z)^2 \newline
& \geq \delta^2
\end{aligned}
$$

We also have:
$$
1-z^2 \geq 1-z \geq \delta
$$

Combining all cases, we have:
$$
\left|z^2-1\right| \geq \max \left(\delta, \delta^2\right)
$$

# 4. Random Matrices

We first start by reviewing the notion of eigenvalues and eigenvectors. In what follows, let $A$ be a real, $n \times n$ matrix.

**Definition 1**. $\lambda$ is a (right) eigenvalue with corresponding (right) eigenvector $v \neq 0$ if:
$$
A v=\lambda v
$$

The above notion corresponds to right multiplication of a matrix $A$ by an appropriate vector $v$. It is also possible to consider left eigenvalues and eigenvectors. A left eigenvalue/eigenvector pair $(\lambda, v)$ satisfies:
$$
v^T A=\lambda v^T \Longleftrightarrow A^T v=\lambda v .
$$

Thus, while left and right eigenvalues/eigenvectors may differ in general, they are equivalent when $A$ is symmetric.

The eigenvalues of $A$ are the roots of the characteristic polynomial $p\_\lambda(A)$, defined as:
$$
p\_\lambda(A)=\operatorname{det}(A-\lambda I) .
$$

The idea is that $A v=\lambda v$ for $v \neq 0$ implies that $(A-\lambda I)$ is singular for appropriate $\lambda$ and thus the determinant is 0 for these choices of $\lambda$. The quantity $p\_\lambda(A)$ is a polynomial in $\lambda$.

Note that in general, polynomials can have complex roots; thus eigenvalues of real matrices can be imaginary (eigenvectors can have complex numbers as components as well). However, note the following:

**Proposition 1**. Suppose $A$ is a $n \times n$ real, symmetric matrix. Then, all eigenvalues (and entries of the eigenvectors) of $A$ are real.

One may consider a related quantity known as singular values. For a real $m \times n$ matrix $A$, a singular value and associated left and right singular vectors satisfy:
$$
A v=\sigma u, \quad A^T u=\sigma v
$$

Unlike eigenvalues, singular values are non-negative.

Any real symmetric $n \times n$ matrix $A$ admits an eigendecomposition of the form:
$$
A=V D V^T
$$
with $V$ orthonormal $\left(V^T V=I, V V^T=I\right)$, and $D$ is a diagonal matrix of the form
$$
D=\left[\begin{array}{lll}
\lambda\_1 & & 0 \newline
& \ddots & \newline
0 & & \lambda\_n
\end{array}\right]
$$
where $\lambda\_1, \ldots, \lambda\_n$ are eigenvalues of $A$ (for concreteness, here we will say the are ordered in descending order by magnitude) and the columns of $V$ contain the corresponding eigenvectors of $A$. It is also common to express $A$ in outerproduct form; that is,
$$
A=\sum\_{i=1}^n \lambda\_i v\_i v\_i^T .
$$

Recall that the trace of a $n \times n$ matrix is given by:
$$
\operatorname{trace}(A)=\sum\_{i=1}^n a\_{i i}
$$

The trace satisfies the cyclic property; for $n \times n$ matrices $A, B, C$ :
$$
\operatorname{trace}(A B C)=\operatorname{trace}(C A B)=\operatorname{trace}(B C A)
$$

Note that arbitrary permutations are not allowed; for example, in general, $\operatorname{trace}(A B C) \neq \operatorname{trace}(A C B)$. We need to preserve the ordering $A \rightarrow B \rightarrow$ $C \rightarrow A$, where order is still preserved when the last element is moved to the front. Combining the eigendecomposition with trace, we may derive the following property:
$$
\begin{aligned}
\operatorname{trace}(A) & =\operatorname{trace}\left(V D V^T\right) \newline
& =\operatorname{trace}\left(V^T V D\right) \newline
& =\sum\_{i=1}^n \lambda\_i
\end{aligned}
$$
We now consider SVD, a more general decomposition, although it is commonly proved using an eigendecomposition of a related symmetric matrix.
Any $m \times n$ real matrix $A$ permits a factorization of the form:
$$
A=\underbrace{U}\_{m \times m} \underbrace{D}\_{m \times n} \underbrace{V^T}\_{n \times n}
$$
where $D$ is a $m \times n$ diagonal matrix with singular values $\sigma\_1 \geq \ldots \geq \sigma\_r \geq 0$ on the diagonal. In fact, the number of non-zero singular values can be shown to be equivalent to the rank of the matrix, so $r=\operatorname{rank}(A) . U$ and $V$ are both orthonormal; that is, $U^T U=U U^T=I\_m$ and $V^T V=V V^T=I\_n$. The columns of $U$ contain the left singular vectors whereas the columns of $V$ contain the right singular vectors.

Using the left and right-singular vectors, $A$ can be written also be written in outer product form as follows:
$$
A=\sum\_{i=1}^r \sigma\_i u\_i v\_i^T .
$$

Moreover, using the SVD to express $A A^T$ (and $A^T A$ ), we see that:
$$
\begin{aligned}
& A^T A=\left(U D V^T\right)^T\left(U D V^T\right)=V D^T U^T U D V^T=V D^T D V^T \newline
& A A^T=\left(U D V^T\right)\left(U D V^T\right)^T=U D D^T U^T,
\end{aligned}
$$

We recognize these expressions as eigendecompositions for $A^T A$ and $A A^T$, respectively. The left singular vectors are eigenvectors of $A A^T$ whereas the right singular vectors correspond to eigenvectors of $A^T A$. Moreover, by examining the diagonal elements of $D D^T$ and $D^T D$, we obtain following relation between the singular values of $A$ and the eigenvalues of $A A^T\left(\right.$ and $A^T A$ ):
$$
\sigma\_i^2(A)=\lambda\_i\left(A A^T\right)=\lambda\_i\left(A^T A\right) .
$$

For real, square symmetric $A$, if we order the eigenvalues by magnitude, we have the relation:
$$
\sigma\_i(A)=\left|\lambda\_i(A)\right|
$$

## Variational Characterizations of Eigenvalues and Singular Values

In what follows, suppose $A$ is a real, symmetric matrix with eigenvalues $\lambda\_1 \geq$ $\ldots \geq \lambda\_n$. One can express the maximum eigenvalue $\lambda\_1$ in terms of the following optimization problem:
$$
\lambda\_1=\max \_{\Vert v\Vert =1} v^T A v=\max \_{v \neq 0} \frac{v^T A v}{v^T v}
$$

In the previous lecture, we were interested in the vector that maximizes this quantity. The quantity $v^T A v / v^T v$ is known as the Rayleigh quotient.
As we saw previously, we also have the following representation for $\lambda\_k$ :
$$
\lambda\_k=\max \_{\substack{v \neq 0 \newline v\_j^T v=0 \quad \forall j<k}} \frac{v^T A v}{v^T v}
$$
where $v\_1, \ldots, v\_n$ are the eigenvectors associated with $\lambda\_1, \ldots, \lambda\_n$. For the minimum eigenvalue $\lambda\_n$, we also have:
$$
\lambda\_n=\min \_{\Vert v\Vert =1} v^T A v=\min \_{v \neq 0} \frac{v^T A v}{v^T v}
$$

We also have the following result, which states that the eigenvalues are also solutions of an optimization problem over a more general constraint set:

**Theorem 1** (Courant-Fischer). Let $A$ be an $n \times n$ real, symmetric matrix with eigenvalues $\lambda\_1 \geq \cdots \geq \lambda\_n$. Furthermore, let $\mathcal{V}\_k$ denote the set of subspaces of $\mathbb{R}^n$ of dimension $k$. Then,
$$
\begin{aligned}
\lambda\_k & =\max \_{W \in \mathcal{V}\_k} \min \_{x \in W, x \neq 0} \frac{x^T A x}{x^T x} \newline
& =\min \_{W \in \mathcal{V}\_{n-k+1}} \max \_{x \in W, x \neq 0} \frac{x^T A x}{x^T x}
\end{aligned}
$$

For example, for $\lambda\_2$, we minimize the Rayleigh quotient for a two-dimensional subspace; however, we choose the two-dimensional subspace that makes this minimum as large as possible. In this case, we choose $v\_1, v\_2$, and the minimizer is $v\_2$, giving us $\lambda\_2$. Alternatively, we maximize the Rayleigh quotient, but take the $n-1$ dimensional subspace that minimizes this quantity. We can choose the subspace that excludes $v\_1$, and then the maximizer is the eigenvector corresponding to the largest remaining eigenvalue $\lambda\_2$​.

Let $A \in \mathbb{R}^{m \times n}$. We have similar variational representations for singular values. For example,
$$
\begin{aligned}
& \sigma\_1(A)=\max \_{x \in \mathcal{S}^{m-1}, y \in \mathcal{S}^{n-1}} x^T A y=\max \_{x, y \neq 0} \frac{x^T A y}{\Vert x\Vert \Vert y\Vert } \newline
& \sigma\_n(A)=\min \_{x \in \mathcal{S}^{m-1}, y \in \mathcal{S}^{n-1}} x^T A y=\min \_{x, y \neq 0} \frac{x^T A y}{\Vert x\Vert \Vert y\Vert }
\end{aligned}
$$

Moreover,
$$
\sigma\_k=\max \_{\substack{x, y \neq 0 \newline x\_j^T x=0 \forall j<k \newline y\_j^T y=0 \forall j<k}} \frac{x^T A y}{\Vert x\Vert \Vert y\Vert }
$$

Since $\sigma\_i^2(A)=\lambda\_i\left(A^T A\right)=\lambda\_i\left(A A^T\right)$, we also have from the variational characterization of eigenvalues:
$$
\begin{aligned}
\sigma\_k & =\max \_{W \in \mathcal{V}\_k} \min \_{x \in W, x \neq 0} \frac{\Vert A x\Vert }{\Vert x\Vert } \newline
& =\min \_{W \in \mathcal{V}\_{n-k+1}} \max \_{x \in W, x \neq 0} \frac{\Vert A x\Vert }{\Vert x\Vert }
\end{aligned}
$$

## Norms on Matrices

Norms are functions that characterize the size of a mathematical object. While we have mostly been working with norms in $\mathbb{R}^d$, one can define norms for more general vector spaces. We consider norms for matrices below.

**Definition 1** (Matrix Norm). Let $\mathcal{V}$ denote the space of all real $m \times n$ matrices. A matrix norm $\Vert \cdot\Vert : \mathcal{V} \mapsto \mathbb{R}$ is a function that satisfies:

1. $\Vert x\Vert  \geq 0$
2. $\Vert x\Vert =0 \Longleftrightarrow x=0$
3. $\Vert \alpha x\Vert =|\alpha| \cdot\Vert x\Vert $
4. $\Vert x+y\Vert  \leq\Vert x\Vert +\Vert y\Vert $

We now state important norms for matrices. The first one is the Frobenius norm, which we have seen before. We can view the Frobenius norm as an entrywise 2-norm. However, some of the alternative representations below are useful.

**Definition 2** (Frobenius norm). Let $B$ be an $m \times n$ matrix, the Frobenius norm of $B$, denoted $\Vert B\Vert \_F$, is given by
$$
\begin{aligned}
\Vert B\Vert \_F & =\sqrt{\sum\_{i=1}^m \sum\_{j=1}^n B\_{i j}^2} \newline
& =\sqrt{\operatorname{trace}\left(B B^T\right)} \newline
& =\sqrt{\operatorname{trace}\left(U \Sigma U^T\right)} \quad \text { by eigendecomposition of } B B^T \newline
& =\sqrt{\sum\_{i=1}^{\min (m, n)} \sigma\_i^2(B)}
\end{aligned}
$$

The last expression demonstrates that the Frobenius norm is closely related to the spectral properties of a matrix. In fact, the Frobenius norm is a type of Schatten norm, which we define below.

**Definition 3** (Schatten $p$-norm). Suppose that $A \in \mathbb{R}^{m \times n}$. The Schatten $p$ norm of $A$ is given by:
$$
\Vert A\Vert \_{\mathcal{S}\_p}=\left(\sum\_{i=1}^{\min (m, n)} \sigma\_i^p\right)^{1 / p}
$$

In other words, Schatten $p$-norms are simply $\ell\_p$​ norms on singular values. It turns out that a norm on singular values also results in a norm for the corresponding matrices. Another important norm is the operator-norm or induced 2 -norm, which we have previously seen.

**Definition 4** (Operator norm). Suppose $A \in \mathbb{R}^{m \times n}$. Then the operator norm of $A$ is defined as:
$$
\begin{aligned}
\Vert B\Vert \_{o p} & =\sup \_{\Vert v\Vert =1}\Vert B v\Vert  \newline
& =\sup \_{\Vert v\Vert  \leq 1}\Vert B v\Vert  \newline
& =\sup \_{\Vert v\Vert <1}\Vert B v\Vert  \newline
& =\sup \_{v \neq 0} \frac{\Vert B v\Vert }{\Vert v\Vert } \newline
& =\inf \left(c>0 \mid\Vert A v\Vert  \leq c\Vert v\Vert  \forall v \in \mathbb{R}^n\right)
\end{aligned}
$$

The first and fourth formulations of the operator norm are arguably the most common; it is okay if you remember just those ones. Intuitively, with the operator norm, we are measuring the size of $B$ by what it does to unit vectors. Again, we take a worst-case type norm with respect the quantity $B v$​. We also have the following important equivalence:

**Proposition 1** (Operator norm and maximum singular value). Let $B$ be a real, $m \times n$ matrix and let $\sigma\_1(B)$ be its largest singular value. Then,
$$
\Vert B\Vert \_{o p}=\sigma\_1(B)
$$

This proposition immediately follows from the variational characterization of singular values. The operator norm has several important/useful properties. First, since it gives a worst case bound on $\Vert A v\Vert $ over unit vectors, we have the following:

**Proposition 2** (Upper bounds on matrix-vector products). For any $m \times n$ vector $B$ and vector $v \in \mathbb{R}^n$,
$$
\Vert B v\Vert  \leq\Vert B\Vert \_{o p}\Vert v\Vert 
$$

Proof. This property follows immediately from the last characterization of the operator norm. Alternatively, for $v \neq 0$,
$$
\Vert B v\Vert  \leq \sup \_{v \neq 0} \frac{\Vert B v\Vert }{\Vert v\Vert } \cdot\Vert v\Vert =\Vert B\Vert \_{o p}\Vert v\Vert 
$$

For $v=0$, the upper bound is trivially true.
Now, suppose that $A, B$ are compatible matrices and consider the product $A B$. A matrix norm is said to be sub-multiplicative if:
$$
\Vert A B\Vert  \leq\Vert A\Vert \Vert B\Vert 
$$

Not all matrix norms are sub-multiplicative. However, the operator norm is, as we demonstrate below.

**Proposition 3**. The operator norm $\Vert \cdot\Vert \_{o p}$ is sub-multiplicative.
Proof. Observe that, for any $v \in \mathbb{R}^n$,
$$
\Vert A(B v)\Vert  \leq\Vert A\Vert \_{o p}\Vert B v\Vert 
$$

Therefore, it follows that:
$$
\Vert A B\Vert \_{o p} \leq\Vert A\Vert \_{o p} \cdot \sup \_{\Vert v\Vert =1}\Vert B v\Vert =\Vert A\Vert \_{o p}\Vert B\Vert \_{o p}
$$

Now, we establish the relationship between the Frobenius and operator norms below.

**Proposition 4**. For any $m \times n$ matrix $A$ with $\operatorname{rank}(A)=r$,
$$
\Vert A\Vert \_{o p} \leq\Vert A\Vert \_F \leq \sqrt{r}\Vert A\Vert \_{o p}
$$

Proof. Since $\Vert A\Vert \_{o p}=\sigma\_1(A)=\max \_{1 \leq i \leq \min (m, n)} \sigma\_i$, it is the Schatten $\infty$-norm. Recall that for $\ell^p$ norms on $\mathbb{R}^d,\Vert x\Vert \_{\infty} \leq\Vert x\Vert \_2 \leq \sqrt{d}\Vert x\Vert \_{\infty}$. The result follows after applying this inequality to the vector of singular values $\left(\sigma\_1, \ldots, \sigma\_r\right)$.

Arguably, the most practically important part of the previous proposition is that $\Vert A\Vert \_{o p} \leq\Vert A\Vert \_F$. While the operator norm is perhaps less intuitive than the Frobenius norm, it is generally smaller; in fact, the two norms are only equal to each other when $\operatorname{rank}(A) \leq 1$. The operator norm will often turn out to be the "right" norm to consider when working with high-dimensional matrices.

We now establish a result related to sub-multiplicativity of the Frobenius norm. While the Frobenius norm is sub-multiplicative, the upper bound below is tighter and often more useful.

**Proposition 5**. Suppose that $A$ and $B$ are conformable matrices. Then, the following hold:
$$
\Vert A B\Vert \_F \leq\Vert A\Vert \_F\Vert B\Vert \_{o p},\Vert A B\Vert \_F \leq\Vert A\Vert \_{o p}\Vert B\Vert \_F
$$

Proof. We show the latter inequality; the proof for the former is analogous. For concreteness, suppose $A \in \mathbb{R}^{m \times n}, B \in \mathbb{R}^{n, p}$. Let $b\_1, \ldots, b\_p$ denote the columns of $B$. Since $A B=\left(A b\_1, \ldots, A b\_p\right)^T$ and the Frobenius-norm is an element-wise 2-norm, it follows that $\Vert A B\Vert \_F^2=\sum\_{i=1}^p\left\Vert A b\_i\right\Vert ^2$. Moreover,
$$
\begin{aligned}
\Vert A B\Vert \_F^2=\sum\_{i=1}^p\left\Vert A b\_i\right\Vert ^2 & \leq \sum\_{i=1}^p\Vert A\Vert \_{o p}^2\left\Vert b\_i\right\Vert ^2 \newline
& =\Vert A\Vert \_{o p}^2 \sum\_{i=1}^p\left\Vert b\_i\right\Vert ^2=\Vert A\Vert \_{o p}^2\Vert B\Vert \_F^2
\end{aligned}
$$

The result follows after taking the square root of both sides of the inequality.

## Other Matrix Norms

While the Frobenius and operator norms are the most common in high-dimensional statistics and probability, one should also be familiar with a few other norms. One such norm is the entrywise maximum norm, defined as:
$$
\Vert A\Vert \_{\infty}=\max \_{i, j}\left|A\_{i j}\right|
$$

We will compare how the errors $\Vert \hat{\Sigma}-\Sigma\Vert \_{o p}$ and $\Vert \hat{\Sigma}-\Sigma\Vert \_{\infty}$ differ as $d$ grows with $n$ in a few lectures. It turns out that the norm $\Vert \cdot\Vert \_{\infty}$ scales much better with dimension (it does not tend to grow as fast), so covariance matrix estimation is easier in this norm. Unfortunately, the performance of various procedures related to the spectral properties of $\Sigma$ depend on $\Vert \cdot\Vert \_{o p}$ instead, which does not scale as well as $d$ grows.
$\ell\_{p, q}$ norms are also relatively common. For an $m \times n$ matrix $A$, the $\ell\_{p, q}$ first applies the $\ell\_p$ norm to columns $a\_1, \ldots, a\_n$. Then, an $\ell\_q$ norm is applied to the vector $\left(\left\Vert a\_1\right\Vert \_p, \ldots,\left\Vert a\_n\right\Vert \_p\right)$. Thus,
$$
\Vert A\Vert \_{p, q}=\left(\sum\_{j=1}^n\left\Vert a\_j\right\Vert \_p^q\right)^{1 / q}=\left(\sum\_{j=1}^n\left(\sum\_{i=1}^m\left|a\_{i j}\right|^p\right)^{q / p}\right)^{1 / q}
$$

Common norms of this type include:
$$
\Vert A\Vert \_{2,1}=\sum\_{j=1}^n\left\Vert a\_j\right\Vert \_2=\sum\_{j=1}^n\left(\sum\_{i=1}^m\left|a\_{i j}\right|^2\right)^{1 / 2}
$$
and:
$$
\Vert A\Vert \_{1, \infty}=\max \_{1 \leq j \leq n} \sum\_{i=1}^m\left|a\_{i j}\right|
$$

It turns out that the norm $\Vert \cdot\Vert \_{1, \infty}$ is equivalent to an operator norm of the form:
$$
\Vert A\Vert \_{o p, 1}=\sup \_{\Vert x\Vert \_1=1}\Vert A x\Vert \_1=\max \_{1 \leq j \leq n} \sum\_{i=1}^m\left|a\_{i j}\right|
$$

Similarly, we have:
$$
\Vert A\Vert \_{o p, \infty}=\sup \_{\Vert x\Vert \_{\infty}=1}\Vert A x\Vert \_{\infty}=\max \_{1 \leq i \leq m} \sum\_{j=1}^n\left|a\_{i j}\right|
$$

## Spectral Perturbation

### Introduction

Suppose a $n \times n$ symmetric matrix $A$ can be expressed as
$$
A=\underbrace{M}\_{\text {signal }}+\underbrace{E}\_{\text {noise }} .
$$

A common question that arises in the analysis of various algorithms in data science is the following: when are the eigenvalues/eigenvectors of $A$ close to those of $M$ ? One may also consider similar questions related to $m \times n$ matrices and the singular values/singular vectors of analgous matrices.

Suppose $X\_i \in \mathbb{R}^d$ and $\mathbb{E}\left[X\_i\right]=0$. In the context of PCA, the above quantities are:
$$
\begin{aligned}
A & =\hat{\Sigma}=\frac{1}{n} \sum\_{i=1}^n X\_i X\_i^T \newline
M & =\Sigma=E\left(X X^T\right), \newline
E & =\hat{\Sigma}-\Sigma=\frac{1}{n} \sum\_{i=1}^n X\_i X\_i^T-E\left(X X^T\right)
\end{aligned}
$$

It will turn out that, in general, closeness of eigenvalues and eigenvectors of $A$ to $M$ will be related to $\Vert E\Vert \_{o p}=\Vert A-M\Vert \_{o p}$, how close they are in the spectral norm. We state inequalities below that establish this connection.

### Eigenvalue Perturbation

Our first result gives us a bound on how much eigenvalues of a matrix can change when it is perturbed by noise. The bound below is very general in the sense that the perturbation can be deterministic, probabilistic, or adversarial.

**Theorem 1** (Weyl's inequality). Suppose $A, B$ are real symmetric matrices with eigenvalues $\lambda\_1(A) \geq \cdots \geq \lambda\_n(A)$, and $\lambda\_1(B) \geq \cdots \geq \lambda\_n(B)$, respectively. Then
$$
\max \_{1 \leq i \leq n}\left|\lambda\_i(A)-\lambda\_i(B)\right| \leq\Vert A-B\Vert \_{o p}
$$
Applying Weyl's inequality to covariance matrices, we have:
$$
\max \_{1 \leq i \leq n}\left|\lambda\_i(\hat{\Sigma})-\lambda\_i(\Sigma)\right| \leq\Vert \hat{\Sigma}-\Sigma\Vert \_{o p} .
$$

Therefore, if we have a bound on $\Vert \hat{\Sigma}-\Sigma\Vert \_{o p}$, we can say how close sample eigenvalues are to their population counterparts. At this point in the course, we have not developed bounds for the operator norm of a covariance matrix; we will do this soon.

It turns out that one can show a similar result for singular values. We state this result below.

**Theorem 2** (Weyl's inequality for singular values). Let $p=\min (m, n)$ and suppose that $A, B$ are $m \times n$ matrices with singular values $\sigma\_1(A) \geq \cdots \geq \sigma\_p(A)$ and $\sigma\_1(B) \geq \cdots \geq \sigma\_p(B)$ respectively. Then,
$$
\max \_{1 \leq i \leq p}\left|\sigma\_i(A)-\sigma\_i(B)\right| \leq\Vert A-B\Vert \_{o p} .
$$

In certain situations, one needs to control the deviation of eigenvalues in a stronger norm than the $\infty$​-norm. The following result a celebrated result from linear algebra.

**Theorem 3** (Hoffman-Wielandt inequality). Under the same conditions as Weyl's inequality,
$$
\sum\_{i=1}^n\left(\lambda\_i(A)-\lambda\_i(B)\right)^2 \leq\Vert A-B\Vert \_F^2 .
$$

More generally,
$$
\left\Vert \lambda\_i(A)-\lambda\_i(B)\right\Vert \_p \leq\Vert A-B\Vert \_{\mathcal{S}\_p} .
$$

Above, $\left\Vert \lambda\_i(A)\right\Vert \_p$ is the $\ell^p$ norm applied to the vector $\left(\lambda\_1(A), \ldots, \lambda\_n(A)\right)$ and $\Vert \cdot\Vert \_{\mathcal{S}\_p}$ is the Schatten $p$-norm. We will not use the Hoffman-Wielandt inequality much in this course, but Weyl's inequality is helpful. It should be noted that, while Weyl's inequality is "sharp" in general, it is possible to improve on the upper bound if one imposes more structure on the noise (e.g. the noise matrix $E$ has independent components and is light-tailed).

### Eigenvector Perturbation

When are, for example, eigenvectors of $\hat{\Sigma}$ and $\Sigma$ close? This turns out to be delicate question because eigenvectors are not uniquely defined. As discussed previously, if $v$ is an eigenvector corresponding to the eigenvalue $\lambda$, then so is $-v$ since:
$$
-A v=-\lambda v \Longleftrightarrow A v=\lambda v
$$
If the multiplicity of an eigenvalue is greater than 1 (we have repeated eigenvalues), then any linear combination of eigenvectors corresponding to $\lambda$ is also an eigenvector corresponding to $\lambda$. To see this, observe that:
$$
A(a u+b v)=\lambda(a u+b v)
$$

Therefore, when we have repeated eigenvalues, then we need to discuss closeness of subspaces spanned by a subset of eigenvectors.

The standard way of comparing two subspaces of dimension $d$, which we denote $E$ and $F$, is to compute canonical angles $\left(\theta\_1, \ldots, \theta\_d\right)$. We start by explaining the intuition for the first angle $\theta\_1$. Let's say that $E=F$. Then, we should be able to pick one unit vector from both $E$ and $F$ so that the vectors are perfectly aligned.

If the subspaces are the same, we should be able to pick another pair of unit vectors that are perfectly aligned and orthogonal to the first vectors. We should be able to do this $d$ times since the subspaces are $d$-dimensional. If the subspaces are not equal to each other, then at some point, we would not be able to pick vectors that are perfectly aligned.
So, how do we compute angles? Recall from calculus that:
$$
\begin{aligned}
a^T b & =\Vert a\Vert \Vert b\Vert  \cos \theta, \newline
\Longrightarrow a^T b & =\cos \theta \text { if } a, b \text { are unit vectors. }
\end{aligned}
$$

Therefore, we consider $\theta=\cos ^{-1}\left(a^T b\right)$. We will only consider $0 \leq a^T b \leq 1$, which corresponds to $0 \leq \theta \leq \pi / 2$. We now define the first canonical angle below. In what follows let $\operatorname{col}(A)$ denote the column space of a matrix $A$.

**Definition 1** (Canonical angle). Let $E$ and $F$ be $n \times d$ matrices with orthonormal columns, where $n \geq d$. The first canonical angle is given by
$$
\begin{aligned}
& \theta\_1=\cos ^{-1}\left(\sup \_{\substack{u \in \operatorname{col}(E), v \in \operatorname{col}(F) \newline
\Vert u\Vert =1,\Vert v\Vert =1}} u^T v\right) \newline
& \stackrel{(i)}{=} \cos ^{-1}\left(\sup \_{\Vert E x\Vert =1,\Vert E y\Vert =1}(E x)^T(F y)\right) \newline
& \stackrel{(i i)}{=} \cos ^{-1}\left(\sup \_{\mid x\Vert =1,\Vert  y \Vert =1} x^T\left(E^T F\right) y\right) \newline
& =\cos ^{-1}\left(\sigma\_1\left(E^T F\right)\right)=\cos ^{-1}\left(\sigma\_1\left(F^T E\right)\right) \newline
&
\end{aligned}
$$
The $k^{\text {th }}$ canonical angle is given by
$$
\begin{aligned}
& \theta\_k=\cos ^{-1}\left(\sup \_{\substack{u \in \operatorname{col}(E), v \in \operatorname{col}(F) \newline
\Vert u\Vert =1,\Vert v\Vert =1 \newline
u^T u\_r=0, v^T v\_r=0, \forall 0<r<k}} u^T v\right) \newline
& =\cos ^{-1}\left(\sigma\_k\left(E^T F\right)\right)=\cos ^{-1}\left(\sigma\_k\left(F^T E\right)\right) . \newline
&
\end{aligned}
$$

For $(i)$, notice that maximizing over $u \in \operatorname{col}(E), v \in \operatorname{col}(F)$ with $u$ and $v$ unit vectors is equivalent to maximizing over $E x$ and $F y$ where each of these are unit vectors. For $(i i)$, notice that $\Vert E x\Vert ^2=x^T E^T E x=\Vert x\Vert ^2$ and similarly, $\Vert F y\Vert ^2=\Vert y\Vert ^2$. Therefore, it suffices to enforce $\Vert x\Vert =1,\Vert y\Vert =1$, even though the dimension of $x, y$ need not be the same as the dimension of $u, v$.

Since $\cos (0)=1$, it is common to consider $\sin \theta$ when one considers distances related to principle angles. Let $\sin \Theta=\operatorname{diag}\left(\sin \theta\_1, \ldots, \sin \theta\_d\right) \in \mathbb{R}^{d \times d}$. It turns out that $\Vert \sin \Theta\Vert \_F$ is a metric on $d$-dimensional linear spaces.

In what follows, we state a variant of the Davis-Kahan $\sin \Theta$ theorem, which establishes perturbation bounds for eigenvectors. There are general theorems related to $\Vert \sin \Theta\Vert \_F$, but in what follows, we focus on the important special case in which we are interested in comparing subspaces of dimension 1. Let $0 \leq \angle(u, v) \leq \pi / 2$ denote the (canonical) angle between $u$ and $v$. We have the follow result:

Theorem 4 (Davis-Kahan $\sin \Theta$ Theorem). Let $S$ and $T$ be symmetric, $n \times n$ matrices. Suppose that the ith eigenvalue of $S$ is well separated from the rest of the spectrum; that is,
$$
\min \_{j \neq i}\left|\lambda\_j(S)-\lambda\_i(S)\right|>\delta
$$
for some $\delta>0$. Then, the angle between eigenvectors corresponding to the ith largest eigenvalues of $S$ and $T$ satisfies:
$$
\sin \angle\left(v\_i(S), v\_i(T)\right) \leq \frac{2\Vert S-T\Vert \_{o p}}{\delta}
$$

The Davis-Kahan theorem gives us a sufficient condition when eigenvectors of $\hat{\Sigma}$ and $\Sigma$ are close. First, suppose that the eigenvector of interest corresponds to a distinct eigenvalue of $\Sigma$. Then, we have some eigengap $\delta$, and we have that:
$$
\sin \angle\left(v\_i(\hat{\Sigma}), v\_i(\Sigma)\right) \leq \frac{2\Vert \hat{\Sigma}-\Sigma\Vert \_{o p}}{\delta}
$$

Thus, the angle depends mostly on the quantity $\Vert \hat{\Sigma}-\Sigma\Vert \_{o p}$. For some intuition as to why the bound also depends on the eigengap $\delta$, if the gap between population eigenvalues is small, then when we add the noise $E=\hat{\Sigma}-\Sigma$, it becomes difficult to tell which eigenvector of $\hat{\Sigma}$ is closely related to the $i$ th eigenvalue of $\Sigma$.

So how is the angle related to the actual distance between two vectors? We have the following corollary.

**Corollary 1**. Suppose that the conditions of the Davis-Kahan Theorem are met. Then,
$$
\min \_{c \in\{-1,1\}}\left\Vert c v\_i(S)-v\_i(T)\right\Vert  \leq \frac{2^{3 / 2}\Vert S-T\Vert \_{o p}}{\delta}
$$

Proof. The result will follow if we can show that:
$$
\min \_{c \in\{-1,1\}}\left\Vert c v\_i(S)-v\_i(T)\right\Vert  \leq \sqrt{2} \sin \angle\left(v\_i(S), v\_i(T)\right)
$$

To this end, pick $\tilde{c}$ so that $\left\langle\tilde{c} v\_i(S), v\_i(T)\right\rangle \geq 0$ and let $\tilde{v}\_i=\tilde{c} v\_i(S), v\_i=v\_i(T)$. Now, observe that
$$
\begin{aligned}
\min \_{c \in\{-1,1\}}\left\Vert c v\_i(S)-v\_i(T)\right\Vert ^2 & \leq\left\Vert \tilde{v}\_i-v\_i\right\Vert ^2 \newline
& =\left\Vert \tilde{v}\_i\right\Vert ^2-2\left\langle\tilde{v}\_i, v\_i\right\rangle+\left\Vert v\_i\right\Vert ^2 \newline
& =2\left(1-\tilde{v}\_i^T v\_i\right) \qquad \left(\tilde{v}\_i \text { and } v\_i \text { are unit vectors }\right)\newline
& \leq 2\left(1-\left(\tilde{v}\_i^T v\_i\right)^2\right)\qquad \left(0 \leq \tilde{v}\_i^T v\_i \leq 1 \Longrightarrow\left(\tilde{v}\_i^T v\_i\right)^2 \leq \tilde{v}\_i^T v\_i\right) \newline
& =2\left[1-\cos ^2 \angle\left(\tilde{v}\_i, v\_i\right)\right] \qquad \left(\tilde{v}\_i^T v\_i=\cos \angle\left(\tilde{v}\_i, v\_i\right)\right)\newline
& =2 \sin ^2 \angle\left(\tilde{v}\_i, v\_i\right) \qquad \left(\sin ^2 \theta+\cos ^2 \theta=1\right)
\end{aligned}
$$
The claim follows after taking the square root of both sides of the inequality.

## Bounds on the Operator Norm of Covariance Matrices

###  Approximating the Unit Sphere with Nets

Suppose that $X\_1, \ldots, X\_n$ are independent random vectors in $\mathbb{R}^d$ with mean 0 . Let $\hat{\Sigma}=\frac{1}{n} \sum\_{i=1}^n X\_i X\_i^T$ and $\Sigma=E(\hat{\Sigma})$. Let $A=\hat{\Sigma}-\Sigma$, which is a real, symmetric matrix. By a variational characterization of singular values, we have:
$$
\Vert A\Vert \_{o p}=\sup \_{x \in \mathcal{S}^{d-1}}\left|x^T A x\right|
$$

Since $\sigma(A)=\max \left(\lambda\_1(A),\left|\lambda\_n(A)\right|\right)$ for real, symmetric matrices, we can recover $\sigma\_1(A)$ by taking the absolute value of a variational characterization of eigenvalues. This quantity is related to the maximum we have considered before for sub-Gaussian random variables, but is more complicated since we are considering all unit vectors. A common trick in these situations is to approximate an infinite set with a finite set, where we perhaps consider finer approximations as $n$ grows. In this case, we will be satisfied with one approximation of a fixed resolution, which will give us an upper bound on the operator norm that at least gets the order (approximate size of the operator norm) right.

It turns out that we can approximate the (uncountably) infinite set $\mathcal{S}^{d-1}$ in the following way: we can choose a finite collection of unit vectors $x\_1^{\*}, \ldots, x\_N^{\*}$ such that for each $x \in \mathcal{S}^{d-1}$, there exists an $x\_i^{\*}$ such that $\left\Vert x-x\_i^{\*}\right\Vert  \leq \varepsilon$. The idea is perhaps easiest to visualize with the unit cube in $\mathbb{R}^3$, which is related to a different norm, but the intuition is the same.

We can fill up the unit cube with a finite number of smaller cubes (some of the smaller cubes may protrude from the unit cube, but this is ok for a covering). If each cube represents an appropriate $\varepsilon$-neighborhood of a point $x^{\*}$, then of course, it is possible to construct a finite collection that has the desired property. The idea is similar with $d-1$ spheres, where $d$ is an arbitrary dimension. Of course, how large $N$ needs to be will depend on the desired accuracy $\varepsilon$ and volume, which in turn depends on the dimension $d$.

In what follows let $(\mathcal{X},\Vert \cdot\Vert )$ be a normed space, with the induced metric $d(x, y)=\Vert x-y\Vert $. Today, we will consider the case where $\mathcal{X}=\mathbb{R}^d$, but later on in the course, we will allow $\mathcal{X}$ to be a space of functions, equipped with an appropriate norm.

**Definition 1** ( $\varepsilon$-net). Let $(\mathcal{X},\Vert \cdot\Vert )$ be a normed space and let $K \subseteq \mathcal{X}$ be a subset. A subset $\mathcal{N}\_\varepsilon \subseteq K$ is an $\varepsilon$-net or $\varepsilon$-covering of $K$ if every point in $K$ is within distance $\varepsilon$ of some point in $\mathcal{N}\_\varepsilon$; in other words,
$$
\forall x \in K, \exists x\_0 \in \mathcal{N}\_\varepsilon \text { s.t. } d\left(x, x\_0\right) \leq \varepsilon
$$

**Definition 2** (Covering Number). Let $(\mathcal{X},\Vert \cdot\Vert )$ be a normed space. The covering number $\mathcal{N}(K, d, \varepsilon)$ is defined as:
$$
\mathcal{N}(K,\Vert \cdot\Vert , \varepsilon)=\min \{N \mid \exists \text { an } \varepsilon \text {-covering of } K \text { of cardinality } N\}
$$

With some of these concepts in hand (we will come back to properties of covering numbers and so forth shortly), we are now ready to prove a bound related to the operator norm of the estimation error associated with covariance matrix estimation. To this end, we provide a proposition below that gives an upper bound on the operator norm after approximating with an $\varepsilon$-net.

**Proposition 1**. Let $A$ be a symmetric, real $n \times n$ matrix and $\mathcal{N}\_\varepsilon$ be an $\varepsilon$-net of $\mathcal{S}^{d-1}$. Then,
$$
\Vert A\Vert \_{o p} \leq \frac{1}{1-2 \varepsilon} \max \_{y \in \mathcal{N}\_\varepsilon}\left|y^T A y\right|
$$

*Proof*. Choose $x^{\*}$ so that $\Vert A\Vert \_{o p}=\left|x^{* T} A x^{\*}\right|$ (we know that such a maximizer exists and is one of the eigenvectors of $A$ ). Pick $y^{\*} \in \mathcal{N}\_\varepsilon$ such that $d\left(x^{\*}, y^{\*}\right) \leq \varepsilon$. Now, using Cauchy-Schwarz inequality in the first inequality,
$$
\begin{aligned}
\left|x^{* T} A x^{\*}-y^{* T} A y^{\*}\right| & =\left|\left(x^{* T} A x^{\*}-x^{* T} A y^{\*}\right)+\left(x^{* T} A y^{\*}-y^{* T} A y^{\*}\right)\right| \newline
& \leq\left\Vert x^{\*}\right\Vert  \cdot\left\Vert A\left(x^{\*}-y^{\*}\right)\right\Vert +\left\Vert y^{\*}\right\Vert  \cdot\left\Vert A\left(x^{\*}-y^{\*}\right)\right\Vert  \newline
& \leq 2 \varepsilon\Vert A\Vert \_{o p}
\end{aligned}
$$
Therefore, it follows that:
$$
\begin{aligned}
\Vert A\Vert \_{o p} & =\left|x^{* T} A x^{\*}\right| \newline
& \leq\left|x^{* T} A x^{\*}-y^{* T} A y^{\*}\right|+\left|y^{* T} A y^{\*}\right| \newline
& \leq 2 \varepsilon\Vert A\Vert \_{o p}+\max \_{y \in \mathcal{N}\_\varepsilon}\left|y^T A y\right|
\end{aligned}
$$

Now, observe that:
$$
\Vert A\Vert \_{o p} \leq 2 \varepsilon\Vert A\Vert \_{o p}+\max \_{y \in \mathcal{N}\_\varepsilon}\left|y^T A y\right| \Longrightarrow\Vert A\Vert \_{o p} \leq \frac{1}{1-2 \varepsilon} \max \_{y \in \mathcal{N}\_\varepsilon}\left|y^T A y\right|
$$

The result follows.

### A Tail Bound for the Operator Norm

Now, we are finally ready to provide a bound on the operator norm. After the proving the theorem, we will translate it into a statement that gives us an idea of how large $d$ can be relative to $n$.

**Theorem 1**. Suppose that $X\_1, \ldots, X\_n \in \mathbb{R}^d$ are independent, mean $0, \operatorname{sub} G\left(\sigma^2\right)$ random vectors. Then, there exists some $K$ depending only on $\sigma^2$ such that:
$$
P\left(\Vert \hat{\Sigma}-\Sigma\Vert \_{o p} \geq t\right) \leq 2 \cdot 9^d \exp \left(-K n \min \left(t^2, t\right)\right)
$$

Proof. Let $\varepsilon=1 / 4$. Then, by Proposition 1, we have that:
$$
\Vert \hat{\Sigma}-\Sigma\Vert \_{o p} \leq 2 \max \_{y \in \mathcal{N}\_{1 / 4}} y^T(\hat{\Sigma}-\Sigma) y
$$

Thus, by a union bound, if $\mathcal{N}\_{1 / 4}$ is chosen to be a minimal covering, we have that:
$$
\begin{aligned}
P\left(\Vert \hat{\Sigma}-\Sigma\Vert \_{o p} \geq t\right) & \leq P\left(\max \_{y \in \mathcal{N}\_{1 / 4}}\left|2 y^T(\hat{\Sigma}-\Sigma) y\right| \geq t\right) \newline
& \leq N\left(\mathcal{S}^{d-1},\Vert \cdot\Vert \_2, 1 / 4\right) \max \_{y \in \mathcal{N}\_{1 / 4}} P\left(2\left|y^T(\hat{\Sigma}-\Sigma) y\right| \geq t\right)
\end{aligned}
$$

We will argue later in these lecture notes that $N\left(\mathcal{S}^{d-1},\Vert \cdot\Vert \_2, 1 / 4\right) \leq 9^d$. Moreover, observe that, for any $y \in \mathcal{N}\_{1 / 4}$ :
$$
\begin{aligned}
P\left(2\left|y^T \hat{\Sigma} y-y^T \Sigma y\right| \geq t\right) & =P\left(\left|\frac{1}{n} \sum\_{i=1}^n\left(y^T X\_i\right)^2-E\left[\left(y^T X\_i\right)^2\right]\right| \geq \frac{t}{2}\right) \newline
& =P\left(\left|\frac{1}{n} \sum\_{i=1}^n Z\_i^2-E\left[Z\_i^2\right]\right| \geq \frac{t}{2}\right)
\end{aligned}
$$
where $Z\_i \sim \operatorname{SubG}\left(\sigma^2\right)$, and therefore, $Z\_i^2 \sim \operatorname{subE}\left(\sigma^2\right)$. Therefore, by Bernstein's inequality, we have:
$$
P\left(\Vert \hat{\Sigma}-\Sigma\Vert \_{o p} \geq t\right) \leq 2 \cdot 9^d \exp \left(-K n \min \left(t^2, t\right)\right)
$$

The claim follows.

Now, how large can $d$ be relative to $n$ ? We can convert the above statement to a high probability bound.

**Corollary 1**. Suppose that the conditions in Theorem 1 hold. Then, there exists $0<C<\infty$ depending on $\sigma$ and $\delta$ such that, with probability at least $1-\delta$,
$$
\Vert \hat{\Sigma}-\Sigma\Vert \_{o p} \leq C\left(\sqrt{\frac{d}{n}}+\frac{d}{n}\right)
$$

Proof. Our strategy will be to pick an appropriate value of $t$ so that the probability statement from Theorem 1 is less than or equal to $\delta$. Observe that:
$$
\begin{aligned}
9^d \exp \left(-K n \min \left(t^2, t\right)\right) & \leq \delta / 2 \newline
\Longrightarrow c d-K n \min \left(t^2, t\right) & \leq \log (\delta / 2) \newline
\Longrightarrow \min \left(t^2, t\right) & \geq \frac{c d}{K n}-\frac{\log (\delta / 2)}{K n} \newline
\Longrightarrow t & \geq \max \left(\sqrt{\frac{K^{\prime} d}{n}}, \frac{K^{\prime} d}{n}\right)
\end{aligned}
$$

Thus, for an appropriate $0<C<\infty$, if we choose $t=C\left(\sqrt{\frac{d}{n}}+\frac{d}{n}\right)$, which is greater than or equal to the max, the result follows.

Unfortunately, the dimension dependence of the covering number is exponential in $d$; therefore, we generally need $d / n \rightarrow 0$. One may look at the bound we derived in Theorem 1 and wonder whether this is loose. Even if we use more sophisticated tools, without additional assumptions, it turns out that we generally need $d / n \rightarrow 0$. PCA, however, can work when $d \gg n$​ if one is willing to make more assumptions, which ultimately boil down to the effective dimension being small even if the dimension is large.

### More on Covering Numbers and Metric Entropy

We now provide some additional background on covering numbers and related concepts, which will then give us the bound $N\left(\mathcal{S}^{d-1},\Vert \cdot\Vert \_2, 1 / 4\right) \leq 9^d$. Covering numbers are closely related to the concept of compactness from real analysis. In fact, a subset $K$ is precompact (or totally bounded) if $N(K, d, \varepsilon)<\infty$ for every $\varepsilon>0$​. The covering number is quantifying a notion of size/volume of the subset.

Later on this course, we will talk more about metric entropy. We define this below.

**Definition 3** (Metric Entropy). Let $(\mathcal{X},\Vert \cdot\Vert )$ be a normed space. The metric entropy of a subset $K \subseteq \mathcal{X}$ is given by:
$$
\log N(K,\Vert \cdot\Vert , \varepsilon)
$$

It will turn out that log scale is more natural in many analyses. For the operator norm bound, we cared a lot about how the covering number depended on $d$, but later on this course, we will also be interested in how fast it increases as $\varepsilon \downarrow 0$, which corresponds to increasing the accuracy of the approximation.

It turns out that covering numbers are closely related to packing numbers, which we define below:

**Definition 4** ( $\varepsilon$-packing). Let $(\mathcal{X},\Vert \cdot\Vert )$ be a normed space. An $\varepsilon$-packing of $K$ is a subset $K\_0 \subseteq K$ such that $d(x, y)>\varepsilon$ for all $x, y \in K\_0$. The packing number $\mathcal{P}(K,\Vert \cdot\Vert , \varepsilon)$ is defined as:
$$
\mathcal{P}(K,\Vert \cdot\Vert , \varepsilon)=\max \{P \mid \exists \text { an } \varepsilon \text {-packing of } K \text { of cardinality } P\}
$$

The following proposition establishes the relationship between packing and covering numbers.

**Proposition 2** (Equivalence of Covering and Packing Numbers). For any $K \subseteq$ $\mathcal{X}$ and $\varepsilon>0$,
$$
\mathcal{P}(K,\Vert \cdot\Vert , 2 \varepsilon) \leq \mathcal{N}(K,\Vert \cdot\Vert , \varepsilon) \leq \mathcal{P}(K,\Vert \cdot\Vert , \varepsilon)
$$

Proof. We will first establish the upper bound $\mathcal{N}(K,\Vert \cdot\Vert , \varepsilon) \leq \mathcal{P}(K,\Vert \cdot\Vert , \varepsilon)$. We will do so by arguing that a maximal packing is in fact a covering of the set $K$. We argue by contradiction. Suppose that a maximal packing is not a covering. Then, there exists some $x \in K$ that is not contained in any $\varepsilon$-ball centered at the elements $K\_0$; that is, $d(x, y)>\varepsilon \forall y \in K\_0$. If this is the case, the we can include an additional ball centered at $x$ to the packing, but this contradicts the assumption that the packing is maximal.

Now, we establish the bound $\mathcal{P}(K,\Vert \cdot\Vert , 2 \varepsilon) \leq \mathcal{N}(K,\Vert \cdot\Vert , \varepsilon)$. Let $K\_{0,2 \varepsilon}$ be a corresponding maximal packing. It suffices to show that we need at least $\mathcal{P}(K,\Vert \cdot\Vert , 2 \varepsilon) \varepsilon$-balls to cover the collection $K\_{0,2 \varepsilon}$. Let $x\_0$ be an arbitrary point in $K\_{0,2 \varepsilon}$ and let $x^{\*} \in K$ be a potential center for the $\varepsilon$-ball containing $x\_0$. By triangle inequality, for any $y\_0 \in K\_{0,2 \varepsilon}$ not equal to $x\_0$,
$$
2 \varepsilon<d\left(x\_0, y\_0\right) \leq d\left(x\_0, x^{\*}\right)+d\left(x^{\*}, y\_0\right) \leq \varepsilon+d\left(x^{\*}, y\_0\right) \Longrightarrow d\left(x^{\*}, y\_0\right)>\varepsilon
$$

Thus, each $\varepsilon$-ball containing an element of $K\_{0,2 \varepsilon}$ contains exactly one element. The result follows.

Now, we proceed to providing a bound the covering number of a set $K$ in terms of volumes of a ball for an arbitrary norm $\Vert \cdot\Vert $. In what follows, let $B\_\varepsilon^{(d)}=\left(x \in \mathbb{R}^d \mid\Vert x\Vert  \leq \varepsilon\right)$ and let $A+B=\{x+y \mid x \in A, y \in B\}$​ denote the Minkowski sum of two sets. We have the following result:

**Proposition 3**. Let $K$ be a subset of $\mathbb{R}^d,\Vert \cdot\Vert $ be a norm and $\varepsilon>0$. Then,
$$
\frac{\operatorname{Vol}(K)}{\operatorname{Vol}\left(B\_\varepsilon^{(d)}\right)} \leq \mathcal{N}(K,\Vert \cdot\Vert , \varepsilon) \leq \mathcal{P}(K,\Vert \cdot\Vert , \varepsilon) \leq \frac{\operatorname{Vol}\left(K+B\_{\varepsilon / 2}^{(d)}\right)}{\operatorname{Vol}\left(B\_{\varepsilon / 2}^{(d)}\right)}
$$

*Proof*. We first note that the inequality $\mathcal{N}(K,\Vert \cdot\Vert , \varepsilon) \leq \mathcal{P}(K,\Vert \cdot\Vert , \varepsilon)$ is proved in Proposition 2. For the lower bound, we have the inequality:
$$
\operatorname{Vol}(K) \leq \mathcal{N}(K,\Vert \cdot\Vert , \varepsilon) \cdot \operatorname{Vol}\left(B\_\varepsilon^{(d)}\right)
$$
since the corresponding covering contains all of $K$, but each of the balls need not be disjoint and hence, some regions maybe double-counted when totaling the volume of the balls. The lower bound follows from re-arranging the inequality.

For the upper bound, note that given a maximal packing, one can construct a collection of disjoint balls of radius $\varepsilon / 2$ with centers given by the elements of the packing. These balls may not be contained in $K$ (the centers of these balls may be on the boundary of $K$, for example), but these disjoint balls will be contained in the Minkowski sum $K+B\_{\varepsilon / 2}$. Therefore, it follows that,
$$
\mathcal{P}(K,\Vert \cdot\Vert , \varepsilon) \cdot \operatorname{Vol}\left(B\_{\varepsilon / 2}^{(d)}\right) \leq \operatorname{Vol}\left(K+B\_{\varepsilon / 2}^{(d)}\right)
$$
and the result follows from rearranging the inequality.
We now use this general result to give a lower and upper bound for the covering number of the unit Euclidean ball, which we denote $\mathcal{B}\_1^{(d)}$. This of course provides an upper bound on the covering number for $\mathcal{S}^{d-1}$.

**Proposition 4** (Covering Number for the Unit Euclidean Ball).
$$
\left(\frac{1}{\varepsilon}\right)^d \leq \mathcal{N}\left(\mathcal{B}\_1^{(d)},\Vert \cdot\Vert \_2, \varepsilon\right) \leq\left(1+\frac{2}{\varepsilon}\right)^d
$$

*Proof*. The volume of a $d$-ball of radius $R$, which we denote $\mathcal{B}\_R^{(d)}$, is given by:
$$
\operatorname{Vol}\left(\mathcal{B}\_R^{(d)}\right)=\frac{\pi^{d / 2} R^d}{\Gamma\left(\frac{d}{2}+1\right)}
$$

Therefore, it follows that:
$$
\operatorname{Vol}\left(\mathcal{B}\_R^{(d)}\right)=R^d \cdot \operatorname{Vol}\left(\mathcal{B}\_1^{(d)}\right)
$$

Since $\mathcal{B}\_1^{(d)}+\mathcal{B}\_{\varepsilon / 2}^{(d)}=\mathcal{B}\_{1+\varepsilon / 2}^{(d)}$, the result follows from Proposition 3.
Using Proposition 4, it is now clear that:
$$
\mathcal{N}\left(\mathcal{S}^{d-1},\Vert \cdot\Vert \_2, 1 / 4\right) \leq \mathcal{N}\left(\mathcal{B}\_1^{(d)},\Vert \cdot\Vert \_2, 1 / 4\right) \leq\left(1+\frac{2}{1 / 4}\right)^d=9^d
$$

