---
title: "On Optimizing Intra- and Inter-chiplet Interconnection Networks in Multi-chiplet Systems for Accelerating FHE Encrypted Neural Network Applications"
collection: "publications"
permalink: "/publications/CASES2025"
venue: "the 14th International Conference on Compilers, Architectures, and Synthesis for Embedded Systems. CASES 2025"
publication_year: 2025
citation: "<b>On Optimizing Intra- and Inter-chiplet Interconnection Networks in Multi-chiplet Systems for Accelerating FHE Encrypted Neural Network Applications</b>. Zewei Lai, Jinhui Ye, Xiaohang Wang, Zheang Fu, Amit Kumar Singh, Yingtao Jiang, Kui Ren, Mei Yang, Sihai Qiu, Xiaodong Li, Xin Tang, Jie Song, Mingzhe Zhang. <i>the 14th International Conference on Compilers, Architectures, and Synthesis for Embedded Systems</i>. <b>CASES 2025</b>"
---

## Abstract

Fully Homomorphic Encryption (FHE) is regarded as a promising way to protect data privacy with encrypted computation. Due to high computation overhead, hardware based FHE accelerators were proposed to speed up FHE applications. To support complicated FHE-encrypted neural network applications, multi-chiplet based FHE accelerators were further proposed for scaling up system size, whereas one of the challenges is designing efficient intra- and inter-chiplet interconnection networks to accelerate data transfer. Conventional regular topologies like mesh or Kite either lead to high inter-chiplet transmission latency or excessive power consumption as these topologies assume uniform bandwidth or radix for nodes/links, ignoring the highly irregular distribution of inter-chiplet communication volumes. On the other hand, the problem of generating customized intra- and inter-chiplet interconnection networks has high complexity and previous network-on-chip topology generation works cannot efficiently improve the performance of intra- and inter-chiplet interconnection networks. In this article, the intra- and inter-chiplet interconnection optimization problem is defined, aiming to minimize the execution time of FHE applications under cost and power constraints. To efficiently solve this problem, we propose a bilevel optimization algorithm, which decomposes the problem into three sub-problems: (1) FHE parameters selection, (2) task-to-core mapping, and (3) intra-/inter-chiplet interconnection network topology generation. These sub-problems are then solved iteratively. Experimental results demonstrate that our proposed method reduces execution time by 51.66%, 43.16%, 39.44%, 43.34%, and 27.70% compared with REED and four multi-chiplet based FHE accelerators with mesh, Kite, Butterfly, and Florets as inter-chiplet interconnection networks. Therefore, the proposed method can effectively accelerate FHE applications on large-scale multi-chiplet systems.

[Abstract source](https://doi.org/10.1145/3762995)

## Paper links

- [Official paper / download](https://doi.org/10.1145/3762995)
- [Official PDF](https://dl.acm.org/doi/pdf/10.1145/3762995)
