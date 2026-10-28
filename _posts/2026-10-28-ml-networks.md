---
layout: post
title: "Addressing Model and Data Heterogeneity in Multimodal LLM Training"
date: 2026-10-28
paper_authors: "Z. Zhang et al."
paper_venue: "SIGCOMM 2025"
paper_url: "https://dl.acm.org/doi/10.1145/3718958.3750472"
week: 5
tags: [LLM, machine learning training, multi-modal model]
---


## Key Idea 

LLM training frameworks, such as Megatron-LM, assume uniform model and uniform data, with every pipeline stage and every sample costing about the same. However, this paper shows that multimodal LLMs violate such assumptions. The encoder, LLM backbone, and generator need very different amounts of compute, and each sample carries a different amount of image data, which leads to unbalanced pipelines and stragglers. 
The authors hence propose **DistTrain**, which extends Megatron's framework by giving each module its own parallelism configuration and by moving data preprocessing and reordering off the GPU nodes.


## Critique
I found the problem diagnosis convicing and timely, since treating three very different modules as one homogeneous model clearly wastes GPUs. 
However, DistTrain's design depends on predicting workload in advance. The GPU split across modules is fixed before training from a sample of the data, and reordering estimates which samples are expensive from their size, yet the paper never shows how performance holds up when these predictions are wrong, e.g., when later training phases use more or larger images.

## Connections
A recurring theme in our readings has been systems whose built-in assumptions no longer match how they are actually used. DistTrain brings this theme to LLM training: just as [dcSim](/cs440-blog/2026/10/21/datacenter-transport/) and [DCP](/cs440-blog/2026/10/26/rdma/) rework the network for bursty AI traffic, DistTrain reworks the training system itself, because frameworks built for uniform text models no longer fit multimodal workloads.

