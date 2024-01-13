---
title: Forward Mapping
description: ''
date: '2021-07-26T21:58:19.425Z'
venue: Inverse Theory
---

Simulating data requires being able to solve

$$ \mathcal{F}[m] = d $$

where $m$ is an element of the model space $\mathcal{M}$, and $\mathcal{F}$ is the forward mapping. $\mathcal{F}$ encompasses the physics of the problem, the geometry of the survey and details about Tx and Rx. The operation generates a simulated data set which is an element of data space $\mathcal{D}$. The procedure is conceptualized in the diagram below (@fig:forward-mapping).

```{figure} images/VNMrkxzChhdveZyf6lmb-3zKlKqaAqrRWcQMMX7H6-v2.png
:name: fig:forward-mapping
:align: center
:width: 60%
Mapping between model space and data space
```

### Model space

Model space is a vector space with key components. Its elements can be functions or Euclidean vectors. Model space comes equipped with two important attributes:

Rules for inner products
: This allows the concept of angles between elements to be computed. This allows us to determine whether elements are parallel or perpendicular to each other.

Norms to measure length
: In our optimization solution it will be important to measure the “length” of the vectors so that we can distinguish between small and large elements.

See @parker_geophysical_1994 for a more in depth discussion.

For our seismic refraction problem (@seismic-refraction-experiment) our model space elements can be functions $v(z)$ or an $M$-length vector of velocity values: $\mathbf{v}=(v_1, \dots,v_M)$. These are shown in @fig:seismic-velocity-values.

```{figure} images/VNMrkxzChhdveZyf6lmb-1MMgRl6oRm8JDCBnlEsk-v3.png
:name: fig:seismic-velocity-values
:align: center
:width: 30%

Model space elements can be functions $v(z)$ or $M$-length vector of velocity values.
```

### Data Space

Observed data are generally a set of numbers and are consolidated into an elements of data space $\mathbf{d}=(d_1,\dots,d_N)~\in\R^N$. Each datum is calculated using

```{math}
\label{eq:datum}
d_j=\mathcal{F}_j[m]
```

The subscript $j$ allows us to keep track of specifics for that datum, such as survey parameters, which field, etc.

### Forward Mapping Operators

The forward mapping operator $\mathcal{F}$ is problem dependent and can be formulated as an integral or differential operator. Fundamentally however, it is useful to distinguish between two types: linear and nonlinear operators. Linear operators are the easiest to deal with in an inverse problem and understanding them forms a solid foundation for attacking nonlinear inverse problems.

#### Linear and Nonlinear Mappings

Let $f$ and $g$ be two elements of the model space and $\alpha$ and $\beta$ be two constants. A mapping $\mathcal{F}$ is linear if and only if

$$
\label{eq:linear-mapping}
\mathcal{F}[\alpha f+\beta g]=\alpha\mathcal{F}[f]+\beta\mathcal{F}[g]
$$

When this does not hold, the mapping is said to be nonlinear.

Many linear functionals can be written in integral form. A generic representation that we will use is

$$
\label{eq:kernel}
d_j=\int^b_ag_j(x)m(x)dx
$$

where $d_j$ is the $j^{th}$ datum, $g_j$ is the associated kernel function, and $m$ is the model of interest. @eq:kernel is a Fredholm equation of the second kind and it often appears in physical literature.

For example the equation for convolution,

$$ y = m \otimes w $$

takes the following form

```{math}
y(t_j)=\int^{\infty}_{-\infty}m(\tau)w(t_j-\tau)d\tau
```

In reflection seismology $m$ could be the reflectivity function, $w$ a wavelet, and $y$ an output seismogram. With reference to {eq}`eq:kernel`, each kernel is a time shifted version of $w$. Another form of our linear system ({eq}`eq:kernel`) is the [Biot-Savart](https://en.wikipedia.org/wiki/Biot%E2%80%93Savart_law) equation

```{math}
\vec{B}(\vec{r}_j)=\frac{\mu_0}{4\pi}\int\frac{\vec{J}(\vec{r}')\times\hat{r}}{\left|\vec{r}_j-\vec{r}'\right|^2}
```

Here the model is a vector, $m=\vec{J}$ where $\vec J$ is the current density, the kernel is the geometric function inside the integral and $\vec B$ is the magnetic flux density.

We first show that {eq}`eq:kernel` is a linear mapping. Suppose we have two models $m_1(x)$ and $m_2(x)$, a kernel $g_j$ and two datum $d_j^{(1)}$ and $d_j^{(2)}$.

```{math}
d_j^{(1)}=\int^b_a g_j(x)m_1(x)dx
```

```{math}
d_j^{(2)}=\int^b_a g_j(x)m_2(x)dx
```

The new datum, which is formed by a linear combination of the two models (@eq:datum and @eq:linear-mapping) is given by

```{math}
\begin{aligned}
d_j =\int^b_a g_j(x)[\alpha & m_1(x) +\beta m_2(x)]     \\
d_j =                \alpha & d_j^{(1)}+\beta d_j^{(2)}
\end{aligned}
```

and so the linearity condition in {eq}`eq:kernel` is satisfied. This is to be contrasted with an example like

```{math}
d_j=\int^b_ag_j(x)m^2(x)dx
```

This is clearly a nonlinear relationship; if $m(x)$ increases by a factor of two then the datum in increased by a factor of four.

Another example of nonlinearity is that encountered in DC resistivity. The controlling differential equation is

```{math}
\nabla\cdot\sigma\nabla V=-I\delta(\vec{r}-\vec{r}')
```

where is the electrical conductivity, is the potential which are the data, and the right hand side is a source. Doubling is will not result in a doubling of V.

The seismic refraction problem, is also a nonlinear mapping between travel time and velocity. Doubling the velocity of the earth will not increase the travel time by a factor of two. In fact, the majority of problem we deal with in geophysics are nonlinear.

:::{prf:example} Reflection seismology
:label: ex-reflection-seismology
Throughout this module we will work with both linear and nonlinear problems. A simple insightful example appears in reflection seismology. It is the relationship between the rms velocity $V_{rms}$ and interval velocity $v_{int}$ [@sheriff_exploration_1995].

```{math}
:label: eq:rms-velocity
V^2_{rms}(t_j)=\frac{1}{t_j}\int^{t_{max}}_0 v^2_{int}(u)H(t_j-u)du
```

Here $H(t)$ is the Heaviside step function. If we think about the “model” as being $v_{int}$ then the problem is nonlinear. However, if we let $m=v^2_{int}$ then we have a linear relationship between data ($V^2_{rms}$) and $m$. Thus, sometimes a problem can be made linear just by redefining the variables. We note also that the independent variable is time, rather than depth. Thus to use this equation, where the velocity is $v(z)$, there has been a depth-to-time conversion. We will explore the consequences of these choices later but for now we’ll use the full nonlinear problem to show how nonuniqueness and ill-conditioning arises in the inverse problem.
:::
