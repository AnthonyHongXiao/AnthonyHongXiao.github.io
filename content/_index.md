# Xiao (Anthony) Hong

*Poetry is the art of calling the same thing by different names.* -- Anonymous.

*Yes, and mathematics is the art of calling different things by the same name.* -- Henri Poincaré.

## About Me
{{< imageRight src="/images/photos/Portrait.jpg" alt="Photo credit: Pascal." caption="Photo credit: Pascal." width="20%" >}}
Hello! I am Anthony, a senior undergraduate at **Washington University in St. Louis (WUSTL)**, majoring in joint program Econ+CS, with a double major in Mathematics. My early study in architecture and art led me to an interest in **geometry**, which I now explore with a focus on **data** in a broad sense. I’m interested in various geometric structures, including symplectic and noncommutative geometry, as well as probabilistic and coarse geometry. I also enjoy visual models in low-dimensional topology and discrete differential geometry.

I recently participated in the geometry processing program at [MIT SGI](https://sgi.mit.edu/sgi-2024), where I took part in a tutorial week and group projects guided by both industry professionals and academics. I’m currently working on my undergraduate thesis in symplectic geometry and toric manifolds with Prof. Tang Xiang.

Outside of math 🔢, I enjoy reading social theories 📖, listening to classical music 🎻, traveling ⛰️, and spending time with my cat 🐈.
{{< imageRight src="/images/photos/NY.jpg" alt="Photo: New York. Dec 2022." caption="Photo: New York. Dec 2022." width="20%" >}}
### Contact
- **Email: hong[dot]x@wustl[dot]edu**
- **LinkedIn: [https://www.linkedin.com/in/xiao-hong-anthony/](https://www.linkedin.com/in/xiao-hong-anthony/)**
- **Twitter: [https://x.com/AnthonyHongXiao](https://x.com/AnthonyHongXiao)**

<br>
<br>

### Talks/Teaching
- Speaker at Midstates Consortium for Math and Science 23 ([session I.B.3](https://www.mathsciconsortium.org/uncategorized/2023-undergraduate-research-symposium-in-physical-sciences-mathematics-and-computer-science-at-university-of-chicago/)) at University of Chicago. ([beamer presentation](pdfs/presentation_on_Ollivier_Ricci_Curvature.pdf)). The work was also presented at [Prof. Martinkainen's session](https://sites.wustl.edu/henri/online-early-career-morning-sessions-april-13-14-2024/) and WashU SP24 Undergraduate Research Symposium ([video](https://youtu.be/g_lOmxUgVNw)).
- Teaching assistant for Math5046 Differential Topology
- Grader for Math4111 Introduction to Analysis, Math4171 Topology I, and Math5051 Measure Theory and Functional Analysis I

### Seminars
- Math586 Topic in Statistics: Network Statistics.
{{< imageRight src="/images/portfolio/Aryclic_Painting_Urbanity_and_Space.jpg" alt="Aryclic Painting: Urbanity and Space. Aug 2020." caption="Aryclic Painting: Urbanity and Space. Aug 2020." width="20%" >}}
- Math547 Topic in Geometry: Combinatorics of Polytopes.
- Math497 Topics in Mathematics: Group Theory From a Historical Perspective
- [UNC Undergraduate Analysis and PDE Seminar](https://tarheels.live/waves/analysis-and-pde-seminar/) FL22-SP24.
- WashU Reading Group SP23: Algebraic Geometry.
- WashU Reading Group FL23: Representation Theory.
- StanCon 2023 Workshop:
  [Convention on Stan Programming and Bayesian Modeling](https://mc-stan.org/events/stancon2023/#tutorials)
- WUSTL Metamorphic Architecture Workshop 2019, Dean Heather Woofter's tutee.

<br>

<hr style="border: none; height: 1px; background-color: #333; margin: 40px 0;">

## Publications

{{< imageRight src="/images/Great_Gatsby_Curve.png" alt="The Great Gatsby Curve." caption="The Great Gatsby Curve." width="35%" >}}
### 1. Study of Intergenerational Mobility and Urbanization Based on OLS Method and Ordered Probit Model

**IEEE-CS/MSIEID2020, Dec 18 2020.**

[DOI: 10.1109/MSIEID52046.2020.00092](https://ieeexplore.ieee.org/abstract/document/9382602)

The study, using the CHARLS dataset and techniques like OLS and ordered probit model, reveals a growing educational disparity across generations in China, highlighting an increasing trend in educational inequality despite overall improvements, especially between urban and rural regions.

<hr style="border: none; height: 1px; background-color: #333; margin: 40px 0;">

## Projects

### 1. Undergraduate Thesis on Symplectic Geometry
**Feb 2024 - Present**

The project aims to present the Atiyah-Guillemin-Sternberg convexity theorem at the end. Current readings include Ana Cannas da Silva’s *Lectures on Symplectic Geometry* and *Symplectic Toric Manifolds*.

<!---------------------------- seperation line ---------------------------->

### 2.  Curvature of Cayley Graph of Abelian and Nilpotent Groups
{{< imageRight src="/images/torus.png" alt="Evolving Point Measures." caption="Evolving Point Measures." width="35%" >}}
**Jul 2023 - Jan 2024**

This is a summer research with Prof. Renato Feres beginning in July 2023. The study aims to use efficient algorithms to compute [Ollivier-Ricci curvature](https://www.sciencedirect.com/science/article/pii/S002212360800493X), or [Lin-Lu-Yau curvature](https://people.math.sc.edu/lu/papers/graphcurv.pdf), of Cayley graphs of certain groups and find out some patterns. Currently, efficient optimization algorithm is found for Cayley graph and theoretical justifications for interesting patterns about curvature are concluding. 

<!---
[beamer presentation](pdfs/presentation_on_Ollivier_Ricci_Curvature.pdf))
-->

There is also a second project I am working with Prof. Feres. The project studies the Wasserstein distance of point measures that evolved along their geodesics after initiations.

$$
W_p(\mu_1,\mu_2)=\left(\inf_{\mu\in \Gamma(\mu_1,\mu_2)}{\int_{X^2}d(x,y)^pd\mu(x,y)}\right)^{\frac{1}{p}}=\left(\inf_{\mu\in \Gamma(\mu_1,\mu_2)}{\mathbf{d}(\mu,\nu)^p_{L^p(\mu;X)}}\right)^{\frac{1}{p}}
$$
with
$$
\forall A\in \mathcal{B}(\mathcal{M}):\text{ }\mu_1(t)(A)=\frac{1}{n}\sum_{i=1}^{n}{\delta_{\gamma_{v_i}(t)}}(A)=\frac{\text{ number of }\gamma_{v_i}(t)\text{ in }A}{n}
$$

<!---------------------------- seperation line ---------------------------->

{{< imageRight src="/images/image_classification.png" alt="MNIST digit examples." caption="MNIST digit examples." width="35%" >}}
### 3. Image Classification Using Wasserstein Distance from Monge-Kantorovich Solvers

**Final project in Prof. Yixin Chen's CSE543 Nonlinear Optimization, with Jingyuan Zhu, Mingzhen Li, Ruiqi Wang, Fall 2023.**

A review of the [paper](https://arxiv.org/abs/1612.00181) on gradient descent and finite element method for solving the Monge-Kantorovich problem with quadratic cost
$$
\min_{\text{measurable }T\text{ s.t. } T_{\sharp} \mu=\nu}\left(\int_X \frac{1}{2}\left|x-T^*(x)\right|^2 f(x) d x\right)^{1 / 2}
$$
with application in image classification.

[Paper Link](/pdfs/543_Image_Classification_Using_W_dist.pdf); image from the [database](https://yann.lecun.com/exdb/mnist/).

<br>

### 4. MIT Summer Geometry Initiative (SGI)

**Jul 2024 - Aug 2024**

The [MIT SGI](https://sgi.mit.edu/sgi-2024) is a program that starts with a week-long tutorial in geometry processing, followed by group projects mentored by experts in the field. Below are the projects I contributed to:

#### Deforming Mesh
In this project, I explored different metrics to compare the "wiggliness" of shapes, focusing on Gromov-Hausdorff, Hausdorff, and Chamfer distances. The project involved applying these metrics to analyze and quantify shape dissimilarities. My work contributed to developing a deeper understanding of how these distances can be used in practical geometry processing applications.

[Project Link](https://summergeometry.org/sgi2024/how-to-match-the-wiggliness-of-two-shapes/)

{{< imageRight src="/images/SGI/SDF.png" width="25%" >}}

#### Signed Distance Functions (SDFs)
This project involved designing and reconstructing signed distance functions (SDFs) using the marching squares algorithm. We studied how SDFs can be characterized on planes, proving a theorem that connects SDFs to the Eikonal equation and the closest point condition. The project aimed at improving the precision of surface reconstructions, which has broad implications for fields like computer graphics and computational geometry.

[Part 1](https://summergeometry.org/sgi2024/a-study-on-surface-reconstruction-from-signed-distance-data-part-1/) | [Part 2](https://summergeometry.org/sgi2024/a-study-on-surface-reconstruction-from-signed-distance-data-part-2-error-methods/)

{{< imageRight src="/images/SGI/Nefertiti.png" width="25%" >}}

#### Fitting Inconsistent Input with Noise Regularization
In this project, I worked on reconstructing surfaces from point clouds that include noise and outliers. We utilized shallow neural networks coupled with adversarial modules to regularize the noise and improve the surface fitting process. The project demonstrated how combining machine learning with geometric techniques can lead to more robust and accurate surface reconstructions, even with imperfect data.

[Project Link](https://summergeometry.org/sgi2024/fitting-surfaces-with-noise-regularization/)

#### Winding Numbers Vectorization
This project focused on computing winding numbers, which are essential in understanding the topological properties of shapes. I worked on applying these calculations to a torus and its universal cover, using intrinsic triangulations to optimize the mesh. The project aimed at solving issues related to mesh connectivity and color region disconnections by embedding these properties in a feature space. The work has practical implications for texture mapping and mesh processing in computer graphics.

*Project Link: coming soon.*

{{< imageRight src="/images/SGI/flat_torus.png" width="25%" >}}
#### Bridging Curvatures: From Riemann to Gauss
This project aimed to introduce the concept of curvature to a broader audience, particularly those familiar with surface curvatures. I reviewed the isometric embedding of a flat torus and explored Gromov's convex integration technique. The project served as an educational resource, connecting classical differential geometry concepts with more advanced topics, making them accessible to members of the SGI community.

[Project Link](https://summergeometry.org/sgi2024/bridging-curvatures-from-riemann-to-gauss/); image from [paper](https://www.pnas.org/doi/pdf/10.1073/pnas.1118478109).

<!---------------------------- seperation line ---------------------------->

### 5. Hex & Brouwer Paper Report

{{< imageRight src="/images/Hex_board.png" alt="Hex board game." caption="Hex board game." width="25%" >}}

**Midterm project in Prof. Chi's Math 4181 Algebraic Topology, Spring 2022.**

[Report Link](/pdfs/4181_Hex_and_Brouwer.pdf)

A report that correctsm a error on neighborhood size and reestablishes the proof of equivalence between the Hex theorem and the Bouwer Fixed-Point in David Gale’s paper “The Game of Hex and The Brouwer Fixed-Point Theorem.”

Image from [Wolfram](https://mathworld.wolfram.com/GameofHex.html).

<br>

<!---------------------------- seperation line ---------------------------->

### 6. Split Spoils: Solution to Stolen Necklace Problem Via Borsuk-Ulam Theorem

**Final project in Prof.Chi's Math 4181 Algebraic Topology, Spring 2022.**

[Report Link](/pdfs/4181_Necklace_Problem.pdf)

Aiming for high-schooler reading, the paper demonstrates how to solve a mathematical problem. Specifically, guided by [Using the Borsuk-Ulam Theorem](https://kam.mff.cuni.cz/~matousek/akt.html) and 3b1b YouTube [video on necklace problem](https://www.youtube.com/watch?v=yuVqxCSsE7c), we presented the Borsuk-Ulam Theorem intuitively and used it to solve the 2-dimensional Necklace division problem.

<!---------------------------- seperation line ---------------------------->
{{< imageRight src="/images/covering.jpg" alt="A covering." caption="A covering." width="25%" >}}

### 7. A Note about Algebraic and Geometric Characteristics of Archetypal Riemann Surfaces

**Final project in Dr. Rodsphon's Math 497 Topic in Group Theory, Spring 2023.**

A.B. Sossinsky in [Geometries](https://bookstore.ams.org/stml-64/) classified subgroups of $\text{SO}(3)$ and $\text{Isom}(\mathbb{R}^2)$ for Platonic bodies and tillings. Aimed for understanding such visual applications, we wrote a summary of curvatures, isometry groups, and automorphism groups of 3 Riemann Surfaces $\hat{\mathbb{C}}, \mathbb{C}, \triangle$ in uniformization theorem.
[Paper Link](/pdfs/497_A_Note_on_Algebraic_and_Geometric_Characteristics_of_Archetypal_Riemann_Surfaces.pdf)

[Presentation: An Exposition of Modernism in Geometry and Physics](https://docs.google.com/presentation/d/1o8KRS4pxbBGSSJmRdzsk2t1VcwMVyEX8/edit?usp=sharing&ouid=100293676418265540630&rtpof=true&sd=true)

<br>
<br>

<div style="border-top: 4px solid #333; margin: 40px 0;"></div>

## Gallery

{{< figure src="/images/portfolio/Critique.jpg" caption="Final critique, Metamorphic Workshop 2019." height="70%" width="70%" class="imagecenter" >}}

{{< figure src="/images/portfolio/Model_Market-Pavilion_Continuum(detail)_Metamorphic_Workshop.jpg" caption="Market-Pavilion Continuum (detail), Metamorphic Workshop 2019." height="80%" width="80%" class="imagecenter" >}}

{{< figure src="/images/portfolio/Model_The_Memory_Museum.jpg" caption="Model: The Memory Museum. Made in 12/2019." height="80%" width="80%" class="imagecenter" >}}

{{< figure src="/images/photos/SZ.jpg" caption="Photo: Shenzhen Airport. 8/2022." height="60%" width="80%" class="imagecenter" >}}

{{< figure src="/images/portfolio/Oil_Painting_Oblivion.jpg" caption="Oil Painting: Oblivion. 7/2020." height="60%" width="60%" class="imagecenter" >}}




