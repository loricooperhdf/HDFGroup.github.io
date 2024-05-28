---
title: Collective Calling Requirements in Parallel HDF5 Applications
redirect_from:
  - display/HDF5/Collective%2BCalling%2BRequirements%2Bin%2BParallel%2BHDF5%2BApplications
---

# Collective Calling Requirements in Parallel HDF5 Applications

## Introduction
This document addresses two topics of concern in a parallel computing environment:
* HDF5 functions that must be called collectively and when
* Properties that must be used in a coordinated manner
The term Macro in the “Additional notes” column indicates that the first item in the “Function” column of the same row is a macro that is selectively mapped to one of the two immediately-following functions. For example, H5Acreate is a macro that can be mapped to either H5Acreate1 or H5Acreate2. This mapping is configurable and is explained in [API Compatibility Macros in HDF5](API compatibility...). The macro structure was introduced at HDF5 Release 1.8.0.

## Always collective
The following functions must always be called collectively.

| API |   Function  | All processes:<br>same datatype<br>& dataspace | All processes:<br>same access<br>properties | All processes:<br>same creation<br>properties | Available<br>in releases since | Additional notes |
| --- | ----------- | ---------------- | ---------------------------------------- | ------------------------------------------ | ------------------------------ | ----------- |
| H5A | H5Acreate<br>H5Acreate1<br>H5Acreate2 | ✓ | ✓ | ✓ | 1.8.x | [Macro](API compatibility...)<br>The function H5Acreate was renamed to H5Acreate1 at Release 1.8.0. |
|     | H5Acreate_by_name                     | ✓ | ✓ | ✓ | 1.8.x | |
|     | H5Adelete                             |   |   |   |       | |
|     | H5Adelete_by_idx                      |   |   |   | 1.8.x | |
|     | H5Adelete_by_name                     |   |   |   | 1.8.x | |
|     | H5Arename                             |   |   |   | 1.6.x | |
|     | H5Arename_by_name                     |   |   |   | 1.8.x | |
|     | H5Awrite                              |   |   |   |       | Because raw data for an attribute is cached locally, all processes must participate in order to guarantee that future H5Aread calls return correct results on all processes. |
| H5D | H5Dcreate<br>H5Dcreate1<br>H5Dcreate2 | ✓ | ✓ | ✓ | 1.8.x | [Macro](API compatibility...)<br>The function H5Dcreate was renamed to H5Dcreate1 at Release 1.8.0. |
|     | H5Dcreate_anon                        | ✓ | ✓ | ✓ | 1.8.x | |
|     | H5Dextend                             |   |   |   |       | All processes must participate only if the number of chunks in the dataset actually changes.<br>All processes must use the same dataspace dimensions. |
|     | H5Dset_extent                         |   |   |   | 1.6.x | All processes must participate only if the number of chunks in the dataset actually changes.<br>All processes must use the same dataspace dimensions. |
| H5F | H5Fclose                              |   |   |   |       | All processes must participate only if this is the last reference to the file identifier. |
|     | H5Fcreate                             |   | ✓ | ✓ |       | |
|     | H5Fflush                              |   |   |   |       | |
|     | H5Fmount                              |   |   |   |       | |
|     | H5Fopen                               |   | ✓ |   |       | |
|     | H5Freopen                             |   |   |   |       | |
|     | H5Funmount                            |   |   |   |       | |
| H5G | H5Gcreate<br>H5Gcreate1<br>H5Gcreate2 |   | ✓ | ✓ | 1.8.x | [Macro](API compatibility...)<br>The function H5Gcreate was renamed to H5Gcreate1 at Release 1.8.0. |
|     | H5Gcreate_anon                        |   | ✓ | ✓ | 1.8.x | |
|     | H5Glink                               |   |   |   |       | |
|     | H5Glink2                              |   |   |   | 1.6.x | |
|     | H5Gmove                               |   |   |   |       | |
|     | H5Gmove2                              |   |   |   | 1.6.x | |
|     | H5Gset_comment                        |   |   |   |       | |
|     | H5Gunlink                             |   |   |   |       | |
| H5I | H5Idec_ref                            |   |   |   | 1.6.x | This function may be called independently if the object identifier does not refer to an object that was collectively opened. |
|     | H5LIinc_ref                           |   |   |   | 1.6.x | This function may be called independently if the object identifier does not refer to an object that was collectively opened. |
| H5L | H5Lcopy                               |   |   |   | 1.8.x | |
|     | H5Lcreate_external                    |   |   | ✓ | 1.8.x | |
|     | H5Lcreate_hard                        |   |   | ✓ | 1.8.x | |
|     | H5Lcreate_soft                        |   |   | ✓ | 1.8.x | |
|     | H5Lcreate_ud                          |   |   | ✓ | 1.8.x | |
|     | H5Ldelete                             |   |   |   | 1.8.x | |
|     | H5Ldelete_by_idx                      |   |   |   | 1.8.x | |
|     | H5Lmove                               |   |   |   | 1.8.x | |
| H5O | H5Ocopy                               |   |   |   | 1.8.x | |
|     | H5Odecr_refcount                      |   |   |   | 1.8.x | |
|     | H5Oincr_refcount                      |   |   |   | 1.8.x | |
|     | H5Olink                               |   |   |   | 1.8.x | |
|     | H5Oset_comment                        |   |   |   | 1.8.x | |
|     | H5Oset_comment_by_name                |   |   |   | 1.8.x | |
| H5R | H5Rcreate                             |   |   |   |       | |
| H5T | H5Tcommit<br>H5Tcommit1<br>H5Tcommit2 |   | ✓ | ✓ | 1.8.x | [Macro](API compatibility...)<br>The function H5Tcommit was renamed to H5Tcommit1 at Release 1.8.0. |
|     | H5Tcommit_anon                        |   | ✓ | ✓ | 1.8.x | |

## Collective, unless target object will not be modified

The following functions must normally be called collectively. If, however, the target object will not be modified, they may be called independently.

| API |   Function  | All processes:<br>same datatype<br>& dataspace | All processes:<br>same access<br>properties | All processes:<br>same creation<br>properties | Available<br>in releases since | Additional notes |
| --- | ----------- | ---------------- | ---------------------------------------- | ------------------------------------------ | ------------------------------ | ----------- |
| H5A | H5Aclose        |   | ✓ |   | 1.8.x | All processes must participate only if all file identifiers for a file have been closed and this is the last outstanding object identifier. |
|     | H5Aopen         |   | ✓ |   | 1.8.x | |
|     | H5Aopen_by_idx  |   | ✓ |   | 1.8.x | |
|     | H5Aopen_by_name |   | ✓ |   | 1.8.x | |
|     | H5Aopen_idx     |   | ✓ |   |       | |
|     | H5Aopen_name    |   | ✓ |   |       | |
| H5D | H5Dclose        |   |   |   | 1.8.x | 	All processes must participate only if all file identifiers for a file have been closed and this is the last outstanding object identifier. |
|     | H5Dopen<br>H5Dopen1<br>H5Dopen2 |   | ✓ |   | 1.8.x | [Macro](API compatibility...)<br>The function H5Dopen was renamed to H5Dopen1 at Release 1.8.0. |
| H5G | H5Gclose        |   |   |   |       | All processes must participate only if all file identifiers for a file have been closed and this is the last outstanding object identifier. |
|     | H5Gopen<br>H5Gopen1<br>H5Gopen2 |   | ✓ |   | 1.8.x | [Macro](API compatibility...)<br>The function H5Gopen was renamed to H5Dopen1 at Release 1.8.0. |
| H5I | H5Iget_file_id  |   |   |   | 1.8.x | |
| H5O | H5Oclose        |   |   |   | 1.8.x | All processes must participate only if all file identifiers for a file have been closed and this is the last outstanding object identifier. |
|     | H5Oopen         |   | ✓ |   | 1.8.x | |
|     | H5Oopen_by_addr |   | ✓ |   | 1.8.x | |
|     | H5Oopen_by_idx  |   | ✓ |   | 1.8.x | |
| H5R | H5Rdereference  |   |   |   |       | |                       
| H5T | H5Tclose        |   |   |   |       | All processes must participate only if the datatype is for a committed datatype, all the file identifiers for the file have been closed, and this is the last outstanding object identifier. |
     H5Topen
H5Topen1
H5Topen2         ✓         1.8.x    [Macro](API compatibility...)
The function H5Topen was renamed to H5Topen1 at Release 1.8.0.

## Properties

The following properties must be set to the same values for an object or link in all cases where the object or link is accessed in a parallel program.
Function    Available in
releases since
Dataset creation properties
H5Pmodify_filter    1.8.x
H5Premove_filter    1.8.x
H5Pset_alloc_time     
H5Pset_chunk     
H5Pset_external     
H5Pset_fill_time     
H5Pset_fill_value     
H5Pset_filter     
H5Pset_fletcher32    1.8.x
H5Pset_layout     
H5Pset_nbit    1.8.x
H5Pset_shuffle     
H5Pset_szip     
 
Dataset transfer properties
H5Pset_btree_ratios     
H5Pset_buffer     
H5Pset_dxpl_mpio     
H5Pset_hyper_cache     
H5Pset_preserve     
 
File access properties
H5Pset_alignment     
H5Pset_cache     
H5Pset_fapl_mpio     
H5Pset_fclose_degree     
H5Pset_gc_references     
H5Pset_latest_format    1.8.x
H5Pset_libver_bounds    1.8.x
H5Pset_mdc_config     
H5Pset_meta_block_size     
H5Pset_small_data_block_size        
H5Pset_sieve_buf_size     
 
Function    Available in
releases since
File creation properties
H5Pset_istore_k     
H5Pset_shared_mesg_index    1.8.x
H5Pset_shared_mesg_nindexes    1.8.x
H5Pset_shared_mesg_phase_change    1.8.x
H5Pset_sizes     
H5Pset_sym_k     
H5Pset_userblock     
 
Group creation properties
H5Pset_ext_link_info    1.8.x
H5Pset_link_creation_order    1.8.x
H5Pset_link_phase_change    1.8.x
H5Pset_local_heap_size_hint    1.8.x
 
Link creation properties
H5Pset_char_encoding    1.8.x
H5Pset_create_intermediate_group       1.8.x
 
Object creation properties
H5Pset_attr_phase_change    1.8.x
H5Pset_attr_creation_order    1.8.x
H5Pset_obj_track_times    1.8.x
 
Object copy properties
H5Pset_copy_object    1.8.x

