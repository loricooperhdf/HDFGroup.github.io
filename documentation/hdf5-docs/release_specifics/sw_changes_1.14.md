---
title: Software Changes from Release to Release for HDF5 1.14
redirect_from: 
  - /display/HDF5/Software+Changes+from+Release+to+Release+for+HDF5+1.14
---

# Software Changes from Release to Release in HDF5 1.14

## API Compatibility

See [API Compatibility Macros](api_comp_macros.html) in HDF5 for details on using HDF5 version 1.14 with previous releases.

* [Compatibility report for Release 1.14.3 versus Release 1.14.2](https://htmlpreview.github.io/?https://raw.githubusercontent.com/HDFGroup/hdf5doc/master/html/ADGuide/Compatibility_Report/hdf5-1.14.2-vs-hdf5-1.14.3-interface_compatibility_report.html)

* [Compatibility report for Release 1.14.2 versus Release 1.14.1](https://htmlpreview.github.io/?https://raw.githubusercontent.com/HDFGroup/hdf5doc/master/html/ADGuide/Compatibility_Report/hdf5-1.14.1-2-vs-hdf5-1.14.2-interface_compatibility_report.html)

* [Compatibility report for Release 1.14.1 versus Release 1.14.0](https://htmlpreview.github.io/?https://raw.githubusercontent.com/HDFGroup/hdf5doc/master/html/ADGuide/Compatibility_Report/hdf5-1.14.0-vs-hdf5-1.14.1-interface_compatibility_report.html)

* [Compatibility report for Release 1.14.0 versus Release 1.12.2](https://htmlpreview.github.io/?https://raw.githubusercontent.com/HDFGroup/hdf5doc/master/html/ADGuide/Compatibility_Report/hdf5-1.12.2-vs-hdf5-1.14.0-interface_compatibility_report.html)

 
This page provides information on the changes that a maintenance developer needs to be aware of between successive releases of HDF5, such as:

New or changed features or tools
Syntax and behavioral changes in the existing application programming interface (the API)
Certain types of changes in configuration or build processes
Note that bug fixes and performance enhancements in the C library are automatically picked up by the C++, Fortran, and Java libraries.

The following information is included below.

* <a href="#4versus3">Release 1.14.4 versus Release 1.14.3</a>
* <a href="#3versus2">Release 1.14.3 versus Release 1.14.2</a>
* <a href="#2versus1">Release 1.14.2 versus Release 1.14.1</a>
* <a href="#1versus0">Release 1.14.1 versus Release 1.14.0</a>
* <a href="#0versus12\_2">Release 1.14.1 versus Release 1.12.2</a>

The release notes also list changes made to the library, but these notes tend to be more at a more detail-oriented level. The release notes may include new features, bugs fixed, supported configuration features, platforms on which the library has been tested, and known problems. The release note files are listed below and can be found at the top level of the HDF5 source code tree in the release\_docs directory.

<h2 id="4versus3">Release 1.14.4 versus Release 1.14.3</h2>
<h2 id="3versus2">Release 1.14.3 versus Release 1.14.2</h2>

<h2 id="2versus1">Release 1.14.2 versus Release 1.14.1</h2>

This section lists interface-level changes and other user-visible changes in behavior in the transition from HDF5 Release 1.14.1 to Release 1.14.2.

### New and Changed Functions, Classes, Subroutines, Wrappers, and Macros
Following are the new APIs introduced in HDF5-1.14.2.

#### In the C Interface (main library)

| Function                           | Description                                                  |
| ---------------------------------- | ------------------------------------------------------------ |
| H5FDread\_from\_selection          | Performs a series of scalar reads.
| H5FDread\_vector\_from\_selection  | Performs a vector read if vector reads are supported, or a series of scalar reads, otherwise.
| H5FDwrite\_from\_selection         | Performs a series of scalar writes.
| H5FDwrite\_vector\_from\_selection | Performs a vector write if vector writes are supported, or a series of scalar writes, otherwise.
| H5Pget\_fapl\_ros3\_token	         | Returns session/security token of the ros3 file access property list
| H5Pset\_fapl\_ros3\_token	         | Modifies the file access property list to use the H5FD\_ROS3 driver


<h2 id="1versus0">Release 1.14.1 versus Release 1.14.0</h2>
This section lists interface-level changes and other user-visible changes in behavior in the transition from HDF5 Release 1.14.0 to Release 1.14.1.

### New and Changed Functions, Classes, Subroutines, Wrappers, and Macros
Following are the new APIs introduced in HDF5-1.14.1.

#### In the C Interface (main library)

H5PGET\_MODIFY\_WRITE\_BUF
Retrieves the "modify write buffer" property
H5PGET\_NO\_SELECTION\_IO\_CAUSE	Retrieves the cause for not performing selection or vector I/O on the last parallel I/O call
H5PGET\_SELECTION\_IO	Retrieves the selection I/O mode
H5PSET\_MODIFY\_WRITE\_BUF	Allows the library to modify the contents of the write buffer
H5PSET\_SELECTION\_IO	Sets the selection I/O mode


In the Fortran Interface

h5pget\_modify\_write\_buf\_f
Retrieves the "modify write buffer" property
h5pget\_selection\_io\_f	Retrieves the selection I/O mode
h5pset\_modify\_write\_buf\_f	Allows the library to modify the contents of the write buffer
h5pset\_selection\_io\_f	Sets the selection I/O mode
 

<h2 id="0versus12.2">Release 1.14.0 versus Release 1.12.2</h2>
HDF5 version 1.14.0 introduces the following new features:

Asynchronous I/O operations
New tools h5dwalk and h5delete
Subfiling VFD
Onion VFD
Multi Dataset I/O
Users might find these names familiar already and that is because they were introduced in the experimental series 1.13.

In addition, this version provides many new C APIs and other user-visible changes in behavior in the transition from HDF5 Release 1.12.2 to Release 1.14.0.  HDF5 1.14.0 adds no new API calls that require use of the API Compatibility Macros for the main library.  Some calls have been removed or have had their signature change, however.

New and Changed Functions, Classes, Subroutines, Wrappers, and Macros
In the C Interface (main library)

Following are the new APIs introduced in HDF5-1.14.0. 

 

H5A\_CLOSE\_ASYNC

N

Asynchronous version of H5Aclose

H5A\_CREATE\_ASYNC

N

Asynchronous version of H5Acreate

H5A\_CREATE\_BY\_NAME\_ASYNC

N

Asynchronous version of H5Acreate\_by\_name

H5A\_EXISTS\_ASYNC

N

Asynchronous version of H5Aexists

H5A\_EXISTS\_BY\_NAME\_ASYNC

N

Asynchronous version of H5Aexists\_by\_name

H5A\_OPEN\_ASYNC

N

Asynchronous version of H5Aopen

H5A\_OPEN\_BY\_IDX\_ASYNC

N

Asynchronous version of H5Aopen\_by\_idx

H5A\_OPEN\_BY\_NAME\_ASYNC

N

Asynchronous version of H5Aopen\_by\_name

H5A\_READ\_ASYNC

N

Asynchronous version of H5Aread

H5A\_RENAME\_ASYNC

N

Asynchronous version of H5Arename

H5A\_RENAME\_BY\_NAME\_ASYNC

N

Asynchronous version of H5Arename\_by\_name

H5A\_WRITE\_ASYNC

N

Asynchronous version of H5Awrite

 	 	 
H5D\_CHUNK\_ITER

N	Iterate over all chunks of a chunked dataset
H5D\_CLOSE\_ASYNC

N	Asynchronous version of H5Dclose
H5D\_CREATE\_ASYNC

N	Asynchronous version of H5Dcreate
H5D\_GET\_SPACE\_ASYNC

N	Asynchronous version of H5Dget\_space
H5D\_OPEN\_ASYNC

N	Asynchronous version of H5Dopen
H5D\_READ\_ASYNC

N	Asynchronous version of H5Dread
H5D\_READ\_MULTI

N	Reads raw data from a set of datasets into the provided buffers
H5D\_READ\_MULTI\_ASYNC

N	Asynchronous version of H5Dread\_multi
H5D\_SET\_EXTENT\_ASYNC

N	Asynchronous version of H5Dset\_extent
H5D\_WRITE\_ASYNC

N	Asynchronous version of H5Dwrite
H5D\_WRITE\_MULTI

N	Writes raw data from a set buffers to a set of datasets
H5D\_WRITE\_MULTI\_ASYNC

N	Asynchronous version of H5Dwrite\_multi
 	 	 
H5E\_APPEND\_STACK

N	Appends one error stack to another, optionally closing the source stack
 	 	 
H5ES\_CANCEL

N	Attempt to cancel operations in an event set
H5ES\_CLOSE

N	Terminates access to an event set
H5ES\_CREATE

N	Creates an event set
H5ES\_FREE\_ERR\_INFO

N	Convenience routine to free an array of H5ES\_err\_info\_t structs
H5ES\_GET\_COUNT

N	Retrieves number of events in an event set
H5ES\_GET\_ERR\_COUNT

N	Retrieves the number of failed operations
H5ES\_GET\_ERR\_INFO

N	Retrieves information about failed operations
H5ES\_GET\_ERR\_STATUS

N	Checks for failed operations
H5ES\_GET\_OP\_COUNTER

N	Retrieves the accumulative operation counter for an event set
H5ES\_REGISTER\_COMPLETE\_FUNC

N	Registers a callback to invoke when an operation completes within an event set
H5ES\_REGISTER\_INSERT\_FUNC

N	Registers a callback to invoke when a new operation is inserted into
H5ES\_WAIT

N	 Waits for operations in event set to complete
 	 	 
H5FD\_ONION\_GET\_REVISION\_COUNT

N	Gets the number of revisions
H5P\_GET\_FAPL\_ONION

N	Gets the onion info from the file access property list
H5P\_SET\_FAPL\_ONION

N	Sets the onion info for the file access property list
 	 	 
H5F\_CLOSE\_ASYNC

N	Asynchronous version of H5Fclose
H5F\_CREATE\_ASYNC

N	Asynchronous version of H5Fcreate
H5F\_FLUSH\_ASYNC

N	Asynchronous version of H5Fflush
H5F\_OPEN\_ASYNC

N	Asynchronous version of H5Fopen
H5F\_REOPEN\_ASYNC

N	Asynchronous version of H5Freopen
 	 	 
H5G\_CLOSE\_ASYNC

N	Asynchronous version of H5Gclose
H5G\_CREATE\_ASYNC

N	Asynchronous version of H5Gcreate
H5G\_GET\_INFO\_ASYNC

N	Asynchronous version of H5Gget\_info
H5G\_GET\_INFO\_BY\_IDX\_ASYNC

N	Asynchronous version of H5Gget\_info\_by\_idx
H5G\_GET\_INFO\_BY\_NAME\_ASYNC

N	Asynchronous version of H5Gget\_info\_by\_name
H5G\_OPEN\_ASYNC

N	Asynchronous version of H5Gopen
 	 	 
H5I\_REGISTER\_FUTURE

N	Registers a "future" object under a type and returns an ID for it
 	 	 
H5L\_CREATE\_HARD\_ASYNC

N	Asynchronous version of H5Lcreate\_hard
H5L\_CREATE\_SOFT\_ASYNC

N	Asynchronous version of H5Lcreate\_soft
H5L\_DELETE\_ASYNC

N	Asynchronous version of H5Ldelete
H5L\_DELETE\_BY\_IDX\_ASYNC

N	Asynchronous version of H5Ldelete\_by\_idx
H5L\_EXISTS\_ASYNC

N	Asynchronous version of H5Lexists
H5L\_ITERATE\_ASYNC

N	Asynchronous version of H5Literate
 	 	 
H5O\_CLOSE\_ASYNC

N	Asynchronous version of H5Oclose
H5O\_COPY\_ASYNC

N	Asynchronous version of H5Ocopy
H5O\_FLUSH\_ASYNC

N	Asynchronous version of H5Oflush
H5O\_GET\_INFO\_BY\_NAME\_ASYNC

N	Asynchronous version of H5Oget\_info\_by\_name
H5O\_OPEN\_ASYNC

N	Asynchronous version of H5Oopen
H5O\_OPEN\_BY\_IDX\_ASYNC

N	Asynchronous version of H5Oopen\_by\_idx
H5O\_REFRESH\_ASYNC

N	Asynchronous version of H5Orefresh
 	 	 
H5P\_GET\_DRIVER\_CONFIG\_STR

N	Retrieves a string representation of the configuration for the driver set on the given FAPL
H5P\_GET\_VOL\_CAP\_FLAGS

N	Query the capability flags for the VOL connector that will be used with this file access property list (FAPL)
H5P\_SET\_DATASET\_IO\_HYPERSLAB\_SELECTION

N	Sets a hyperslab file selection for a dataset I/O operation
H5P\_SET\_DRIVER\_BY\_NAME

N	Sets a file driver according to a given driver name
H5P\_SET\_DRIVER\_BY\_VALUE

N	Sets a file driver according to a given driver value (ID)
 	 	 
H5\_ATCLOSE

N	Registers a callback for the library to invoke when it's closing
H5\_IS\_LIBRARY\_TERMINATING

N	Checks whether the HDF5 library is closing
 	 	 
H5R\_OPEN\_ATTR\_ASYNC

N	Asynchronous version of H5Ropen\_attr
H5R\_OPEN\_OBJECT\_ASYNC

N	Asynchronous version of H5Ropen\_object
H5R\_OPEN\_REGION\_ASYNC

N	Asynchronous version of H5Ropen\_region
 	 	 
H5T\_CLOSE\_ASYNC

N	Asynchronous version of H5Tclose
H5T\_COMMIT\_ASYNC

N	Asynchronous version of H5Tcommit2
H5T\_OPEN\_ASYNC

N	Asynchronous version of H5Topen2
