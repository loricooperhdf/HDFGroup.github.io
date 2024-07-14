---
title: Software Changes from Release to Release for HDF5 1.14
redirect_from: 
  - /display/HDF5/Software+Changes+from+Release+to+Release+for+HDF5+1.14
---

# Software Changes from Release to Release in HDF5 1.14

## API Compatibility

See [API Compatibility Macros](https://docs.hdfgroup.org/hdf5/develop/api-compat-macros.html) in HDF5 for details on using HDF5 version 1.14 with previous releases.


* [Compatibility report for Release 1.14.4 versus Release 1.14.3](https://github.com/HDFGroup/hdf5/releases/download/hdf5_1.14.4.2/hdf5-1.14.4-2.html.abi.reports.tar.gz)
* [Compatibility report for Release 1.14.3 versus Release 1.14.2](https://htmlpreview.github.io/?https://raw.githubusercontent.com/HDFGroup/hdf5doc/master/html/ADGuide/Compatibility_Report/hdf5-1.14.2-vs-hdf5-1.14.3-interface_compatibility_report.html)
* [Compatibility report for Release 1.14.2 versus Release 1.14.1](https://htmlpreview.github.io/?https://raw.githubusercontent.com/HDFGroup/hdf5doc/master/html/ADGuide/Compatibility_Report/hdf5-1.14.1-2-vs-hdf5-1.14.2-interface_compatibility_report.html)
* [Compatibility report for Release 1.14.1 versus Release 1.14.0](https://htmlpreview.github.io/?https://raw.githubusercontent.com/HDFGroup/hdf5doc/master/html/ADGuide/Compatibility_Report/hdf5-1.14.0-vs-hdf5-1.14.1-interface_compatibility_report.html)
* [Compatibility report for Release 1.14.0 versus Release 1.12.2](https://htmlpreview.github.io/?https://raw.githubusercontent.com/HDFGroup/hdf5doc/master/html/ADGuide/Compatibility_Report/hdf5-1.12.2-vs-hdf5-1.14.0-interface_compatibility_report.html)

 
This page provides information on the changes that a maintenance developer needs to be aware of between successive releases of HDF5, such as:

* New or changed features or tools
* Syntax and behavioral changes in the existing application programming interface (the API)
* Certain types of changes in configuration or build processes
* Note that bug fixes and performance enhancements in the C library are automatically picked up by the C++, Fortran, and Java libraries.

The following information is included below.

* <a href="#4versus3">Release 1.14.4 versus Release 1.14.3</a>
* <a href="#3versus2">Release 1.14.3 versus Release 1.14.2</a>
* <a href="#2versus1">Release 1.14.2 versus Release 1.14.1</a>
* <a href="#1versus0">Release 1.14.1 versus Release 1.14.0</a>
* <a href="#0versus12_2">Release 1.14.1 versus Release 1.12.2</a>

The release notes also list changes made to the library, but these notes tend to be more at a more detail-oriented level. The release notes may include new features, bugs fixed, supported configuration features, platforms on which the library has been tested, and known problems. The release note files are listed in each release section and can be found at the top level of the HDF5 source code tree in the release_docs directory.

<h2 id="4versus3">Release 1.14.4 versus Release 1.14.3</h2>

### New and Changed Functions, Classes, Subroutines, Wrappers, and Macros
Following are the new APIs/macros introduced in HDF5-1.14.4.

#### In the C Interface (main library)

| Function                             | Description                                  |
| ------------------------------------ | -------------------------------------------- |
| [H5Pget_relax_file_integrity_checks](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#gab1e57751a5f34c1a7cb6dd0194877d3e) | Retrieves relaxed file integrity check flags |
| [H5Pset_relax_file_integrity_checks](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#gafa8e677af3200e155e9208522f8e05c0) | Relaxes certain file integrity checks        |

| Macro              | Description                         |
| ------------------ | ----------------------------------- |
| H5T_IEEE_F16BE     | 16-bit big-endian IEEE floating-point numbers |
| H5T_IEEE_F16LE     | 16-bit little-endian IEEE floating-point numbers |
| H5T_NATIVE_FLOAT16 | C-style `_Float16` |

* [Compatibility report for Release 1.14.4 versus Release 1.14.3](https://github.com/HDFGroup/hdf5/releases/download/hdf5_1.14.4.2/hdf5-1.14.4-2.html.abi.reports.tar.gz)

<h2 id="3versus2">Release 1.14.3 versus Release 1.14.2</h2>

This section lists interface-level changes and other user-visible changes in behavior in the transition from HDF5 Release 1.14.2 to Release 1.14.3.

### New and Changed Functions, Classes, Subroutines, Wrappers, and Macros
Following are the new APIs introduced in HDF5-1.14.3.

#### In the C Interface (main library)

| Function                           | Description                         |
| ---------------------------------- | ----------------------------------- |
| [H5Pget_actual_selection_io_mode](https://docs.hdfgroup.org/hdf5/v1_14/group___d_x_p_l.html#ga252fe801869970c14a5e800a1ea7ab84) | Retrieves the type(s) of I/O performed on raw data |

#### In the Fortran Interface

| Function                           | Description                         |
| ---------------------------------- | ----------------------------------- |
| [h5get_free_list_sizes_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5.html#gac849cafadb09ed2c3cd9272a4ef8af3c) | Gets the current size of the free lists used to manage memory |
| [h5dwrite_chunk_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_d.html#ga2fd1e4afdf4b99f2f7e442dc62abed2d) | Writes a raw data chunk from a buffer directly to a dataset in a file |
| [h5dread_chunk_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_d.html#ga65717cab74e512b25906af44091f4fd5) | Reads a raw data chunk directly from a dataset in a file into a buffer |
| [h5fget_info_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_f.html#ga1b95a395f594fdf83021447f68f01e72) | Retrieves global file information |
| [h5lvisit_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_l.html#gad2ff5308e86d5065e972904e2701a6bf) | Recursively visits all links starting from a specified group |
| [h5lvisit_by_name_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_l.html#ga48c154c5f9b95b4bcced7b0b4f700232) | Recursively visits all links starting from a specified group |
| [h5pget_no_selection_io_cause_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_p.html#ga325eaad4d3f2c2e1419628f2ce6580bd) | Retrieves the cause for not performing selection or vector I/O on the last parallel I/O call |
| [h5pget_mpio_no_collective_cause_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_p.html#ga5ab340d6c40b8cc504caf594c5779bd6) | Retrieves local and global causes that broke collective I/O on the last parallel I/O call |
| [h5sselect_shape_same_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_s.html#gaf868fca7ef836b464bb39d3c8da38b77) | Checks if two selections are the same shape |
| [h5sselect_intersect_block_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_s.html#ga41e9d402d76e0d453202706592d4b148) | Checks if current selection intersects with a block |
| [h5pget_file_space_page_size_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_p.html#ga92e75dfef3a339f1987002fbea5f2bfb) | Gets the file space page size for a file creation property list |
| [h5pset_file_space_page_size_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_p.html#ga35605e8cfdceaffc3840aa386d63aa00) | Sets the file space page size for a file creation property list |
| [h5pget_file_space_strategy_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_p.html#ga730a5864c03cdfc2722e3f4369910fa5) | Gets the file space handling strategy and persisting free-space values for a file creation property list |
| [h5pset_file_space_strategy_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_p.html#ga06e49a3cde33e52115c5a7dcc0c642da) | Sets the file space handling strategy and persisting free-space values for a file creation property list |

In addition, there are other new Fortran functions including the Fortran async APIs
and the Fortran VOL capability definitions.

* [Compatibility report for Release 1.14.3 versus Release 1.14.2](https://htmlpreview.github.io/?https://raw.githubusercontent.com/HDFGroup/hdf5doc/master/html/ADGuide/Compatibility_Report/hdf5-1.14.2-vs-hdf5-1.14.3-interface_compatibility_report.html)

<h2 id="2versus1">Release 1.14.2 versus Release 1.14.1</h2>

This section lists interface-level changes and other user-visible changes in behavior in the transition from HDF5 Release 1.14.1 to Release 1.14.2.

### New and Changed Functions, Classes, Subroutines, Wrappers, and Macros
Following are the new APIs introduced in HDF5-1.14.2.

#### In the C Interface (main library)

| Function                           | Description                                                  |
| ---------------------------------- | ------------------------------------------------------------ |
| [H5FDread_from_selection](https://docs.hdfgroup.org/hdf5/v1_14/_h5_f_ddevelop_8h.html#a562c69aaa9cd0cac7f2e81110c2fa04d) | Performs a series of scalar reads. |
| [H5FDread_vector_from_selection](https://docs.hdfgroup.org/hdf5/v1_14/_h5_f_ddevelop_8h.html#a04a29af1028d1db99edb765c80cf6f5c) | Performs a vector read if vector reads are supported, or a series of scalar reads, otherwise. |
| [H5FDwrite_from_selection](https://docs.hdfgroup.org/hdf5/v1_14/_h5_f_ddevelop_8h.html#a0ba732516878e1a18f6244b43a4055cc) | Performs a series of scalar writes. |
| [H5FDwrite_vector_from_selection](https://docs.hdfgroup.org/hdf5/v1_14/_h5_f_ddevelop_8h.html#adeed09246b8feb1a5a301e263e9236b2) | Performs a vector write if vector writes are supported, or a series of scalar writes, otherwise. |

| Function                           | Description                                                  |
| ---------------------------------- | ------------------------------------------------------------ |
| [H5Pget\_fapl\_ros3\_token](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#gafa91f06270a937cbbf20457ce0a7027e) | Returns session/security token of the ros3 file access property list |
| [H5Pset\_fapl\_ros3\_token](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#ga42bc76c556951027e30c4d26394323c6) | Modifies the file access property list to use the H5FD_ROS3 driver |

* [Compatibility report for Release 1.14.2 versus Release 1.14.1](https://htmlpreview.github.io/?https://raw.githubusercontent.com/HDFGroup/hdf5doc/master/html/ADGuide/Compatibility_Report/hdf5-1.14.1-2-vs-hdf5-1.14.2-interface_compatibility_report.html)

<h2 id="1versus0">Release 1.14.1 versus Release 1.14.0</h2>

This section lists interface-level changes and other user-visible changes in behavior in the transition from HDF5 Release 1.14.0 to Release 1.14.1.

### New and Changed Functions, Classes, Subroutines, Wrappers, and Macros
Following are the new APIs introduced in HDF5-1.14.1.

#### In the C Interface (main library)

| Function                         | Description                                                  |
| -------------------------------- | ------------------------------------------------------------ |
| [H5Pget_modify_write_buf](https://docs.hdfgroup.org/hdf5/v1_14/group___d_x_p_l.html#ga7a3e4d3f7b5c276873d00af3f92cdc22) | Retrieves the "modify write buffer" property |
| [H5Pget_no_selection_io_cause](https://docs.hdfgroup.org/hdf5/v1_14/group___d_x_p_l.html#gad6fa6bfa5956e8c0bd69c22bde65f84c) | Retrieves the cause for not performing selection or vector I/O on the last parallel I/O call |
| [H5Pget_selection_io](https://docs.hdfgroup.org/hdf5/v1_14/group___d_x_p_l.html#ga324f2407a698f376c9970331dd8c8d16) | Retrieves the selection I/O mode |
| [H5Pset_modify_write_buf](https://docs.hdfgroup.org/hdf5/v1_14/group___d_x_p_l.html#ga6f65ca81d8a10015513a69fe76c5d542) | Allows the library to modify the contents of the write buffer |
| [H5Pset_selection_io](https://docs.hdfgroup.org/hdf5/v1_14/group___d_x_p_l.html#ga7d4d11c9c273d5a5ce2d174d66e4fa10) | Sets the selection I/O mode 

#### In the Fortran Interface

| Function                         | Description                                                  |
| -------------------------------- | ------------------------------------------------------------ |
| [h5pget_modify_write_buf_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_p.html#gae0ee05629782098d640b85b3ff60c04e) | Retrieves the "modify write buffer" property                 |
| [h5pget_selection_io_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_p.html#ga613c962a80f27ef990dc8ba6a011a452) | Retrieves the selection I/O mode                             |
| [h5pset_modify_write_buf_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_p.html#ga098bf9a1a922826ff09623d78b49797d) | Allows the library to modify the contents of the write buffer|
| [h5pset_selection_io_f](https://docs.hdfgroup.org/hdf5/v1_14/group___f_h5_p.html#ga634a2040e0dc820085cd87edb014ffd5) | Sets the selection I/O mode                                  |
 

<h2 id="0versus12.2">Release 1.14.0 versus Release 1.12.2</h2>

HDF5 version 1.14.0 introduces the following new features:

* Asynchronous I/O operations
* New tools h5dwalk and h5delete
* Subfiling VFD
* Onion VFD
* Multi Dataset I/O

Users might find these names familiar already and that is because they were introduced in the experimental series 1.13.

In addition, this version provides many new C APIs and other user-visible changes in behavior in the transition from HDF5 Release 1.12.2 to Release 1.14.0.  HDF5 1.14.0 adds no new API calls that require use of the API Compatibility Macros for the main library.  Some calls have been removed or have had their signature change, however.

New and Changed Functions, Classes, Subroutines, Wrappers, and Macros
In the C Interface (main library)

Following are the new APIs introduced in HDF5-1.14.0. 

 
| Function                           | Fortran | Description                                        |
| ---------------------------------- | ------- | ---------------------------------------------------|
| [H5Aclose_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga121fb36f6571bfaf17eb0a92f3275560) | N | Asynchronous version of H5Aclose |
| [H5Acreate_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga9b3ce1af9b445a6381479e8f3b58e6d9) | N | Asynchronous version of H5Acreate |
| [H5Acreate_by_name_async](uhttps://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga13dd8779381c7834b59a4ac5521c83barl) | N | Asynchronous version of [H5Acreate_by_name](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_a.html#ga004160c28e281455ec48aa7fe557ef8a) |
| [H5Aexists_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gaeb69d6b6c9dcf8ee77481010c619d664) | N | Asynchronous version of H5Aexists |
| [H5Aexists_by_name_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga42b804d43e11cc0db6e0e58be7b3bd3c) | N | Asynchronous version of [H5Aexists_by_name](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_a.html#gaa1d2305651a4524f6aa0f8b56eec1a37) |
| [H5Aopen_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga8167b57603377742ae78a278dda27634) | N | Asynchronous version of H5Aopen |
| [H5Aopen_by_idx_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga1bef4a2dce9cfc0ddaa7472ac1e2d1dd) | N | Asynchronous version of [H5Aopen_by_idx](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_a.html#gab1451cdff4f77dcf9feaee83c8179b2d) |
| [H5Aopen_by_name_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga42e2c5c72201f05b32e1c9dda6df0e30) | N | Asynchronous version of [H5Aopen_by_name](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_a.html#gadb49a0b5b9798d2e944d877adba8ae10) |
| [H5Aread_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga7a74c8bd935164e2d19d4b253cde815a) | N | Asynchronous version of [H5Aread](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_a.html#gaacb27a997f7c98e8a833d0fd63b58f1c) |
| [H5Arename_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga5eb1ec49226fd0ec8e6dedc608f134f8) | N | Asynchronous version of H5Arename |
| [H5Arename_by_name_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga27e7336cbf2182a85d8fba3cdf476d8e) | N | Asynchronous version of H5Arename_by_name |
| [H5Awrite_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gae841dec1e2f4fecd88252307d20c1a59) | N | Asynchronous version of H5Awrite |
| [H5Dchunk_iter](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_d.html#gac482c2386aa3aea4c44730a627a7adb8) | N | Iterate over all chunks of a chunked dataset |
| [H5Dclose_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga0933c085c070e86350e3548e337e4e7e) | N | Asynchronous version of H5Dclose |
| [H5Dcreate_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gad18a501b7425902947237ec81706182e) | N | Asynchronous version of H5Dcreate |
| [H5Dget_space_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga3eb6290902f6d709c762f80d067da3d3) | N | Asynchronous version of H5Dget_space |
| [H5Dopen_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga6df171aded96ec4926cd46000bf94f7d) | N | Asynchronous version of H5Dopen |
| [H5Dread_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga32856023e22cb8ed2ffa74b1651037b6) | N | Asynchronous version of H5Dread |
| [H5Dread_multi](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_d.html#ga8eb1c838aff79a17de385d0707709915) | N | Reads raw data from a set of datasets into the provided buffers |
| [H5Dread_multi_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga7434c55da618b62d2c20cde4e0e040fc) | N | Asynchronous version of H5Dread_multi |
| [H5Dset_extent_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gab8e6d326fabbad5683ef6d0f669bae75) | N | Asynchronous version of H5Dset_extent |
| [H5Dwrite_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga7773f0c3503418421bcb535a95ee832e) | N | Asynchronous version of H5Dwrite |
| [H5Dwrite_multi] (https://docs.hdfgroup.org/hdf5/v1_14/group___h5_d.html#gaf6213bf3a876c1741810037ff2bb85d8) | N | Writes raw data from a set buffers to a set of datasets |
| [H5Dwrite_multi_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga1efc4f95c82571ce3897002c76469fdc) | N | Asynchronous version of H5Dwrite_multi |
| [H5Eappend_stack](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_e.html#gaa35a1b27d704a90f2a933f9d41df35ec) | N | Appends one error stack to another, optionally closing the source stack |
| [H5EScancel](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_e_s.html#ga45ec0f886c4914f9503ab42e811a496a) | N | Attempt to cancel operations in an event set |
| [H5ESclose](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_e_s.html#ga1159e2c6748f200857dffa55011ae060) | N | Terminates access to an event set |
| [H5EScreate](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_e_s.html#gae3cd0a94586acf2d824033ef59fd3ccc) | N | Creates an event set |
| [H5ESfree_err_info](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_e_s.html#gadaab9ec7ce5725bed34636e0cf8cad8d) | N | Convenience routine to free an array of H5ES_err_info_t structs |
| [H5ESget_count](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_e_s.html#ga1a5a9212958bf7054a56107587d480d2) | N | Retrieves number of events in an event set |
| [H5ESget_err_count](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_e_s.html#ga42b502d05e0dff40ec550c85bb54ca1c) | N | Retrieves the number of failed operations |
| [H5ESget_err_info](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_e_s.html#ga7fe438ffe2d7fcede25e4bec5194c923) | N | Retrieves information about failed operations |
| [H5ESget_err_status](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_e_s.html#gad419f0af15bbddc13d79662bc6b31d7c) | N | Checks for failed operations |
| [H5ESget_op_counter](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_e_s.html#ga1880fb2353f677ef56a6204706cec4d0) | N | Retrieves the accumulative operation counter for an event set |
| [H5ESregister_complete_func](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_e_s.html#gaad19a0bf9ef8816d178f3ee6d1d1ef50) | N | Registers a callback to invoke when an operation completes within an event set |
| [H5ESregister_insert_func](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_e_s.html#gac2255859e4038a02e8dea94b2585e9e8) | N | Registers a callback to invoke when a new operation is inserted into |
| [H5ESwait](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_e_s.html#gab118d8202a0edf6241812420b870a64e) | N | Waits for operations in event set to complete |
| [H5FDonion_get_revision_count](https://docs.hdfgroup.org/hdf5/v1_14/_h5_f_donion_8h.html#a132aba14546c0da4cc2e467ba4219715) | N | Gets the number of revisions |
| [H5Pget_fapl_onion](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#ga89b9f918d53dee5e6c80060667b8d32f) | N | Gets the onion info from the file access property list |
| [H5Pset_fapl_onion](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#ga4d053c7682e54287e550113972b7dda6) | N | Sets the onion info for the file access property list |
| [H5Fclose_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gac4e2607f507f9b098d3987e7a90b3eeb) | N | Asynchronous version of H5Fclose |
| [H5Fcreate_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gaa8e7c2dfa274c41d3ac30678ce77647e) | N | Asynchronous version of H5Fcreate |
| [H5Fflush_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gaae5544d73d2100e21858ad49c9c53494) | N | Asynchronous version of H5Fflush |
| [H5Fopen_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gaba13f96a277191516514093a63aa9aee) | N | Asynchronous version of H5Fopen |
| [H5Freopen_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga540c3c083deadfb3165fd2c7468e206d) | N | Asynchronous version of H5Freopen |
| [H5Gclose_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gaedca4d2a02bac2dad772dc41dbdd6d68) | N | Asynchronous version of H5Gclose |
| [H5Gcreate_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gaae55331055ebaab0da4dad974b1b0c91) | N | Asynchronous version of H5Gcreate |
| [H5Gget_info_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga50a254bdae888fcd08fe42465b5f386f) | N | Asynchronous version of H5Gget_info |
| [H5Gget_info_by_idx_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga87d9d82991d998f5f1dd4378e611f46b) | N | Asynchronous version of H5Gget_info_by_idx |
| [H5Gget_info_by_name_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga79226604034b9f7d60aabbe48f53c18a) | N | Asynchronous version of H5Gget_info_by_name |
| [H5Gopen_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga51711cab3f8ae549df283aa2ba384527) | N | Asynchronous version of H5Gopen |
| [H5Iregister_future](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_i.html#gad61703cd16f392fb194da648099e69a9) | N | Registers a "future" object under a type and returns an ID for it |
| [H5Lcreate_hard_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gaecc69b84cafb71d27dbcc244c35930c7) | N | Asynchronous version of H5Lcreate_hard |
| [H5Lcreate_soft_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga7ba84c7db6ef67e270fa7bc3413d4def) | N | Asynchronous version of H5Lcreate_soft |
| [H5Ldelete_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga6074beb8fd1d7761db082fc611519b54) | N | Asynchronous version of H5Ldelete |
| [H5Ldelete_by_idx_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga7dc3198d8cfaeb6a780863af8d0af253) | N | Asynchronous version of H5Ldelete_by_idx |
| [H5Lexists_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gae33482c2e6df9771dde47ae47874fa18) | N | Asynchronous version of H5Lexists |
| [H5Literate_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga0f56b7243d036cdeb5280d8c41f2436e) | N | Asynchronous version of H5Literate |
| [H5Oclose_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga2979a4a45d3cd92c427735db6dcdf431) | N | Asynchronous version of H5Oclose |
| [H5Ocopy_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gae4364b88f8860f680d7782a721bba7af) | N | Asynchronous version of H5Ocopy |
| [H5Oflush_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga90669c99295348e3e169103404d3e61a) | N | Asynchronous version of H5Oflush |
| [H5Oget_info_by_name_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga4c164275a34ff8208d8bcc9f701d47fe) | N | Asynchronous version of H5Oget_info_by_name |
| [H5Oopen_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gaefb9550c0b6faeb8c299dc67f92e1494) | N | Asynchronous version of H5Oopen |
| [H5Oopen_by_idx_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga3775880873cc64059e71f35f5693b4f6) | N | Asynchronous version of H5Oopen_by_idx |
| [H5Orefresh_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gaf3b20ade9902067b99a16e53f171c657) | N | Asynchronous version of H5Orefresh |
| [H5Pget_driver_config_str](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#gac0d9eb573b84ce125433e81b2a475085) | N | Retrieves a string representation of the configuration for the driver set on the given FAPL |
| [H5Pget_vol_cap_flags](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#ga2ad4dc5c6e5e4271334a7b1c6ee0777d) | N | Query the capability flags for the VOL connector that will be used with this file access property list (FAPL) |
| [H5Pset_dataset_io_hyperslab_selection](https://docs.hdfgroup.org/hdf5/v1_14/group___d_x_p_l.html#gadd73dca2b824491cbe768028d7377b2f) | N | Sets a hyperslab file selection for a dataset I/O operation |
| [H5Pset_driver_by_name](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#ga156702db27ece40d21b37be5fe5e8b15) | N | Sets a file driver according to a given driver name |
| [H5Pset_driver_by_value](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#gac4426b1d36aa8766fbe2deaf67a18c06) | N | Sets a file driver according to a given driver value (ID) |
| [H5atclose](https://docs.hdfgroup.org/hdf5/v1_14/group___h5.html#gade62a3e6b75bed52234d9e8432c27fb2) | N | Registers a callback for the library to invoke when it's closing |
| [H5is_library_terminating](https://docs.hdfgroup.org/hdf5/v1_14/group___h5.html#gac2fdfe0e7a1012b796bdeafbed9ab970) | N | Checks whether the HDF5 library is closing |
| [H5Ropen_attr_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#gadd7445737dd9d2d4e519fb7fcf3c3630) | N | Asynchronous version of H5Ropen_attr |
| [H5Ropen_object_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga4ef748212709bcf2030828dcd9dc66a2) | N | Asynchronous version of H5Ropen_object |
| [H5Ropen_region_async](https://docs.hdfgroup.org/hdf5/v1_14/group___a_s_y_n_c.html#ga5f282a3adc66b0d2eafe5d333a6188a9) | N | Asynchronous version of H5Ropen_region |
| [H5Tclose_async](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_t.html#ga2da609983e073f83bcd0d8eff8b528ff) | N | Asynchronous version of H5Tclose |
| [H5Tcommit_async](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_t.html#ga4d0466c9f9762e184e03fdbdb2855ead) | N | Asynchronous version of H5Tcommit2 |
| [H5Topen_async](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_t.html#gad92e4af6b8ac52712fb4238281f921e9) | N | Asynchronous version of H5Topen2 |
