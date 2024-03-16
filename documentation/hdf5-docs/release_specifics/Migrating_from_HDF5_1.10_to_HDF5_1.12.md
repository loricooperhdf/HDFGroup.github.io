---
title: Migrating from HDF5 1.10 to HDF5 1.12
redirect_from: 
  - /display/HDF5/Migrating+from+HDF5+1.10+to+HDF5+1.12.html
---

# Migrating from HDF5 1.10 to HDF5 1.12

Also see the video presentation: [Moving Applications from 1.10 to 1.12](https://www.hdfgroup.org/2020/03/moving-applications-from-1-10-to-hdf5-1-12-video-materials)

There were many existing functions that were modified in 1.12. Applications created with 1.10 or earlier that use these functions will encounter errors when compiled with 1.12. This page describes how to compile 1.10 and earlier applications with 1.12 without modifying an application, and provides details on the functions that changed for users who wish to update their applications.

* [Compiling 1.10 and earlier applications with 1.12](#Compiling-1.10-and-earlier-applications-with-1.12)
* [Functions that changed](#Functions-that-changed)

For further information, see:

* [New Features in 1.12](/documentation/hdf5-docs/release_specifics/new_features_1_12.md)
* [Software Changes from release to release](/documentation/hdf5-docs/release_specifics/sw_changes_1.12.md)
* [API Compatibility Macros in HDF5](/documentation/hdf5-docs/release_specifics/api_comp_macros.md)

### Compiling 1.10 and earlier applications with 1.12

Applications that were created with earlier HDF5 releases may not compile with 1.12 by default. The API Compatibility Macros in HDF5 allow users to work around this issue. Users can specify a compatibility macro mapping for the version of HDF5 that an application was built with. For example, a 1.10 application can be built with 1.12 using either an application or library mapping as follows:

* To compile an application built with a version of HDF5 that includes deprecated symbols (the default), make sure to pass -DH5_USE_110_API to the compiler. For example:

~~~
Autotools:   h5cc -DH5_USE_110_API (C)

CMake:       cmake -DCMAKE_C_FLAGS="-DH5_USE_110_API" (and likewise for other CMAKE_<LANG>_FLAGS)
~~~

* To build an HDF5 library with the 1.10 APIs specify --with-default-api-version=v110 (Autotools) or -DDEFAULT_API_VERSION:STRING=v110 (CMake).

~~~
Autotools: 
./configure --with-default-api-version=v110

CMake:
If using the source code packaged with CMake configuration files (CMake-hdf5-1.12.0*), edit HDF5options.cmake, and add this line:

set(ADD_BUILD_OPTIONS "${ADD_BUILD_OPTIONS} -DDEFAULT_API_VERSION:STRING=v110")

View the libhdf5.settings file to verify that the library was built with the 1.10 APIs:

Default API mapping: v110 (under Features:)
~~~

#### However, users will not be able to take advantage of some of the new features in 1.12 if using these compatibility mappings.

### Functions that changed
Functions were modified in HDF5 version 1.12 to support a token type used in the Virtual Object Layer (VOL) and to enable 64-bit selection encodings. These changes are described below.

~~~
The updated versions of the functions have a number (for eg '2' or '3') at the end of the original function name.   
The original versions of these functions were retained and renamed to have an earlier number (for eg '1') at the end of the original function name.  
A macro was created with the name of the original function.   
Please read [API Compatibility Macros in HDF5](/documentation/hdf5-docs/release_specifics/api_comp_macros.md) for more details on how the function names changed in version 1.12.
~~~

### Token Type
In HDF5 1.12, a token type, H5O_token_t, replaced the address type, haddr_t, for representing locations in an HDF5 file. This change better supports the Virtual Object Layer (VOL), as the concept of an "address" does not make sense for many connectors. A token type is a more generic type that can function as both a connector and address location.

This change affected the following functions:

| Original Function in 1.10/Maroc in 1.12 (H5xxx) | Deprecated Function in 1.12 (H5xxx1) | New Function (using token type) <br>(H5xxx2 or H5xxx3 |
| ----------------------------------------------- | ------------------------------------ | ------------------------------- |
|                                                 |                                      |                                 |
| H5L_GET_INFO                                    | H5L_GET_INFO1                        | H5L_GET_INFO2                   |
| H5L_GET_INFO_BY_IDX                             | H5L_GET_INFO_BY_IDX1                 | H5L_GET_INFO_BY_IDX2            |
| H5L_ITERATE                                     | H5L_ITERATE1                         | H5L_ITERATE2                    |
| H5L_ITERATE_BY_NAME                             | H5L_ITERATE_BY_NAME1                 | H5L_ITERATE_BY_NAME2            |
| H5L_VISIT                                       | H5L_VISIT1                           | H5L_VISIT2                      |
| H5L_VISIT_BY_NAME                               | H5L_VISIT_BY_NAME1                   | H5L_VISIT_BY_NAME2              |
| H5O_GET_INFO                                    | H5O_GET_INFO1                        | H5O_GET_INFO3                   |
| H5O_GET_INFO_BY_IDX                             | H5O_GET_INFO_BY_IDX1                 | H5O_GET_INFO_BY_IDX3            |
| H5O_GET_INFO_BY_NAME                            | H5O_GET_INFO_BY_NAME1                | H5O_GET_INFO_BY_NAME3           |
| H5O_VISIT                                       | H5O_VISIT1                           | H5O_VISIT3                      |
| H5O_VISIT_BY_NAME                               | H5O_VISIT_BY_NAME1                   | H5O_VISIT_BY_NAME3              |
|                                                 |                                      |                                 |

### Encoding Properties
These functions were introduced in HDF5 version 1.12 as part of the H5Sencode format change to enable 64-bit selection encodings and a dataspace selection that is tied to a file. See the [H5Sencode / H5Sdecode Format Change - RFC](https://docs.hdfgroup.org/hdf5/rfc/H5Sencode_format.docx.pdf) format change RFC for details.

| Original Function in 1.10/Maroc in 1.12 (H5xxx) | Deprecated Function in 1.12 (H5xxx1) | New Function (using token type) |
| ----------------------------------------------- | ------------------------------------ | ------------------------------- |
|                                                 |                                      |                                 |
| H5P_ENCODE                                      | H5P_ENCODE1                          | H5P_ENCODE2                     |
| H5S_ENCODE                                      | H5S_ENCODE1                          | H5S_ENCODE2                     |
|                                                 |                                      |                                 |
