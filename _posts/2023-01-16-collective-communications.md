---
layout: post
title: Collective communications with MPI
---

## General concepts

* Collective communications allow making a series of point-to-point communications
in one single call.
* A collective communication always concerns all the processes of the indicated
communicator.
* For each process, the call ends when its participation in the collective call is completed, in the sense of point-to-point communications (therefore, when the
concerned memory area can be changed).
* The management of tags in these communications is transparent and system-dependent. Therefore, they are never explicitly defined during calls to subroutines. An advantage of this is that collective communications never interfere with point-to-point communications.

### Types of collective communications
1. One which ensures global synchronizations : `MPI_Barrier()`
2. Ones which only transfer data :
  * Global distribution of data : `MPI_Bcast()`
  *  Selective distribution of data : `MPI_Scatter()`
  *  Collection of distributed data : `MPI_Gather()`
  *  Collection of distributed data by all the processes : `MPI_Allgather()`
  *  Collection and selective distribution by all the processes of distributed data : `MPI_Alltoall()`
3. Ones which, in addition to the communications management, carry out operations
on the transferred data :
  * Reduction operations (sum, product, maximum, minimum, etc.), whether of a
predefined or personal type : `MPI_Reduce()`
  * Reduction operations with distributing of the result (this is in fact equivalent to an MPI_Reduce() followed by an MPI_Bcast() ) : `MPI_Allreduce()`
