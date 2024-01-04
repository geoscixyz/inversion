---
title: Forward Mapping
description: ''
date: '2021-07-26T21:58:19.425Z'
name: forward-mapping
oxa: oxa:VNMrkxzChhdveZyf6lmb/0VkRIdgDMntmQzhLzHiP
tags: []
---

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/X7PezrLoTdQEBWzoWsBb.2"}

Simulating data requires being able to solve

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/Iv43QHUhUicMsAvpWgAb.8"}

```{math}
:label: 77e80a1d

\mathcal{F}[m] = d
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/AXgh2yqCwkiDu5HjZat0.3"}

where $m$ is an element of the model space $\mathcal{M}$, and $\mathcal{F}$ is the forward mapping. $\mathcal{F}$ encompasses the physics of the problem, the geometry of the survey and details about Tx and Rx. The operation generates a simulated data set which is an element of data space $\mathcal{D}$. The procedure is conceptualized in the diagram below ({numref}`Figure %s <3zKlKqaAqrRWcQMMX7H6>`).

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/3zKlKqaAqrRWcQMMX7H6.2"}

```{figure} images/VNMrkxzChhdveZyf6lmb-3zKlKqaAqrRWcQMMX7H6-v2.png
:name: 3zKlKqaAqrRWcQMMX7H6
:align: center
:width: 60%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/CpLB2bNalogSqtyD138N.4"}

### 1\.4.1. Model space

Model space is a vector space with key components. Its elements can be functions or Euclidean vectors. Model space comes equipped with two important attributes:

- **Rules for inner products** - This allows the concept of angles between elements to be computed. This allows us to determine whether elements are parallel or perpendicular to each other.
- **Norms to measure length** - In our optimization solution it will be important to measure the “length” of the vectors so that we can distinguish between small and large elements.

See {cite:p}`parker_geophysical_1994` for a more in depth discussion.

For our seismic refraction problem our model space elements can be functions $v(z)$ or $M$\-length vector of velocity values: $\mathbf{v}=(v_1, \dots,v_M)$. These are shown in {numref}`Figure %s <1MMgRl6oRm8JDCBnlEsk>`.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/1MMgRl6oRm8JDCBnlEsk.3"}

```{figure} images/VNMrkxzChhdveZyf6lmb-1MMgRl6oRm8JDCBnlEsk-v3.png
:name: 1MMgRl6oRm8JDCBnlEsk
:align: center
:width: 30%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/XY13c0lSssiWXajWCw0Q.4"}

### 1\.4.2. Data Space

Observed data are generally a set of numbers and are consolidated into an elements of data space $\mathbf{d}=(d_1,\dots,d_N)~\in\R^N$. Each datum is calculated using

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/58SCTuc4u4OkpuZPuoUB.5"}

```{math}
:label: 3ffde9a8

d_j=\mathcal{F}_j[m]
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/4kSVLuYWs1eP6YAygvA4.1"}

The subscript $j$ allows us to keep track of specifics for that datum, such as survey parameters, which field, etc.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/GxWwK5fXdsCNhDBmI1dK.4"}

### 1\.4.3. Forward Mapping Operators

The forward mapping operator $\mathcal{F}$ is problem dependent and can be formulated as an integral or differential operator. Fundamentally however, it is useful to distinguish between two types: linear and nonlinear operators. Linear operators are the easiest to deal with in an inverse problem and understanding them forms a solid foundation for attacking nonlinear inverse problems.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/teCrqE51E9OHmLi76POI.4"}

#### 1\.4.3.1 Linear and Nonlinear Mappings

Let $f$ and $g$ be two elements of the model space and $\alpha$ and $\beta$ be two constants. A mapping $\mathcal{F}$ is linear if and only if

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/2612PkADvNiBlkg5RysF.7"}

```{math}
:label: ec8a3fad

\mathcal{F}[\alpha f+\beta g]=\alpha\mathcal{F}[f]+\beta\mathcal{F}[g]
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/Zzv6XxAJIjKIntg9DL4b.3"}

When this does not hold, the mapping is said to be nonlinear.

Many linear functionals can be written in integral form. A generic representation that we will use is

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/kcG1fkQEwzcMhorgrH32.12"}

```{math}
:label: f40ae85f

d_j=\int^b_ag_j(x)m(x)dx
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/Q62zNtrxrD4fYWSe68B7.4"}

where $d_j$ is the $j^{th}$ datum, $g_j$ is the associated kernel function, and $m$ is the model of interest. {eq}`f40ae85f` is a Fredholm equation of the second kind and it often appears in physical literature.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/mIpjF5sWRaYY1EXnpFQU.3"}

For example the equation for convolution,

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/bzvw8czOV3HO6mqz7Oet.6"}

```{math}
:label: c61a0203

y = m \otimes w
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/y2pvzSGE7yzwJOI2AEQ8.1"}

takes the following form

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/lO4LLkjjq7kbDfS6TCXp.7"}

```{math}
:label: a7524253

y(t_j)=\int^{\infty}_{-\infty}m(\tau)w(t_j-\tau)d\tau
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/C6kzbMAo8xZWOJAbqCYK.4"}

In reflection seismology $m$ could be the reflectivity function, $w$ a wavelet, and $y$ an output seismogram. With reference to {eq}`f40ae85f`, each kernel is a time shifted version of $w$. Another form of our linear system ({eq}`f40ae85f`) is the Biot-Savart equation

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/5ifQPlmRIekmKf3BDcM0.9"}

```{math}
:label: 32fe3486

\vec{B}(\vec{r}_j)=\frac{\mu_0}{4\pi}\int\frac{\vec{J}(\vec{r}\prime)\times\hat{r}}{\left|\vec{r}_j-\vec{r}\prime\right|^2}
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/rWYokpEhRPJY21r7T4p1.2"}

Here the model is a vector, $m=\vec{J}$ where $\vec J$ is the current density, the kernel is the geometric function inside the integral and $\vec B$ is the magnetic flux density.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/KV5MLwoPXVU4KlTV77YQ.4"}

We first show that {eq}`f40ae85f` is a linear mapping. Suppose we have two models $m_1(x)$ and $m_2(x)$, a kernel $g_j$ and two datum $d_j^{(1)}$ and $d_j^{(2)}$.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/XsjJaecfwHID0KAINBLu.9"}

```{math}
:label: 9e1acfa8

d_j^{(1)}=\int^b_a g_j(x)m_1(x)dx
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/T266ULKhnxY9ij5tql83.7"}

```{math}
:label: 89373b07

d_j^{(2)}=\int^b_a g_j(x)m_2(x)dx
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/MO7eBvVyg8cmAi4XEC7j.2"}

The new datum, which is formed by a linear combination of the two models ({eq}`3ffde9a8` and {eq}`ec8a3fad`) is given by

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/LyvrSwMQ8phodV2Zk4sm.8"}

```{math}
:label: fc8ce57f

\begin{aligned}d_j=\int^b_a g_j(x)[\alpha & m_1(x) +\beta m_2(x)]\\ d_j=\alpha &d_j^{(1)}+\beta d_j^{(2)}\end{aligned}
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/ibyUtdVKAfJUq1cKdNFU.4"}

and so the linearity condition in {eq}`f40ae85f` is satisfied. This is to be contrasted with an example like

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/DdipWkTJ9eCP4tao8oW9.8"}

```{math}
:label: 7f61dce7

d_j=\int^b_ag_j(x)m^2(x)dx
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/boXBd6npQ21lGJYI45vu.1"}

This is clearly a nonlinear relationship; if $m(x)$ increases by a factor of two then the datum in increased by a factor of four.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/hQiUZV5SNJOilgvAbY2T.1"}

Another example of nonlinearity is that encountered in DC resistivity. The controlling differential equation is

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/FCouZX8qA3eeWl1zi0Zr.7"}

```{math}
:label: 0c8e0714

\nabla\cdot\sigma\nabla V=-I\delta(\vec{r}-\vec{r}\prime)
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/qJDGd2c08DaR1a5dy4hl.3"}

where is the electrical conductivity, is the potential which are the data, and the right hand side is a source. Doubling is will not result in a doubling of V.

The seismic refraction problem, is also a nonlinear mapping between travel time and velocity. Doubling the velocity of the earth will not increase the travel time by a factor of two. In fact, the majority of problem we deal with in geophysics are nonlinear.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/jAoQMSJcF1GLLucMoosR.5"}

Throughout this module we will work with both linear and nonlinear problems. A simple insightful example appears in reflection seismology. It is the relationship between the rms velocity $V_{rms}$ and interval velocity $v_{int}$ {cite:p}`sheriff_exploration_1995`.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/7vm3mQYoOAkNVRhsglMU.13"}

```{math}
:label: a19b615c

V^2_{rms}(t_j)=\frac{1}{t_j}\int^{t_{max}}_0 v^2_{int}(u)H(t_j-u)du
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/Rhk3F1nxOLRCb3GwrTfl.4"}

Here $H(t)$ is the Heaviside step function. If we think about the “model” as being $v_{int}$ then the problem is nonlinear. However, if we let $m=v^2_{int}$ then we have a linear relationship between data ($V^2_{rms}$) and $m$. Thus, sometimes a problem can be made linear just by redefining the variables. We note also that the independent variable is time, rather than depth. Thus to use this equation, where the velocity is $v(z)$ ,there has been a depth-to-time conversion. We will explore the consequences of these choices later but for now we’ll use the full nonlinear problem to show how nonuniqueness and ill-conditioning arises in the inverse problem.

