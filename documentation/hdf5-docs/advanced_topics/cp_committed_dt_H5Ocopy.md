---
title: Copying Committed Datatypes with H5Ocopy
redirect\_from:

---
##\*\*\* Work-in-Progress \*\*\*

# Copying Committed Datatypes with H5Ocopy

HDF5 Release 1.8.9 May 2012

Contents
1. Copying Committed Datatypes with H5Ocopy
Committed datatypes can be a powerful feature in HDF5. They can be used to share a single datatype description among multiple datasets, to save space or ensure that the datatypes are truly identical, and to assign a name to that datatype within the HDF5 group structure. The object copy API, H5Ocopy, can be used to copy HDF5 objects from one file to another, including committed datatypes and objects that use them. However, problems can occur when a dataset using a committed datatype or an object with an attribute that uses a committed datatype is copied to another file with H5Ocopy.

When copying a dataset that uses a committed datatype or an object with an attribute that uses a committed datatype between files, the library by default does not look for a matching committed datatype in the destination file. The library creates a new committed datatype in the destination file without any links to it (an anonymous committed datatype) and then links the dataset to the anonymous committed datatype. This means that, when copying multiple datasets in separate calls to H5Ocopy, a new committed datatype is created for each H5Ocopy call. While it is possible to have all of the copied datasets share the same committed datatype by copying them in a single call to H5Ocopy, this is not always attainable.

For example, imagine that a user has an application that automatically creates many data files, each with many datasets that all use a single committed datatype. At the end of a project, the user wants to merge all of these files into a single file. The HDF5 Library can have all of the datasets in the combined file use the same committed datatype, but the default behavior of the library is to create an anonymous committed datatype for each dataset.

To make sure that shared committed datatypes in the source are shared in the copy, use the H5Pset\_copy\_object property list API routine to set the H5O\_COPY\_MERGE\_COMMITTED\_DTYPE\_FLAG flag. When this flag is set and H5Ocopy encounters an object or attribute that uses a committed datatype, H5Ocopy will search for a matching committed datatype in the destination file. If a matching committed datatype is found, then it will be used by the copied dataset or attribute. The next few paragraphs describe in more detail the process that H5Ocopy goes through.

When the H5O\_COPY\_MERGE\_COMMITTED\_DTYPE\_FLAG flag is set, H5Ocopy will search the destination file for committed datatypes and build a temporary list in memory of all the committed datatypes it finds. Then, whenever H5Ocopy encounters a dataset that uses a committed datatype or an object with an attribute that uses a committed datatype in the source, it will check that list to see if it contains a datatype equal to the source datatype. If H5Ocopy finds an equal datatype, it will modify the copied object or attribute to use the found committed datatype as its datatype. H5Ocopy will then update the list if a new committed datatype is created in the destination file as a result of the copy. When later datasets and attributes using committed datatypes are encountered, the library will again check to see if the list contains a matching datatype.

To determine if two committed datatypes are equal, the library will compare their descriptions in a manner similar to H5Tequal. In addition, if either committed datatype has one or more attributes, then all attributes must be present in both committed datatypes, and the attributes must all be identical. Each attribute’s datatype description, dataspace, and raw data must be identical. However, if an attribute uses a committed datatype, then the attributes of the attribute’s committed datatype will not be compared.

When H5Ocopy encounters a committed datatype object in the source file, it will similarly search for a matching committed datatype in the destination file. If a match is found, the library will create a hard link in the destination file to the found datatype. If a match is not found, the library will copy the committed datatype normally and add it to the temporary list of committed datatypes in the destination file.

By default, H5Ocopy will search the entire destination file for a matching committed datatype. It is possible to focus where H5Ocopy will search. This focusing should result in a faster search. If there are locations in the destination file where a matching committed datatype might be found, then those locations can be specified with the H5Padd\_merge\_committed\_dtype\_path property.

The example below shows how to enable the feature described above for use with H5Ocopy.

Example 1. Setting the object copy property list

hid\_t ocpypl\_id;
ocpypl\_id = H5Pcreate(H5P\_OBJECT\_COPY);
status = H5Pset\_copy\_object(ocpypl\_id, H5O\_COPY\_MERGE\_COMMITTED\_DT\_FLAG);
  status = H5Ocopy(file1\_id, src\_name, file2\_id, dst\_name, ocpypl\_id, H5P\_DEFAULT);
1.1. Callback Function
If no matching datatype is found in the locations specified by the call to H5Padd\_merge\_committed\_dtype\_path, then H5Ocopy will by default search the entire destination file. In some cases, this may not be desirable. For instance, the user may expect the datatype to always have a match in the specified locations and may wish to return an error if a match is not found. The user may also have a very large file for which the full search incurs a substantial performance penalty. In this instance, the user may wish to log these events so that other datatypes can be added with H5Padd\_merge\_committed\_dtype\_path, or the user may wish to abort the search and copy the datatype normally.

To support these use cases, the functions H5Pset\_mcdt\_search\_cb and H5Pget\_mcdt\_search\_cb have been added. These functions allow the user to define a callback function that will be called every time the list of paths added by H5Padd\_merge\_committed\_dtype\_path has been exhausted but before beginning the full search of the file. The prototype for the callback function is defined by H5O\_mcdt\_search\_cb\_t. The only argument to the callback function is a user supplied user data pointer, and the return value is an enum, defined by H5O\_mndt\_search\_ret\_t, which tells the library to either continue with the full file search, abort the search and copy the datatype normally (create a new committed datatype in the destination file), or return an error.

1.2. Function Summary
Functions used in committed datatype copying operations are listed below.

Function Listing 1. Committed datatype copying related functions

C Function
Fortran

Purpose
H5Ocopy
H5ocopy\_f

Allows an application to copy an object within an HDF5 file or to another HDF5 file.
H5Pset\_copy\_object
h5pset\_copy\_object\_f

Allows an application to set properties to be used when an object is copied.
H5Padd\_merge\_committed\_dtype\_path
(none)

Allows an application to add a path to the list of paths that will be searched in the destination file for a matching committed datatype.
H5Pfree\_merge\_committed\_dtype\_paths
(none)

Allows an application to clear the list of paths stored in the object copy property list ocpypl\_id.
H5Pset\_mcdt\_search\_cb
(none)

Allows an application to set the callback function that H5Ocopy will invoke before searching the entire destination file for a matching committed datatype.
H5Pget\_mcdt\_search\_cb
(none)

Allows an application to retrieve the callback function from the specified object copy property list.
H5O\_mcdt\_search\_cb\_t
(none)

Definition of the callback function set by H5Pset\_mcdt\_search\_cb. Provides the mechanism by which a user application may set an action for H5Ocopy to take after checking all suggested paths for a matching committed datatype but before starting the global search of the destination file.
1.3. Resources
See the following for more information.

See the “HDF5 Datatypes” chapter in the HDF5 User’s Guide.

See these entries in the HDF5 Reference Manual:

H5Ocopy
H5Pset\_copy\_object
H5Padd\_merge\_committed\_dtype\_path
H5Pfree\_merge\_committed\_dtype\_paths
H5Pset\_mcdt\_search\_cb
H5Pget\_mcdt\_search\_cb

