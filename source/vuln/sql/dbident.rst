数据库检测
================================

MySQL
--------------------------------
- sleep ``sleep(1)``
- benchmark ``BENCHMARK(5000000, MD5('test'))``
- 字符串连接
    - ``SELECT 'a' 'b'``
    - ``SELECT CONCAT('some','string')``
- version 
    - ``SELECT @@version``
    - ``SELECT version()``
- 识别用函数
    - ``connection_id()``
    - ``last_insert_id()``
    - ``row_count()``

Oracle
--------------------------------
- 字符串连接 
    - ``'a'||'oracle' --``
    - ``SELECT CONCAT('some','string')``
- version 
    - ``SELECT banner FROM v$version``
    - ``SELECT banner FROM v$version WHERE rownum=1``

SQLServer
--------------------------------
- WAITFOR ``WAITFOR DELAY '00:00:10';``
- SERVERNAME ``SELECT @@SERVERNAME``
- version ``SELECT @@version``
- 字符串连接
    - ``SELECT 'some'+'string'``
- 常量
    - ``@@pack_received``
    - ``@@rowcount``

PostgreSQL
--------------------------------
- sleep ``pg_sleep(1)``
