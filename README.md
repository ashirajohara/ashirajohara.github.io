# The Cache Coherency Chronicles 
**15-618 Spring 2026 Final Project** by **Ashira Johara (ajohara)** & **Caitlyn Fong (ckfong)** <br />

## Summary
In modern multicore CPU systems, where each processor core maintains a private cache, cache coherence becomes a critical challenge when the same memory block is shared between multiple caches. To study this problem, we will build upon an existing trace-driven cache simulator to implement multiple cache coherence protocols, including invalidation-based protocols and write-update-based protocols. Our project will systematically compare and evaluate these protocols across several dimensions in order to understand how different coherence strategies impact performance, coherence traffic, and scalability across diverse workloads. 

## Background
In maintaining memory consistency across multiple processing cores, our simulator will explore several Snoopy-based cache coherence paradigms. Snooping protocols rely on a shared communication medium, typically a bus, where all cache controllers can observe all memory transactions. When a core needs to read or write to a memory line it lacks, it broadcasts a request to all other cores. Under snooping-based cache coherence, there are two types of policies: 
1. Invalidation-Based Protocols<br />
Under a write-invalidate policy, such as the MESI protocol shown below, a core must obtain exclusive access to a cache line before modifying it. It does this by broadcasting an invalidation signal, forcing all other caches to mark their copies of the line as invalid.<br /> 
<img width="1116" height="802" alt="image" src="https://github.com/user-attachments/assets/755bbb4d-ce64-4890-998f-7d5eb9d89bf3" />
2. Update-Based Protocols<br />
Under a write-update policy, such as the Dragon protocol below, instead of invalidating shared copies upon a write, the modifying core broadcasts the updated data to all other caches holding that line. This keeps all shared copies perfectly synchronized and prevents read misses for other cores.<br />
<img width="869" height="561" alt="image" src="https://github.com/user-attachments/assets/0f3255e3-82e1-49dc-8d8b-ef164f75c034" />

## The Challenge 
1. Protocol Implementation: The biggest challenge in our project would be in implementing and adding each of the coherence protocols we outline below to the existing cache simulation framework. 
2. Analyzing Performance: In analyzing tradeoffs between coherence protocols, we have to understand how the underlying mechanisms of each protocol could impact its overall performance, generated coherence traffic, and scalability across diverse workloads.

## Resources
We will use Professor Railing’s [Computer Architecture Design Simulator for Students](https://github.com/bprail/cadss_public) (CADSS) from the 15-346 Computer Architecture: Design and Simulation course as a starting point, which already contains an implementation of the snoopy MI protocol. The starter code also contains multiple trace files for simple testing, as well as “task graphs”, which are more detailed traces.<br /> 
In implementing invalidation-based protocols (MI, MSI, MESI, MOESI, and MESIF), we aim to reference the cache coherency lectures (12, 13, 14) covered on the [15-618 course website](https://www.cs.cmu.edu/~418/schedule.html).<br />
In implementing write-update-based protocols (Dragon and Firefly), we aim to reference these papers: 
- [The Dragon Processor ](https://dl.acm.org/doi/10.1145/36206.36185)
- [Performance of the Firefly RPC](https://dl.acm.org/doi/10.1145/77648.77653)

## Goals and Deliverables 
[PLAN TO ACHIEVE] 
Our overarching objective is to holistically evaluate the performance, scalability, and bandwidth trade-offs of modern cache coherence design. We will achieve this through implementing various coherence protocols to the cache simulator corresponding to three primary comparative phases: 
1. Baseline Evaluation of Invalidate-Based Protocols: We will implement and compare classic write-invalidate protocols (MI, MSI, MESI, MOESI, and MESIF) to establish a baseline. We will evaluate how adding specific states (like Exclusive or Owned) reduces bus traffic under various sharing patterns. 
2. Invalidate vs. Write-Update Protocol Evaluation: We will compare our invalidate protocols with update-based protocols (Dragon and Firefly) to analyze bandwidth consumption and miss rates. 
To evaluate each of these protocols, we aim to run the set of traces, or, more specifically, task graphs, provided by the CADSS platform as benchmarks to measure the performance of each coherence protocol under varying workloads. We plan to analyze performance by measuring the following metrics for each protocol: 
- Number of total cache hits & misses
  - Number of coherence misses 
- Memory Latency (Average memory access time (AMAT)) 
- Coherence overhead (ratio of bus transactions due to control messages vs. data transfers) 
- Overall completion time (simulated number of clock cycles) 
- Scalability (changes in metrics above as number of processors increase)
We aim to answer the following overarching question:
What are the **performance tradeoffs** associated with each coherence paradigm, and how does this impact the performance of different workloads? 

## Platform Choice 
We aim to utilize Professor Railing’s [Computer Architecture Design Simulator for Students](https://github.com/bprail/cadss_public) (CADSS) as a baseline implementation for our cache coherence simulator. In running simulations and measuring performance, we will be using the GHC machines. 

## Schedule 
<br />Week 1 (March 25 - 28):<br /> 
1. Finalized project goals, implementation plans, and metrics for success. 
2. Set up Professor Railing’s CADSS infrastructure to successfully compile and run on the GHC machines.

<br />Week 2 (March 29 - April 4):<br /> 
1. Began implementing the classic write-invalidate protocols (MI, MSI, MESI, MOESI, and MESIF) to establish a baseline. 
2. Began writing additional traces to verify correctness and comprehensively test the invalidate-based protocols. 

Week 3 (April 5 - 11):<br /> 
1. Met with TA Helen to discuss our project schedule and gain a better understanding of Professor Railing’s CADSS infrastructure. 
2. Finished the following write-invalidate protocols: MI, MSI, and MESI. 
3. Wrote additional traces with 2, 4, and 8 processors that test a variety of sharing patterns for benchmarking. 

Week 4.0 (April 12 - 14):<br /> 
1. Finished implementation of MOESI and MESIF. 
* Milestone Report due April 14

Week 4.5 (April 15 - 18):<br /> 
1. Ashira: Begin implementation of the first write-update protocol, Dragon, which may include introducing additional signals, and supporting the broadcast of new data to other shared caches.
2. Caitlyn: Add in performance counters and investigate running the taskgraphs on the GHC machines. 

Week 5.0 (April 19 - 21):<br /> 
1. Caitlyn: Begin implementing the second write-update protocol, Firefly. 
2. Ashira: Compare and evaluate how adding specific states (like Exclusive or Owned) reduces bus traffic under various sharing patterns. 
<br />Week 5.5 (April 22 - 25):<br /> 
1. Ashira & Caitlyn: Perform invalidate vs. update comparisons by running write-heavy workloads on both MESI and the update protocols. 
2. Ashira & Caitlyn: Work on the final performance and measurement analysis for the final report. 
* File Report due April 30

