---
title: Using Identifiers
redirect from:
  - display/HDF5/Using%2BIdentifiers
---

# Using Identifiers

The purpose of this topic is to describe how identifiers behave and how they should be treated by application programs.

When an application program uses the HDF5 library to create or open an item, a unique identifier is returned. The items that return a unique identifier when they are created or opened include the following: dataset, group, datatype, dataspace, file, attribute, property list, referenced object, error stack, and error message.

An application may open one of the items listed above more than once at the same time. For example, an application might open a group twice, receiving two identifiers. Information from one dataset in the group could be handled through one identifier, and the information from another dataset in the group could be handled by a different identifier.

An application program should track every identifier it receives as a result of creating or opening one of the items listed above. In order for an application to close properly, it must release every identifier it has opened. If an application opened a group twice for example, it would need to issue two [H5Gclose](https://portal.hdfgroup.org/hdf5/develop/group___h5_g.html#ga8dbe20b390d2504f0bd3589ed8f4e221) commands, one for each identifier. Not releasing identifiers causes resource leaks. Until an identifier is released, the item associated with the identifier is still open.

The library considers a file open until all of the identifiers associated with the file and with the file’s various items have been released. The identifiers associated with these open items must be released separately. This means that an application can close a file and still work with one or more portions of the file. Suppose an application opened a file, a group within the file, and two datasets within the group. If the application closed the file with [H5Fclose](https://portal.hdfgroup.org/hdf5/develop/group___h5_f.html#gac55cd91d80822e4f8c2a7f04ea71b124), then the file would be considered closed to the application, but the group and two datasets would still be open.

There are several exceptions to the above file closing rule. One is when the [H5close](https://portal.hdfgroup.org/hdf5/develop/group___h5.html#ga8a9fe81dcf66972ed75ea481e7750574) function is used instead of [H5Fclose](https://portal.hdfgroup.org/hdf5/develop/group___h5_f.html#gac55cd91d80822e4f8c2a7f04ea71b124). [H5close](https://portal.hdfgroup.org/hdf5/develop/group___h5.html#ga8a9fe81dcf66972ed75ea481e7750574) causes a general shut down of the library: all data is written to disk, all identifiers are closed, and all memory used by the library is cleaned up. Another exception occurs on parallel processing systems. Suppose on a parallel system an application has opened a file, a group in the file, and two datasets in the group. If the application uses the [H5Fclose](https://portal.hdfgroup.org/hdf5/develop/group___h5_f.html#gac55cd91d80822e4f8c2a7f04ea71b124) function to close the file, the call will fail with an error. The open group and datasets must be closed before the file can be closed. A third exception is when the file access property list includes the property H5F_CLOSE_STRONG. This property causes the closing of all of the file’s open items when the file is closed with [H5Fclose](https://portal.hdfgroup.org/hdf5/develop/group___h5_f.html#gac55cd91d80822e4f8c2a7f04ea71b124). For more information about [H5close](https://portal.hdfgroup.org/hdf5/develop/group___h5.html#ga8a9fe81dcf66972ed75ea481e7750574), [H5Fclose](https://portal.hdfgroup.org/hdf5/develop/group___h5_f.html#gac55cd91d80822e4f8c2a7f04ea71b124), and [H5Pset_fclose_degree](https://portal.hdfgroup.org/hdf5/develop/group___f_a_p_l.html#ga60e3567f677fd3ade75b909b636d7b9c), see the [HDF5 Reference Manual](https://docs.hdfgroup.org/hdf5/develop/_r_m.html).

The reference manual entries for functions that return identifiers describe what might be returned as follows:

**Returns**:
     Returns an identifier if successful; otherwise returns a negative value.

In other words, a successful operation will return a non-negative identifier which will never be 0 (zero) and will always be a positive value.

## Functions that Return Identifiers

Some of the functions that return identifiers are listed below.

* [H5Acreate](https://portal.hdfgroup.org/hdf5/develop/group___h5_a.html#ga4a76e4e5ab6eb0fd2aa7990d38d55f24)
* [H5Acreate_by_name](https://portal.hdfgroup.org/hdf5/develop/group___h5_a.html#ga004160c28e281455ec48aa7fe557ef8a)
* [H5Aget_type](https://portal.hdfgroup.org/hdf5/develop/group___h5_a.html#ga0b070b714b2e535df2e1cb3005026a44)
* [H5Aopen](https://portal.hdfgroup.org/hdf5/develop/group___h5_a.html#ga59863b205b6d93b2145f0fbca49656f7)
* [H5Aopen_by_idx](https://portal.hdfgroup.org/hdf5/develop/group___h5_a.html#gab1451cdff4f77dcf9feaee83c8179b2d)
* [H5Aopen_by_name](https://portal.hdfgroup.org/hdf5/develop/group___h5_a.html#gadb49a0b5b9798d2e944d877adba8ae10)
* [H5Dcreate](https://portal.hdfgroup.org/hdf5/develop/group___h5_d.html#ga0647ba4bbd26d5230cc07f3a5685b2cf)
* [H5Dcreate_anon](https://portal.hdfgroup.org/hdf5/develop/group___h5_d.html#ga15a77e82383d821fee8ecbf9ab8408cb)
* [H5Dget_access_plist](https://portal.hdfgroup.org/hdf5/develop/group___h5_d.html#ga252c0ddac7a7817bd757190e7398353b)
* [H5Dget_create_plist](https://portal.hdfgroup.org/hdf5/develop/group___h5_d.html#ga8848f14f4aba8e6160c3d8bb7f1be163)
* [H5Dget_space](https://portal.hdfgroup.org/hdf5/develop/group___h5_d.html#gad42a46be153d895d8c28a11ebf5a0d0a)
* [H5Dget_type](https://portal.hdfgroup.org/hdf5/develop/group___h5_d.html#ga7cd04b8332e8a0939b9973fbc500cadb)
* [H5Dopen](https://portal.hdfgroup.org/hdf5/develop/_h5version_8h.html#a7dba2e5b2045f31c0932123ffb54f7a3)
* [H5Ecreate_msg](https://portal.hdfgroup.org/hdf5/develop/group___h5_e.html#ga99a705d98873dcdd1bb6f9d5eebc5afd)
* [H5Ecreate_stack](https://portal.hdfgroup.org/hdf5/develop/group___h5_e.html#ga8bfca811dc01e97b4ab0736dd8775b39)
* [H5Fcreate](https://portal.hdfgroup.org/hdf5/develop/group___h5_f.html#gae64b51ee9ac0781bc4ccc599d98387f4)
* [H5Fopen](https://portal.hdfgroup.org/hdf5/develop/group___h5_f.html#gaa3f4f877b9bb591f3880423ed2bf44bc)
* [H5Freopen](https://portal.hdfgroup.org/hdf5/develop/group___h5_f.html#ga3f213eb05c5419d63ba168c30036e47b)
* [H5Gcreate](https://portal.hdfgroup.org/hdf5/develop/group___h5_g.html#ga187cee27a9fc4f1a311eb19b0522c7b8)
* [H5Gcreate_anon](https://portal.hdfgroup.org/hdf5/develop/group___h5_g.html#gab52641f0736281faaaae4e3039bbb344)
* [H5Gopen](https://portal.hdfgroup.org/hdf5/develop/group___h5_g.html#ga3eca6807deff4f9e51fc5fe0befc2245)
* [H5Oopen](https://portal.hdfgroup.org/hdf5/develop/group___h5_o.html#ga9f635f58c7ddf17f87c253bfbca08bc1)
* [H5Oopen_by_addr](https://portal.hdfgroup.org/hdf5/develop/group___h5_o.html#ga137f3823adab4daaaf8fe87b40453fa2)
* [H5Oopen_by_idx](https://portal.hdfgroup.org/hdf5/develop/group___h5_o.html#gaeb66e5cbb3ca79890fc284a0b06762be)
* [H5Pcreate](https://portal.hdfgroup.org/hdf5/develop/group___p_l_c_r.html#gaf1b11da01d4d45d788c45f8bc5f0cbfa)
* [H5Pget_virtual_srcspace](https://portal.hdfgroup.org/hdf5/develop/group___d_c_p_l.html#ga8319e9386cdb9b3881a8b698edfc78fc)
* [H5Pget_virtual_vspace](https://portal.hdfgroup.org/hdf5/develop/group___d_c_p_l.html#ga6425cabbc055b66e218b4728d6eb911d)
* [H5Rdereference](https://portal.hdfgroup.org/hdf5/develop/group___h5_r.html#ga5dc19b9d1833af66c5e1f819f2c05c4a)
* [H5Rget_region](https://portal.hdfgroup.org/hdf5/develop/group___h5_r.html#ga1702d609e85b9edd3d1e526a0276484f)
* [H5Screate](https://portal.hdfgroup.org/hdf5/develop/group___h5_s.html#gabee514327cba34ca9951b24fa14fb083)
* [H5Screate_simple](https://portal.hdfgroup.org/hdf5/develop/group___h5_s.html#ga8e35eea5738b4805856eac7d595254ae)
* [H5Tcopy](https://portal.hdfgroup.org/hdf5/develop/group___h5_t.html#gaec07efbab84f4e5b4ed22f010786be8e)
* [H5Tcreate](https://portal.hdfgroup.org/hdf5/develop/group___h5_t.html#gaa9afc38e1a7d35e4d0bec24c569b3c65)
* [H5Tdecode](https://portal.hdfgroup.org/hdf5/develop/group___h5_t.html#ga186d7ed91fc0f9c55e19dcd96c7b229b)
* [H5Tget_member_type](https://portal.hdfgroup.org/hdf5/develop/group___c_o_m_p_o_u_n_d.html#gaf5de0eabe28246f040342e275b9a63eb)
* [H5Tget_super](https://portal.hdfgroup.org/hdf5/develop/group___h5_t.html#ga331e8f7b388a50af77294018db788de3)
* [H5Topen](https://portal.hdfgroup.org/hdf5/develop/group___h5_t.html#ga1d14b407603fdcedfbed1f723784c209)
