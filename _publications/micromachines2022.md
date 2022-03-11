---
title: "Application-Oriented Data Migration to Accelerate In-Memory Database on Hybrid Memory"
collection: publications
permalink: /publications/micromachines2022
venue: "Micromachines"
date: 2021-12-29
citation: '<b>Application-Oriented Data Migration to Accelerate In-Memory Database on Hybrid Memory</b>. Wenze Zhao, Yajuan Du, <b>Mingzhe Zhang</b>, Mingyang Liu, Kailun Jin, Rachata Ausavarungnirun. <i>Micromachines</i>.'
---

## Abstract
With the advantage of faster data access than traditional disks, in-memory database systems, such as Redis and Memcached, have been widely applied in data centers and embedded systems. The performance of in-memory database greatly depends on the access speed of memory. With the requirement of high bandwidth and low energy, die-stacked memory (e.g., High Bandwidth Memory (HBM)) has been developed to extend the channel number and width. However, the capacity of die-stacked memory is limited due to the interposer challenge. Thus, hybrid memory system with traditional Dynamic Random Access Memory (DRAM) and die-stacked memory emerges. Existing works have proposed to place and manage data on hybrid memory architecture in the view of hardware. This paper considers to manage in-memory database data in hybrid memory in the view of application. We first perform a preliminary study on the hotness distribution of client requests on Redis. From the results, we observe that most requests happen on a small portion of data objects in in-memory database. Then, we propose the Application-oriented Data Migration called ADM to accelerate in-memory database on hybrid memory. We design a hotness management method and two migration policies to migrate data into or out of HBM. We take Redis under comprehensive benchmarks as a case study for the proposed method. Through the experimental results, it is verified that our proposed method can effectively gain performance improvement and reduce energy consumption compared with existing Redis database.