---
title: "Fully Homomorphic Encryption Acceleration: A Full-Stack Perspective"
permalink: /fhe-system/
author_profile: true
---

<div id="top"></div>

<style>
.fhe-nav { padding: 1em 1.2em; background: #f5f8fb; border-left: 3px solid #376b91; }
.fhe-nav ul { margin: .5em 0 0; padding-left: 1.3em; }
.fhe-nav li { margin: .3em 0; }
.fhe-nav li ul { font-size: .95em; }
.fhe-back { margin: 1.5em 0; font-size: .85em; }
.fhe-figure { margin: 1.5em 0; }
.fhe-art { position: relative; overflow: hidden; width: 100%; }
.fhe-art img { position: absolute; display: block; width: 100%; max-width: none; height: auto; left: 0; }
.fhe-figure figcaption { margin-top: .6em; font-size: .8em; color: #526170; line-height: 1.6; }
.fhe-note { padding: .9em 1.1em; background: #f5f8fb; font-size: .9em; }
</style>

Full-stack research on FHE acceleration · Algorithms, compilation, architecture, and systems

<nav class="fhe-nav" aria-label="Page contents">
<strong>On this page</strong>
<ul>
  <li><a href="#introduction">Introduction</a></li>
  <li><a href="#research-map">Research Overview and Cross-Layer Collaboration</a>
    <ul>
      <li><a href="#compiler">1. Algorithms and Compilation</a></li>
      <li><a href="#gpu">2. GPU Acceleration</a></li>
      <li><a href="#hardware">3. Dedicated Architecture and Circuits</a></li>
      <li><a href="#systems">4. Applications, Systems, and Supporting Tools</a></li>
    </ul>
  </li>
  <li><a href="#outlook">Future Directions</a></li>
</ul>
</nav>

<h2 id="introduction">Introduction</h2>

Fully Homomorphic Encryption (FHE) allows servers to compute directly on encrypted data. Users encrypt inputs locally, the cloud performs computation without decryption, and users decrypt the results. A cloud model can therefore run inference on encrypted inputs without learning their plaintext values.

This capability comes with substantial computation and data movement. A single model operation can expand into polynomial arithmetic, data rearrangement, key switching, and bootstrapping. Encoded model weights can also grow dramatically. Faster individual operators therefore do not necessarily make the entire application faster.

Our research asks: **How can improvements across the stack translate into end-to-end gains in deployable systems?** We study commercial GPUs, dedicated accelerators, and heterogeneous systems, considering execution efficiency, memory capacity, communication, energy, and development cost together. The long-term research plan described on this website spans 2024–2029, building on earlier GPU and dedicated-architecture work.

<p class="fhe-back"><a href="#top">Back to the top</a></p>

<h2 id="research-map">Research Overview and Cross-Layer Collaboration</h2>

We organize the research into four connected areas, guided by three goals: **improve device utilization, reduce computation, and reduce storage and data transfers**. These goals overlap: operator fusion, for example, can eliminate both arithmetic and intermediate writes to device memory.

<figure class="fhe-figure">
<div class="fhe-art" style="aspect-ratio: 1248 / 300;"><img src="{{ '/images/fhe-system/research-atlas.png' | relative_url }}" style="top: 0; margin-top: -0.0%;" alt="Full-stack research: applications define requirements, algorithms and compilers optimize programs, and GPUs, dedicated architectures, and circuits provide efficient execution." /></div>
<figcaption>Figure 1 · Four connected research areas and their shared optimization goals. The illustration organizes research concepts rather than depicting a physical chip layout.</figcaption>
</figure>

| Research area | Core question | Contribution to the stack |
| :--- | :--- | :--- |
| Algorithms and compilation | Which operations can be avoided, and when is bootstrapping needed? | Encrypted programs with lower depth and less redundancy |
| GPU acceleration | How can existing parallel execution units be used effectively? | Efficient kernels and program-level execution mappings |
| Dedicated architecture and circuits | How should hardware adapt to bit widths, operators, and encryption schemes? | Reusable and reconfigurable compute and storage resources |
| Applications and heterogeneous systems | Where should models, keys, and tasks reside? | Multi-device execution and end-to-end validation |

Four terms help explain the work below. **CKKS** supports approximate numerical computation. The **Number Theoretic Transform (NTT)** is a key kernel for polynomial multiplication. **KeySwitch** uses evaluation keys and intermediate polynomials to switch ciphertexts between keys. **Bootstrapping** restores the capacity for further encrypted computation, but is itself expensive.

<p class="fhe-back"><a href="#top">Back to the top</a></p>

<h2 id="compiler">1. Algorithms and Compilation: Reducing Computation</h2>

### Research Approach

The cost of an encrypted program depends on both its operations and their representation. Successive multiplications consume the available multiplicative depth. Poor bootstrapping decisions, isolated optimization of cryptographic primitives, and restrictive operator boundaries can add overhead. We expose cross-operator optimization opportunities and jointly plan depth, data reuse, and execution order while preserving application semantics and accuracy requirements.

<figure class="fhe-figure">
<div class="fhe-art" style="aspect-ratio: 1248 / 243;"><img src="{{ '/images/fhe-system/research-atlas.png' | relative_url }}" style="top: 0; margin-top: -24.759615384615387%;" alt="Algorithms and compilation: depth planning and operator fusion produce optimized encrypted programs." loading="lazy" /></div>
<figcaption>Figure 2 · Program-level optimization reduces redundant operations and unnecessary consumption of multiplicative depth.</figcaption>
</figure>

### Representative Results

- [FHEFusion · CGO 2026]({{ '/publications/CGO2026' | relative_url }}): Preserves neural-network semantics alongside FHE-specific operations in its intermediate representation. Algebraic rules and a cost model expose fusion opportunities that reduce multiplicative depth.
- [HPAO · CGO 2027]({{ '/publications/CGO2027' | relative_url }}): Expresses cross-primitive optimizations at the polynomial level, enabling systematic application of techniques such as ModUp and ModDown hoisting and lazy modular reduction. The listed conference year is 2027.
- [A Survey on FHE Compilers · Cybersecurity 2025]({{ '/publications/Cybersecurity2025-2' | relative_url }}): Reviews parameter selection, ciphertext management, and program optimization, providing an entry point to the FHE compilation toolchain.

- [Libra · USENIX Security 2026]({{ '/publications/Security2026' | relative_url }}): Combines a cross-scheme representation with pattern-aware, hardware-aware scheduling to generate efficient GPU code for computations spanning multiple FHE schemes.

### Additional Work Highlighted in the Presentation

The presentation also highlights [ANT-ACE (CGO 2025)](https://ant-research.github.io/ace-compiler/), a compiler framework for automating neural-network inference, and [ReSBM (ASPLOS 2025)](https://ant-research.github.io/ace-compiler/), which plans region-based scaling and minimal-level bootstrapping through a min-cut formulation. These works connect program construction with depth and refresh management. Both links lead to the official ANT-ACE website, which provides project information and publications.

<p class="fhe-back"><a href="#top">Back to the top</a></p>

<h2 id="gpu">2. GPU Acceleration: Using Commercial Hardware Effectively</h2>

### Research Approach

GPU parallelism alone does not guarantee high FHE performance. Dependencies in transform kernels cause pipeline stalls, intermediate results repeatedly travel through device memory, and native algorithms may not match matrix execution units. We combine algorithm transformations, data-layout optimization, and kernel fusion to use CUDA Cores and Tensor Cores effectively, then evaluate the gains in complete applications.

<figure class="fhe-figure">
<div class="fhe-art" style="aspect-ratio: 1248 / 238;"><img src="{{ '/images/fhe-system/research-atlas.png' | relative_url }}" style="top: 0; margin-top: -45.2724358974359%;" alt="GPU acceleration: hardware-aware mapping of NTT, basis conversion, and inner products to CUDA Cores and Tensor Cores." loading="lazy" /></div>
<figcaption>Figure 3 · Mapping cryptographic computation to suitable execution units while reducing traffic across kernel boundaries. The arithmetic symbols on the left are conceptual, rather than a shared exact formula for NTT, basis conversion, and inner products.</figcaption>
</figure>

### Representative Results

- [TensorFHE · HPCA 2023]({{ '/publications/HPCA2023-1' | relative_url }}): Reformulates NTT as matrix computation and batches independent operations to improve parallel GPU execution.
- [WarpDrive · HPCA 2025]({{ '/publications/HPCA2025' | relative_url }}): Combines computation decomposition, fine-grained memory access, and CUDA Core/Tensor Core cooperation to improve compute and memory utilization.
- [Neo · ISCA 2025]({{ '/publications/ISCA2025-2' | relative_url }}): Extends matrix-unit acceleration to basis conversion and inner products through joint algorithm and data-layout optimization.
- [Helios · MICRO 2026]({{ '/publications/MICRO2026-2' | relative_url }}): Optimizes recurring hot modules using graph rewriting to enlarge fusion regions, followed by microarchitecture-aware mapping to reduce device-memory traffic.
- [GPU FHE Programming and Optimization Framework · ASPLOS 2026]({{ '/publications/ASPLOS2026-2' | relative_url }}): Connects encrypted-program development and optimization with GPU execution through a unified framework.

- [TensorFHE+ · IEEE TC 2025]({{ '/publications/TC2025' | relative_url }}): Extends linear-algebra-based GPU acceleration through vector/matrix formulations, vectorized modular arithmetic, and memory-efficient layouts.
- [HyperDrive · ISCA 2026]({{ '/publications/ISCA2026-1' | relative_url }}): The paper “Hierarchical Exploitation of Memory Efficiency for GPU-Based FHE Acceleration” optimizes register, shared-memory, and global-memory access together with operation-level reuse.
- [MNEMOS · ISCA 2026]({{ '/publications/ISCA2026-2' | relative_url }}): Targets TFHE through memory-aware data layouts, access scheduling, and Tensor-Core-oriented FFT mapping for programmable bootstrapping.
- [Understanding and Boosting FHE Applications on GPU · Cybersecurity 2025]({{ '/publications/Cybersecurity2025-3' | relative_url }}): Characterizes instruction-cache pressure, dependency stalls, and cache underutilization, and studies lightweight architectural support.

### Related GPU Cryptography

- [FORGE · HPCA 2027]({{ '/publications/HPCA2027-3' | relative_url }}): Uses GPU-oriented FAFFT ring arithmetic and end-to-end execution optimization for HQC and BIKE. These are post-quantum key-encapsulation mechanisms, rather than FHE schemes; this work provides related expertise in GPU cryptographic execution. The listed conference year is 2027.

The presentation additionally lists **GIF-FHE (IEEE TPDS)**, an implementation and evaluation of GPU-accelerated FHE using integer and floating-point computation. A dedicated publication page is not currently available on this website.

<p class="fhe-back"><a href="#top">Back to the top</a></p>

<h2 id="hardware">3. Dedicated Architecture and Circuits: Adapting Hardware to FHE</h2>

### Research Approach

Dedicated hardware offers control over compute units and on-chip dataflow, with trade-offs among performance, area, energy, and generality. We study arithmetic bit widths, shared operator structure, key decomposition, and on-chip capacity. The aim is to adapt parallelism to demand, reuse hardware across operators or encryption schemes, and reduce expensive modular arithmetic and inter-chip transfers.

<figure class="fhe-figure">
<div class="fhe-art" style="aspect-ratio: 1248 / 193;"><img src="{{ '/images/fhe-system/research-atlas.png' | relative_url }}" style="top: 0; margin-top: -65.22435897435898%;" alt="Dedicated architecture and circuits: tunable bit widths, shared compute resources, and reconfigurable accelerators adapt hardware to cryptographic computation." loading="lazy" /></div>
<figcaption>Figure 4 · Bit-width adaptation, resource sharing, and reconfigurable computation balance performance, area, and compatibility.</figcaption>
</figure>

### Representative Results

- [Trinity · MICRO 2024]({{ '/publications/MICRO2024' | relative_url }}): Uses reconfigurable compute resources to support different FHE schemes, combining broader applicability with efficient acceleration.
- [FAST · ISCA 2025]({{ '/publications/ISCA2025-1' | relative_url }}): Matches compute units to varying bit-width requirements, exposing scalable arithmetic parallelism.
- [HAWK · MICRO 2025]({{ '/publications/MICRO2025-1' | relative_url }}): Aligns key decomposition with fixed hardware word lengths to reduce extra arithmetic and evaluation-key storage.
- [Falcon · ASPLOS 2026]({{ '/publications/ASPLOS2026' | relative_url }}): Co-designs bootstrapping algorithms and hardware to organize computation, fuse operations, and reuse results under on-chip capacity and communication constraints.
- [ALLMod · DAC 2025]({{ '/publications/DAC2025' | relative_url }}): Improves the area efficiency of lookup-table-based large-integer modular reduction through hybrid workloads.
- [ArborDorp · TCAD 2026]({{ '/publications/TCAD2026-4' | relative_url }}): Extracts common arithmetic across kernels to share compute units and improve area efficiency.
- [AutoNest · HPCA 2026]({{ '/publications/HPCA2026' | relative_url }}): Co-optimizes FPGA NTT algorithms and dataflow, with support for automated accelerator generation.
- [CACO · TCAD 2026]({{ '/publications/TCAD2026-3' | relative_url }}): Exploits higher-level parallelism and optimized mappings to reduce inter-chiplet communication.

### Additional Architectures and Arithmetic Building Blocks

- [Poseidon · HPCA 2023]({{ '/publications/HPCA2023-2' | relative_url }}): An early dedicated homomorphic-encryption accelerator that forms part of the architectural foundation of this research program.
- [Taiyi · IEEE TC 2026]({{ '/publications/TC2026' | relative_url }}): Targets advanced KeySwitch computation and the balance among inner products, NTT, and basis conversion. The linked page identifies its abstract as originating from an earlier preprint.
- [Alchemist · DAC 2024]({{ '/publications/DAC2024' | relative_url }}): Uses fine-grained Meta-OPs and slot-based data management to support arithmetic and logic workloads across FHE schemes.
- [Chimera · DAC 2026]({{ '/publications/DAC2026' | relative_url }}): Improves TFHE compatibility in a unified accelerator through dual-mode FFT/NTT computation, bootstrapping-key organization, and hardware-oriented KeySwitch support.
- [LP-HENN · Cybersecurity 2025]({{ '/publications/Cybersecurity2025-1' | relative_url }}): Combines a RISC-V vector coprocessor with ReRAM crossbars for low-power, energy-efficient FHE execution.
- [Bitwidth-Flexible Modular Multiplier · ISCAS 2026]({{ '/publications/ISCAS2026' | relative_url }}): Uses shift-free accumulation and parallel modular-reduction subcomputations to improve the arithmetic building blocks of NTT.
- [Karatsuba-Based Barrett Modular Multiplication · IEEE TCAD 2025]({{ '/publications/tcad2025' | relative_url }}): Studies Karatsuba evaluation and interpolation to improve modular-multiplication efficiency. The two similar TCAD titles in the presentation are represented here by the single corresponding paper currently listed on this website, rather than counted separately.
- [Binary Subscript Representation and Pipelined NTT · IEEE TCAD 2026]({{ '/publications/TCAD2026' | relative_url }}): Studies number representation and pipelined NTT as arithmetic foundations for efficient transform hardware.
- [Large-Bitwidth Modular Multiplication · ASP-DAC 2027]({{ '/publications/ASP-DAC2027' | relative_url }}): A related cryptographic-arithmetic study of pipelined Karatsuba multiplication. Its scope extends beyond FHE; the listed conference year is 2027.
- [FHE Chiplet Interconnection Optimization · CASES 2025]({{ '/publications/CASES2025' | relative_url }}): Jointly explores parameter selection, task mapping, and intra-/inter-chiplet network topology under cost and power constraints.

<p class="fhe-back"><a href="#top">Back to the top</a></p>

<h2 id="systems">4. Applications, Systems, and Supporting Tools: Capacity and End-to-End Latency</h2>

### Research Approach

Complex applications combine multiple bottlenecks. Encrypted LLMs require efficient linear computation and costly nonlinear operations, while encoded weights and evaluation keys may exceed GPU memory. We consider data representation, generation, placement, and communication scheduling together: compress repeated structure, generate plaintexts on demand, move key-intensive computation closer to storage, and balance load against communication across GPUs.

<figure class="fhe-figure">
<div class="fhe-art" style="aspect-ratio: 1248 / 245;"><img src="{{ '/images/fhe-system/research-atlas.png' | relative_url }}" style="top: 0; margin-top: -81.57051282051282%;" alt="Applications and heterogeneous systems: encrypted LLM inference supported by multiple GPUs and computational storage." loading="lazy" /></div>
<figcaption>Figure 5 · Application requirements guide device roles. Multi-GPU execution and computational storage are complementary research directions; the illustration does not imply that every result uses the same deployment.</figcaption>
</figure>

### Representative Results

- [WPC · CCS 2025]({{ '/publications/CCS2025' | relative_url }}): Uses periodic slot arrangements to compress encoded weights and reduce weight-plaintext storage for encrypted CNN inference. The compressed objects are encoded plaintext weights, rather than encrypted user inputs.
- [ROSETTA · CCS 2026]({{ '/publications/CCS2026' | relative_url }}): Targets autoregressive LLM decoding, selecting nonlinear implementations using complementary CKKS and TFHE capabilities to balance accuracy and latency.
- [LUTHE · MICRO 2026]({{ '/publications/MICRO2026-1' | relative_url }}): When evaluation keys exceed GPU memory, moves key-intensive primitives to a Computational Storage Drive (CSD) and pipelines them with compute-intensive primitives on the GPU.
- [HELM · HPCA 2027]({{ '/publications/HPCA2027-1' | relative_url }}): Combines on-demand plaintext generation, program-level optimization, and multi-GPU partitioning for homomorphic LLM inference. The paper page reports a 48.8-second time to first token for Llama3-8B with 128 input tokens on eight H20 GPUs, alongside a 96-fold storage reduction. These results apply to the reported model, input length, and hardware configuration. The listed conference year is 2027.

Prefill processes the input sequence, whereas decoding generates output tokens one at a time. Their parallelism, caching needs, and critical paths differ. HELM's system optimizations and ROSETTA's decoding optimizations should therefore be interpreted within their respective experimental settings; their speedups cannot simply be multiplied.

### Further Application and System Results

- [CipherPrune · ICLR 2025]({{ '/publications/ICLR2025' | relative_url }}): Reduces private Transformer inference work through encrypted token pruning and polynomial-degree reduction, combined with protocol-aware network optimization. This is application/protocol optimization for private inference, rather than a standalone FHE hardware accelerator.
- [HOLMES · PPoPP 2027]({{ '/publications/PPoPP2027' | relative_url }}): The paper “Accelerating Fully Homomorphic Encryption for Large Language Model Inference on Multi-GPU Systems” partitions complete LLM operations, co-models computation, memory, and communication, and pipelines execution to reduce imbalance. The listed conference year is 2027.
- [OmniCifro · IEEE TCAD 2026]({{ '/publications/TCAD2026-2' | relative_url }}): Combines a dedicated Homomorphic Processing Unit with processing-in-memory modules, mapping compute-intensive and memory-bound primitives to different resources.
- [Flagger · ISCA 2024]({{ '/publications/ISCA2024' | relative_url }}): Cooperatively uses a DPU and computational storage for large-scale cross-silo federated-learning aggregation protected by homomorphic encryption. This is an HE-enabled application system with a distinct workload from FHE LLM inference.
- [FHE from a Storage I/O Perspective · APPT 2025]({{ '/publications/APPT2025' | relative_url }}): Analyzes how storage traffic can undermine accelerator performance, motivating capacity-aware execution and system-level I/O optimization.

### Supporting Storage, Interconnect, and Simulation Research

These results, also represented in the presentation's system and tool categories, support the exploration of scalable heterogeneous systems. They are general infrastructure research, rather than direct measurements of FHE acceleration.

- [XHarvest · ISCA 2025]({{ '/publications/ISCA2025-3' | relative_url }}): Explores CXL-driven SSD architecture for high performance and cost efficiency, contributing storage-system design expertise.
- [LEGOSim · MICRO 2025]({{ '/publications/MICRO2025-2' | relative_url }}): Integrates heterogeneous chiplet simulators with adaptive synchronization and inter-chiplet network modeling for architectural design-space exploration.
- [Xerxes · FAST 2026]({{ '/publications/FAST2026' | relative_url }}): Models CXL-connected heterogeneous systems and interconnect behavior to explore scalable topologies and device interactions.
- [FCS · HPCA 2027]({{ '/publications/HPCA2027-2' | relative_url }}): Uses frontier-based commit-time synchronization to improve modular parallel simulation. This supports efficient system evaluation; the listed conference year is 2027.

<p class="fhe-back"><a href="#top">Back to the top</a></p>

<h2 id="outlook">Future Directions: Validating Full-Stack Gains in Complete Applications</h2>

Our next steps focus on building complex encrypted applications, improving single-device efficiency, and bringing tiered storage, I/O optimization, and heterogeneous scheduling into multi-device systems. Priorities include support for domestic computing platforms and toolchains, controlling the latency of GPU-memory spills, and choosing operator placement and dataflow to overlap communication with computation.

We assess progress through practical questions: Can the system accommodate larger models, reduce user waiting time, and run reliably at an affordable cost? Can developers reuse existing cryptographic libraries, compilers, and devices to build applications? Research across the stack ultimately needs to improve these end-to-end outcomes.

<div class="fhe-note" markdown="1">
This page draws on the November 22, 2026 presentation, “Full-Stack Collaboration and System Enablement: Explorations and Practice in Homomorphic Encryption Acceleration,” and this website's publication pages. The selected results have dedicated pages on this site and do not reproduce the presentation's full bibliography. See the linked papers for experimental parameters, baselines, and scope.
</div>

<p class="fhe-back"><a href="#top">Back to the top</a></p>

[Back to Research]({{ '/research/' | relative_url }}) · [Full Publication List]({{ '/publications/' | relative_url }})
