---
layout: post
title: PDC Summer School | Multithreading & Parallel Computer Architecture
---

## Introduction to computer systems

*Main keywords*: CPUs, memory, caching, accelerators…

*Main goals*: precision, reliability, large-scalability, efficiency, higher performance & speed-up, energy consumption...

### Computing machines

*Computer systems*: A mix of hardwares & softwares systems used to execute applications.

### Computer architecture representation

- HPC makes extensive use of the computer systems with parallelism

### Representation of the data

- Bits & bit vectors representation
- Interpretation of data & datatypes
- Ensuring correctness, performance & efficiency

### Processor’s basic operations & inner workings

- *CPU* executes the application (execution progress), fetches instructions & data, computes ALU operations & manages results
- *Memory* stores, receives by adresses, & replies with data i.e. a bit vector
- *Bus* facilitates information of bits movement between components

### Memory 

- Organized as linear spaces with word-size granularity 
- Code & data are stored as address
- Memory operations are slow e.g off-chip, read/write operations & fetching...

### CPU-memory gap

*Flat memory model*:
- All accesses = same latency
- Memory latency slower to improve, than processor speed 
- Which means that we are waiting longer for any DRAM access

*Memory hierarchy*: registers, L1, L2, L3, SRAM, DRAM, local disks, remote secondary storage… 
- Multiple layers of memory from small & fast to large & slow

*Cache*: a smaller, faster storage device that acts as a staging area for a subset of the date in a larger slower device.

*Locality principle*: programs tend to use data & instructions with addresses near or equal to those they have used recently.
Locality can be *temporal* in the sucession of operations or *spatial* in the order of addresses.

- Problems of size for every memory address, organisation loading & policies
- Hit: access found data in fast memory.
- Miss: data not found in fast memory causing high latency & penalty.
- Metric: fraction of accesses that hit.

Memory allocations & operations are the main bottleneck in HPC today. Needing to improve locality with better data memory layout & access patterns

Core i7 Matrix Multiply Performances (see below)

![url](https://github.com/cmarsone/cmarsone.github.io/assets/109908559/3d6f5d42-19e0-4fe2-be25-8f15e9bbc712)

## ￼Parallelism & parallel machines

First taxonomy (classification) introduced by Michael Flynn in 1966
Single/Multiple = Instructions/Data

![image](https://github.com/cmarsone/cmarsone.github.io/assets/109908559/732de32a-33e1-4e0f-a2f9-525665f428fc)

*Moore’s law* predicts that the transistor density of semiconductor chips double roughly every 18 months
However around 2005: “hitting the walls” for clock frequency, power...

*CPUs levels of parallelism* => Instruction-Level Parallelism, SIMD Data Parallelism (fine), Multi-Core Task/DataParallelism (coarse), Heterogeneous computing

## Multi-core CPUs

- Hardware threads, SIMD units (vector lanes)
- L1 & L2 dedicated caches (individual)
- L3, Last-Level Cache - LLC (shared)
- Main memory, I/O (off-chip)

1. *ILP*: multiple instructions executed in the same cycle. Gaining parallelism but needing independent task. Implementing by super-scalar processors with dynamic scheduling (most of high-end CPUs) & VLIW (Very Long Instruction Word) processors with static scheduling (most of GPUs). *Features of modern CPUs*: Pipelining, superscalar (multiple instructions in one cycle) & out-of-order (reordering operations in hardware) spaculative execution, branch prediction...
2. Streaming *SIMD* Extension (SSE): same instruction executed on multiple data items by special registers & functional units. Scalar=sequential & vector=parallel. Compiler directives of auto-vectorization typically enabled with “-O” flag. Assembly instructions
3. *Multi-core parallelism*: different streams of instructions to be executed in parallel as software threads.
4. *Many-Cores GPUs*: GPUs act as accelerators and depend on the CPU. Texture Processor Cluster = group of Streaming Multi-Processor (SM) = CUDA cores + special function units + local memory. Warps = pieces of data at a time that can be concurrently processed by a core. GPU integration with PCI Express or NVLink (10x faster). Graphics & textures processing clusters.

*Hardware supported multi-threading*. Cores manages thread context:
- Interleaved, temporal multi-threading - employed in GPUs to hide the latency of stalls
- Simultaneous co-located execution e.g. Intel Hyperthreading

Requires replication of register file but increases throughput

*Using intrinsics refers to utilizing specialized instructions provided by the CPU's instruction set architecture to perform specific operations directly in code, often at a lower level than standard high-level programming constructs. Intrinsics allow programmers to take advantage of hardware-specific optimizations and capabilities for improved performance in applications such as multimedia processing, cryptography, signal processing, and more.* => Intel AVX

*AMD*:
- Much better perfs
- Poorer software drivers, a lot less libraries & tools, smaller community effort
  arm*:
- Low-power devices, mostly mobile platforms
- Lower perfs
*Intel*:
- Support own CPUs with integrated graphics
All are programmed in a similar way with OpenCL & have similar architecture.

*“OpenCL (Open Computing Language) is a framework for writing programs that execute across heterogeneous platforms consisting of central processing units (CPUs), graphics processing units (GPUs), digital signal processors (DSPs), field-programmable gate arrays (FPGAs) and other processors or hardware accelerators.”*

*Fundamental difference latency/throughput*

CPU: low latency, high flexibility, excellent for irregular codes with limited parallelism. Smallest time to execute one operation

GPU: high throughput. Excellent for massively parallel workloads. Max operations at the same time

*Putting all together*: multiple nodes, communication network, homogenous/heterogenous, peak performances, energy consumption, measurements 

### Scaling out

*Supercomputers*: distributed combinations of multi-core & many-cores where we have to understand architectures.

### Parallel Systems Models

### Shared Memory
- Multiple compute nodes
- One single shared address space, typical example of multi-cores

### Distributed Memory
- Multiple compute nodes
- Multiple, local (disjoint) address spaces
- Virtual shared memory: software/hardware layer “emulates” shared memory, typical example of clusters

### Hybrids
- Multiple compute nodes, typically heterogeneous
- Mixed address space(s), some shared, some global memory, typical example: supercomputers

### Major issues

*Shared Memory model*: Scalability problems (interconnect) & Programming challenge: RD/WR Conflicts

*Distributed Memory model*: Data distribution is mandatory & Programming challenge: remote accesses, consistency

*Virtual Shared Memory model*: Significant virtualization overhead • Easier programming

*Hybrid models*: Local/remote data more difficult to trace

--------------------------------------------------------------

The Translation Lookaside Buffer (TLB) is a hardware memory management component used in computer systems, specifically in modern CPUs, to improve the efficiency of virtual memory operations. Virtual memory is a memory management technique that allows an operating system to use more memory than is physically available by utilizing a combination of physical RAM and disk storage.

In a virtual memory system, each program or process running on the computer has its own virtual address space, which is divided into smaller units called pages. These virtual pages are mapped to physical pages in the computer's actual RAM. The TLB acts as a cache for the page table, which is a data structure used by the CPU to perform the mapping between virtual addresses and physical addresses.

When a program accesses a memory location, the CPU first checks the TLB to see if the virtual-to-physical mapping is already present. If it is, this is known as a TLB hit, and the physical address is directly used to access the data in RAM. If the mapping is not in the TLB (a TLB miss), the CPU must consult the full page table stored in main memory to find the correct physical address. This process, known as a page table walk, is slower than a TLB hit due to the additional memory accesses involved.

The TLB helps to reduce the latency of memory accesses by storing frequently used virtual-to-physical mappings, thereby speeding up the translation process. It is a critical component for achieving efficient virtual memory management and improving overall system performance. However, the TLB's effectiveness can be affected by factors such as TLB size, replacement policies, and the access patterns of running programs.

A Memory Ordering Buffer (MOB) is a component in modern processors designed to manage and enforce the order of memory operations within a multi-core or multi-threaded environment. It plays a crucial role in maintaining memory consistency and ensuring that the results of memory operations are observed by different threads or cores in a predictable and coherent manner.

In a multi-core or multi-threaded system, different processor cores or threads can execute instructions concurrently and access shared memory locations. Ensuring that memory operations from different cores or threads are observed in a consistent order is essential to prevent issues like data races, where concurrent memory accesses can lead to unpredictable and incorrect behavior.

The MOB helps manage memory operations by temporarily storing memory requests or instructions issued by different cores or threads. It ensures that memory operations from different sources are executed and observed in a way that respects their original program order. This includes enforcing the order of reads and writes to memory locations to prevent situations where the results of memory operations appear out of order.

The MOB works in conjunction with the memory subsystem, which includes caches, memory controllers, and memory modules. It helps to ensure that memory operations are properly coordinated and that the memory hierarchy's performance characteristics are maintained while still adhering to the desired memory ordering semantics.

In summary, the Memory Ordering Buffer is a hardware component that helps maintain memory consistency and order within a multi-core or multi-threaded processor, ensuring that memory operations from different sources are observed in a predictable and coherent manner to avoid data inconsistencies and preserve the integrity of program execution
