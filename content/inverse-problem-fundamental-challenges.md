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

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/5p6zd29P0irLdHwChIYv.11","tags":[]}

Inversion $\mathcal{F}^{-1}$ is the process of mapping from the data space $\mathcal{D}$ to the model space $\mathcal{M}$ $(\mathcal{F}^{-1}:~\mathcal{D}\rightarrow\mathcal{M})$, shown in {numref}`Figure %s <5BftNeWYsxYv8h6lhtx5>`.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/5BftNeWYsxYv8h6lhtx5.2","tags":[]}

```{figure} images/VNMrkxzChhdveZyf6lmb-5BftNeWYsxYv8h6lhtx5-v2.png
:name: 5BftNeWYsxYv8h6lhtx5
:align: center
:width: 50%

Inversion $\mathcal{F}^{-1}$ is the process of mapping from the data space $\mathcal{D}$ to the model space $\mathcal{M}(\mathcal{F}^{-1}:~\mathcal{D}\rightarrow\mathcal{M})$.
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/uqWEH8OaD8K8aIJKplzd.5","tags":[]}

Two fundamental challenges when inverting data is the ill-conditioning of the problem and nonuniqueness of the solution. We can obtain intuition for this by considering the relationship in seismology between rms velocity $V_{rms}$ and interval velocity $v_{int}$ originally presented in [1.3 Forward Mapping](oxa:VNMrkxzChhdveZyf6lmb/0VkRIdgDMntmQzhLzHiP '1.3 Forward Mapping')-{eq}`a19b615c`. For this problem we define the following:

- **Forward Problem** $\mathcal{F}$: Given the model $v_{int}$ compute the data $V_{rms}$
- **Inverse Problem** $\mathcal{F}^{-1}$: Given the data $V_{rms}$ compute the model $v_{int}$

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/ozWUHg27kr03Son7n3z8.1","tags":[]}

Thus, given the data, $V_{rms}$, what is the velocity model, $v_{int}$ that produced the data? There are numerous questions that can be asked:

- Does a solution exist? - Is there any model that can produce the data?
- How do we construct a solution?
- Is the solution unique? - If you have found one candidate, are there others?
- How do we handle nonuniqueness? - If there are multiple solutions, which model best reflects the subsurface physical property distribution?

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/sY7Ye0pfJgtKtLqeG4uk.1","tags":[]}

The answers to these questions depend on the available data and it’s insightful to consider the following cases

- infinite amount of accurate data (perfection ✨ )
- finite amount of accurate data (no noise 💯 )
- finite amount of inaccurate data (reality 🌎 )
- changes to the model due to a small perturbation of the data

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/VelHTm1PnjcptCJY1AxO.8","tags":[]}

In the forward problem we are given $v_{int}$ and we calculate $V_{rms}$ “exactly” by carrying out the integration analytically ({eq}`cc63b0e8`) or numerically using extreme precision. The result is a function $V_{rms}(t)$ on the interval $[0, t_{max}]$.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/TS1EFEmJCuYjiRf9oce2.9","tags":[]}

```{math}
:label: cc63b0e8

V^2_{rms}(t)=\frac{1}{t}\int^{t_{max}}_0 v_{int}^2(u)H(t-u)du
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/WGo71zvzMK3kb1e1XMfb.1","tags":[]}

We notice that each datum is an integral of $v_{int}$ and hence structure observed in $v_{int}$ will appear as smoothed structure in the data $V_{rms}$. That is, the forward operator is a “smoother”. As an example consider an interval $v_{int} = v_0 + a sin(2 \pi f t)$. The interval velocity model and data are shown below for the special case of xxxx

```{figure} images/VNMrkxzChhdveZyf6lmb-Ca2uDOJsWjEA5cwlDOni-v1.png
:name: ae6b407d
:align: center
:width: 70%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/PFnAtoSIMS46aI5eKQ2u.1","tags":[]}

As a general rule all forward modelling operators are smoothers and the issue is conceptualized in the figure below

```{figure} images/VNMrkxzChhdveZyf6lmb-SwmBorpIy8mSuxNTdkyF-v1.png
:name: ad4a70ad
:align: center
:width: 70%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/Pa5NeI8W0JpU1Fp487U4.2","tags":[]}

If the forward mapping F smooths, then the inverse operator F^-1must “roughen”. This is easily seen in our example where the analytic inverse

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/uFaTmz0sPKcluy5Srd4U.6","tags":[]}

$\mathcal{F}^{-1}$ exists.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/YN3xWuUFLvRxO1PyurOF.9","tags":[]}

```{math}
:label: 815dcec5

v_{int}=V_{rms}(t)\left(1+\frac{2tV'_{rms}(t)}{V_{rms}(t)}\right)^{\frac{1}{2}}
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/MBUIkiuuF4QO9Bnrjwms.4","tags":[]}

We notice that there is a time derivate $V_{rms}^\prime (t)$ of the data. Differentiation is a roughening operator. Moreover this derivative is multiplied by $t$ which means that small changes in the data at later times will produce large changes in $v_{int}$. To explore the main concepts, we define an example for the rms velocity data,

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/BoYqRK5BjSO6jwAAB4AW.10","tags":[]}

```{math}
:label: c2de4591

V_{rms}(t)=v_0+a\sin(2\pi ft)
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/ZBXjFzV8ccV0HOspODip.4","tags":[]}

where $v_0$ is a constant, $a$ the amplitude of the sinusoid, and $f$ the frequency in Hz. The corresponding derivative of the data, required for the analytic inverse calculation ({eq}`815dcec5`) is

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/dB1iZKL3R6gRTlI9mOVG.9","tags":[]}

```{math}
:label: 2f6367b7

V'_{rms}(t)=2\pi af\cos(2\pi ft)
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/tqNqTtoTVeiFmAJdURL6.1","tags":[]}

###

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/be0sepFJN3LNFJQS70CQ.1","tags":[]}

We can solve equation (2) numerically by evaluating the integrand on a very fine mesh and using a quadrature integration and a finite difference for the derivative. The result is presented in Fig xx

```{figure} images/VNMrkxzChhdveZyf6lmb-sr29Sc2xALrSfJTtHDKY-v1.png
:name: ab267060
:align: center
:width: 70%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/qKK0zJkt4m0DJMjwsKL4.1","tags":[]}

The true and recovered interval velocity are identical.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/rZBBRuSPdpXuCjQ6TceZ.1","tags":[]}

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/F03gjrzBIdp3emPh9ETl.6","tags":[]}

### 1.5.1 Nonuniqueness

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

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/xCfraYyphToLWaBABFif.2","tags":[]}

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/N64DvToncDWajXOApNkl.7","tags":[]}

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/BU6WZmJSykuMsVv83LLh.5","tags":[]}

Whereas in {numref}`Figure %s <5BftNeWYsxYv8h6lhtx5>` the application of $\mathcal{F}^{-1}$ maps to a single point in model space, with a finite number of data, we have many possible models; these are indicated by the dark green subspace of the model space in {numref}`Figure %s <tfJv6scxau4VO7AZtTO3>`.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/tfJv6scxau4VO7AZtTO3.2","tags":[]}

```{figure} images/VNMrkxzChhdveZyf6lmb-tfJv6scxau4VO7AZtTO3-v2.png
:name: tfJv6scxau4VO7AZtTO3
:align: center
:width: 40%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/uviwyCwHooverPPCsPSo.5","tags":[]}

The nonuniqueness is exacerbated when we have a finite number of data contaminated with noise. As shown in {numref}`Figure %s <R7LoaGMcurI6TlSKSRyH>` below there are now more ways to interpolate the data and each interpolation will produce a different $v_{int}(t)$.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/8zjjwtZbOi53B4Jx3zp0.1","tags":[]}

```{figure} images/VNMrkxzChhdveZyf6lmb-OaY83EoVsmYutnckX6Db-v1.png
:name: a1e83824
:align: center
:width: 70%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/O5UR8EX1aalPReLSmIuz.1","tags":[]}

In the example below we add Gaussian noise with zero mean and standard deviation = 0.03 sec to the true data values. The point observations, along with error bars, are plotted in Fig xx. These data are linearly interpolated to generate $V_{rms}(t)$ for inversion. Even with small errors, the recovered model is exhibits considerable incorrect structure.

```{figure} images/VNMrkxzChhdveZyf6lmb-Etolf3e1mEkhU6ZFNOTK-v1.png
:name: a573121e
:align: center
:width: 70%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/NIR8aVm9C5uGUVWZ6O29.5","tags":[]}

With respect to our mapping diagram, the inaccurate data to be inverted now populate the dark blue region of the data space and the inverse process maps to a larger, dark green, region of the model space ({numref}`Figure %s <CCyR4OOMNpenuGi2LINI>`).

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/CCyR4OOMNpenuGi2LINI.2","tags":[]}

```{figure} images/VNMrkxzChhdveZyf6lmb-CCyR4OOMNpenuGi2LINI-v2.png
:name: CCyR4OOMNpenuGi2LINI
:align: center
:width: 50%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/lJDQKHXKIoxNaMsnzTFC.5","tags":[]}

### 1.5.2. Ill-conditioning

A second important aspect of the inverse problem is that of ill-conditioning. In most problems in geophysics, the forward operator is a smoothing operator. We saw that in the examples above but other insight arises from the fact that a geophysical datum often depends upon the physical properties in a volume of the subsurface. For instance, a gravity datum depends on the volumetric density distribution, or a DC potential depends upon all of the charges built up in the subsurface when a current is injected. So the data is effectively “averaging” the underlying physical property that we are attempting to find. The inverse problem must therefore “undo” this averaging. As in the previous examples, this often involves some type of differentiation of data to “roughen” the model. The practical question is whether that roughening results in model structures that are representative of the earth, or whether they present unrealistic structure. To quantify this we consider the following.

Let

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/eWJc8RI8UDu2T19kMQSt.6","tags":[]}

```{math}
:label: 1bc2c17d

d^{obs}=d^{true}+\delta d
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/Pdy4C81W4wlFSUo2wv9W.1","tags":[]}

where $\delta d$ is a perturbation on the data. Let

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/TaXITd9sMowbH20A8EKE.6","tags":[]}

```{math}
:label: d73ceb50

\mathcal{F}^{-1}[d^{true}]=m_c
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/2boWVqpPu3q9t6hq0mt5.2","tags":[]}

where $m_c$ is the constructed model. We can then write

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/yJTiTKTETafVxEIFbai8.8","tags":[]}

```{math}
:label: 5c78d503

\mathcal{F}^{-1}[d^{obs}]=\mathcal{F}^{-1}[d^{true}+\delta d]=m_c+\delta m
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/mG55hpI5lTCqKIYGJv2v.4","tags":[]}

Suppose $\|\delta d\|$ is small, does that mean $\|\delta m\|$ is small? If it is not, then we will say that the problem is “ill-conditioned”.

Using the relationship between $V_{rms}$ and $v_{int}$ in {eq}`815dcec5` suppose that our data is a constant, $V_{rms}=v_0$. The resulting model would be that same constant, $v_{int}(t) = v_0$. We can add a small sinusoidal perturbation to the data $(\delta d=a\sin(2\pi ft))$, such that the data is defined in {eq}`c2de4591`. Despite the addition of small perturbation to the data, the resulting perturbation to the model $\delta m$ is not small, as shown in {eq}`2f6367b7`, and thus

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/LvqtQqFT2lBARuGaF4jb.5","tags":[]}

```{math}
:label: ec61be48

\delta v_{int}\propto \sqrt{\frac{fta}{v_0}}
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/cuhkHQTICcIaX07Hxilh.1","tags":[]}

Therefore $\delta v_{int}$ can be made arbitrarily large even if $a$ is small; we only need to increase the product $tf$. This inverse problem is considered ill-conditioned.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/jWbtZAiUHnqlljFzy7AE.2","tags":[]}

## Hands on with the app
