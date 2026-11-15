---
title: "Accelerating Fully Homomorphic Encryption for Large Language Model Inference on Multi-GPU Systems"
collection: "publications"
permalink: "/publications/PPoPP2027"
venue: "ACM SIGPLAN Symposium on Principles and Practice of Parallel Programming"
publication_year: 2027
citation: "<b>Accelerating Fully Homomorphic Encryption for Large Language Model Inference on Multi-GPU Systems</b>. Jianyu Zhao, Zhiyuan Zhang, Guang Fan, Mingzhe Zhang, Shoumeng Yan, Lei Ju, Zhuoran Ji. <i>ACM SIGPLAN Symposium on Principles and Practice of Parallel Programming</i>. <b>PPoPP 2027</b>."
---

## Abstract

In sensitive domains such as healthcare and finance, large language models (LLMs) can use fully homomorphic encryption (FHE) to protect both user data and model parameters. However, FHE incurs prohibitive computational overhead, and even single-GPU execution remains too slow for practical deployment, necessitating multi-GPU acceleration. Existing systems typically either partition each FHE primitive across GPUs using a general-purpose strategy or exploit application-level parallelism by distributing tokens or linear-projection outputs across GPUs. However, FHE-based LLM inference differs fundamentally from plaintext inference and therefore requires specialized multi-GPU algorithms.

This paper presents HOLMES, a multi-GPU framework for FHE-based LLM inference. Rather than partitioning individual primitives, HOLMES parallelizes at the granularity of complete LLM operations, targeting the two dominant kernels: linear projection and activation evaluation. For linear projection, a cost model jointly captures computation, memory usage, and communication to select partitioning strategies. Component- and tower-granular pipelining overlaps input broadcasts with rotations, while readiness-driven reduction mitigates runtime imbalance. For activation evaluation, HOLMES maps polynomial evaluation onto a binary-anchor wavefront to shorten the critical path, pre-aggregates giant-step partial sums to reduce communication, and permutes block ownership across stages to balance baby-step workloads. Evaluation shows that HOLMES achieves average and peak speedups of 5.86X and 7.65X, respectively, on an A100 SXM system, versus 2.47X and 3.37X for the state-of-the-art multi-GPU implementation.
