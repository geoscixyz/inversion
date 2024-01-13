---
title: 'Inverse Problem Fundamental Challenges '
description: ''
date: '2021-07-27T00:16:57.040Z'
name: inverse-problem-fundamental-challenges
venue: Inverse Theory
oxa: oxa:VNMrkxzChhdveZyf6lmb/xCROwv5D13g0WO6TJCti
tags: []
keywords: []
---

Inversion $\mathcal{F}^{-1}$ is the process of mapping from the data space $\mathcal{D}$ to the model space $\mathcal{M}$ $(\mathcal{F}^{-1}:~\mathcal{D}\rightarrow\mathcal{M})$, shown in @fig:inverse-mapping.

```{figure} images/VNMrkxzChhdveZyf6lmb-5BftNeWYsxYv8h6lhtx5-v2.png
:name: fig:inverse-mapping
:align: center
:width: 50%

Inversion $\mathcal{F}^{-1}$ is the process of mapping from the data space $\mathcal{D}$ to the model space $\mathcal{M}(\mathcal{F}^{-1}:~\mathcal{D}\rightarrow\mathcal{M})$.
```

Two fundamental challenges when inverting data is the ill-conditioning of the problem and nonuniqueness of the solution. We can obtain intuition for this by considering the relationship in seismology between rms velocity $V_{rms}$ and interval velocity $v_{int}$ from [](#ex-reflection-seismology) and @eq:rms-velocity. For this problem we define the following:

Forward Problem
: $\mathcal{F}$: Given the model $v_{int}$ compute the data $V_{rms}$

Inverse Problem
: $\mathcal{F}^{-1}$: Given the data $V_{rms}$ compute the model $v_{int}$

Thus, given the data, $V_{rms}$, what is the velocity model, $v_{int}$ that produced the data? There are numerous questions that can be asked:

- Does a solution exist? - Is there any model that can produce the data?
- How do we construct a solution?
- Is the solution unique? - If you have found one candidate, are there others?
- How do we handle nonuniqueness? - If there are multiple solutions, which model best reflects the subsurface physical property distribution?

The answers to these questions depend on the available data and it’s insightful to consider the following cases

- infinite amount of accurate data (perfection ✨ )
- finite amount of accurate data (no noise 💯 )
- finite amount of inaccurate data (reality 🌎 )
- changes to the model due to a small perturbation of the data

In the forward problem we are given $v_{int}$ and we calculate $V_{rms}$ “exactly” by carrying out the integration analytically @eq:vrms-integration or numerically using extreme precision. The result is a function $V_{rms}(t)$ on the interval $[0, t_{max}]$.

```{math}
:label: eq:vrms-integration
V^2_{rms}(t)=\frac{1}{t}\int^{t_{max}}_0 v_{int}^2(u)H(t-u)du
```

We notice that each datum is an integral of $v_{int}$ and hence structure observed in $v_{int}$ will appear as smoothed structure in the data $V_{rms}$. That is, the forward operator is a “smoother”. As an example consider an interval $v_{int} = v_0 + a \sin(2 \pi f t)$. The interval velocity model and data are shown below for the special case of xxxx

```{figure} images/VNMrkxzChhdveZyf6lmb-Ca2uDOJsWjEA5cwlDOni-v1.png
:name: ae6b407d
:align: center
:width: 70%
```

As a general rule all forward modelling operators are smoothers and the issue is conceptualized in the figure below

```{figure} images/VNMrkxzChhdveZyf6lmb-SwmBorpIy8mSuxNTdkyF-v1.png
:name: ad4a70ad
:align: center
:width: 70%
```

If the forward mapping $\mathcal{F}$ smooths, then the inverse operator $\mathcal{F}^{-1}$ must “roughen”. This is easily seen in our example where the analytic inverse $\mathcal{F}^{-1}$ exists.

```{math}
:label: 815dcec5

v_{int}=V_{rms}(t)\left(1+\frac{2tV'_{rms}(t)}{V_{rms}(t)}\right)^{\frac{1}{2}}
```

We notice that there is a time derivate $V_{rms}' (t)$ of the data. Differentiation is a roughening operator. Moreover this derivative is multiplied by $t$ which means that small changes in the data at later times will produce large changes in $v_{int}$. To explore the main concepts, we define an example for the rms velocity data,

```{math}
:label: c2de4591

V_{rms}(t)=v_0+a\sin(2\pi ft)
```

where $v_0$ is a constant, $a$ the amplitude of the sinusoid, and $f$ the frequency in Hz. The corresponding derivative of the data, required for the analytic inverse calculation ({eq}`815dcec5`) is

```{math}
:label: 2f6367b7

V'_{rms}(t)=2\pi af\cos(2\pi ft)
```

We can solve equation (2) numerically by evaluating the integrand on a very fine mesh and using a quadrature integration and a finite difference for the derivative. The result is presented in Fig xx

```{figure} images/VNMrkxzChhdveZyf6lmb-sr29Sc2xALrSfJTtHDKY-v1.png
:name: ab267060
:align: center
:width: 70%
```

The true and recovered interval velocity are identical.

## Nonuniqueness

The above example illustrated the idealistic case where we have an infinite number of accurate data. We were able to recover the initial velocity model. We now explore the case where only a finite number of data exist. We do this by sampling $V_{rms}$ at $N$ times $t_j, (j=1,N)$, interpolate the data to obtain the function$, V_{rms}(t)$, as illustrated in the figure below.

```{figure} images/VNMrkxzChhdveZyf6lmb-LQkp6djx1ixLcOdo8Apb-v1.png
:name: a5bf0205
:align: center
:width: 70%
```

We then use the analytic formula (equation 2) to recover the interval velocity. The recovered model will depend upon the sampling and the interpolation scheme used.

In the figure below we show the models recovered by using a linear and a cubic spline interpolation. At the scale plotted, the interpolated data are not greatly different but the cubic spline interpolated values are smoother and this is important when estimating a derivative of the data. The recovered velocities all show the five cycles in the mode but differ they from each other and also from the true model. Sine there are an infinite number of ways in which the finite number of data can be interpolated, the inverse problem is inherently non-unique.

```{figure} images/VNMrkxzChhdveZyf6lmb-HBm9xIwehE0eqMVibHIt-v1.png
:name: a6272967
:align: center
:width: 70%
```

```{figure} images/VNMrkxzChhdveZyf6lmb-WhcNmXNwXor24V3A5rin-v1.png
:name: ac8221da
:align: center
:width: 70%
```

Whereas in @fig:inverse-mapping the application of $\mathcal{F}^{-1}$ maps to a single point in model space, with a finite number of data, we have many possible models; these are indicated by the dark green subspace of the model space in {numref}`Figure %s <tfJv6scxau4VO7AZtTO3>`.

```{figure} images/VNMrkxzChhdveZyf6lmb-tfJv6scxau4VO7AZtTO3-v2.png
:name: tfJv6scxau4VO7AZtTO3
:align: center
:width: 40%
```

The nonuniqueness is exacerbated when we have a finite number of data contaminated with noise. As shown in {numref}`Figure %s <R7LoaGMcurI6TlSKSRyH>` below there are now more ways to interpolate the data and each interpolation will produce a different $v_{int}(t)$.

```{figure} images/VNMrkxzChhdveZyf6lmb-OaY83EoVsmYutnckX6Db-v1.png
:name: a1e83824
:align: center
:width: 70%
```

In the example below we add Gaussian noise with zero mean and standard deviation = 0.03 sec to the true data values. The point observations, along with error bars, are plotted in Fig xx. These data are linearly interpolated to generate $V_{rms}(t)$ for inversion. Even with small errors, the recovered model is exhibits considerable incorrect structure.

```{figure} images/VNMrkxzChhdveZyf6lmb-Etolf3e1mEkhU6ZFNOTK-v1.png
:name: a573121e
:align: center
:width: 70%
```

With respect to our mapping diagram, the inaccurate data to be inverted now populate the dark blue region of the data space and the inverse process maps to a larger, dark green, region of the model space ({numref}`Figure %s <CCyR4OOMNpenuGi2LINI>`).

```{figure} images/VNMrkxzChhdveZyf6lmb-CCyR4OOMNpenuGi2LINI-v2.png
:name: CCyR4OOMNpenuGi2LINI
:align: center
:width: 50%
```

### Ill-conditioning

A second important aspect of the inverse problem is that of ill-conditioning. In most problems in geophysics, the forward operator is a smoothing operator. We saw that in the examples above but other insight arises from the fact that a geophysical datum often depends upon the physical properties in a volume of the subsurface. For instance, a gravity datum depends on the volumetric density distribution, or a DC potential depends upon all of the charges built up in the subsurface when a current is injected. So the data is effectively “averaging” the underlying physical property that we are attempting to find. The inverse problem must therefore “undo” this averaging. As in the previous examples, this often involves some type of differentiation of data to “roughen” the model. The practical question is whether that roughening results in model structures that are representative of the earth, or whether they present unrealistic structure. To quantify this we consider the following.

Let

```{math}
:label: 1bc2c17d

d^{obs}=d^{true}+\delta d
```

where $\delta d$ is a perturbation on the data. Let

```{math}
:label: d73ceb50

\mathcal{F}^{-1}[d^{true}]=m_c
```

where $m_c$ is the constructed model. We can then write

```{math}
:label: 5c78d503

\mathcal{F}^{-1}[d^{obs}]=\mathcal{F}^{-1}[d^{true}+\delta d]=m_c+\delta m
```

Suppose $\|\delta d\|$ is small, does that mean $\|\delta m\|$ is small? If it is not, then we will say that the problem is “ill-conditioned”.

Using the relationship between $V_{rms}$ and $v_{int}$ in {eq}`815dcec5` suppose that our data is a constant, $V_{rms}=v_0$. The resulting model would be that same constant, $v_{int}(t) = v_0$. We can add a small sinusoidal perturbation to the data $(\delta d=a\sin(2\pi ft))$, such that the data is defined in {eq}`c2de4591`. Despite the addition of small perturbation to the data, the resulting perturbation to the model $\delta m$ is not small, as shown in {eq}`2f6367b7`, and thus

```{math}
:label: ec61be48

\delta v_{int}\propto \sqrt{\frac{fta}{v_0}}
```

Therefore $\delta v_{int}$ can be made arbitrarily large even if $a$ is small; we only need to increase the product $tf$. This inverse problem is considered ill-conditioned.

## Hands on with the app
