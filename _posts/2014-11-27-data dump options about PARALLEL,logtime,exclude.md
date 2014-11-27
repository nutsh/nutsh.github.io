---
layout: post
title: Data dump options about  PARALLEL,logTime & exclude
category: oracle
tag: [oracle, ops]
shortinfo: Data dump options about  PARALLEL,logTime & exclude
---

Data dump options about  PARALLEL,logTime & exclude

# PARALLEL Option
`PARALLEL` is not user for Object Struct creation , but effect with Data.

## Suggestion:
- Set the degree of parallelism to two times the number of CPUs, then tune from there.
- For Data Pump Export, the PARALLEL parameter value should be less than or equal to the number of dump files.
- For Data Pump Import, the PARALLEL parameter value should not be much larger than the number of files in the dump file set.

##snippet
```sh
#expdp
expdp IMPEXP/IMPEXP@AT1 schemas=C51HITR2 PARALLEL=1 directory=DATA_PUMP_DIR dumpfile=AT_HOST_20141125_1_%U.dmp LOGFILE=AT_HOST_20141125_1.log logtime=all;
expdp IMPEXP/IMPEXP@AT1 schemas=C51HITR2 PARALLEL=2 directory=DATA_PUMP_DIR dumpfile=AT_HOST_20141125_2_%U.dmp LOGFILE=AT_HOST_20141125_2.log logtime=all; 
#impdp
impdp IMPEXP/IMPEXP@POSTBOD3 schemas=C51HITR2 PARALLEL=6 directory=DATA_PUMP_DIR dumpfile=AT_HOST_20141125_2_%U.dmp LOGFILE=2_6.log content=ALL logtime=all
impdp IMPEXP/IMPEXP@POSTBOD3 schemas=C51HITR2 PARALLEL=4 directory=DATA_PUMP_DIR dumpfile=AT_HOST_20141125_4_%U.dmp LOGFILE=4_2.log content=ALL logtime=all 
 ```
##link
- Checklist For Slow Performance Of DataPump Export (expdp) And Import (impdp) (Doc ID 453895.1) 
- Parallel Capabilities of Oracle Data Pump 

#logTime Option 
One new parameter introduced in Oracle 12c data pump which is called **logtime**. This is a command-line parameter which will display the messages or status in log with timestamp (time stamped format). This parameter helps the DBA to identify the time taken for each granule of export job. 

There are 4 possible options available for logtime parameter.
*  **NONE** – By default value and it will not show any timestamp
*  **STATUS** – Will display the timestamp for status messages
*  **LOGTIME** – Will display timestamp for log file messages
*  **ALL** – will display timestamp for both status   
```sh
impdp IMPEXP/IMPEXP@POSTBOD3 schemas=C51HITR2 PARALLEL=4 directory=DATA_PUMP_DIR dumpfile=AT_HOST_20141125_4_%U.dmp LOGFILE=4_2.log content=ALL logtime=all
24-JUL-13 16:32:35.300: Starting "SYS"."QUERY_EXPORT":  /******** AS SYSDBA parfile=exp.par
24-JUL-13 16:32:35.412: Estimate in progress using BLOCKS method...
24-JUL-13 16:32:42.715: Processing object type TABLE_EXPORT/TABLE/TABLE_DATA
24-JUL-13 16:33:15.654: Total estimation using BLOCKS method: 109.2 GB
24-JUL-13 16:35:25.113: Processing object type TABLE_EXPORT/TABLE/TABLE
24-JUL-13 16:35:45.230: Processing object type TABLE_EXPORT/TABLE/GRANT/OWNER_GRANT/OBJECT_GRANT
24-JUL-13 16:36:15.370: Processing object type TABLE_EXPORT/TABLE/INDEX/INDEX
24-JUL-13 16:36:39.349: Processing object type TABLE_EXPORT/TABLE/CONSTRAINT/CONSTRAINT
24-JUL-13 16:38:27.765: Processing object type TABLE_EXPORT/TABLE/INDEX/STATISTICS/INDEX_STATISTICS
24-JUL-13 16:38:45.984: Processing object type TABLE_EXPORT/TABLE/CONSTRAINT/REF_CONSTRAINT
24-JUL-13 16:41:35.178: Processing object type TABLE_EXPORT/TABLE/STATISTICS/TABLE_STATISTICS
```
#exclude Option
Enables you to filter the metadata that is exported by specifying objects and object types that you want excluded from the import/export operation.

```
> expdp hr/hr EXCLUDE=INDEX:\"LIKE \'EMP%\'\" DUMPFILE=dpump_dir1:exp.dmp
NOLOGFILE=y
>
> impdp \"sys/****@gansu AS SYSDBA\" schemas=HJLBDEV exclude=TABLE:\"= \'GL_MASTER_222\'\" directory=DATA_PUMP_DIR dumpfile=HJLBDEV_17062014_AllBrn_SetlAcct_BeforeEOP_comp_Dump.dmp logfile=HJLBDEV_17062014_AllBrn_SetlAcct_BeforeEOP_comp_Dump_2.log remap_schema=HJLBDEV:GANSUH REMAP_TABLESPACE=HJLBDEV:GANSUH  
```
