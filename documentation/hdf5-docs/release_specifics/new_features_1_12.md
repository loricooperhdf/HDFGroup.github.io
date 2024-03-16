---
title: New Features in HDF5 1.12
redirect from: 
  - display/HDF5/New+Features+in+HDF5+Release+1.12
---

This release includes changes in the HDF5 storage format. PLEASE NOTE that HDF5-1.10 and earlier releases cannot read files created with the new features described below that are marked with a \*.

HDF5 1.12 introduces several new features in the HDF5 library:

* [H5Sencode / H5Sdecode Format Change - RFC](https://docs.hdfgroup.org/hdf5/rfc/H5Sencode_format.docx.pdf)
* [Update to References](https://docs.hdfgroup.org/hdf5/rfc/RFC_Update_to_HDF5_References.pdf)
* [Update to Selections](https://docs.hdfgroup.org/hdf5/rfc/selection_io_RFC_210610.pdf)
* [Virtual Object Layer](https://docs.hdfgroup.org/hdf5/develop/_v_o_l__connector.html)
* [Hyperslab Performance Improvement](#Hyperslab-Performance-Improvements)

### Virtual Object Layer (VOL)  (RFC)

See the [Virtual Object Layer](https://docs.hdfgroup.org/hdf5/develop/_h5_v_l__u_g.html#sec_vol) page for more information.

The Virtual Object Layer (VOL) is an abstraction layer within the HDF5 library that enables different methods for accessing data and objects that conform to the HDF5 data model. The VOL intercepts all HDF5 API calls that potentially modify data on disk and forwards those calls to a plugin "object driver". The data on disk can be a different format than the HDF5 format.



The plugins can actually store the objects in variety of ways. A plugin could, for example, have objects be distributed remotely over different platforms, provide a raw mapping of the model to the file system, or even store the data in other file formats (like native netCDF or HDF4 format). The user still gets the same data model where access is done to a single HDF5 \"container\"; however the plugin object driver translates from what the user sees to how the data is actually stored. Having this abstraction layer maintains the object model of HDF5 and allows better usage of new object storage file systems that are targeted for Exascale systems.

### Hyperslab Performance Improvements
In 1.12.0 the hyperslab selection code was optimized to achieve better performance. In general, performance improved by an order of a magnitude. In the case of reading a regular selection from a 20 GB dataset into a one dimensional array, performance improved by a factor of 6000. If you are interested in the benchmark we ran, please see issue HDFFV-10930 by logging into jira.hdfgroup.org with your hdfgroup.org login.

### Update to References (RFC) *
See the Update to References page for details on the changes in HDF5-1.12.

HDF5 references were extended to support attributes, as well as object and dataset selections that reside in another HDF5 file. In order to support these features several functions were introduced:

* Create (H5R_CREATE\*) functions were added for each reference type: object, dataset region and attribute.
* A function was added to release a reference (H5R_DESTROY). This is required because a region reference no longer modifies the original file.
* Functions were added to query references (H5R_GET\*).
* Other functions were added to simplify or clarify the API.

### Update to Selections
Several new H5S APIs were introduced to allow a user to more flexibly operate on two hyperslab selections. See Update to Selections for more details.
