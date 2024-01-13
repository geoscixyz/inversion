---
title: Nonlinear Inversion
description: ''
date: '2021-02-10T05:04:54.876Z'
venue: nonlinear inversion
thumbnail: thumbnails/nonlinear-inversion.png
---

In the previous sections we showed how observations from a linear system can be inverted to generate a candidate for the underlying model $m$ that produced the data. The model was found by minimizing an objective function composed of a misfit and regularization function. When both terms were represented as a sum of squares, the objective function is quadratic, and the solution can be found by solving a linear system of equations. In practise, things are often more complicated. This occurs when the mapping in the forward problem, $d=F[m]$, is non-linear, or when a non-quadratic regularization or misfit function is desired. In this case the objective function is non-quadratic and it likely has multiple local minima as well as the desired global minimum. There are many ways to attack this problem and some excellent references are (eg XXXX). In our work we will use iterative techniques where we start at a guessed solution and compute a perturbation step that takes us towards a nearest local minimum.

In this chapter we …..

## Linear Inversion Review

The inverse problem is set to minimize the objective function $\phi=\phi_d+\beta\phi_m$ with the data misfit function $\phi_d=\sum^N_{j=1}\left(\frac{\mathcal{F}_j(m)-d_j^{obs}}{\varepsilon_j}\right)^2$. For the linear problem, the forward problem is defined as $\mathbf{d}=\mathbf{Gm}$, and we make use of quadratic regularization $\int_v\left(m-m_{ref}\right)^2dv$ so as to solve the problem in one step.

## Non-linear Inversion

The inverse problem becomes non-linear in any of the following cases:

- when the forward operation $\mathcal{F}[m]$ is non-linear
- when the data misfit $\phi_d$ is not defined using an $l_2$-norm, e.g. $\sum\left|\frac{\mathcal{F}_i[m]-d_i}{\varepsilon_i}\right|$
- when the model objective function is not quadratic

### Forward

The forward problem is defined as $d=\mathcal{F}[m]$. If the forward operation is a linear operator, $\mathbf{d}=\mathbf{Gm}$, but if it is non-linear then $\mathcal{F}[am_1+bm_1] \neq a\mathcal{F}[m_1]+b\mathcal{F}[m_2]$. Such examples of non-linear problems include seismic, Maxwell’s first order wave equation, and DC resistivity.

### Inverse Problem

We now solve an optimization problem to minimize the objective function $\phi(m)=\phi_d+\beta\phi_m(m)$. Step 1 is to discretize the PDE and solve the forward problem, then Step 2 is to iterate until a suitable model is found.

### Non-linear Optimization

Consider a single variable $x$ and function $f$. We want to minimize the function $f(x)$. If $\mathcal{f}$, shown below, is the quadratic function

$$\begin{aligned} f(x)&=\frac{1}{4}x^2-3x+9\\ &=\left(\frac{1}{2}x-3\right)^2 \end{aligned}$$

```{figure} images/VNMrkxzChhdveZyf6lmb-tinZJdU5RuCJxORAqwav-v1.png
:name: 368d4baf
:align: center
:width: 40%
```

then we can take the derivative, set it equal to 0, and solve for $x$.

$$\begin{aligned} f\prime(x)&=\left(\frac{1}{2}x-3\right) \\ &=0\\ x&=6 \end{aligned}$$

We know that the minimum of $f{\prime}(x)=0$ and $f\prime\prime(x)>0$.

Suppose we have a function that is not quadratic, such as

$$f(x)=\left(\frac{1}{2}x-3\right)^2+ax^3+bx^4$$

where there are now multiple minimums, as shown below.

```{figure} images/VNMrkxzChhdveZyf6lmb-EXP3jQf2xeHRRI0TVrB0-v1.png
:name: ad8a4e5e
:align: center
:width: 40%
```

#### Newton’s Method

1. Begin with an initial guess of the minimum, $x_k$ along the non-quadratic function we want to minimize, $\mathcal{f}$.
2. Approximate $\mathcal{f}$ with a local quadratic $\hat{\mathcal{f}}$ at $x_k$ and solve for a step $\delta x$ that minimizes $\hat{\mathcal{f}}$ . The local quadratic $\hat{\mathcal{f}}$ is indicated in the example below by the black dashed parabola.

   $\begin{aligned}\hat{\mathcal{f}}(x_k+\delta x)&=\mathcal{f}(x_k)+\mathcal{f}\prime (x_k)\delta x+\frac{1}{2}f\prime\prime (x_k)\delta x^2 +\cancel{\mathcal{O}(\delta x^3)}\\ \hat{\mathcal{f}}\prime&=\mathcal{f}\prime (x_k)\delta x+\frac{1}{2}f\prime\prime (x_k)\delta x^2+\cancel{\mathcal{O}(\delta x^3)}\\ &=0\\ \mathcal{f}\prime\prime(x_k)\delta x&=-\mathcal{f}\prime(x_k)\\ \delta x&=-\frac{\mathcal{f}\prime(x_k)}{\mathcal{f}\prime\prime(x_k)}\end{aligned}$

3. Update the guess $x_{k+1}=x_k+\delta x$

```{figure} images/VNMrkxzChhdveZyf6lmb-ovg2L6KfGwtD178yCikC-v1.png
:name: e74ebf60
:align: center
:width: 40%
```

Quadratic converge: $\left|x_{k+1}-x^*\right|<c\left|x_k-x^*\right|^2$

Things can go wrong with $\delta x=-\frac{\mathcal{f}\prime(x_k)}{\mathcal{f}\prime\prime(x_k)}$

```{figure} images/VNMrkxzChhdveZyf6lmb-1mml1gcmD3h5d22iU5RT-v1.png
:name: 06320bb0
:align: center
:width: 40%
```

If we move in the wrong direction, we likely have negative curvature $\left(-\mathcal{f}\prime\prime(x)\right)$ and should instead use only the gradient $\delta x = c\mathcal{f}\prime (x)$, where $c$ is a constant. We choose $c$ such that $\left|\mathcal{f}(x+\delta x)-\mathcal{f}(x)\right|>\varepsilon$. It is also possible to move in the correct direction, but the curvature $\mathcal{f}\prime\prime(x)$ is wrong, indicating that our step length $\alpha$ is too large. We can change $\alpha$ and scale the step, so the updated guess $x_{k+1}=x_k+\alpha\delta x$ where $\alpha<1$.

#### Convergence Conditions

- $\mathcal{f}\prime(x)<$ tolerance
- $\|\delta x\|<$ tolerance
- $\mathcal{f}\prime\prime (x)>0$

```{figure} images/VNMrkxzChhdveZyf6lmb-sWVhtajmnVBB0FiEstWj-v1.png
:name: 620a16a8
:align: center
:width: 40%
```

#### Summary (Newton’s Method)

Linear:

```{figure} images/VNMrkxzChhdveZyf6lmb-uVcBRJMQuHKcQjqN4QC1-v1.png
:name: ed3cdd84
:align: center
:width: 40%
```

- solution in one step
- $\mathcal{f}\prime\prime(x)\delta x=-\mathcal{f}\prime(x)$
- $x^*=-\frac{\mathcal{f}\prime(x)}{\mathcal{f}\prime\prime(x)}$

Non-linear

```{figure} images/VNMrkxzChhdveZyf6lmb-YGM9uWk1k77zBRycRYe2-v1.png
:name: 4342909e
:align: center
:width: 40%
```

- iterate to convergence
- $\mathcal{f}\prime\prime(x_k)\delta x=-\mathcal{f}\prime(x_k)$
- $\delta x=-\frac{\mathcal{f}\prime(x_k)}{\mathcal{f}\prime\prime(x_k)}$
- $x_{k+1}=x_k+\alpha\delta x, ~ \alpha<1$

### Multivariate functions

- Minimize $\phi(m), ~ m\in\{m_1, m_2, \dots, m_M\}$
- Taylor expansion of $\phi(m)$
  - $\phi(m+\delta m)=\phi(m)+(\nabla_m\phi(m))^T\delta m+\frac{1}{2}\delta m^T\nabla_m(\nabla_m\phi(m))^T\delta m+\mathcal{O}(\delta m^3)$
- Note the similarity to single variable
  - $\mathcal{f}(x+\delta x)=\mathcal{f}(x)+\mathcal{f}\prime(x)\delta x+\frac{1}{2}\mathcal{f}\prime\prime(x)\delta x^2+\mathcal{O}(\delta x^3)$

Define the Gradient

$$\begin{aligned} g(m)&=\nabla_m\phi, ~ g\in \R^M \\ &=\begin{pmatrix} \frac{ \partial \phi}{\partial m_1} \\ \vdots \\ \frac{ \partial \phi}{\partial m_M} \end{pmatrix}\end{aligned}$$

The minimum of the gradient is defined such that $g(m^*)=0$.

Define the Hessian (symmetric matrix)

$$\begin{aligned} H(m)&=\nabla_m\nabla^T_m\phi, ~H\in\R^{M\times M} \\ &=\begin{pmatrix} \frac{\partial^2 \phi}{\partial m_1^2} & \frac{\partial^2 \phi}{\partial m_1\partial m_2} & \cdots & \frac{\partial^2 \phi}{\partial m_1 \partial m_M} \\  \frac{\partial^2 \phi}{\partial m_2\partial m_1} & \frac{\partial^2 \phi}{\partial m_2^2} & \cdots & \frac{\partial^2 \phi}{\partial m_2\partial m_M} \\  \vdots  & \vdots  & \ddots & \vdots  \\  \frac{\partial^2 \phi}{\partial m_M\partial m_1} & \frac{\partial^2 \phi}{\partial m_M\partial m_2} & \cdots & \frac{\partial^2 \phi}{\partial m_M^2}\end{pmatrix} \\ H_{i,j}&=\frac{\partial^2\phi}{\partial m_i \partial m_j}\end{aligned}$$

The minimum of the Hessian is defined such that $H(m^*)$ is positive definite.

### Finding a Solution

1. Begin with an initial model $m^{(k)}$
2. Solve $H\left(m^{(k)}\right)\delta m=-g\left(m^{(k)}\right), ~ \text{c.f.}\{\mathcal{f}\prime\prime(x)\delta x=\mathcal{f}\prime(x)\}$
3. Update the model $m^{(k+1)}=m^{(k)}+\alpha\delta m$

### Our Inversion

Minimize

$$\phi(m) = \frac{1}{2} \left|\left| \mathcal{F}[m]-d^{obs}\right|\right|^2 + \frac{\beta}{2} \| m \|^2$$

Gradient

$$\begin{aligned} g(m) &= \nabla_m \phi \\ &= J^T \left( \mathcal{F}[m]-d^{obs}\right) + \beta m \end{aligned}$$

Sensitivity:

$$\begin{aligned} \nabla_m\mathcal{F}(m)&=J\\ J_{ij}&=\frac{\partial \mathcal{F}_i[m]}{\partial m_j} \end{aligned}$$

Hessian:

$$\begin{aligned} H(m) &= \nabla_m g(m) \\ &= J^T J + \cancel{ (\nabla_m J)^T \big(\mathcal{F}[m]-d^{obs}\big)}  +\beta\end{aligned}$$

\*we neglect the second term

Final:

$$\begin{aligned} H\delta m &= -g\\ & \downarrow \\ \left(J^TJ+\beta\right)\delta m &=-\left(J^T\delta d+\beta m\right) \\ \delta d &= \mathcal{F}[m]-d^{obs}\end{aligned}$$

### Linear v. Non-linear

Non-linear Problem $\left(\mathcal{F}[m]=d\right)$:

$$\left(J^TJ+\beta\right)\delta m=-\left(J^T\delta d+\beta m\right), ~\delta d=\mathcal{F}[m]-d^{obs}$$

Linear Problem $(Gm=d)$:

$$\left(G^TG+\beta\right)\delta m=-\left(G^Td+\beta m\right)$$

The sensitivity $J$ acts as a local linear for non-linear operator $J\delta m=\delta d$

### General Algorithm

Minimize $\phi=\phi_d+\beta\phi_m$

1. initialize the model and $\beta$: $m^{(0)}, ~\beta^{(0)}$
2. Until convergence is reached, iterate through the following:
   1. $H\delta m=-g$
   2. $m^{(k+1)}=m^{(k)}+\alpha\delta m$, (via line search)
   3. $\beta^{(k+1)}=\frac{\beta^{(k)}}{\gamma}$, (via cooling)

There are a variety of ways to solve the system and selecting $\beta$ beyond a line search and the cooling rate.

```{figure} images/VNMrkxzChhdveZyf6lmb-NklWKxEiSORKecmGRyrh-v1.png
:name: 4778d796
:align: center
:width: 60%
```

### Summary

$$\phi(m)=\frac{1}{2}\left|\left|\mathcal{F}[m]-d^{obs}\right|\right|^2+\frac{\beta}{2}\left|\left|m\right|\right|^2$$

Linear

- Forward: $d=Gm$
- Inverse:

Non-linear

- $d=\mathcal{F}[m]$
- $\left(J^TJ+\beta\right)\delta m=-\left(J^T\delta d+\beta m\right)$
  - $\delta d=\mathcal{F}[m]-d^{obs}$
- $m^{(k+1)}=m^{(k)}+\alpha m$

All understanding from the linear problem is valid for the non-linear problem
