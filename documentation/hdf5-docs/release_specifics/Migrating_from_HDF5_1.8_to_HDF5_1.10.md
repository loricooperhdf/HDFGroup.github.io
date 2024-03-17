---
title: Migrating from HDF5 1.8 to HDF5 1.10
redirect_from: 
  - /display/HDF5/Migrating+from+HDF5+1.8+to+HDF5+1.10.html
---

# Migrating from HDF5 1.8 to HDF5 1.10

The HDF Group will drop support for HDF5 1.8.\* releases in the summer of 2020. We strongly recommend that our users start migrating their applications as soon as possible and we ask that any problems that are encountered be reported to The HDF Group. Problems can be reported by sending email to help@hdfgroup.org, submitting a request to the [Service Desk Portal](https://jira.hdfgroup.org/servicedesk/customer/portal/2), or posting to the [HDF-FORUM](https://forum.hdfgroup.org/).

Please follow these steps for moving your HDF5 application to HDF5 1.10:

1. Make sure the latest (1.1.0.5+)  version of HDF5 1.10 is installed on your system. You can download the HDF5 1.10 release source code or pre-built binaries from [The HDF Group ftp server](https://support.hdfgroup.org/ftp/HDF5/prev-releases/hdf5-1.10/) and follow the included installation instructions.

2. If on Unix, you can recompile and relink your application with HDF5 1.10, by using the h5cc script with any compiler flags needed for your application. The h5cc script can be found under the bin sub-directory of the HDF5 1.10 installation point.  In cases where your software package has a more complex build system and dependencies, just make sure you point to the new HDF5 1.10.* library when rebuilding your software.

3. If your application or software package has any regression test suite, run it and make sure that all tests pass.

4. Please contact us if you find any problems.

If you have concerns about the files created by the rebuilt application (or software package), you may wish to consider several verification steps to assure that the files can be read by applications built with HDF5 1.8 releases.

1. Use the tools you regularly work with to open, browse, and modify the files created by the rebuilt application (for example, HDFView, MATLAB, IDL, etc.).

2. If you have an HDF5 1.8.* installation on your system, use h5dump from that installation to read files created by the rebuilt application. If you encounter any errors, please rerun h5dump with the  "--enable-error-stack” flag and report the issue.

3. If you have files created by your application that were built with HDF5 1.8, use h5diff from the HDF5 1.8 installation to compare with the files created by the rebuilt application.

If you want to learn more, please see the frequently asked questions (FAQ) below.

## FAQ
### What is the difference between the HDF5 1.8 and HDF5 1.10 releases ?
 
Many new features (e.g., SWMR, VDS, paged allocation, etc.) that required extensions to the HDF5 file format were added to HDF5 1.10.0.
For more information please see the Release Specific Information pages.

### Why one should (or should not) move an application to HDF5 1.10 ?
HDF5 1.8 will not be supported after the May 2020 release, i.e., there will be no more public releases of HDF5 1.8 with security patches, bug fixes, performance improvements and support for OSs and compilers.

In addition, applications originally written for use with HDF5 Release 1.8.x can be linked against the HDF5 Release 1.10.x library, thus taking advantage of performance improvements in 1.10. Users are encouraged to move to the latest releases of HDF5 1.10 or to HDF5 1.12.0 (coming out in the summer of 2019) if they want to stay with the current HDF5 upgrades.

If you are not planning to upgrade your system environment, and a version of HDF5 1.8.* works for you, then there is no reason to upgrade to the latest HDF5. However, if you regularly update your software to use the latest HDF5 1.8 maintenance release, then you need to plan a transition to HDF5 1.10 after the HDF5 1.8 May 2020 release.
 

### Why do I need to rebuild my application with HDF5 1.10?

The HDF5 1.10.* binaries are not ABI compatible with the HDF5 1.8.* binaries due to changes in the public header files and APIs. One has to rebuild an application with the HDF5 1.10.* library. The HDF Group tries hard to maintain ABI compatibility for minor maintenance releases, for example when moving from 1.8.21 to 1.8.22, or 1.10.5 to 1.10.6, but this is not the case when migrating from one major release to another, for example, from 1.8.21 to 1.10.5. If you want to learn more about HDF5 versioning please see HDF5 Library Release Version Numbers.

### Can I migrate my application if I still use the HDF5 1.6 APIs?

Yes, use the -DH5_USE_16_API compiler flag. For more information see the [API compatibility Macros in HDF5](api_comp_macros.md) document.

### Will my old software read files created by an application rebuilt with HDF5 1.10?

If the application built on HDF5 Release 1.10 avoids use of the new features and does not request use of the latest format, applications built on HDF5 Release 1.8.x will be able to read files the first application created.

### Can I use the HDF5 tools I use now to read files created with the new HDF5 1.10 features?

Unfortunately, no. However, we provide a few tools that will help you to “downgrade” the file, so it can be opened and used with tools and applications built with the 1.8 versions of HDF5.

If your application uses SWMR, then the h5format_convert tool can be used to “downgrade” the file to the HDF5 1.8 compatible file format without rewriting raw data.

The h5repack tool with –l flag can be used to repack VDS source datasets into the HDF5 file using contiguous, chunked or compact storage.  The tool can also be used to rewrite the file using the HDF5 1.8 format by specifying the –high=H5F_LIBVER_V18 flag.
