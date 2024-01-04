---
title: Nonuniqueness
description: ''
date: '2021-07-27T18:48:22.184Z'
name: nonuniqueness
oxa: oxa:VNMrkxzChhdveZyf6lmb/GnzA9JWkZwIOCRGpfoEU
tags: []
---

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/ANgIxKDhtmoGvjQnl6AK.4"}

An inversion attempts to solve a linear system of equations where we have fewer equations $(N)$ than we have unknowns $(M)$. In the app the default number of parameters was $100$ while the number of data was $20$. The system of equations is underdetermined and there is an infinite number of models that can fit the data.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/nLkIUw91Lwxk7uy50ILv.7"}

This nonuniqueness, and insight about how to deal with it, is exemplified by a toy example consisting of two model parameters $\mathbf m = (m_1, m_2)$ and one datum $m_1+2m_2=2$. What is the solution to this problem? In fact any point along the straight line in {numref}`Figure %s <QnSQFBXrMEDwAXuinSO3>` below is a valid solution. Possibilities include $\mathbf m = (1, 0.5)$ or $\mathbf m = (2, 0)$.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/QnSQFBXrMEDwAXuinSO3.2"}

```{figure} images/VNMrkxzChhdveZyf6lmb-QnSQFBXrMEDwAXuinSO3-v2.png
:name: QnSQFBXrMEDwAXuinSO3
:align: center
:width: 50%

Nonuniqueness
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/LjTZihIcM0nejXxwYA18.5"}

If our goal is to find a single “best” answer to our inverse problem then we clearly need to incorporate additional information as a constraint. A metaphor that is sometimes helpful is the problem of selecting a specific person in a school classroom as portrayed in the image below {cite:p}`{numref}`Figure %s <8Fvod2SfmrYQX8isU0AC>``. To select a single individual via an optimization framework, we need to define a ruler by which to measure each candidate. A ruler, when applied to any member of the set, generates a single number, and this allows us to find the biggest or smallest member as evaluated with that ruler. The potential rulers are unlimited in number and they could be associated with: height, age, length of fingers, amount of hair, number of wrinkles, etc. In general, choosing a different ruler yields a different solution; although it is possible that the youngest person is also the shortest.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/8Fvod2SfmrYQX8isU0AC.2"}

```{figure} images/VNMrkxzChhdveZyf6lmb-8Fvod2SfmrYQX8isU0AC-v2.png
:name: 8Fvod2SfmrYQX8isU0AC
:align: center
:width: 40%

Selecting a specific person in a school classroom.
```

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/38o5NYqVb959O2LcklXN.6"}

The analogy with vectors is straight forward. Rulers for measuring length of vectors are quantified via a norm. For instance in the toy example above, the smallest Euclidean length vector that lies along the constraint line is shown by the red dot {cite:p}`{numref}`Figure %s <QnSQFBXrMEDwAXuinSO3>``. Of all of the points it is the one that is closest to the origin, that is, the one for which $(m_1^2 + m_2^2)$ is smallest.

+++ {"oxa":"oxa:VNMrkxzChhdveZyf6lmb/XdTnhWboEv4gm4L5t5NN.1"}

A methodology by which we can get a solution to the inverse problem is now clear. We define a “ruler” that can measure the size of each element in our solution space. We choose the one that has the smallest length and that still adequately fits the data. The name for our “ruler” varies but any of the following descriptors are valid: model norm, model objective function, regularization function or regularizer. We’ll use the term “model norm” since we are explicitly concerned the ranking the elements by their “size”.

