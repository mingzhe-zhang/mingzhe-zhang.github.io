---
title: "Understanding and Boosting Fully Homomorphic Encryption Applications on GPU"
collection: "publications"
permalink: "/publications/Cybersecurity2025-3"
venue: "CyberSecurity."
publication_year: 2025
citation: "<b>Understanding and Boosting Fully Homomorphic Encryption Applications on GPU</b>. Shengyu fan; Xianglong Deng; Xulong Tang; Weizhi Xu; Mingzhe Zhang. <i>CyberSecurity</i>."
---

## Abstract

Fully Homomorphic Encryption (FHE) is considered one of the most promising candidates for future privacy computing since it allows to directly compute the encrypted data. Though FHE enables secure computation on untrusted servers, its utilization is limited due to the dramatically increased computation workload and a 4–5 orders of magnitude slowdown ratio. Several previous works have been proposed to accelerate FHE on GPUs, while most of these efforts focus on the algorithm or scheduling and still leave a significant performance gap. However, there is a lack of understanding of the FHE applications from the micro-architecture level, which is important for further optimization of FHE applications or designing hardware accelerators. In this paper, we make a detailed analysis for running FHE on GPUs and present the following key performance bottlenecks at the micro-architecture level: (1) FHE applications require more capacity for the I-cache than other workloads; (2) FHE causes large amount of pipeline stalls due to the Read-After-Write (RAW) issues and significantly hurts the performance due to poor hardware utilization; (3) the capacity of texture cache is severely under-utilized in FHE execution. We propose a simple yet effective pure-hardware scheme for boosting FHE on GPUs based on these observations. Our proposed scheme significantly reduces the RAW-caused pipeline stalls by adding a small forwarding buffer. Besides, our proposed scheme also leverages a partition of the texture cache as the victim buffer for the proposed forwarding buffer to minimize the hardware overheads. We explore various design choices to balance the performance and hardware complexity. The experiment results show that our design improves the performance of the end-to-end FHE workflow by 47.5% with only 0.5% additional hardware overhead.

[Abstract source](https://doi.org/10.1186/s42400-025-00482-2)

## Paper links

- [Official paper / download](https://doi.org/10.1186/s42400-025-00482-2)
- [Official PDF](https://link.springer.com/content/pdf/10.1186/s42400-025-00482-2.pdf)
