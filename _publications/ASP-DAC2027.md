---
title: "Investigation of Karatsuba Algorithm for Large-Bitwidth Modular Multiplication"
collection: "publications"
permalink: "/publications/ASP-DAC2027"
venue: "Asia and South Pacific Design Automation Conference"
publication_year: 2027
citation: "<b>Investigation of Karatsuba Algorithm for Large-Bitwidth Modular Multiplication</b>. Bo Zhang, Xiaoyi Ye, Mingyu Gao, Mingzhe Zhang, Shoumeng Yan. <i>Asia and South Pacific Design Automation Conference</i>. <b>ASP-DAC 2027</b>."
---

## Abstract

As a fundamental primitive operation in contemporary cryptographic protocols, such as zero-knowledge proofs, elliptic curve cryptography, and Rivest–Shamir–Adleman, it is desirable to develop an efficient design for large-bitwidth modular multiplication. We present an efficient design, in which the pipelined data flow shortens the critical path, and the $$k$$-term Karatsuba algorithm reduces cycles from $$k^2$$ to $$T^{(k)}$$, which is close to $$k^{\log_2(3)}$$.

Represented by a matrix pair $$(E^{(k)}, I^{(k)})$$, the Karatsuba algorithm also brings unexpected overhead from the extra evaluation and interpolation phases. We first propose efficient $$k$$-term Karatsuba algorithms when $$k$$ is a power-of-two. The uniform sign of all columns of $$E^{(k)}$$ and $$I^{(k)}$$ removes most of the negation logic. Later, an efficient row-based mechanism is proposed to process all rows of $$I^{(k)}$$ in a multiple cycle manner. The redundant computations for constant 0 are eliminated. The bitwidth of intermediate results roughly reduces by a factor of $$k$$. Rigorous proof allows us to accumulate intermediate results through compression, rather than the more complex addition. As such, experimental results demonstrate 24.12% and 38.99% savings in area/throughput, when compared with the state-of-art 1024-bit and 2048-bit designs.
