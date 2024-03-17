---
title: Asynchronous Operations with HDF5 VOL Connectors
redirect_from:
  - display/HDF5/Asynchronous+operations+with+HDF5+VOL+connectors
---

# Asynchronous Operations with HDF5 VOL Connectors

HDF5 provides asynchronous APIs for the HDF5 VOL connectors that
support asynchronous HDF5 operations using the [HDF5 Event Set](event_set.md) (H5ES)
API. This allows I/O to proceed in the background while the application
is performing other tasks.

To support AIO capabilities for the HDF5 VOL connectors, the AIO
versions for the functions listed in the table below were added to HDF5
library version 1.14.0 and later. The async version of the function has
"\_async" suffix added to the function name. For example, the async
version for H5Fcreate is H5Fcreate_async.


| Interface | Functions |
| --------- | --------- |
| H5F       | H5Fcreate, H5Fflush, H5Fis_accessible, H5Fopen, H5Fclose |
| H5G       | H5Gcreate, H5Gget_info, H5Gget_info_by_idx, H5Gget_info_by_name, H5Gclose |
| H5D       | H5Dcreate, H5Dopen, H5Dset_extent3, H5Dwrite, H5Dread, H5Dget_space, H5Dclose |
| H5A       | H5Acreate, H5Acreate_by_name, H5Aopen, H5Aopen_by_name, H5Aexists, H5Awrite, H5Aread, H5Aclose, H5Aopen_by_idx, H5Arename, H5Arename_by_name |
| H5L       | H5Lcreate_hard, H5Lcreate_soft, H5delete, H5Ldelete_by_idx, H5Lexists |
| H5O       | H5Ocopy, H5Orefresh, H5Oflush, H5Oclose, H5Open, H5Oopen_by_index |
| H5R       | H5Ropen_attr, H5Ropen_obj, H5Ropen_region, H5Rdereference |
| H5M       | H5Mcreate, H5Mopen, H5Mput, H5Mget, H5Mclose |
| H5T       | H5Tcommit, H5Topen, H5Tcopy, H5Tclose |



Async versions of the functions have an extra parameter called the event set parameter or es_id.  For example, compare the signatures of H5Dclose and H5Dclose_async:

herr_t H5Dclose(hid_t dset_id);
herr_t H5Dclose_async(hid_t dset_id, hid_t es_id);

An event set is an in-memory object that is created by an application and used to track many asynchronous operations with a single object. They function like a ``bag'' -- holding request tokens from one or more asynchronous operations and provide a simple interface for inspecting the status of the entire set of operations.

See the [H5ES](event_set.md) APIs that were added to the HDF5 library to manage event sets.
