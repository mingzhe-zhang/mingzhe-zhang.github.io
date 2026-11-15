---
title: "A Bitwidth-Flexible Modular Multiplier with Shift-Free Accumulation for Efficient NTT Acceleration in FHE"
collection: "publications"
permalink: "/publications/ISCAS2026"
venue: "2026 IEEE International Symposium on Circuits and Systems. ISCAS 2026"
publication_year: 2026
citation: "<b>A Bitwidth-Flexible Modular Multiplier with Shift-Free Accumulation for Efficient NTT Acceleration in FHE</b>. Zihao Yang, Dian Jiao, Shengyu Fan, Xianglong Deng, Rui Hou, Mingzhe Zhang. <i>2026 IEEE International Symposium on Circuits and Systems</i>. <b>ISCAS 2026</b>"
---

## Abstract

The Number Theoretic Transform (NTT) dominates computation time in Fully Homomorphic Encryption (FHE), often consuming up to 90% of execution in schemes like CKKS. Consequently, NTT performance critically determines FHE accelerator efficiency. As NTT accelerators rely on modular multipliers, their cost and performance are bottlenecked by two key issues: 1) Overflow Handling requiring large bit-widths, increasing area/cost, and 2) Serial Shifting limits the parallelization and performance of modular multipliers. This paper presents a novel hardware-software co-designed NTT accelerator addressing these limitations. First, we transform the modular multiplication algorithm to decouple shift operations, converting shift-dependent steps into precomputable constants, eliminating the serial shift bottleneck. Second, leveraging these constants, we decompose modular reduction into a set of parallelizable sub-computations. Crucially, each unit operates without reserving bits for overflow, significantly reducing latency via parallelization while simultaneously eliminating overflow-handling circuit overhead. We implement an accelerator incorporating these techniques. Experimental results demonstrate the efficiency of the proposed scheme in NTT computational performance improvement.

[Abstract source](https://doi.org/10.1109/iscas66217.2026.11562590)

## Paper links

- [Official paper / download](https://doi.org/10.1109/iscas66217.2026.11562590)
