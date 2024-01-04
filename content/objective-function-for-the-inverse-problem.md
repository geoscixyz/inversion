---
title: Objective Function for the Inverse Problem
description: ''
date: '2021-07-30T20:57:23.168Z'
name: objective-function-for-the-inverse-problem
oxa: oxa:VNMrkxzChhdveZyf6lmb/46OlD42gDBzA8SkHBwSK
tags: []
---

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/z5DzshyonIYiMpyvruQm.3"}

We pose our inverse problem in the following way: find a model $m$ that minimizes the model norm $\phi_m$ and produces an acceptable data misfit $(\phi_d<\phi_d^*)$. To do this we combine the data misfit $\phi_d(m)$ and model norm $\phi_m(m)$ terms and minimize the objective function

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/QvyNTADmViOIBRurAW2M.6"}

```{math}
:label: fd471526

\phi(m) = \phi_d(m)+\beta\phi_m(m)
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/ly8rAZgs0J06zFrUvgky.3"}

The parameter $\beta$ is known as the Tikhonov parameter or trade-off parameter. It is used to balance the relative influence of the two terms. Note that we explicitly include the dependence of the model $m$ in the two components of the objective function. We do this for clarity, since this is the vector of parameters we want to find. Optimization problems like this are prevalent in society where we want to simultaneously minimize two quantities.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/OXTW8i3WCpEtelAzO2ls.1"}

As a metaphorical example to understand the role of $\beta$ , we consider the options faced by a traveller who leaves his home at A and wants to drive to location B. He is concerned about travel time T, and fuel consumption F. These quantities are each related to speed. It is not possible to simultaneously minimize both T and F so the compromise is to consider

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/bZ96k0YcsCv0EP1eoqhM.4"}

```{math}
:label: 7c304ef3

\phi=T+\beta F
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/ag79PFLKWAt6nrpamhsq.6"}

When $\beta → 0$ we minimize the time irrespective of the fuel consumption. The gas peddle is on the floor. When $\beta → \infin$ the driver wants to use the absolute minimum amount of fuel so the gas peddle is barely engaged. This is displayed in {numref}`Figure %s <d31AdH08dO30KTmaxlYO>` where both T and F are plotted as a function of $\beta$. It is customary have the $\beta$ axis extend from a high value $\beta_H$ to a low value $\beta_L$ and this is indicated in the first two plots. A plot of $T~\text{vs}~F$ is shown in the third plot of {numref}`Figure %s <d31AdH08dO30KTmaxlYO>`. This is a monotonic curve and each point on the curve corresponds to a single $\beta$.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/d31AdH08dO30KTmaxlYO.2"}

```{figure} images/VNMrkxzChhdveZyf6lmb-d31AdH08dO30KTmaxlYO-v2.png
:name: d31AdH08dO30KTmaxlYO
:align: center
:width: 70%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/OBBaiqDj1UbmyP1vNT35.8"}

The tradeoff curve, often referred to as the Tikhonov curve, provides a suite of possible outcomes. A specific outcome may be obtained after applying an additional constraint: Suppose we want to minimize $F$, subject to a desired travel time $T^*=2hr$. That target value is plotted on the third diagram in {numref}`Figure %s <d31AdH08dO30KTmaxlYO>`.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/06wVl7O0rPQVMNFxLla8.3"}

The relationship between the travel example and the objective function for the inversion problem (Equation 2.17) is clear when the Tikhonov curve in {numref}`Figure %s <d31AdH08dO30KTmaxlYO>` is compared to that in {numref}`Figure %s <E9qugPIRBWvRhBsBAThm>`. The travel time $T$ is analogous to the data misfit $\phi_d$ and the target $T^*$ is analogous to the target misfit $\phi_d^*$ . The fuel consumption $F$ is analogous to the model norm $\phi_m$.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/E9qugPIRBWvRhBsBAThm.2"}

```{figure} images/VNMrkxzChhdveZyf6lmb-E9qugPIRBWvRhBsBAThm-v2.png
:name: E9qugPIRBWvRhBsBAThm
:align: center
:width: 70%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/Br1UjFWty7rYiqlb3Wm6.4"}

We have now generated the important components for our inverse problem. The misfit and model norm have been defined and minimization of our combined objective function {eq}`fd471526` yields a specific model to be interpreted. An important remaining item is “what value of $\beta$ is appropriate”?

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/ZM5nw7EUDUm1PyEmMPGx.3"}

A priori, we have no way of estimating an optimal $\beta^*$ and in practice it can vary by many orders of magnitude in different problems. To address this, we choose a suite of $\beta$ values that extend over many orders of magnitude, and then minimize {eq}`fd471526` for each $\beta_k$. Each minimization provides a model $m_k$, a misfit $\phi_{dk}$ and a model norm $\phi_{mk}$. These values can be plotted as shown below in the inversion simulation using the model and data created above ([Figure E](https://curvenote.com/oxa:VNMrkxzChhdveZyf6lmb/ejAaQ7Q2KvAmHkRE6dwa.18)). One choice for an optimal trade-off parameter $\beta^*$ is based upon the target misfit $\phi_d^*$. In practice however, we shall want to examine the Tikhonov curve more closely and use characteristics of that to help make a decision.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/ejAaQ7Q2KvAmHkRE6dwa.18"}

```{mdast} objective-function-for-the-inverse-problem.mdast.json#n0rxyKvZhA
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/WTMLL1nxDUXjSsyYlgco.3"}

**Figure E:** Inversion simulation results using the model ([2\.3. Forward Problem](oxa:VNMrkxzChhdveZyf6lmb/xqM34l8moONMZ4iDWIQf "2.3. Forward Problem")\-[Figure A](https://curvenote.com/oxa:VNMrkxzChhdveZyf6lmb/8WfrIYP5O9W6zakEQaa3.7)) and data ([2\.3. Forward Problem](oxa:VNMrkxzChhdveZyf6lmb/xqM34l8moONMZ4iDWIQf "2.3. Forward Problem")\-[Figure D](https://curvenote.com/oxa:VNMrkxzChhdveZyf6lmb/f4ZOfRjwPn87rmRQmgT3.9)) created in the Forward process above. The first panel displays the true model and recovered model from the inversion. The second panel shows both the observed (noisy) data and predicted data from the inversion. The third panel displays the data misfit and model norm terms as function of the trade-off parameter $\beta$, having run a suit of inversions with different values $\beta_k$, the optimal $\beta^*$ value indicated by the star. [LinearTikhonovInversion_Notebook.ipynb](oxa:VNMrkxzChhdveZyf6lmb/lb7CgEnVPzfs79VcKpB1 "LinearTikhonovInversion_Notebook.ipynb")

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/NHw33lGPn7Z9fmRjPGrH.2"}

If $\beta$ is too large, the model $\mathbf{m}$ is underfitting the data, causing loss of structural information.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/ZJvsuAh5doPl7d9VBAON.4"}

```{figure} images/VNMrkxzChhdveZyf6lmb-ZJvsuAh5doPl7d9VBAON-v4.png
:name: ZJvsuAh5doPl7d9VBAON
:align: center
:width: 70%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/LxF0fImli3FufWtnmAV5.2"}

```{figure} images/VNMrkxzChhdveZyf6lmb-LxF0fImli3FufWtnmAV5-v2.png
:name: LxF0fImli3FufWtnmAV5
:align: center
:width: 70%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/NPLpHWxCnHPSnqTZHfTm.2"}

If $\beta$ is too small, the model $\mathbf{m}$ is overfitting the data, causing noise to be imaged as structure.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/HjWa8hCAUYbiYNyQqLh6.3"}

```{figure} images/VNMrkxzChhdveZyf6lmb-HjWa8hCAUYbiYNyQqLh6-v3.png
:name: HjWa8hCAUYbiYNyQqLh6
:align: center
:width: 70%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/Hx4fVnPbS2LUU4eiZOLF.2"}

```{figure} images/VNMrkxzChhdveZyf6lmb-Hx4fVnPbS2LUU4eiZOLF-v2.png
:name: Hx4fVnPbS2LUU4eiZOLF
:align: center
:width: 70%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/kdrgidlY4lhnipbg5z1q.3"}

If $\beta$ is just right $(\phi^*_d \simeq N)$, the model $\mathbf{m}$ optimally fits the data, producing the best estimate to adequately recreate the observations as was shown in [Figure E](https://curvenote.com/oxa:VNMrkxzChhdveZyf6lmb/ejAaQ7Q2KvAmHkRE6dwa.18).

