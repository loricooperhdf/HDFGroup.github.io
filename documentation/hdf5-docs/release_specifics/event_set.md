---
title: Even set
redirect_from:
  - display/HDF5/Event+Set
---

Managing Event Sets (H5ES)

|         |         |         |
| ------- | ------- | ------- | 
| H5ES_CLOSE    | H5ES_GET_ERR_STATUS | H5ES_GET_OP_COUNTER |
| H5ES_CREATE   | H5ES_GET_ERR_COUNT  | H5ES_WAIT           |
| H5ES_GET_COUNT | H5ES_GET_ERR_INFO   |

This interface can be only used with the HDF5 VOL connectors that enable the asynchronous feature in HDF5. The native HDF5 library has only synchronous operations.

HDF5 VOL connectors with support for asynchronous operations:

* ASYNC
* DAOS


 Example:

~~~
 fid = H5Fopen(..); 
 gid = H5Gopen(fid, ..);  //Starts when H5Fopen completes
 did = H5Dopen(gid, ..);  //Starts when H5Gopen completes

 es_id = H5EScreate();  // Create event set for tracking async operations 
 status = H5Dwrite_async(did, .., es_id);  //Asynchronous, starts when H5Dopen completes, 
                                           // may run concurrently with other H5Dwrite_async 
                                           // in event set.
 status = H5Dwrite_async(did, .., es_id); //Asynchronous, starts when H5Dopen completes, 
                                          // may run concurrently with other H5Dwrite_async 
                                          // in event set....
 <other user code>
 ...
 H5ESwait(es_id); //Wait for operations in event set to complete, buffers used for H5Dwrite_async must only be changed after wait returns.
~~~
