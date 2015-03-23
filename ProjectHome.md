This package delivers the following four LDA training programs:
  1. single thread on single node
  1. multi-thread on single node
  1. single thread on multiple nodes
  1. multi-thread on multiple nodes  (multithreading + distributed computing)

The multi-threading functionality depends on OpenMP.  I tested this
functionality using GCC 4.2.1 on Mac OS X (Snow Leopard).

The multiple-node (distributed computing) functionality depends on
MPI.  I tested this functionality using MPICH2 on Snow Leopard, Ubuntu
and Cygwin (Windows XP).

The parallel algorithms implemented in this package can be found in
the following papers:

  * David Newman, Padhraic Smyth, Mark Steyvers, Scalable Parallel Topic Models, Journal of Intelligence Community Research and Development (2006).

  * David Newman, Arthur Asuncion, Padhraic Smyth, MaxWelling, Distributed Inference for Latent Dirichlet Allocation.  NIPS 2007.

This project is an enhancement to PLDA (code.google.com/p/plda) in terms of multi-threading.

Updated [26, 2010](March.md): Now this project has a sister project: http://http://code.google.com/p/lda-go, which is a copy of this project, but written in Google's Go programming language.