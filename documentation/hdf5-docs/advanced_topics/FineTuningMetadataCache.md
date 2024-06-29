---
title: Fine Tuning Metadata Cache
redirect_from:
  - https://docs.hdfgroup.org/archive/support/HDF5/docNewFeatures/NewFeaturesFineTuningMetadataCacheDocs.html
---

# Fine-tuning the Metadata Cache Documentation

This page briefly describes the documentation available for those who want to fine-tune how the metadata cache in HDF5 behaves.

## HDF5 Library APIs
 
|                   |                                                              |
| ----------------- |:------------------------------------------------------------ |
| [H5Pget_evict_on_close](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#ga12789fcfeaea073c13202e6401f404a6) | Retrieves the property list setting that determines whether an HDF5 object will be evicted from the library's metadata cache when it is closed. |
| [H5Pset_evict_on_close](https://docs.hdfgroup.org/hdf5/v1_14/group___j_h5_p.html#ga50cff2ac2560cee0471fcbf15dcb86c6) | Controls the library's behavior of evicting metadata associated with a closed object. |
| [H5Pget_mdc_image_config](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#gaaa18d59ee9efb12626410b1638f76f00) | Retrieves the metadata cache image option setting from a file access property list. |
| [H5Pset_mdc_image_config](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#ga65cf9fea33d1324009efc2d5db848434) | Sets the metadata cache image option for a file access property list. |
| [H5Fget_mdc_image_info](https://docs.hdfgroup.org/hdf5/v1_14/group___m_d_c.html#ga7b37da15ff80c4aa5c275649f1f45b0a) | Gets information about a metadata cache image for a file if it exists. |
| [H5Fget_metadata_read_retry_info](https://docs.hdfgroup.org/hdf5/v1_14/group___s_w_m_r.html#gaa80bd62f19993e414e383db7d1623e5f) | Retrieves the collection of read retries for metadata items with checksum. |
| [H5Pget_metadata_read_attempts](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#ga670948d56435920f1e1c2e88b823935e) | Retrieves the number of read attempts from a file access property list. |
| [H5Pset_metadata_read_attempts](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#gab827cef16ec569c87cec94a8b3f350c5) | Sets the number of read attempts in a file access property list. |
| [H5Dflush](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_d.html#ga4a2175a62baa1e35ad2467bb1fdff1f7) | Causes all buffers associated with a dataset to be immediately written to disk without removing the data from the cache. |
| [H5Drefresh](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_d.html#ga3c1ea7e5db3f62d9cf03dd62d1fb08da) | Causes all buffers associated with a dataset to be cleared and immediately re-loaded with updated contents from disk storage. |
| [H5Gflush](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_g.html#ga1d55dbf931f8003bb329c4340b8fe4d6) | Causes all buffers associated with a group to be immediately flushed to disk without removing the data from the cache. |
| [H5Grefresh](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_g.html#ga0a8bdd0eb1b001222c27d3d39a909840) | Causes all buffers associated with a group to be cleared and immediately re-loaded with updated contents from disk storage. |
| [H5Oflush](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_o.html#gad99f35048cba4534b6393214684f090f) | Causes all buffers associated with an object to be immediately flushed to disk without removing the data from the cache. |
| [H5Orefresh](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_o.html#gaf0318b68be9ab23a92b8a6bee0af9e2f) | Causes all buffers associated with an object to be cleared and immediately re-loaded with updated contents from disk storage. |
| [H5Tflush](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_t.html#gafd60389b49e1e5e6f37caffbe6cbf6e5) | Causes all buffers associated with a committed datatype to be immediately flushed to disk without removing the data from the cache. |
| [H5Trefresh](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_t.html#ga5bc56f6b85e114829dc12d6b18d66f4d) | Causes all buffers associated with a committed datatype to be cleared and immediately re-loaded with updated contents from disk storage. |
| [H5Fget_intent](https://docs.hdfgroup.org/hdf5/v1_14/group___h5_f.html#ga466179d7783d256329c2e3110055a16c) | Determines the read/write or read-only status of a file. |
 
## Logging APIs
 
|                   |                                                              |
| ----------------- |:------------------------------------------------------------ |
| [H5Pset_mdc_log_options](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#ga4d7206c5679d7243410058eceae59b2c) | Sets metadata cache logging options. |
| [H5Pget_mdc_log_options](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#gaa3a1ca6e294cc5074933239cc3d0e4a3) | Gets metadata cache logging options. |
| [H5Fstart_mdc_logging](https://docs.hdfgroup.org/hdf5/v1_14/group___m_d_c.html#ga378fb5863071278b47070cf205f53e67) | Starts logging metadata cache events if logging was previously enabled. |
| [H5Fstop_mdc_logging](https://docs.hdfgroup.org/hdf5/v1_14/group___m_d_c.html#ga78627b23010f82002b837f4d312bf234) | Stops logging metadata cache events if logging was previously enabled and is currently ongoing. |
| [H5Fget_mdc_logging_status](https://docs.hdfgroup.org/hdf5/v1_14/group___m_d_c.html#ga998ebdc7b5190cf3d0fdf2fbe71e9780) | Gets the current metadata cache logging status. |
 
## Fine-tuning the Metadata Cache Design Documents and Information

The design documents listed below provide background information for the functions that have been developed to provide better control of the metadata cache and why better control might be useful.
 
[Fine-grained Control of Metadata Cache Flushes (PDF)](https://docs.hdfgroup.org/hdf5/rfc/RFC%20H5Ocork%20v5%20new%20fxn%20names.pdf) - This document describes some new functions which allow dynamic, fine-grained flush control of the entire metadata cache and the caches related to individual HDF5 objects.
 
[Read Attempts for Metadata with Checksum (PDF)](https://docs.hdfgroup.org/hdf5/rfc/RFC-Read-Attempts-for-Metadata-with-Checksum-v3.pdf) - The HDF5 Library encounters intermittent checksum failures from reading metadata of an HDF5 file opened with single-writer/multiple-reader (SWMR) access. The failure is from a checksum check that does not reflect the data read. This document describes the modifications to the library that address this problem.
 
[Metadata Cache Image (PDF)](https://docs.hdfgroup.org/hdf5/rfc/cache_image_RFC_150929-QAK.docx.pdf) - This document describes the metadata cache image feature and how it improves performance by writing the metadata cache in a single block on file close, and then populating the cache with the contents of this block on file open. This avoids the many small I/O operations that would otherwise be required on file open and close.
 
Metadata Cache Evict on Close - This feature will cause all metadata for an object to be evicted from the cache as long as metadata is not referenced from any other open object. This can relieve memory pressure on an application or system caused by a large amount of metadata in the metadata cache. See the [H5Pget_evict_on_close](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#ga12789fcfeaea073c13202e6401f404a6) and [H5Pset_evict_on_close](https://docs.hdfgroup.org/hdf5/v1_14/group___f_a_p_l.html#gaa44cc0e592608e12082dad9305b3c74d) APIs for more details.
 
[Metadata Cache Logging (PDF)](https://docs.hdfgroup.org/hdf5/rfc/Design-MetadataCache-Logging-THG20140224-v4.pdf) - This document describes the improvements made to the library’s metadata cache logging facility. The changes include APIs that can be used to control logging operations and the format of log messages.
 
[Flush Dependency Testing (PDF)](https://docs.hdfgroup.org/hdf5/rfc/Design-HDF5-FlushDependencyTesting-20130630-v1.1.pdf) - This document considers how to design tests for flush dependencies of metadata cache items for single-writer/multiple-reader (SWMR) access.
 
## Tools

The following tool was modified to support the Metadata Cache Image feature.

h5clear	The "-m" and "--image" flags were added to h5clear to close a cache image if it exists.

