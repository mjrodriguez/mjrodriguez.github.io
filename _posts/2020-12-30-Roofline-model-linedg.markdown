---
layout: post
title: "Why GPUs? And Why DG?"
date: 2020-12-30 10:16:19 -0700
categories: cuda GPU hpc discontinuous-galerkin dg high-order CFD
---

# Introduction

Modern high-performance computing is transitioning to be heavily reliant on GPU accelerators to achieve peak performance FLOPs. For example, [Sierra](https://hpc.llnl.gov/hardware/platforms/sierra) at [Lawrence Livermore National Laboratory](https://www.llnl.gov/) has a peak total of 125,626 TFLOPs and 120,960 peak TFLOPs are performed by the NVidia V100 GPUs. So we can see that about 96% of the total FLOPs are done by the GPUs.

![Sierra](https://hpc.llnl.gov/sites/default/files/sierra-during-siting-cropped-LLNL.png) 

**Figure 1** - Sierra Supercomputer at Lawrence Livermore National Laboratory. [Source](https://hpc.llnl.gov/sites/default/files/sierra-during-siting-cropped-LLNL.png). 

 In this transition, we have to look to methods that meet the constraints set forth by the GPUs such as small memory (*i.e.* NVidia Tesla V100 has 16 GB of memory) and perform optimally when there exists a high [arithmetic intensity](https://crd.lbl.gov/departments/computer-science/par/research/roofline/introduction/). We define high arithmetic intensity as the ratio of FLOPs per byte of memory. Therefore we need to look into methods that perform as many computations for every byte of memory that we transfer to the device. On the more physics side of scientific computing, there is also need for higher order methods to help reduce the numerical diffusiveness. To sumarize, here are the three criteria for choosing an algorithm to help us transition into modern high-performance computing:

 1. Low memory footprint
 2. High arithmetic intensity
 3. High order method

![v100](https://www.nvidia.com/content/dam/en-zz/es_em/Solutions/Data-Center/tesla-v100/data-center-tesla-v100-nvlink-625-ud@2x.jpg) 

**Figure 2** - NVIDIA Tesla V100 GPU. [Source](https://www.nvidia.com/content/dam/en-zz/es_em/Solutions/Data-Center/tesla-v100/data-center-tesla-v100-nvlink-625-ud@2x.jpg).

# Finding an Appropriate Method for GPUs

The classical finite difference (FD) method offers a great and simple spatial discetization for PDEs but the stencil size grows as the order of the method increases. Moreover, FD method has difficulty with shocks due to solution of the strong form equations. Although [[1]](#1), provides modern point of view on the finite difference method. The finite volume (FV) method offers an alternative where the weak form of the equations are considered and thus the differentiation requirement of the solution is dropped. However, FV method also suffers from the increasing stencil size as the order of the method increases. In [[2]](#2), Shu provides a helpful discussion in the differences of FD, FV, and discontinuous Galerkin (DG) method. 

Nodal discontinuous Galerkin methods offer a good solution to our criteria of high arithmetic intensity and high order methods. With DG methods, it is very easy to increase the order of the method to achieve high orders. One of the good characteristics of DG methods is that the stencil remains within a single element and its adjacent elements providing a great way to scale parallelization. However, we should note that in order to fulfill the high arithmetic intensity we should consider nodal DG in the matrix-free setting. Since DG discretization operator can be formed from small dense matrices then we can expect the arithmetic intensity to be high since most of our work will be with dense matrices. The [Lawrence Berkeley Laboratory](https://www.lbl.gov/) provides this nice figure for arithmetic intensity and some popular methods:

![ai](https://crd.lbl.gov/assets/Uploads/FTG/Projects/Roofline/_resampled/ResizedImage600300-rooflineai.png "Arithmetic Intensity for Popular Algorithms") 

**Figure 3** - Arithmetic intensity for popular methods. [Source](https://crd.lbl.gov/assets/Uploads/FTG/Projects/Roofline/_resampled/ResizedImage600300-rooflineai.png).


# References

<a id="1">[1]</a> Reyes, Adam, et al. "A variable high-order shock-capturing finite difference method with GP-WENO." Journal of Computational Physics 381 (2019): 189-217.

<a id="2">[2]</a> Shu, Chi-Wang. "High order WENO and DG methods for time-dependent convection-dominated PDEs: A brief survey of several recent developments." Journal of Computational Physics 316 (2016): 598-613.