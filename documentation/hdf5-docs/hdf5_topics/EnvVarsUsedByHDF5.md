---
title: Using Compression in HDF5
redirect from:
  - display/HDF5/Environment+Variables+Used+by+HDF5
---

# Building HDF5

## Configuring the Software

The following environment variables can be used to override the choices used by autotools or CMake. These can be seen by typing `./configure -help` from the top directory of the HDF5 source code.

| Environment Variable | Description                                                           |
| -------------------- | --------------------------------------------------------------------- |
| CC                   | C compiler command |
| CFLAGS               | C compiler flags |
| LDFLAGS              | linker flags, e.g. -L<lib dir> if you have libraries in a nonstandard directory <lib dir> |
| LIBS                 | libraries to pass to the linker, e.g. -l<library> |
| CPPFLAGS             | (Objective) C/C++ preprocessor flags, e.g. -I<include dir> if you have headers in a nonstandard directory <include dir> |
| CPP                  | C preprocessor |
| FC                   | Fortran compiler command |
| FCFLAGS              | Fortran compiler flags |
| CXX                  | C++ compiler command |
| CXXFLAGS             | C++ compiler flags |
| CXXCPP               | C++ preprocessor |
| LT_SYS_LIBRARY_PATH  | User-defined run-time library search path |

## Ignoring errors when building the tests
You can set the environment variable HDF5_Make_Ignore to tell the hdf5 Makefile to ignore test errors and continue on. For example:

~~~
env HDF5_Make_Ignore=yes gmake check
~~~

## File locking
A configure option is available to disable file locking:

~~~
-disable-libtool-lock 
~~~

You can also set the HDF5_USE_FILE_LOCKING environment variable to FALSE to disable file locking.

## Parallel HDF5
There are environment variables (for example, RUNPARALLEL and RUNSERIAL) that can be used when building Parallel HDF5. See the release_docs/INSTALL_parallel file in the HDF5 source code for further details.

# Using HDF5 and HDF5 Tools

## Adjusting the h5repack buffer size
If encountering poor performance using h5repack with large datasets, the  H5TOOLS_BUFSIZE environment variable can be used to improve performance. This environment variable specifies the hyperslab (selection) buffer size (in bytes) that is used by h5repack.

## Dynamic Filter Plugins
The Registered Filter Plugins are (compression) filters that users have created and contributed, and which have been registered with The HDF Group. The plugins depend on the environment variable, HDF5_PLUGIN_PATH.
