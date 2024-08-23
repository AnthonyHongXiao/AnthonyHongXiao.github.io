+++
title = "Multifractal"
date = "2024-08-18T23:21:31+08:00"
tags = []
+++

# Local Dimensions and Multifractal Spectra

Multifractals provide a complex and rich framework for understanding the intricate structures seen in various natural phenomena and mathematical constructs. Central to the study of multifractals are the concepts of local dimensions and multifractal spectra, particularly the functions $ f(\alpha) $ and $ \tau(q) $. These tools allow for a deep understanding of the variability in scaling behavior across different subsets of a fractal.

## Local Dimensions

Local dimensions offer insights into the density of measures at specific points within a set or fractal structure.

### Definition of Local Dimension

For a measure $ \mu $ on $ \mathbb{R}^n $ and a point $ x $ in its support, the local dimension at $ x $, denoted as $ \dim_{\mathrm{loc}} \mu(x) $, is defined as:

$$
\dim_{\mathrm{loc}} \mu(x) = \lim_{\epsilon \to 0^+} \frac{\log \mu(B(x; \epsilon))}{\log \epsilon}
$$

where $ B(x; \epsilon) $ is a ball centered at $ x $ with radius $ \epsilon $. This dimension quantifies how the measure $ \mu $ behaves as one zooms in around the point $ x $.

## $ f(\alpha) $ and $ \tau(q) $: Multifractal Spectra

The multifractal spectrum and the associated functions $ f(\alpha) $ and $ \tau(q) $ provide a framework for analyzing the spread and intensity of dimensions across a measure.

### The $ \tau(q) $ Function

Defined implicitly by the relationship:

$$
\sum_{i=1}^m p_i^q c_i^{\tau(q)} = 1
$$

where $ p_i $ are probabilities and $ c_i $ are scaling factors associated with the iterated function system defining the fractal, $ \tau(q) $ explores how different moments of the measure scale.

### Multifractal Spectrum $ f(\alpha) $

The function $ f(\alpha) $, which is the Legendre transform of $ \tau(q) $, describes the dimension of the sets of points for which the local dimension is $ \alpha $. It is given by:

$$
f(\alpha) = \inf_{-\infty < q < \infty} \{\tau(q) + \alpha q\}
$$

## Key Properties

The following key properties hold:

1. $ \beta(q) $ is a strictly convex function of $ q $, meaning $ \frac{\mathrm{d}^2 \beta}{\mathrm{d} q^2} > 0 $ for all $ q $.
2. The range of $ \alpha $ for which $ f(\alpha) $ is defined is $ [\alpha_{\min}, \alpha_{\max}] $, where
    $$
    \alpha_{\min} = \min_{1 \leqslant i \leqslant m} \frac{\log p_i}{\log c_i} \quad \text{and} \quad \alpha_{\max} = \max_{1 \leqslant i \leqslant m} \frac{\log p_i}{\log c_i}.
    $$
3. For each $ \alpha \in [\alpha_{\min}, \alpha_{\max}] $, the graph of $ \beta(q) $ has a unique line of support with slope $ -\alpha $.
4. $ f(\alpha) $ is a concave function of $ \alpha $, meaning $ \frac{\mathrm{d}^2 f}{\mathrm{d} \alpha^2} \leq 0 $.
5. $ f(\alpha) $ achieves its maximum at $ \alpha(0) $, which corresponds to the Hausdorff dimension of the support of $ \mu $.

*proof*:

The proof is adpated from [Falconer's *Fractal Geometry: Mathematical Foundations and Applications*](https://onlinelibrary.wiley.com/doi/book/10.1002/0470013850), p.287-288.

The convexity of $ \beta(q) $ is established by differentiating the defining equation for $ \beta(q) $ twice with respect to $ q $:
$$
\sum_{i=1}^m p_i^q c_i^{\beta(q)} \left( \log p_i + \frac{\mathrm{d} \beta}{\mathrm{d} q} \log c_i \right) = 0,
$$
$$
\sum_{i=1}^m p_i^q c_i^{\beta(q)} \left( \frac{\mathrm{d}^2 \beta}{\mathrm{d} q^2} \log c_i + \left(\log p_i + \frac{\mathrm{d} \beta}{\mathrm{d} q} \log c_i \right)^2 \right) = 0.
$$
From the second derivative, since $ \frac{\mathrm{d}^2 \beta}{\mathrm{d} q^2} \geq 0 $, $ \beta(q) $ is convex. When the values $ \log p_i / \log c_i $ are distinct, strict convexity ($ \frac{\mathrm{d}^2 \beta}{\mathrm{d} q^2} > 0 $) is ensured.

The range $ [\alpha_{\min}, \alpha_{\max}] $ is derived from the limits $ q \rightarrow -\infty $ and $ q \rightarrow \infty $, which correspond to the minimum and maximum slopes of the graph of $ \beta(q) $, giving the values of $ \alpha_{\min} $ and $ \alpha_{\max} $.

The concavity of $ f(\alpha) $ follows from the fact that it is the Legendre transform of the convex function $ \beta(q) $. The second derivative of $ f(\alpha) $ with respect to $ \alpha $ can be written as:
$$
\frac{\mathrm{d}^2 f}{\mathrm{d} \alpha^2} = \frac{\mathrm{d}}{\mathrm{d} \alpha}\left(\frac{\mathrm{d} q}{\mathrm{d} \alpha}\right) = -\frac{\mathrm{d} q}{\mathrm{d} \alpha}.
$$
Since $ q $ decreases as $ \alpha $ increases, $ \frac{\mathrm{d} q}{\mathrm{d} \alpha} $ is negative, confirming the concavity.

Finally, the maximum of $ f(\alpha) $ occurs when $ q = 0 $, which corresponds to the Hausdorff dimension of the support of $ \mu $. The identity $ f(\alpha(1)) = \alpha(1) = \operatorname{dim}_{\mathrm{H}} \mu $ confirms that $ f(\alpha) $ touches the line $ f(\alpha) = \alpha $ at this point.

---

For more insights and detailed discussions on fractal geometry and multifractal analysis, consider exploring Kenneth Falconer's work in-depth, which offers a plethora of information and mathematical rigor to these fascinating topics.

