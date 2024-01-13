---
title: 'Exercise 2: Linear Tikhonov Inversion'
description: ''
date: '2021-07-27T21:40:39.390Z'
venue: Linear Tikhonov Inversion
---

In this investigation you can explore the components of a 1D synthetic inversion example, starting with model building, defining the kernel function, then forward modelling the data, adding noise, and finally inverting the data to recover a model. Specific instances of these components have been shown throughout the text above, and can be reproduced in the Jupyter notebook [LinearTikhonovInversion_Notebook.ipynb](oxa:VNMrkxzChhdveZyf6lmb/lb7CgEnVPzfs79VcKpB1 'LinearTikhonovInversion_Notebook.ipynb'). The corresponding notebook [LinearTikhonovInversion_App.ipynb](oxa:VNMrkxzChhdveZyf6lmb/8gDAkt6Yn0QN26MssI0p 'LinearTikhonovInversion_App.ipynb') contains the interactive widgets that allow you to adjust parameters and view results for the following.

## Forward Problem

The concepts about forward modelling can be explored individually in Steps 1-3, or in the composite widget. There are many aspects to explore but one idea can be readily investigated is that a datum is an inner product of the kernel function with the model. Equivalently, a datum is a volumetric “average” of the model with the “averaging function” being the kernel function. This is a useful mental model and forms the basis of resolution analysis, data importance and nonuniqueness that will be discussed throughout this module. For each forward modelling concept, consider the following questions while adjusting parameters:

- **Step 1 - Create a model**
  - _How does changing the structure of model change the data?_
  - _How does the data changed when a constant background is added to the model?_
- **Step 2 - Generate a sensitivity matrix**
  - _How does changing the number of data_ $N$_change your insights from the data?_
    - _Is there a number of data_ $N$ _where you no longer see changes in the data plot?_
  - _Adjust the parameters controlling the decay rate -_ $p_{min}, p_{max}$
    - _How do the rows of $\mathbf{G}$ change?_
    - _How does the data change?_
  - _Adjust the parameters controlling the frequency -_ $q_{min}, q_{max}$
    - _How do the rows of $\mathbf{G}$ change?_
    - _How does the data change?_
- **Step 3 - Simulate data and add noise**
  - _Consider different noise levels_
    - _When is the data dominated by the noise rather than signal from the model?_

## Inverse Problem

The numerical details regarding how we obtain a solution to the inverse problem are postponed until the [next chapter](https://curvenote.com/@geosci/inversion-module/inversion-with-svd/), but using Step 4 we can investigate the essential elements and understanding of linear Tikhonov inversion. By adjusting both the parameters in the Forward and Inverse Problems, consider the following scenarios and questions:

- **Clean data** - run the inversion with clean data (no noise added)
  - _Can the true model be recovered from the inversion exactly? Why or why not?_
  - _How does changing the misfit change the recovered model in this case (the misfit value must be non-zero)?_
- **Noise estimation** - run the inversion with noise contaminated data
  - _It is typical in field surveys to have only an estimate of the noise level - What happens if the estimated noise in the misfit is different from what was added in the Forward Problem? Too high? Too low?_
- **Noise level** - run the inversion with different levels of noise contaminated data
  - _How does changing the noise level of the data in the Forward Problem change the recovered model?_
- **Number of data** - run the inversion with different values of $N$
  - _Does more data always improve the recovered model?_
    - _Consider a large number of data with a higher noise level_
    - _Consider a smaller number of data with a lower noise level_
- **Reference model** - run the inversion with variations of the reference model
  - _Recall $m_{ref}$ is an adjustable constant and is effective only in the smallest model component - the derivative of a constant is zero_
  - _How much influence does the reference model $m_{ref}$ have on the recovered model?_
    - _Consider a zero reference model_
    - _Consider a reference model equal to the background model_
    - _Consider an incorrect reference model_
- **Model norms** - run the inversion with varying values of $\alpha_s$ and $\alpha_x$
  - Recall the smallest model and flattest model norms are not on the same scale
  - _How does the model change with only the smallest model norm included? $(\alpha_x =0)$_
  - _How does the model change with only the flattest model norm is included? $(\alpha_s =0)$_
    - _Does this scenario make sense?_
  - _Does the same balance of these terms work for different true models?_
- **Model components**
  - _Which components of the true model are best recovered by the inversion? Why?_
    - _Consider the location, amplitude, and shape of both the boxcar and Gaussian, the background value_
    - _Future consideration - If you knew something about the expected model, how could you influence the model to recover those details?_
    - _Does changing the kernel function parameters ($p, q$) change the recovered model components?_
- **Trade-off Parameter $\beta$** - run the inversion with varying $\beta$ ranges
  - _Do you get the same model with different ranges of $\beta$ values?_
  - _What happens the range of $\beta$ values is too small? - try several small ranges_
  - _What happens if are only a few values of $\beta$ over a large range?_
  - _Does the optimal value $\beta^_$ stay the same or similar when any of the changes in this investigation are made?\*
  - _In Explore mode view the $\phi_d~\text{vs}~\phi_m$ plot and adjust $\beta_i$ - similar to the examples in _[_2.7. Objective Function for the Inverse Problem_](oxa:VNMrkxzChhdveZyf6lmb/46OlD42gDBzA8SkHBwSK '2.7. Objective Function for the Inverse Problem')_-{numref}`Figure %s <LxF0fImli3FufWtnmAV5>` and {numref}`Figure %s <Hx4fVnPbS2LUU4eiZOLF>`_
  - _How does the model change when a $\beta$ that is too large is chosen? (overfitting the data)_
    - _How does the model change when a $\beta$ that is too small is chosen? (underfitting the data)_
- **Target Misfit** - run the inversion with varying values of $\chi_{fact}$
  - Recall the target data misfit value is $\phi_d^*=\chi_{fact}N$, thus when $\chi_{fact}=1$ the expected value of the misfit is the number of data $N$ ({eq}`198b31c2`)
  - _How does the model change when the inversion overfits the data_ $(\chi_{fact}<<1)$?
  - _How does the model change when the inversion underfits the data_ $(\chi_{fact}>>1)$?

The Jupyter notebooks associated with this investigation can be downloaded and run locally or run through the Binder link at the top of the notebooks. More details on this can be found in [Getting Started - Jupyter Notebook Apps](oxa:VNMrkxzChhdveZyf6lmb/txiA7lIdCWcNNYh4xduj 'Getting Started - Jupyter Notebook Apps').
