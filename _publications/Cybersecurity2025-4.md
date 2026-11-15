---
title: "Corrosion Hammer: A Self-Activated Bit-Flip Attack to the Processing-In-Memory Accelerator"
collection: "publications"
permalink: "/publications/Cybersecurity2025-4"
venue: "CyberSecurity."
publication_year: 2025
citation: "<b>Corrosion Hammer: A Self-Activated Bit-Flip Attack to the Processing-In-Memory Accelerator</b>. ZIHAO YANG; Mengxin Zheng; Shengyu Fan; Qian Lou; Rui Hou; Dan Meng; Mingzhe Zhang. <i>CyberSecurity</i>."
---

## Abstract

The Resistive Random-Access-Memory (ReRAM) crossbar-based Processing-In-Memory (PIM) accelerator shows great promise in accelerating neural networks (NNs). This technique boasts low energy consumption and exceptional performance in multiplication and accumulations (MAC) operations, making ReRAM-based PIM accelerators an ideal solution for intelligent computing in wearable and low-power mobile devices. However, security concerns related to PIM have not been adequately addressed. In this paper, we present a new attack framework called SolutionName for ReRAM-based PIM accelerators. SolutionName builds upon the Bit Flip Attack (BFA), a weight modification attack that manipulates the NN function by flipping specific bits in the deployed quantized NN model. Unlike previous BFA methods that require explicit memory fault injection techniques, such as Row Hammer, to modify sensitive bits in the victim NN, SolutionName implants the trojan during the hardware-software co-design phase and flips sensitive bits using read disturbance. Read disturbance is a common noise in ReRAM caused by normal read operations. This approach enables the trojan to be activated quietly during normal use, eliminating the need for explicit attacks. Furthermore, we explore the impact of inputs on the activation time of the trojan and propose a method to expedite activation using normal input. Our experimental results demonstrate that SolutionName achieves an extremely covert trojan implantation and activation method, with an adversarial attack success rate of 94.38%. Additionally, with a specially designed method, the trojan activation can be accelerated on average by 61.98 \(\times \) , providing controllable activation.

[Abstract source](https://doi.org/10.1186/s42400-025-00513-y)

## Paper links

- [Official paper / download](https://doi.org/10.1186/s42400-025-00513-y)
- [Official PDF](https://link.springer.com/content/pdf/10.1186/s42400-025-00513-y.pdf)
