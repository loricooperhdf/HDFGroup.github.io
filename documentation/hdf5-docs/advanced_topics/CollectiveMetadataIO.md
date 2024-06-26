---
title: Collective Metadata I/O
redirect_from:
  - 
---

# Collective Metadata I/O

The purpose of this page is to briefly describe the new HDF5 Collective Metadata I/O feature and provide a gateway to available documentation. The page includes the following sections:

* <a href="#overview">Collective Metadata I/O Overview</a>

* <a href="#resource">Collective Metadata I/O User and Resource Documents</a>

* <a href="#apis">HDF5 Library APIs</a>

<h2 id="overview">Collective Metadata I/O Overview</h2>

Calls for HDF5 metadata can result in many small reads and writes. On metadata reads, collective metadata I/O can improve performance by allowing the library to perform optimizations when reading the metadata, by having one rank read the data and broadcasting it to all other ranks.

Collective metadata I/O improves metadata write performance through the construction of an MPI derived datatype that is then written collectively in a single call.

<h2 id="resource">Collective Metadata I/O User and Resource Documents</h2>

HDF5 Collective Metadata I/O User Document (This document is not yet available.)

Until an *HDF5 Collective Metadata I/O User Document* becomes available, users may find the following resources helpful:

RFC: Collective Metadata Reads ([PDF]([1]/RFC-CollectiveMetadataReads.pdf))

RFC: Collective Metadata Writes ([PDF]([1]/RFC-CollectiveMetadataWrites.pdf))

Taken together, these papers discuss the motivation, design, implementation, and API for HDF5’s Collective Metadata I/O feature.

<h2 id="apis">HDF5 Library APIs</h2>

### New Collective Metadata I/O Functions

|                   |                                                              |
| ----------------- | ------------------------------------------------------------ |
| [H5Pset_coll_metadata_write]([2]/group___f_a_p_l.html#ga6380f9929cf42c8203813f7e72dde35c) | Establishes I/O mode property setting, collective or independent, for metadata writes |
| [H5Pget_coll_metadata_write]([2]/group___f_a_p_l.html#gac83ab4e788a5b6e0d578f40ca67d8d00) | Retrieves I/O mode property setting for metadata writes | 
| [H5Pset_all_coll_metadata_ops]([2]/group___g_a_p_l.html#ga5bc0b1fc7e1e3961bf0b441e722949eb) | Establishes I/O mode, collective or independent, for metadata read operations | 
| [H5Pget_all_coll_metadata_ops]([2]/group___g_a_p_l.html#ga8792cbe7eeace1382f588ed12a92092a) | Retrieves I/O mode for metadata read operations |

### Additional API Reference

#### Functions with No Access Property List Parameter that May Generate Metadata Reads

Currently there are several operations in HDF5 that can issue metadata reads from the metadata cache, but that take no property list. It is therefore not possible set a collective requirement individually for those operations. The only solution with the HDF5 1.10.0 release is to set the collective requirement globally on H5Fopen or H5Fcreate for all metadata operations to be collective.

The following is a list of those functions in the HDF5 library. This list is integral to the discussion in the H5Pset_all_coll_metadata_ops entry:

|                   |
| ----------------- |
| [H5Awrite]([2]/group___h5_a.html#gab70871e205d57450c83efd9912be2b5c) |
| [H5Aread]([2]/group___h5_a.html#gaacb27a997f7c98e8a833d0fd63b58f1c) |
| [H5Arename]([2]/group___h5_a.html#ga490dcd6db246c1fda7295badfce28203) |
| [H5Aiterate2]([2]/group___h5_a.html#ga9315a22b60468b6e996559b1b8a77251) |
| [H5Adelete]([2]/group___h5_a.html#gada9fa3d6db52329f1fd55662de6ff6ba) |
| [H5Aexists]([2]/group___h5_a.html#ga293b5be270d90cd5e47f782ca9aec80b) |
|  |
| [H5Dget_space_status]([2]/group___h5_d.html#ga7639ef5c12cb906c71670ce73b856a4c) |
| [H5Dget_storage_size]([2]/group___h5_d.html#gafb249479a493e80891f0c7f5d8a91b00) |
| [H5Dset_extent]([2]/group___h5_d.html#gad31e1e0129f4520c531ce524de2a056f) |
| [H5Ddebug](url) |
| [H5Dclose]([2]/group___h5_d.html#gae47c3f38db49db127faf221624c30609) |
| [H5Dget_get_create_plist](url) |
| [H5Dget_space]([2]/group___h5_d.html#gad42a46be153d895d8c28a11ebf5a0d0a) (when dataset is a virtual dataset) |
|  |
| [H5Gget_create_plist]([2]/group___h5_g.html#ga0b959a53cbffa48f5d68ce33b43b7ed8) |
| [H5Gget_info]([2]/group___j_h5_g.html#gaece6d1057c42630d336dad0f3915b337) |
| [H5Gclose]([2]/group___h5_g.html#ga8dbe20b390d2504f0bd3589ed8f4e221) |
|  |
| [H5Literate]([2]/group___j_h5_l.html#ga4e9e84159546db7f17d3d0c6ee709371) |
| [H5Lvisit]([2]/group___t_r_a_v.html#gac0558936502924d9e898d8b6e041ed69) |
|  |
| [H5Rcreate]([2]/group___h5_r.html#ga0ac6997b5de26b11d91a95de2869950d) |
| [H5Rdereference2]([2]/group___h5_r.html#ga9b09586f7b6ec708434dd8f95f58a9b7) (when reference is an object reference) |
| [H5Rget_region]([2]/group___h5_r.html#ga1702d609e85b9edd3d1e526a0276484f) |
| [H5Rget_obj_type2]([2]/group___h5_r.html#ga766e39a76bcdd68dc514425353eff807) |
| [H5Rget_name]([2]/group___h5_r.html#ga4c112c388f697324270fd085100dccaa) |
|  |
| [H5Ocopy]([2]/group___h5_o.html#gaa94449be6f67f499be5ddd3fc44f4225) |
| [H5Oopen_by_addr]([2]/group___h5_o.html#ga137f3823adab4daaaf8fe87b40453fa2) |
| [H5Oincr_refcount]([2]/group___h5_o.html#ga2086bad6c3cd2a711c306a48c093ff55) |
| [H5Odecr_refcount]([2]/group___h5_o.html#ga60c20da5e244c28a653d4fa23d316b44) |
| [H5Oget_info]([2]/group___h5_o.html#gaf4f302a33faba9e1c2b5f64c62ca4ed5) |
| [H5Oset_comment]([2]/group___h5_o.html#ga8b5cf8e916204e29616516046121f631) |
| [H5Ovisit]([2]/group___h5_o.html#ga5ce86255fcc34ceaf84a62551cd24233) |
|  |
| [H5Fis_hdf5]([2]/group___h5_f.html#ga6055c2ea3438bd4aaf221eba66843225) |
| [H5Fflush]([2]/group___h5_f.html#gae686870f0a276c4d06bbc667b2c24124) |
| [H5Fclose]([2]/group___h5_f.html#gac55cd91d80822e4f8c2a7f04ea71b124) |
| [H5Fget_file_image]([2]/group___h5_f.html#gadc53f4e76b1199cb5d2a8cb7fbb114ad) |
| [H5Freopen]([2]/group___h5_f.html#ga3f213eb05c5419d63ba168c30036e47b) |
| [H5Fget_freespace]([2]/group___h5_f.html#ga3ef2673183567543346668a8f1eca2e9) |
| [H5Fget_info2]([2]/group___h5_f.html#gaced8c09c1559636a9c3f33dff3f4520e) |
| [H5Fget_free_sections]([2]/group___h5_f.html#gab9cbf1a45f9dcda34b43f985b7848434) |
| [H5Fmount]([2]/group___h5_f.html#ga7c4865fd36ee25d839725252150bb53b) |
| [H5Funmount]([2]/group___h5_f.html#gae8f807d3f04a33f132ffb6c5295e897f) |
|  |
| [H5Iget_name]([2]/group___h5_i.html#ga9c84a8dc29566b82b6d1ff7a6e6828f1) |
|  |
| [H5Tget_create_plist]([2]/group___h5_t.html#ga6802c22c6e90216aa839a4a83909a54c) |
| [H5Tclose]([2]/group___h5_t.html#gafcba4db244f6a4d71e99c6e72b8678f0) |
|  |
| [H5Zunregister]([^2]/group___h5_z.html#ga6b8bcdde70c9256c50c7c62ba66380f8) |
| H5Zunregister([^2]/group___h5_z.html#ga6b8bcdde70c9256c50c7c62ba66380f8) |

In addition, most deprecated functions fall into this category.

The HDF Group may address the above limitation in a future major release, but no decision has been made at this time. Such a change might, for example, include adding new versions of some or all the above functions with an extra property list parameter to allow an individual setting for the collective calling requirement.

[1]: https://docs.hdfgroup.org/hdf5/rfc
[2]: https://portal.hdfgroup.org/hdf5/develop
