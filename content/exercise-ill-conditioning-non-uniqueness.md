---
title: 'Exercise 1: Nonuniqueness and Ill-conditioning '
description: ''
date: '2021-07-27T21:10:24.329Z'
name: exercise-ill-conditioning-non-uniqueness
oxa: oxa:VNMrkxzChhdveZyf6lmb/GGlM0PGWLPr83CAg9qM7
tags: []
---

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/Sd1fQKcbgQiVQ12ldX6Z.7"}

In this investigation you can explore the ideas of nonuniqueness and ill-conditioning as applied in the forward and inverse mappings using the rms to interval velocity shown above. The images throughout the previous examples are reproduced in the Jupyter notebook RMStoIntervalVelocity_Notebook. The corresponding notebook [RMStoIntervalVelocity_App.ipynb](oxa:VNMrkxzChhdveZyf6lmb/mdpRd2BmRVWZ830Wf1cp "RMStoIntervalVelocity_App.ipynb") contains interactive widgets that allow you to adjust parameters and view the results for the following:

- **Forward modelling** - calculated rms velocity data $V_{rms}$ given an adjustable interval velocity model $v_{int}$
- **Invert ‘infinite’ accurate data** - given the adjustable $V_{rms}$ data, recover the $v_{int}$ model from inversion and compare with the true model
  - The data function is over-sampled to approximate an infinite number of data points
- **Invert a of finite number of accurate data** - given the adjustable $V_{rms}$ data, recover the $v_{int}$ model from inversion and compare different interpolation methods
  - *What changes do you see in the data when the interpolation method is changed?*
    - *Do small changes in the data produce small changes in the model?*
  - *Which interpolation method provides the best approximation of the true model?*
  - *How would the changes in interpolation change your interpretation of the model?*
- **Invert a finite number of noisy data** - given the adjustable $V_{rms}$ data, recover the $v_{int}$ model from inversion and compare different interpolation methods and noise levels
  - *What changes do you see in the data when noise is added?*
    - *Do small changes in the data produce small changes in the model?*
  - *With noise added, does your choice of the optimal interpolation method change?*
  - *How many different data sets and models you could create from the adjustable parameters?*

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/ktobej3ViGF4zIsgYfEy.1"}

The Jupyter notebooks associated with this investigation can be downloaded and run locally or run through the Binder link at the top of the notebooks. More details on this can be found in [Getting Started - Jupyter Notebook Apps](oxa:VNMrkxzChhdveZyf6lmb/txiA7lIdCWcNNYh4xduj "Getting Started - Jupyter Notebook Apps").

