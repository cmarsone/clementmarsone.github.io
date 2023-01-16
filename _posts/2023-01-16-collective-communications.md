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
1. One which ensures global synchronizations : `int MPI_Barrier (MPI_Comm MPI_COMM_WORLD)`
2. Ones which only transfer data :
  * Global distribution of data : `int MPI_Bcast (void *buffer, int count, MPI_Datatype datatype, int root, MPI_Comm comm)`
  *  Selective distribution of data : `int MPI_Scatter (const void *sendbuf,int sendcount,
MPI_Datatype sendtype,void *recvbuf,
int recvcount,MPI_Datatype recvtype,
int root,MPI_Comm comm)`
  *  Collection of distributed data : `int MPI_Gather (const void*sendbuf,int sendcount,
MPI_Datatype sendtype,void *recvbuf,
int recvcount,MPI_Datatype recvtype,
int root,MPI_Comm comm)`
  *  Collection of distributed data by all the processes : `int MPI_Allgather (const void *sendbuf,int sendcount,
MPI_Datatype sendtype,void *recvbuf,
int recvcount,MPI_Datatype recvtype,
MPI_Comm comm`
  *  Collection and selective distribution by all the processes of distributed data : `int MPI_Alltoall (const void *sendbuf,int sendcount,
MPI_Datatype sendtype,void *recvbuf,
int recvcount,MPI_Datatype recvtype,
MPI_Comm comm)`
3. Ones which, in addition to the communications management, carry out operations
on the transferred data :
  * Reduction operations (sum, product, maximum, minimum, etc.), whether of a
predefined or personal type : `int MPI_Reduce (const void*sendbuf,void *recvbuf,int count,
MPI_Datatype datatype,MPI_Op op,int root,
MPI_Comm comm)`
  * Reduction operations with distributing of the result (this is in fact equivalent to an MPI_Reduce() followed by an MPI_Bcast() ) : `int MPI_Allreduce (const void *sendbuf,void *recvbuf,int count,
MPI_Datatype datatype,MPI_Op op,MPI_Comm comm)`
 
