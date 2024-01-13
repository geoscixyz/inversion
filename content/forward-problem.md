---
title: Forward Problem
description: ''
date: '2021-07-27T18:32:54.975Z'
name: forward-problem
venue: Linear Tikhonov Inversion
oxa: oxa:VNMrkxzChhdveZyf6lmb/xqM34l8moONMZ4iDWIQf
tags: []
keywords: []
---

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/DMWKEs4uFE0tm2fBjdUr.7","tags":[]}

For a linear system, the forward problem ({eq}`3ffde9a8`) can often be represented in the form of an integral equation (technically a Fredholm equation of the Second kind) as shown below.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/kcG1fkQEwzcMhorgrH32.12","tags":[]}

```{math}
:label: f40ae85f

d_j=\int^b_ag_j(x)m(x)dx
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/9lMYejPm485dUq7eA2Wc.1","tags":[]}

The model $m(x)$ is a function defined on the closed region $[a,b]$, and $g_j(x)$ is the kernel function which encapsulates the physics of the problem. The datum, $d_j$ is the inner product of the kernel and the model. It is sometimes helpful to think of the kernel as the “window” through which a model is viewed. In this section we will step through the essential details for carrying out the forward modelling. We first design a model, introduce a “mesh” to discretize it, discretize the kernels and form sensitivities, generate the data through a matrix vector multiplication and then add noise. These data will then be inverted.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/KNLhGSpYYfAko6951cZ1.5","tags":[]}

For our synthetic problem, we start by creating the function that we will later want to retrieve with the inversion. The model can be any function but here we combine a background, box car, and a Gaussian; the domain will be \[0,1\], shown in [Figure A](https://curvenote.com/oxa:VNMrkxzChhdveZyf6lmb/8WfrIYP5O9W6zakEQaa3.7).

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/8WfrIYP5O9W6zakEQaa3.7","tags":[]}

```{mdast} forward-problem.mdast.json#QZMVNZHNwK

```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/vKzG4OucE2WYlaSjDkHV.4","tags":[]}

**Figure A:** Default model from the corresponding inversion application. The model combines a background value with box car and Gaussian functions on the domain \[0,1\]. [LinearTikhonovInversion_Notebook.ipynb](oxa:VNMrkxzChhdveZyf6lmb/lb7CgEnVPzfs79VcKpB1 'LinearTikhonovInversion_Notebook.ipynb')

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/2L7K4fl4gBMQacD284lu.4","tags":[]}

### Mesh

In our next step we design a mesh on which our model is defined and on which all of the numerical computations are carried. We discretize our domain into $M$ cells of uniform thickness. If we think about the “x-direction” as being depth, then this discretization would be like having a layered earth.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/TWKjAN0EuRr4mN1jslTl.2","tags":[]}

```{figure} images/VNMrkxzChhdveZyf6lmb-TWKjAN0EuRr4mN1jslTl-v2.png
:name: TWKjAN0EuRr4mN1jslTl
:align: center
:width: 70%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/T6sWWsMvnDL5JuJbHPsm.4","tags":[]}

Our “model” is now an M-length vector $\mathbf m = (m_1, m_2, …, m_M)$. In fact, the function plotted in [Figure A](https://curvenote.com/oxa:VNMrkxzChhdveZyf6lmb/8WfrIYP5O9W6zakEQaa3.7) has already been discretized.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/qvGJ12IANr3L9Jk4UzMn.9","tags":[]}

### Kernels and Data

Our goal is to carry out an experiment that produces data that are sensitive to the model shown in [Figure A](https://curvenote.com/oxa:VNMrkxzChhdveZyf6lmb/8WfrIYP5O9W6zakEQaa3.7). For our linear system ({eq}`f40ae85f`) this means choosing the kernel functions. In reality, these kernel functions are controlled by the governing physical equations and the specifics of the sources and receivers for the experiment. For our investigation we select oscillatory functions which decay with depth. These are chosen because they are mathematically easy to manipulate and they also have a connection with many geophysical surveys, for example, in a frequency domain electromagnetic survey a sinusoidal wave propagates into the earth and continually decays as energy is dissipated. The kernel $g_j(x)$ corresponding to $d_j$ is given by

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/xQEIP2FNnxfk6ELkP28o.8","tags":[]}

```{math}
:label: 4f6a44b9

g_j(x)= e^{p_jx}\cos(2\pi q_jx)
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/Y47bmurJfiCyDyYRpma2.2","tags":[]}

Thus $p_j$ controls the rate of decay of the kernel and $q_j$ controls the frequency; the kernel will undergo $q_j$ complete cycles in the domain \[0,1\]. In our example, each of the ranges $[p_{min}, p_{max}]$ and $[q_{min}, q_{max}]$ is divided into M intervals but this is only for convenience. In principle these numbers can be arbitrarily specified. As an example the image below displays three kernels produced with $q = [1, 2, 3]$ and $p = [0, 1, 2]$. Note the successive decrease in amplitude at $x=1.0$.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/2btzRAPgnmItoV2GkvSV.10","tags":[]}

```{mdast} forward-problem.mdast.json#vGPcPxYoBq

```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/RZ8O7dw1PjELPxImDYX7.5","tags":[]}

**Figure B:** Example of three kernels ({eq}`4f6a44b9`) for the app where q=\[1,2,3\] and p=\[0,1,2\]. [LinearTikhonovInversion_Notebook.ipynb](oxa:VNMrkxzChhdveZyf6lmb/lb7CgEnVPzfs79VcKpB1 'LinearTikhonovInversion_Notebook.ipynb')

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/NbyT8tGzv13fNGkHWrYF.6","tags":[]}

To simulate the data we need to evaluate {eq}`f40ae85f`. The model has been discretized with the 1D mesh. The expression for the data becomes

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/Gm7gHsFXic5G1yoZSCkn.10","tags":[]}

```{math}
:label: be6adec9

\begin{aligned} d_j&=\int_0^{x_1}g_j(x)m_1dx +\int_{x_1}^{x_2}g_j(x)m_2dx+\dots \\ &=\sum^M_{i=1}\left(\int_{x_{k-1}}^{x_k}g_j\left(x\right)dx\right)m_i\\ &\\ d_j &= \mathbf g_j \mathbf m\end{aligned}
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/wjpBYcrqF20qxcYzGhmG.2","tags":[]}

where $\mathbf g_j$ is now referred to as a sensitivity kernel. When the discretization is uniform, the only difference between the kernel $g_j(x)$ and the sensitivity $\mathbf g_j$ is a scaling factor that is equal to the discretization width. However, for nonuniform meshes these quantities can look quite different, and confusing kernels and sensitivities, can lead to unintended consequences in an inversion. We shall make this distinction clear at the outset.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/QAUzP83WiVsFwT45K4v2.1","tags":[]}

To expand the above to deal with $N$ data. We define a sensitivity matrix $\mathbf{G}$. The $j^{th}$ row of $\mathbf{G}$ is formed by $\mathbf g_j$ so $\mathbf{d}$ looks like

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/UY5AXhKxS1h3WyGYrl2H.13","tags":[]}

```{math}
:label: d031bcf8

\begin{aligned} \mathbf{d} = \mathbf{G}\mathbf{m} = \begin{bmatrix} d_1\\ \vdots\\ d_{N} \end{bmatrix}\end{aligned}
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/Ry2YW3DdFtdKzELaESoU.1","tags":[]}

where the individual elements of $G$ are

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/2phjcwor9mrVgYufGT39.7","tags":[]}

```{math}
:label: 2664f2ef

G_{jk} = \int_{x_{k-1}}^{x_k} g_j(x) dx
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/UO99dTvoas4VsZCvxLKG.7","tags":[]}

$\mathbf{G}$ is an $N \times M$ matrix ($N$ data and $M$ model elements). Using the model in [Figure A](https://curvenote.com/oxa:VNMrkxzChhdveZyf6lmb/8WfrIYP5O9W6zakEQaa3.7) and our sensitivity matrix $\mathbf{G}$ we forward model the data. The model, rows of the sensitivity matrix, and corresponding data are shown in [Figure C](https://curvenote.com/oxa:VNMrkxzChhdveZyf6lmb/gqkXJ3NUlhOxm8lbUq2p.14). The data are considered “clean” or “true” because they do not contain noise.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/gqkXJ3NUlhOxm8lbUq2p.14","tags":[]}

```{mdast} forward-problem.mdast.json#tx5YkrqMmm

```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/RFRP8LmlqdS43tHPhh8p.5","tags":[]}

**Figure C:** Default display from the app of the model, rows (sensitivity kernels) of the matrix $\mathbf{G}$, and clean data. [LinearTikhonovInversion_Notebook.ipynb](oxa:VNMrkxzChhdveZyf6lmb/lb7CgEnVPzfs79VcKpB1 'LinearTikhonovInversion_Notebook.ipynb')

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/BkSnNlITIGCWKaHVZM7F.3","tags":[]}

### Adding Noise

Until now, we have only calculated the data $\mathbf{d}$, but observed data $\mathbf{d}^{obs}$ contain additive noise,

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/GtIrygcvqO2irqYxf3Ek.8","tags":[]}

```{math}
:label: adc69a91

\mathbf{d}^{obs}=\mathbf{d}+\mathbf{n}
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/wjec6ZKKu9MOlOxJmh9v.2","tags":[]}

Throughout our work, the noise for a datum $d_j$ is assumed to be a realization of a Gaussian random variable with zero mean and standard deviation

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/BGPdowi0KZw5sVvtq3iu.9","tags":[]}

```{math}
:label: 9e813186

\epsilon_j = \%|d_j| + \nu_j
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/qMpnnaEGMyfNg4YfvMrb.4","tags":[]}

this is a percentage of the datum plus a floor. The reason for this choice is as follows. In every experiment there is a base-level of noise due to instrument precision and other factors such as wind noise or ground vibrations. This can be represented as a Gaussian random variable with zero mean and standard deviation $\nu_j$ and a single value might be applicable for all of the data in the survey. This is often when the data do not have a large dynamic range such as might be found in gravity or magnetic data. In other cases the data can have a large dynamic range, such as in DC resistivity surveys or time domain EM data. To capture uncertainties in the data, a percentage value is more appropriate. If data range from $1.0$ to $1e-4$ then a standard deviation of $10 \%$ of the smallest datum is likely an under-estimate for the datum that has unit amplitude.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/wMAfxMpTBwoswZfrOVbY.3","tags":[]}

These are important concepts and we’ll revisit them in more detail later. For now it suffices that “noise” can be added to the data according to {eq}`adc69a91`. Here we choose $\epsilon_j = 0.03$. An example of the clean (true) data, a realization of the noise, and the noisy data are shown in [Figure D](https://curvenote.com/oxa:VNMrkxzChhdveZyf6lmb/f4ZOfRjwPn87rmRQmgT3.9). The error bars are superposed on the noisy data.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/f4ZOfRjwPn87rmRQmgT3.9","tags":[]}

```{mdast} forward-problem.mdast.json#NfDRb6qOjD

```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/qtFqSCengsdJ79xXoIN7.4","tags":[]}

**Figure D:** Display of the clean data from Figure 2.5 with the added noise to create the noisy data. [LinearTikhonovInversion_Notebook.ipynb](oxa:VNMrkxzChhdveZyf6lmb/lb7CgEnVPzfs79VcKpB1 'LinearTikhonovInversion_Notebook.ipynb')

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/jLmU23G920AaVhBYnOTC.10","tags":[]}

The construction of the forward problem for the 1D synthetic example provided many of the elements needed for the inverse problem. We have observed data, an estimate of the uncertainty within the data, the ability to forward model and we have discretized our problem. Our goal is to find the model that gave rise to the data. Within the context of our flow chart in [2.2. Defining the Inverse Problem](oxa:VNMrkxzChhdveZyf6lmb/iPh2GcyPHcbKFJrzGLc4 '2.2. Defining the Inverse Problem')-{numref}`Figure %s <cFtpNM4K3qAT83AO13wl>` the next two items to address are the misfit criterion and model norm. We first address the issue of data misfit.
