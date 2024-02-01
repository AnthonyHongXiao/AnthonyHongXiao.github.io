+++
title = "High-Dimensional Probability and Statistics"
date = "2024-01-14T12:01:56+08:00"
tags = ["probability"]

+++

This file is for the notes and exercises for the book Roman Vershynin's  [High-Dimensional Probability](/pdfs/HDP-book.pdf), one of the references used in Prof Lunde's Math5440. The other references are Ramon van Handel's [Probability in High Dimension](\pdfs\PHD-book.pdf) and Martin J.Wainwright's [High-Dimensional Statistics](/pdfs/HDS-book.pdf).

Errata and update of HDP: [errata](/pdfs/Vershynin-Errata-2020.pdf), [update](/pdfs/Vershynin-Updates-2020.pdf).

Exercises solns for HDP: [soln](https://zhuanlan.zhihu.com/p/338822722).

Exercises solns for HDS: [soln](https://high-dimensional-statistics.github.io/).

# 0. Appetizer

## Key Takeaways

1. **convex combination** $\sum_{i=1}^m \lambda_i z_i \quad$ where $\quad \lambda_i \geq 0 \quad$ and $\quad \sum_{i=1}^m \lambda_i=1$.

2. **convex hull of a set $T$**, $\mathrm{conv}(T)$ is the set of all convex combinations of $z_1, \cdots, z_m \in T$ for $m \in \mathbb{N}$.

3. **Theorem 0.0.1 (Caratheodory's Theorem)**: Every point in the convex hull of a set $T\subseteq \mathbb{R}^n$ can be expressed as a convex combination of at most $n+1$ points from $T$. 

4. **Theorem 0.0.2 (Approximate form of Caratheodory's Theorem)**: Consider a set $T\subseteq \mathbb{R}^n$ whose diameter is bounded by $1$. Then, for every point $x\in \mathrm{conv}(T)$ and every integer $k$, one can find points $x_1,\cdots,x_k\in T$ such that
   $$
   \left\Vert x-\frac{1}{k}\sum^{k}_{j=1}x_j\right\Vert^2_2\le \frac{1}{\sqrt{k}}
   $$

5. **Corollary 0.0.4 (Covering polytopes by balls)**: Let $P$ be a polytope in $\mathbb{R}^n$ with $N$ vertices and whose diameter is bounded by $1$. Then $P$ can be covered by at most $N^{\lceil{1}/{\varepsilon^2}\rceil}$ Euclidean balls of radii $\varepsilon>0$.

## Exercises

### Exercise 0.0.3

Check the following variance identities, which we used in the proof of Theorem 0.0.2:

**(a)** Let $Z_1, \ldots, Z_k$ be independent mean-zero random vectors in $\mathbb{R}^n$. Show that
$$
\mathbb{E}\left\Vert\sum_{j=1}^k Z_j\right\Vert_2^2=\sum_{j=1}^k \mathbb{E}\left\Vert Z_j\right\Vert_2^2 .
$$

**(b)** Let $Z$ be a random vector in $\mathbb{R}^n$. Show that
$$
\mathbb{E}\Vert Z-\mathbb{E} Z\Vert_2^2=\mathbb{E}\Vert Z\Vert_2^2-\Vert\mathbb{E} Z\Vert_2^2
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

1. **Random Variables**, **expectation** $\mathbb{E}(X)$, **variance** $\mathbb{E}(X-\mathbb{E}(X))^2$, **moment generating function** $M_X(t)=\mathbb{E}(e^{tX})$, **p-th moment** $\mathbb{E}(X^p)$, **p-th absolute moment** $\mathbb{E}(|X|^p)$, and **$L^P$ norm** and **essential norm** of a random variable
   $$
   \begin{aligned}
   \Vert X\Vert_{L^p}&=(\mathbb{E}|X|^p)^{1/p}, p\in (0,\infty)\\
   \Vert X\Vert_{L^{\infty}}&=\mathrm{ess\; sup}|X|=\inf\{M|\;|f|\le M\text{ for }\mu-\text{a.e. }x\in X\}
   \end{aligned}
   $$

2. For fixed $p$ and a given probability space $(\Omega, \Sigma, \mathbb{P})$, the classical vector space $L^p=L^p(\Omega, \Sigma, \mathbb{P})$ consists of all random variables $X$ on $\Omega$ with finite $L^p$ norm, that is
   $$
   L^p=\set{X:\|X\|_{L^p}<\infty}.
   $$

   If $p \in[1, \infty]$, the quantity $\|X\|_{L^p}$ is a norm and $L^p$ is a **Banach space**. This fact follows from **Minkowski's inequality**. For $p<1$, the triangle inequality fails and $\|X\|_{L^p}$ is not a norm.

   The exponent $p=2$ is special in that $L^2$ is not only a Banach space but also a **Hilbert space**. The inner product and the corresponding norm on $L^2$ are given by
   $$
   \langle X, Y\rangle_{L^2}=\mathbb{E} X Y, \quad\|X\|_{L^2}=\left(\mathbb{E}|X|^2\right)^{1 / 2} .
   $$

   Then the **standard deviation** of $X$ can be expressed as
   $$
   \|X-\mathbb{E} X\|_{L^2}=\sqrt{\operatorname{Var}(X)}=\sigma(X) .
   $$

   Similarly, we can express the **covariance** of random variables of $X$ and $Y$ as
   $$
   \operatorname{cov}(X, Y)=\mathbb{E}(X-\mathbb{E} X)(Y-\mathbb{E} Y)=\langle X-\mathbb{E} X, Y-\mathbb{E} Y\rangle_{L^2} .
   $$

3. **Jensen's Inequality**: for $\varphi:\mathbb{R}\to \mathbb{R}$​ convex, we have
   $$
   \varphi(\mathbb{E}X)\le \mathbb{E}\varphi(X)
   $$

4. **Corollary**: $\Vert X\Vert_{L^p}$ is an increasing function in $p$, i.e.
   $$
   \Vert X\Vert_{L^p}\le \Vert X\Vert_{L^q}\quad \text{for any }0\le p\le q=\infty
   $$

5. **Minkowski's inequality**: for any $p\in [1,\infty]$ and any random variables $X,Y\in L^p$​, we have
   $$
   \Vert X+Y\Vert_{L^p}\le \Vert X\Vert_{L^p}+\Vert Y\Vert_{L^p}
   $$

6. **Cauchy-Schwarz inequality**: for any random variables $X,Y\in L^2$, we have
   $$
   |\mathbb{E}XY|\le \Vert X\Vert_{L^2}\Vert Y\Vert_{L^2}
   $$

7. **Holder inequality**: suppose $p,q\in (1,\infty)$ such that $1/p+1/q=1$, i.e., they are **conjugate exponents**. The random variables $X\in L^p$ and $Y\in L^q$​ satisfy
   $$
   |\mathbb{E}XY|\le \Vert X\Vert_{L^p}\Vert Y\Vert_{L^q}
   $$
   The inequality also holds for the pair $p=1,q=\infty$.

8. Definition of **distribution**, **propability density function (pdf)**, and **cumulative distribution function (cdf)**.

9. **Lemma 1.2.1 (Integral identity)**. Let $X$ be a non-negative random variable. Then
   $$
   \mathbb{E} X=\int_0^{\infty} \mathbb{P}\{X>t\} d t .
   $$

   The two sides of this identity are either finite or infinite simultaneously.

10. **Exercise 1.2.2 (Generalization of integral identity)**. for any random variable $X$ (not necessarily non-negative):
    $$
    \mathbb{E} X=\int_0^{\infty} \mathbb{P}\{X>t\} d t-\int_{-\infty}^0 \mathbb{P}\{X<t\} d t
    $$

11. **Exercise 1.2.3 ( $p$-moments via tails)**. Let $X$ be a random variable and $p \in(0, \infty)$. Show that
    $$
    \mathbb{E}|X|^p=\int_0^{\infty} p t^{p-1} \mathbb{P}\{|X|>t\} d t
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
    &\mathbb{E}(aX+b)=a\mathbb{E}(X)+b\\
    &\operatorname{Var}(aX+b)=a^2\operatorname{Var}(X)\\
    \end{aligned}
    $$
    **Proposition (Ross (e8) p.129, p.191)**: The expectation of function of random variable is given by
    $$
    \begin{aligned}
    \mathbb{E}[g(X)]&=\sum_xg(x)p(x)\\
    \mathbb{E}[g(X)]&=\int_{-\infty}^{\infty}g(x)f(x)dx
    \end{aligned}
    $$
    **Proposition (Ross (e8) p.298)**: if $X$ and $Y$ have a joint probability mass function $p(x,y)$, then
    $$
    \mathbb{E}[g(X,Y)]=\sum_y\sum_x g(x,y)p(x,y)
    $$
    If they have joint probability density function $f(x,y)$, then
    $$
    \mathbb{E}[g(X,Y)]=\int_{-\infty}^{\infty}\int_{-\infty}^{\infty}g(x,y)f(x,y)dxdy
    $$
    **Corollary (Ross e8 p.299)**: for finite $X,Y$ and $g(X,Y)=X+Y$, we have $\mathbb E(X+Y)=\mathbb E(X)+\mathbb E(Y)$.

    **Variance of sum of var.**: if they are independent,
    $$
    \operatorname{Var}(X_1+\cdots+X_n)=\operatorname{Var}(X_1)+\cdots+\operatorname{Var}(X_n)
    $$
    if they are also identically distributed,
    $$
    \operatorname{Var}\left(\frac{1}{N} \sum_{i=1}^N X_i\right)=\frac{\sigma^2}{N}
    $$
    For more formulae, see Ross (e8) p.322 section 7.4 Covariance, Variance of Sums, and Correlations.

15. **Theorem 1.3.1 (Strong law of large numbers)**. Let $X_1, X_2, \ldots$ be a sequence of i.i.d. random variables with mean $\mu$. Consider the sum
    $$
    S_N=X_1+\cdots +X_N .
    $$

    Then, as $N \rightarrow \infty$,
    $$
    \frac{S_N}{N} \rightarrow \mu \quad \text { almost surely. }
    $$
    That is, **converges in probability**: for any $\varepsilon>0$,
    $$
    \lim_{N\to \infty}\mathbb{P}\left(\left|\frac{S_N}{N}-\mu\right|\le \varepsilon\right)=1
    $$

16. **Theorem 1.3.2 (Lindeberg-Lévy central limit theorem)**. Let $X_1, X_2, \ldots$ be a sequence of i.i.d. random variables with mean $\mu$ and variance $\sigma^2$. Consider the sum
    $$
    S_N=X_1+\cdots+X_N
    $$
    and normalize it to obtain a random variable with zero mean and unit variance as follows:
    $$
    Z_N:=\frac{S_N-\mathbb{E} S_N}{\sqrt{\operatorname{Var}\left(S_N\right)}}=\frac{1}{\sigma \sqrt{N}} \sum_{i=1}^N\left(X_i-\mu\right) .
    $$

    Then, as $N \rightarrow \infty$,
    $$
    Z_N \rightarrow N(0,1) \text { in distribution. }
    $$

    That is, **converges in distribution**: for a sequence of r.v. $X_i$ with their cdf $F_{X_i}$, one has pointwise convergence of $F_{X_i}$ to cdf $F_X$ of a r.v. $X$:
    $$
    \forall x,\lim_{N\to \infty}F_i(x)=F(x)
    $$
    The convergence in distribution means that the $\mathrm{CDF}$ of the normalized sum converges pointwise to the CDF of the standard normal distribution. We can express this in terms of tails as follows. Then for every $t \in \mathbb{R}$, we have
    $$
    \mathbb{P}\set{Z_N \geq t} \rightarrow \mathbb{P}\{g \geq t\}=\frac{1}{\sqrt{2 \pi}} \int_t^{\infty} e^{-x^2 / 2} d x
    $$
    as $N \rightarrow \infty$, where $g \sim N(0,1)$​ is a standard normal random variable.

17. **Corollary (de Moivre-Laplace theorem)**: 

    One remarkable special case of the central limit theorem is where $X_i$ are Bernoulli random variables with some fixed parameter $p \in(0,1)$, denoted
    $$
    X_i \sim \operatorname{Ber}(p) .
    $$

    Recall that this means that $X_i$ take values 1 and 0 with probabilities $p$ and $1-p$ respectively; also recall that $\mathbb{E} X_i=p$ and $\operatorname{Var}\left(X_i\right)=p(1-p)$. The sum
    $$
    S_N:=X_1+\cdots+X_N
    $$
    is said to have the binomial distribution $\operatorname{Binom}(N, p)$. The central limit theorem (Theorem 1.3.2) yields that as $N \rightarrow \infty$,
    $$
    \frac{S_N-N p}{\sqrt{N p(1-p)}} \rightarrow N(0,1) \text { in distribution. }
    $$

18. **Corollary (Poisson limit theorem)**: 

    Theorem 1.3.4 (Poisson Limit Theorem). Let $X_{N, i}, 1 \leq i \leq N$, be independent random variables $X_{N, i} \sim \operatorname{Ber}\left(p_{N, i}\right)$, and let $S_N=\sum_{i=1}^N X_{N, i}$. Assume that, as $N \rightarrow \infty$,
    $$
    \max_{i \leq N} p_{N, i} \rightarrow 0 \quad \text{ and } \quad \mathbb{E} S_N=\sum_{i=1}^N p_{N, i} \rightarrow \lambda<\infty .
    $$

    Then, as $N \rightarrow \infty$,
    $$
    S_N \rightarrow \operatorname{Pois}(\lambda) \quad\text { in distribution. }
    $$

# 2. Concentration of Sums of Independent Random Variables

## Key Takeaways

### 2.1 Why Concentration Inequalities?

- An example (Question 2.1.1) on estimation of number of heads of flipping coins by Chebyshev's inequality and central limit theorem.

- Our Math5440 gives some more examples (see Lecture 2).

### 2.2 Hoeffding's Inequality

- symmetric Bernoulli distribution is the uniform distribution for discrete variable $X$ that takes values $1$ and $-1$, i.e., $\mathbb{P}(X=1)=\mathbb{P}(X=-1)=\frac{1}{2}$.

**Theorem 2.2.2 (Hoeffding's Inequality)**: Let $X_1,\cdots,X_N$ be independent symmetric Bernoulli random variables, and let $a=(a_1,\cdots,a_N)\in \R^N$. Then, for any $t>0$, we have
$$
\mathbb{P}\left[\sum_{i=1}^Na_iX_i\ge t\right]\le \mathbb P\left(-\frac{t^2}{2\Vert a\Vert_2^2}\right)
$$
**Remark 2.2.4 (Non-asymptotic results)**: Note that CLT gives a bound of tail that works for large $N$​, while Hoeffding bound gets rid of that requirement.

Two generalizations are given:

**Theorem 2.2.5 (Two sided Hoeffding's inequality)** Let $X_i$ and $a$ be the same. Then, for $t>0$,
$$
\mathbb{p}\left[\left|\sum_{i=1}^Na_iX_i\right|\ge t\right]\le 2\exp\left(-\frac{t^2}{2\Vert a\Vert_2^2}\right)
$$
**Theorem 2.2.6 (Hoeffding's inequaity for general bounded random variables)** Let $X_1,\cdots,X_N$ be independent random variables. Assume that $X_i\in [m_i,M_i]$ for every $i$. Then, for any $t>0$, we have
$$
\mathbb{P}\left[\sum_{i=1}^N(X_i-\mathbb{E}X_i)\ge t\right]\le \exp\left(-\frac{2t^2}{\sum_{i=1}^N(M_1-m_1)^2}\right)
$$

### 2.3 Chernoff's Inequality

**Theorem 2.3.1 (Chernoff's inequality (upper tail))**

Let $X_i$ be independent Bernoulli random variables with parameters $p_i$. Consider their sum $S_N=\sum_{i=1}^NX_i$ and denote its mean by $\mu=\mathbb{E}S_N$. Then, for $t>\mu$, we have
$$
\mathbb{E}[S_N\le t]\le e^{-\mu}\left(\frac{e\mu}{t}\right)^t
$$
**Exercise 2.3.2 (Chernoff's inequality (lower tail))**

Let $X_i$ and $S_N$ be the same. When $t<\mu$, we have
$$
\mathbb{E}[S_N\le t]\le e^{-\mu}\left(\frac{e\mu}{t}\right)^t
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
- $\Vert X\Vert_{L^p}=(\mathbb{E}|X|^p)^{1/p}=\sqrt{2}\left(\frac{\Gamma((1+p)/2)}{\Gamma(1/2)}\right)^{1/p}$.
- $\Vert X\Vert_{L^P}=O(\sqrt{p}),\quad  p\to \infty$.
- Its MGF is given by $\mathbb{E}(e^{tX})=e^{t^2/2},\quad \forall t\in \R$.

#### Some facts about Beta and Gamma functions

(Rudin's *Introduction to Mathematical Analysis* (e3) p.192 has some of the following properties.)

- Beta Function $B(x,y)=\int_0^1 t^{x-1}(1-t)^{y-1}dt$. This indefinite integral is convergent for  $x>0,y<0$.

- Gamma Function $\Gamma(x)=\int_0^{+\infty}t^{x-1}e^{-t}dt$. This indefinite integral is convergent for $x>0$.

- property 1: for $0<x<\infty$, $\Gamma (x+ 1) = x\Gamma(x)$.

- property 2: $\Gamma(n)=n!$ for $n=1,2,3,\cdots$.

- property 3: $\log \Gamma$ is convex on $(0,\infty)$.

- property 4: if $x>0$ and $y>0$, then
  $$
  B(x,y)=\int_0^1 t^{x-1}(1-t)^{y-1}dt=\frac{\Gamma(x)\Gamma(y)}{\Gamma(x+y)}
  $$

- property 5: both $\Beta$ and $\Gamma$ are continuous on their convergent regions.

- property 6 (**Stirling's Formula**): 
  $$
  \lim _{x \rightarrow \infty} \frac{\Gamma(x+1)}{(x / e)^x \sqrt{2 \pi x}}=1
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
P(X-\mu \geq t) & \leq \inf _{\lambda>0} E\left(e^{\lambda(X-\mu)}\right) e^{-\lambda t} \\
& \leq \inf _{\lambda>0} \exp \left(\frac{\lambda^2 \sigma^2}{2}-\lambda t\right) \\
& \left.=\exp \left(\frac{t^2}{2 \sigma^2}-\frac{t^2}{\sigma^2}\right) \text { (plugging in minimizer } \lambda=t / \sigma^2\right) \\
& =\exp \left(\frac{-t^2}{2 \sigma^2}\right)
\end{aligned}
$$

Therefore, if a random variable is sub-Gaussian, we have tail decay of the form $\exp \left(-t^2 / 2 K_1^2\right)$, which is quite fast. One can show an analogous bound for the left tail. So what random variables are sub-Gaussian? It turns out that bounded random variables are sub-Gaussian.

**Proposition 1**. Suppose $X$ is mean 0 and $a \leq X \leq b$ with probability 1. Then, $X$ is sub-Gaussian with $\sigma^2=(b-a)^2 / 4$.

In what follows, let $K_i$ be the sub-Gaussian constant associated with the $i$-th notion of sub-Gaussianity. It turns out that different notions of sub-Gaussianity are equivalent in the sense that they are related to each other by some universal constant. In other words, if $X ∼ \mathrm{subGaussian}(K_i)$, then there exists some constant $C$ (that does not depend on the distribution of $X$) such that $X ∼ \mathrm{subGaussian}(CK_j)$ for an equivalent notion of sub-Gaussianity. Another way of saying this is that for any $i,j=1,\cdots,5$, there is some absolute constant $C$ such that $K_i\le CK_j$.

**Proposition 2.5.2 (Sub-Gaussian Properties)**: Let $X$ be a random variable. Then the following properties are equivalent.

(i) The tails of $X$ satisfy
$$
\mathbb{P}\{|X| \geq t\} \leq 2 \exp \left(-t^2 / K_1^2\right) \quad \text { for all } t \geq 0 .
$$
(ii) The moments of $X$ satisfy
$$
\|X\|_{L^p}=\left(\mathbb{E}|X|^p\right)^{1 / p} \leq K_2 \sqrt{p} \quad \text { for all } p \geq 1 .
$$
(iii) The MGF of $X^2$ satisfies
$$
\mathbb{E} \exp \left(\lambda^2 X^2\right) \leq \exp \left(K_3^2 \lambda^2\right) \quad \text { for all } \lambda \text { such that }|\lambda| \leq \frac{1}{K_3} \text {. }
$$
(iv) The MGF of $X^2$ is bounded at some point, namely
$$
\mathbb{E} \exp \left(X^2 / K_4^2\right) \leq 2 .
$$

Moreover, if $\mathbb{E} X=0$ then properties $i$-iv are also equivalent to the following one.
(v) The MGF of $X$ satisfies
$$
\mathbb{E} \exp (\lambda X) \leq \exp \left(K_5^2 \lambda^2\right) \quad \text { for all } \lambda \in \mathbb{R}
$$
**Orlicz Norm** and **Sub-Gaussian Norm**:

Suppose that $\Psi:[0, \infty) \mapsto[0, \infty)$ is a monotone increasing, convex function such that $\Psi(0)=0$ and $\lim _{x \rightarrow \infty} \Psi(x)=\infty$. The **Orlicz space** $L_\psi =L_\psi (\Omega,\Sigma,\mathbb P)$ consists of all random variables $X$ on the probability space $(\Omega,\Sigma,\mathbb P)$ with finite Orlicz norm, i.e., $L_\psi :=\{X:\Vert X\Vert_{\psi}<\infty\}$ where the **Orlicz norm** of a random variable $X$ is given by
$$
\|X\|_{\Psi}=\inf \left\{t>0: \mathbb E\left[\Psi\left(\frac{|X|}{t}\right)\right] \leq 1\right\}
$$

It can be shown that this is indeed a norm on the space of random variables for which this quantity is finite. When we put $\psi(x)=x^p$ for $p\ge 1$, the resulting Orlicz space is the classical space $L^p$.  It can also shown that for the choice of function $\psi_2(x)=e^{x^2}-1$, the sub-Gaussian condition:
$$
\mathbb E\left(\exp \left(X^2 / K_4^2\right)\right) \leq 2
$$
is equivalent to:
$$
\|X\|_{\psi_2} \leq K_4
$$

We let this **sub-Gaussian norm** of a sub-Gaussian be specifically denoted as
$$
\Vert X\Vert_{\psi_2}=\inf \{t>0:\mathbb E\exp(X^2/t^2)\le 2\}
$$
 Other restatements of sub-Gaussianities using the norm are given in (2.14)-(2.16):
$$
\begin{gathered}
\mathbb{P}\{|X| \geq t\} \leq 2 \exp \left(-c t^2 /\|X\|_{\psi_2}^2\right) \quad \text { for all } t \geq 0 \\
\|X\|_{L^p} \leq C\|X\|_{\psi_2} \sqrt{p} \quad \text { for all } p \geq 1 \\
\mathbb{E} \exp \left(X^2 /\|X\|_{\psi_2}^2\right) \leq 2 \\
\text{if }\mathbb{E} X=0\text{ then }\mathbb{E} \exp (\lambda X) \leq \exp \left(C \lambda^2\|X\|_{\psi_2}^2\right) \quad\forall \lambda \in \mathbb{R}
\end{gathered}
$$
where $c,C$ are absolute constants. Morover, up to absolute constant factors, $\Vert X\Vert_{\psi_2}$ is the smallest possible number that makes each of these inequalities holds. 

**Examples and non-examples of sub-gaussian r.v.**

(i) **Gaussian** ☑️: Due to equation (2.3) from the book and symmetry, we have that for for $X\sim N(0,1)$ and any $p\ge 1$, $\mathbb{P}[|X|\ge t]\le 2\exp(-t^2/2)\quad \forall t\in R$ . Therefore, it is sub-Gaussian. In fact, if $X\sim N(0,\sigma^2)$, we recall that the MGF of $X\sim N(\mu,\sigma^2)$ is $\exp (\mu t+\sigma^2t^2/2)$. For $\mu=0$, this is $\exp (\sigma^2t^2/2)$. Criterion (v) of Proposition 2.5.2 then concludes that it is sub-Gaussian.

(ii) **Bernoulli** ☑️: Let $X$ be a random variable with symmetric Bernoulli distribution. Since $|X|=1$, it follows that $X$ is a sub-Gaussian random variable with $\Vert X\Vert_{\psi_2}=\frac{1}{\sqrt{\ln 2}}$. Just note that when $t\ge 1$, we have
$$
\mathbb P[|X|\ge t]=0\le 2\exp(-t^2/K^2_1)
$$
When $t<1$, we have
$$
\mathbb P[|X|\ge t]=1
$$
By letting $K_1=\frac{1}{\sqrt{\ln 2}}$​ and noticing that $t<1\Rightarrow -t^2>-1$, we have 
$$
2\exp \left(-\frac{t^2}{-\frac{1}{\ln 2}}\right)=2\cdot 2^{-t^2}>2\cdot 2^{-1}=1= \mathbb P[|X|\ge t]
$$
(iii) **Bounded** ☑️: More generally, any bounded random variable $X$ is a sub-Gaussian random variable with
$$
\Vert X\Vert_{\psi_2}\le C\Vert X\Vert_{\infty}
$$
where $C=1/\sqrt{\ln 2}$.

(iv) **Poisson** ❌: let $X\sim \mathrm{Pois}(\lambda)$. Note that $X=k=0,1,\cdots$ Then its pmf is
$$
f(k ; \lambda)=\mathbb P(X=k)=\frac{\lambda^k e^{-\lambda}}{k !}
$$
Now, let $m$ be the smallest integer that is larger or equal to $t$. Then
$$
\mathbb P(|X|\ge t)=\mathbb P(X \geq t)=\sum_{k\ge t}\mathbb P(X=k)>\frac{e^{-\lambda} \lambda^m}{m !}
$$
Then apply Stirling's approximation to get a lower bound that decay slower than Gaussian.

(v) **Exponential** ❌: let $X\sim \mathrm{Exp}(\lambda)$. Then,
$$
f(x ; \lambda)= \begin{cases}\lambda e^{-\lambda x} & x \geq 0 \\ 0 & x<0\end{cases}
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

(vi) **Pareto** ❌: It is one of those heavy-tailed dist. Its pdf is $f(x)=\frac{\alpha x_m^{\alpha}}{x^{\alpha+1}}$, and its cdf is $1-\left(\frac{x_m}{x}\right)^{\alpha}$. Thus,
$$
\mathbb P[|X|\ge t]=\mathbb P[X\ge t]=\left(\frac{x_m}{x}\right)^{\alpha}
$$
It is easy to see that the polynomial decay is slower than the gaussian one.

(vii) **Cauchy** ❌: Another heavy-tailed dist. Compare its growth to gaussian.

### 2.6 General Hoeffding and Khintchine Inequalities

The **rotation invariance property** (i.i.d $X_i\sim N(0,\sigma_i^2)\Rightarrow\sum{i=1}^NX_i\sim N\left(0,\sum^N_{i=1}\sigma_i^2\right)$)  extends to the sub-Gaussians, albeit up to an absolute constant.

**Proposition 2.6.1 (Sums of independent sub-Gaussians)**: Let $X_1,\cdots,X_N$ be independent sub-Gaussians with zero-means. Then $\sum_{i=1}^NX_i$ is also a sub-Gaussian r.v., and
$$
\left\Vert \sum_{i=1}^N X_i^2 \right\Vert_{\psi_2}^2\le C\sum_{i=1}^N\Vert X_i\Vert_{\psi_2}^2
$$
where $C$ is an absolute constant.

**Theorem 2.6.3 (General Hoeffding's inequality)**. Let $X_1, \ldots, X_N$ be independent, mean zero, sub-gaussian random variables, and $a=\left(a_1, \ldots, a_N\right) \in \mathbb{R}^N$. Then, for every $t \geq 0$, we have
$$
\mathbb{P}\left\{\left|\sum_{i=1}^N a_i X_i\right| \geq t\right\} \leq 2 \exp \left(-\frac{c t^2}{K^2\|a\|_2^2}\right)
$$
where $K=\max _i\left\|X_i\right\|_{\psi_2}$​.

**Theorem 2.6.2**: when $a=(1,\cdots,1)$​​ in Theorem 2.6.3 above.

When the means are not zero, we can show that centering does not harm the sub-Gaussian property, just as $\Vert X-\mathbb X\Vert_{L^2}\le \Vert X\Vert_{L^2}$:

**Lema 2.6.8 (Centering)** If $X$ is sub-Gaussian then $X-\mathbb E X$ is sub-Gaussian too and
$$
\Vert X-\mathbb EX\Vert_{\psi_2}\le C\Vert X\Vert_{\psi_2}
$$
where $C$ is an absolute constant.

**Exercise 2.6.5 (Khintchine's inequality).** Let $X_1, \ldots, X_N$ be independent sub-gaussian random variables with zero means and unit variances, and let $a=$ $\left(a_1, \ldots, a_N\right) \in \mathbb{R}^N$. Prove that for every $p \in[2, \infty)$ we have
$$
\left(\sum_{i=1}^N a_i^2\right)^{1 / 2} \leq\left\|\sum_{i=1}^N a_i X_i\right\|_{L^p} \leq C K \sqrt{p}\left(\sum_{i=1}^N a_i^2\right)^{1 / 2}
$$
where $K=\max _i\left\|X_i\right\|_{\psi_2}$ and $C$ is an absolute constant.
**Exercise 2.6.6 (Khintchine's inequality for $p=1$ ).** Show that in the setting of Exercise 2.6.5, we have
$$
c(K)\left(\sum_{i=1}^N a_i^2\right)^{1 / 2} \leq\left\|\sum_{i=1}^N a_i X_i\right\|_{L^1} \leq\left(\sum_{i=1}^N a_i^2\right)^{1 / 2} .
$$

Here $K=\max _i\left\|X_i\right\|_{\psi_2}$ and $c(K)>0$ is a quantity which may depend only on $K$.
Hint: Use the following extrapolation trick. Prove the inequality $\|Z\|_2 \leq\|Z\|_1^{1 / 4}\|Z\|_3^{3 / 4}$ and use it for $Z=\sum a_i X_i$. Get a bound on $\|Z\|_3$ from Khintchine's inequality for $p=3$.
**Exercise 2.6.7 (Khintchine's inequality for $p \in(0,2)$ ).** State and prove a version of Khintchine's inequality for $p \in(0,2)$​.
Hint: Modify the extrapolation trick in Exercise 2.6.6.

### 2.7 Sub-Exponential Distributions

We previously stated that some common families of random variables are not sub-Gaussian. Consider for example the $\chi^2$ distribution, which comes up with some frequency in statistics. Recall that if $Z \sim N(0,1)$, then $Z^2 \sim \chi_1^2$. Thus, for a $\chi^2$ random variable $Y$, we have that:
$$
P(|Y| \geq t)=P\left(Z^2 \geq t\right)=2 P(Z \geq \sqrt{t}) \leq 2 \exp \left(-\frac{t}{2}\right)
$$

Therefore, $\chi^2$ random variables have tails that decay like $\exp (-C t)$ (**exponential decay**) rather than $\exp \left(-C t^2\right)$ (**gaussian decay**) as we have with Gaussian random variables. It turns out that $\chi^2$ random variables are an example of sub-exponential random variables.

**Proposition 2.7.1 (Sub-exponential properties).** Let $X$ be a random variable. Then the following properties are equivalent; the parameters $K_i>0$ appearing in these properties differ from each other by at most an absolute constant factor.

(i) The tails of $X$ satisfy
$$
\mathbb{P}\{|X| \geq t\} \leq 2 \exp \left(-t / K_1\right) \quad \text { for all } t \geq 0 .
$$
(ii) The moments of $X$ satisfy
$$
\|X\|_{L^p}=\left(\mathbb{E}|X|^p\right)^{1 / p} \leq K_2 p \quad \text { for all } p \geq 1 .
$$
(iii) The $M G F$ of $|X|$ satisfies
$$
\mathbb{E} \exp (\lambda|X|) \leq \exp \left(K_3 \lambda\right) \quad \text { for all } \lambda \text { such that } 0 \leq \lambda \leq \frac{1}{K_3} \text {. }
$$
(iv) The MGF of $|X|$ is bounded at some point, namely
$$
\mathbb{E} \exp \left(|X| / K_4\right) \leq 2
$$

Moreover, if $\mathbb{E} X=0$ then properties $a-d$ are also equivalent to the following one.
(v) The MGF of $X$ satisfies
$$
\mathbb{E} \exp (\lambda X) \leq \exp \left(K_5^2 \lambda^2\right) \quad \text { for all } \lambda \text { such that }|\lambda| \leq \frac{1}{K_5}
$$
**Definition 2.7.5 (Sub-exponential random variables).** A random variable $X$ that satisfies one of the equivalent properties (i)-(iv) Proposition 2.7.1 is called a **sub-exponential random variable**. The sub-exponential norm of $X$, denoted $\|X\|_{\psi_1}$, is defined to be the smallest $K_3$ in property 3. In other words,
$$
\|X\|_{\psi_1}=\inf \{t>0: \mathbb{E} \exp (|X| / t) \leq 2\} .
$$

Sub-gaussian and sub-exponential distributions are closely related. First, any sub-gaussian distribution is clearly sub-exponential.

Second, the square of a sub-gaussian random variable is sub-exponential (**Lemma 2.7.6**); more generally, the product of two sub-gaussian random variables is sub-exponential (**Lemma 2.7.7**).

**Example 2.7.8 (sub-exponentials)** Let us mention a few examples of sub-exponential random variables. As we just learned, all sub-gaussian random variables and their squares are sub-exponential, for example $g^2$ for $g\sim N(\mu,\sigma)$​. Apart from that, sub-exponential distributions include the exponential and Poisson distributions. 

**Exercise 2.7.10 (Centering)** With a similar proof as Lemma 2.6.8, we can show that for sub-exponential $X$,
$$
\Vert X-\mathbb E X\Vert_{\psi_1}\le C\Vert X\Vert_{\psi_1}
$$

## Exercises

### Exercise 2.1.4

Let $g\sim N(0,1)$. Show that, for all $t>1$, we have
$$
\mathbb{E}(g^2\mathbf{1}_{\{g>t\}})=t\frac{1}{\sqrt{2\pi}}e^{-t^2/2}+\mathbb{P}\{g>t\}\le \left(t+\frac{1}{t}\right)\frac{1}{\sqrt{2\pi}}e^{-t^2/2}
$$
*soln*:

The pdf of $g\sim N(0,1)$ is $p(x)=\frac{1}{\sqrt{2\pi}}e^{-x^2/2}$. We observe that $p'(x)=-x\frac{1}{\sqrt{2\pi}}e^{-x^2/2}=-xp(x)$. By formula (27) (expectation of function of variable), we compute
$$
\begin{aligned}
\mathbb{E}(g^2\mathbf{1}_{\{g>t\}})&=\int_t^{\infty}x^2p(x)dx\\
&=\int_t^{\infty}-xp'(x)dx\\
&=[-xp(x)]_t^{\infty}+\int_t^{\infty}p(x)dx\\
&=t\frac{1}{\sqrt{2\pi}}e^{-t^2/2}+\mathbb{P}\{g>t\}
\end{aligned}
$$
where for the last step we notice that $\lim_{x\to \infty}xp(x)=0$ for $p(x)$ decreases exponentially fast to zero. This proved the equality. To show the inequality is obtained by using Proposition 2.1.2 in HDP.

### Exercise 2.2.3

show that
$$
\cosh (x)\le e^{x^2/2},\quad \forall x\in \mathbb{R}
$$
*soln 1*:
$$
\cosh (x)=\prod_{k=1}^{\infty}\left(1+\frac{4 x^2}{\pi^2(2 k-1)^2}\right) \leq \exp \left(\sum_{k=1}^{\infty} \frac{4 x^2}{\pi^2(2 k-1)^2}\right)=\exp \left(x^2 / 2\right)
$$
*soln 2*:

This is equivalent of showing $\ln \cosh(x)\le x^2/2$. Define $f(x)=\ln (\cosh x)-x^2 / 2$ and see that $f^{\prime}(x)=\tanh (x)-x$. Let it be zero to find maximum of $f$.

### Exercise 2.2.8

(Boosting Randomized Algorithm) Calculate the probability of correctness for majority vote where each voter has $\frac{1}{2}+\delta$ probability of being correct.

*soln*:

Let each of the voter be $X_i\sim B(\frac{1}{2}+\delta)$. By Theorem 2.2.6 (Hoeffding's inequaity for general bounded random variables), we have
$$
\begin{aligned}
\mathbb{P}\left[\sum_{i=1}^NX_i\le \frac{N}{2}\right]&= \mathbb{P}\left[\sum_{i=1}^N(-X_i)\ge -\frac{N}{2}\right]\\
&=\mathbb{P}\left[\sum_{i=1}^N((-X_i)-\mathbb{E}(-X_i))\ge -\frac{N}{2}+N\left(\frac{1}{2}+\delta\right)\right]\\
&\le \exp\left(-\frac{2(N\delta)^2}{N}\right)=\exp(-2N\delta^2)
\end{aligned}
$$
When $N\ge \frac{1}{2}\delta^{-2}\ln (\varepsilon^{-1})$, we have $\exp(-2N\delta^2)\le \exp(-\ln(\varepsilon^{-1}))=\varepsilon$. The probability that the answer voted by majority is incorrect is at most $\varepsilon$.

### Exercise 2.2.10

Let $X_1,\cdots,X_N$ be non-negative independent random variables with continuous distributions. Assume that the densities of $X_i$ are uniformly bounded by $1$.

**(a)** Show that the MGF of $X_i$ satisfies 
$$
\mathbb{E}\exp (-tX_i)\le \frac{1}{t}\quad \forall t>0
$$
**(b)** Deduce that, for any $\varepsilon>0$, we have
$$
\mathbb{P}\left[\sum_{i=1}^NX_i\le \varepsilon N\right]\le (e\varepsilon)^N
$$
*soln*:

**(a)** We note that these r.v. are non-negative, so
$$
\mathbb{E}\exp (-tX_i)\le \frac{1}{t}=\int_0^{\infty}p_i(x)e^{-tx}dx
$$
and we bound it by its absolute value and use the condition of uniform boundedness of the family,
$$
\text{RHS}\le \left|\int_0^{\infty}p_i(x)e^{-tx}dx\right|\le \int_0^{\infty}\underbrace{|p_i(x)|}_{\le 1}\underbrace{|e^{-tx}|}_{=e^{-tx}}dx\le\int_0^{\infty}e^{-tx}dx=\left[-\frac{1}{t}e^{-tx}\right]_0^{\infty}=\frac{1}{t}
$$
**(b)** We mimic the proof of Theorem 2.2.2 (Hoeffding's inequality), i.e., using Markov's inequality and the fact that MGF of sum is product of MGF for independent $X_i$:
$$
\begin{aligned}
\mathbb{P}\left[\sum_{i=1}^N X_i\le \varepsilon N\right]&=\mathbb{P}\left[\exp\sum_{i=1}^N(-tX_i)\ge \exp(-t\varepsilon N)\right]\\
&\le \frac{\mathbb{E}\left(\exp \sum_{i=1}^N(-tX_i)\right)}{\exp(-t\varepsilon N)}\\
&=\frac{\prod_{i=1}^N\mathbb{E}\left(\exp (-tX_i)\right)}{\exp(-t\varepsilon N)}\\
&\le e^{t\varepsilon N}\prod_{i=1}^N\frac{1}{t}=e^{t\varepsilon N}/t^N
\end{aligned}
$$
Letting $t=1/\varepsilon$ to maximize it to get $(e\varepsilon)^N$​​​. 

### Exercise 2.5.9

We did this when listing examples and non-examples of sub-Gaussians above.

### Exercise 2.6.5

The first inequality is simply because $\|\bullet\|_{L^2} \leq\|\bullet\|_{L^P}$. As for the second one, by Exercise 1.2 .3 and Hoeffding's inequality (Theorem 2.6.3),
$$
\begin{aligned}
\mathbb{E}\left|\sum_{i=1}^N a_i X_i\right|^p & =\int_0^{\infty} p t^{p-1} \mathbb{P}\left\{\left|\sum_{i=1}^N a_i X_i\right|>t\right\} \mathrm{d} t \\
& \leq 2 p \int_0^{\infty} t^{p-1} \exp \left(-\frac{c t^2}{K^2\|a\|_2^2}\right) \mathrm{d} t \\
& =p\left(\frac{K\|a\|_2}{\sqrt{c}}\right)^p \int_0^{\infty} s^{p / 2-1} \mathrm{e}^{-s} \mathrm{~d} s \quad=p\left(\frac{K\|a\|_2}{\sqrt{c}}\right)^p \Gamma\left(\frac{p}{2}\right) .
\end{aligned}
$$

It follows that $\left\|\sum_{i=1}^N a_i X_i\right\|_{L^p} /\left(K \sqrt{p}\|a\|_2\right) \leq(p \Gamma(p / 2))^{1 / p} / \sqrt{c p}=O(1)$ by Stirling's formula.

### Exercise 2.6.7

The second inequality is simply because $\|\bullet\|_{L^P} \leq\|\bullet\|_{L^2}$. As for the first one, by the Cauchy-Schwartz inequality and Exercise 2.6.5,
$$
\begin{aligned}
\mathbb{E}\left|\sum_{i=1}^N a_i X_i\right|^p & \geq\left(\mathbb{E}\left|\sum_{i=1}^N a_i X_i\right|^2\right)^2 / \mathbb{E}\left|\sum_{i=1}^N a_i X_i\right|^{4-p} \\
& \geq\|a\|_2^4 /\left(C K \sqrt{4-p}\|a\|_2\right)^{4-p} \quad=c_p(K)^p\|a\|_2^p
\end{aligned}
$$
with $c_p(K)=(C K \sqrt{4-p})^{1-4 / p}$​.

### 











