---
title: HDF5 Application Developer's Guide

redirect_from:
    display/HDF5/HDF5+Application+Developer's+Guide
    display/HDF5/General+Topics+in+HDF5
    display/HDF5/Advanced+Topics+in+HDF5
---

# HDF5 Application Developer's Guide

## General Topics in HDF5

##\*\*\* Work-in-Progress \*\*\*

| Topic                         | Description                                                  |
| ----------------------------- | ------------------------------------------------------------ |
| [Chunking in HDF5](hdf5_topics/chunking_in_hdf5.md) | Detailed information regarding chunking in HDF5 |
| [Environment Variables Used by HDF5]() | Environment variables that can be used when building or using HDF5 |
| [Using Compression in HDF5]() | Resources regarding compression |
| [Improving I/O Performance When Working with HDF5 Compressed Datasets](hdf5_topics/HDF5ImprovingIOPerformanceCompressedDatasets.pdf) | A description of the factors that should be considered when storing compressed data in HDF5 files and how to tune those parameters to optimize the I/O performance of an HDF5 application when working with compressed datasets (PDF) |
| [Parallel HDF5]() | Information on Parallel HDF5 |
| [Fill Value and Space Allocation Behavior]() | A table summarizing of the behavioral interactions of HDF5 fill value and storage allocation settings  |
| [H5Fill Behavior]() | The library's fill value behavior for property list settings |
| [SZIP Compression in HDF5]() | A description of SZIP compression in HDF5, H5Pset_szip, terms of use and copyright notice, and references  |
| [Using Identifiers](hdf5_topics/UsingIdentifiers.md) | Description of how identifiers work |
| [UTF-8 encoding in HDF5 applications](hdf5_topics/UsingUTF-8EncodinginHDF5Apps.md) | Information on using UTF-8 encoding in HDF5 applications |
| [HDF5 Dimension Scale Specification and Design Notes](hdf5_topics/H5DS_Spec.pdf) | |

<!--- In doxygen/technical notes -->
<!--- | [HDF5 Library Release Versions Numbers]() | A description of HDF5 library release version numbering | -->


<!---
Parallel HDF5   Information on Parallel HDF5

Fill Value and Space Allocation Behavior    A table summarizing of the behavioral interactions of HDF5 fill value and storage allocation settings

H5Fill Behavior The library's fill value behavior for property list settings

SZIP Compression in HDF5    A description of SZIP compression in HDF5, H5Pset_szip, terms of use and copyright notice, and references

HDF5 Library Release Versions Numbers   A description of HDF5 library release version numbering

Using Identifiers   Description of how identifiers work

-->
<!---
### [New Features](hdf5_topics/feature.md)
### [New Features](hdf5_topics/feature.md)
### [New Features](hdf5_topics/feature.md)
-->

## Advanced Topics in HDF5

### [HDF5 File Image Operations](https://docs.hdfgroup.org/hdf5/rfc/HDF5FileImageOperations.pdf)
### [Copying Committed Datatypes with H5Ocopy](https://docs.hdfgroup.org/hdf5/develop/group___o_c_p_p_l.html)
### [HDF5 Data Flow Pipeline for H5Dread](advanced_topics/data_flow_pline_H5Dread.md)
### [Introduction to Single-Writer_Multiple-Reader (SWMR)](advanced_topics/intro_SWMR.md)
### [Introduction to the Virtual Dataset - VDS](advanced_topics/intro_VDS.md)
### [Modified Region Writes](advanced_topics/ModifiedRegionWrites.pdf)
<!---
### [New Features](advanced_topics/feature.md)
### [New Features](advanced_topics/feature.md)
### [New Features](advanced_topics/feature.md)
-->
