---
title: Inversion with SVD
description: ''
date: '2021-03-08T22:43:15.613Z'
venue: Inversion with SVD
---

Fundamental understanding about non-uniqueness and ill-conditioning of the linear inverse problem is readily achieved with the aid of Singular Value Decomposition (SVD). In this chapter we show how this decomposition ……

# Recall

### The Inverse Problem from [Inverse Theory Overview](https://curvenote.com/@geosci/inversion-module/inverse-theory-overview/)

Given observations $d^{obs}_i, ~i=1,\dots,N$, uncertainties $\epsilon_j$ and the ability to forward model $\mathcal{F}[m]=d$

```{figure} images/VNMrkxzChhdveZyf6lmb-ftaQ4p4rpJZF4uK1UOqy-v1.png
:name: e4147170
:align: center
:width: 30%
```

Find the earth model $m$ that gave rise to the data

```{figure} images/VNMrkxzChhdveZyf6lmb-hb0KkmXFAOqpLtWtFmsE-v1.png
:name: 36f2ec65
:align: center
:width: 30%
```

```{figure} images/VNMrkxzChhdveZyf6lmb-nkVSwUc4U6NH9a2SpAHb-v1.png
:name: b417fdf2
:align: center
:width: 30%
```

### The Linear Inverse Problem from [Linear Tikhonov Inversion](https://curvenote.com/@geosci/inversion-module/linear-tikhonov-inversion/)

$$\begin{aligned} d_i&=\int_vg_i(x)m(x)dx \\ g_i(x)&=e^{ipx}cos(2\pi iqx) \end{aligned}$$

where $d_j$ is the i{sup}`th` datum, $g_j$ the kernel function for the i{sup}`th` datum, and $m$ is the model

Each datum is an inner product of the model with the kernel function. If we evaluate one case: $d_i=\mathbf{g}\cdot\mathbf{m}=4.89$

```{figure} images/VNMrkxzChhdveZyf6lmb-uo7cfX7wdBJZH0QRCwh6-v1.png
:name: 3bec1691
:align: center
:width: 70%
```

### Basic Challenges of the Inverse Problem: Non-uniqueness

The data are defined such that

$$\begin{aligned} d_i&=\sum^M_{j=1}G_{ij}m_j \\ \mathbf{d}&=\mathbf{Gm}, ~~~G:(N\times M)\end{aligned}$$

Typically $M>N$ creating an underdetermined problem, which has infinitely many solutions. The inverse problem in this case is also ill-conditioned and small changes in the data will yield large changes in the model.

In this chapter we consider the question: How do we understand and deal with these elements?

# Solving $\mathbf{Gm}=\mathbf{d}$

Given $\mathbf{Gm}=\mathbf{d}$ and knowing $\mathbf{G}\in\R^{N\times M}$, $\mathbf{m}\in\R^M$, and $\mathbf{d}\in\R^N$, we want to write $\mathbf{m}=\mathbf{G}^{-1}\mathbf{d}$, but $\mathbf{G}$ is not sparse and $\mathbf{G}^{-1}$ does not exist.

For example, if we write $Gm=d$ as $m_1+2m_2=2$ such that $G=[1,2]$, $d=2$, and $m=(m_1,m_2)^T$ and consider $m=G^{-1}d$.

# Singular Value Decomposition

$\mathbf{G}=\mathbf{U}_p\mathbf{\Lambda}\mathbf{V}^T_p$

$d_i=\int_vg_i(x)m(x)dx$

$\mathbf{G}_p =\begin{pmatrix} ~-& \mathbf{g}_1 & -~ \\ & \vdots & \\ ~-& \mathbf{g}_N & - ~\end{pmatrix}$, where $\mathbf{G}$ is a $(M\times N)$ matrix

$\mathbf{U}_p =\begin{pmatrix} |& & | \\ \mathbf{u}_1 & \dots & \mathbf{u}_p\\ |& & | \end{pmatrix}$, where $\mathbf{U}_p$ is a $(N\times P)$ matrix and $\mathbf{u}_i$ are the singular vectors of the data space $(\mathbf{U}_p^T\mathbf{U}_p=\mathbf{I}_p)$

$\mathbf{\Lambda}_p =\begin{pmatrix} \lambda_1& & \\ & \ddots & \\ & & \lambda_p\\\end{pmatrix}$, where $\mathbf{\Lambda}_p$ is a $(P\times P)$ matrix and $\lambda_i$ are the singular values $(\lambda_1\geq\lambda_2\geq\dots\lambda_p>0)$

$\mathbf{V}_p =\begin{pmatrix} |& & | \\ \mathbf{v}_1 & \dots & \mathbf{v}_p\\ |& & | \end{pmatrix}$, where $\mathbf{V}_p$ is a $(M\times P)$ matrix and $\mathbf{v}_i$ are the singular vectors of the model space $(\mathbf{V}^T_p\mathbf{V}_p=\mathbf{I}_p)$

```{figure} images/VNMrkxzChhdveZyf6lmb-2Rz9jykJ0aipptum2uR6-v1.png
:name: e437840d
:align: center
:width: 70%
```

$\mathbf{m}^{\parallel}$: activated portion of the model space

$\mathbf{m}^{\perp}$: annihilator space

## Solving with SVD

$\begin{aligned}\mathbf{Gm}&=\mathbf{d}, ~\mathbf{G}=\mathbf{U\Lambda V}^T \\ \mathbf{U\Lambda V}^T\mathbf{m}&=\mathbf{d}\\ \mathbf{\Lambda V}^T&=\mathbf{U}^T\mathbf{d}\\ \mathbf{V}^T\mathbf{m}&=\mathbf{\Lambda}^{-1}\mathbf{U}^T\mathbf{d}\\ \mathbf{VV}^T\mathbf{m}&=\mathbf{V}\mathbf{\Lambda}^{-1}\mathbf{U}^T\mathbf{d}\end{aligned}$

Define $\mathbf{G}^\dagger=\mathbf{V\Lambda}^{-1}\mathbf{U}^T, ~\mathbf{m}_c=\mathbf{G}^\dagger\mathbf{d}$

$\mathbf{m}^\parallel=\mathbf{m}_c=\mathbf{VV}^T\mathbf{m}=\mathbf{V\Lambda}^{-1}\mathbf{U}^T\mathbf{d}$

$\mathbf{m}_c=\mathbf{V\Lambda}^{-1}\mathbf{U^T}\mathbf{d}=\sum^N_{i=1}\left(\frac{\mathbf{u}_i^T\mathbf{d}}{\lambda_i}\right)\mathbf{v}_i$

Effects: successively add vectors

```{figure} images/VNMrkxzChhdveZyf6lmb-2AFS7hbRY8Rq8mu5dFPk-v1.png
:name: 9291ec92
:align: center
:width: 70%
```

Each vector $\mathbf{v}_i$ is scaled by $\frac{\mathbf{u}_i^T\mathbf{d}}{\lambda_i}\rightarrow\infty$ if $\lambda_i\rightarrow0$

$\phi_d=\|\mathbf{Gm}-\mathbf{d}\|^2$

$\phi_m=\|\mathbf{m}\|^2$

$\mathbf{m}_c=\sum^p_{i=1}\left(\frac{\mathbf{u}_i^T\mathbf{d}}{\lambda_i}\right)\mathbf{v}_i$

## Ill-conditionedness

$\mathbf{m}_c=\sum^p_{i=1}\left(\frac{\mathbf{u}_i^T\mathbf{d}}{\lambda_i}\right)\mathbf{v}_i$

Small singular value $\leftrightarrow$ highly oscillatory, large amplitude of noise

```{figure} images/VNMrkxzChhdveZyf6lmb-NeDRwHOyXlMJEzfll63g-v1.png
:name: 2ca7cb19
:align: center
:width: 70%
```

## Truncated SVD

If data are inaccurate the noise is also amplified by $\frac{1}{\lambda_i}$

$\mathbf{m}_c=\sum^q_{i=1}\left(\frac{\mathbf{u}_i^T\mathbf{d}}{\lambda_i}\right)\mathbf{v}_i + \sum^N_{i=q+1}\left(\frac{\mathbf{u}_i^T\mathbf{d}}{\lambda_i}\right)\mathbf{v}_i$ but the second term causes more harm than good

So we simply use $\mathbf{m}_c=\sum^q_{i=1}\left(\frac{\mathbf{u}_i^T\mathbf{d}}{\lambda_i}\right)\mathbf{v}_i$, meaning the solution lies in a small sub-space.

Truncated SVD treats/takes care of issues caused by non-uniqueness and ill-conditioning

```{figure} images/VNMrkxzChhdveZyf6lmb-aIl7MDj8tcnYjjFT6W2r-v1.png
:name: 1f881a5f
:align: center
:width: 70%
```

```{figure} images/VNMrkxzChhdveZyf6lmb-ZyxhJFSnMyNj4YE2XJiB-v1.png
:name: 4ed31852
:align: center
:width: 70%
```

## Consider Tikhonov Solution

```{figure} images/VNMrkxzChhdveZyf6lmb-sHgfAJaEgBj52Bzxb5pg-v1.png
:name: 1494ed10
:align: center
:width: 70%
```

Data misfit $\phi_d=\|\mathbf{Gm}-\mathbf{d}\|^2$

Regularization (Model norm?) $\phi_m=\|\mathbf{m}\|^2$

Minimize $\begin{aligned}\phi&=\phi_d+\beta\phi_m\\ &=\|\mathbf{Gm}-\mathbf{d}\|^2+\beta\|\mathbf{m}_c\|^2\end{aligned}$

Minimum $\nabla\mathbf{g}=\nabla_m\phi=0$

Differentiate with respect to vector $\frac{\partial\phi}{\partial\mathbf{m}}=2\mathbf{G}^T(\mathbf{Gm}-\mathbf{d})+2\beta\mathbf{m}=0$

So $(\mathbf{G}^T\mathbf{G}+\beta\mathbf{I})\mathbf{m}=\mathbf{G}^T\mathbf{d}$, where $\mathbf{G}^T\mathbf{G}$ is a rank deficient $(M\times M)$ matrix, where $rank(\mathbf{G})\leq N, ~M>N$, but $\beta>0$, so adding $\beta\mathbf{I}$ makes all the Eigen values $\geq\beta$

Solve $\mathbf{Am}=\mathbf{b}$, letting $\mathbf{A}=\mathbf{G}^T\mathbf{G}+\beta\mathbf{I}$ and $\mathbf{b}=\mathbf{G}^T\mathbf{d}$

#### Tikhonov solution v TSVD

```{figure} images/VNMrkxzChhdveZyf6lmb-dVPDsLKXmCuyThbkOnIq-v1.png
:name: e98508a7
:align: center
:width: 70%
```

### Tikhonov, TSVD, weighted TSVD

$(\mathbf{G}^T\mathbf{G}+\beta\mathbf{I})\mathbf{m}=\mathbf{G}^T\mathbf{d}$

Exact correspondence is obtained by modifying to include weights

$\mathbf{m}_c=\mathbf{VT\Lambda}^{-1}\mathbf{Ud}$

$\mathbf{m}_c=\sum^p_{i=1}t_i\left(\frac{\mathbf{u}_i^T\mathbf{d}}{\lambda_i}\right)\mathbf{v}_i$

$\mathbf{T} =\begin{pmatrix} t_1& & \\ & \ddots & \\ & & t_p \end{pmatrix},~~0\leq t_i\leq 1$

$t_i=\frac{\lambda_i^2}{\lambda_i^2+\beta}$

```{figure} images/VNMrkxzChhdveZyf6lmb-vyKKknQjvQOTo5518bMs-v1.png
:name: ea907a1b
:align: center
:width: 70%
```

# Summary

```{figure} images/VNMrkxzChhdveZyf6lmb-2Rz9jykJ0aipptum2uR6-v1.png
:name: d31cfca1
:align: center
:width: 70%
```

$\mathbf{Gm}=\mathbf{d}$

$\mathbf{G}=\mathbf{U\Lambda V}^T$

$\mathbf{m}_c=\sum^p_{i=1}t_i\left(\frac{\mathbf{u}_i^T\mathbf{d}}{\lambda_i}\right)\mathbf{v}_i$

Small singular values are associated with high frequency vectors in the model space and amplify the noise

Instabilities are handled by truncating, adjusting their influence ($t_i=\frac{\lambda_i^2}{\lambda_i^2+\beta}$), which is exactly the same as solving the Tikhonov problem.

Minimize $\begin{aligned}\phi&=\phi_d+\beta\phi_m\\ &=\|\mathbf{Gm}-\mathbf{d}\|^2+\beta\|\mathbf{m}_c\|^2\end{aligned}$

#### What does the solution tell us?

```{figure} images/VNMrkxzChhdveZyf6lmb-Y8TUWflKXz3fEEjiG87N-v1.png
:name: b12e600b
:align: center
:width: 70%
```

A full data set can recover information about $\mathbf{m}^{\parallel}$

The regularized solution is in a reduced region of the model space

The geophysical model lies outside of this region. To explore that we need to incorporate more information.
