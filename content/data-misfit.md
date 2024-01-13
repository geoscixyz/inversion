---
title: Data Misfit
description: ''
date: '2021-07-27T18:43:48.580Z'
venue: Linear Tikhonov Inversion
---

The observations $d^{obs}$ encode our knowledge about the model obtained from the survey. Any candidate solution $m$ must produce simulated (or predicted) data $d$ that “fit” the observations. Central to this goal is the choice of a “criterion” for measuring misfit between observed and predicted data, and a “tolerance” for deciding what value constitutes an acceptable fit. This is a subject on which an enormous amount of literature has been written but a good reference, written for the inverse problem, is {cite:t}`parker_geophysical_1994`. When errors are Gaussian with zero mean and known standard deviation, then the $L_2$ -norm, is an appropriate choice. We define the misfit to be

```{math}
:label: 9424a329

\phi_d=\sum^N_{j=1}\left(\frac{d_j-d_j^{obs}}{\epsilon_j}\right)^2
```

where $d_j^{obs}$ is the observation, $\epsilon_j$ is its estimated standard deviation, and $d_j$ is the predicted datum. The quantity

```{math}
:label: c93bd419

\eta_j = \frac {d_j - d_j^{obs}} {\epsilon_j}
```

is a random variable with zero mean and unit standard deviation and $\phi_d$ , which is the sum of squares of these variables, is the well known $\chi^2$ statistical variable. It has an expected value ({eq}`198b31c2`) and variance ({eq}`000e5f6c`).

```{math}
:label: 198b31c2

E[\chi^2] = N
```

```{math}
:label: 000e5f6c

Var[\chi^2] = 2N
```

Thus if we are attempting to find a model $m$ that acceptably fits the data, then models with $\phi_d \simeq N$ are good candidates. For many problems we often denote a target misfit $\phi_d^*$ to be

```{math}
:label: 8e0a1ed0

\phi_d^*=N
```

but this must only be regarded as a reasonable estimate and some flexibility should be entertained.

In times past, it was felt that getting an acceptable fit to the data was a sufficient criterion for having a successful inversion. The observed data $\mathbf{d}_{obs}$ are inverted to produce a model $\mathbf{m}$, which is used to forward model the predicted data $\mathbf{d}$. The observed and predicted data are then compared using the data misfit measure. If $\phi_d<\phi_d^*$ the model $\mathbf{m}$ is accepted, but if not, the inversion parameters are adjusted and the process is repeated until an acceptable model is reached. The workflow procedure is delineated below.

```{figure} images/VNMrkxzChhdveZyf6lmb-6EB3FEfgScnvf73UHMPg-v2.png
:name: 6EB3FEfgScnvf73UHMPg
:align: center
:width: 70%
```

Finding a model that fits the data is a necessary component of an inversion algorithm, but as shown in the next section, it is not sufficient.
