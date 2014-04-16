---
layout: post
title: Uninstall Oracle DB 12c
category: oracle
tag: [oracle, ops]

---



# uninstall oracle DB 12c on linux

```sh
[oradb@infbjvm10 deinstall]$  cd ${oracle_home}/deinstall
[oradb@infbjvm10 deinstall]$  ./deinstall
Checking for required files and bootstrapping ...
Please wait ...
Location of logs /tmp/deinstall2014-04-02_10-43-53AM/logs/

############ ORACLE DEINSTALL & DECONFIG TOOL START ############


######################### CHECK OPERATION START #########################
## [START] Install check configuration ##


Checking for existence of the Oracle home location /oracle/product/12.1/db
Oracle Home type selected for deinstall is: Oracle Single Instance Database
Oracle Base selected for deinstall is: /oracle
Checking for existence of central inventory location /oracle/oraInventory
Checking for sufficient temp space availability on node(s) : 'infbjvm10.cn.oracle.com'

## [END] Install check configuration ##


Network Configuration check config START

Network de-configuration trace file location: /tmp/deinstall2014-04-02_10-43-53AM/logs/netdc_check2014-04-02_10-47-11-AM.log

Specify all Single Instance listeners that are to be de-configured [LISTENER]:LISTENER

Network Configuration check config END

Database Check Configuration START

Database de-configuration trace file location: /tmp/deinstall2014-04-02_10-43-53AM/logs/databasedc_check2014-04-02_10-49-06-AM.log

Use comma as separator when specifying list of values as input
```


```sh

Specify the list of database names that are configured in this Oracle home [test]: test
```

```sh
###### For Database 'test' ######

Specify the type of this database (1.Single Instance Database|2.Oracle Restart Enabled Database) [1]: 1
Specify the diagnostic destination location of the database [/oracle/diag/rdbms/test]: /oracle/diag/rdbms/test
Specify the storage type used by the Database ASM|FS []:
Specify the storage type used by the Database ASM|FS []:
```

```sh
Specify the storage type used by the Database ASM|FS []: FS
```

```sh
Specify the list of directories if any database files exist on a shared file system. If 'test' subdirectory is found, then it will be deleted. Otherwise, the specified directory will be deleted. Alternatively, you can specify list of database files with full path [ ]:
```
```sh
Specify the fast recovery area location, if it is configured on the file system. If 'test' subdirectory is found, then it will be deleted. []:
```

```sh
Specify the database spfile location [ ]:
```

```sh
Database Check Configuration END
Oracle Configuration Manager check START
OCM check log file location : /tmp/deinstall2014-04-02_10-43-53AM/logs//ocm_check8585.log
Oracle Configuration Manager check END

######################### CHECK OPERATION END #########################


####################### CHECK OPERATION SUMMARY #######################
Oracle Home selected for deinstall is: /oracle/product/12.1/db
Inventory Location where the Oracle home registered is: /oracle/oraInventory
Following Single Instance listener(s) will be de-configured: LISTENER
The following databases were selected for de-configuration : test
Database unique name : test
Storage used : FS
Checking the config status for CCR
Oracle Home exists with CCR directory, but CCR is not configured
CCR check is finished
Do you want to continue (y - yes, n - no)? [n]: y

Exited from program.

############# ORACLE DEINSTALL & DECONFIG TOOL END #############

[oradb@infbjvm10 deinstall]$  ./deinstall
Checking for required files and bootstrapping ...
Please wait ...
Location of logs /tmp/deinstall2014-04-02_10-54-59AM/logs/

############ ORACLE DEINSTALL & DECONFIG TOOL START ############


######################### CHECK OPERATION START #########################
## [START] Install check configuration ##


Checking for existence of the Oracle home location /oracle/product/12.1/db
Oracle Home type selected for deinstall is: Oracle Single Instance Database
Oracle Base selected for deinstall is: /oracle
Checking for existence of central inventory location /oracle/oraInventory
Checking for sufficient temp space availability on node(s) : 'infbjvm10.cn.oracle.com'

## [END] Install check configuration ##


Network Configuration check config START

Network de-configuration trace file location: /tmp/deinstall2014-04-02_10-54-59AM/logs/netdc_check2014-04-02_10-55-56-AM.log

Specify all Single Instance listeners that are to be de-configured [LISTENER]:LISTENER

Network Configuration check config END

Database Check Configuration START

Database de-configuration trace file location: /tmp/deinstall2014-04-02_10-54-59AM/logs/databasedc_check2014-04-02_10-56-27-AM.log

Use comma as separator when specifying list of values as input

Specify the list of database names that are configured in this Oracle home [test]: test

###### For Database 'test' ######

Specify the type of this database (1.Single Instance Database|2.Oracle Restart Enabled Database) [1]: 1
Specify the diagnostic destination location of the database [/oracle/diag/rdbms/test]: /oracle/diag/rdbms/test
Specify the storage type used by the Database ASM|FS []:FS

Specify the list of directories if any database files exist on a shared file system. If 'test' subdirectory is found, then it will be deleted. Otherwise, the specified directory will be deleted. Alternatively, you can specify list of database files with full path [ ]:

Specify the fast recovery area location, if it is configured on the file system. If 'test' subdirectory is found, then it will be deleted. []:

Specify the database spfile location [ ]:

Database Check Configuration END
Oracle Configuration Manager check START
OCM check log file location : /tmp/deinstall2014-04-02_10-54-59AM/logs//ocm_check435.log
Oracle Configuration Manager check END

######################### CHECK OPERATION END #########################


####################### CHECK OPERATION SUMMARY #######################
Oracle Home selected for deinstall is: /oracle/product/12.1/db
Inventory Location where the Oracle home registered is: /oracle/oraInventory
Following Single Instance listener(s) will be de-configured: LISTENER
The following databases were selected for de-configuration : test
Database unique name : test
Storage used : FS
Checking the config status for CCR
Oracle Home exists with CCR directory, but CCR is not configured
CCR check is finished
Do you want to continue (y - yes, n - no)? [n]: y
A log of this session will be written to: '/tmp/deinstall2014-04-02_10-54-59AM/logs/deinstall_deconfig2014-04-02_10-55-55-AM.out'
Any error messages from this session will be written to: '/tmp/deinstall2014-04-02_10-54-59AM/logs/deinstall_deconfig2014-04-02_10-55-55-AM.err'

######################## CLEAN OPERATION START ########################
Database de-configuration trace file location: /tmp/deinstall2014-04-02_10-54-59AM/logs/databasedc_clean2014-04-02_10-57-46-AM.log
Database Clean Configuration START test
This operation may take few minutes.
Database Clean Configuration END test

Network Configuration clean config START

Network de-configuration trace file location: /tmp/deinstall2014-04-02_10-54-59AM/logs/netdc_clean2014-04-02_10-59-31-AM.log

De-configuring Single Instance listener(s): LISTENER

De-configuring listener: LISTENER
    Stopping listener: LISTENER
    Warning: Failed to stop listener. Listener may not be running.
    Deleting listener: LISTENER
    Listener deleted successfully.
Listener de-configured successfully.

De-configuring Naming Methods configuration file...
Naming Methods configuration file de-configured successfully.

De-configuring backup files...
Backup files de-configured successfully.

The network configuration has been cleaned up successfully.

Network Configuration clean config END

Oracle Configuration Manager clean START
OCM clean log file location : /tmp/deinstall2014-04-02_10-54-59AM/logs//ocm_clean435.log
Oracle Configuration Manager clean END
Setting the force flag to false
Setting the force flag to cleanup the Oracle Base
Oracle Universal Installer clean START

Detach Oracle home '/oracle/product/12.1/db' from the central inventory on the local node : Done

Delete directory '/oracle/product/12.1/db' on the local node : Done

Delete directory '/oracle/oraInventory' on the local node : Done

Failed to delete the directory '/oracle'. The directory is in use.
Delete directory '/oracle' on the local node : Failed <<<<

Oracle Universal Installer cleanup completed with errors.

Oracle Universal Installer clean END


## [START] Oracle install clean ##

Clean install operation removing temporary directory '/tmp/deinstall2014-04-02_10-54-59AM' on node 'infbjvm10'

## [END] Oracle install clean ##


######################### CLEAN OPERATION END #########################


####################### CLEAN OPERATION SUMMARY #######################
Successfully de-configured the following database instances : test
Following Single Instance listener(s) were de-configured successfully: LISTENER
Cleaning the config for CCR
As CCR is not configured, so skipping the cleaning of CCR configuration
CCR clean is finished
Successfully detached Oracle home '/oracle/product/12.1/db' from the central inventory on the local node.
Successfully deleted directory '/oracle/product/12.1/db' on the local node.
Successfully deleted directory '/oracle/oraInventory' on the local node.
Failed to delete directory '/oracle' on the local node.
Oracle Universal Installer cleanup completed with errors.


Run 'rm -rf /etc/oraInst.loc' as root on node(s) 'infbjvm10' at the end of the session.

Run 'rm -rf /opt/ORCLfmap' as root on node(s) 'infbjvm10' at the end of the session.
Run 'rm -rf /etc/oratab' as root on node(s) 'infbjvm10' at the end of the session.
Oracle deinstall tool successfully cleaned up temporary directories.
#######################################################################


############# ORACLE DEINSTALL & DECONFIG TOOL END #############

```
