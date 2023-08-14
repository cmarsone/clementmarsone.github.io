---
layout: post
title: PDC Summer School | Parallel Computer Architectures
---

## Introduction to computer systems

*Main keywords*: CPUs, memory, caching, accelerators…

*Main goals*: precision, scale, range, datatypes, high performance, energy consumption, speed-up….

### Computing machines

- A mix of hardwares & softwares systems used to execute applications

### Computer architecture representation

- HPC makes extensive use of the computer systems

### Representation of the data

- Bits & bit vectors representation
- Interpretation & datatypes
- Careful to correctness, performance & efficiency

### Processor’s basic operations & inner workings

- CPU executes the application (execution progress PC), fetches Instructions & data, ALU operations& manage results
- Memory stores, receives by adresses, & replies with data (bit vector)
- Bus facilitates information of bits movement

### Memory 

Organised as linear spaces with word-size granularity 
Code & data stored as address
Memory operation are slow: off-chip, read/write operations, s

### CPU-memory gap

Flat memory Model
- All accesses with same latency
- Memory latency slower to improve than processor speed 
- Which leans we wait longer for DRAM access

Memory hierarchy: registers, L1, SRAM, DRAM, local disks, remote secondary storage… multiple layers of memory from small & fast to large slow

Cache: a smaller, faster storage device that acts as a staging area fora subset of the date in a larger slower device

Locality principle: programs tend to use data & instructions with addresses near or equal to those they have used recently.
Temporal & spatial locality

Problems of size for every memory address, organisation loading & policies
Performance of hit, miss, metric (accesses, fails, penalties…)

Core i7 matrix multiply performance (see below)

## ￼Parallelism & parallel machines

First taxonomy (classification): Michael Flynn of 1966
Single/Multiple = Instructions/Data

Moore’s Law predicts that the transistor density of semiconductor chips double roughly every 18 months

Around 2005: “hitting the walls” for clock speed, power

CPUs levels of parallelism
=> Instruction-Level Parallelism, SIMD Data Parallelism (fine), Multi-Core Task/DataParallelism (coarse)

Multi-core CPUs

￼
- Hardware threads, SIMD units (vector lanes)
- L1& L2 dedicated caches (individual)
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
