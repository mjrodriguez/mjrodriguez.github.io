---
layout: post
title:  "Requesting Interactive Session"
date:   2020-02-28 11:16:19 -0700
categories: git
---

My current research project relates to [implicit time integration schemes](https://en.wikipedia.org/wiki/Explicit_and_implicit_methods) for [discontinuous Galerkin methods](https://en.wikipedia.org/wiki/Discontinuous_Galerkin_method). Therefore, we need to solve a linear system at every time step. If we consider a nonlinear system then we need to linearize and assemble the Jacobian matrix. My current task is to assemble the Jacobian matrix on a GPU. To ease the development process then I request interactive sessions on the cluster. Here is what the command I use to request the interactive sessions:

```shell
srun -N 1 --partition=gpu-partition --time=2:00:00 --pty bash -i
```
I request one node (which has two GPUs) and for 2 hour chunks. This gives plenty of time to test the code. The partition will have to change depending on the cluster you are working on.