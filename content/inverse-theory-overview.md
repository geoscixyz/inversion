---
title: Inverse Theory Overview
description: ''
date: '2021-02-15T23:27:01.295Z'
venue: Inverse Theory
thumbnail: thumbnails/inverse-theory-overview.png
---

To understand our physical world we resort to experiments. Energy is input to an unknown system and data are recorded. The goal of inversion is to extract information about the system. In this chapter we look at the general inverse problem and, to provide context, present it within the discipline of geophysics. The procedures however are applicable to experiments in all areas of the physical sciences.

The goals for this chapter are to view the forward and inverse mappings as connections between “data space”, which contains our observations, and “model space” which contains the functions or vectors that describe our underlying system. The information about a sought model, the element that gave rise to the data, depends upon the physics of the experiment, the number of data and their uncertainties. There are many ways to pose, and solve, an inverse problem, but fundamental to all approaches is the realization that the solution is nonunique. Any inversion technique must address this at the outset.

In this overview we provide a simple interactive example with the corresponding Jupyter notebook, to illustrate why the goal of obtaining the sought model, with knowledge of the data alone, is “ill-posed” and generally “ill-conditioned”. This understanding serves as an introduction to our next chapter regarding how to solve an inverse problem using optimization.

## Contents

[Geophysical Experiment](./geophysical-experiments.md)
: Defining the geophysical problems we intend to model. For each problem, this includes defining the survey (sources and receivers), the data and the diagnostic physical property.

[Introduction to Inversion](./introduction-to-inversion.md)
: Providing a basic conceptual description of geophysical inversion.

[Forward Mapping](./forward-mapping.md)
: Representing the forward problem as a discrete mapping from the model space to the data space.

[Inverse Problem Fundamental Challenges](./inverse-problem-fundamental-challenges.md)
: Exploring the effects of non-uniqueness and ill-conditioning encountered when solving geophysical inverse problems.

[Solving an Ill-Posed Problem](./solving-an-ill-posed-problem.md)
: Overview of approaches for solving ill-posed (non-unique and/or ill-conditioned) inverse problems.

[Summary](./theory-summary.md)
: An overview of what was learned in this chapter.
