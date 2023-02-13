---
layout: post
title: Communicators in MPI
---

*Aim*: to create subgroups on which we can carry out
operations such as collective or point-to-point communications. Each subgroup will
have its own communication space

#### Default communicator

- A *communicator* can only be created from another communicator. The first one will
be created from the `MPI_COMM_WORLD`.
- After the `MPI_Init()` call, a communicator is created for the duration of the
program execution.
- Its identifier `MPI_COMM_WORLD` is an integer value defined in the header files.
- This communicator can only be destroyed via a call to `MPI_Finalize()`.
- By *default*, therefore, it sets *the scope* of collective and point-to-point
communications *to include all the processes* of the application.

A *communicator* consists of :
- A *group*, which is an ordered group of processes.
- A communication *context* put in place by calling one of the communicator construction
subroutines, which allows determination of the communication space

#### Groups and communicators

- The communication contexts are managed by MPI (the programmer has no action
on them : It is a hidden attribute).
- In the MPI library, the following subroutines exist for the purpose of building
communicators : `MPI_Comm_create()` , `MPI_Comm_dup()` ,
`MPI_Comm_split()`
- The *communicator constructors* are *collective calls*.
- Communicators created by the programmer can be destroyed by using the
`MPI_Comm_free()` subroutine.

#### Partitioning of a communicator with `MPI_Comm_split()`

![image](https://user-images.githubusercontent.com/109908559/218407122-4ffde9dc-719a-4714-a8fb-69685dbace96.png)

#### Communicator built by defining a group of processes with `MPI_Comm_create()`
