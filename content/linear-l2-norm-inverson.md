---
title: Linear L2-norm Inversion
description: ''
date: '2021-02-05T05:11:21.278Z'
venue: Linear L2-norm Inversion
thumbnail: thumbnails/linear-l2-norm-inverson.png
---

In this chapter we put the principles of Tikhonov inversion into practice and address the numerical under-pinnings for solving the linear problem using L2 norms for the misfit and model regularization. The function to be minimized is a quadratic and a solution the inverse problem can be achieved in a single step by solving a linear system of equations. We use our flowchart to keep us on-track as we step through the basic elements. For each element we provide background that will be of use when attacking any inverse problem. These include issues about the noise and misfit, the model norm, how to solve the system numerically, how to choose a tradeoff parameter, and some basic principles for evaluating the results of the inversion and potentially carrying out an inversion with revised parameters.

# Key Points

### Workflow for Inversion

A successful inversion of any data set requires a workflow in which each element can be critically addressed. The quality of a final result depends upon how well each of these is implemented and in the following we elaborate on each component.

```{figure} images/VNMrkxzChhdveZyf6lmb-KV36nNTMujTCmChumcXX-v1.png
:name: ab68fc54
:align: center
:width: 60%
```

```{margin}
**Figure 2.1:** The inverse workflow displays the necessary inputs and steps taken within the generic inverse problem.

```

### Inputs

There are three boxes under the “Inputs” heading.

#### Field Observations and error estimates.

This includes the obvious components such as knowing your survey acquisition parameters, the fields that are measured, and estimates of the uncertainties in the data. For instance, in a DC resistivity survey we need to know the locations of the current and potential electrodes, the transmitter current, how the electric potentials at the receiver electrodes are converted from the repetitions of the bi-polar transmitter current and stacked and subsequently processed to give a datum that corresponds to an ideal step-on transmitter current. Field logs are often required to reveal where challenges were encountered; for example electrodes could not be placed in their proposed locations because of trees, gullies, asphalt roads etc. These will later have to be modelled within the inversion, or included as “noise” in uncertainty estimates. Lastly, it is essential that all details about the subsequent processing of the data are known and importantly the final units of the data. Determining final units of the data and normalizations is traditionally one of the major hurdles for getting started on an inversion.

#### Prior Knowledge

Assembling your a priori knowledge about the project area is crucial. This includes what is known about the geologic structure, lithologies, rock types and their physical property values, borehole constraints, and information for other geophysical surveys. The culmination of this work is the development of a “reference model”. Ideally this is a 3D geologic model with each unit having an estimated range of the sought physical property. Even a simple geologic sketch or a deposit model for a mineral can be valuable at this stage. For some problems the reference model might be detailed and complicated while for other problems, where little is known, the reference model might be uniform and represented by a single number. Irrespective, development of a reference model in these early stages has three important benefits:

- it will be used in the model norm to ameliorate the non-uniqueness
- when linked with the survey and forward modelling, it provides a set of predicted data that can be used as a first order check about normalizations of the data
- compiling a priori information into a reference model often clarifies what is known, and what is unknown, about the earth model. This in turn helps generate objectives for carrying out the inversion. That is, what question about the earth do we want answered when the geophysical data are included in the inversion. This becomes important in a later box in the flowchart where the parameters for inversion are specified.

#### Forward modelling

The crucial component for solving an inverse problem is the ability to carry out a forward modelling to simulate data from an input model. That is, we want to evaluate

```{margin}
**Equation 1.4** Forward mapping operation $\mathcal{F}$ applied to an element of the model space $m$ to calculate the corresponding element in the data space $d$.

```

$$\mathcal{F}[m] = d$$

The forward modelling needs to be accurate, which in practice means that numerical errors are less than the “noise” in the data. It must also be efficient since the forward modelling must be done many times during the course of the inversion.

To numerically simulate data we generally discretize the problem onto a mesh (1D, 2D, 3D). The cells must be sufficiently small and extend to large enough distances so that relevant boundary conditions are satisfied and that the forward modelling operator produces sufficiently accurate results. In the case of our 1D problem, you can experiment with the accuracy of the simulation by comparing data generated with a very large number of cells with data produced by discretizing with fewer cells. The inaccuracies in this case also arise because of the way the integration of the kernels is carried out for each cell; here, a mid-point rule is chosen. This becomes less accurate as the size of the cells increases and/or the frequency of the kernel function increases.

### Define Inversion parameters

```{figure} images/VNMrkxzChhdveZyf6lmb-QxW3uQzDww1XhwRlz16b-v1.png
:name: 0772fe92
:align: center
:width: 60%
```

```{margin}
**Figure 4.1:** The inverse workflow ([Figure 2.1](https://curvenote.com/oxa:VNMrkxzChhdveZyf6lmb/Y1lrL2Ti6uotZ7Per2zY)), with focus on the definition of the inverse model parameters.

```

###

```{figure} images/VNMrkxzChhdveZyf6lmb-QxW3uQzDww1XhwRlz16b-v1.png
:name: bd8949cf
:align: center
:width: 40%
```

The mesh used for forward simulation is designed so that simulated results are high quality. We could use the same mesh for the inverse problem, as done in the notebook, but that is not necessary. Our inversion mesh could be composed of fewer cells, either by fixing the values of some cells and not including them in the inversion, or by homogenizing groups of cells. Moreover, the model parameters used for inversion might be different from those used in the forward simulation. As an example, in an electromagnetic problem the basic equations and forward simulation uses the electrical conductivity $\sigma$ so $\mathcal F[\sigma] =d$. But electrical conductivity is positive and varies over orders of magnitude. Both of these attributes can be handled readily by having the inversion parameters be $m = \log (\sigma)$.

### Misfit criterion

As discussed in the Tikhonov section we need some way to evaluate how close the predicted data are to the observations and then a criterion for choosing a target value for that misfit.

```{figure} images/VNMrkxzChhdveZyf6lmb-9lu75re1S6DPdYwYZfcl-v1.png
:name: 60b17fdb
:align: center
:width: 50%
```

Our observed datum is defined such that $d_j^{obs}=\mathcal{F}_j\left[m\right]+\tilde{n}_j$ where $\mathcal{F}_j\left[m\right]$ is our mathematical representation of the forward operator and $\tilde{n}_j$ is the additive noise. We want to find a model $m$ that gave rise to the data $d^{obs}$. The noise $\tilde n_j$ is a challenging element to quantify. It is built up from modelling errors and well as traditional experimental noise that is associated with any survey.

We first address modelling errors. The forward modelling for our physical system is as $\mathcal{F}_j\left[m\right]=F_j\left(m\right)$ where $m$ is a function and $\mathcal{F}[ \cdot]$ includes the complete physics of our problem. Our numerical forward operator $F_j[\cdot]$ does not represent that exactly. Thus $\mathcal{F}_j\left[m\right]=F_j\left(m\right)+\hat{n}_j$, where $\hat{n}_j$ are the discrepancies between the forward operator $F_j\left(m\right)$ and our mathematical representation $\mathcal{F}_j\left[m\right]$. These discrepancies are due to a variety of factors and assumptions such as the wrong dimension (1-D, 3-D), incomplete physics, or discretization errors. The statistics of these discrepancies are problem dependent and not easily quantified.

In addition to modelling errors there are also additional additive noise \\$\hat{n}_j\hat{n}_j$ that arises from the survey. Rewriting our observed datum with the numerical forward operator, $d_j^{obs}=F_j\left(m\right)+\hat{n}_j+\tilde{n}_j$. We can combine the additive noise in the observed data $\tilde{n}_j$ and the discrepancies in the forward operator $\hat{n}_j$ into one statistical variable that accounts for all the noise in the system $n_j$. Our observed datum is now $d_j^{obs}=F_j\left(m\right)+n_j$. Clearly the statistics of $n_j$ is challenging to quantify but for our present purposes, we assume that each is characterized by Gaussian distribution with a zero mean and a standard deviation $\epsilon_j$, that is $N[0, \epsilon_j]$. This is a huge simplification but we can take some comfort in the Central Limit Theorem (ref).

Consider a random variable $x_j \in \mathcal{N}(0,1)$. By taking a sum of squares we then define a new random variable, $\chi^2_N=\sum^N_{j=1}x^2_j$, which follows a chi-squared distribution with N-degrees of freedom. For this distribution the expected value is $E(\chi^2_N)=N$, the variance is $Var(\chi^2_N)=2N$, and the standard deviation is $std(\chi^2_N)=\sqrt{2N}$. In the next section we shall use $\chi^2_N$ as a misfit function for our inverse problem and its expected value as a target value.

### Misfit Function

There are two important components for any misfit function: specifying the metric used and determining the target misfit value. Here we will use an L2-norm, also known as the least-squares statistic, to define the data misfit function as

$\phi_d=\sum^N_{j=1}\left(\frac{F_j(m)-d_j^{obs}}{\varepsilon_j}\right)$.

We define the data weighting matrix

$\mathbf{W}_d=diag\left[\frac{1}{\varepsilon_1},\dots,\frac{1}{\varepsilon_N}\right]$

and rewrite the data misfit function as

$\phi_d=\left|\left|\mathbf{W}_d\left(F\left[\mathbf{m}\right]-d^{obs}\right)\right|\right|^2_2$.

In reality we do not know the uncertainties within the system so we estimate them as a percentage of the observed data, plus a constant noise floor,

$\varepsilon_j=\%\left|d_j^{obs}\right|+floor$.

Because the data misfit function is now a $\chi^2_N$ variable, the expected value is approximately the number of data, $E\left[\phi_d\right]=N$. In practise we often specify our target misfit $\phi_d^* = \chi N$ where $\chi$ is a scaler. Running inversions with $\chi < 1$ allows the Tikhonov curve to be explored and helps with the decision about how well we want to fit field data where the uncertainties are only guessed at.

Assigning uncertainties to data is a critical step in a practical inversion. This point cannot be over-emphasized. Unfortunately, there is no easy one-size-fits-all recipe. Each survey is different and much care and attention needs to paid for estimating each $\epsilon_j$. We offer some comments, although simplistic and general, might be useful.

- Try to balance the relative errors between data. If one datum is twice as noisy as another, this should be reflected in the relative value of assigned $\epsilon$. Balancing is especially important when working with a least squares misfit. If the uncertainty for one datum is a factor $\eta$ too small then its contribution to $\chi^2_N$ is a factor of $\eta^2$larger than it should be and this will over-weight the effects of that datum. This is a strong motivation to use a more robust statistical measure of misfit, such as an $L_1$ norm but we postpone that analysis until later.
- If the relative errors in the data set are balanced then a global scaling of the uncertainties can be handled by making use of the $\chi$ factor in $\phi_d^* = \chi N$. The effects of reducing all of the assigned uncertainties by a factor of two is the same as working with the existing problem and setting $\chi=4N$. This is convenient we shall make frequent use of this.
- The balancing of uncertainties mentioned above holds when thinking about two data or two sets of data. Suppose you have generated a procedure where you assign

: Below we outline some The suggestion of $\varepsilon_j=\%\left|d_j^{obs}\right|+floor$ and uncertainty is a good starting point.

### Model Objective Function

The model objective function can consist of one or a combination of the following model norms, discussed previously in LINK TO Linear Tikhonov Inversion:

- Smallest Model Norm

$$\phi_m=\int m^2 dx$$

- Smallest Model Norm with Reference Model

$$\phi_m=\int (m-m^{ref})^2 dx$$

- Smoothest Model Norm

$$\phi_m=\int \left(\frac{dm}{dx}\right)^2 dx$$

- Smallest & Smoothest Model Norm

$$\phi_m=\alpha_s\int (m-m^{ref})^2 dx+\alpha_x\int (\frac{d(m-m^{ref})}{dx})^2 dx$$

$$\phi_m=\alpha_s\left|\left|\mathbf{W}_s(\mathbf{m}-\mathbf{m}^{ref})\right|\right|^2+\alpha_x\left|\left|\mathbf{W}_x(\mathbf{m})\right|\right|^2$$

### Perform Inversion

We combine the data misfit and model objective functions into the objective function $\phi(\mathbf{m})=\frac{1}{2}\left|\left|\left(\mathbf{Gm}-\mathbf{d}^{obs}\right)\right|\right|^2_2+\frac{1}{2}\left|\left|\mathbf{W}_m\left(\mathbf{m}-\mathbf{m}_{ref}\right)\right|\right|^2_2$.

To solve the quadratic objective function for a single variable we calculate the derivative of the objective function with respect to the model $\mathbf{m}$

$$\begin{aligned} \mathbf{g}&=\nabla_m\phi\\ &= \mathbf{G}^T\mathbf{W}_d^T\mathbf{W}_d\left(\mathbf{Gm}-\mathbf{d}^{obs}\right)+\beta\mathbf{W}_m^T\mathbf{W}_m\left(\mathbf{m}-\mathbf{m}_{ref}\right)\\ \mathbf{g}&=0\\ \left(\mathbf{G}^T\mathbf{W}_d^T\mathbf{W}_d\mathbf{G}+\beta\mathbf{W}_m^T\mathbf{W}_m\right) &= \mathbf{G}^T\mathbf{W}_d^T\mathbf{W}_d\mathbf{d}^{obs}+\beta\mathbf{W}_m^T\mathbf{W}_m\mathbf{m}_{ref}\end{aligned}$$

Consider the matrix vector equation $\mathbf{Am}=\mathbf{b}$, where $\mathbf{A}\in\R ^{M\times M}$ is full rank and $\mathbf{m},\mathbf{b}\in\R ^M$, then the above can then be considered in the form $\mathbf{m}=\mathbf{A}^{-1}\mathbf{b}$.

### Managing Misfit with $\beta$

In the inverse problem we minimize $\phi_d+\beta\phi_m$ to find a model $\mathbf{m}$, but what $\beta$ should we use? If the standard deviations of the data are known, then the expected value of the data misfit is the number of data, $E\left[\phi_d\right]=N$, thus the desired misfit is $\phi_d^*\simeq N$. We must choose $\beta$ so $\phi_d(m)=\phi_d^*$.

```{figure} images/VNMrkxzChhdveZyf6lmb-QStXShQWyGTKQOBgS5V5-v1.png
:name: 9759ad1c
:align: center
:width: 30%
```

```{figure} images/VNMrkxzChhdveZyf6lmb-tkNFHSZ6cTZWDsixMv12-v1.png
:name: fa8363f9
:align: center
:width: 90%
```

There are several options for choosing $\beta$

1. Fix $\beta$ - guess a constant value for $\beta$ and perform the inversion
2. Solve $\mathbf{A}(\beta)\mathbf{m}=\mathbf{b}$ - for a logarithmic number of $\beta$, choose
   1. $\beta ^*$ where $\phi_d\simeq\phi_d^*$
   2. Select the corner point of the L-shaped curve, point of maximum curvature
3. GCV - Generalized Cross-Validation
4. Cooling strategy - perform successive inversions with $\beta _k=\frac{\beta _{k-1}}{\gamma}, ~ \gamma>1$
