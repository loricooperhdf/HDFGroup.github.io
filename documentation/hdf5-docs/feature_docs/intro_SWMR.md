---
title: Introduction to Single-Writer\_Multiple-Reader (SWMR)
redirect_from:

---

# Introduction to Single-Writer\_Multiple-Reader (SWMR)

Introduction to SWMR
The Single-Writer / Multiple-Reader (SWMR) feature enables multiple processes to read an HDF5 file while it is being written to (by a single process) without using locks or requiring communication between processes.



All communication between processes must be performed via the HDF5 file. The HDF5 file under SWMR access must reside on a system that complies with POSIX write() semantics.

The basic engineering challenge for this to work was to ensure that the readers of an HDF5 file always see a coherent (though possibly not up to date) HDF5 file.

The issue is that when writing data there is information in the metadata cache in addition to the physical file on disk: 

However, the readers can only see the state contained in the physical file:



The SWMR solution implements dependencies on when the metadata can be flushed to the file. This ensures that metadata cache flush operations occur in the proper order, so that there will never be internal file pointers in the physical file that point to invalid (unflushed) file addresses.

A beneficial side effect of using SWMR access is better fault tolerance. It is more difficult to corrupt a file when using SWMR.


Documentation
SWMR User's Guide

 PDF

HDF5 Library APIs
Page:
H5F_START_SWMR_WRITE — Enables SWMR writing mode for a file
Page:
H5DO_APPEND — Appends data to a dataset along a specified dimension
Page:
H5P_SET_OBJECT_FLUSH_CB — Sets a callback function to invoke when an object flush occurs in the file
Page:
H5P_GET_OBJECT_FLUSH_CB — Retrieves the object flush property values from the file access property list
Page:
H5O_DISABLE_MDC_FLUSHES — Prevents metadata entries for an HDF5 object from being flushed from the metadata cache to storage
Page:
H5O_ENABLE_MDC_FLUSHES — Enables flushing of dirty metadata entries from a file’s metadata cache
Page:
H5O_ARE_MDC_FLUSHES_DISABLED — Determines if an HDF5 object has had flushes of metadata entries disabled
Tools
Page:
h5watch — Outputs new records appended to a dataset as the dataset grows
Page:
h5format_convert — Converts the layout format version and chunked indexing types of datasets created with HDF5-1.10 so that applications built with HDF5-1.8 can access them
Page:
h5clear — Clears superblock status_flags field, removes metadata cache image, prints EOA and EOF, or sets EOA of a file
Design Documents
Error while fetching page properties report data:

Programming Model
Please be aware that the SWMR feature requires that an HDF5 file be created with the latest file format. See H5P_SET_LIBVER_BOUNDS for more information.

To use SWMR follow the the general programming model for creating and accessing HDF5 files and objects along with the steps described below.

SWMR Writer:
The SWMR writer either opens an existing file and objects or creates them as follows.

Open an existing file:

Call H5Fopen using the H5F_ACC_SWMR_WRITE flag.
Begin writing datasets.
Periodically flush data.
Create a new file:

Call H5Fcreate using the latest file format.
Create groups, datasets and attributes, and then close the attributes.
Call H5F_START_SWMR_WRITE to start SWMR access to the file.
Periodically flush data.
Example Code:

Create the file using the latest file format property:

   fapl = H5Pcreate (H5P_FILE_ACCESS); 
   status = H5Pset_libver_bounds (fapl, H5F_LIBVER_LATEST, H5F_LIBVER_LATEST); 
   fid = H5Fcreate (filename, H5F_ACC_TRUNC, H5P_DEFAULT, fapl); 
[Create objects (files, datasets, ...). Close any attributes and named datatype objects. Groups and datasets may remain open before starting SWMR access to them.]

Start SWMR access to the file:

   status = H5Fstart_swmr_write (fid);  
Reopen the datasets and start writing, periodically flushing data:

   status = H5Dwrite (dset_id, ...);
   status = H5Dflush (dset_id); 
SWMR Reader:
The SWMR reader must continually poll for new data:

 

Call H5Fopen using the H5F_ACC_SWMR_READ flag.
Poll, checking the size of the dataset to see if there is new data available for reading.
Read new data, if any.
Example Code:

Open the file using the SWMR read flag:

   fid = H5Fopen (filename, H5F_ACC_RDONLY | H5F_ACC_SWMR_READ, H5P_DEFAULT);
Open the dataset and then repeatedly poll the dataset, by getting the dimensions, reading new data, and refreshing:

   dset_id = H5Dopen (...);
   space_id = H5Dget_space (...);
   while (...) { 
      status = H5Dread (dset_id, ...);
      status = H5Drefresh (dset_id);
      space_id = H5Dget_space (...);
   }

Limitations and Scope
An HDF5 file under SWMR access must reside on a system that complies with POSIX write() semantics. It is also limited in scope as follows:

The writer process is only allowed to modify raw data of existing datasets by;

Appending data along any unlimited dimension.
Modifying existing data
The following operations are not allowed (and the corresponding HDF5 files will fail):

The writer cannot add new objects to the file.
The writer cannot delete objects in the file.
The writer cannot modify or append data with variable length, string or region reference datatypes.
File space recycling is not allowed. As a result the size of a file modified by a SWMR writer may be larger than a file modified by a non-SWMR writer.

Tools for Working with SWMR
Two new tools, h5watch and h5clear, are available for use with SWMR. The other HDF5 utilities have also been modified to recognize SWMR:

The h5watch tool allows a user to monitor the growth of a dataset.
The h5clear tool clears the status flags in the superblock of an HDF5 file.
The rest of the HDF5 tools will exit gracefully but not work with SWMR otherwise.

Programming Example
A good example of using SWMR is included with the HDF5 tests in the source code. You can run it while reading the file it creates. If you then interrupt the application and reader and look at the resulting file, you will see that the file is still valid. Follow these steps:

Download the HDF5-1.10 source code to a local directory on a filesystem (that complies with POSIX write() semantics). Build the software. No special configuration options are needed to use SWMR.

Invoke two command terminal windows. In one window go into the bin/ directory of the built binaries. In the other window go into the test/ directory of the HDF5-1.10 source code that was just built.

In the window in the test/ directory compile and run use_append_chunk.c. The example writes a three dimensional dataset by planes (with chunks of size 1 x 256 x 256).

In the other window (in the bin/ directory) run h5watch on the file created by use_append_chunk.c (use_append_chunk.h5). It should be run while use_append_chunk is executing and you will see valid data displayed with h5watch.

Interrupt use_append_chunk while it is running, and stop h5watch.

Use h5clear to clear the status flags in the superbock of the HDF5 file (use_append_chunk.h5).

View the file with h5dump. You will see that it is a valid file even though the application did not close properly. It will contain data up to the point that it was interrupted.
