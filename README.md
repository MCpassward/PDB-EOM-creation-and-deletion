# [ORACLE DATABASE MANAGEMENT SQL COMMANDS FOR PLUGGABLE DATABASE OPERATIONS](https://example.com)


         PDB 1 creation
![pluggable db1](https://github.com/user-attachments/assets/b1666a31-5186-48f8-bd44-485811fffb2f)
       
         PDB 2 creation
![pluggable db2](https://github.com/user-attachments/assets/d7c6477c-503f-41cb-aff4-6561552bfabf)

         PDB2 deletion
![pluggable deletion](https://github.com/user-attachments/assets/d6d8da29-cab6-42e4-bd67-15659e828a23)

## [MY ORACLE ENTERPRISE MANAGEMENT DASHBOARD](https://example.com)
![enyerprise dashboard1](https://github.com/user-attachments/assets/9a458633-4b8b-44f3-9aeb-f243513ed8f0)       
       
![enyerprise dashboard1](https://github.com/user-attachments/assets/bec7ef50-f84b-48c9-b50d-ffb9082f52b3)


##### FOR MORE INFO:
## **Oracle 21c Express Edition: Step-by-Step Guide for Managing Pluggable Databases (PDBs)**



-- Connect to the Oracle database as SYSDBA (superuser privileges)
SQL*Plus: Release 21.0.0.0.0 - Production on Thu Oct 3 13:03:36 2024
Version 21.3.0.0.0

Enter password:

Connected to:
Oracle Database 21c Express Edition Release 21.0.0.0.0 - Production
Version 21.3.0.0.0

-- Connect to the Oracle database as SYSDBA (superuser privileges)
SQL*Plus: Release 21.0.0.0.0 - Production on Thu Oct 3 13:03:36 2024
Version 21.3.0.0.0

Enter password:

Connected to:
Oracle Database 21c Express Edition Release 21.0.0.0.0 - Production
Version 21.3.0.0.0

    SQL> show user;
-- Shows the current user you are logged in as
USER is "SYS"

    SQL> SELECT instance_name FROM v$instance;
 Retrieves the current instance name
 INSTANCE_NAME
----------------
xe



    SQL> show pdbs;
-- Shows pluggable databases (PDBs) and their status (open mode and restriction status)

CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
 2 PDB$SEED                       READ ONLY  NO
 3 XEPDB1                         READ WRITE NO

    SQL> create pluggable database plsql_class2024db
  2  admin user pdbadmin identified by admin
  3  file_name_convert=('C:\APP\USER\PRODUCT\21C\ORADATA\XE\pdbseed',
                        'C:\APP\USER\PRODUCT\21C\ORADATA\XE\plsql_class2024');
-- Creates a new pluggable database (PDB) named 'plsql_class2024db' with a new admin user and specific file name conversion

Pluggable database created.

 
    SQL> alter session set container =plsql_class2024db;
-- Corrects the command by setting the session to the correct container (PDB)

Session altered.

    SQL> alter pluggable database plsql_class2024db open;
-- Opens the newly created pluggable database

Pluggable database altered.

    SQL> alter pluggable database plsql_class2024db save state;
-- Saves the state of the pluggable database to keep it open after the container is restarted

Pluggable database altered.

    SQL> create user ch_plsqlauca identified by chazz;
-- Creates a new user 'ch_plsqlauca' with the password 'chazz'

User created.

    SQL> grant all privileges to ch_plsqlauca;
-- Grants all system privileges to the newly created user

Grant succeeded.

    SQL> show pdbs;
-- Shows the PDBs, including the newly created one 'plsql_class2024db'

CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
   4 PLSQL_CLASS2024DB              READ WRITE NO

    SQL> show con_name;
-- Shows the name of the currently connected PDB (plsql_class2024db)

CON_NAME
------------------------------
PLSQL_CLASS2024DB

    SQL> alter session set container =cdb$root;
-- Switches the session back to the root container (CDB$ROOT)

Session altered.

    SQL> alter session set container =ch_to_delete_pdb;
-- Switches the session to a different PDB (ch_to_delete_pdb)

Session altered.

    SQL> show pdbs;
-- Shows details of all PDBs, including the one to delete

CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
   6 ch_TO_DELETE_PDB               MOUNTED

    SQL> alter session set container=ch_to_delete_pdb;
-- Confirms switching the session to 'ma_to_delete_pdb'

Session altered.

    SQL> alter pluggable database ch_to_delete_pdb open;
-- Opens the pluggable database 'ch_to_delete_pdb'

Pluggable database altered.

    SQL> alter pluggable database ch_to_delete_pdb save state;
-- Saves the state of 'ch_to_delete_pdb' to remain open after restart

Pluggable database altered.

    SQL> show pdbs;
-- Displays the status of PDBs, including 'ch_to_delete_pdb'

 CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
 6 ch_TO_DELETE_PDB               READ WRITE NO

    SQL> alter session set container=cdb$root;
-- Switches back to the root container

Session altered.

    SQL> alter pluggable database ch_to_delete_pdb close immediate;
-- Closes the pluggable database 'ch_to_delete_pdb' immediately

Pluggable database altered.

    SQL> alter pluggable database ch_to_delete_pdb unplug into 
      'C:\app\User\product\21c\admin\XE\dpdump\ch_to_delete_pdb.xml';
-- Unplugs the pluggable database 'ch_to_delete_pdb' and exports its metadata to the specified XML file

Pluggable database altered.

    SQL> drop pluggable database ch_to_delete_pdb including datafile;
-- Drops the pluggable database 'ch_to_delete_pdb' from the container

Pluggable database dropped.
