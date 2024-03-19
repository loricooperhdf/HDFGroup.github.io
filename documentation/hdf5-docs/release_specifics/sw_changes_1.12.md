---
title: Software Changes from Release to Release for HDF5 1.12
redirect_from: 
  - /display/HDF5/Software+Changes+from+Release+to+Release+for+HDF5+1.12
---

# Software Changes from Release to Release in HDF5 1.12

For a description of the major new features that were introduced, please see [New Features in HDF5 Release 1.12](sw_changes_1.12.md).

This page provides information on the changes that a maintenance developer needs to be aware of between successive releases of HDF5, such as:

* New or changed features or tools
* Syntax and behavioral changes in the existing application programming interface (the API)
* Certain types of changes in configuration or build processes

Note that bug fixes and performance enhancements in the C library are automatically picked up by the C++, Fortran, and Java libraries.

The following information is included below.

* [Release 1.12.2 versus Release 1.12.1](#release-1.12.2-versus-release-1.12.1)
* [Release 1.12.1 versus Release 1.12.0](#release-1.12.1-versus-release-1.12.0)
* [Release 1.12.0 versus Release 1.10.6](#release-1.12.0-versus-release-1.10.6)

The release notes also list changes made to the library, but these notes tend to be more at a more detail-oriented level. The release notes may include new features, bugs fixed, supported configuration features, platforms on which the library has been tested, and known problems. The release note files are listed below and can be found at the top level of the HDF5 source code tree in the release_docs directory.

|                          |                                                              |
| ------------------------ | ------------------------------------------------------------ |
| Release Notes            | Technical notes regarding the current release of the HDF5 library (RELEASE.txt in the source code) |
| HISTORY-1_12.txt | Release information for HDF5-1.12.0 through 1.12.1 |
| HISTORY-1_10_0-1_12_0.txt | Development history between the HDF5-1.10.0 and HDF5-1.12.0 releases |
| HISTORY-1_10.txt | Release information for all HDF5-1.10 releases |
| HISTORY-1_8_0-1_10_0.txt | Development history between the HDF5-1.8.0 and HDF5-1.10.0 releases |
| HISTORY-1_8.txt | Release information for HDF5-1.8.0 through 1.8.21 |
| HISTORY-1_0-1_8_0_rc3.txt | Technical notes starting with HDF5-1.0.0 and ending with HDF5-1.8.0-rc3 (the state of the code prior to the HDF5-1.8.0 release) |

## Release 1.12.2 versus Release 1.12.1
This section lists interface-level changes and other user-visible changes in behavior in the transition from HDF5 Release 1.12.1 to Release 1.12.2.

### New and Changed Functions, Classes, Subroutines, Wrappers, and Macros

The following are new C functions in this release:

H5DSwith_new_ref	Determines if new references are used with dimension scales
H5LTget_attribute_ullong	Reads an unsigned long long attribute
H5LTset_attribute_ullong	Create an unsigned long long attribute
H5VLobject_is_native	Determines whether an object ID represents a native VOL connector object
See API Compatibility Reports for 1.12.2 for complete details.

## Release 1.12.1 versus Release 1.12.0
This section lists interface-level changes and other user-visible changes in behavior in the transition from HDF5 Release 1.12.0 to Release 1.12.1.

The following are new C functions in this release:

H5P_GET_FAPL_SPLITTER
Retrieves information for a splitter file access property list
H5P_SET_FAPL_SPLITTER	Sets the file access property list to use the splitter driver
H5P_GET_FILE_LOCKING	Gets the file locking property values
H5P_SET_FILE_LOCKING	Sets the file locking property values
H5_GET_ALLOC_STATS 
Gets the memory allocation statistics for the library
H5_GET_FREE_LIST_SIZES	Gets the current size of the free lists used to manage memory
H5S_SEL_ITER_RESET	Resets a dataspace selection iterator back to an initial state
H5VL_QUERY_OPTIONAL	Determines whether a VOL connector supports a particular optional callback operation
 

In the C++ Wrapper

The following C++ wrappers were added:

DataSet::operator=
Operator= for DataSet class

FileAccPropList::getFileLocking
See H5P_GET_FILE_LOCKING for details

FileAccPropList::setFileLocking 
See H5P_SET_FILE_LOCKING for details

See the API Compatibility report for complete details.

Compatibility Notes and Report
See API Compatibility Reports for 1.12 for information regarding compatibility with previous releases.

## Release 1.12.0 versus Release 1.10.6
This section lists interface-level changes and other user-visible changes in behavior in the transition from HDF5 Release 1.10.6 to Release 1.12.0.

### New Features
For a description of the major new features that were introduced, please see New Features in HDF5 Release 1.12.

### New and Changed Functions, Classes, Subroutines, Wrappers, and Macros

### In the C/Fortran Interface (main library)

Folllowing are the new or changed APIs introduced in HDF5-1.12.0. Those introduced with a new feature list the specific new feature that they were added for.

H5F_DELETE	N	Deletes an HDF5 file
H5F_GET_FILENO	Y	Retrieves a file's file number that uniquely identifies the open file
H5F_IS_ACCESSIBLE	Y	Determines if a file can be opened with a given fapl
 	 	 
H5I_ITERATE	N	Calls a callback for each member of the identifier type specified
 	 	 
H5L_GET_INFO, H5L_GET_INFO1, H5L_GET_INFO2	Y (no change)	
The function H5L_GET_INFO was moved to H5L_GET_INFO1, and H5L_GET_INFO2 was introduced. The macro H5L_GET_INFO was created that can be mapped to either H5L_GET_INFO1 or H5L_GET_INFO2. For HDF5-1.12, H5L_GET_INFO is mapped to H5L_GET_INFO2 by default.  In earlier releases, H5L_GET_INFO is mapped to H5L_GET_INFO1.

H5L_GET_INFO_BY_IDX, H5L_GET_INFO_BY_IDX1, H5L_GET_INFO_BY_IDX2	Y (no change)	The function H5L_GET_INFO_BY_IDX was moved to H5L_GET_INFO_BY_IDX1, and H5L_GET_INFO_BY_IDX2 was introduced. The macro H5L_GET_INFO_BY_IDX was created that can be mapped to either H5L_GET_INFO_BY_IDX1 or H5L_GET_INFO_BY_IDX2. For HDF5-1.12, H5L_GET_INFO_BY_IDX is mapped to H5L_GET_INFO_BY_IDX2 by default.  In earlier releases, H5L_GET_INFO_BY_IDX is mapped to H5L_GET_INFO_BY_IDX1.
H5L_ITERATE, H5L_ITERATE1, H5L_ITERATE2	Y (no change)	The function H5L_ITERATE was moved to H5L_ITERATE1, and H5L_ITERATE2 was introduced. The macro H5L_ITERATE was created that can be mapped to either H5L_ITERATE1 or H5L_ITERATE2. For HDF5-1.12, H5L_ITERATE is mapped to H5L_ITERATE2 by default.  In earlier releases, H5L_ITERATE is mapped to H5L_ITERATE1.
H5L_ITERATE_BY_NAME, H5L_ITERATE_BY_NAME1, H5L_ITERATE_BY_NAME2	Y (no change)	The function H5L_ITERATE_BY_NAME was moved to H5L_ITERATE_BY_NAME1, and H5L_ITERATE_BY_NAME2 was introduced. The macro H5L_ITERATE_BY_NAME was created that can be mapped to either H5L_ITERATE_BY_NAME1 or H5L_ITERATE_BY_NAME2. For HDF5-1.12, H5L_ITERATE_BY_NAME is mapped to H5L_ITERATE_BY_NAME2 by default.  In earlier releases, H5L_ITERATE_BY_NAME is mapped to H5L_ITERATE_BY_NAME1.
H5L_VISIT, H5L_VISIT1, H5L_VISIT2	N	The function H5L_VISIT was moved to H5L_VISIT1, and H5L_VISIT2 was introduced. The macro H5L_VISIT was created that can be mapped to either H5L_VISIT1 or H5L_VISIT2. For HDF5-1.12, H5L_VISIT is mapped to H5L_VISIT2 by default.  In earlier releases, H5L_VISIT is mapped to H5L_VISIT1.
H5L_VISIT_BY_NAME, H5L_VISIT_BY_NAME1, H5L_VISIT_BY_NAME2	N	The function H5L_VISIT_BY_NAME was moved to H5L_VISIT_BY_NAME1, and H5L_VISIT_BY_NAME2 was introduced. The macro H5L_VISIT_BY_NAME was created that can be mapped to either H5L_VISIT_BY_NAME1 or H5L_VISIT_BY_NAME2. For HDF5-1.12, H5L_VISIT_BY_NAME is mapped to H5L_VISIT_BY_NAME2 by default.  In earlier releases, H5L_VISIT_BY_NAME is mapped to H5L_VISIT_BY_NAME1.
 	 	 
H5O_GET_INFO, H5O_GET_INFO3	N/A	The function H5O_GET_INFO was replaced by the macro H5O_GET_INFO and the function H5O_GET_INFO3 was added.
H5O_GET_INFO_BY_IDX, H5O_GET_INFO_BY_IDX3	N/A	The function H5O_GET_INFO_BY_IDX was replaced by the macro H5O_GET_INFO_BY_IDX. The function H5O_GET_INFO_BY_IDX3 was added.
H5O_GET_INFO_BY_NAME, H5O_GET_INFO_BY_NAME3	N/A	The function H5O_GET_INFO_BY_NAME was replaced by the macro H5O_GET_INFO_BY_NAME. The function H5O_GET_INFO_BY_NAME3 was added.
H5O_GET_NATIVE_INFO	N	Retrieves the native file format information about an object
H5O_GET_NATIVE_INFO_BY_IDX	N	Retrieves native file format information about an object according to the order of an index
H5O_GET_NATIVE_INFO_BY_NAME	N	Retrieves native file format information about an object given its name
H5O_OPEN_BY_TOKEN	Y	Opens an object in an HDF5 file using its VOL independent token
H5O_TOKEN_CMP	Y	Compares two VOL connector object tokens
H5O_TOKEN_FROM_STR	N	Deserializes a string into a connector object token
H5O_TOKEN_TO_STR	N	Serializes a connector's object token into a string
H5O_VISIT, H5O_VISIT3	N/A	The function H5O_VISIT was replaced by the macro H5O_VISIT and the function H5O_VISIT3 was added
H5O_VISIT_BY_NAME, H5O_VISIT_BY_NAME3	N/A	The function H5O_VISIT_BY_NAME was replaced by the macro H5O_VISIT_BY_NAME, and the function H5O_VISIT_BY_NAME3 was added.
 	 	 
H5P_ENCODE, H5P_ENCODE1, H5P_ENCODE2

N	
Encodes properties on a property list into a buffer

The previous function was renamed to H5P_ENCODE1 and deprecated, and the macro H5P_ENCODE was introduced.

H5P_GET_VOL_ID	Y	Returns the identifier of the current VOL connector
H5P_GET_VOL_INFO	N	Returns a copy of the VOL information for a connector
H5P_SET_VOL	Y	Set the file VOL connector for a file access property list
 	 	 
H5R_COPY	N	Copies an existing reference
H5R_CREATE_ATTR	N	Creates an attribute reference
H5R_CREATE_OBJECT	N	Creates an object reference
H5R_CREATE_REGION	N	Creates a region reference
H5R_DESTROY	N	Closes a reference
H5R_EQUAL	N	Determines whether two references are equal
H5R_GET_ATTR_NAME	N	Retrieves the attribute name for a referenced object
H5R_GET_FILE_NAME	N	Retrieves the file name for a referenced object
H5R_GET_OBJ_NAME	N	Retrieves the object name for a referenced object
H5R_GET_OBJ_TYPE3	N	Retrieves the type of object that an object reference points to
H5R_GET_TYPE	N	Retrieves the type of reference
H5R_OPEN_ATTR	N	Opens the referenced HDF5 attribute
H5R_OPEN_OBJECT	N	Opens the referenced HDF5 object
H5R_OPEN_REGION	N	Sets up a dataspace and selection as specified by a region reference
 	 	 
H5S_COMBINE_HYPERSLAB	N	Performs an operation on a hyperslab and an existing selection and returns the resulting selection
H5S_COMBINE_SELECT	N	
Combines two hyperslab selections with an operation, returning a dataspace with the resulting selection

H5S_ENCODE, H5S_ENCODE1, H5S_ENCODE2

N/A	
Encodes a dataspace object description into a binary buffer

The function H5S_ENCODE was renamed to H5S_ENCODE1 and deprecated in this release. The macro H5S_ENCODE and the function H5S_ENCODE2 were introduced in this release.

H5S_MODIFY_SELECT	N	
Refines a hyperslab selection with an operation using a second hyperslab to modify it

H5S_SEL_ITER_CLOSE	
N

Closes a dataspace selection iterator

H5S_SEL_ITER_CREATE	N	Creates a dataspace selection iterator for a dataspace's selection
H5S_SEL_ITER_GET_SEQ_LIST	N	Retrieves a list of offset / length sequences for the elements in an iterator
H5S_SELECT_ADJUST	N	 Adjusts a selection by subtracting an offset
H5S_SELECT_COPY	N	Copies a selection from one dataspace to another
H5S_SELECT_INTERSECT_BLOCK	N	Checks if current selection intersects with a block
H5S_SELECT_PROJECT_INTERSECTION	N	Projects the intersection of two source selections to a destination selection
H5S_SELECT_SHAPE_SAME	N	
Checks if two selections are the same shape

 	 	 
H5T_RECLAIM	N	Frees the buffers allocated for storing variable-length data in memory
 	 	 
H5VL_CLOSE	Y	Closes a VOL connector identifier
H5VL_GET_CONNECTOR_ID	Y	Retrieves the VOL connector identifier for a given object identifier
H5VL_GET_CONNECTOR_ID_BY_NAME	Y	Retrieves the identifier for a registered VOL connector name
H5VL_GET_CONNECTOR_ID_BY_VALUE	Y	Retrieves the identifier for a registered VOL connector value
H5VL_GET_CONNECTOR_NAME	Y	Retrieves the connector name for the VOL associated with the object or file identifier
H5VL_IS_CONNECTOR_REGISTERED_BY_NAME	Y	Tests whether a VOL class has been registered or not for a connector name
H5VL_IS_CONNECTOR_REGISTERED_BY_VALUE	Y	Tests whether a VOL class has been registered or not for a connector value
H5VL_REGISTER_CONNECTOR	N	Registers a new VOL connector
H5VL_REGISTER_CONNECTOR_BY_NAME	Y	Registers a new VOL connector by name
H5VL_REGISTER_CONNECTOR_BY_VALUE	Y	Registers a new VOL connector by connector value
H5VL_UNREGISTER_CONNECTOR	Y	Removes a VOL connector identifier from the library
 

In the C++ Wrapper

H5File::getFileNum  	See H5F_GET_FILENO
H5File::isAccessible	See H5F_IS_ACCESSIBLE
LinkCreatPropList::getCreateIntermediateGroup	See H5P_GET_CREATE_INTERMEDIATE_GROUP
LinkCreatPropList::setCreateIntermediateGroup	See H5P_SET_CREATE_INTERMEDIATE_GROUP
H5Location::getLinkInfo	See H5L_GET_INFO
H5Location::getNativeObjinfo	See H5O_GET_NATIVE_INFO
H5Location::getObjinfo
See H5O_GET_INFO
H5Object::visit	See H5O_VISIT


## API Compatibility
See API Compatibility Macros in HDF5 for details on using HDF5 version 1.12 with previous releases.

[Compatibility report for Release 1.12.0 versus Release 1.10.6](Compatibility report for Release 1.12.0 versus Release 1.10.6)

 
