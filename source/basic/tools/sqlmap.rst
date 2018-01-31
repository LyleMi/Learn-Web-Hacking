SQLMap使用
================================

安装 ``git clone https://github.com/sqlmapproject/sqlmap.git sqlmap-dev``

常用参数
--------------------------------

- ``-u`` ``--url`` 指定目标url
- ``-m`` 从文本中获取多个目标扫描
- ``-r`` 从文件中加载HTTP请求
- ``--data`` 以POST方式提交数据
- ``-random-agent`` 随机ua
- ``--user-agent`` 指定ua
- ``--delay`` 设置请求间的延迟
- ``--timeout`` 指定超时时间
- ``--dbms`` 指定db，sqlmap支持的db有MySQL、Oracle、PostgreSQL、Microsoft SQL Server、Microsoft Access、SQLite等
- ``--os`` 指定数据库服务器操作系统
- ``--tamper`` 指定tamper
- ``--level`` 指定探测等级
- ``--risk`` 指定风险等级
- ``--technique`` 注入技术
    - B: Boolean-based blind SQL injection
    - E: Error-based SQL injection
    - U: UNION query SQL injection
    - S: Stacked queries SQL injection
    - T: Time-based blind SQL injection
