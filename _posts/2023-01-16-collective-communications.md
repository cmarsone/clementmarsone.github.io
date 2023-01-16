---
layout: post
title: Collective communications with MPI
---

## General concepts

* Collective communications allow making *a series of point-to-point communications* in one single call. It always concerns all the processes of the indicated communicator.
* For each process, *the call ends when its participation in the collective call is completed*. The management of tags in these communications is transparent and system-dependent. Therefore, they are never explicitly defined during calls to subroutines. An advantage of this is that *collective communications never interfere with point-to-point communications*.

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
  * Reduction operations with distributing of the result. It is equivalent to a reduce followed by a broadcast : `MPI_Allreduce()`

## Communication modes

* *Point-to-Point send modes* : Standard `MPI_Send()`, Synchronous `MPI_Ssend()`, Buffered `MPI_Bsend()`
* *Blocking call* : A call is blocking if the memory space used for the communication can be reused immediately after the exit of the call. The data sent can be modified after the call & the data received can be read after the call.
* *Synchronous send* : A synchronous send involves a synchronization between the involved processes i.e. send cannot start until its receive is posted. There can be no communication before the two processes are ready to communicate. ⚠ to the deadlocks !
* *Buffered sends* : The program can send multiple packets of data from the buffer at once, rather than sending them one at a time. A buffered send implies the copying of data into an intermediate memory space. There is then no coupling between the two processes of communication. Therefore, the return of this type of send is optional & does not mean that the receive has occurred. 
* *Non-blocking communication* : A non-blocking call returns very quickly but it does not authorize the immediate re-use of the memory space which was used in the communication. Before using it again, it is necessary to make sure that the communication is fully completed before using it again, with `MPI_Wait()` for instance.
* *One-Sided communications* or Remote Memory Access consists of accessing the memory of a distant process in read or write without the distant process having to manage this access explicitly. The target process does not intervene during the transfer.
