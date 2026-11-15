---
title: "Falcon: Algorithm-Hardware Co-Design for Efficient Fully Homomorphic Encryption Accelerator"
collection: "publications"
permalink: "/publications/ASPLOS2026"
venue: "31st International Conference on Architectural Support for Programming Languages and Operating Systems. ASPLOS 2026"
publication_year: 2026
citation: "<b>Falcon: Algorithm-Hardware Co-Design for Efficient Fully Homomorphic Encryption Accelerator</b>. Liang Kong, Shengyu Fan, Xianglong Deng, Lei Chen, Guang Fan, Yilan Zhu, Geng Yang, Yisong Chang, Shoumeng Yan, Mingzhe Zhang. <i>31st International Conference on Architectural Support for Programming Languages and Operating Systems</i>. <b>ASPLOS 2026</b> "
---

## Abstract

Fully homomorphic encryption (FHE) enables computation on encrypted data without compromising privacy, positioning it as a promising solution for secure cloud computing. However, its substantial computational overhead impedes practical deployment, prompting the development of dedicated hardware accelerators. In practice, when deploying cryptographic algorithm optimizations on FHE accelerators, hardware constraints typically such as limited memory capacity, often lead to a disparity between theoretical algorithmic advantage and achievable hardware efficiency. We present Falcon, an algorithm-hardware co-design for efficient FHE acceleration. We first conduct computational analysis of the prevalent minimum key-switching method, and propose hardware-oriented algorithmic optimizations that substantially reduce computational overhead. We then introduce further refinements to decrease the inherent inter-cluster communication overhead in multi-cluster architectures, while preserving computational advantages. By characterizing the arithmetic patterns intrinsic to primary primitives, we devise hardware-specific arithmetic fusion and functional reuse across computational units. Finally, we present a memory-adaptive strategy to effectively deploy Falcon to prior accelerators under constrained on-chip memory budgets. Experimental results demonstrate that applying our algorithm–hardware co-design delivers up to a 1.48× speedup with a negligible area overhead (only a 0.8% increase).

[Abstract source](https://doi.org/10.1145/3779212.3790160)

## Paper links

- [Official paper / download](https://doi.org/10.1145/3779212.3790160)
