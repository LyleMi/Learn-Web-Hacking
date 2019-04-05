SQLMap使用
================================

安装 ``git clone https://github.com/sqlmapproject/sqlmap.git sqlmap``

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


Tamper 速查
--------------------------------

================================            ========================
脚本名称                                    作用
================================            ========================
apostrophemask.py                           用utf8代替引号
equaltolike.py                              like 代替等号
space2dash.py                               绕过过滤'=' 替换空格字符(")，('' - ')后跟一个破折号注释，一个随机字符串和一个新行('\n')
greatest.py                                 绕过过滤'>' ,用GREATEST替换大于号。
space2hash.py                               空格替换为#号 随机字符串 以及换行符
apostrophenullencode.py                     绕过过滤双引号，替换字符和双引号。
halfversionedmorekeywords.py                当数据库为mysql时绕过防火墙，每个关键字之前添加mysql版本评论
space2morehash.py                           空格替换为 #号 以及更多随机字符串 换行符
appendnullbyte.py                           在有效负荷结束位置加载零字节字符编码
ifnull2ifisnull.py                          绕过对 IFNULL 过滤。 替换类似'IFNULL(A, B)'为'IF(ISNULL(A), B, A)'
space2mssqlblank.py                         空格替换为其它空符号
base64encode.py                             用base64编码替换
space2mssqlhash.py                          替换空格
modsecurityversioned.py                     过滤空格，包含完整的查询版本注释
space2mysqlblank.py                         空格替换其它空白符号(mysql)
between.py                                  用between替换大于号(>)
space2mysqldash.py                          替换空格字符(")(' - ')后跟一个破折号注释一个新行(' n')
multiplespaces.py                           围绕SQL关键字添加多个空格
space2plus.py                               用+替换空格
bluecoat.py                                 代替空格字符后与一个有效的随机空白字符的SQL语句。 然后替换=为like
nonrecursivereplacement.py                  取代predefined SQL关键字with表示 suitable for替代(例如 .replace("SELECT"、"")) filters
space2randomblank.py                        代替空格字符("")从一个随机的空白字符可选字符的有效集
sp_password.py                              追加sp_password'从DBMS日志的自动模糊处理的有效载荷的末尾
chardoubleencode.py                         双url编码(不处理以编码的)
unionalltounion.py                          替换UNION ALL SELECT UNION SELECT
charencode.py                               url编码
randomcase.py                               随机大小写
unmagicquotes.py                            宽字符绕过 GPC addslashes
randomcomments.py                           用 ``/**/`` 分割sql关键字
charunicodeencode.py                        字符串unicode编码
securesphere.py                             追加特制的字符串
versionedmorekeywords.py                    注释绕过
space2comment.py                            Replaces space character ``' '`` with comments ``/**/``
================================            ========================
