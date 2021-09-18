---
title: "Distilling Bit-level Sparsity Parallelism for General Purpose Deep Learning Acceleration"
collection: publications
permalink: /publications/MICRO2021
venue: "The 54th Annual IEEE/ACM International Symposium on Microarchitecture (MICRO ’21)"
date: 2021-10-18
citation: ''
---

## Abstract

Along with the rapid evolution of deep neural networks, the ever- increasing complexity imposes formidable computation intensity to the hardware accelerator. In this paper, we propose a novel computing philosophy called “bit interleaving” and the associate accelerator design called “Bitlet” to maximally exploit the bit-level sparsity. Apart from existing bit-serial/parallel accelerators, Bitlet leverages the abundant “sparsity parallelism” in the parameters to enforce the inference acceleration. Bitlet is versatile by supporting diverse precisions on a single platform, including floating-point 32 and fixed-point from 1𝑏 to 24𝑏. The versatility enables Bitlet feasible for both efficient inference and training. Empirical studies on 12 domain-specific deep learning applications highlight the following results: (1) up to 81×/21× energy efficiency improvement for training/inference over recent high performance GPUs; (2) up to 15×/8× higher speedup/efficiency over state-of-the-art fixed-point accelerators; (3) 1.5𝑚𝑚2 area and scalable power consumption from 570𝑚𝑊 (𝑓𝑙𝑜𝑎𝑡32) to 432𝑚𝑊 (16𝑏) and 365𝑚𝑊 (8𝑏) @28𝑛𝑚 TSMC; (4) highly configurable justified by abundant ablation and sensitivity studies.