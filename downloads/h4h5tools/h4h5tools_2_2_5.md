# h4h5tools 2.2.5

## Release Information

| Version | h4h5tools 2.2.5 |
| --- | --- | 
| Release Date | 3/10/2020|
| Additional Release Information | Documentation |
|| Release Notes | 


## Files 
  
| File | Type | Install Instructions |
| ---- | ---- | ---- | 


| File | Operating System | Compilers | Comment | sha256 file | 
| ---- | ---- | ---- | ---- | ---- | 
| h4h5tools-2.2.5.tar.gz | Source release || Gzipped source tarball| h4h5tools-2.2.5-src.sha256 |
| h4h5tools-2.2.5.zip | Source release || Windows zip file| " | 
| h4h5tools-1.10.6-2.2.5-centos7_64.tar.gz | Linux 3.10 CentOS 7 x86_64 | gcc 4.8.5| Pre-built tar file (CMake)| h4h5tools-1.10.6-2.2.5-centos7_64.tar.gz.sha256 |
| h4h5tools-1.10.6-2.2.5-osx1013_64-clang.tar.gz | macOS 10.13.6 | clang/clang++ 10.0.0 | Pre-built tar file (CMake) | h4h5tools-1.10.6-2.2.5-osx1013_64-clang.tar.gz.sha256 |
| h4h5tools-1.10.6-2.2.5-win10_64-vs15.zip | Windows 10 64-bit | VS 2017 | Windows zip file (CMake) | h4h5tools-1.10.6-2.2.5-win10_64-vs15.zip.sha256 |
| h4h5tools-1.10.6-2.2.5-win10_64-vs14.zip | Windows 10 64-bit | VS 2015 | Windows zip file (CMake) | h4h5tools-1.10.6-2.2.5-win10_64-vs14.zip.sha256 |
| h4h5tools-1.10.6-2.2.5-win7_64-vs14.zip | Windows 7 64-bit | VS 2015 | Windows zip file (CMake)| h4h5tools-1.10.6-2.2.5-win7_64-vs14.zip.sha256 |
| h4h5tools-1.10.6-2.2.5-win7_64-vs14.zip | Windows 7 64-bit | VS 2015 | Windows zip file (CMake) | h4h5tools-1.10.6-2.2.5-win7_64-vs14.zip.sha256 |

## Release Notes

Please note that macOS version 10.13.6 was also tested (with clang/clang++ 10.0.0).

H4H5TOOLS version 2.2.5 released on 2020-03-10
================================================================================

1. Introduction
===============

This document describes the H4H5TOOLS and contains information on
the platforms tested and limitations. The H4H5TOOLS distribution includes
three products: H4toH5 conversion library, H4toH5 conversion utility,
and H5toH4 conversion utility.

Both the H4toH5 conversion library and the H4toH5 conversion utility follow
the HDF4 to HDF5 mapping document.  This document can be found at:
    https://portal.hdfgroup.org/display/HDF5/Mapping+HDF4+Objects+to+HDF5+Objects

The H4toH5 conversion library user guide and reference manual can be found at:
    https://portal.hdfgroup.org/display/support/h4h5+User%27s+Guide
    https://portal.hdfgroup.org/display/support/h4h5+Reference+Manual

If you have any questions or comments, please send them to:
    help@hdfgroup.org


2. Platforms Tested
===================
This release is tested with HDF4 v4.2.15 and HDF5 v1.8.21 and v1.10.6 on the following
platforms and compilers:

    Linux 2.6.32-696.16.1.el6.ppc64 gcc (GCC) 4.4.7 20120313 (Red Hat 4.4.7-18)
    #1 SMP ppc64 GNU/Linux        IBM XL C/C++ V13.1
    (ostrich)

    Linux 3.10.0-327.10.1.el7   GNU C (gcc)
    #1 SMP x86_64 GNU/Linux       compilers:
    (kituo/moohan)                Version 4.8.5 20150623 (Red Hat 4.8.5-4)
                                    Version 4.9.3, Version 5.2.0,
                                  Intel(R) C (icc)
                                  compilers:
                                     Version 17.0.0.098 Build 20160721

    SunOS 5.11 32- and 64-bit     Sun C 5.12 SunOS_sparc
    (emu)

    Windows 7                     Visual Studio 2015 (cmake)

    Windows 7 x64                 Visual Studio 2015 (cmake)
                                  Visual Studio 2015 w/ Intel C (cmake)

    Windows 10                    Visual Studio 2015 (cmake)

    Windows 10 x64                Visual Studio 2015 (cmake)
                                  Visual Studio 2017 (cmake)
                                  Visual Studio 2019 (cmake)

    Mac OS X Yosemite 10.10.5     Apple clang/clang++ version 6.1 from Xcode 7.0
    64-bit
    (osx1010dev/osx1010test)      Intel icc version 15.0.3

    Mac OS X El Capitan 10.11.6   Apple clang/clang++ version 7.3.0 from Xcode 7.3
    64-bit
    (osx1011dev/osx1011test)      Intel icc version 16.0.2

    Mac OS Sierra 10.12.6         Apple LLVM version 8.1.0 (clang/clang++-802.0.42)
    64-bit
    (kite)                        Intel icc 17.0.2

2.1 Optional Features
====================
The h4toh5 command-line utility, with the options (-eos -nc4 -nc4strict)
that can convert HDF-EOS2 to netCDF-4, is tested with HDF4 V4.2.15,
HDF5 1.10.6, HDF-EOS2 2.20, and ncdump from the netCDF 4.7.3 
distribution on the following platform and compiler:

   Linux 3.10 (x86_64), gcc 4.8.5
   Linux 2.6.32(x86_64) gcc 4.4.7
   MacOS X Catalina 10.15.3 Apple LLVM version 11.0.0 (clang-1100.0.33.17)


3. New Features and Bug Fixes Since Version 2.2.4
=================================================
   Configuration
   -------------
    - Update CMake for VS2019 support

      CMake added support for VS2019 in version 3.15. Changes to the CMake
      generator setting required changes to scripts. Also updated version
      references in CMake files as necessary.

      (ADB - 2019/11/18, HDFFR-1581)

    - Update CMake tests to use FIXTURES

      CMake test fixtures allow setup/cleanup tests and other dependency
      requirements as properties for tests. This is more flexible for
      modern CMake code.

      (ADB - 2019/07/23, HDFFV-10529)

    - Windows PDB files are always installed

      There are build configuration or flag settings for Windows that may not
      generate PDB files. If those files are not generated then the install
      utility will fail because those PDB files are not found. An optional
      variable, DISABLE_PDB_FILES, was added to not install PDB files.

      (ADB - 2019/07/17, HDFFV-10424)

    - Add mingw CMake support with a toolchain file

      There has been a number of mingw issues that has been linked under
      HDFFV-10845. It has been decided to implement the CMake cross-compiling
      technique of toolchain files. We will use a linux platform with the mingw
      compiler stack for testing. Only the C language is fully supported, and
      the error tests are skipped. The C++ language works for static but shared
      builds has a shared library issue with the mingw Standard Exception Handling
      library, which is not available on Windows. Fortran has a common cross-compile
      problem with the fortran configure tests.

      (ADB - 2019/07/12, HDFFV-10845, HDFFV-10595)

    - Windows PDB files are installed incorrectly

      For static builds, the PDB files for windows should be installed next
      to the static libraries in the lib folder. Also the debug versions of
      libraries and PDB files are now correctly built using the default
      CMAKE_DEBUG_POSTFIX setting.

      (ADB - 2019/07/09, HDFFV-10581)

    - Add option to build only shared libs

      A request was made to prevent building static libraries and only build
      shared.  A new option was added to CMake, ONLY_SHARED_LIBS, which will
      skip building static libraries. Certain utility functions will build with
      static libs but are not published. Tests are adjusted to use the correct
      libraries depending on SHARED/STATIC settings.

      (ADB - 2019/06/12, HDFFV-10805)

   Library
   -------

   Tools
   -----
    - Fixed potential memory leaking issues.  

      (KY - 2019/07/18 HFRHFVTOOLS-147)
     
     

   Documentation
   -------------
   - No major update


4. Known problems
=================

   - [None]

5. Optional HDF-EOS2/netCDF-4 Verifier
======================================
An optional HDF-EOS2/netCDF-4 verifier utility is available with the
2.2.4 release in the subdirectory misc/verify_eos2nc4/.  See the
README.txt file under that directory.

6. Limitations
==============
1. h4toh5: For the option -na(h4toh5 -na), if a dimension name is assigned to 
           an HDF4 SDS dimension, that dimension must have a dimension scale.
           Otherwise, an error will be generated.
2. h5toh4: Check the h5toh4_limitation.txt under /release_docs.



CMake vs. Autotools installations
=================================
While both build systems produce similar results, there are differences.
Each system produces the same set of folders on linux (only CMake works
on standard Windows); bin, include, lib and share. Autotools places the
COPYING and RELEASE.txt file in the root folder, CMake places them in
the share folder.

The bin folder contains the tools and the build scripts (autotools only).
Additionally, CMake creates dynamic versions of the tools with the suffix
"-shared". Autotools installs one set of tools depending on the
"--enable-shared" configuration option.
  build scripts
  -------------
  Autotools: h4h5cc

The include folder holds the header files.

The lib folder contains the library files.

The share folder will have the most differences because CMake builds include
a number of CMake specific files for support of CMake's find_package and support
for the H4H5 Examples CMake package.
