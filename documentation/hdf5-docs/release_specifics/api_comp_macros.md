---
title: API Compatibility Macros
redirect_from: 
  - display/HDF5/API+Compatibility+Macros
---

Audience
The target audience for this document has existing applications that use the HDF5 library, and is considering moving to the latest HDF5 release to take advantage of the latest library features and enhancements.

Compatibility Issues
With each major release of HDF5, such as 1.12 or 1.10, certain compatibility issues must be considered when migrating applications from an earlier major release.

This document describes the approach taken by The HDF Group to help existing users of HDF5 address compatibility issues in the HDF5 API.

Summary and Motivation
In response to new and evolving requirements for the library and data format, several basic functions have changed since HDF5 was first released. To allow existing applications to continue to compile and run properly, all versions of these functions have been retained in the later releases of the HDF5 library.

Given the scope of changes available with each major release of HDF5, and recognizing the potentially time-consuming task of editing all the affected calls in user applications, The HDF Group has created a set of macros that can be used to flexibly and easily map existing API calls to previous release functions. We refer to these as the API compatibility macros.

The HDF Group generally encourages users to update applications to work with the latest HDF5 library release so that all new features and enhancements are available to them. At the same time, The HDF Group understands that, under some circumstances, updating applications may not be feasible or necessary. The API compatibility macros, described in this document, provide a bridge from old APIs to new and can be particularly helpful in situations such as these:

Source code is not available - only binaries are available; updating the application is not feasible.
Source code is available, but there are no resources to update it.
Source code is available, as are resources to update it, but the old version works quite well so updates are not a priority. At the same time, it is desirable to take advantage of certain efficiencies in the newer HDF5 release that do not require code changes.
Source code is available, as are resources to update it, but the applications are large or complex, and must continue to run while the code updates are carried out.
Understanding and Using the Macros
As part of latest HDF5 release, several functions that existed in previous versions of the library were updated with new calling parameters and given new names. The updated versions of the functions have a number (for eg '2') at the end of the original function name. The original versions of these functions were retained and renamed to have an earlier number (for eg '1') at the end of the original function name.

For example, consider the function H5Lvisit in HDF5 release 1.10 as compared with 1.12:

Original function name and signature in 1.10.0	
herr_t H5Lvisit ( hid_t grp_id, H5_index_t idx_type, H5_iter_order_t order, H5L_iterate_t op, void *op_data )

Updated function and signature, introduced in release 1.12.0	
herr_t H5Lvisit2 ( hid_t group_id, H5_index_t idx_type, H5_iter_order_t order, H5L_iterate2_t op, void *op_data )

Original function and signature, renamed in release 1.12.0	
herr_t H5Lvisit1 ( hid_t group_id, H5_index_t idx_type, H5_iter_order_t order, H5L_iterate1_t op, void *op_data )

API compatibility macro, introduced in release 1.12.0	
H5Lvisit

The macro, H5Lvisit, will be mapped to either H5Lvisit1 or H5Lvisit2. The mapping is determined by a combination of the configuration options use to build the HDF5 library and compile-time options used to build the application. The calling parameters used with the H5Lvisit compatibility macro should match the number and type of the function the macros will be mapped to (H5Lvisit1 or H5Lvisit2).

The function names ending in ‘1’ or ‘2’ are referred to as versioned names, and the corresponding functions are referred to as versioned functions. For new code development, The HDF Group recommends use of the compatibility macro mapped to the latest version of the function. The original version of the function should be considered deprecated and, in general, should not be used when developing new code.  

Compatibility Macro Mapping Options
To determine the mapping for a given API compatibility macro in a given application, a combination of user-controlled selections, collectively referred to as the compatibility macro mapping options, is considered in the following sequence:

What compatibility macro configuration option was used to build the HDF5 library? We refer to this selection as the library mapping.
 
Was a compatibility macro global compile-time option specified when the application was built? We refer to this (optional) selection as the application mapping. If an application mapping exists, it overrides the library mapping. (See adjacent notes.)
 
Were any compatibility macro function-level compile-time options specified when the application was built? We refer to these (optional) selections as function mappings. If function mappings exist, they override library and application mappings for the relevant API compatibility macros. (See adjacent notes.)
Notes: An application mapping can map APIs to the same version or to a version older than the configured library mapping. When the application attempts to map APIs to a newer version of the API than the library was configured with, it will fail to “upgrade” the mapping (and may fail silently).
When it is necessary to “upgrade” the macro mappings from those set in the library mapping, it must be done at the per-function level, using the function-level mappings. As long as one does not try to map a function to a version that was compiled out in the library mapping, individual functions can be upgraded or downgraded freely.

 

Library Mapping Options

When the HDF5 library is built, configure flags can be used to control the API compatibility macro mapping behavior exhibited by the library. This behavior can be overridden by application and function mappings. One configure flag excludes deprecated functions from the HDF5 library, making them unavailable to applications linked with the library.

 

Table 1:  Library Mapping Options
--with-default-api-version=v112

(the default in 1.12)

1.12.x   (H5Lvisit2)	yes
--with-default-api-version=v110
1.10.x   (H5Lvisit1)	yes
--with-default-api-version=v18	1.8.x     (H5Lvisit1)	yes
--with-default-api-version=v16	1.6.x     (H5Lvisit1)	yes
--disable-deprecated-symbols	1.12.x   (H5Lvisit2)	no
 

Refer to the file libhdf5.settings in the directory where the HDF5 library is installed to determine the configure flags used to build the library. In particular, look for the two lines shown here under Features:

   Default API mapping: v112

  With deprecated public symbols: yes

Application Mapping Options

When an application using HDF5 APIs is built and linked with the HDF5 library, compile-time options to h5cc can be used to control the API compatibility macro mapping behavior exhibited by the application. The application mapping overrides the behavior specified by the library mapping, and can be overridden on a function-by-function basis by the function mappings.

If the HDF5 library was configured with the --disable-deprecated-symbols flag, then the deprecated functions will not be available, regardless of the application mapping options.

 

Table 2:  Application Mapping Options
-DH5_USE_112_API

(Default behavior if no option specified.)

1.12.x    (HLvisit2)	yes*
*if available in library
-DH5_USE_110_API	1.10.x    (HLvisit1)	yes*
*if available in library
-DH5_USE_18_API	1.8.x     (H5Lvisit1)	yes*
*if available in library
-DH5_USE_16_API	1.6.x     (H5Lvisit1)	yes*
*if available in library
-DH5_NO_DEPRECATED_SYMBOLS	1.10.x    (H5Lvisit1)	no
 

Function Mapping Options

Function mappings are specified when the application is built. These mappings can be used to control the mapping of the API compatibility macros to underlying functions on a function-by-function basis. The function mappings override the library and application mappings discussed earlier.

If the HDF5 library was configured with the --disable-deprecated-symbols flag, or -DH5_NO_DEPRECATED_SYMBOLS is used to compile the application, then the deprecated functions will not be available, regardless of the function mapping options.

For every function with multiple available versions, a compile-time version flag can be defined to selectively map the function macro to the desired versioned function. The function mapping consists of the function name followed by "_vers" which is mapped by number to a specific function or struct:

H5xxx	H5xxx_vers=1	H5xxx1
 	H5xxx_vers=2	H5xxx2
 

For example, in version 1.10 the H5Rreference macro can be mapped to either H5Rreference1 or H5Rreference2. When used, the value of the H5Rreference_vers compile-time version flag determines which function will be called:

When H5Rreference_vers is set to 1, the macro H5Rreference will be mapped to H5Rreference1.
     h5cc ... -DH5Rreference_vers=1 ...
 

When H5Rdereference_vers is set to 2, the macro H5Rdereference will be mapped to H5Rdereference2.
     h5cc ... -DH5Rreference_vers=2 ...
 

When H5Rreference_vers is not set, the macro H5Rreference will be mapped to either H5Rreference1 or H5Rreference2, based on the application mapping, if one was specified, or on the library mapping.
     h5cc ...
Please be aware that some function mappings use mapped structures, as well.  If compiling an application with a function mapping that uses a mapped structure, you must include each function and mapped structure plus EVERY function that uses the mapped structure, whether or not that function is used in the application. In 1.12, mappings of structures are used by the H5L and H5O function mappings.

For example, the application h5ex_g_iterate.c (found on the Examples by API page under "Groups") only calls H5Lvisit , H5Ovisit , and H5Oget_info_by_name . To compile this application with 1.10 APIs in 1.12 with the function specific mappings, then not only must H5Lvisit_vers, H5Ovisit_vers, and H5Oget_info_by_name_vers be specified on the command line, but the mapped structures and every function that uses the mapped structures must be included, as well. The full compile line is shown below:

h5cc -DH5Lvisit_vers=1 -DH5Ovisit_vers=1 -DH5Oget_info_by_name_vers=1 -DH5Lvisit_by_name_vers=1 -DH5Literate_vers=1 -DH5Literate_by_name_vers=1 -DH5O_info_t_vers=1 -DH5L_info_t_vers=1 -DH5L_iterate_t_vers=1 -DH5Lget_info_by_idx_vers=1 -DH5Lget_info_vers=1 h5ex_g_visit.c

Function Mapping Options in Releases 1.12.x





H5L_GET_INFO	
H5L_GET_INFO2

Function mapping: H5Lget_info_vers=2
Struct mapping: H5L_info_t_vers=2
H5L_GET_INFO1

Function mapping H5Lget_info_vers=1
Struct mapping: H5L_info_t_vers=1
H5L_GET_INFO_BY_IDX	
H5L_GET_INFO_BY_IDX2

Function mapping: H5Lget_info_by_idx_vers=2
Struct mapping: H5L_info_t_vers=2
H5L_GET_INFO_BY_IDX1

Function mapping: H5Lget_info_by_idx_vers=1
Struct mapping: H5L_info_t_vers=1
H5L_ITERATE	
H5L_ITERATE2

Function mapping: H5Literate_vers=2
Struct mapping: H5L_iterate_t_vers=2
H5L_ITERATE1

Function mapping: H5Literate_vers=1
Struct mapping: H5L_iterate_t_vers=1
H5L_ITERATE_BY_NAME	
H5L_ITERATE_BY_NAME2

Function mapping: H5Literate_by_name_vers=2
Struct mapping: H5L_iterate_t_vers=2
H5L_ITERATE_BY_NAME1

Function mapping: H5Literate_by_name_vers=1
Struct mapping: H5L_iterate_t_vers=1
H5L_VISIT	
H5L_VISIT2

Function mapping: H5Lvisit_vers=2
Struct mapping: H5L_iterate_t_vers=2
H5L_VISIT1

Function mapping: H5Lvisit_vers=1
Struct mapping: H5L_iterate_t_vers=1
H5L_VISIT_BY_NAME	
H5L_VISIT_BY_NAME2

Function mapping: H5Lvisit_by_name_vers=2
Struct mapping: H5L_iterate_t_vers=2
H5L_VISIT_BY_NAME1

Function mapping: H5Lvisit_by_name_vers=1
Struct mapping: H5L_iterate_t_vers=1
H5O_GET_INFO	
H5O_GET_INFO3

Function mapping: H5Oget_info_vers=3
Struct mapping: H5O_info_t_vers=2
H5O_GET_INFO1

Function mapping: H5Oget_info_vers=1
Struct mapping: H5O_info_t_vers=1
H5O_GET_INFO_BY_IDX	
H5O_GET_INFO_BY_IDX3

Function mapping: H5Oget_info_by_idx_vers=3
Struct mapping: H5O_info_t_vers=2
H5O_GET_INFO_BY_IDX1

Function mapping: H5Oget_info_by_idx_vers=1
Struct mapping: H5O_info_t_vers=1
H5O_GET_INFO_BY_NAME	
H5O_GET_INFO_BY_NAME3

Function mapping: H5O_get_info_by_name_vers=3
Struct mapping: H5O_info_t_vers=2
H5O_GET_INFO_BY_NAME1

Function mapping: H5O_get_info_by_name_vers=1
Struct mapping: H5O_info_t_vers=1
H5O_VISIT	
H5O_VISIT3

Function mapping: H5Ovisit_vers=3
Struct mapping: H5O_iterate_t_vers=2
H5O_VISIT1

Function mapping: H5Ovisit_vers=1
Struct mapping: H5O_iterate_t_vers=1
H5O_VISIT_BY_NAME	
H5O_VISIT_BY_NAME3

Function mapping: H5Ovisit_by_name_vers=3
Struct mapping: H5O_iterate_t_vers=2
H5O_VISIT_BY_NAME1

Function mapping: H5Ovisit_by_name_vers=1
Struct mapping: H5O_iterate_t_vers=1
H5P_ENCODE	
H5P_ENCODE2

Function mapping: H5Pencode_vers=2
H5P_ENCODE1

Function mapping: H5Pencode_vers=1
H5S_ENCODE	
H5S_ENCODE2

Function mapping: H5Sencode_vers=2
H5S_ENCODE1

Function mapping: H5Sencode_vers=1
Function Mapping Options in Releases 1.10.x

The versioned H5Oget_info functions (H5Oget_info1 and H5Oget_info2) were added in 1.10.3, and H5Oget_info was replaced by a macro to invoke H5Oget_info1 or H5Oget_info2. However, this broke compatibility and caused problems for users because there was no longer a function H5Oget_info.  In 1.10.4 and subsequent 1.10.x versions the macro was removed, H5Oget_info1 was deprecated, and H5Oget_info was resurrected as a function. H5Oget_info2 remained as a function, but is not a versioned alternative to the original H5Oget_info. The same is true for H5Oget_info_by name, H5Oget_info_by_idx, H5Ovisit, and H5Ovisit_by_name. The version 2 functions were added to improve performance.

The unversioned originals and version 2 of those functions exist in 1.10 because having released them in 1.10.3, it would break compatibility to remove them, so the original and version 2 functions remained in the source but without any macro to map to one or the other.  Therefore, version 2 functions are available, but only when invoked directly.

In 1.12 there is a version 3 of all 5 functions which uses version 2 H5Oinfo2_t or H5Oiterate2_t structures.  Both versions 1 and 2 are deprecated and macros replace the unversioned functions, mapping to version 1 for 18 and 110 default apis and to version 3 for 112 default api.  Version 2 is available, but will only be invoked if invoked directly.

 

Macro	
Default function used

(if no macro specified)

Introduced in

h5cc version flag and value	Mapped to function or struct
H5Rdereference

H5Rdereference2	HDF5-1.10.0	-DH5Rdereference_vers=1	H5Rdereference1
-DH5Rdereference_vers=2	H5Rdereference2
H5Fget_info

H5Fget_info2	HDF5-1.10.0	-DH5Fget_info_vers=1	H5Fget_info1 with struct H5F_info1_t
-DH5Fget_info_vers=2	H5Fget_info2 with struct H5F_info2_t
H5Oget_info

H5Oget_info1	HDF5-1.10.3	-DH5Oget_info_vers=1	H5Oget_info1
-DH5Oget_info_vers=2	H5Oget_info2
H5Oget_info_by_idx

H5Oget_info_by_idx1	HDF5-1.10.3	-DH5Oget_info_by_idx_vers=1	H5Oget_info_by_idx1
-DH5Oget_info_by_idx_vers=2	H5Oget_info_by_idx2
H5Oget_info_by_name	H5Oget_info_by_name1	HDF5-1.10.3	-DH5Oget_info_by_name_vers=1	H5Oget_info_by_name1
-DH5Oget_info_by_name_vers=2	H5Oget_info_by_name2
H5Ovisit	H5Ovisit1	HDF5-1.10.3	-DH5Ovisit_vers=1	H5Ovisit1
-DH5Ovisit_vers=2	
H5Ovisit2

H5Ovisit_by_name	H5Ovisit_by_name1	HDF5-1.10.3	-DH5Ovisit_by_name_vers=1	H5Ovisit_by_name1
-DH5Ovisit_by_name_vers=2	H5Ovisit_by_name2
Function Mapping Options in Releases 1.8.x

At release 1.8.0, the API compatibility macros, function mapping compile-time version flags and values, and corresponding versioned functions listed in the following table were introduced. If the application being compiled to run with any 1.10.x release was written to use any 1.6.x release of HDF5, you must also consider these macros and mapping options.

 

Table 5:  Function Mapping Options in Releases 1.8.x
Macro	h5cc version flag and value	Mapped to function
or struct
H5Acreate	-DH5Acreate_vers=1	H5Acreate1
-DH5Acreate_vers=2	H5Acreate2
H5Aiterate	-DH5Aiterate_vers=1	H5Aiterate1
with struct H5A_operator1_t
-DH5Aiterate_vers=2	H5Aiterate2
with struct H5A_operator2_t
H5Dcreate	-DH5Dcreate_vers=1	H5Dcreate1
-DH5Dcreate_vers=2	H5Dcreate2
H5Dopen	-DH5Dopen_vers=1	H5Dopen1
-DH5Dopen_vers=2	H5Dopen2
H5Eclear	-DH5Eclear_vers=1	H5Eclear1
-DH5Eclear_vers=2	H5Eclear2
H5Eprint	-DH5Eprint_vers=1	H5Eprint1
-DH5Eprint_vers=2	H5Eprint2
H5Epush	-DH5Epush_vers=1	H5Epush1
-DH5Epush_vers=2	H5Epush2
H5Eset_auto	-DH5Eset_auto_vers=1	H5Eset_auto1
-DH5Eset_auto_vers=2	H5Eset_auto2
H5Eget_auto	-DH5Eget_auto_vers=1	H5Eget_auto1
-DH5Eget_auto_vers=2	H5Eget_auto2
H5E_auto_t
Struct for H5Eset_auto
and H5Eget_auto	-DH5E_auto_t_vers=1	H5E_auto1_t
-DH5E_auto_t_vers=2	H5E_auto2_t
H5Ewalk	-DH5Ewalk_vers=1	H5Ewalk1
with callback H5E_walk1_t
and struct H5E_error1_t
-DH5Ewalk_vers=2	H5Ewalk2
with callback H5E_walk2_t
and struct H5E_error2_t
H5Gcreate	-DH5Gcreate_vers=1	H5Gcreate1
-DH5Gcreate_vers=2	H5Gcreate2
H5Gopen	-DH5Gopen_vers=1	H5Gopen1
-DH5Gopen_vers=2	H5Gopen2
H5Pget_filter	-DH5Pget_filter_vers=1	H5Pget_filter1
-DH5Pget_filter_vers=2	H5Pget_filter2
H5Pget_filter_by_id	-DH5Pget_filter_by_id_vers=1	H5Pget_filter_by_id1
-DH5Pget_filter_by_id_vers=2	H5Pget_filter_by_id2
H5Pinsert	-DH5Pinsert_vers=1	H5Pinsert1
-DH5Pinsert_vers=2	H5Pinsert2
H5Pregister	-DH5Pregister_vers=1	H5Pregister1
-DH5Pregister_vers=2	H5Pregister2
H5Rget_obj_type	-DH5Rget_obj_typevers=1	H5Rget_obj_type1
-DH5Rget_obj_type_vers=2	H5Rget_obj_type2
H5Tarray_create	-DH5Tarray_create_vers=1	H5Tarray_create1
-DH5Tarray_create_vers=2	H5Tarray_create2
H5Tcommit	-DH5Tcommit_vers=1	H5Tcommit1
-DH5Tcommit_vers=2	H5Tcommit2
H5Tget_array_dims	-DH5Tget_array_dims_vers=1	H5Tget_array_dims1
-DH5Tget_array_dims_vers=2	H5Tget_array_dims2
H5Topen	-DH5Topen_vers=1	H5Topen1
-DH5Topen_vers=2	H5Topen2
H5Z_class_t Struct for H5Zregister	-DH5Z_class_t_vers=1	H5Z_class1_t
-DH5Z_class_t_vers=2	H5Z_class2_t
 

Further Information

See the HDF5 Reference Manual  for complete descriptions of all API compatibility macros and versioned functions shown.

It is possible to specify multiple function mappings for a single application build:

h5cc ... -DH5Rdereference_vers=1 -DH5Fget_info_vers=2 ...As a result of the function and struct mappings in this compile example, all occurrences of the macro H5Rdereference will be mapped to H5Rdereference1 and all occurrences of the macro H5Fget_info will be mapped to H5Fget_info2 for the application being built.

The function and struct mappings can be used to guarantee that a given API compatibility macro will be mapped to the desired underlying function or struct version regardless of the library or application mappings. In cases where an application may benefit greatly from features offered by some of the later APIs, or must continue to use some earlier API versions for compatibility reasons, this fine-grained control may be very important.

As noted earlier, the function mappings can only reference versioned functions that are included in the HDF5 library, as determined by the configure flag used to build the library. For example, if the HDF5 library being linked with the application was built with the --disable-deprecated-symbols option, version 1 of the underlying functions would not be available, and the example above that defined H5Rdereference_vers=1 would not be supported.

The function mappings do not negate any available functions. If H5Rdereference1 is available in the installed version of the HDF5 library, and the application was not compiled with the -DH5_NO_DEPRECATED_SYMBOLS flag, the function H5Rdereference1 will remain available to the application through its versioned name. Similarly, H5Rdereference2 will remain available to the application as H5Rdereference2. The function mapping version flag H5Rdereference_vers only controls the mapping of the API compatibility macro H5Rdereference to one of the two available functions.

This can be especially useful in any case where the programmer does not have direct control over global macro definitions, such as when writing code meant to be copied to multiple applications or when writing code in a header file.

Compatibility Macros in HDF5 1.6.8 and Later
A series of similar compatibility macros were introduced into the release 1.6 series of the library, starting with release 1.6.8. These macros simply alias the ‘1’ version functions, callbacks, and typedefs listed above to their original non-numbered names.

These macros were strictly a forward-looking feature at that time; they were not necessary for compatibility in 1.6.x. These macros were created at that time to enable writing code that could be used with any version of the library after 1.6.8 and any library compilation options except H5_NO_DEPRECATED_SYMBOLS, by always using the ‘1’ version of versioned functions and types. For example, H5Dopen1 will always be interpreted in exactly the same manner by any version of the library since 1.6.8.

Common Use Case
A common scenario where the API compatibility macros may be helpful is the migration of an existing application to a new HDF5 release An incremental migration plan is outlined here:

Build the HDF5 library without specifying any library mapping configure flag. In this default mode, the 1.6.x, 1.8.x, and 1.10.x versions of the underlying functions are available, and the API compatibility macros will be mapped to the current HDF5 versioned functions.
 

Compile the application with the -DH5_USE_NN_API application mapping option if it was written for use with an earlier HDF5 library.  Because the application mapping overrides the library mapping, the macros will all be mapped to the earlier versions of the functions.
 

Remap one API compatibility macro at a time (or sets of macros), to use the current HDF5 versions. At each stage, use the function mappings to map the macros being worked on to the current versions. For example, use the -DH5Rdereference_vers=2 version flag setting to remap the H5Rdereference macro to H5Rdereference2, the 1.10.x version.
During this step, the application code will need to be modified to change the calling parameters used with the API compatibility macros to match the number and type of the 1.10.x versioned functions. The macro name, for example H5Rdereference, should continue to be used in the code, to allow for possible re-mappings to later versioned functions in a future release.

 

After all macros have been migrated to the latest versioned functions in step 3, compile the application without any application or function mappings. This build uses the library mappings set in step 1, and maps API compatibility macros to the latest versions.
 

Finally, compile the application with the application mapping -DH5_NO_DEPRECATED_SYMBOLS, and address any failures to complete the application migration process.