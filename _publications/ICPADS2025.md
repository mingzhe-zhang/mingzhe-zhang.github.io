---
title: "Analysis of Bit-Flip Attacks on Encrypted Neural Networks"
collection: "publications"
permalink: "/publications/ICPADS2025"
venue: "31st IEEE International Conference on Parallel and Distributed Systems. ICPADS 2025"
publication_year: 2025
citation: "<b>Analysis of Bit-Flip Attacks on Encrypted Neural Networks</b>. Zihao Yang, Yilan Zhu, Rui Hou, Dan Meng, Shengyu Fan, Mingzhe Zhang. <i>31st IEEE International Conference on Parallel and Distributed Systems</i>. <b>ICPADS 2025</b>"
---

## Abstract

With the swift progression of artificial intelligence and deep learning, neural networks have achieved remarkable success in domains such as image recognition, natural language processing, and autonomous driving. However, the proliferation of data scales and the extensive deployment of computational resources have engendered significant privacy concerns for users. In scenarios involving personal sensitive data, the safeguarding of privacy is of utmost importance. Homomorphic encryption technology, particularly the CKKS scheme, is capable of performing computations with minimal computational error while preserving data privacy, and it has been extensively utilized in encrypted neural networks. This paper studies Bit-Flip Attacks (BFAs) on encrypted neural networks under the RNS-CKKS scheme. We empirically analyze the effects of bit flips at different memory locations—covering ciphertext data, model weights, and evaluation keys—and report their observable outcomes (silent misclassification, irregular yet decodable outputs, or computation aborts). Under a realistic threat model where the adversary cannot precisely target bytes nor observe model predictions, BFAs can corrupt results but do not leak additional information. Our findings indicate that key corruption often produces conspicuous anomalies that offer detection potential for defenders.

[Abstract source](https://doi.org/10.1109/icpads67057.2025.11322962)

## Paper links

- [Official paper / download](https://doi.org/10.1109/icpads67057.2025.11322962)
