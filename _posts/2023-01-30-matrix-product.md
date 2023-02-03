---
layout: post
title: Matrix-matrix product in MPI
---

Dimension : $N \times N$  and $N_ L = \frac{N}{N _ \text{processes}}$ according to lines ands columns such that $N$ may be divisible by $N_ \text{processes}$
- Process $0$ initializes matrices $A$ and $B$ and scatter them to all processes
- Scatter of $A$ is done in line, scatter of $B$ is done in column
- 1. Each process sends his slice to the process `iter` & receives in `TEMP` the slice from the process `iter`. We use `MPI_Sendrecv()` 
- 2. Or each process sends his slice to the previous process & receives a slice from the next process. We may use `MPI_Sendrecv_replace()`
- Then each process computes the blocks upper and under the main diagonal line
- Finally, process $0$ gathers the slices from all processes to form the result
- Do not forget to release local tables
