---
title: Linear Tikhonov Inversion
description: ''
date: '2021-01-18T19:49:36.029Z'
venue: Linear Tikhonov Inversion
thumbnail: thumbnails/linear-tikhonov-inversion.png
---

## Introduction

In this chapter we present the basic elements for how an inverse problem can be formulated and solved using optimization theory. The quantity to be minimized is a weighted sum of misfit and regularization terms with their relative importance controlled by an adjustable Tikhonov parameter.

The inverse problem has many elements and a solution is best achieved by adhering to the workflow shown in {numref}`Figure %s <KV36nNTMujTCmChumcXX>` below. Throughout this chapter we investigate each of these steps and illustrate the concepts with a simple linear problem. Jupyter notebooks are provided so that the concepts can be explored ([LinearTikhonovInversion_App.ipynb](oxa:VNMrkxzChhdveZyf6lmb/8gDAkt6Yn0QN26MssI0p 'LinearTikhonovInversion_App.ipynb')) and all the corresponding figures in this article can be reproduced using [LinearTikhonovInversion_Notebook.ipynb](oxa:VNMrkxzChhdveZyf6lmb/lb7CgEnVPzfs79VcKpB1 'LinearTikhonovInversion_Notebook.ipynb'). The formative material for this chapter is extracted from the tutorial paper Inversion for Applied Geophysics: A Tutorial {cite:p}`Oldenburg20055`.

```{figure} images/VNMrkxzChhdveZyf6lmb-KV36nNTMujTCmChumcXX-v2.png
:name: KV36nNTMujTCmChumcXX
:align: center
:width: 70%
```

**Key Points**

- Forward Problem - model, mesh, kernel function, data, noise
- Inverse Problem - data misfit, regularization function, norms
- Optimization - choice of Tikhonov parameter

## Contents

**2.1. Forward Problem:** Defining the model, kernel function, data and noise for the forward problem. We also define the mesh, model parameters and mapping for discrete forward problems that can be solved numerically.

**2.2. Defining the Inverse Problem:**

**2.3. Data Misfit:**

**2.4. Non-Uniquness:**

**2.5. Model Norm:**

**2.6. Objective Function:**

**2.7. Summary:** An overview of what was learned in this chapter.
