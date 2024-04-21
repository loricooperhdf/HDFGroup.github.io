---
title: Using Identifiers
redirect from:
  - display/HDF5/Using%2BIdentifiers
---

# Using Identifiers

The purpose of this topic is to describe how identifiers behave and how they should be treated by application programs.

When an application program uses the HDF5 library to create or open an item, a unique identifier is returned. The items that return a unique identifier when they are created or opened include the following: dataset, group, datatype, dataspace, file, attribute, property list, referenced object, error stack, and error message.

An application may open one of the items listed above more than once at the same time. For example, an application might open a group twice, receiving two identifiers. Information from one dataset in the group could be handled through one identifier, and the information from another dataset in the group could be handled by a different identifier.

An application program should track every identifier it receives as a result of creating or opening one of the items listed above. In order for an application to close properly, it must release every identifier it has opened. If an application opened a group twice for example, it would need to issue two H5Gclose commands, one for each identifier. Not releasing identifiers causes resource leaks. Until an identifier is released, the item associated with the identifier is still open.

The library considers a file open until all of the identifiers associated with the file and with the file’s various items have been released. The identifiers associated with these open items must be released separately. This means that an application can close a file and still work with one or more portions of the file. Suppose an application opened a file, a group within the file, and two datasets within the group. If the application closed the file with H5Fclose, then the file would be considered closed to the application, but the group and two datasets would still be open.

There are several exceptions to the above file closing rule. One is when the H5close function is used instead of H5Fclose. H5close causes a general shut down of the library: all data is written to disk, all identifiers are closed, and all memory used by the library is cleaned up. Another exception occurs on parallel processing systems. Suppose on a parallel system an application has opened a file, a group in the file, and two datasets in the group. If the application uses the H5Fclose function to close the file, the call will fail with an error. The open group and datasets must be closed before the file can be closed. A third exception is when the file access property list includes the property H5F_CLOSE_STRONG. This property causes the closing of all of the file’s open items when the file is closed with H5Fclose. For more information about H5close, H5Fclose, and H5Pset_fclose_degree, see the [HDF5 Reference Manual](https://docs.hdfgroup.org/hdf5/develop/_r_m.html).

The reference manual entries for functions that return identifiers describe what might be returned as follows:

**Returns**:
     Returns an identifier if successful; otherwise returns a negative value.

In other words, a successful operation will return a non-negative identifier which will never be 0 (zero) and will always be a positive value.

## Functions that Return Identifiers

Some of the functions that return identifiers are listed below.

* H5Acreate
* H5Acreate_by_name
* H5Aget_type
* H5Aopen
* H5Aopen_by_idx
* H5Aopen_by_name
* H5Dcreate
* H5Dcreate_anon
* H5Dget_access_plist
* H5Dget_create_plist
* H5Dget_space
* H5Dget_type
* H5Dopen
* H5Ecreate_msg
* H5Ecreate_stack
* H5Fcreate
* H5Fopen
* H5Freopen
* H5Gcreate
* H5Gcreate_anon
* H5Gopen
* H5Oopen
* H5Oopen_by_addr
* H5Oopen_by_idx
* H5Pcreate
* H5Pget_virtual_srcspace
* H5Pget_virtual_vspace
* H5Rdereference
* H5Rget_region
* H5Screate
* H5Screate_simple
* H5Tcopy
* H5Tcreate
* H5Tdecode
* H5Tget_member_type
* H5Tget_super
* H5Topen
