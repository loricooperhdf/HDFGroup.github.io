If using the CTest script and configuration method to build HDF4, you can easily change the build options by either specifying the options on the command line or adding them to the options file, HDF4options.cmake.

## Change options from the command line

As described on the [Building HDF4 with CMake](/documentation/hdf4-docs/building_hdf4_with_cmake.html) page, batch files for Windows and a shell script for Unix are provided for building HDF4. These files each contain a command that gets executed on the command line to build HDF4. They can be edited to add or change these options to the build command:

| Option | Purpose |  
| --- | ---| 
| BUILD_GENERATOR	| Which CMake generator to use (required) |
| INSTALLDIR | Root folder where HDF4 is installed |
| CTEST_CONFIGURATION_TYPE | Release, Debug, RelWithDebInfo |
| CTEST_SOURCE_NAME | Name of source folder (eg. hdf-4.2.N) |

These are described at the top of the `HDF4config.cmake` file.

## Change options with the options file

The `HDF4options.cmake` file is provided so that users can change build options without modifying the configuration file. It gets included by the configuration file and it overrides the settings in the configuration file.

Options can be set by using the following format:
    `set(ADD_BUILD_OPTIONS "${ADD_BUILD_OPTIONS} -DXXX:YY=ZZZZ")`
    
The `config/cmake/cacheinit.cmake` file has a complete list of the options that can be used to build HDF4. (Section V in the `INSTALL_CMake.txt` file lists the default CMake options used by HDF4.)

Several options are included in the `HDF4options.cmake` file, such as the options to turn off ZLIB or SZIP. Additional options can be added to this file, as needed. Common configure options that can be turned off or on in the `HDF4options.cmake` file are listed below.

## Common CMake and configure Options

There are numerous CMake options available to users, many of which correspond directly to configure options. Below are a few important options and how to change them in the configuration file. The corresponding configure option is also shown:

| Option | Configure | Cmake | 
| --- | --- | --- | 
| Build shared libraries | --enable-shared | `set(ADD_BUILD_OPTIONS "${ADD_BUILD_OPTIONS} -DBUILD_SHARED_LIBS:BOOL=ON")` |
| Build HDF4 Fortran library | --enable-fortran | `set(ADD_BUILD_OPTIONS "${ADD_BUILD_OPTIONS} -DHDF4_BUILD_FORTRAN:BOOL=ON") |
| Disable ZLIB filter | --with-zlib	| `set(ADD_BUILD_OPTIONS "${ADD_BUILD_OPTIONS} -DHDF4_ENABLE_Z_LIB_SUPPORT:BOOL=OFF")` | 
| Disable SZIP filter | --with-szlib | `set(ADD_BUILD_OPTIONS "${ADD_BUILD_OPTIONS} -DHDF4_ENABLE_SZIP_SUPPORT:BOOL=OFF")` <br> `set(ADD_BUILD_OPTIONS "${ADD_BUILD_OPTIONS} -DHDF4_ENABLE_SZIP_ENCODING:BOOL=OFF")` |
| Build HDF4 Java library | --enable-java | `set(ADD_BUILD_OPTIONS "${ADD_BUILD_OPTIONS} -DHDF4_BUILD_JAVA:BOOL=ON")` <br> Also specify the location of Java in the JAVA_HOME environment variable. |
