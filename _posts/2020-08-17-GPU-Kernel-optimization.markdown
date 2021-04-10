---
layout: post
title:  "Collection of CUDA Kernel Optimization Links"
date:   2020-08-17 11:16:19 -0700
categories: CUDA GPU
---

Here is a collection of links that [Yohann Dudouit](https://people.llnl.gov/dudouit1) provided to me when I began optimizing the Jacobian assembly kernel. 

- What is a Roofline Model? [Click here to find out!](https://en.wikipedia.org/wiki/Roofline_model)
- Some general optimization links:
    - [roofline model](https://developer.download.nvidia.com/video/gputechconf/gtc/2019/presentation/s9624-performance-analysis-of-gpu-accelerated-applications-using-the-roofline-model.pdf)
    - [Shared mem](http://developer.download.nvidia.com/GTC/PDF/1083_Wang.pdf)
    - [Memory diagram](https://stackoverflow.com/questions/37732735/nvprof-option-for-bandwidth)
    - [White paper](https://arxiv.org/pdf/1804.06826.pdf)
    - [Intel advisor roofline](https://software.intel.com/content/www/us/en/develop/articles/intel-advisor-roofline.html)

- You can look at the stall reasons:
    - [Issue Efficiency](https://docs.nvidia.com/gameworks/content/developertools/desktop/analysis/report/cudaexperiments/kernellevel/issueefficiency.htm)
    - [Metrics](https://docs.nvidia.com/cuda/profiler-users-guide/index.html#metrics-reference-7x)
    - [Stall reasons Stack Overflow Question](https://stackoverflow.com/questions/14887807/what-are-other-issue-stall-reasons-displayed-by-the-nsight-profiler)

- You can use `nvprof` with:

    - `stall_constant_memory_dependency` for Percentage of stalls occurring because of immediate constant cache miss
    - `stall_exec_dependency` for Percentage of stalls occurring because an input required by the instruction is not yet available
    - `stall_inst_fetch` for Percentage of stalls occurring because the next assembly instruction has not yet been fetched
    - `stall_memory_dependency` for Percentage of stalls occurring because a memory operation cannot be performed due to the required resources not being available or fully utilized, or because too many requests of a given type are outstanding
    - `stall_memory_throttle` for Percentage of stalls occurring because of memory throttle
    - `stall_not_selected` for Percentage of stalls occurring because warp was not selected
    - `stall_other` for Percentage of stalls occurring due to miscellaneous reasons
    - `stall_pipe_busy` for Percentage of stalls occurring because a compute operation cannot be performed because the compute pipeline is busy
    - `stall_sync` for Percentage of stalls occurring because the warp is blocked at a `__syncthreads()` call
    - `stall_texture` for Percentage of stalls occurring because the texture sub-system is fully utilized or has too many outstanding requests

- Other resources:
    - [Memory vs. Compute bound](https://stackoverflow.com/questions/12811684/memory-bound-kernel-and-compute-bound-kernel-in-gpus)
    - [Basic GPU Optimization Strategies](https://www.paranumal.com/single-post/2018/02/26/basic-gpu-optimization-strategies)
    - [Roofline Model LBNL](https://docs.nersc.gov/development/performance-debugging-tools/roofline/)

The [MFEM](https://mfem.org/) team has recently written a nice little document containing many tips for optimizing GPU kernels in this [post](https://mfem.org/gpu-tips-n-tricks/).

Last updated: 11/16/2020