---
title: New Features in HDF5 1.10
redirect_from:
  - display/HDF5/New+Features+in+HDF5+Release+1.10
---

# New Features in HDF5 1.10

HDF5 1.10 introduces several new features in the HDF5 library. These new features were added in the first three releases of HDF5-1.10. For a brief description of each new feature see:

* [New Features Introduced in HDF5 1.10.8](#new-features-introduced-in-hdf5-1.10.8)
* [New Features Introduced in HDF5 1.10.7](#new-features-introduced-in-hdf5-1.10.7)
* [New Features introduced in HDF5 1.10.6](#new-features-introduced-in-hdf5-1.10.6)
* [New Features introduced in HDF5 1.10.5](#new-features-introduced-in-hdf5-1.10.5)
* [New Features Introduced in HDF5 1.10.2](#new-features-introduced-in-hdf5-1.10.2)
* [New Features Introduced in HDF5 1.10.1](#new-features-introduced-in-hdf5-1.10.1)
* [New Features Introduced in HDF5 1.10.0](#new-features-introduced-in-hdf5-1.10.0)

~~~
This release includes changes in the HDF5 storage format. For detailed information on the changes, see: Changes to the File Format Specification

PLEASE NOTE that HDF5-1.8 cannot read files created with the new features described below that are marked with \*.

These changes come into play when one or more of the new features is used or when an application calls for use of the latest storage format (H5P_SET_LIBVER_BOUNDS). See the RFC for more details.

Due to the requirements of some of the new features, the format of a 1.10.x HDF5 file is likely to be different from that of a 1.8.x HDF5 file. This means that tools and applications built to read 1.10.x files will be able to read a 1.8.x file, but tools built to read 1.8.x files may not be able to read a 1.10.x file.

If an application built on HDF5 Release 1.10 avoids use of the new features and does not request use of the latest format, applications built on HDF5 Release 1.8.x will be able to read files the first application created. In addition, applications originally written for use with HDF5 Release 1.8.x can be linked against a suitably configured HDF5 Release 1.10.x library, thus taking advantage of performance improvements in 1.10.
~~~

### New Features Introduced in HDF5 1.10.8
The following important new features and changes were introduced in HDF5-1.10.8. For complete details see the Release Notes and the Software Changes from Release to Release page.

### New Features Introduced in HDF5 1.10.7
The following important new features and changes were introduced in HDF5-1.10.7. For complete details see the Release Notes and the Software Changes from Release to Release page.

Addition of AEC (open source SZip) Compression Library
HDF5 now supports building with the AEC library as a replacement library for SZip.

Addition of the Splitter and Mirror VFDs
Two VFDs were added in this release:

The Splitter VFD maintains separate R/W and W/O channels for "concurrent" file writes to two files using a single HDF5 file handle.
The Mirror VFD uses TCP/IP sockets to perform write-only (W/O) file I/O on a remote machine.
Improvements to Performance
Performance has continued to improve in this release. Please see the images under Compatibility and Performance Issues on the Software Changes from Release to Release page.

Addition of Hyperslab Selection Functions
Several hyperslab selection routines introduced in HDF5-1.12 were ported to 1.10. See the Software Changes from Release to Release page for details.
                                                                                                ### New Features Introduced in HDF5 1.10.6
The following important new features and changes were introduced in HDF5-1.10.6. For complete details see the Release Notes and the Software Changes from Release to Release page:

#### Improvements to the CMake Support
Several improvements were added to the CMake support, including:

Support was added for VS 2019 on Windows (with CMake 3.15).
Support was added for MinGW using a toolchain file on Linux (C only).
#### Virtual File Drivers - S3 and HDFS
Two Virtual File Drivers (VFDs) have been introduced in 1.10.6:

* The S3 VFD enables access to an HDF5 file via the Amazon Simple Storage Service (Amazon S3).
* The HDFS VFD enables access to an HDF5 file with the Hadoop Distributed File System (HDFS).

See the Virtual File Drivers - S3 and HDFS page for more information.

#### Improvement to Performance
Performance was improved when creating a large number of small datasets.

### New Features Introduced in HDF5 1.10.5
The following important new features were added in HDF5-1.10.5. Please see the release announcement and Software Changes from Release to Release page for more details regarding these features:

#### Minimized Dataset Object Headers (RFC)
The ability to minimize dataset object headers was added to reduce the file bloat caused by extra space in the dataset object header. The file bloat can occur when creating many, very small datasets. See the Release Notes for more details regarding this issue.

The following APIs were introduced to support this feature:

H5F_GET_DSET_NO_ATTRS_HINT

Retrieves the setting for determining whether the specified file does or does not create minimized dataset object headers
                                                                                                H5F_SET_DSET_NO_ATTRS_HINT

Sets the flag to create minimized dataset object headers

H5P_GET_DSET_NO_ATTRS_HINT

Retrieves the setting for determining whether the specified DCPL does or does not create minimized dataset object headers

H5P_SET_DSET_NO_ATTRS_HINT

Sets the flag to create minimized dataset object headers

#### Parallel Library Change (RFC)

A change was added to the default behavior in parallel when reading the same dataset in its entirety (i.e. H5S_ALL dataset selection) which is being read by all the processes collectively. The dataset must be contiguous, less than 2GB, and of an atomic datatype. The new behavior in the HDF5 library uses an MPI_Bcast to pass the data read from the disk by the root process to the remaining processes in the MPI communicator associated with the HDF5 file.

A CFD application was used to benchmark CGNS with:

* compact storage
* read-proc0-and-bcast

These results were reported by Greg Sjaardema from Sandia National Laboratories.

(image missing)

Series 1 is the read-proc0-and-bcast solution
Series 2 is a single MPI_Bcast
Series 3 uses multiple MPI_Bcast totaling 2 MiB total data 64 bytes at a time (IIRC)
Series 4 is unmodified CGNS develop
Compact is using compact storage
Compact 192 is also using compact storage
Compact 384 is also using compact storage
The last 3 "compact" curves are just three different batch jobs on 192, 384, and 552 nodes (with 36 core/node). The Series 2 and 3 curves are not related to the CGNS benchmark, but give a qualitative indication on the scaling behavior of MPI_Bcast. Both read-proc0-and-bcast and compact storage follow MPI_Bcast's trend, which makes sense since both methods rely on MPI_Bcast. (See the RFC for better resolution.)

#### OpenMPI Support
Support for OpenMPI was added. For known problems and issues please see OpenMPI Build Issues. To better support OpenMPI, all MPI-1 API calls were replaced by MPI-2 equivalents.

#### Chunk Query Functions (RFC)
New functions were added to find locations, sizes and filters applied to chunks of a dataset. This functionality is useful for applications that need to read chunks directly from the file, bypassing the HDF5 library.

H5D_GET_CHUNK_INFO  Retrieves information about a chunk specified by the chunk index
H5D_GET_CHUNK_INFO_BY_COORD Retrieves information about a chunk specified by its coordinates
H5D_GET_NUM_CHUNKS  Retrieves number of chunks that have nonempty intersection with a specified selection

### New Features Introduced in HDF5 1.10.2
Several important features and changes were added to HDF5 1.10.2. See the release announcement and blog for complete details. Following are the major new features:

#### Forward Compatibility for HDF5 1.8-based Applications Accessing Files Created by HDF5 1.10.2 ( RFC )
In HDF5 1.8.0, the H5P_SET_LIBVER_BOUNDS function was introduced for specifying the earliest ("low") and latest ("high") versions of the library to use when writing objects. With HDF5 1.10.2, new values for "low" and "high" were introduced: H5F_LIBVER_18 and H5F_LIBVER_LATEST is now mapped to H5F_LIBVER_V110. See the H5P_SET_LIBVER_BOUNDS function for details.

#### Performance Optimizations for HDF5 Parallel Applications
Optimizations were introduced to parallel HDF5 for improving the performance of open, close and flush operations at scale.


#### Using Compression with HDF5 Parallel Applications
HDF5 parallel applications can now write data using compression (and other filters such as the Fletcher32 checksum filter).


### New Features Introduced in HDF5 1.10.1

#### Metadata Cache Image ( RFC ) -> Fine-tuning the Metadata Cache *
HDF5 metadata is typically small, and scattered throughout the HDF5 file. This can affect performance, particularly on large HPC systems. The Metadata Cache Image feature can improve performance by writing the metadata cache in a single block on file close, and then populating the cache with the contents of this block on file open, thus avoiding the many small I/O operations that would otherwise be required on file open and close.

#### Metadata Cache Evict on Close -> Fine-tuning the Metadata Cache
The HDF5 library's metadata cache is fairly conservative about holding on to HDF5 object metadata (object headers, chunk index structures, etc.), which can cause the cache size to grow, resulting in memory pressure on an application or system. The "evict on close" property will cause all metadata for an object to be evicted from the cache as long as metadata is not referenced from any other open object.

#### Paged Aggregation ( RFC ) -> File Space Management *
The current HDF5 file space allocation accumulates small pieces of metadata and raw data in aggregator blocks which are not page aligned and vary widely in sizes. The paged aggregation feature was implemented to provide efficient paged access of these small pieces of metadata and raw data.

#### Page Buffering ( RFC )
Small and random I/O accesses on parallel file systems result in poor performance for applications. Page buffering in conjunction with paged aggregation can improve performance by giving an application control of minimizing HDF5 I/O requests to a specific granularity and alignment.




### New Features Introduced in HDF5 1.10.0

#### SWMR *
Data acquisition and computer modeling systems often need to analyze and visualize data while it is being written. It is not unusual, for example, for an application to produce results in the middle of a run that suggest some basic parameters be changed, sensors be adjusted, or the run be scrapped entirely.

To enable users to check on such systems, we have been developing a concurrent read/write file access pattern we call SWMR (pronounced swimmer). SWMR is short for single-writer/multiple-reader. SWMR functionality allows a writer process to add data to a file while multiple reader processes read from the file.

#### Fine-tuning the Metadata Cache
The orderly operation of the metadata cache is crucial to SWMR functioning. A number of APIs have been developed to handle the requests from writer and reader processes and to give applications the control of the metadata cache they might need. However, the metadata cache APIs can be used when SWMR is not being used; so, these functions are described separately.

#### Collective Metadata I/O
Calls for HDF5 metadata can result in many small reads and writes. On metadata reads, collective metadata I/O can improve performance by allowing the library to perform optimizations when reading the metadata, by having one rank read the data and broadcasting it to all other ranks.

#### Collective metadata I/O improves metadata write performance through the construction of an MPI derived datatype that is then written collectively in a single call.

#### File Space Management *
Usage patterns when working with an HDF5 file sometimes result in wasted space within the file. This can also impair access times when working with the resulting files. The new file space management feature provides strategies for managing space in a file to improve performance in both of these arenas.

#### Virtual Datasets (VDS) *
With a growing amount of data in HDF5, the need has emerged to access data stored across multiple HDF5 files using standard HDF5 objects, such as groups and datasets, without rewriting or rearranging the data. The new virtual dataset (VDS) feature enables an application to draw on multiple datasets and files to create virtual datasets without moving or rewriting any data.

#### Partial Edge Chunk Options *
New options for the storage and filtering of partial edge chunks in a dataset provide a tool for tuning I/O speed and file size in cases where the dataset size may not be a multiple of the chunk size.

#### Additional New APIs
In addition to the features described above, several additional new functions, a new struct, and new macros have been introduced or newly versioned in this release.

### Changes to the File Format Specification
The file format of the HDF5 library has been changed to support the new features in HDF5-1.10.

See the HDF5 File Format Specification for complete details on the changes. This specification describes how the bytes in an HDF5 file are organized on the storage media where the file is kept. In other words, when a file is written to disk, the file will be written according to the information described in this file. The following sections have been added or changed:

* Another version of the superblock was added.
* Additional B-tree types were added to the version 2 B-trees.
* The global heap block for virtual datasets was added.
* The Data Layout Message was changed: the name was changed, and version 4 of the data layout message was added for the virtual type.
* Additional types of indexes were added for dataset chunks.

HDF5-1.8 cannot read files created with the new features described on this page that are marked with *.
