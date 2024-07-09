+++
title = "Compare Two Powers"
date = "2024-07-03T18:07:52+08:00"
tags = []
+++

I found an interesting way to compare two powers, $e^\pi$ and $\pi^e$, although there should have already been many interesting articles illustrating this idea and possibly including couple of more ways to compare them.

Here is the idea:

Consider the function $f(x)=\frac{1}{x}$, which is continuous and strictly decreasing for $x>0$. Notice that $\pi>e$. We then integrate the function over the intervel $[e,\pi]$ too get
$$
\int_{e}^{\pi}\frac{1}{x}dx=\ln\pi-\ln e=\ln\pi -1
$$
which equals to the area under the curve $f(x)$ above the intervel $[e,\pi]$. Since $f(x)$ is strictly decreasing, we have the following inequality:
$$
\underbrace{f(e)(\pi-e)}_{\text{rectangle }ABDC}>\underbrace{\ln\pi -1}_{=\text{area under curve}}>\underbrace{f(\pi)(\pi-e)}_{\text{rectangle }CDEF}
$$
where $A=(e,f(e))$, $B=(\pi,f(e))$, $C=(e,f(\pi))$, $D=(\pi,f(\pi))$, $E=(e,0)$, and $F=(\pi,0)$. We will only use the first inequality, i.e.,
$$
\begin{aligned}
\frac{\pi-e}{e}&>\ln\pi -1\\
\frac{\pi}{e}&>\ln\pi \\
\pi&>\ln\pi^e\\
e^\pi&>\pi^e
\end{aligned}
$$
