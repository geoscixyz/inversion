---
title: Model Norm
description: ''
date: '2021-07-27T19:02:24.879Z'
venue: Linear Tikhonov Inversion
---

Although all of our computations for solving the inverse problem are done using vectors and matrices, for most of our inverse problems were are attempting to find a function in 1D, 2D, or 3D that could have given rise to the data. When we address nonuniqueness it is helpful to remember that the theoretical underpinnings of our problem reside in a function space. As such we first introduce some norms for our function space and then discretize them with our mesh to get the final quantity to be minimized.

### Smallest Model Norm

```{math}
:label: 5bb81c63

\phi_m=\int (m-m^{ref})^2 dx
```

This norm penalizes the amplitude difference between the sought model $m$ and the reference model $m^{ref}$. Minimizing $\phi_m$ produces a solution that is close to $m^{ref}$ everywhere on the domain. Incorporating $m^{ref}$ a powerful way to include additional information into the inversion. It is common for inversionists to omit the reference model term and then say that they have not included apriori information. That is not correct; omitting it is the same as setting $m^{ref}=0$. The inversion will then produce a solution that is as close to zero as possible, and the details and character of that result might be quite incorrect.

### Flattest Model Norm

```{math}
:label: dd987b9d

\phi_m=\int \left(\frac{d(m-m^{ref})}{dx}\right)^2 dx
```

This norm penalizes derivatives and reduces the amount of structure in the final solution. The reference model $m^{ref}$ can be kept in this term or omitted. In the latter case the final solution is smooth throughout the domain. In working with this norm we often talk about the “smoothest” model but any verbal confusion is clarified by the equations. The choice of including a nonzero reference depends upon what you know about the underlying model and your goals for the inversion. We will address these subtitles later.

### Combined Norms

In most cases we desire a model that is close to a prescribed reference model and is also smooth. Mathematically this can be accomplished by combining the above two norms in a single objective function

```{math}
:label: 05257042

\phi_m=\alpha_s\int (m-m^{ref})^2 dx+\alpha_x\int (\frac{d(m-m^{ref})}{dx})^2 dx
```

The quantities $\alpha_s$ and $\alpha_x$ are nonnegative constants that adjust the relative importance of the two terms. If $\alpha_x=0$ then the result will be a smallest model (often with a substantial amount of structure) while setting $\alpha_s=0$ will generate a smooth model with fewer oscillations.

Intuitively, it might seem that if $\alpha_s = \alpha_x$ then the components of the model norm are equally important in controlling the final model. However, this is not the case. We note that the two integrals in {eq}`05257042` have different dimensions. The flattest model norms is scaled by $1/{dx^2}$ compared to the smallest model norm. If the cell size is 0.01, as it is in the app, then that amplifies the size of the norm by a factor of $10^4$. For the two terms, $\alpha_s \phi_s$ and $\alpha_x \phi_x$ to have similar magnitudes, $\alpha_s \simeq 10^4$ . This is a somewhat subtle point, but it is very important. The decision about what values of $\alpha$ are small, or large, depends upon the functions inside the integral and the discretization used in the problem. We shall revisit this aspect in later chapters.

The function norms presented above have their counter-parts in vector space. The smallest model can be written as

```{math}
:label: 64af53ab

\phi_m=\|\mathbf{m - m^{ref}}\|^2=\sum_{i=1}^M(m_i-m^{ref}_i)^2
```

For our toy problem, if $m^{ref}=0$, then the solution that fits the data is $\mathbf{m} = (0.392, 0.784)$ and $\phi_m = 0.768$. It is the black dot in [2.5. Nonuniqueness](oxa:VNMrkxzChhdveZyf6lmb/GnzA9JWkZwIOCRGpfoEU '2.5. Nonuniqueness')-{numref}`Figure %s <QnSQFBXrMEDwAXuinSO3>`. If the reference model is $\mathbf{m^{ref}}=(1, 1)$ the solution is $\mathbf{m} = (0.8, 0.6)$ and 0.2. It is shown as the blue dot.

The smoothness or flattest model term, written as

```{math}
:label: 8242954b

\phi_m=\|\frac{d\mathbf{m}}{dx}\|^2=\sum_{i=1}^{M-1}(m_{i+1}-m_i)^2
```

uses discrete differences and therefore has one fewer element in the summation. For our toy problem $\phi_m=(m_2-m_1)^2$; the solution is $\mathbf{m} = (0.667, 0.667)$ and $\phi_m = 0$, shown as the red dot in[2.5. Nonuniqueness](oxa:VNMrkxzChhdveZyf6lmb/GnzA9JWkZwIOCRGpfoEU '2.5. Nonuniqueness')-{numref}`Figure %s <QnSQFBXrMEDwAXuinSO3>`.
