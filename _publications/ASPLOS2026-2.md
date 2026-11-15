---
title: "A Framework for Developing and Optimizing Fully Homomorphic Encryption Programs on GPUs"
collection: "publications"
permalink: "/publications/ASPLOS2026-2"
venue: "31st International Conference on Architectural Support for Programming Languages and Operating Systems. ASPLOS 2026"
publication_year: 2026
citation: "<b>A Framework for Developing and Optimizing Fully Homomorphic Encryption Programs on GPUs</b>. Zhuoran Ji, Jianyu Zhao, Guang Fan, Mingzhe Zhang, Shoumeng Yan, Xueyu Wu, Lei Ju. <i>31st International Conference on Architectural Support for Programming Languages and Operating Systems</i>. <b>ASPLOS 2026</b>"
---

## Abstract

In sensitive domains such as healthcare and finance, machine learning increasingly employs Fully Homomorphic Encryption (FHE) to secure both user data and models. Although FHE's intrinsic parallelism naturally aligns with GPU architectures, optimizing GPU kernels alone remains insufficient for efficient end-to-end FHE application development. The inherent complexity of FHE schemes and intricate GPU-specific details impede developers from focusing on high-level program logic. Additionally, FHE's high memory requirements, fine-grained memory operations, and redundant computations introduce further optimization challenges, resulting in inefficiencies even when GPU kernels are individually optimized. This paper introduces EasyFHE, a framework designed to simplify the development and optimization of GPU-accelerated FHE applications. Similar to PyTorch, EasyFHE provides high-level interfaces for defining computational logic while automatically handling low-level tasks, such as implementation selection and memory management. Furthermore, it incorporates an optimization framework that systematically addresses performance bottlenecks by applying tailored optimization passes during the lowering from high-level FHE programs to GPU kernels. Compared to state-of-the-art open-source GPU FHE libraries, EasyFHE uniquely supports FHE programs with memory requirements exceeding typical GPU capacities, achieving an average speedup of 2.88× with a peak of 4.39×.

[Abstract source](https://doi.org/10.1145/3779212.3790120)

## Paper links

- [Official paper / download](https://doi.org/10.1145/3779212.3790120)
