---
layout: post
title: PDC Summer School | Parallel Computer Architecture
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

https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.researchgate.net%2Ffigure%2FFlynns-Taxonomy-of-Computer-Architectures-13_fig1_268011284&psig=AOvVaw3CLLvIA_OEsc36O7wlEuo_&ust=1692115160919000&source=images&cd=vfe&opi=89978449&ved=0CBEQjRxqFwoTCMCgvq_C3IADFQAAAAAdAAAAABAD![image](https://github.com/cmarsone/cmarsone.github.io/assets/109908559/732de32a-33e1-4e0f-a2f9-525665f428fc)

*Moore’s law* predicts that the transistor density of semiconductor chips double roughly every 18 months
However around 2005: “hitting the walls” for clock speed, power...

*CPUs levels of parallelism* => Instruction-Level Parallelism, SIMD Data Parallelism (fine), Multi-Core Task/DataParallelism (coarse)

## Multi-core CPUs

- Hardware threads, SIMD units (vector lanes)
- L1 & L2 dedicated caches (individual)
- L3 shared cache (shared)
- Main memory, I/O (off-chip)

1. ILP: multiple instructions executed in the same cycle. Gaining parallelism but needing independent task. Implementing by super-scalar processors with dynamic scheduling (most of CPUs) & VLIW (Very Long Instruction Word) processors with static scheduling (most of GPUs)
2. SIMD: same instruction executed on multiple data items. Scalar=sequential & vector=parallel. Compiler directives of auto-vectorisation typically enabled with “-O” flag.
3. Multi-Core: concurrent tasks to be executed in parallel
4. Many-Cores GPUs: GPUs act as accelerators and depend on the CPU. Texture Processor Cluster = group of Streaming Multi-Processor (SM) = CUDA cores + special function units + local memory. GPU integration with PCI Express or NVLink (10x faster)

AMD:
- Much better perf
- Poorer software, a lot less libraries , small community effort

Arm:
- Low power devices mobile platforms
- Lower performances
Intel:
- Support processors with graphics integrated
All are programmed with OpenCL
“OpenCL (Open Computing Language) is a framework for writing programs that execute across heterogeneous platforms consisting of central processing units (CPUs), graphics processing units (GPUs), digital signal processors (DSPs), field-programmable gate arrays (FPGAs) and other processors or hardware accelerators.”

Fundamental difference latency/throughput
CPU: low latency, high flexibility, excellent for irregular codes with limited parallelism. Smallest time to execute one operation
GPU: high throughput. Excellent for massively parallel workloads. Max operations at the same time

Putting all together: multiple nodes, communication network, homogenous/heterogenous, peak performances, energy consumption, measurements 

Supercomputers: distributed combinations of multi-core & many-cores where we have to understand architectures. 
