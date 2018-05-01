数据库检测
================================

MySQL
--------------------------------
- sleep ``sleep(1)``
- benchmark ``BENCHMARK(5000000, MD5('test'))``
- 字符串连接 ``select 'a' 'b'``
- version ``SELECT @@version``

Oracle
--------------------------------
- 字符串连接 ``'a'||'oracle' --``
- version ``SELECT banner FROM v$version``

SQLServer
--------------------------------
- WAITFOR ``WAITFOR DELAY '00:00:10';``
- SERVERNAME ``SELECT @@SERVERNAME``
