---
layout: post
title: Derived datatypes in MPI
---

The goal is to create more complex data structures by using different subroutines `MPI_Datatype`. Indeed, they are powerful data description portable mechanisms, they allow simplifying the writing of interprocess exchanges

*Contiguous* datatypes ($\neq$ Fortran) `MPI_Type_contiguous()`

*Homogenous* datatypes, separated by a constant stride in memory: `MPI_Type_vector()` in number of elements, `MPI_Type_create_hvector()` in number of bytes. See also indexed option `MPI_Type_indexed()`

*Commit derived* datatypes : commit `MPI_Type_commit()` and release (free) data `MPI_Type_free()`

*Size of a datatype* : `MPI_Type_size()` returns the number of bytes needed to send a datatype. This value ignores any holes present in the datatype.

*Extent of a datatype* : By default, it is the space in memory between the first and last component of a datatype i.e. the bounds included and with alignment considerations. We can modify the extent to create a new datatype by adapting the preceding one using `MPI_Type_create_resized()`. This provides a way to choose the stride between two successive datatype elements.

`MPI_Type_create_struct()` is useful for creating MPI datatypes corresponding to
Fortran derived datatypes or to C structures

`MPI_Get_address()` provides the address of a variable. It’s equivalent of & operator in C.
