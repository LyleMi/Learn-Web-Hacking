Database detection
================================

MySQL
--------------------------------
- sleep ``sleep(1)``
- benchmark ``BENCHMARK(5000000, MD5('test'))``
- String connection
- ``SELECT 'a' 'b'``
- ``SELECT CONCAT('some','string')``
- version
- ``SELECT @@version``
- ``SELECT version()``
- Functions for identification
- ``connection_id()``
- ``last_insert_id()``
- ``row_count()``

Oracle
--------------------------------
- String connection
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
- String connection
- ``SELECT 'some'+'string'``
- Constant
- ``@@pack_received``
- ``@@rowcount``

PostgreSQL
--------------------------------
- sleep ``pg_sleep(1)``
