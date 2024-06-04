---
title: Parallel HDF5
redirect_from:
  - display/HDF5/Parallel%2BHDF5
---

# Installation Instructions
Instructions for installing HDF5 can be found in the INSTALL_parallel file in the release_docs/ directory of the source code.

# Tutorials and Presentations
There are several HDF5 tutorials and presentations that will help in learning Parallel HDF5:

* [Learning the Basics](https://hdfgroup.github.io/hdf5/develop/_learn_basics.html)
: New users to HDF5 should work through this tutorial first. It does not cover parallel programming but contains basic information needed in order to use Parallel HDF5. For example, subsetting is not a parallel feature but it is commonly used in Parallel HDF5 and important to understand.

* [Introduction to Parallel HDF5](https://hdfgroup.github.io/hdf5/develop/_intro_par_h_d_f5.html)
: This tutorial is for users who are familiar with HDF5. It provides information on creating and writing to files with Parallel HDF5.

* Presentations:
: [Parallel HDF5 Short Course](HDF5-PARALLEL_ShortCourse.pdf)
: [Parallel HDF5 Performance Tuning](Parallel-HDF5-Performance-Tuning.pdf)
: [ECP Tutorial](20200206_ECPTutorial-final.pdf)

Users may also be interested in the [Introduction to Scientific I/O (PDF)](2016_NERSC_Introduction_to_Scientific_IO.pdf) tutorial provided by NERSC. It contains information on scientific I/O and parallel programming (which includes HDF5).

# Using Parallel HDF5
Further information on using Parallel HDF5 can be found here:

Frequently Asked Questions (under construction)
: These are questions that came from helping users.

[Collective Calling Requirements](CollectiveCallsInParallel.md) in Parallel HDF5 Applications
: This page contains information on how HDF5 functions must be called (collectively or independently) and properties used in Parallel HDF5.

# Information on Performance
Information on performance can be found in the following documents and frequently asked question:

### An I/O Study of ECP Applications ([blog](https://www.hdfgroup.org/2020/10/an-i-o-study-of-ecp-applications))
### Tuning HDF5 for Lustre File Systems ([PDF](howison_hdf5_lustre_iasds2010.pdf))
### Taming Parallel I/O Complexity with Auto-Tuning ([PDF](https://www.mcs.anl.gov/papers/P4091-0713_2.pdf))
### Hints to using Parallel HDF5 ([PDF](parallelhdf5hints.pdf))
### How to improve performance with Parallel HDF5

Tuning parallel HDF5 for a specific application on a specific system requires playing with a lot of tunable parameters many of which are specific to certain platforms. Not all hints are applicable to all platforms, and some hints may be ignored even if they can be applied. The best practice here is to look at each system's webpage on how to tune I/O parameters.

Here are some general parameters that users should consider tuning when they see slow I/O performance from HDF5:

***HDF5 parameters:***

  * Chunk size and dimensions: If the application is using chunked dataset storage, performance usually varies depending on the chunk size and how the chunks are aligned with block boundaries of the underlying parallel filesystem. Extra care must be taken on how the application is accessing the data to be able to set the chunk dimensions.

  * Metadata cache: it is usually a good idea to increase the metadata cache size if possible to avoid small writes to the file system. See: [H5P_SET_MDC_CONFIG](https://hdfgroup.github.io/hdf5/develop/group___f_a_p_l.html#gaf234199ad4cf9c708f45893f7f9cd4d3)

  * Alignment properties: For MPI IO and other parallel systems, choose an alignment which is a multiple of the disk block size. See: [H5P_SET_ALIGNMENT](https://hdfgroup.github.io/hdf5/develop/group___f_a_p_l.html#gab99d5af749aeb3896fd9e3ceb273677a)

***MPI-IO parameters:***

There are several MPI-I/O parameters to tune. Usually it is done by setting info keys in the info object passed to HDF5. Some implementations might allow other ways to pass those hints to the MPI library. The MPI standard reserves some key values. An implementation is not required to interpret these key values, but if it does interpret the key value, it must provide the functionality described. The best thing to do again here is to consult with the specific MPI implementation and system used documentation to see what parameters are available to tune. For example, ROMIO in MPICH provides a user guide with a section describing the hints that are available to tune:

[http://www.mcs.anl.gov/research/projects/romio/doc/users-guide.pdf](http://www.mcs.anl.gov/research/projects/romio/doc/users-guide.pdf)

Here are some general parameters that are usually tunable:

  * cb_block_size (integer): This hint specifies the block size to be used for collective buffering file access. Target nodes access data in chunks of this size. The chunks are distributed among target nodes in a round-robin (CYCLIC) pattern.

  * cb_buffer_size (integer): This hint specifies the total buffer space that can be used for collective buffering on each target node, usually a multiple of cb_block_size.

  * cb_nodes (integer): This hint specifies the number of target nodes to be used for collective buffering.

MPI implementations other than ROMIO might provide a way to tune those parameters, but not necessarily through info hints. OMPIO (an Open MPI native MPI-IO implementation) for example uses OMPI MCA parameters to tune those hints.

***Parallel File System parameters:***

Depending on the parallel file system and what version it is, there are several ways to tune performance. It is very hard to come up with a general list of tunable parameters for all file systems, since there are not many common ones. Users should individually check the documentation for the particular file system they are using.

For most parallel file systems the two parameters that are usually tunable and very important to consider are:

  * Stripe size: Controls the striping unit (in bytes).
  * Stripe Count: Controls the number of I/O devices to stripe across.

# PHDF5 Design Documents
Enabling a Strict Consistency Semantics Model in Parallel HDF5([PDF](https://docs.hdfgroup.org/hdf5/rfc/RFC%20PHDF5%20Consistency%20Semantics%20MC%20120328.docx.pdf))
