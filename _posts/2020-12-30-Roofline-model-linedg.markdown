---
layout: post
title: "Why GPUs? And Why DG?"
date: 2020-12-30 10:16:19 -0700
categories: cuda, GPU, hpc, discontinuous-galerkin, high-order, CFD
---

Modern high-performance computing is transitioning to be heavily reliant on GPU accelerators to achieve peak performance FLOPs. For example, [Sierra](https://hpc.llnl.gov/hardware/platforms/sierra) at Lawrence Livermore National Laboratory has a peak total of 125,626 TFLOPs and 120,960 peak TFLOPs are performed by the NVidia V100 GPUs. So we can see that about 96% of the total FLOPs are done by the GPUs.

 In this transition, we have to look to methods that meet the constraints set forth by the GPUs such as small memory (*i.e.* NVidia Tesla V100 has 16 GB of memory) and perform optimally when there exists a high [arithmetic intensity](https://crd.lbl.gov/departments/computer-science/par/research/roofline/introduction/). We define high arithmetic intensity as the ratio of FLOPs per byte of memory. Therefore we need to look into methods that perform as many computations for every byte of memory that we transfer to the device. On the more physics side of scientific computing, there is also need for higher order methods to help reduce the numerical diffusiveness. To sumarize, here are the three criteria for choosing an algorithm to help us transition into modern high-performance computing:

 1. Low memory footprint
 2. High arithmetic intensity
 3. High order method

Nodal discontinuous Galerkin (DG) methods offer a perfect solution for the high arithmetic intensity requirement. With DG methods, it is very easy to increase the order of the method to achieve high orders. One of the good characteristics of DG methods is that the stencil remains within a single element and its adjacent elements providing a great way to scale parallelization. We should note that arithmetic intensity will increase as the order of the DG method increases. 