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

(a) Let $Z_1, \ldots, Z_k$ be independent mean-zero random vectors in $\mathbb{R}^n$. Show that
$$
\mathbb{E}\left\Vert\sum_{j=1}^k Z_j\right\Vert_2^2=\sum_{j=1}^k \mathbb{E}\left\Vert Z_j\right\Vert_2^2 .
$$

(b) Let $Z$ be a random vector in $\mathbb{R}^n$. Show that
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

**Theorem 2.2.5 (Two sided Hoeffding's inequality)**

**Theorem 2.2.6 (Hoeffding's inequaity for general bounded random variables)**

### 2.3 Chernoff's Inequality



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

