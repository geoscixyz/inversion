---
title: Defining the Inverse Problem
description: ''
date: '2021-07-27T18:04:01.725Z'
name: statement-of-the-inverse-problem
venue: Linear Tikhonov Inversion
oxa: oxa:VNMrkxzChhdveZyf6lmb/iPh2GcyPHcbKFJrzGLc4
tags: []
keywords: []
---

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/dGelkLiTk1csJHaM8AU8.3","tags":[]}

In a typical physical problem we perform an experiment to collect data and use those data to infer something about the earth. The procedure is schematically represented in the diagram below. The “inversion processing” is the computational component that links the observations to the unknown earth model.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/cFtpNM4K3qAT83AO13wl.3","tags":[]}

```{figure} images/VNMrkxzChhdveZyf6lmb-cFtpNM4K3qAT83AO13wl-v3.png
:name: cFtpNM4K3qAT83AO13wl
:align: center
:width: 70%
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/zJDOeckTE5abcJopQU2h.13","tags":[]}

Let $m$ be a generic symbol for the physical property or parameters that are being sought. We refer to $m$ as the “model”. A more rigorous statement of the inverse problem is: “Given observed data, $d_{j}^{obs}$, where $j=1,\dots,N$, an estimate of their uncertainties, $\epsilon_j$, and the ability to carry out forward modelling,

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/58SCTuc4u4OkpuZPuoUB.5","tags":[]}

```{math}
:label: 3ffde9a8

d_j=\mathcal{F}_j[m]
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/3EPmPnjyjaHxreLlKGXY.5","tags":[]}

find the model that generated the data”. The quantity $\mathcal{F_j}$ is the forward modelling operator that was explained in [1. Inverse Theory Overview](oxa:VNMrkxzChhdveZyf6lmb/n4krShPqra002w55QQvU '1. Inverse Theory Overview'). It encompasses the physical equations, geometries and all details about the source and receiver.

Solving an inverse problem using optimization theory is a multi-step process and in this section we look at each component in detail. It suffices to work with a simple synthetic example to establish fundamental principles that will be essential for every inverse problem we encounter. We first develop the forward modelling.
