# Compiling HDF5 Applications

## Tools and Instructions on Compiling

The h5cc/h5fc/h5c++ compile scripts are included when building with configure. Simplified versions of these compile scripts have also been added to CMake for Linux ONLY. If you are using CMake, also see [Building HDF5 with CMake](https://raw.githubusercontent.com/HDFGroup/hdf5/hdf5_1_14_3/release_docs/INSTALL_CMake.txt).

### Windows

#### CMake:

See [Building HDF5 with CMake](https://raw.githubusercontent.com/HDFGroup/hdf5/hdf5_1_14_3/release_docs/INSTALL_CMake.txt) for information on compiling an application with CMake. Also see `USING_CMake_Examples.txt` for building the examples that are included with the pre-built binaries. These examples can be obtained separately from the Building HDF5 with CMake page under Compiling an Application.

#### Visual Studio:

See the `USING_HDF5_VS.txt` file in the HDF5 source code for building an application with Visual Studio.

### Unix
When the library is built with configure (autotools), the following compile scripts are included:

| *h5cc:* |   compile script for HDF5 C programs| 
| *h5fc:*   | compile script for HDF5 F90 programs| 
|    *h5c++:*  |  compile script for HDF5 C++ programs| 

These scripts are included for CMake on Linux, but they are very simple. However, they can be used to compile single file applications, such as those included in the tutorial. See [Building HDF5 with CMake](https://raw.githubusercontent.com/HDFGroup/hdf5/hdf5_1_14_3/release_docs/INSTALL_CMake.txt) for information on compiling an application with CMake.

#### Examples of Using the Unix Compile Scripts:

Following are examples of compiling and running an application with the Unix compile scripts:
```
   h5fc myprog.f90
   ./a.out

   h5cc -o myprog myprog.c
   ./myprog
```

To see the libraries linked in with a compile script use the -show option. For example, if using `h5cc` type:
   `h5cc -show myprog.c`

##### NOTES:

* You are not required to use these compile scripts.
* You can use a compile script in place of a compiler in a makefile.
* ALL of your libraries should be built with the same compiler to avoid problems.

##### Makefiles:

We encourage users to use the compile scripts. Following are example makefiles for those users who do not wish to use the scripts. These makefiles are only minimally tested:

    Fortran Makefile
    C Makefile

##### Detailed Description of Unix Compile Scripts:

The `h5cc`, `h5c++`, and `h5fc` compile scripts come with the HDF5 source code and binary distributions (include files, libraries, and utilities) for the platforms we support. The h5c++ and h5fc utilities are ONLY present if the library was built with C++ and Fortran.

After you have installed your binaries in their final destination, you can use the scripts to compile. However, if using the pre-built binaries or moving the binaries to a new location, you must:

* Run `./h5redeploy` to change site specific paths in the scripts.
* Edit each script and update the paths for the external libraries in LDFLAGS and CPPFLAGS (ZLIB, SZIP).

You may also need to change other variables in the scripts, depending on how things are set up on your system. Here are some of the variables to check:

  prefix      - Path to the HDF5 top level installation directory
  CCBASE      - Name of the alternative C compiler
  CLINKERBASE - Name of the alternative linker
  LIBS        - Libraries your application will link with

For information on settings used to build the HDF5 libraries, please refer to:

    ./lib/libhdf5.settings 
    ./lib/libhdf5_fortran.settings (if Fortran enabled)  
    ./lib/libhdf5_cpp.settings (if C++ enabled)

## HDF5 Libraries

Following are the libraries included with HDF5. Whether you are using the Unix compile scripts or Makefiles, or are compiling on Windows, these libraries are or may need to be specified. The order they are specified is important:

    libhdf5_hl_cpp.a    - HDF5 High Level C++ APIs 
    libhdf5_cpp.a       - HDF5 C++ Library  
    libhdf5hl_fortran.a - HDF5 High Level Fortran APIs
    libhdf5_fortran.a   - HDF5 Fortran Library
    libhdf5_hl.a        - HDF5 High Level C APIs
    libhdf5.a           - HDF5 C Library

The -show option for h5cc, hc++ and h5fc will display the libraries in the correct order.

### External Libraries:

    libsz.a             - SZIP Compression Library
    libz.a              - ZLIB or DEFLATE Compression Library
    (any other system libraries, such as -lrt -lm ...)

You may also see shared versions of these libraries.

The pre-compiled binaries, in particular, are built (if at all possible) with these libraries as well as with SZIP and ZLIB. If using shared libraries you may need to add the path to the library to LD_LIBRARY_PATH.
