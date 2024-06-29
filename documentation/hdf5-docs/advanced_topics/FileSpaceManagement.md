---
title: File Space Management
redirect_from:
  - display/HDF5/File%2BSpace%2BManagement
---

# File Space Management

This page briefly describes the documentation available to those who use the file space management feature found in the HDF5 library.

The HDF5 library's file space management activities encompass both the allocation of file space and the management of free space. When an HDF5 object (group, dataset, etc.) is created and written, file space is allocated for storing its metadata and raw data. When an object is removed, the space associated with the object becomes free space.

The following are the sections on this page:

<a href="#strategies">File Space Management Strategies</a>
<a href="#userguide">File Space Management User’s Guide</a>
<a href="#apis">HDF5 Library APIs</a>
<a href="#tools">Tools</a>
<a href="#bw-110-18">Differences between HDF5-1.10 and HDF5-1.8</a>
<a href="#removefspace">How to Remove the Free Space in an Existing File</a>

<h2 id="strategies"> File Space Management Strategies</h2>
The HDF5 library uses three mechanisms to manage space in an HDF5 file. They are:

Free-space managers that track free-space sections of various sizes in the file that are not currently allocated.
Aggregators, which are contiguous blocks of free space in the file.
Virtual file drivers, which use the virtual file driver interface to request additional space from the file driver associated with the file.
There are four file space-handling strategies available to users that use these mechanisms:

H5F_FSPACE_STRATEGY_FSM_AGGR
This strategy has always been available in HDF5 and is the default. The mechanisms used for this strategy are free-space managers, aggregators, and virtual file drivers.

H5F_FSPACE_STRATEGY_PAGE
The current HDF5 file space allocation accumulates small pieces of metadata and raw data in aggregator blocks. However, these blocks are not page aligned and vary widely in sizes. The paged aggregation feature provides efficient paged access of these small pieces of metadata and raw data. It accumulates metadata and raw data into well-aligned pages called file space pages. The library defines a default file space page size but a user can set the page size via a new public routine.

The mechanisms used for this strategy are free-space managers with embedded paged aggregation and virtual file drivers.

See the RFC on this feature for complete details.

H5F_FSPACE_STRATEGY_AGGR
With this strategy the library will request space from either the metadata or raw data aggregator depending on the file space type. If the request is not satisfied, the library will request space from the virtual file driver.

The mechanisms used for this strategy are aggregators and virtual file drivers. It does not use the free-space manager.

H5F_FSPACE_STRATEGY_NONE
This strategy will request space from the virtual file driver. The only mechanism used is the virtual file driver. It does not use the free-space manager.

<h2 id="userguide"> File Space Management User’s Guide</h2>
(This document is not yet available.)

<h2 id="apis"> HDF5 Library APIs</h2>
The APIs listed below from the HDF5 Reference Manual provide a means for users to directly manage the file space management feature.
 
|                   |                                                              |
| ----------------- | ------------------------------------------------------------ |
| [H5Fget_free_sections](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_f.html#gab9cbf1a45f9dcda34b43f985b7848434) | Retrieves free-space section information for a file |
| [H5Fget_freespace](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_f.html#ga3ef2673183567543346668a8f1eca2e9) | Returns the amount of free space in a file |
| [H5Fget_info2](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_f.html#gaced8c09c1559636a9c3f33dff3f4520e) | Returns global information for a file |
| [H5Pget_file_space_strategy](https://docs.hdfgroup.org/hdf5/v1_14/group___f_c_p_l.html#ga54cf6ca4f897ba9ee3695a15fe8e6029) | Retrieves the File Space Strategy for a file creation property list |
| [H5Pset_file_space_strategy](https://docs.hdfgroup.org/hdf5/v1_14/group___f_c_p_l.html#ga167ff65f392ca3b7f1933b1cee1b9f70) | Sets the File Space Strategy for a file creation property list |
| [H5Pget_file_space_page_size](https://docs.hdfgroup.org/hdf5/v1_14/group___f_c_p_l.html#gaab5e8c08e4f588e0af1d937fcebfc885) | Retrieves the file space page size for paged aggregation |
| [H5Pset_file_space_page_size](https://docs.hdfgroup.org/hdf5/v1_14/group___f_c_p_l.html#gad012d7f3c2f1e1999eb1770aae3a4963) | Sets the file space page size for paged aggregation |

<h2 id="tools"> Tools</h2>

The tools listed below have been modified to preserve or modify file freepace information appropriately when processing files employing this feature.

|             |                                                              |
| ----------- | ------------------------------------------------------------ |
| h5dump      | When printing the file creation property information for the superblock via the -B option, h5dump includes the block size obtained via H5Pget_file_space_page_size |
| h5stat      | When printing the file space information via the -S option, h5stat includes the block size obtained via H5Pget_file_space_page_size |
| h5repack    | The following options were added to h5repack: |
|             | -G FS_PAGESIZE,--fs_pagesize=FS_PAGESIZE enables the file space page size to be changed to FS_PAGESIZE |
|             | -P FS_PERSIST,--fs_persist=FS_PERSIST sets the persisting free space to persist (1) or to not persist (0) |
|             | -S FS_STRATEGY, --fs_strategy=FS_STRATEGY sets the file space management strategy |
|             | -T FS_THRESHOLD, --fs_threshold=FS_THRESHOLD sets the free-space section threshold |

<h2 id="bw-110-18"> Differences between HDF5-1.10 vs HDF5-1.8</h2>

### HDF5-1.10

File space management strategies were introduced via H5Pset_file_space_strategy to manage the unused space in a file.

While a file is open, HDF5 tracks and re-uses the unused space in the file according to the strategy used. If using a strategy that uses the free space manager, then free space can be tracked across file opens by use of the "persist" flag and a minimum free space threshold can be specified. If not specifying a strategy that uses the free space manager, then when the file is closed, any free space is lost and will remain in the file.

### HDF5-1.8

File space management only occurs between the HDF5 file open and close, and the free space is NOT tracked beyond file closed. In other words, when you delete a dataset, the space used by the dataset becomes free space that can be re-used as long as the file is open. Once the file is closed, the free space is lost and will remain in the file.

<h2 id="removefspace"> How to Remove the Free Space in an Existing File</h2>

The h5repack utility can be used to remove the unused space in a file, by writing the file to a new file. This utility comes with the HDF5 binary distribution.
